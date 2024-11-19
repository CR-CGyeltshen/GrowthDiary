---
title: "API Endpoint Design"
categories: [CAP, Work 1]
tags: [CAP]
---

## Entity Relationships

### [Database Schema](https://lucid.app/lucidchart/ab48d5c6-8d3b-4d96-974c-b9e08c1514fa/edit?invitationId=inv_51cb4802-82c6-40a9-8815-9fa714dcf867&page=0_0#)

- **Merchant and Store**: One-to-One (Each merchant can create only one store using a single email).
- **Customer and Order**: One-to-Many (A customer can make multiple orders, but each order is associated with only one customer).
- **Order and Payment**: One-to-One (An order can have only one payment, and each payment corresponds to one order).
- **Order and OrderItems**: One-to-Many (An order can contain multiple order items, but each order item belongs to only one order).
- **OrderItems and Product**: One-to-One (An order item can have only one product, and each product can be associated with a single order item).
- **Store and Order**: One-to-Many (A store can have multiple orders, but each order is associated with only one store).
- **Store and Product**: One-to-Many (A store can post multiple products, but each product is associated with only one store).

## Functional Requirements

**Platform User Types:**
1. **Merchant (or Store Owner)**
2. **Customer**

### Merchant Capabilities
- **View** the list of orders.
- **Add** new orders.
- **Update** order statuses.
- **View** products.
- **Add** products.
- **Edit** products.
- **Update** store details (name, description, image, dzongkhag, gewog, village).
- Ensure order details are **updated** when a user modifies order information.

### Customer Capabilities
- **View** customer profile.
- **View** list of stores.
- **View** orders placed.
- **View** items in cart.
- **Edit** profile (name, image, phone number, location).
- **Add** new orders.
- **Add** items to cart.
- **Edit** existing orders.

## API Endpoints

### Endpoint: `Post /create/merchant/stores`
- **Description**: Create a new store as soon as a new merchnat is been registered.
- **Query Logic**: Create a new record to the new merchant table with a unique `merchnat_id` and with same `merchnat_id`, create a new store to that respected merchant.
- **Response**:
    - **200 OK**: Returns a success Message with status code 200

      ```json
      {
            "merchant_id": "{merchant_id}",
            "reault":
                {
                    "Name": name,
                    "Email": email,
                    "Password": password,
                    "Dzongkhag": dzongkhag,
                    "Gewog": gewog,
                    "Village": village
                },
            "store_id":"{store_id}",

            "data":{
                "storeName": storeName,
                "storeDescription":storeDescription,
                "storeDzongkhag":storeDzongkhag,
                "storeGewog":storeGewog,
                "storeVillage":storeVillage,
                "merchantId":result.id
                }
      }
      ```
    - **404 Not Found**: Returns person with the above email already exists.

### Endpoint: `GET /store/{store_id}/orders`
- **Description**: Retrieve orders placed by customers at a specific store.
- **Query Logic**: Query the database for orders associated with the specified `store_id`.
- **Response**:
    - **200 OK**: Returns a list of orders with relevant details:

      ```json
      {
          "store_id": "{store_id}",
          "orders": [
              {
                  "customer_name": true,
                  "total_amount": true,
                  "items": true,
                  "order_date": true,
                  "fulfillment_date": true,
                  "status": true,
                  "location": true,
                  "location_description": true,
                  "phone_number": true
              }
          ]
      }
      ```
    - **404 Not Found**: Returns "Store not found" or "No orders found for store" if applicable.

---

### Endpoint: `POST /store/{store_id}/orders`
- **Description**: Add a new order manually by the store owner.
- **Query Logic**: Inserts a new order record for the specified `store_id`.
- **Response**:
    - **200 OK**: Creates a new order with the following details:

      ```json
      {
          "store_id": "{store_id}",
          "order": {
              "total_amount": total_amount,
              "order_date": order_date,
              "orderItems": orderItems,
              "status": 0,
              "dzongkhag": dzongkhag,
              "gewog": gewog,
              "village": village,
              "address_description": address_description,
              "phone_number": phone_number,
              "latitude": latitude,
              "longitude": longitude,
              "note_from_orderer": note_from_orderer
          }
      }
      ```
    - **400 Bad Request**: Returns "Incomplete order details, please provide complete information."

---

### Endpoint: `PATCH /store/{store_id}/orders/{order_id}`
- **Description**: Update the status of a specific order when delivery is completed.
- **Query Logic**: Updates the order status for the specified `order_id` under `store_id`.
- **Response**:
    - **200 OK**: Successfully updates the order status to `Delivered` for `order_id`:

      ```json
      {
          "order_id": "{order_id}",
          "status": 1
      }
      ```
    - **404 Not Found**: Returns "Order not found."

---

