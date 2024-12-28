# API endpoint desig for GeoHasardSystem

## **Master Data Management**


### ENDPOINT: `POST  /create/record/:adminID`

* **Description :** Create a new record

* **Query Logic :** Rrtrive the path parameter `id` and check the `user role`. Based on the user_role and the permission granted to the user, allow the user to perform its task.

* **Response:**

    * **200 OK :** New record created.
    ```py title="index.py"
    {
        "adminID":"id",
        "data":
            {
                "Code": "Code",
                "Name": "Name",
                "Description": "Description",
                "recordStatus":1
            }
    }
    ```
    * **404 - Not Found :** Missing Required Fields.
    * **409 :** Unique Code and Name already exist.

### ENDPOINT: `PATCH  /update/dataRecords/:adminID/:id`

* **Description :** Update the existing records
* **Query Logic :** Check the `adminID` and if it is valid, allow the admin to update the existing recorder based on a unique identifire like `Code` or `Name`.

* **Response:**
    * **200 OK :** Record updated with the unique identifier `Code` or `Name`.
    ```py title="index.py"
    {
        "adminID":"adminID",
        "record_id":"id",
        "data":
            {
                "Code":"Code",
                "Name":"Name",
                "Description":"Descripiton",
                "recordStatus":1
            }
    }
    ```
    * **404 - Not Found :** Missing Required Fields `id`.

### ENDPOINT: `PATCH  /update/activeStatus/:adminID/:id`
* **Description :** Update the recordStatus to `0` indicating deactive or archived.
* **Query Logic :** Check the `adminID`, if the adminID is authorized, find the specific data record with `id` and update the record.

* **Response:**
    * **200 OK :** Data with the id `id` is succesfully updated.
    ```py title="index.py"

    {
        "adminID":"adminID",
        "recordID":"id",
        "data":
            {
                "Code":"Code",
                "Name":"Name",
                "Description":"Descripiton",
                "recordStatus":0
            }
    }
    ```
    * **404 - Not Found :** Requested data with the `recordID` does not exist.

## **Intensity Scale**

### ENDPOINT: `POST  /create/intensityScale/records`
* **Description :** Create a new intensityScale with a unique indentifier `Code`.
* **Query Logic :** Check the `adminID`, if the adminID is authorized, create a new intensity record with a unique identifier `intensityScale`.

* **Response:**
    * **200 OK :** Succefully created a new intensityScale record with an id `intensityScale`.
    ```py title="index.py"

    {
        "adminID":"adminID",
        "data":
            {
                "Code":"Code",
                "IntensityScale":"Intensity Scale ",
                "DamageDescription":"DamageDescription"
            }
    }
    ```
    * **404 - Not Found :** Missing Required Fields.
    * **409 :** Unique Code `Code` already exist.


## **Survey Questionnaire**

### ENDPOINT: `POST  /create/questionnaire/:adminID`

* **Description :** API endpoint for creating a new questionnaire by the admin.
* **Query Logic :** Check the `adminID`, if it is autorized then allow the admin to create a new question.
* **Response:**
    * **200 OK :** Succesfully created a new question.
    ```py title="index.py"

    {
        "adminID":"adminID",
        "data" : 
            {
                "Code":"Code",
                "Question":"Question",
                "AnswerType":"AnswerType",
                "Answer":"Answer",
                "Remarks":"Remarks"
            }
    }
    ```
    * **404 - Not Found :** Missing Required Fields.
    * **409 :** Unique Code `Code` already exist.

### ENDPOINT: `GET  /questionnaire/list/:userID?page={pageNumber}%limit={limit}`

* **Description :** Paginated API endpoint for retriving all the questionnairs. 
* **Query Logic :** Query database to get all the questions.
* **Response:**
    * **200 OK :** Succesfully retrivell all `limit` data from `offset`. 
    ```py title="index.py"

    {
        "userID":"userID",
        "pageNumber":"pageNumber",
        "limit":"limit",
        "questionList": 
            {
                "Code":"Code",
                "Question":"Question",
                "AnswerType":"AnswerType",
                "Answer":"Answer",
                "Remarks":"Remarks"
            }
    }
    ```
    * **404 - Not Found :** Bed request.
    * **409 :** User `userID` to authorized.


### ENDPOINT: `PATCH  /update/questionnaire/:id/:userID`

