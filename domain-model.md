# Domain Model for Bob's Bagels

## User Stories

```
1.
As a member of the public,
So I can order a bagel before work,
I'd like to add a specific type of bagel to my basket.
```

```
2.
As a member of the public,
So I can change my order,
I'd like to remove a bagel from my basket.
```

```
3.
As a member of the public,
So that I can not overfill my small bagel basket
I'd like to know when my basket is full when I try adding an item beyond my basket capacity.
```

```
4.
As a Bob's Bagels manager,
So that I can expand my business,
I’d like to change the capacity of baskets.
```

```
5.
As a member of the public
So that I can maintain my sanity
I'd like to know if I try to remove an item that doesn't exist in my basket.
```

```
6.
As a customer,
So I know how much money I need,
I'd like to know the total cost of items in my basket.
```

```
7.
As a customer,
So I know what the damage will be,
I'd like to know the cost of a bagel before I add it to my basket.
```

```
8.
As a customer,
So I can shake things up a bit,
I'd like to be able to choose fillings for my bagel.
```

```
9.
As a customer,
So I don't over-spend,
I'd like to know the cost of each filling before I add it to my bagel order.
```

```
10.
As the manager,
So we don't get any weird requests,
I want customers to only be able to order things that we stock in our inventory.
```

## Domain Model

Basket

| Member Variables                 | Methods                         | Scenario                                                                  | Output                                                                                       | Satisfies User Story |
|----------------------------------|---------------------------------|---------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|----------------------|
| HashMap<Products, int\> products | add(String SKU)                 | Add product to basket, if already in basket increase amount.              | "Added <PRODUCT\> to basket", returns true if added.                                         | S1 & S8 & S10        |
| int capacity                     |                                 | Cannot add more products than capacity allows. Checks if item is on menu. | "Your basket is full", returns false if not added.                                           | S3                   |
| int items                        | remove(String SKU)              | Remove product from basket, receive message when not in basket.           | "Removed <PRODUCT> from basket", returns true if removed.                                    | S2                   |
| User user                        |                                 | Remove item that's not in basket.                                         | "This product is not in your cart", returns false if not removed.                            | S5                   |
|                                  | updateCapacity(int newCapacity) | Allows managers to update capacity. Needs authorization.                  | "Capacity updated." \|\| "Cannot update capacity." returns true if updated, false otherwise. | S4                   |
|                                  | totalCost()                     | Displays the total cost of all items in basket.                           | Sum of every item's price, takes account of amounts.                                         | S6                   |
|                                  | displayMenu()                   | To see what a products costs before buying.                               | Displays products and price of each product.                                                 | S7 & S9              |
|                                  | getProducts()                   | getter for products variable. to see what is in basket.                   | products                                                                                     |                      |
|                                  | getUser()                       | getter for user variable.                                                 | user                                                                                         |                      |
|                                  | getCapacity()                   | getter for capacity variable.                                             | capacity                                                                                     |                      |
|                                  | setCapacity(int)                | setter for capacity variable.                                             | Can set new value for capacity if user is manager and the new value is a positive number.    |                      |
|                                  | checkout()                      | for when the customer wants to pay.                                       | displays a receipt                                                                           |                      |
|                                  | applyDiscount()                 | applies discount. 12 bagels for 3.99 and 6 bagels for 2.49                | true if discount applied, false if not                                                       |                      |
|                                  | printReceipt()                  | overview after checkout.                                             | a full print of receipt, displays discounts and total cost                                   |                      |

Bagel ()

| Methods         | Member Variables        | Scenario                                                                          |
|-----------------|-------------------------|-----------------------------------------------------------------------------------|
| getMoneySaved() | double moneySaved       | if discount is applied, holds difference between price before and after discount. |
| setPrice()      |                         | new price.                                                                        |

Product

| Methods       | Member Variables        | Scenario                        |
|---------------|-------------------------|---------------------------------|
| getSKU()      | String SKU              | Unique identifier, product code |
| getName()     | String name             | Name og product.                |
| getPrice()    | double price            | Price of product                |
| hasDiscount() | boolean appliedDiscount | Does not have discount.         |
| getType()     |                         |                                 |






