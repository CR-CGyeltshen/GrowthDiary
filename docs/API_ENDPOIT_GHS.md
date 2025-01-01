# API Endpoint Design for GeoHazardSystem

## **1. Master Data Management**

### ENDPOINT: `POST /create/record/:adminID`

* **Description:** Create a new record.

* **Query Logic:** Retrieve the path parameter `adminID` and check the `user role`. Based on the user role and permissions, allow the user to perform the task.

* **Response:**

    * **200 OK:** New record created.
    ```py title="index.py"
    {
        "adminID": "adminID",
        "data": {
            "Code": "Code",
            "Name": "Name",
            "Description": "Description",
            "recordStatus": 1
        }
    }
    ```
    * **404 Not Found:** Missing required fields.
    * **409 Conflict:** Unique `Code` and `Name` already exist.

---

### ENDPOINT: `PATCH /update/dataRecords/:adminID/:id`

* **Description:** Update existing records.

* **Query Logic:** Check the `adminID`. If valid, allow the admin to update the existing record based on a unique identifier like `Code` or `Name`.

* **Response:**

    * **200 OK:** Record updated with the unique identifier `Code` or `Name`.
    ```py title="index.py"
    {
        "adminID": "adminID",
        "recordID": "id",
        "data": {
            "Code": "Code",
            "Name": "Name",
            "Description": "Description",
            "recordStatus": 1
        }
    }
    ```
    * **404 Not Found:** Missing required field `id`.

---

### ENDPOINT: `PATCH /update/activeStatus/:adminID/:id`

* **Description:** Update the `recordStatus` to `0`, indicating deactivation or archiving.

* **Query Logic:** Check the `adminID`. If authorized, find the specific data record with `id` and update the record.

* **Response:**

    * **200 OK:** Data with the `id` successfully updated.
    ```py title="index.py"
    {
        "adminID": "adminID",
        "recordID": "id",
        "data": {
            "Code": "Code",
            "Name": "Name",
            "Description": "Description",
            "recordStatus": 0
        }
    }
    ```
    * **404 Not Found:** Requested data with `recordID` does not exist.

---

## **2. Intensity Scale**

### ENDPOINT: `POST /create/intensityScale/records`

* **Description:** Create a new intensity scale with a unique identifier `Code`.

* **Query Logic:** Check the `adminID`. If authorized, create a new intensity record with a unique identifier `intensityScale`.

* **Response:**

    * **200 OK:** Successfully created a new intensity scale record.
    ```py title="index.py"
    {
        "adminID": "adminID",
        "data": {
            "Code": "Code",
            "IntensityScale": "Intensity Scale",
            "DamageDescription": "Damage Description"
        }
    }
    ```
    * **404 Not Found:** Missing required fields.
    * **409 Conflict:** Unique `Code` already exists.

---

## **3. Survey Questionnaire**

### ENDPOINT: `POST /create/questionnaire/:adminID`

* **Description:** API endpoint for creating a new questionnaire by the admin.

* **Query Logic:** Check the `adminID`. If authorized, allow the admin to create a new question.

* **Response:**

    * **200 OK:** Successfully created a new question.
    ```py title="index.py"
    {
        "adminID": "adminID",
        "data": {
            "Code": "Code",
            "Question": "Question",
            "AnswerType": "AnswerType",
            "Answer": "Answer",
            "Remarks": "Remarks"
        }
    }
    ```
    * **404 Not Found:** Missing required fields.
    * **409 Conflict:** Unique `Code` already exists.

---

### ENDPOINT: `GET /questionnaire/list/:userID?page={pageNumber}&limit={limit}`

* **Description:** Paginated API endpoint for retrieving all the questionnaires.

* **Query Logic:** Query the database to get all the questions.

* **Response:**

    * **200 OK:** Successfully retrieved all `limit` data from `offset`.
    ```py title="index.py"
    {
        "userID": "userID",
        "pageNumber": "pageNumber",
        "limit": "limit",
        "questionList": {
            "Code": "Code",
            "Question": "Question",
            "AnswerType": "AnswerType",
            "Answer": "Answer",
            "Remarks": "Remarks"
        }
    }
    ```
    * **404 Not Found:** Bad request.
    * **409 Conflict:** User `userID` not authorized.

---

### ENDPOINT: `PATCH /update/questionnaire/:id/:userID`

* **Description:** Update the existing questionnaire with corresponding answers.

* **Query Logic:** Check the `userID`. If authorized, allow the user to update the questionnaire with relevant answers.

* **Response:**

    * **200 OK:** Successfully answered the questionnaire with `id`.
    ```py title="index.py"
    {
        "userID": "userID",
        "questionID": "id",
        "questionList": {
            "AnswerType": "AnswerType",
            "Answer": "Answer",
            "Remarks": "Remarks"
        }
    }
    ```
    * **404 Not Found:** Missing required field.
    * **409 Conflict:** Question with the unique identifier `id` does not exist.

 ## **4. Notification Rules**

### **ENDPOINT: `POST /create/rules/:adminID`**

