# Betao Back-End assignment

## Case

Netao is a tech startup that got traction selling a web application for a one-time fee of 100€. The process is simple: the user would go on their website, buy the service using a credit card, and Netao would then deliver access to the web application. Payments are currently collected through a third-party credit card processor. 

A business developer at Netao wants to increase revenue by switching to a subscription-based model. He suggests that by offering a SaaS (software-as-a-service) solution to their clients and lowering the initial fee, Netao will be able to collect recurring revenue and increase their turnover.

The project was approved, and now the engineering team is in charge of creating a subscription engine that is able to collect fees from users every month, as well as lock out users from accessing the web application if their payment fails or the subscription is cancelled.

Currently, Netao sells the web application for a one-time fee of 100€. The business analyst suggests selling the web application for 50€ and collecting a monthly recurring fee of 20€ for continuous access. The first month of access would be included in the initial 50€ fee.


Below are the current partial implementations of the User, Product and Transaction models. Currently, there is only one product, so has_access (whether or not the user can use the software) has been left on the User model.

```
/** PSEUDOCODE **/

class User
    /* Unique identifier */
    public int id
    /* Allows permanent access to the web application if the user has made a purchase */
    public boolean has_access

class Product
    /* Unique identifier */
    public int id
    public string name
    /* Recommended price */ 
    public int price

class Transaction:
    /* Buyer's ID */
    public int user_id // buyer
    /* product paid for */
    public int product_id
    /* date of purchase */
    public date date
    /* actual price paid */
    public int price
``` 

You have been assigned the task to enhance Netao's system to be able to handle multiple products, recurring subscriptions, and product access management. Here are the requirements we have gathered:

- Each Product (=software) has a recommended initial price and a recurring price. There is great likelyhood that we will need to implement discounts for specific users later on.
- The initial price will be charged immediately as the user subscribes. The user will have access to the service for 30 days after the initial payment.
- The system needs to persist every payment made, by who, when and for what product.
- The recurring price will be charged every 30 days, and will kick in after 30 days from the initial subscription. For example, if a user buys the service on `2021-01-01T00:00` and pays the initial price, the system will attempt to charge her the recurring price at `2021-01-31T00:00`, then on `2021-03-02T00:00`, and so forth.
- If a recurring payment fails, the user will lose access to the service, and no further attempts at collecting payments will be made.
- Each user can have multiple subscriptions running concurrently, but only one subscription per product.

## Tasks
1. Suggest a Python class model to support those requirements. The new data model needs to be able to express and persist transactions (payments made), subscriptions, ("User A is subscribed to product B") and product accesses ("Does User A have access to Product B at this datetime?"). The model does not need to implement any method yet, but if during your work you decided to write some methods to try out your models, there is no downside in leaving them in the submission.
2. Write a function `should_charge` that takes as input a set of Users from the model you suggested in the question above, and that returns all users that should be charged until that date and for how much, as a list of strings. As stated in the requirements, users should be charged if it has been more than a month since their last successful payment on any subscription they belong to. 

Example use of `should_charge`:
```python
   # users is a list that holds your model of users as defined in the answer to question 1
   should_charge(users=users, dt=datetime.now()) -> ['bob@betao.se: 290kr', 'john@betao.se: 290kr']
```

Mock all data necessary in order to run the function. Examples of a dataset for testing the function given below (not required to be used). Do not use a database.
```
Users: 
  bob@betao.se - last successful payment: 2021-01-01T00:00:00 - subscribed to Product A
  john@betao.se - last successful payment: 2021-01-15T00:00:00 - subscribed to Product A
  peter@betao.se - last successful payment: 2021-01-15T00:00:00 - subscribed to Product B
  andrew@betao.se - last successful payment: 2021-01-17T00:00:00 - subscribed to Product B
  boris@betao.se - last successful payment: 2020-12-15T00:00:00 - subscribed to Product A
  boris@betao.se - last successful payment: 2020-12-15T00:00:00 - subscribed to Product B
Products:
  Product A: 590kr initial, 290kr recurring
  Product B: 1090kr initial, 109kr recurring
Current date: 2021-02-16
```


Bonus:
3. Write a function that takes an user and a product as input, and returns if the user is currently able to access that product (as a boolean).

## Submission
Send your zipped files to `solen@betao.se` and `emma.edlund@betao.se`.
