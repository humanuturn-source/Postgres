
# Video Resource: Learn Postgres in 2 Minutes
## Quick Installation Guide (Docker & pgAdmin)

This companion guide provides the exact steps and commands shown in the video to get your PostgreSQL database and pgAdmin management tool up and running locally using Docker.

---

### Prerequisites
Before running the commands, ensure you have **Docker Desktop** installed and running on your machine:
* [Download Docker Desktop](https://www.docker.com/products/docker-desktop/)

---

### Step 1: Create a Dedicated Docker Network
To allow your PostgreSQL database and pgAdmin containers to communicate securely with each other, create a shared Docker network:

```bash
docker network create pg-network
```

### Step 2: Deploy the PostgreSQL Database Container
Run the following command to pull the official PostgreSQL image and spin up your database container with default administrative credentials:

```bash
docker run --name postgres-db \\
  --network pg-network \\
  -e POSTGRES_USER=admin \\
  -e POSTGRES_PASSWORD=myadmin \\
  -e POSTGRES_DB=dev_db \\
  -p 5432:5432 \\
  -d postgres
```

Database Configuration Reference:
• Container Name: postgres-db
• Network: pg-network
• Username: admin
• Password: myadmin
• Default Database: dev_db
• Local Port: 5432


### Step 3: Deploy the pgAdmin Management Tool Container
To easily view and manage your data through a web interface, deploy the pgAdmin container connected to the same network:

```bash

docker run --name pgadmin-tool \\
  --network pg-network \\
  -e PGADMIN_DEFAULT_EMAIL=sample@gmail.com \\
  -e PGADMIN_DEFAULT_PASSWORD=pgadmin \\
  -p 5050:80 \\
  -d dpage/pgadmin4
```

pgAdmin Login Credentials:
• Web Interface URL: http://localhost:5050
• Email / Username: sethrajaram100@gmail.com
• Password: pgadmin


### Step 4: Connecting pgAdmin to Your Postgres Database

1. Open your browser and navigate to http://localhost:5050.
2. Log in using the pgAdmin credentials provided in Step 3.
3. Right-click on Servers -> Register -> Server...
4. Under the General tab, name the connection (e.g., Local Dev DB).
5. Under the Connection tab, use the following configuration:  
  • Host name/address: postgres-db
  • Port: 5432 
  • Maintenance database: dev_db 
  • Username: admin 
  • Password: myadmin

6. Click Save, and you are ready to build your database!

### Step 5: Create Table

```sql
CREATE TABLE Products (
    product_id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    size VARCHAR(50),
    price NUMERIC(10, 2)
);
```


### Step 6: Load data

```sql
INSERT INTO Products (name, size, price) VALUES
('Whole Milk', '1 Gallon', 4.29),
('Low Fat Milk 2%', '1 Gallon', 4.19),
('Skim Milk', '0.5 Gallon', 2.89),
('Organic Almond Milk', '32 oz', 3.49),
('Oat Milk Barista Blend', '32 oz', 4.19),
('Greek Yogurt Plain', '32 oz', 5.49),
('Strawberry Yogurt Cup', '6 oz', 0.89),
('Cheddar Cheese Block', '8 oz', 3.99),
('Shredded Mozzarella', '16 oz', 4.89),
('Salted Butter', '16 oz', 4.49),
('Unsalted Butter', '16 oz', 4.49),
('Heavy Whipping Cream', '16 oz', 3.29),
('Sour Cream', '16 oz', 2.49),
('Cream Cheese', '8 oz', 2.99),
('Large White Eggs', '12 Count', 3.19),
('Organic Brown Eggs', '12 Count', 4.59),
('White Bread', '20 oz', 2.49),
('Whole Wheat Bread', '20 oz', 2.99),
('Sourdough Loaf', '16 oz', 4.29),
('Croissants', '4 Pack', 4.99),
('Chocolate Chip Cookies', '12 Count', 3.89),
('Blueberry Muffins', '4 Pack', 4.49),
('Bagels Plain', '6 Count', 3.69),
('Tortillas Corn', '30 Count', 1.99),
('Tortillas Flour', '10 Count', 2.49),
('White Rice Long Grain', '5 lb', 4.99),
('Brown Rice', '2 lb', 2.49),
('Quinoa Organic', '16 oz', 3.99),
('Spaghetti Pasta', '16 oz', 1.49),
('Penne Pasta', '16 oz', 1.49),
('Marinara Pasta Sauce', '24 oz', 2.99),
('Olive Oil Extra Virgin', '16.9 oz', 8.99),
('Vegetable Oil', '48 oz', 4.69),
('Apple Cider Vinegar', '16 oz', 3.29),
('Soy Sauce', '15 oz', 2.79),
('Mayonnaise', '30 oz', 4.99),
('Ketchup', '20 oz', 2.89),
('Yellow Mustard', '14 oz', 1.79),
('Dill Pickle Spears', '24 oz', 3.49),
('Peanut Butter Creamy', '16 oz', 2.99),
('Strawberry Jam', '18 oz', 3.49),
('Honey Pure', '12 oz', 4.99),
('Granulated Sugar', '4 lb', 3.29),
('All-Purpose Flour', '5 lb', 3.49),
('Baking Powder', '8.1 oz', 2.19),
('Sea Salt Shaker', '26 oz', 1.99),
('Black Pepper Ground', '4 oz', 3.49),
('Garlic Powder', '3 oz', 2.29),
('Cinnamon Ground', '2.5 oz', 2.49),
('Coffee Beans Medium Roast', '12 oz', 7.99),
('Instant Coffee', '7 oz', 6.49),
('Black Tea Bags', '100 Count', 3.99),
('Green Tea Bags', '20 Count', 2.79),
('Coca-Cola Soda', '12 Pack', 6.99),
('Diet Coke', '12 Pack', 6.99),
('Sparkling Water Lime', '8 Pack', 3.99),
('Spring Water', '24 Pack', 4.99),
('Apple Juice', '64 oz', 3.29),
('Orange Juice No Pulp', '52 oz', 3.99),
('Cranberry Juice', '64 oz', 3.79),
('Potato Chips Classic', '13 oz', 4.29),
('Tortilla Chips', '13 oz', 3.99),
('Pretzels Twists', '16 oz', 2.99),
('Ranch Dip', '16 oz', 2.79),
('Salsa Medium', '16 oz', 3.19),
('Roasted Almonds Salted', '16 oz', 6.99),
('Cashews Whole', '14 oz', 7.49),
('Gummy Bears', '5 oz', 1.89),
('Milk Chocolate Bar', '3.5 oz', 2.19),
('Dark Chocolate 70%', '3.5 oz', 2.49),
('Microwave Popcorn Butter', '3 Pack', 2.99),
('Oatmeal Old Fashioned', '18 oz', 2.89),
('Corn Flakes Cereal', '12 oz', 3.49),
('Honey Nut Oats Cereal', '15.4 oz', 4.29),
('Granola Oats & Honey', '11 oz', 3.79),
('Frozen Pizza Pepperoni', '22 oz', 5.99),
('Frozen Ice Cream Vanilla', '48 oz', 4.49),
('Frozen Peas', '16 oz', 1.29),
('Frozen Mixed Berries', '16 oz', 3.99),
('Frozen Chicken Nuggets', '32 oz', 6.49),
('Frozen Waffles', '10 Count', 2.69),
('Bananas', '1 lb', 0.59),
('Gala Apples', '3 lb Bag', 4.49),
('Strawberries Fresh', '1 lb', 3.29),
('Blueberries Fresh', '1 Pint', 2.99),
('Lemons', '1 lb Bag', 2.49),
('Avocados Hass', '4 Pack', 4.99),
('Yellow Onions', '3 lb Bag', 2.79),
('Russet Potatoes', '5 lb Bag', 3.49),
('Baby Carrots', '16 oz', 1.49),
('Fresh Broccoli Crowns', '1 lb', 1.99),
('Romaine Hearts', '3 Pack', 3.29),
('Cherry Tomatoes', '10 oz', 2.49),
('Garlic Bulb', '3 Pack', 1.49),
('Fresh Ginger Root', '0.5 lb', 1.99),
('Canned Tuna in Water', '5 oz', 1.29),
('Canned Black Beans', '15 oz', 0.99),
('Canned Garbanzo Beans', '15 oz', 0.99),
('Canned Tomato Paste', '6 oz', 0.79),
('Canned Chicken Noodle Soup', '18.6 oz', 2.29);
```
---



---
