# DOCX2MD Converter

This Bash script is intended to prepare Baxter CCDS word files for DITA conversion.

## Dependencies: 

- [PANDOC](https://pandoc.org/installing.html)
- [BASH](https://git-scm.com/downloads)

*Note: Ensure PATH variables for PANDOC are set*

It does the following:
1. Creates a folder named output (if it doesn't already exist)
1. Runs PANDOC conversion to Markdown (incl. extensions for: extracting media, pipetables and atx-header)
1. Runs a series of GREP operations to tidy and/or mark text for further work
1. Moves extracted media from default 'media' to 'images' folder
  
 Following the use of this script, it's expected that you will use a tool (e.g. OxgyenXML) to convert the Markdown output to DITA XML. 

``` bash
# DOCX2MD Converter
# by Owen Rowe 2021

# Create folder

if [ ! -d "output" ]; then
    mkdir output
fi

# Declare variables
declare path="output"
declare ofile="output.md"

# With any DOCX found, convert to Markdown

for filename in *.docx
do
	pandoc -f docx -t commonmark-pipe_tables --wrap=none --extract-media=$path --markdown-headings=atx $filename -o $ofile  
done

# Normalise titles -> titlecase - needs work
# sed -i 's/#\s.*/\L&/; s/#.*[a-z]/\u&.*/g' $path/$ofile
# sed -i -E 's|(^#.*)|\L\1|;s|^(#\s*)([a-z])([^\s*) ([a-z])|\1\u\2\3\u\4|g'
# sed -i '1s#/sh$#/bash#' ftc.sh

# GREP deletions
sed -i -E 's|<!-- -->||;s|^[ \t]+<|<|' $ofile

# GREP fix image links
sed -i -E 's|output/media/|images/|g' $ofile

# Fix block quotes
sed -i -E 's|^>\s?||' $ofile

# Fix Topic IDs
#sed -i -E 's|'

# Fix bullet characters
sed -i -E 's|•|-|' $ofile 

# Strip Heading Style from Table titles 

# Fix level 1 headers
sed -i -E 's|^(# )(.*)|\U\1\2|' $ofile

# Normalise element text
sed -i -r -E 's|(</?)([^>]*)(>)|\1\L\2\E\3|g' $ofile

# Keyref instances of "[Product]"
sed -i -r -E 's|\\\[[Pp]roduct\\\]|<ph keyref="product_name"\/>|g' $ofile

# Fix newline at titles <=== DOES NOT WORK
# grep -P -e 's|\*\*\s+[\r\n]{1,2}*|BOSS|' $ofile

# Highlight for clean up 'See Section XX?.X?' text.
sed -i -E 's|\\?\[?\(([Ss]ee [Ss]ection [[:digit:]][[:digit:]]?\.?[[:digit:]]?[^\n\(\)]*)\)\\?\]?|<required-cleanup remap="xref">\1</required-cleanup>|g' $ofile

# Highlight footnotes for cleanup
sed -i -r 's|^\\\*{1,2}(\s?[^\n]*)|<required-cleanup remap="footnote">\1</required-cleanup>|' $ofile

# Set mandatory <p> tag on bolded content
sed -i -r 's|^(-)?\s+?\*\*(.*)\*\*|\1 <p outputclass="mandatory">\2</p>|;s|\*\*||g' $ofile

# Convert RA comments to <draft-comment> tag
sed -i -E 's|\\\[([^\\]*)\\\]|<draft-comment author="admin">\1</draft-comment>|' $ofile

# Fix extraneous indents and header styles before tags(#)
sed -i -r -E 's|^[# ]*(<)|\1|' $ofile

# Flag <sup> tag for required-cleanup @footnote
sed -i -E 's|^\*{0,2}?(<sup>.{1,4}</sup>\s?[^\n\*]*)\*{0,2}?\.?|<required-cleanup remap="footnote">\1</required-cleanup>|' $ofile

# Fix sections
#sed -i -r -E 's|^<u>(.*)</u>$|#### \1 {.section}|' $ofile

# Fix extraneous indents and header styles on empty lines
sed -i -r -E 's|^[# ]*$||' $ofile

# Strip blockquotes
sed -i -E 's|</?blockquote>||g' $ofile

# MODULES remove hash (#) on script (sed) lines to activate
# ====================================================
# Triple chamber bags
# sed -i -E -f resources/3Cbags.txt $ofile

# Splitter function (not generally required since Oxygen can do this better See: Refactoring>Convert Nested Topics to New Topics)
# csplit $path/$ofile '/^# /' {*} --suffix-format="%d.md" -f $path/section

# Move images 
mv $path/media $path/images

```
