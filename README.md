<!--How many users are there?
sqlite> select count (*) from users;
count (*)
50

What are the 5 most expensive items?
63|Incredible Concrete Chair|Shoes, Toys & Music|Object-based even-keeled orchestration|121
24|Rustic Steel Shirt|Sports|Implemented dedicated structure|301
56|Fantastic Concrete Chair|Automotive, Home & Electronics|Operative mission-critical orchestration|551
47|Rustic Plastic Gloves|Shoes, Computers & Kids|Customer-focused upward-trending initiative|612
51|Rustic Steel Shirt|Tools, Clothing & Toys|Proactive incremental attitude|615

    sqlite> select * from items order by price desc;-->

<!--What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)
sqlite> select category, title, price from items where category like '%Books%' order by price;
Books|Ergonomic Granite Chair|1496-->

<!--Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
sqlite> select user_id from addresses where street = '6439 Zetta Hills' AND city = 'Willmouth' AND state='WY';
user_id
40

select * from addresses with user_id = 40
id|user_id|street|city|state|zip
43|40|6439 Zetta Hills|Willmouth|WY|15029
44|40|54369 Wolff Forges|Lake Bryon|CA|31587-->


Correct Virginie Mitchell's address to "New York, NY, 10108".
sqlite> select * from users where first_name = 'Virginie' AND last_name = 'Mitchell';
id|first_name|last_name|email
39|Virginie|Mitchell|daisy.crist@altenwerthmonahan.biz

sqlite> select * from addresses where user_id = 39;
id|user_id|street|city|state|zip
41|39|12263 Jake Crossing|Roxanehaven|NY|34705
42|39|83221 Mafalda Canyon|Bahringerland|WY|24028

sqlite> update addresses SET city = 'New York', state = 'NY', zip = '10108' WHERE user_id = 39;
sqlite> select * from addresses where user_id = 39;
41|39|12263 Jake Crossing|New York|NY|10108
42|39|83221 Mafalda Canyon|New York|NY|10108

How much would it cost to buy one of each tool?
sqlite> select sum(price) from items where category like '%tool%';
sum(price)
46477

How many total items did we sell?
orders - quanity - sum

How much was spent on books?
<!--search for orders - get headings, pull quanity sold ** this will show total spent  transactions over time***-->
<!--search for items to find the price of each item-->
<!--find the sume of those values (from two seperate tables)-->
<!--order.item_id to match item.id-->
sqlite> SELECT SUM(orders.quantity*items.price) as total_spent_on_books FROM orders JOIN items on orders.item_id = items.id WHERE items.category LIKE '%book%';
total_spent_on_books
1081352

Simulate buying an item by inserting a User for yourself and an Order for that User.
sqlite> INSERT INTO users (first_name, last_name, email) values ('Sara', 'Trempe', '88.trempe.sara@gmail.com');
sqlite> select * from users;
51|Sara|Trempe|88.trempe.sara@gmail.com

sqlite> insert into orders (user_id, item_id, quantity, created_at) values ('51', '45', '3', datetime());
sqlite> select * from orders where user_id = '51';
id|user_id|item_id|quantity|created_at
378|51|45|3|2017-03-06 22:17:48
sqlite> 