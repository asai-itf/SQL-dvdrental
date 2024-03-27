# SQL-dvdrental

## 課題  
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
