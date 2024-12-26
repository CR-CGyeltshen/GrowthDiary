# Object Oriented Programing

## Class 

Defination : Classs is blueprint or templet for creating a object.

```python

class Item1:
    pass


```
## Instance of a class

* Instance of a class is an object created from a class.

* In object-oriented programming, a class acts as a blueprint, and instances are the actual objects created using that blueprint.

```python 

class Item1:
    pass

item1 = Item1()

```

* **item1** is a instance created from class **Item1**.

## Attribute 

* An **Attribute** is a piece of data that belongs to an object or a classs.

* It describes the property of a class or an object.

```python

class Item1:
    pass 

item1 = Item1()
item1.name = "phone"
item1.price = 100
item1.quantity = 5

```

* **name**,**price** and **quantity** are characteristics **item1** which is a instance of class **Item1**.

## Methods in class

In Object-Oriented Programming (OOP), a method is a function that is defined inside a class and is associated with objects (instances) of that class. 

Method defines behaviour and action that a object of a class can perform 

**syntex for a class** 

```python
class ClassName:
    
    def method_name(self, parameter1, parameter2):

        return parameter1 * parameter2

    # Creating a instance or object from a class 
    instanceName = method_name()

    # calling the method of a instance or object
    print (instanceName.method_name(parametersValue1, parametersValue2))

```

**self** inside a method is a **reference to the instance** of the class that is calling the method, example **instanceName** is the instance that is calling the methond **method_name**.

Python automatically gives the method the object that called it **instanceName**, and this object is called **self**.


## Constructor 

**Constructor** is a special method that is called automatically when an object is created from a class. 

its main role is to initialize the objects by setting up its attributes.

* There are two types of constructore 
1. __new__
2. __init__

### __new__ method 

* __new__ method id responsible for **creating a new instance** of a class.

* it allocates memory and **returns the new instance or object**.

* it is called before __init__ method.

* **Self** parameter in a constructor referes to the instance created followed by parameters that are needed for initializing the object.

### __init__ method 

* __init__ method initializer that sets up the instances's attribute after creation.

***How to add attribute to a instance through __init__ method??***

```python

class Car:

    # dynamically seting up the attribute(name and model) to a instance 
    def __init__(self, name, model):
        self.name = name
        self.model = model

# creating a instance with attribute name= "toyata" and model = 2020
car = Car("Toyata",2020)

# calling the instance
print(car.name)

```

**How to validate the arguments received in a constructor**

### `assert` is uesd to validate the arguments

```python

class Item1:

    def __init__(self,name: str, price: float,quantity: float):
        
        # Validating the arguments provided to a instance
        assert price >= 0, f"Price {price} should be greater than ot equal to zero"
        assert quantity >= 0, f"Quantity {quantity} should be greater than ot equal to zero"

        # Dynamically assigning the argument to a instance
        self.name = name 
        self.price = price
        self.quantity = quantity

    def Calculate_totalPrice(self):
        return self.price * self.quantity

item1 = Item1("tea",20, 4)
item2 = Item1("momo",30,2)

```



