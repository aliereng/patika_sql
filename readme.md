Sorguların uygulandığı [veritabanı](https://www.postgresqltutorial.com/postgresql-getting-started/postgresql-sample-database/) 
## Ödev 1
**film tablosunda bulunan title ve description sütunlarındaki verileri sıralayınız.**
```sql
  SELECT title, description FROM film;
```
**film tablosunda bulunan tüm sütunlardaki verileri film uzunluğu (length) 60 dan büyük VE 75 ten küçük olma koşullarıyla sıralayınız.**
```sql
  SELECT title, length FROM film
  WHERE  length > 60 AND length < 75;
```
**film tablosunda bulunan tüm sütunlardaki verileri rental_rate 0.99 VE replacement_cost 12.99 VEYA 28.99 olma koşullarıyla sıralayınız.**
```sql
  SELECT * FROM film
  WHERE rental_rate = 0.99 AND (replacement_cost = 12.99 OR replacement_cost = 28.99);
```
**customer tablosunda bulunan first_name sütunundaki değeri 'Mary' olan müşterinin last_name sütunundaki değeri nedir?**
```sql
  SELECT first_name, last_name FROM customer
  WHERE first_name = 'Mary';
```
**film tablosundaki uzunluğu(length) 50 ten büyük OLMAYIP aynı zamanda rental_rate değeri 2.99 veya 4.99 OLMAYAN verileri sıralayınız.**
```sql
  SELECT * FROM film
  WHERE length < 50 AND NOT(rental_rate = 2.99 OR rental_rate = 2.99 );
```

## Ödev 2

**film tablosunda bulunan tüm sütunlardaki verileri replacement cost değeri 12.99 dan büyük eşit ve 16.99 küçük olma koşuluyla sıralayınız**
```sql
  SELECT * FROM film
  WHERE replacement_cost BETWEEN 12.99 AND 16.99;
```
**actor tablosunda bulunan first_name ve last_name sütunlardaki verileri first_name 'Penelope' veya 'Nick' veya 'Ed' değerleri olması koşuluyla sıralayınız.**
```sql
  SELECT first_name, last_name FROM actor
  WHERE first_name IN ('Penelope', 'Nick', 'Ed');
```

**film tablosunda bulunan tüm sütunlardaki verileri rental_rate 0.99, 2.99, 4.99 VE replacement_cost 12.99, 15.99, 28.99 olma koşullarıyla sıralayınız.**

```sql
  SELECT * FROM film
  WHERE rental_rate IN (0.99, 2.99, 4.99) AND replacement_cost IN (12.99, 15.99, 28.99);
```

## Ödev 3
**country tablosunda bulunan country sütunundaki ülke isimlerinden 'A' karakteri ile başlayıp 'a' karakteri ile sonlananları sıralayınız.**
```sql
  SELECT * FROM country
  WHERE country LIKE 'A%a';
```
**country tablosunda bulunan country sütunundaki ülke isimlerinden en az 6 karakterden oluşan ve sonu 'n' karakteri ile sonlananları sıralayınız.**
```sql
  SELECT * FROM country
  WHERE country LIKE '%_____n';
```

**film tablosunda bulunan title sütunundaki film isimlerinden en az 4 adet büyük ya da küçük harf farketmesizin 'T' karakteri içeren film isimlerini sıralayınız.**
```sql
  SELECT * FROM film
  WHERE title ILIKE '%t%t%t%t%';
```

**film tablosunda bulunan tüm sütunlardaki verilerden title 'C' karakteri ile başlayan ve uzunluğu (length) 90 dan büyük olan ve rental_rate 2.99 olan verileri sıralayınız.**
```sql
  SELECT * FROM film
  WHERE title LIKE 'C%' AND length > 90 AND rental_rate = 2.99;
```
## Ödev 4
**film tablosunda bulunan replacement_cost sütununda bulunan birbirinden farklı değerleri sıralayınız.**
```sql
  SELECT DISTINCT replacement_cost FROM film;
```
**film tablosunda bulunan replacement_cost sütununda birbirinden farklı kaç tane veri vardır?**
```sql
  SELECT COUNT(DISTINCT replacement_cost) FROM film;
```
**film tablosunda bulunan film isimlerinde (title) kaç tanesini T karakteri ile başlar ve aynı zamanda rating 'G' ye eşittir?**
```sql
  SELECT COUNT(*) FROM film
  WHERE title LIKE 'T%' AND rating = 'G';
```
**country tablosunda bulunan ülke isimlerinden (country) kaç tanesi 5 karakterden oluşmaktadır?**
```sql
  SELECT COUNT(*) FROM country
  WHERE country LIKE '_____';
```
**city tablosundaki şehir isimlerinin kaç tanesi 'R' veya r karakteri ile biter?**
```sql
  SELECT COUNT(*) from city
  WHERE city ILIKE '%r';
```
## Ödev 5
**film tablosunda bulunan ve film ismi (title) 'n' karakteri ile biten en uzun (length) 5 filmi sıralayınız.**

```sql
  SELECT * FROM film
  WHERE title LIKE '%n'
  ORDER BY length DESC
  LIMIT 5;
```

**film tablosunda bulunan ve film ismi (title) 'n' karakteri ile biten en kısa (length) ikinci(6,7,8,9,10) 5 filmi(6,7,8,9,10) sıralayınız.**
```sql
  SELECT film_id, title, length FROM film
  WHERE title LIKE '%n'
  ORDER BY length ASC
  OFFSET 5
  LIMIT 5;
```
offset ve limit bilgisi olmadan attığımız sorgunun sonucu ile offset ve limit bilgisi olarak attığımız sorgunun sonucunda length = 61 olan 4 adet verinin limit ve offset işleminden önceki sıralama ile gelmediği görülmüştür. Bunun sebebi limit bilgisi birer birer arttırldığında ortaya çıkmış olup 61 li grubun en son elemanının en başa sondan bir önceki elemanının 2. sıraya ilk elemanının da son sıraya yerleşmiş olduğu görülmüştür. Buradan yapılan çıkarım ise bit grup veri aynı değere sahip ve bir limitleme işlemi yapılacak ise  - burada aynı değer 61 ve limit işlemi 5 - bu 61 li grubun sıralamaya göre tam tersinin response olacağıdır.

**customer tablosunda bulunan last_name sütununa göre azalan yapılan sıralamada store_id 1 olmak koşuluyla ilk 4 veriyi sıralayınız.**
```sql
  SELECT * FROM customer
  WHERE store_id = 1
  ORDER BY last_name DESC
  LIMIT 4;
```

## Ödev 6
**film tablosunda bulunan rental_rate sütunundaki değerlerin ortalaması nedir?**
```sql
  SELECT ROUND(AVG(rental_rate),4) AS avarage_rental_rate FROM film;
```
**film tablosunda bulunan filmlerden kaç tanesi 'C' karakteri ile başlar?**

```sql
  SELECT COUNT(*) AS start_with_c FROM film
  WHERE title LIKE 'C%';
```
**film tablosunda bulunan filmlerden rental_rate değeri 0.99 a eşit olan en uzun (length) film kaç dakikadır?**

```sql
  SELECT MAX(length) FROM film
  WHERE rental_rate = 0.99;
```
**film tablosunda bulunan filmlerin uzunluğu 150 dakikadan büyük olanlarına ait kaç farklı replacement_cost değeri vardır?**

```sql
  SELECT COUNT(DISTINCT(replacement_cost)) FROM film
  WHERE length > 150
```

## Ödev 7
**film tablosunda bulunan filmleri rating değerlerine göre gruplayınız.**
```sql
  SELECT rating, COUNT(*) FROM film
  GROUP BY rating;
```
**film tablosunda bulunan filmleri replacement_cost sütununa göre grupladığımızda film sayısı 50 den fazla olan replacement_cost değerini ve karşılık gelen film sayısını sıralayınız.**

```sql
  SELECT replacement_cost, COUNT(*) FROM film
  GROUP BY replacement_cost
  HAVING COUNT(*) > 50;
```
**customer tablosunda bulunan store_id değerlerine karşılık gelen müşteri sayılarını nelerdir?**

```sql
  SELECT store_id, COUNT(*) FROM customer
  GROUP BY store_id
```
**city tablosunda bulunan şehir verilerini country_id sütununa göre gruplandırdıktan sonra en fazla şehir sayısı barındıran country_id bilgisini ve şehir sayısını paylaşınız.**

```sql
  SELECT country_id, COUNT(country_id) as adet FROM city  
  GROUP BY country_id
  ORDER BY COUNT(country_id) DESC
  FETCH FIRST 1 ROW ONLY;
```
## Ödev 8
**test veritabanınızda employee isimli sütun bilgileri id(INTEGER), name VARCHAR(50), birthday DATE, email VARCHAR(100) olan bir tablo oluşturalım.**
```sql
  CREATE TABLE employee (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    birthday DATE DEFAULT CURRENT_DATE,
    email VARCHAR(100);
```

**Oluşturduğumuz employee tablosuna 'Mockaroo' servisini kullanarak 50 adet veri ekleyelim.**

```sql
insert into employee (name, birthday, email) values ('Maurits', '1994-02-27', 'mhartwell0@cdc.gov');
insert into employee (name, birthday, email) values ('Taite', '1963-06-04', 'tpipkin1@ebay.com');
...
insert into employee (name, birthday, email) values ('Catlin', null, 'cwythill1d@samsung.com');
```

**Sütunların her birine göre diğer sütunları güncelleyecek 5 adet UPDATE işlemi yapalım.**

```sql
UPDATE employee
SET name = 'updated',
    birthday = '1555-05-15',
    email = 'updated@email.com
WHERE id = 1;

UPDATE employee
SET name = 'updated1',
    birthday = '1555-05-15',
    email = 'updated1@email.com
WHERE name LIKE '%a';

UPDATE employee
SET name = 'updated2',
    birthday = '1555-05-15',
    email = 'updated2@email.com
WHERE email IS NULL;

UPDATE employee
SET name = 'updated3',
    birthday = '1555-05-15',
    email = 'updated3@email.com
WHERE id > 30;

UPDATE employee
SET name = 'updated4',
    birthday = '1555-05-15',
    email = 'updated4@email.com
WHERE name ILIKE '%__a%' AND email IS NOT NULL;
```
**Sütunların her birine göre ilgili satırı silecek 5 adet DELETE işlemi yapalım.**
```sql
DELETE FROM employee
WHERE id = 1;

DELETE FROM employee
WHERE name LIKE '%a';

DELETE FROM employee
WHERE email IS NULL;

DELETE FROM employee
WHERE id > 30;

DELETE FROM employee
WHERE name ILIKE '%__a%' AND email IS NOT NULL;
```

## Ödev 9

**city tablosu ile country tablosunda bulunan şehir (city) ve ülke (country) isimlerini birlikte görebileceğimiz INNER JOIN sorgusunu yazınız.**

```sql
  SELECT city.city, country.country FROM city
  INNER JOIN country
  ON city.country_id = country.country_id;
```

**customer tablosu ile payment tablosunda bulunan payment_id ile customer tablosundaki first_name ve last_name isimlerini birlikte görebileceğimiz INNER JOIN sorgusunu yazınız.**

```sql
SELECT payment.payment_id, customer.first_name, customer.last_name FROM payment
INNER JOIN customer
ON payment.customer_id = customer.customer_id;
```

**customer tablosu ile rental tablosunda bulunan rental_id ile customer tablosundaki first_name ve last_name isimlerini birlikte görebileceğimiz INNER JOIN sorgusunu yazınız.**

```sql
SELECT rental.rental_id, customer.first_name, customer.last_name FROM rental
INNER JOIN customer
ON rental.customer_id = customer.customer_id;
```

## Ödev 10

**city tablosu ile country tablosunda bulunan şehir (city) ve ülke (country) isimlerini birlikte görebileceğimiz LEFT JOIN sorgusunu yazınız.**

```sql
SELECT city, country FROM city
LEFT JOIN country
ON city.country_id = country.country_id;
```

**customer tablosu ile payment tablosunda bulunan payment_id ile customer tablosundaki first_name ve last_name isimlerini birlikte görebileceğimiz RIGHT JOIN sorgusunu yazınız.**
```sql
SELECT first_name, last_name, payment_id FROM customer
RIGHT JOIN payment
ON payment.customer_id = customer.customer_id;
```
**customer tablosu ile rental tablosunda bulunan rental_id ile customer tablosundaki first_name ve last_name isimlerini birlikte görebileceğimiz FULL JOIN sorgusunu yazınız.**
```sql
SELECT rental_id, first_name, last_name FROM rental
FULL JOIN customer
ON rental.customer_id = customer.customer_id;
```
