# Brazillian E-Commerce Dataset
(Downloaded from [Kaggle](https://www.kaggle.com/olistbr/brazilian-ecommerce))



[TOC]



### About the data:

> The dataset has information of 100k orders from 2016 to 2018 made at multiple marketplaces in Brazil. Its features allows viewing an order from multiple dimensions: from order status, price, payment and freight performance to customer location, product attributes and finally reviews written by customers. We also released a geolocation dataset that relates Brazilian zip codes to lat/lng coordinates.

### About Olist.com

> This dataset was generously provided by Olist, the largest department store in Brazilian marketplaces. Olist connects small businesses from all over Brazil to channels without hassle and with a single contract. Those merchants are able to sell their products through the Olist Store and ship them directly to the customers using Olist logistics partners.

### Attention

- An order might have multiple items.
- Each item might be fulfilled by a distinct seller.
- All text identifying stores and partners where replaced by the names of Game of Thrones great houses.

### Schema

<img src="figures/ds-schema.png">



### Description of columns

|   Dataset   | Column                        | Description                                                  |
| :---------: | ----------------------------- | ------------------------------------------------------------ |
|  *Orders*   | order_id                      | unique identifier of the order.                              |
|  *Orders*   | customer_id                   | key to the customer dataset. Each order has a unique customer_id. |
|  *Orders*   | order_status                  | Reference to the order status (delivered, shipped, etc).     |
|  *Orders*   | order_purchase_timestamp      | Shows the purchase timestamp.                                |
|  *Orders*   | order_approved_at             | Shows the payment approval timestamp.                        |
|  *Orders*   | order_delivered_carrier_date  | Shows the order posting timestamp. When it was handled to the logistic partner. |
|  *Orders*   | order_delivered_customer_date | Shows the actual order delivery date to the customer.        |
|  *Orders*   | order_estimated_delivery_date | Shows the estimated delivery date that was informed to customer at the purchase moment. |
|     ---     | ---                           | ---                                                          |
| *Payments*  | payment_sequential            | a customer may pay with more than one payment method. If so, a sequence will be created to accommodate all payments. |
| *Payments*  | payment_type                  | method of payment chosen by the customer.                    |
| *Payments*  | payment_installments          | number of installments chosen by the customer.               |
| *Payments*  | payment_value                 | transaction value.                                           |
|     ---     | ---                           | ---                                                          |
|  *Reviews*  | review_id                     | unique review identifier                                     |
|  *Reviews*  | review_score                  | Note ranging from 1 to 5 given by the customer on a satisfaction survey. |
|  *Reviews*  | review_comment_title          | Comment title from the review left by the customer, in Portuguese. |
|  *Reviews*  | review_comment_message        | Comment message from the review left by the customer, in Portuguese. |
|  *Reviews*  | review_creation_date          | Shows the date in which the satisfaction survey was sent to the customer. |
|  *Reviews*  | review_answer_timestamp       | Shows satisfaction survey answer timestamp.                  |
|     ---     | ---                           | ---                                                          |
|   *Items*   | order_item_id                 | sequential number identifying number of items included in the same order. |
|   *Items*   | product_id                    | product unique identifier                                    |
|   *Items*   | seller_id                     | seller unique identifier                                     |
|   *Items*   | shipping_limit_date           | Shows the seller shipping limit date for handling the order over to the logistic partner. |
|   *Items*   | price                         | item price                                                   |
|   *Items*   | freight_value                 | item freight value item (if an order has more than one item the freight value is splitted between items) |
|     ---     | ---                           | ---                                                          |
| *Products*  | product_category_name         | root category of product, in Portuguese.                     |
| *Products*  | product_name_lenght           | number of characters extracted from the product name.        |
| *Products*  | product_description_lenght    | number of characters extracted from the product description. |
| *Products*  | product_photos_qty            | number of product published photos                           |
| *Products*  | product_weight_g              | product weight measured in grams.                            |
| *Products*  | product_length_cm             | product length measured in centimeters.                      |
| *Products*  | product_height_cm             | product height measured in centimeters.                      |
| *Products*  | product_width_cm              | product width measured in centimeters.                       |
|     ---     | ---                           | ---                                                          |
| *Customers* | customer_id                   | key to the orders dataset. Each order has a unique customer_id. |
| *Customers* | customer_unique_id            | unique identifier of a customer.                             |
| *Customers* | customer_zip_code_prefix      | first five digits of customer zip code                       |
| *Customers* | customer_city                 | customer city name                                           |
| *Customers* | customer_state                | customer state                                               |
|     ---     | ---                           | ---                                                          |
|  *Sellers*  | seller_id                     | seller unique identifier                                     |
|  *Sellers*  | seller_zip_code_prefix        | first 5 digits of seller zip code                            |
|  *Sellers*  | seller_city                   | seller city name                                             |
|  *Sellers*  | seller_state                  | seller state                                                 |



### Questions:

- Which product sells the most? Do they profit more from cheap or from expensive products?
- Do orders vary throughout the year?
- How much does the average customer spend? Does it vary with geographical location? 
- How much does the average shop sell? Does it vary with geographical location?



## Which products sell best?

The products dataset shows that **32951** products were sold in 100k orders. Are there products that sell more than others? Or were they all sold approximately 3 times?

We calculated the probability of each product being sold and show it here in a 2d hexbin histogram with price. The colors of each bin are determined by the average revenue generated by the products in each bin.

<img src="C:\Users\Zaca\Documents\GitHub\projects\brazilian-ecommerce\figures\product_probability.png" alt="product_probability" style="zoom: 33%;" />

Conclusions: Olist makes more