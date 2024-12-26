# My Understanding of the BRD

## 2. Background

### 2.1 Backgroud

* Earthquake and Geophysics division under MoENR monitors the seismic event within and outside bhutan, its main responsibility is to disseminate the eqrthquick info as soon as earthquake occurs.

**Therefore**, NEMN and EIMN are stable and up-time 99.9% with accurate, reliable data for public.

## 2.2 Objectives

1. Scalable and ***user-friendly system*** that ***integrates various data*** and diverse functionality.
2. Ensure quality data and information processing which incudes 
    * collectig 
    * Management
    * Accessibility of data collected(data collection is done from thirt party division)


## 2.2 Scope 

* Development of GeoHazard **web portal**

## 2.4 Current State 

* No web portal for for collecting the information fromthe source and disseminating it to public.

## 2.5 Desire future state 

* Centralized database ensurig data quality 
* information processing 
* Data disseminating with various stakeholders and public.


## 3. **Functionality Requremments** 

### 3.1. **User Authentication and Role Based Access Control**

1. **Secure Login**

* **Secure login** using **National Digital Identity**(NDI)

* **Verify the identity** and assign role like public viewer and GHS admin.

2. **User Management**

* Allow the Adimn to perform **CRUD functionality** on user.

3. **Role Mangement**

* Allow the Adimn to perform **CRUD functionality** on user role.***(what roles are there ?)***

4. **Permission Management :**

* System should be able to assign permission like CRUD functionality.

* Ensure assignign multiple permission to a role.

### 3.2. **Master Data Management**

* Validate the incoming data and accurate data dissemination.

* Deactivate or achiving of data without deleting the data(data needs to be in the db with a status and frontend needs to temporarly deactivater the data...... A sprcial permission need to be there to update the data status)

* Parent child relatonship between categories of data (doubt : categorires to be parent and data to be child under the category ??? is it ?)

* No redundent data storage.