* **Description :** Update the existing questionnair with corresponding answer. 
* **Query Logic :** Check the `userID`, if it is autorized then allow the user to update the questionnair with relivent answer.
* **Response:**
    * **200 OK :** Succesfully answered the questionnairs with id `id`. 
    ```py title="index.py"

    {
        "userID":"userID",
        "questionID":"id",
        "questionList" : 
            {
                "AnswerType":"AnswerType",
                "Answer":"Answer",
                "Remarks":"Remarks"
            }
    }
    ```
    * **404 - Not Found :** Missing required field.
    * **409 :** Question with the unique identifier `id` do not exist.

 
## **Notification Rules**


### ENDPOINT: `POST  /create/rules/:adminID`

* **Description :** Create new rules for sending notification.
* **Query Logic :** Check the `adminID`, if it is authorized then allow the admin to `create` a new rule.
* **Response:**
    * **200 OK :** Succesfully created a rule with id `ruleID`. 
    ```py title="index.py"

    {
        "adminID":"adminID",
        "data": 
            {
                "MeasurementType":"MeasurementType",
                "Value":"Value",
                "Notification":"Notification"
            }
    }
    ```
    * **404 - Not Found :** Missing Required Field.
    * **409 :** Admin with the `adminID` is not authorized to create rule.



### ENDPOINT: `PATCH  /update/rules/:adminID/:id`

* **Description :** Update the existing rules.
* **Query Logic :** Check the `adminID`, if it is authorized then allow the admin to `update` a rule.
* **Response:**
    * **200 OK :** Succesfully updated a rule with id `ruleID`. 
    ```py title="index.py"

    {
        "adminID":"adminID",
        "ruleID":"id",
        "data" : 
            {
                "MeasurementType":"MeasurementType",
                "Value":"Value",
                "Notification":"Notification"
            }
    }
    ```
    * **404 - Not Found :** Rule with the id `ruleID` do not exist.
    * **409 :** Admin with the `adminID` is not authorized to update rule.



### ENDPOINT: `DELETE  /delete/rules/:adminID/:id`

* **Description :** Delete a existing rule with a given id.
* **Query Logic :** Check the `adminID`, if it is authorized then allow the admin to `delete` a rule with a given `ruleID.`
* **Response:**
    * **200 OK :** Succesfully deleted a rule with id `ruleID`. 
    ```py title="index.py"

    {
        "adminID":"adminID",
        "where":{
            "adminID":"id"
        }
    }
    ```
    * **404 - Not Found :** Rule with the id `ruleID` do not exist.
    * **409 :** Admin with the `adminID` is not authorized to update rule.


### ENDPOINT: `POST  /send/notificaiton/:adminID`

* **Description :** Send notification if the intensity level exceeds the value provided in the rules.
* **Query Logic :** Check the `adminID`, if it is authorized then allow the admin to `send` notification to all the respective stackholders.
* **Response:**
    * **200 OK :** Succesfully delivered the notification. 
    ```py title="index.py"

    {
        "adminID":"adminID",
        "where":{
            "recipientPhoneNumber": ["17828281", "77267272","17282828"]
        },
        "data": 
            {
                "type":"SMS",
                "title":"Hazard Alarm",
                "Notification":"Notification"
            }
    }
    ```
    * **404 - Not Found :** Missing Required Field.
    * **409 :** Admin with the `adminID` is not authorized to create rule.


## **Felt Report**

### ENDPOINT: `POST  /create/servayQuestion/:adminID`

* **Description :** Create `felt like report` questions for public.
* **Query Logic :** Check the `adminID`, if it is autorized then allow the admin to create a new questions.
* **Response:**
    * **200 OK :** Succesfully created a new questions for `felt like report`.
    ```py title="index.py"

    {
        "adminID":"adminID",
        "data" : 
            {
                "Question":"Question",
                "Options":"Options",
                "Remarks":"Remarks"
            }
    }
    ```
    * **404 - Not Found :** Missing Required Fields.
    * **409 :** Unique Code `Code` already exist.


### ENDPOINT: `GET  /feltReport/list?page={pageNumber}%limit={limit}`

* **Description :** Paginated API endpoint for retriving all the questions for `felt like report`. 
* **Query Logic :** Query database to get all the questions.
* **Response:**
    * **200 OK :** Succesfully retrivell all `limit` data from `offset`. 
    ```py title="index.py"

    {
        "pageNumber":"pageNumber",
        "limit":"limit",
        "feltLikeReport": 
            {
                "Question":"Question",
                "Options":"Options",
                "Remarks":"Remarks"
            }
    }
    ```
    * **404 - Not Found :** Bed request.


