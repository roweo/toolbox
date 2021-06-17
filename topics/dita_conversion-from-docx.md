# Word to DITA \(via MarkDown\) {#convert-docx-to-dita}

It is difficult to predict how well a conversion will go, but we can alleviate some known problems by starting with a well formatted Word doc - failing that, we can construct regular expressions to identify and correct problems in the MarkDown text. MarkDown is used here as a stepping stone to full `XML`.

Word document preparation:

-   Complex tables \(merged/joined cells, etc.\) can be problematic - can they be simplified?
-   Styles should be used consistently - heading progression is important \(you cannot skip heading levels e.g. **Heading 1** \> **Heading 4**\)
-   Optional flags include: `-raw_html` & `--extract-media`

**Important:** Pandoc is needed for Step 2 \(see [Pandoc](https://pandoc.org/index.html)\)

1.  Start with a `.docx` file, if you try to use `.doc`, the conversion will fail. Resave any `.doc` files to `.docx`\)

2.  Using Pandoc \(via commmandline\), convert `.docx` to CommonMark with extensions --atx-headers & --wrap=none options\) *NB: replace \[\]*.

    ```
    pandoc -f docx -t commonmark --wrap=none --markdown-headings=atx [input_filename.docx] -o [output_filename.md]
    ```

3.  With the generated MarkDown file, process any text artifacts in a suitable text file editor \(e.g. using any appropriate Regex\)

4.  Test the MarkDown document for DITA compliance within OxygenXML \(i.e.*does it render to DITA?*\)

5.  Using context menu \(right click\) **Export as DITA topic**

6.  Save as DITA file

7.  Create a new DITAMAP and associate the DITA file to the map.

8.  Using XML Refactoring to **Convert nested topics to new topics**

9.  Arrrange your topics appropriately and tidy up!


**Related information**  


[Markdown Syntax Reference](https://github.com/jelovirt/dita-ot-markdown/wiki/Syntax-reference)

[Learn Markdown](https://commonmark.org/help/)
