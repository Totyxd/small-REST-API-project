============================================
============================================
### This is the documentation for a small e-commerce site that follows RESTful convention for URLS and endpoints. The goal was developing a small project to get the hang of REST APIs and write this docs to get an even better domain over the conventions these APIs use.

* Note
    - Headers contain many keys, but for this exercise we'll focus on **Content-Type** and **Location**, since browser usually handles the others.

### DOCUMENTATION

### Ask for the Home Page

Request components:
- Method: GET
- URL: /
- Headers: none
- Body: none

Response components:
- Status Code: 200
- Headers:
  - Content-Type: text/html
- Body: HTML page with navigation links to other pages

=============================================
=============================================

### Ask for a page that doesn't exist

Request components:
- Method: GET
- URL: /monkeys
- Headers: None
- Body: None

Response components:
- Status code: 404
- Headers:
  - Content-Type: text/html
- Body: The html of the 404 error indicating that the resource that the client is trying to access does not exist.

### Ask for the products list page

Request components:
- Method: GET
- URL: /products
- Headers: None
- Body: None

Response components:
- Status code: 200
- Headers:
  - Content-Type: text/html
- Body: The html that server gave us as a response that includes a collection of resources (all the products from the e-commerce).

### Ask for the product detail page

Here's an example product on the server:

| detail      | value                                                      |
| ----------- | ---------------------------------------------------------- |
| productId   | 1                                                          |
| name        | "Facial Cleansing Brush"                                   |
| description | "Reaches deep pores to cleanse oil, dirt, and blackheads." |
| price       | 23.99                                                      |
| categories  | "beauty", "electronics"                                    |

Request components:
- Method: GET
- URL: /products/:productId
- Headers: None
- Body: None

Response components:
- Status code: 200
- Headers:
  - Content-Type: text/html
- Body: HTML respone of the specific product associated with the ID.

### Ask for the create new product page

Request components:
- Method: GET
- URL: /products/new
- Headers: None
- Body: None

Response components:
- Status code: 200
- Headers:
  - Content-Type: text/html
- Body: HTML response with the page to add a new product to the product list.

### Submit a new product

For a traditional HTML web server, whenever a successful `POST`
request is sent to the server, the server should respond with a redirection to
a page.

After successful submission, user should be looking at the product detail page.

Here are the categories on the server:

| tag         | name           |
| ----------- | -------------- |
| grocery     | Grocery        |
| electronics | Electronics    |
| beauty      | Beauty         |
| toys-games  | Toys and Games |
| health      | Health         |
| furniture   | Furniture      |
| clothing    | Clothing       |


Request components:
- Method: POST
- URL: /products
- Headers:
  - Content-Type: application/x-www-form-urlencoded
  - Referer: /products/new
- Body: Form data in key value pairs for the product needed.

Response components:
- Status code: 302 (Redirection) // 200(Succesful GET; second request)
- Headers:
  - Location: /products/:productId
  - Content-Type: text/html
- Body: None.

### Ask for the edit product page

Request components:
- Method: GET
- URL: products/:productId/edit
- Headers: None
- Body: None

Response components:
- Status code: 200
- Headers:
  - Content-Type: text/html
- Body: HTML page with the form to edit an already created product.

### Submit an edit for an existing product

After successful submission, user should be looking at the product detail page.

Request components:
- Method: POST
- URL: /products/:productId
- Headers:
  - Content-Type: application/x-www-form-urlencoded
  - Referer: products/:productId/edit
- Body: Form data in key value pairs for the product that requires editing.

Response components:
- Status code: 302
- Headers:
  - Location: /products/:productId
  - Content-Type: text/html
- Body: None

### Submit a delete for an existing product

After successful submission, user should be looking at the products list page.

Request components:
- Method: POST
- URL: /products/:productId/delete
- Headers:
  - Content-Type: application/x-www-form-urlencoded
- Body: None

Response components:
- Status code: 302
- Headers:
  - Location: /products
  - Content-Type: text/html
- Body: None

### Submit a new review for a product

After successful submission, user should be looking at the product detail page.

Here's an example review on the server:

| detail     | value                  |
| ---------- | ---------------------- |
| reviewId   | 1                      |
| comment    | "I love this product!" |
| starRating | 5                      |
| productId  | 1                      |

Request components:
- Method: POST
- URL: /products/:productId/reviews
- Headers:
  - Content-Type: application/x-www-form-urlencoded
- Body: Form data in key value pairs related to the product review.

Response components:
- Status code: 302
- Headers:
  - Location: /products/:productId
  - Content-Type: text/html
- Body: None

### Ask for the edit review page for a product

Request components:
- Method: GET
- URL: /reviews/:reviewId/edit
- Headers: None
- Body: None

Response components:
- Status code: 200
- Headers:
  - Content-Type: text/html
- Body: HTML form page to edit a review.

### Submit an edit for an existing review

After successful submission, user should be looking at the product detail page.

Request components:
- Method: POST
- URL: /reviews/:reviewId
- Headers:
  - Content-Type: application/x-www-form-urlencoded
- Body: Form data in key value pairs to edit the review.

Response components:
- Status code: 302
- Headers:
  - Location: /product/:productId (related to the review)
  - Content-Type: text/html
- Body: None

### Submit a delete for an existing review

After successful submission, user should be looking at the product detail page.

Request components:
- Method: POST
- URL: /reviews/:reviewId/delete
- Headers:
  - Content-Type: application/x-www-form-urlencoded
- Body: None

Response components:
- Status code: 302
- Headers:
  - Location: /product/:productId (related to the review)
  - Content-Type: text/html
- Body: None.

### Ask for all the products in a particular category by tag of the category

Request components:
- Method: GET
- URL: /categories/:categoryId/products
- Headers: None
- Body: None

Response components:
- Status code: 200
- Headers:
  Content-Type: text/html
- Body: HTML page with the list of all the products that belong to the category.

### Ask for the best-selling product

Look for clues in the HTML pages from the prior responses for what the route should be.

Request components:
- Method: GET
- URL: /products/best-selling
- Headers: None
- Body: None

Response components:
- Status code: 200
- Headers:
  - Content-Type: text/html
- Body: HTML page with best selling products.
