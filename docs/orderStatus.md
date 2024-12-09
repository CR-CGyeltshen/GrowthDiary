---
title: "Order Status"
categories: [CAP, Work 2]
tags: [CAP]
---

# Order Status

In the context of ecommerce, delivery status is the current state or position of a **customer’s order** as it goes through the delivery process.
It indicates where the order is in the dilivery process, whether it is still being processed, has been dispatched, or has been delivered.

## Different types of order status

[Reference link for order status](https://parcellab.com/glossary/delivery-status/)

[API Endpoint Design Github Repo Link](https://github.com/C-gyeltshen/cocoCommercial_BackEnd.git)

1. **Order Placed**: The order has been succesfully placed by the customer and order has been registerd at the merchant's system.

2. **Order Confirmed**: Process where the **merchant verifies** and **confirms the order** after **receiving payment**.
    - Send an email to the customer confirming the order and providing details like 
    1. Order number
    2. Estimated delivery date
    3. Delivery address
    4. Payment details
    5. Customer information(name) 
2. **Order Processing**: The order is being processed by the merchant. 
    - The merchant will **pick the items** from the warehouse and **pack** them for shipping.
3. **Shipped/Dispatched**: The delivery service now has the order.(Removed)

4. **In transit**: The order is on its way to the customer.

5. **Delivered**: The customer's address has successfully received the package

6. **Canceled**: The order has been canceled by the customer or the merchant due to various reasons.(Customer changed mind, payment issues)

7. **Returned**: The order has been returned by the customer due to various reasons like damaged product, wrong product, etc.

8. **Refunded**: The order has been refunded to the customer due to various reasons like damaged product, wrong product, etc.

