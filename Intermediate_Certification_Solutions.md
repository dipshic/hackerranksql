**Solutions for Hackerrank Intermediate SQL Certifications**

## 1. Product Sales Per City
```
SELECT t1.city_name,t5.product_name,
round(sum(t4.line_total_price) over(partition by t4.product_id,t1.id),2) as amount_spent
FROM invoice_item t4
LEFT JOIN product t5 ON t4.product_id = t5.id
LEFT JOIN invoice t3 ON t4.invoice_id = t3.id
LEFT JOIN customer t2 ON t3.customer_id = t2.id
LEFT JOIN city t1 ON t2.city_id = t1.id
ORDER by amount_spent DESC,
t1.city_name ASC,t5.product_name ASC
```
