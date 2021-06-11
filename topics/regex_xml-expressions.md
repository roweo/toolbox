# XML specific expressions {#xml-specific .reference}

OxygenXML allows to constrain your expressions to your DITA structure using the XML query language XPath. This allows you to create expressions that are constrained to the structures that you define.

**Warning:** Regular expressions by themselves \(without XPATH constraints\), are unaware of XML structure and can invalidate your structure very quickly.

## Remove extra spaces from a specific tag {#remove-extra-spaces-from-a-specific-tag .section}

Within OxygenXML **Find/Replace** using **XPath:** `//p/text()`(replace "p" with any other tag name). This limits the search to the text node of the p element.

| Find      | Replace |
| --------- | ------- |
| `(\s)\s+` | `$1`    |

**Related information**  

[https://en.wikipedia.org/wiki/XPath](https://en.wikipedia.org/wiki/XPath)