- **Description:** Create new rules for sending notifications.
- **Query Logic:** Verify the `adminID`. If authorized, allow the admin to create a new rule.
- **Response:**
  - **200 OK:** Successfully created a rule with ID `ruleID`.
    ```json
    {
        "adminID": "adminID",
        "data": {
            "MeasurementType": "MeasurementType",
            "Value": "Value",
            "Notification": "Notification"
        }
    }
    ```
  - **404 Not Found:** Missing required fields.
  - **409 Conflict:** Admin with `adminID` is not authorized to create a rule.

---

### **ENDPOINT: `PATCH /update/rules/:adminID/:id`**

- **Description:** Update existing rules.
- **Query Logic:** Verify the `adminID`. If authorized, allow the admin to update the rule with `id`.
- **Response:**
  - **200 OK:** Successfully updated the rule with ID `ruleID`.
    ```json
    {
        "adminID": "adminID",
        "ruleID": "id",
        "data": {
            "MeasurementType": "MeasurementType",
            "Value": "Value",
            "Notification": "Notification"
        }
    }
    ```
  - **404 Not Found:** Rule with `ruleID` does not exist.
  - **409 Conflict:** Admin with `adminID` is not authorized to update the rule.

---

### **ENDPOINT: `DELETE /delete/rules/:adminID/:id`**

- **Description:** Delete an existing rule with a given ID.
- **Query Logic:** Verify the `adminID`. If authorized, allow the admin to delete the rule with `ruleID`.
- **Response:**
  - **200 OK:** Successfully deleted the rule with ID `ruleID`.
    ```json
    {
        "adminID": "adminID",
        "ruleID": "id"
    }
    ```
  - **404 Not Found:** Rule with `ruleID` does not exist.
  - **409 Conflict:** Admin with `adminID` is not authorized to delete the rule.

---

### **ENDPOINT: `POST /send/notification/:adminID`**

- **Description:** Send notifications if the intensity level exceeds the value provided in the rules.
- **Query Logic:** Verify the `adminID`. If authorized, allow the admin to send notifications to the respective stakeholders.
- **Response:**
  - **200 OK:** Successfully delivered the notification.
    ```json
    {
        "adminID": "adminID",
        "recipients": ["17828281", "77267272", "17282828"],
        "data": {
            "type": "SMS",
            "title": "Hazard Alarm",
            "Notification": "Notification"
        }
    }
    ```
  - **404 Not Found:** Missing required fields.
  - **409 Conflict:** Admin with `adminID` is not authorized to send notifications.

---

## **5. Felt Report**

### **ENDPOINT: `POST /create/surveyQuestion/:adminID`**

- **Description:** Create "felt like report" questions for the public.
- **Query Logic:** Verify the `adminID`. If authorized, allow the admin to create new questions.
- **Response:**
  - **200 OK:** Successfully created a new question for the "felt like report".
    ```json
    {
        "adminID": "adminID",
        "data": {
            "Question": "Question",
            "Options": "Options",
            "Remarks": "Remarks"
        }
    }
    ```
  - **404 Not Found:** Missing required fields.
  - **409 Conflict:** Unique code `Code` already exists.

---

### **ENDPOINT: `GET /feltReport/list?page={pageNumber}&limit={limit}`**

- **Description:** Paginated API endpoint for retrieving all the questions for the "felt like report".
- **Query Logic:** Query the database to get all the questions.
- **Response:**
  - **200 OK:** Successfully retrieved `limit` data from `offset`.
    ```json
    {
        "pageNumber": "pageNumber",
        "limit": "limit",
        "feltLikeReport": [
            {
                "Question": "Question",
                "Options": "Options",
                "Remarks": "Remarks"
            }
        ]
    }
    ```
  - **404 Not Found:** Bad request.

---

### **ENDPOINT: `PATCH /update/feltReport/:id`**

- **Description:** Update the existing "felt like report" with the corresponding answer.
- **Query Logic:** Update the answer to the corresponding question with the given question ID `id`.
- **Response:**
  - **200 OK:** Successfully answered the questionnaire with ID `id`.
    ```json
    {
        "questionID": "id",
        "feltLikeReport": {
            "Options": "Options",
            "Remarks": "Remarks"
        }
    }
    ```
  - **404 Not Found:** Missing required fields.
  - **409 Conflict:** Question with the unique identifier `id` does not exist.

---

## **6. SMS Stakeholders**

### **ENDPOINT: `POST /create/stakeholders/:adminID`**

- **Description:** Create new stakeholders.
- **Query Logic:** Verify the `adminID`. If authorized, allow the admin to create new stakeholders with a valid phone number.
- **Response:**
  - **200 OK:** Successfully created a stakeholder with the phone number `TelephoneNo`.
    ```json
    {
        "adminID": "adminID",
        "data": {
            "Name": "Name",
            "TelephoneNo": "TelephoneNo",
            "Description": "Description"
        }
    }
    ```
  - **404 Not Found:** Missing required fields.
  - **409 Conflict:** Phone number `TelephoneNo` already exists.

---

### **ENDPOINT: `PATCH /update/stakeholders/:userID`**

