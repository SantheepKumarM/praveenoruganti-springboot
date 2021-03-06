### Sales Order Service

1. Sales order customer- event subscription
   - When a "Customer Created" event is published, sales order service needs to subscribe to it. Fetch the customer details(customer id,email,first_name,last_name) 
     and insert into the local customer table

2. Create Order- create an order and return an order id
   http://localhost:6071/salesorderservice/orders
   Input: Order Description, Order Date, customer id, list of item names
   Output: Order Id
   - validate customer by verifying the table "customer_sos" with cust_id
   - validate the items by calling item service with item name
     http://localhost:6072/itemservice/items/{itemname}
   - create order by inserting the order details in  order table and items for the order details in order_line_item table

```SQL

create database omssalesorderdb;
use omssalesorderdb;
create table hibernate_sequence (next_val bigint) engine=MyISAM;
insert into hibernate_sequence values ( 1 );
create table customer_sos (cust_id bigint not null, cust_creation_date varchar(20) not null, email varchar(50) not null, cust_first_name varchar(50) not null, cust_last_name varchar(50) not null, primary key (cust_id)) engine=MyISAM;
create table order_line_item (id bigint not null, item_name varchar(50) not null, item_quantity double precision, order_id bigint, primary key (id)) engine=MyISAM;
create table sales_order (id bigint not null, cust_id bigint, order_date varchar(20) not null, order_desc varchar(100) not null, total_price double precision, primary key (id)) engine=MyISAM;

```