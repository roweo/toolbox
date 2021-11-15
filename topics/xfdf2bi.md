---
title: xfdf2bi
date: 2021-11-15
draft: true
keyword: 
    - XSLT
    - PDF
---

# XFDF2BI XSLT

## Purpose

The XSLT transforms PDF xfdf data to a regular XML format

For `data/@id`, it's a copy of f/@href at the moment. You can change this with your own function in `<data id="{ /*/f/@href }">`.

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet
	xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
	xmlns:xs="http://www.w3.org/2001/XMLSchema"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:mf="http://www.mekon.com/functions"
	xpath-default-namespace="http://ns.adobe.com/xfdf/"
	exclude-result-prefixes="#all"
	version="2.0">
	
	<xsl:output
		method="xml"
		encoding="UTF-8"
	/>
	
	<xsl:template match="/">
		<data id="{ /*/f/@href }">
			<xsl:apply-templates select="//field"/>
		</data>
	</xsl:template>				
	
	<xsl:template match="field">
		<field>
			<key>
				<xsl:value-of select="@name"/>
			</key>
			<xsl:apply-templates select="value"/>
		</field>
	</xsl:template>

	<xsl:template match="value">
		<value>
			<xsl:value-of select="."/>
		</value>
	</xsl:template>

</xsl:stylesheet>
```
