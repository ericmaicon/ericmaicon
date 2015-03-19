title: "SQL To export Manufacturer from Presta shop"
date: 2015-02-16 22:56:59
categories:
- Presta Shop
tags:
- Presta Shop
---
![Presta Shop](/thumbnails/prestashop.jpg)

Here you can see another simple SQL that may help you to export some data from Presta Shop to do whatever you want.

```SQL
SELECT ps_manufacturer.id_manufacturer
      ,ps_manufacturer.name
      ,concat("http://xxxx.com/img/tmp/manufacturer_mini_", ps_manufacturer.id_manufacturer, ".jpg")
FROM ps_manufacturer
ORDER BY 1
```

**Remember to change the URL inside of the SQL to your Presta Shop URL**