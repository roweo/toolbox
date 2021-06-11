# XML-capable editors {#configuring-vs-code-as-an-authoring-tool}

Source code editors are generally intended for a broader use case and are consequently not focused specifically on DITA XML, they can however be a powerful low/no cost option.

Source code editors can be configured to comply with the rules of the DITA schema.

## Configuring VS Code as an authoring tool { .section}

**Important:** Before proceeding, the following should be installed and up-to-date: [DITA Open Toolkit](https://www.dita-ot.org/) and [Java](https://www.oracle.com/java/technologies/javase-downloads.html).

1.  Download and install VS Code [https://code.visualstudio.com/](https://code.visualstudio.com/)

2.  Install extension: [XML Language Support by Red Hat](https://marketplace.visualstudio.com/items?itemName=redhat.java)


**Configure VS Code**

VS Code is not a DITA specific editor, but it can be configured to validate DITA XML by editing the `settings.json` file.

1.  Open **Command Palette** by pressing Ctrl + Shift + P

    1.  Type **Open Settings \(JSON\)** to directly edit the settings JSON file.

    2.  Type **Open Settings \(UI\)** to open a UI to edit the settings JSON file indirectly.

2.  Set the following \[replace with your local paths\]:


```json
       "xml.catalogs": [
       "[path to dita-ot-version]\\catalog-dita.xml"
       ],
       "xml.java.home": "[path to Java]\\Java\\jre1.8.0_251",
       "xml.validation.resolveExternalEntities": true
```

**Note:** Backslashes are escaped by *an additional slash* in the settings file '\\' = '\\\\'

To inspect whether your DITA XML document is valid \(or receive suggested fixes for invalid markup\), open the **Problems** view by pressing Ctrl + Shift + M

**Parent topic:**[XML Authoring](../topics/xml_authoring.md)