- **Description:** Update the details of the stakeholder.
- **Query Logic:** Verify the `userID`. If authorized, allow the stakeholder to update their information.
- **Response:**
  - **200 OK:** Successfully updated the stakeholder information.
    ```json
    {
        "userID": "userID",
        "data": {
            "Name": "Name",
            "TelephoneNo": "TelephoneNo",
            "Description": "Description"
        }
    }
    ```
  - **404 Not Found:** Invalid phone number `TelephoneNo`.
  - **409 Conflict:** Phone number `TelephoneNo` already exists.

---

### **ENDPOINT: `DELETE /delete/stakeholders/:adminID`**

- **Description:** Delete the details of a stakeholder.
- **Query Logic:** Verify the `adminID`. If authorized, allow the admin to delete the stakeholder.
- **Response:**
  - **200 OK:** Successfully deleted the stakeholder `Name`.
    ```json
    {
        "adminID": "adminID",
        "data": {
            "Name": "Name",
            "TelephoneNo": "TelephoneNo",
            "Description": "Description"
        }
    }
    ```
  - **404 Not Found:** Invalid phone number `TelephoneNo`.
  - **409 Conflict:** Phone number `TelephoneNo` already exists.

## **7. Earthquake Notification**

### **ENDPOINT: `POST /send/notification/public/:adminID`**

- **Description:** Send a notification to the public when the input field `SMS To` is set to `true`.
- **Query Logic:** Check the `adminID`. If authorized, allow the admin to send notifications to the public.
- **Response:**
  - **200 OK:** Successfully delivered SMS to the general public.
    ```json
    {
        "adminID": "adminID",
        "data": {
            "smsTo": true,
            "Message": "Message"
        }
    }
    ```
  - **404 Not Found:** Missing required fields.
  - **409 Conflict:** Admin with the `adminID` is not authorized to send notifications.

---

### **ENDPOINT: `POST /send/notification/stakeholders/:adminID`**

- **Description:** Send a notification to all stakeholders when the input field `SMS To` is set to `true`.
- **Query Logic:** Check the `adminID`. If authorized, allow the admin to send notifications to all stakeholders.
- **Response:**
  - **200 OK:** Successfully delivered SMS to all stakeholders.
    ```json
    {
        "adminID": "adminID",
        "data": {
            "smsTo": true,
            "Message": "Message"
        }
    }
    ```
  - **404 Not Found:** Missing required fields.
  - **409 Conflict:** Admin with the `adminID` is not authorized to send notifications.

---

## **8. Landslide Inventory**

### **ENDPOINT: `POST /create/landslide/record/:adminID`**

- **Description:** Create a new landslide inventory record.
- **Query Logic:** Verify the `adminID`. If authorized, allow the admin to create a new landslide record.
- **Response:**
  - **200 OK:** Successfully created a new landslide inventory record.
    ```json
    {
        "adminID": "adminID",
        "data": {
            "Location": "Location",
            "Date": "Date",
            "Description": "Description",
            "Severity": "Severity"
        }
    }
    ```
  - **404 Not Found:** Missing required fields.
  - **409 Conflict:** Admin with the `adminID` is not authorized to create records.

---

### **ENDPOINT: `GET /landslide/records?page={pageNumber}&limit={limit}`**

- **Description:** Retrieve paginated landslide records.
- **Query Logic:** Fetch all records and return results based on the `pageNumber` and `limit`.
- **Response:**
  - **200 OK:** Successfully retrieved records.
    ```json
    {
        "pageNumber": "pageNumber",
        "limit": "limit",
        "records": [
            {
                "Location": "Location",
                "Date": "Date",
                "Description": "Description",
                "Severity": "Severity"
            }
        ]
    }
    ```
  - **404 Not Found:** No records found.

---

### **ENDPOINT: `PATCH /update/landslide/record/:adminID/:recordID`**

- **Description:** Update an existing landslide inventory record.
- **Query Logic:** Verify the `adminID`. If authorized, allow the admin to update the record with `recordID`.
- **Response:**
  - **200 OK:** Successfully updated the record.
    ```json
    {
        "adminID": "adminID",
        "recordID": "recordID",
        "data": {
            "Location": "Updated Location",
            "Date": "Updated Date",
            "Description": "Updated Description",
            "Severity": "Updated Severity"
        }
    }
    ```
  - **404 Not Found:** Record with `recordID` does not exist.
  - **409 Conflict:** Admin with the `adminID` is not authorized to update records.

---

### **ENDPOINT: `DELETE /delete/landslide/record/:adminID/:recordID`**

- **Description:** Delete an existing landslide inventory record.
- **Query Logic:** Verify the `adminID`. If authorized, allow the admin to delete the record with `recordID`.
- **Response:**
  - **200 OK:** Successfully deleted the record.
    ```json
    {
        "adminID": "adminID",
        "recordID": "recordID"
    }
    ```
  - **404 Not Found:** Record with `recordID` does not exist.
  - **409 Conflict:** Admin with the `adminID` is not authorized to delete records.



