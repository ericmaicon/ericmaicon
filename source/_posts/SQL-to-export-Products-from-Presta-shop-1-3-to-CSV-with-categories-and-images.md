title: "SQL to export Products from Presta shop 1.3.* to CSV with categories and images"
date: 2015-02-16 22:56:40
categories:
- Presta Shop
tags:
- Presta Shop
---
![Presta Shop](/thumbnails/prestashop.jpg)

A customer requested from me to update his Presta shop version. Since he had an old version, it was not possible. So I needed to install a new version and import everything from one to another. To do so, I did this SQL. It may be useful to you, feel free to use it:

```SQL
SELECT ps_product.id_product as id,
       replace(ps_product_lang.name, '"','''') as nome,
       ifnull((select ps_category_lang.name
          from ps_category
          join ps_category_lang on ps_category_lang.id_category = ps_category.id_category
                               and ps_category_lang.id_lang = 3
          join ps_category_product on ps_category_product.id_category = ps_category.id_category
         where ps_category_product.id_product = ps_product.id_product
         limit 1),'') as categoria,
       ps_product.price as preco_atacado,
       ps_product.reduction_price as qtde_desconto,
       ps_product.reduction_percent as percentual_desconto,
       ps_product.reduction_from as desconto_de,
       ps_product.reduction_to as desconto_ate,
       ps_product.reference as referencia,
       ps_product.supplier_reference as fornecedor_Referencia,
       ifnull(ps_supplier.name, '') as fornecedor,
       ifnull(ps_manufacturer.name, '') as fabricante,
       ps_product.weight as peso,
       ps_product.quantity as qtde,
       replace(ps_product_lang.description_short, '"','''') as breve_descricao,
       replace(ps_product_lang.description, '"','''') as descricao,
       replace(ps_product_lang.meta_title, '"','''') as meta_titulo,
       replace(ps_product_lang.meta_keywords, '"','''') as meta_palavra_chave,
       replace(ps_product_lang.meta_description, '"','''') as meta_descricao,
       ps_product_lang.link_rewrite as url_reescrita,
       (select GROUP_CONCAT(concat('http://xxx.com.br/loja/img/p/', ps_product.id_product, '-' , ps_image.id_image, '.jpg') SEPARATOR ','  )
          from ps_image
         where ps_image.id_product = ps_product.id_product)
FROM ps_product
JOIN ps_product_lang ON ps_product_lang.id_product = ps_product.id_product
                               and ps_product_lang.id_lang = 3
LEFT JOIN ps_supplier ON ps_supplier.id_supplier = ps_product.id_supplier
LEFT JOIN ps_manufacturer ON ps_manufacturer.id_manufacturer = ps_product.id_manufacturer
WHERE ps_product.active = 1
ORDER BY 2
```