### Endpoint: `GET /store/{store_id}/products`
- **Description**: Retrieve a list of products for a specific store identified by `store_id`.
- **Query Logic**: Queries the database for products associated with the specified `store_id`.
- **Response**:
    - **200 OK**: Returns a list of products with relevant details:

      ```json
      {
          "store_id": "{store_id}",
          "products": [
              {
                  "product_name": true,
                  "product_price": true,
                  "description": true,
                  "image_url": true,
                  "stock_quantity": true,
                  "created_at": true
              }
          ]
      }
      ```
    - **404 Not Found**: Returns "Products not found" or "No products found for the given store" if applicable.

---

### Endpoint: `POST /store/{store_id}/products`
- **Description**: Add a new product to the specified store.
- **Query Logic**: Adds a new product to the `products` table associated with `store_id`.
- **Response**:
    - **200 OK**: Successfully adds a new product with the provided details:

      ```json
      {
          "store_id": "{store_id}",
          "product": {
              "product_name": product_name,
              "product_price": product_price,
              "description": description,
              "image_url": image_url,
              "stock_quantity": stock_quantity,
              "created_at": created_at
          }
      }
      ```
    - **404 Not Found**: Returns "Store not found" or "Unable to add product" if applicable.

---

### Endpoint: `GET /store/{store_id}/orders`
- **Description**: Retrieve orders placed by customers at a specific store.
- **Query Logic**: Query the database for orders associated with the specified `store_id`.
- **Response**:
    - **200 OK**: Returns a list of orders with relevant details:

      ```json
      {
          "store_id": "{store_id}",
          "orders": [
              {
                  "customer_name": true,
                  "total_amount": true,
                  "items": true,
                  "order_date": true,
                  "fulfillment_date": true,
                  "status": true,
                  "location": true,
                  "location_description": true,
                  "phone_number": true
              }
          ]
      }
      ```
    - **404 Not Found**: Returns "Store not found" or "No orders found for store" if applicable.

---

### Endpoint: `POST /store/{store_id}/orders`
- **Description**: Add a new order manually by the store owner.
- **Query Logic**: Inserts a new order record for the specified `store_id`.
- **Response**:
    - **200 OK**: Creates a new order with the following details:

      ```json
      {
          "store_id": "{store_id}",
          "order": {
              "total_amount": total_amount,
              "order_date": order_date,
              "orderItems": orderItems,
              "status": 0,
              "dzongkhag": dzongkhag,
              "gewog": gewog,
              "village": village,
              "address_description": address_description,
              "phone_number": phone_number,
              "latitude": latitude,
              "longitude": longitude,
              "note_from_orderer": note_from_orderer
          }
      }
      ```
    - **400 Bad Request**: Returns "Incomplete order details, please provide complete information."

---

### Endpoint: `PATCH /store/{store_id}/orders/{order_id}`
- **Description**: Update the status of a specific order when delivery is completed.
- **Query Logic**: Updates the order status for the specified `order_id` under `store_id`.
- **Response**:
    - **200 OK**: Successfully updates the order status to `Delivered` for `order_id`:

      ```json
      {
          "order_id": "{order_id}",
          "status": 1
      }
      ```
    - **404 Not Found**: Returns "Order not found."

---

### Endpoint: `GET /store/{store_id}/products`
- **Description**: Retrieve a list of products for a specific store identified by `store_id`.
- **Query Logic**: Queries the database for products associated with the specified `store_id`.
- **Response**:
    - **200 OK**: Returns a list of products with relevant details:

      ```json
      {
          "store_id": "{store_id}",
          "products": [
              {
                  "product_name": true,
                  "product_price": true,
                  "description": true,
                  "image_url": true,
                  "stock_quantity": true,
                  "created_at": true
              }
          ]
      }
      ```
    - **404 Not Found**: Returns "Products not found" or "No products found for the given store" if applicable.

---

### Endpoint: `POST /store/{store_id}/products`
- **Description**: Add a new product to the specified store.
- **Query Logic**: Adds a new product to the `products` table associated with `store_id`.
- **Response**:
    - **200 OK**: Successfully adds a new product with the provided details:

      ```json
      {
          "store_id": "{store_id}",
          "product": {
              "product_name": product_name,
              "product_price": product_price,
              "description": description,
              "image_url": image_url,
              "stock_quantity": stock_quantity,
              "created_at": created_at
          }
      }
      ```
    - **404 Not Found**: Returns "Store not found" or "Unable to add product" if applicable.

---


