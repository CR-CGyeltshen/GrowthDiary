---
title: "Capstone Discussion - 30th December"
categories: [Capstone, Work]
tags: [Capstone]
---

# Capstone Discussion - 30th December

## **Agenda**
This discussion will cover the progress, ongoing tasks, and upcoming work related to the capstone project. Key areas include database schema design, API implementation, and challenges in the current workflow.

---

## **Work Completed**

1. **Database Schema Design**  
   - Created and finalized schema based on project requirements.

2. **API Endpoint Design**  
   - Defined and structured endpoints for seamless integration.

3. **Implementation of API Endpoints**  
   - Developed and tested API endpoints to ensure functionality.

4. **Corrected Supervisor Recommendations**:  
   - **Edge Case**: Adjusted logic to handle product price changes in the `orderItems` table. 
   - [GitHub Repo Link](https://github.com/C-gyeltshen/cocoCommercial_BackEnd.git) 
   - **Order Status**: Updated `orderStatus` datatype to `ENUM` and introduced new statuses.
   - [orderStatus.md](https://growthdiary-srfw.onrender.com/orderStatus/)
   
---

## **Work in Progress**

1. **Frontend Reference Design**  
   - Creating Figma designs for frontend layout and features.
   - [Figma Link](https://www.figma.com/design/VZJhnYX82SOAtXpGqVjABc/Cococart?node-id=0-1&node-type=canvas&t=ixypeR7rI3cHfmYs-0)

2. **Authentication Integration**  
   - Setting up authentication flow using Auth0.

---

## **Work to be Completed**

1. **Frontend Implementation**  
   - Develop the frontend based on Figma designs.

2. **Auth0 Functionality**  
   - Integrate Auth0 into the existing backend and frontend workflows.

3. **Protected Routes**  
   - Secure specific routes for authorized users only.

4. **Cloud Storage Integration**  
   - Store images in cloud storage to improve performance and accessibility.

5. **Payment Gateway Implementation**  
   - Set up and configure a payment gateway for transaction processing.

---

## **Points for Discussion**

1. **Order Items Table**:  
   - Cross-check the implementation, focusing on how edge cases (e.g., product price changes) are handled.

2. **Manually Added Products**:  
   - Discuss how to manage products manually added to the `orderItems` table by the store owner.

3. **Order Status Updates**:  
   - When to update the `orderStatus` in the `order` table.

4. **Payment Gateway**:  
   - Explore potential solutions and strategies for integrating the payment gateway effectively.
