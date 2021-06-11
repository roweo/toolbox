# General expressions {#general-expressions .reference}

CAUTION:

these are only *lightly* tested - be sure to confirm you have the desired result before proceeding further.

## Convert `[PRODUCT]` to DITA key {#convert-product-to-dita-key .section}

|             Find              |     Replace      |
| :---------------------------: | :--------------: |
| `\\\[(PRODUCT\|Product])\\\]` | `[product_name]` |

## Convert RA style comments to draft comments: {#convert-ra-style-comments-to-xml-style-comments .section}

|        Find        |                Replace                |
| :----------------: | :-----------------------------------: |
| `\\\[([^\\]*)\\\]` | `<draft-comments>$1</draft-comments>` |

## Convert RA style conditions to DITA element for later clean up {#convert-ra-style-conditions-to-dita-element-for-later-clean-up .section}

|        Find        |                  Replace                  |
| :----------------: | :---------------------------------------: |
| `\\\<([^\\]*)\\\>` | `<required-cleanup>$1</required-cleanup>` |

## Standardise to capitals on Titles `(#->####)` {#standardise-to-capitals-on-titles-- .section}

*NB: works in Notepad++, **does not** work in JAVA Regex \(e.g. OxygenXML\)*

|       Find        | Replace  |
| :---------------: | :------: |
| `^(#{1,4}\s)(.+)` | `$1\U$2` |

## Capitals to title case {#capitals-to-title-case .section}

|         Find         |   Replace    |
| :------------------: | :----------: |
| `(#[ ]*)([A-Z])(.+)` | `$1\U$2\L$3` |

## Find trailing spaces after \* and \*\* \(a Word conversion gotcha - can affect bold and italics\) {#find-trailing-spaces-after--and--a-word-conversion-gotcha---can-affect-bold-and-italics .section}

|                                      Find                                       | Replace  |
| :-----------------------------------------------------------------------------: | :------: |
| `((?<=\s)\|(?<=^))(\*+[\w !"\#$%&'()+,\-./:;<=>?@\[\\\]^_{\|}~]+)(\s+)(\*+) \|` | `$2$4$3` |

## Find extra spaces in lists \(ensure a single \[space\] occurs at the end of the replace expression\). {#find-extra-spaces-in-lists .section}

|   Find   | Replace |
| :------: | :-----: |
| `\n-\s+` | `\n- `  |

## Tidies superfluous carriage returns. {#tidies-superfluous-carriage-returns .section}

Find a newline *not* after a period, followed by 2 \(or more\) spaces and preceding one lowercase letter, number, or "\(". Remove newline, trim to one \(1\) space. \*NB: not fully supported by all Regex engines \(works for Oxygen though\)

|                  Find                   | Replace |
| :-------------------------------------: | :-----: |
| `(?!<=\.)\n^(\s){2,}(?=\p{Ll}\|\d\|\()` |  `$1`   |

## Find asterisks in text and leave a comment for a fix \(will drop a comment on the line above the "\*"\) {#adjust-section-tags .section}

|    Find     |                       Replace                        |
| :---------: | :--------------------------------------------------: |
| `(^.*\\\*)` | `<draft-comment>Clean up needed</draft-comment>\n$1` |

## Find newline followed by a lower case \(a-z\) letter \(note space before `[space]$1` in Replace expression\) {#remove-extraneous-returns .section}

|        Find        | Replace |
| :----------------: | :-----: |
| `(?<=\w)\n^([\w])` |  `$1`   |

## Find `**Notes**` \(or similar\) and convert to DITA compliant tags \(esp. device labels\) {#refactor-notes .section}

|           Find           |      Replace      |
| :----------------------: | :---------------: |
| `\*\*NOTE:\*\* ([^\n]*)` | `<note>$1</note>` |

## Find codeblocks "\>" before an image \(leave replace query blank\) {#section_nky_mmf_ynb .section}

|     Find     |  Replace  |
| :----------: | :-------: |
| `^\> (?=\!)` | `[blank]` |

## Adjust table header row of table {#adjust-table-header-row-of-table .section}

Captures content after the `table` tag up to the end of the next `tr` tag. Replaces the first `tbody` tag with `thead`; appends closing `thead` and reopens `tbody` at this new position.

|                     Find                      |              Replace               |
| :-------------------------------------------: | :--------------------------------: |
| `((?<=<table>)[^<]*)(<tbody>)(.*?(?<=</tr>))` | `$1<thead>$3\r\<\thead\>\<tbody\>` |

## Find/replace `codeph` elements that can be specialised to `xmlatt` or `xmlelement` { .section}

|                   Find                   |            Replace            |
| :--------------------------------------: | :---------------------------: |
|       `<codeph>@([^<]*)</codeph>`        |     `<xmlatt>$1</xmlatt>`     |
| `<codeph>&lt;\/?([^\\\>]*)\\?></codeph>` | `<xmlelement>$1</xmlelement>` |

## Convert bolded titles to markdown style { .section}

Finds single line bolded strings starting with a digit and prepends with markdown style header symbol i.e. \#

|                    Find                     |   Replace   |
| :-----------------------------------------: | :---------: |
|        `\*\*(\d\d?\.?\s)([^*]*)\*\*`        |  `## $1$2`  |
|      `\*\*(\d\d?\.\d\d?\s)([^*]*)\*\*`      | `### $1$2`  |
| `\*\*(\d\d?\.\d\d?\.\d\d?\.?\s)([^*]*)\*\*` | `#### $1$2` |

## Create IDs for Headers { .section}

|                    Find                     |     Replace      |
| :-----------------------------------------: | :--------------: |
| `^(#+\s[0-9.]*)([^A-Z]+)([\w -,/]*(?!\{)$)` | `$1$2$3 {#\L$3}` |
|     `(?<=\{#)(.*?)[^a-z\-]+(.*?)(?=\})`     |     `$1-$2`      |
|                                             |                  |

## Convert HTML style img tags to Markdown images {#section_kjt_vmb_lpb .section}

|           Find            |  Replace  |
| :-----------------------: | :-------: |
| `<img src=("[^"]*").+?/>` | `![]($1)` |
|                           |           |

## Create h5 sections { .section}

|         Find          |  Replace   |
| :-------------------: | :--------: |
| `\[([^\]]*)\]\{.ul\}` | `##### $1` |

**Parent topic:** [Regular Expressions](../topics/regex.md)