### ENDPOINT: `PATCH  /update/feltReport/:id`

* **Description :** Update the existing `felt like report` with corresponding answer. 
* **Query Logic :** Update answers to corresponding question with the given questionID `id`.
* **Response:**
    * **200 OK :** Succesfully answered the questionnairs with id `id`. 
    ```py title="index.py"
    {
        "questionID":"id",
        "feltLikeReport" : 
            {
                "Options":"Options",
                "Remarks":"Remarks"
            }
    }
    ```
    * **404 - Not Found :** Missing required field.
    * **409 :** Question with the unique identifier `id` do not exist.


## **SMS Stakeholders**

### ENDPOINT: `POST  /create/stakeholders/:adminID`
* **Description :** Create new stakeholders.
* **Query Logic :** Check the `adminId` provided, if it's authorized then allow the admin to create new `stakeholders` with correct phone number.
* **Response:**
    * **200 OK :** Succesfully created stakeholder with phone number `TelephoneNo`.
    ```py title="index.py"
    {
        "adminID":"adminID",
        "data": 
            {
                "Name":"Name",
                "TelephoneNo":"TelephoneNo",
                "Description":"Description"
            }
    }
    ```
    * **404 - Not Found :** Missing required field.
    * **409 :** Phone Number `TelephoneNo` already exist.


### ENDPOINT: `PATCH  /update/stakeholders/:userID`
* **Description :** Update the details of the sytakeholder. 
* **Query Logic :** Check the `userID` provided, if it's authorized and has valid permissions as a stakeholder then allow that particular stakeholder to update it's `stakeholders` information.
* **Response:**
    * **200 OK :** Succesfully updated your stakeholder information.
    ```py title="index.py"
    {
        "userID":"userID",
        "where":{
            "TelephoneNo":"TelephoneNo",
        }
        "data": 
            {
                "Name":"Name",
                "TelephoneNo":"TelephoneNo",
                "Description":"Description"
            }
    }
    ```
    * **404 - Not Found :** Invalid phone number `TelephoneNo`.
    * **409 :** Phone Number `TelephoneNo` already exist.


### ENDPOINT: `DELETE  /delete/stakeholders/:adminID`
* **Description :** Delete the details of the sytakeholder. 
* **Query Logic :** Check the `adminID` provided, if it's authorized then allow the admin to delete stakeholders.
* **Response:**
    * **200 OK :** Succesfully deleted your stakeholder `Name`.
    ```py title="index.py"
    {
        "userID":"userID",
        "where":{
            "TelephoneNo":"TelephoneNo",
        }
        "data": 
            {
                "Name":"Name",
                "TelephoneNo":"TelephoneNo",
                "Description":"Description"
            }
    }
    ```
    * **404 - Not Found :** Invalid phone number `TelephoneNo`.
    * **409 :** Phone Number `TelephoneNo` already exist.


* **Earthquake Notification**

### ENDPOINT: `POST  /send/notification/public/:adminID`
* **Description :** Send notification to all the public when the input field `SMS To` is set to true.
* **Query Logic :** Check the `adminID`, if it's authorized then allow the admin to send notification to all the public.
* **Response:**
    * **200 OK :** Succesfully delivered sms to general public.
    ```py title="index.py"
    {
        "adminID":"adminID",
        "data": 
            {
                "smsTo":true,
                "Message":"Message"
            }
    }
    ```
    * **404 - Not Found :** Missing Required Fields.
    * **409 :** Admin with the `adminID` is not authorized to create rule.


### ENDPOINT: `POST  /send/notification/stakeholders/:adminID`
* **Description :** Send notification to all the stakeholder when the input field `SMS To` is set to true.
* **Query Logic :** Check the `adminID`, if it's authorized then allow the admin to send notification to all the stakeholders.
* **Response:**
    * **200 OK :** Succesfully deleted your stakeholder `Name`.
    ```py title="index.py"
    {
        "adminID":"adminID",
        "data": 
            {
                "smsTo":true,
                "Message":"Message"
            }
    }
    ```
    * **404 - Not Found :** Missing Required Fields.
    * **409 :** Admin with the `adminID` is not authorized to create rule.



## **Landslide Inventory**

### ENDPOINT: `POST  /send/notification/stakeholders/:adminID`
* **Description :**
* **Query Logic :**
* **Response:**
    * **200 OK :**
    ```py title="index.py"
    {

    }
    ```
    * **404 - Not Found :**
    * **409 :** 