### Endpoint: `PATCH /store/{store_id}`
- **Description**: Update store details for a specific store.
- **Query Logic**: Updates the specified fields (name, description, image, dzongkhag, gewog, village) for the given `store_id`.
- **Response**:
    - **200 OK**: Successfully updates the store details:

      ```json
      {
          "store_id": "{store_id}",
          "updated_fields": {
                "name": "Updated Store Name",
                "description": "Updated Description",
                "image": "image_url",
                "dzongkhag": "updated_dzongkhag",
                "gewog": "updated_gewog",
                "village": "updated_village"
          }
      }
      ```
    - **404 Not Found**: Returns "Store not found."

---

### Endpoint: `PATCH /orders/{order_id}` (work)
- **Description**: Update order details when a user modifies their order information.
- **Query Logic**: Updates order information based on changes provided for the specified `order_id`.
- **Response**:
    - **200 OK**: Successfully updates order details:

      ```json
      {
          "order_id": "{order_id}",
          "updated_order": {
                "order_items": [ /* updated items */ ],
                "total_amount": "updated_total",
                "delivery_address": "updated_address",
                "note": "updated_note"
          }
      }
      ```
    - **404 Not Found**: Returns "Order not found."

---

### Customer-Specific Endpoints

---

### Endpoint: `GET /customer/{customer_id}`
- **Description**: Retrieve profile information for a specific customer.
- **Query Logic**: Retrieves customer details for the given `customer_id`.
- **Response**:
    - **200 OK**: Returns customer profile details:

      ```json
      {
          "customer_id": "{customer_id}",
          "profile": {
                "name": "Customer Name",
                "image": "image_url",
                "phone_number": "phone_number",
                "dzongkhag": "dzongkhag",
                "gewog": "gewog",
                "village": "village"
          }
      }
      ```
    - **404 Not Found**: Returns "Customer not found."

---

### Endpoint: `GET /stores`
- **Description**: Retrieve a list of all available stores.
- **Query Logic**: Retrieves all stores with basic details.
- **Response**:
    - **200 OK**: Returns a list of stores:

      ```json
      {
          "stores": [
              {
                  "store_id": "store_id_1",
                  "name": "Store Name",
                  "description": "Store Description",
                  "image": "image_url",
                  "dzongkhag": "dzongkhag",
                  "gewog": "gewog",
                  "village": "village"
                
              }
          ]
      }
      ```

---

### Endpoint: `GET /customer/{customer_id}/orders`
- **Description**: Retrieve a list of orders placed by a specific customer.
- **Query Logic**: Retrieves orders associated with the specified `customer_id`.
- **Response**:
    - **200 OK**: Returns a list of orders:

      ```json
      {
          "customer_id": "{customer_id}",
          "orders": [
              {
                  "order_id": "order_id",
                  "total_amount": "total",
                  "status": "status",
                  "order_date": "order_date",
                  "items": [ /* items ordered */ ]
              }
          ]
      }
      ```

---

### Endpoint: `PATCH /customer/{customer_id}`
- **Description**: Edit profile information for a specific customer.
- **Query Logic**: Updates fields (name, image, phone number, location) for the given `customer_id`.
- **Response**:
    - **200 OK**: Successfully updates profile details:

      ```json
      {
          "customer_id": "{customer_id}",
          "updated_profile": {
              "name": "Updated Name",
              "image": "image_url",
              "phone_number": "phone_number",
              "dzongkhag": "dzongkhag",
              "gewog": "gewog",
              "village": "village"
          }
      }
      ```
    - **404 Not Found**: Returns "Customer not found."

---

### Endpoint: `POST /stores/{store_id}/customer/{customer_id}/orders`
- **Description**: Place a new order for the specified customer to a specific store.
- **Query Logic**: Adds a new order for the specified `customer_id` with order details.
- **Response**:
    - **200 OK**: Successfully places a new order:

      ```json
      {
          "store_id": "{store_id}",
          "customer_id":{customer_id},
          "order": {
              "order_id": "order_id",
              "total_amount": "total",
              "order_date":"order_date",
              "fullfillment_date":"fullfillment_date",
              "dzongkhag": "dzongkhag",
              "gewog": "gewog",
              "village": "village",
              "address_description":"address_description",
              "phone_number":"phone_number",
              "NOTE_from_orderer":"NOTE_from_orderer",
              "items": [ /* ordered items */ ],
              "status": "Pending"
          }
      }
      ```
    - **400 Bad Request**: Returns "Incomplete order details."

---


### Endpoint: `PATCH /customer/{customer_id}/orders/{order_id}`
- **Description**: Edit an existing order placed by a customer.
- **Query Logic**: Updates specific order details for the specified `order_id` under `customer_id`.
- **Response**:
    - **200 OK**: Successfully updates the order:

      ```json
      {
          "order_id": "{order_id}",
          "updated_order": {
              "items": [ /* updated items */ ],
              "total_amount": "updated_total",
              "delivery_address": "updated_address",
              "note": "updated_note"
          }
      }
      ```
    - **404 Not Found**: Returns "Order not found."
