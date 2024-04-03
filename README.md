# SQL-dvdrental

## SQL初級課題  
- 1
  ```sql
  SELECT title, release_year FROM film;
  ```
- 2
  ```sql
  SELECT title FROM film WHERE rental_rate >= 4;
  ```
- 3
  ```sql
   INSERT INTO customer(store_id,first_name, last_name, email, address_id,activebool) 
   VALUES(
   1,
   'Taeko',
   'Asai',
   'asai.taeko@sakilacustomer.org',
   1,
   true);
  ```
- 4
  ```sql
   UPDATE customer
   SET email='updated@email.com'
   WHERE customer_id = 5;
  ```
## SQL中級課題
1. 複数のJOINの活用（グルーピングなし）
>・要件：まずは、映画のタイトルを確認するために、film テーブルから利用可能な映画の一覧を取得してください。次に、そのリストから好きな映画を一つ選択します。  

`SELECT * FROM film` 　→　film_id:850  　title:Story Side を選択しました。

>1. film テーブル、inventory テーブル、store テーブル、address テーブルを結合（JOIN）します。

```sql
SELECT * FROM film f
INNER JOIN inventory i ON f.film_id = i.film_id
INNER JOIN store s ON i.store_id = s.store_id
INNER JOIN address a ON s.address_id = a.address_id;
```

>2. 選択した映画がどの店舗にあるかを確認します。

```sql
SELECT DISTINCT s.store_id FROM film f
INNER JOIN inventory i ON f.film_id = i.film_id
INNER JOIN store s ON i.store_id = s.store_id
INNER JOIN address a ON s.address_id = a.address_id
WHERE f.title = 'Story Side'
ORDER BY s.store_id;
```

>3. 選択した映画が配置されている店舗のアドレス情報を取得します。

```sql
SELECT DISTINCT a.address_id, a.address, a.district, a.city_id, a.postal_code FROM film f
INNER JOIN inventory i ON f.film_id = i.film_id
INNER JOIN store s ON i.store_id = s.store_id
INNER JOIN address a ON s.address_id = a.address_id
WHERE f.title = 'Story Side'
ORDER BY a.address_id;
```

>4. この情報をリスト化して、選択した映画が置かれている店舗のアドレスを表示します。
>グルーピング（集計）を行わず、選択した映画が置かれている店舗ごとのアドレス情報をリストアップしてください。

```sql
SELECT DISTINCT f.title, s.store_id, a.address, a.district, a.city_id, a.postal_code FROM film f
INNER JOIN inventory i ON f.film_id = i.film_id
INNER JOIN store s ON i.store_id = s.store_id
INNER JOIN address a ON s.address_id = a.address_id
WHERE f.title = 'Story Side'
ORDER BY s.store_id;
```

<br>

2. 複数テーブルのグルーピングと集計の適用  
>・要件：payment テーブル、customer テーブル、rental テーブルを利用して、顧客IDごとの合計支払い金額とその顧客の合計レンタル回数を計算し、合計支払い金額を第1優先、レンタル回数を第2優先として、上位5人の顧客ID、その支払い合計、レンタル回数を取得してください。

```sql
SELECT c.customer_id AS "顧客ID", SUM(p.amount) AS "合計支払い金額", COUNT(r.rental_id) AS "合計レンタル回数"
FROM customer c INNER JOIN payment p ON c.customer_id = p.customer_id
INNER JOIN rental r ON p.rental_id = r.rental_id
GROUP BY c.customer_id
ORDER BY "合計支払い金額" DESC, "合計レンタル回数" DESC LIMIT 5;
```

