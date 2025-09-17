# Table of Contents

1. [Overview](#overview)
2. [Technologies Used](#technologies-used)
3. [Endpoints](#endpoints)
   - 3.1 [Authentication Endpoint](#authentication-endpoint)
   - 3.2 [TraderDashboard Endpoint](#traderdashboard-endpoint)
   - 3.3 [HomePage Endpoint](#homepage-endpoint)
   - 3.4 [Search Endpoint](#search-endpoint)
   - 3.5 [productInfoPage Endpoint](#productinfopage-endpoint)
   - 3.6 [Reviews Endpoint](#reviews-endpoint)
   - 3.7 [Cart Endpoint](#cart-endpoint)
   - 3.8 [User Endpoint](#user-endpoint)
   - 3.9 [Order Endpoint](#order-endpoint)
   - 3.10 [Address Endpoint](#address-endpoint)
4. [Installation](#installation)
5. [Contribution](#contribution)

## Overview

1. **Registration and Authentication**:

   - Users can register and log in securely using JWT Tokens for authentication and authorization.
   - We have implemented ASP.NET Identity for user management and utilized JWT tokens to ensure secure access to the platform and its features.

2. **Homepage**:

   - Upon logging in, users are greeted with a homepage featuring essential information about the website and showcasing the top 9 available products.

3. **Product Page & Filtering**:

   - Users can navigate to the product page to view all products available on the platform.
   - Within the product page, users can filter products based on brand name, model name, model year, category, and price range.

4. **Product Details**:

   - Clicking on a product leads to a detailed page showcasing product information, ratings, comments, trader info, and trader ratings.

5. **Cart Functionality**:

   - Users can add desired products to their cart for later purchase.
   - The cart allows users to manage their selected items, proceed to payment, or remove items.

6. **Address Management**:

   - Users can add their address details for the current payment process, ensuring accurate delivery.

7. **Order Details**:

   - Upon completion of the payment process, users can view detailed order information on a separate page.

8. **product and Trader Reviews**:
   - After payment, users can review both the purchased product and its trader, providing valuable feedback to the community.
9. **Trader Dashboard**:
   - Traders have access to a dashboard where they can manage their inventory.
   - Functions include adding, updating, deleting, and retrieving their products.
   - Traders can also browse products available on the platform.

## Technologies Used

- **ASP.NET Web API**:

  We utilized **ASP.NET Web API**, along with **C#** programming language, to build robust and scalable APIs, enabling seamless communication between the frontend and backend.

- **React**:

  For frontend development, we chose **React.js** and **Redux** for efficient, dynamic, and responsive user interfaces. React's component-based architecture enabled us to create reusable UI elements, ensuring a more maintainable codebase.

- **Entity Framework Core**:

  We have used Entity Framework Core for creating our database based on **ORM** (Object-Relational Mapping) technology.

- **LINQ (Language Integrated Query)**:

  We leveraged LINQ for querying the database, providing a more intuitive and type-safe way to retrieve data.

- **ASP.NET Identity**:

  We have utilized **ASP.NET Identity** to generate **JWT** tokens, facilitating user Authentication and Authorization processes. Microsoft Identity also aids in the generation of Login and Registration Endpoints, as well as **Role-Based Access Control (RBAC)**, ensuring secure access to our platform's features.

## Endpoints

### Authentication Endpoint

#### Route: `api/Authentication`

##### 1. `/Register` (POST)

- **Description:** Registers a new user.
- **Request Body:**

  - `email`: String (required)
  - `password`: String (required)
  - `confirmPassword`: String (required, must match `password`)
  - `firstName`: String (required)
  - `lastName`: String (required)
  - `phoneNumber`: String (required, 11 digits)
  - `role`: String (required)

- **Response:**
  - `token`: String (JWT token)
  - `result`: Boolean (true if successful, false otherwise)
  - `role`: String (role chosen for the user)
  - `errors`: Array (list of errors if any)

##### 2. `/login` (POST)

- **Description:** Logs in an existing user.
- **Request Body:**

  - `email`: String (required)
  - `password`: String (required)

- **Response:**

  - `token`: String (JWT token)
  - `result`: Boolean (true if successful, false otherwise)
  - `role`: String (role of the user)
  - `errors`: Array (list of errors if any)

### TraderDashboard Endpoint

#### Route: `api/TraderDashboard`

This endpoint provides functionalities for managing products on the trader's dashboard. The user is uniquely identified using the bearer token.

#### 1. POST `/`

- **Description:** Adds a new product to the trader's dashboard.

- **Request Body:**

  - `brandName`: String (required) - The brand name of the product.
  - `modelName`: String (required) - The model name of the product.
  - `modelYear`: Integer (required) - The model year of the product.
  - `price`: Float (required) - The price of the product.
  - `productCategory`: String (required) - The category of the product.
  - `productImage`: String (optional) - URL to the image of the product.

- **Response:** Returns the details of the added product.

#### 2. PUT `/{productId}`

- **Description:** Updates the information of a product on the trader's dashboard.

- **Request Parameters:**

  - `productId`: Integer (required) - The unique identifier for the product.

- **Request Body:**

  - Same as the POST request body.

- **Response:** Returns the updated details of the product.

#### 3. DELETE `/{productId}`

- **Description:** Deletes a product from the trader's dashboard.

- **Request Parameters:**

  - `productId`: Integer (required) - The unique identifier for the product.

- **Response:** Returns the details of the deleted product.

#### 4. GET `/`

- **Description:** Retrieves a list of products on the trader's dashboard.

- **Response:** Returns an array of product objects, each containing the following attributes:

  - `brandName`: String - The brand name of the product.
  - `modelName`: String - The model name of the product.
  - `modelYear`: Integer - The model year of the product.
  - `price`: Float - The price of the product.
  - `productCategory`: String - The category of the product.
  - `productImage`: String - URL to the image of the product.

### HomePage Endpoint

#### Route: `api/HomePage`

##### 1. `/` (GET)

- **Description:** Retrieves a list of top 9 products.

- **Response:**

  - Array of product objects, each containing the following attributes:
    - `id`: Integer (unique identifier for the product)
    - `brandName`: String (name of the product brand)
    - `modelName`: String (name of the product model)
    - `modelYear`: Integer (year of the product model)
    - `price`: Float (price of the product)
    - `productCategory`: String (category of the product)
    - `productImage`: String (URL to the product image)
    - `inStock`: Boolean (availability of the product)
    - `orderId`: Integer or null (order ID if the product is ordered, null if not)
    - `traderId`: String (unique identifier of the trader)
    - `averageRating`: Float (average rating of the product)

### Search Endpoint

#### Route: `api/Search`

##### 1. `/` (GET)

- **Description:** Retrieves a list of products based on search criteria.

- **Request Parameters:**

  - `BrandName`: String (optional)
  - `ModelName`: String (optional)
  - `ModelYear`: Integer (optional)
  - `minPrice`: Float (optional)
  - `maxPrice`: Float (optional)
  - `productCategory`: String (optional)
  - `page`: Integer (optional)

- **Response:**

  - `totalCount`: Integer (total number of products matching the search criteria)
  - `page`: Integer (current page number)
  - `products`: Array of product objects, each containing the following attributes:
    - `id`: Integer (unique identifier for the product)
    - `brandName`: String (name of the product brand)
    - `modelName`: String (name of the product model)
    - `modelYear`: Integer (year of the product model)
    - `price`: Float (price of the product)
    - `productCategory`: String (category of the product)
    - `productImage`: String (URL to the product image)
    - `inStock`: Boolean (availability of the product)
    - `orderId`: Integer or null (order ID if the product is ordered, null if not)
    - `traderId`: String (unique identifier of the trader)
    - `reviews`: Array of review objects, each containing the following attributes:

### productInfoPage Endpoint

The `productInfoPage` endpoint provides detailed information about a specific product, including its reviews, trader information, and trader rating.

#### Route

- `/api/productinfo`

##### 1. GET `/{productId}`

- **Description:** Retrieves all information about a product, including its reviews, trader information, and trader rating.

- **Request Parameters:**

  - `productId`: Integer - The unique identifier for the product.

- **Response:**

  - `id`: Integer - The unique identifier for the product.
  - `brandName`: String - The brand name of the product.
  - `modelName`: String - The model name of the product.
  - `modelYear`: Integer - The model year of the product.
  - `price`: Float - The price of the product.
  - `productCategory`: String - The category of the product.
  - `productImage`: String - URL to the image of the product.
  - `inStock`: Boolean - Indicates if the product is in stock.
  - `traderRating`: Float - The rating of the trader associated with the product.
  - `firstName`: String - The first name of the trader.
  - `lastName`: String - The last name of the trader.
  - `phoneNumber`: String - The phone number of the trader.
  - `productReviews`: Array - An array of reviews for the product (empty if no reviews).

### Reviews Endpoint

The `Reviews` endpoint handles posting reviews for products and traders.

#### Route

- `/api/Reviews`

#### 1. POST `/product`

- **Description:** Adds a review for a product.

- **Request Body:**

  - `productId`: Integer (required) - The unique identifier for the product.
  - `rating`: Integer (required) - The rating given for the product.
  - `comment`: String (optional) - An optional comment for the review.

- **Response:** Returns the details of the posted review.

#### 2. POST `/trader`

- **Description:** Adds a review for a trader.

- **Request Body:**

  - `traderId`: String (required) - The unique identifier for the trader.
  - `rating`: Integer (required) - The rating given for the trader.
  - `comment`: String (optional) - An optional comment for the review.

- **Response:** Returns the details of the posted review.

### Cart Endpoint

The `Cart` endpoint manages operations related to a user's shopping cart.

#### Route

- `/api/Cart`

#### 1. GET `/GetCartItems`

- **Description:** Retrieves all products in the user's shopping cart.

- **Response:** Returns an array containing details of all products in the cart.

#### 2. POST `/AddToCart`

- **Description:** Adds a product to the user's shopping cart.

- **Request Parameters:**

  - `productId`: Integer - The unique identifier for the product to be added to the cart.

- **Response:** Returns the details of the added product.

#### 3. DELETE `/DeleteFromCart`

- **Description:** Removes a product from the user's shopping cart.

- **Request Parameters:**

  - `productId`: Integer - The unique identifier for the product to be removed from the cart.

- **Response:** Returns the details of the removed product.

#### 4. POST `/ProceedToPay`

- **Description:** Proceeds to payment after validating cart items.

- **Response:** Returns the details of all products in the cart, ensuring they have not been paid by another user and have not been deleted from the website by their trader.

### User Endpoint

The `User` endpoint allows for managing user information.

### Route

- `/api/User`

#### 1. PUT `/`

- **Description:** Updates user information.
- **Request Body:**

  - `firstName`: String (required)
  - `lastName`: String (required)
  - `email`: String
  - `phoneNumber`: String (required, 11 digits)

- **Response:** Returns new user information.

#### 2. GET `/`

- **Description:** Retrieves user information.
- **Response:** Returns user information.

### Order Endpoint

The Order endpoint provides access to order details.

#### Route

- `/api/order`

#### 1. GET `/`

- **Description:** Retrieves details of a specific order.

- **Request Parameters:**

  - `orderId`: Integer (required) - The unique identifier for the order.

- **Response:**

  - `orderId`: Integer - The unique identifier for the order.
  - `productsInfo`: Array - Information about the products included in the order.
  - `totalPrice`: Decimal - The total price of the order.
  - `paymentStatus`: String - The payment status of the order.
  - `customerName`: String - The name of the customer who placed the order.
  - `purchaseDate`: Datetime - The date and time when the order was placed.

### Address Endpoint

The Address endpoint allows users to add or retrieve their address information.

#### Route

- `/api/address`

#### 1. POST `/`

- **Description:** Adds an address for a user.

- **Request Parameters:**
  - `country`: String (required) - The country of the address.
  - `city`: String (required) - The city of the address.
  - `streetAddress`: String (required) - The street address.
  - `state`: String (required) - The state of the address.
  - `zipCode`: String (required) - The zip code of the address.
- **Response:** Returns the details of the added address.

#### 2. GET `/`

- **Description:** Retrieves the user's address.

- **Response:** Returns the details of all of the user's addresses.

## Installation

To get started with the Automotive E-Commerce Platform, follow these steps:

1.  **Clone the repository** to your local machine:

        git clone https://github.com/Abo-Omar-74/AutomotiveEcommercePlatform.git

2.  **Open the project in Visual Studio.**

3.  **Open the Package Manager Console (PMC)** by navigating to `Tools > NuGet Package Manager > Package Manager Console`.

4.  **Run the following command** in the PMC to apply any pending migrations and update the database:

    `update-database`

5.  **Once the database is updated, you can run the program.**

6.  **You can now start testing the API endpoints** using tools like Postman or Swagger UI.

With these steps completed, you should have the Automotive E-Commerce Platform up and running on your local machine, ready for development or testing.

## Contribution

We welcome contributions from the community to improve the Automotive E-Commerce Platform. If you would like to contribute, please follow these steps:

1. Fork the repository.
2. Create a new branch for your feature or bug fix: `git checkout -b feature-name`.
3. Make your changes and commit them: `git commit -m 'Add new feature'`.
4. Push to your branch: `git push origin feature-name`.
5. Submit a pull request to the `main` branch of the original repository.
6. Provide a detailed description of your changes and why they are necessary.

We appreciate your contributions and look forward to working together to make the Automotive E-Commerce Platform even better!
