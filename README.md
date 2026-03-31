# MIST 4610 Group Project 1 - Group 7

## Group Members:

1. Donovan D'Silva - 	[repo](https://github.com/donmelsil/MIST4610_Group-Project)
2. Noah Hammond	-[repo](https://github.com/NoahHammond1/MIST4610_CoffeeShop_Project)
3. Chase Lin - [repo](https://github.com/cinnamotz/mist4610gp1)
4. Krithin Lokasani	- [repo](https://github.com/lokasanikrithin-source/GP1MIST2610)
5. Jessica Ngo -[repo](https://github.com/jn83499/Mist4610_Group-Project)

## Problem Description
We were assigned a task to model and build a relational database for the general operations of a coffee shop. The central entity in the model is the Orders entity, as it represents each transaction made by customers and serves as the core around which the rest of the system operates. Orders connect key components of the business, including customers, employees, products, and payments.

The coffee shop operates with related entities such as products (menu items), suppliers, and loyalty accounts, all supporting daily operations. Suppliers provide the necessary ingredients and inventory, while customer and order data allow the business to track consumer behavior and service interactions.

We are interested in accurately modeling these relationships, generating sample data, and populating the entities and their attributes. We aim to perform functional queries on this data to provide important and valuable business insights, such as identifying popular menu items, managing inventory needs, and supporting decision-making for purchasing and operational efficiency.
## Data Model
Our model is based on the structure of a hypothetical chain/franchised coffee shop. The orders entity serves as the central part of the system, since it represents each and every transaction made by customers and connects it to multiple entities including employees, products, and payments.

Within the system there are many customers who place orders, and each customer can place multiple orders over time, establishing a one to many relationship between customers and orders entities. Similarly, the coffee shop employs many employees who handle transactions. Each employee can process multiple orders, but each order is handled by a single employee. We identify this relationship as a one to many relationship between Employees and Orders. There also includes a recursive relationship to represent management structure within the coffee shop. Each employee reports to a manager, which is also another employee in the system. We use the ManagerId attribute, which also references the EmployeeID within the same table. As a result this creates a one to many recursive relationship where one manager can supervise multiple employees and each employee reports to only one manager.

We also have a StoreLocation entity that represents the physical coffee shop locations where each location employs many employees but employees are only able to work at a single location. Hence why we created a one to many relationship between StoreLocation and Employees. Orders then breaks down into individual items through OrderItems, acting as an associative entity between Orders and Products. Each order can contain multiple products like drinks and pastries, and then each product can appear in multiple different orders. Because of this, we identify this as a many to many relationship between Orders and Products, and the OrderItems table is used to store details like price, quantity and customizations for each product. This creates a one to many relationship between Orders and OrderItems and a one to many relationship between Products and OrderItems.

The products entity stores all of the items solid by the coffee chain, things like beverages and food. Each product is then assigned to a category, like tea, coffee, pastries, and each category can contain multiple products. This establishes a one to many relationship between category and products, which help in organizing inventory and simplify reporting. Products are then supplied to by external suppliers, and this relationship would be many to many, because a single supplier can provide multiple products and a product can come from multiple suppliers. To solve this, the model uses an associative entity named ProductSupplier, creating two one to many relationships, one between Suppliers and ProductSupplier and another between Products and ProductSupplier.

The model then tracks financial transactions through Payments. Each order is associated with a PaymentID, allowing the system to track how and when transactions are completed. This creates a one to one relationship between Orders and Payments since every Order can only take one payment.

Finally, the coffee chain includes a Loyalty program, which we decided to display through a LoyaltyAccounts entity to manage the customer reward system. Each customer can have one loyalty account, and each loyalty account belongs to a single customer, forming a one to one relationship. This allows both the business and customer to track points and rewards, and specifically for the business to repeat and improve upon customer engagement.

Overall, the data model supports the core function and operations of a local coffee chain by organizing between customers, employees, products, suppliers, and transactions. It ensures the business has a database that can effectively track sales, manage inventory, track consumer behavior and support loyalty programs.
![Coffee Shop Data Model](ProjectDataModel.png)
## Data Dictionary
![Employee Data Dictionary](DataDict_Employees.png)
![Customer Data Dictionary](DataDict_Customers.png)
![Category and Store Location Data Dictionary](DataDict_Cat_StrLoc.png)
![Orders Data Dictionary](DataDict_Orders.png)
![OrderItems and Dictionary](DataDict_OrderItems.png)
![Products Data Dictionary](DataDict_Products.png)
![Loyalty Account and Payment Data Dictionary](DataDict_Loy_Pmt.png)
![Supplier and Product Supplier Data Dictionary](DataDict_Sup_ProdSup.png)
## Queries
| Feature                     | Q1 | Q2 | Q3 | Q4 | Q5 | Q6 | Q7 | Q8 | Q9 | Q10 |
|----------------------------|----|----|----|----|----|----|----|----|----|-----|
| Multiple Table Join        | X  | X  |    | X  | X  |    | X  |    |    |     |
| Subquery                   | X  |    |    | X  |    |    |    |    |    |     |
| GROUP BY                   | X  | X  |    |    | X  | X  |    |    |    |     |
| GROUP BY with HAVING       | X  |    |    |    |    |    |    |    |    |     |
| Multi-condition WHERE      |    |    |    |    |    |    |    |    |    |     |
| Built-in Functions         | X  | X  | X  |    |    | X  |    |    |    |     |
| REGEXP                     |    |    | X  |    |    |    |    |    |    |     |
| NOT EXISTS                 |    |    |    |    |    |    |    |    |    |     |

1. Query 1 finds customers who spend more than average by comparing each customer’s total spending to the overall average payment.
   
![Query1](Query1.png)

Query 1 allows managers to identify the customers who spend the most, helping them focus on high-value customers. This allows them to create targeted promotions, loyalty rewards, and  strategies to increase revenue. It also helps them make smarter business decisions by understanding customer spending patterns.

2. Query 2 adds up the quantity sold for each product and groups the results by product name so you can see the total units sold for each individual product.
   
![Query2](Query2.png)

Query 2 allows managers to see which items are popular so they know what is selling well and what might not be selling well. By identifying top-performing items, managers can know which products to restock or promote more of. It also helps with inventory planning and forecasting demand, so they don’t overstock slow items or run out of popular ones.

3. Query 3 finds the total amount of orders from Decemember 2025.

![Query3](Query3.png)
Query 3 allows for managers and employees to see the total amount of orders for a certain month. In the case of query 3 it is for the month of December. This is useful for managers as they can compare the total amount of orders in December to those of other months, which would help to show how orders increase or decrease from month to month. It would help to show how busy a store is based on the total monthly orders.

4. Query 4 lists the total revenue generated by credit card payments during 2026. The results are ordered in descending order of total revenue.

![Query4](Query4.png)
Query 4 helps managers identify which customers are making large purchases using only credit cards during the 2026 fiscal year. If they notice that most of these high-value transactions come from a small group of repeat customers, it suggests those customers are especially engaged and valuable to the business. With that insight, managers could consider introducing a premium rewards program or offering exclusive perks to these high-spending customers, encouraging them to stay loyal and potentially increasing overall transaction values across store locations.

5. Query 5 lists each store location alongside its total number of orders, total revenue generated, and average order value. The results are ordered in descending order of total revenue.

![Query5](Query5.png)
Query 5 allows managers to compare the performances of each store location against each other in a multitude of ways. The ways are total orders, total revenue, and average order value. Total orders would allow managers to understand how many total orders are being processed by each store relative to their counterparts, to understand which locations are seeing more volume. Total revenue gives a little more of this understanding, by allowing managers to dissect even further into which stores are the most profitable. Average order value allows managers to better understand which stores are able to generate more value based on each individual order, possibly justifying raised prices or expanded premium offerings at certain locations.

6. Query 6 finds what payment method is used the most amongst all the stores.

![Query6](Query6.png)
Query 6 allows for managers to see what type of payment method is the most popular. The query shows that cash is used the least out of all payment methods. Managers might be able to adopt a card and mobile payments only store policy, since they would be faster for store purchases. It would take more time having to count cash and give that back to the customer if they decide to use that as a method of payment.

7. Query 7 shows the amount of loyalty points attached to a customer ID in descending order.

![Query7](Query7.png)
Query 7 allows for customers to see the total amount of loyalty points they have. This is useful for when they need to redeem for different rewards. It would also be useful for employees and managers to see them when during or after a purchase to help loyalty point redemption.

## Database information
Name of Database: al_Group_21482_G7

Additional Info: Each query listed above is marked in the database used stored procedures which are called through the following format: CALL DNCKJ_Q() where "()" is the query number.
