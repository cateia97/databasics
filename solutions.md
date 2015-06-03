How many users are there?

`SELECT COUNT(*) FROM users;`

What are the 5 most expensive items?

`SELECT * FROM items ORDER BY price DESC LIMIT 5;`

What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)

`SELECT * FROM items WHERE category LIKE "%Books%" ORDER BY price ASC LIMIT 1;`

Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?

`SELECT * FROM users INNER JOIN addresses ON addresses.user_id = users.id WHERE addresses.street = "6439 Zetta Hills";`
`SELECT * FROM addresses WHERE user_id = 40;`

Correct Virginie Mitchell's address to "New York, NY, 10108".

`SELECT * FROM addresses JOIN users ON users.id = addresses.user_id WHERE users.first_name = "Virginie" AND users.last_name = "Mitchell" AND addresses.state = "NY";`

`UPDATE addresses SET city = "New York", zip = 10108 WHERE street = "12263 Jake Crossing";`

How much would it cost to buy one of each tool?

`SELECT SUM(price) FROM items WHERE category LIKE "%Tools%"`

How many total items did we sell?

`SELECT SUM(quantity) FROM orders;`

How much was spent on books?
(This question is a bit vague, because the query could include items from categories such as "Toys & Books". So, I'm giving the answer two ways; the first for the broad category search, and the second for the strict "Books" search.)

`SELECT SUM(price) FROM orders JOIN items ON items.id WHERE items.category LIKE "%Books%";`
`SELECT SUM(price) FROM orders JOIN items ON items.id WHERE items.category = "Books";`

Simulate buying an item by inserting a User for yourself and an Order for that User.

`INSERT INTO users (first_name, last_name, email) VALUES ("Kelly", "Bristol", "bristolkr@gmail.com");`
`INSERT INTO addresses (user_id, street, city, state, zip)` 
`VALUES ((SELECT users.id FROM users WHERE first_name = "Kelly" AND last_name = "Bristol"), "123 Puritan Lane", "Small Town", "ND", 58762);`
`INSERT INTO orders (user_id, item_id, quantity, created_at)` 
`VALUES ((SELECT users.id FROM users WHERE users.first_name = "Kelly" AND users.last_name = "Bristol"), (SELECT items.id FROM items WHERE items.title =` `"Intelligent Concrete Pants"), 1, CURRENT_TIMESTAMP);`

What item was ordered most often? Grossed the most money?

Most ordered: `SELECT item_id, SUM(quantity) FROM orders GROUP BY item_id ORDER BY SUM(quantity) DESC LIMIT 1;`
Highest grossing: 

What user spent the most?

What were the top 3 highest grossing categories?
