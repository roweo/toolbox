# VS Code snippets

## Samples

### Create table

```
// Create table

    	"Create Markdown pipetable 2x2": {
		"prefix": "table 2x2",
		"body": [
		  "| $1    |     |",
		  "| --- | --- |",
		  "|     |     |",
		  "|     |     |",
		  "",
		  ": ${TM_SELECTED_TEXT:Caption}"
		],
		"description": "Create Markdown pipetable 2x2"
	  },
	  "Create Markdown pipetable 3x3": {
		"prefix": "table 3x3",
		"body": [
		  "| $1    |     |     |",
		  "| --- | --- | --- |",
		  "|     |     |     |",
		  "|     |     |     |",
		  "|     |     |     |",
		  "",
		  ": ${TM_SELECTED_TEXT:Caption}"
		],
		"description": "Create Markdown pipetable 3x3"
	  },
	"Create Markdown pipetable 4x4": {
		"prefix": "table 4x4",
		"body": [
		  "| $1    |     |     |     |",
		  "| --- | --- | --- | --- |",
		  "|     |     |     |     |",
		  "|     |     |     |     |",
		  "|     |     |     |     |",
		  "|     |     |     |     |",
		  "",
		  ": ${TM_SELECTED_TEXT:Caption}"
		],
		"description": "Create Markdown pipetable 4x4"
	  },
	  
```

## Create footnote

```
       "Create footnote": {
		"prefix": "fn",
		"body": [
		  "^[${TM_SELECTED_TEXT:footnote}]"
		],
		"description": "Create footnote"
	  }
```	  

### Create YAML Header

```	
	"Create YAML Header": {
		"prefix": "header",
		"body": [
			"---",
			"title: ${TM_FILENAME_BASE/([^\\s]*) ([^\\.]*)/$2/}",
			"date: $CURRENT_YEAR-$CURRENT_MONTH-$CURRENT_DATE",
            "author: Owen Rowe",			
			"---",
			"",
			"# ${TM_FILENAME_BASE/([^\\s]*) ([^\\.]*)/$2/}"
            "",
            "## $0",            
		],
		"description": "Create YAML Header"
	},

```

### Add TM block

```
	"Add TM block": {
		"prefix": "TM",
		"body": [
            "",			
			"::: tm",
			"${1:prodName}® is a registered trademark of ${2:companyName}",
			":::",
            ""			
		],
		"description": "Add TM block"
	},
	
```

### Create div

```
	"Create new div": {
		"prefix": "div",
		"body": [
			"",
			"::: ${1:class}",
			"${TM_SELECTED_TEXT:content}",
			":::",
			""
		],
		"description": "Create new div"
	},

```

### Create style block

```
	"Create custom style block": {
		"prefix": "style (block)",
		"body": [
		  "",
		  "::: {custom-style=\"${1:style-name}\" .${2:class}}",
		  "${TM_SELECTED_TEXT}",
		  ":::",
		  ""
		],
```

### Create inline style

```
"Create custom style span": {
		"prefix": "style (inline)",
		"body": [
		  "[${TM_SELECTED_TEXT:content}]{custom-style=\"${1:style-name}\"}"
		],
		"description": "Create custom style span"
	  }
```	  

### TEAMS chat link

```
	"TEAMS chat link": {
		"prefix": "teams chat",
		"body": [
			"https://teams.microsoft.com/l/chat/0/0?users=owen_rowe@baxter.com"
		],
		"description": "TEAMS chat link"
	},
```

### Add video tag

```
	"Add video html tag": {
		"prefix": "video",
		"body": [
		  "<video src=\"${TM_SELECTED_TEXT:href}\" controls>${1:description}</video>"
		],
		"description": "Add video tag"
	  },

```

### Solve with scientific method

```
"Solve with scientific method": {
		"prefix": "problem",
		"body": [
		  "---",
		  "title: ${TM_FILENAME_BASE/([^\\s]*) ([^\\.]*)/$2/}",
		  "author: Owen Rowe",
		  "date: $CURRENT_YEAR-$CURRENT_MONTH-$CURRENT_DATE",
		  "keyword:",
		  "  - problem",
		  "---",
		  "",
		  "# ${1:Title}",
		  "",
		  "## Statement of the problem",
		  "",
		  "${2:Problem}",
		  "",
		  "## Hypotheses as to the cause of the problem",
		  "",
		  "1. $0",
		  "",
		  "## Experiments designed to test each hypothesis",
		  "",
		  "1. ",
		  "",
		  "## Predicted results of the experiments",
		  "",
		  "## Observed results of experiments",
		  "",
		  "## Conclusions from the result of the experiments",
		  ""
		],
		"description": "Solve with scientific method"
	  },
	  "Today's date": {
		"prefix": "date",
		"body": [
		  "$CURRENT_YEAR-$CURRENT_MONTH-$CURRENT_DATE $0"
		],
		"description": "Today's date"
	  }
}
```
