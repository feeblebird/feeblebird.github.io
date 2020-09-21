---
title: XMLStudy
date: 2020-09-20 09:24:05
tags: XML
categories: XML
---

# XML Documents start the document with a declaration, surrounded by \<?xml ... ?\>

\<?xml version = "1.0" encoding = "utf-8" ?>



# XML区分大小写，不同余html

```xml
<?xml version = "1.0" encoding = "utf-8" ?>
<BARS>
    <BAR>
        <name>joe's bar</name>
        <beer>
            <name>bud</name>
            <price>2.50</price>
        </beer>
        <beer>
            <name>miller</name>
            <price>3.00</price>
        </beer>
    </BAR>
    <BAR>
        ...
    </BAR>
</BARS>
```

```xml
<?xml version = "1.0" encoding = "utf-8" ?>
<bars>
	<bar name = "joe's bar">
    	<beer name = "bud" price = 2.50/>
        <beer name = "miller" price = 3.00/>
    </bar>
    <bar>
    	...
    </bar>
</bars>
```

