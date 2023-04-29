# SQL-code
Code used for Database System Group Project
INSERT INTO Orders (customer_id, order_date, total_price, set_menu_id)
VALUES (2, '5-4-23', (SELECT price FROM [Set Menus] WHERE set_menu_id = 1), 1);

INSERT INTO [Order Items] (order_id, item_id, quantity)
VALUES (8, 13, 2);

INSERT INTO Customers (customer_name, customer_phone)
VALUES ('NAME', 21346678);


SELECT [Order Items].order_id, [Menu Items].item_name, [Menu Items].item_type, [Menu Items].price, 
       [Order Items].quantity, [Set Menus].set_menu_name, Customers.customer_name, Customers.customer_phone, Orders.order_date
FROM [Order Items] JOIN [Menu Items] On [Order Items].item_id = [Menu Items].item_id
     JOIN Orders ON Orders.order_id = [Order Items].order_id
     JOIN Customers ON Customers.customer_id = Orders.customer_id
     JOIN [Set Menus] ON Orders.set_menu_id = [Set Menus].set_menu_id
WHERE Orders.order_date = '2-4-23';

SELECT order_id, order_date, customer_name, set_menu_name, price
FROM Customers, Orders, [Set Menus]
WHERE Customers.customer_id = Orders.customer_id
AND [Set Menus].set_menu_id = Orders.set_menu_id
AND Orders.customer_id = 1
ORDER BY order_id;

CREATE VIEW [Order List] AS
    SELECT [Order Items].order_id, [Menu Items].item_name, [Menu Items].item_type, [Menu Items].price, 
           [Order Items].quantity, [Set Menus].set_menu_name, Customers.customer_name, Customers.customer_phone, Orders.order_date
    FROM [Order Items] JOIN [Menu Items] On [Order Items].item_id = [Menu Items].item_id
         JOIN Orders ON Orders.order_id = [Order Items].order_id
         JOIN Customers ON Customers.customer_id = Orders.customer_id
         JOIN [Set Menus] ON Orders.set_menu_id = [Set Menus].set_menu_id;
