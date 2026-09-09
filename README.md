# Olist Order Time Analysis

## السؤال
في أي ساعة يوماً تصل الطلبات لذروتها، ولو الأمر يختلف باختلاف الفصل؟

## الطريقة
استخراج ساعة كل طلب من timestamp، تجميع حسب الفصل والساعة، وترتيب النتائج لإيجاد أعلى ساعة بكل فصل.

## النتيجة
| الفصل | ساعة الذروة (UTC) |
|---|---|
| الصيف | 16 |
| الربيع | 16 |
| الشتاء | 14 |
| الخريف | 13 |

## التوصية
- الصيف والربيع: تركيز الحملات الإعلانية والعروض حوالي الساعة 16
- الشتاء والخريف: الذروة أبكر (14 و13) - يجب إطلاق العروض أبكر بهذين الفصلين
- تنويه: التوقيت غالباً UTC وليس التوقيت المحلي للبرازيل

## SQL Queries المستخدمة

### الصيف (يونيو، يوليو، أغسطس)
```sql
SELECT strftime('%H', order_purchase_timestamp) AS hour, COUNT(*) AS total_orders
FROM olist_orders_dataset
WHERE strftime('%m', order_purchase_timestamp) IN ('06','07','08')
GROUP BY hour
ORDER BY total_orders DESC
LIMIT 3;
```

### الربيع (مارس، أبريل، مايو)
```sql
SELECT strftime('%H', order_purchase_timestamp) AS hour, COUNT(*) AS total_orders
FROM olist_orders_dataset
WHERE strftime('%m', order_purchase_timestamp) IN ('03','04','05')
GROUP BY hour
ORDER BY total_orders DESC
LIMIT 3;
```

### الشتاء (ديسمبر، يناير، فبراير)
```sql
SELECT strftime('%H', order_purchase_timestamp) AS hour, COUNT(*) AS total_orders
FROM olist_orders_dataset
WHERE strftime('%m', order_purchase_timestamp) IN ('12','01','02')
GROUP BY hour
ORDER BY total_orders DESC
LIMIT 3;
```

### الخريف (سبتمبر، أكتوبر، نوفمبر)
```sql
SELECT strftime('%H', order_purchase_timestamp) AS hour, COUNT(*) AS total_orders
FROM olist_orders_dataset
WHERE strftime('%m', order_purchase_timestamp) IN ('09','10','11')
GROUP BY hour
ORDER BY total_orders DESC
LIMIT 3;
```
