[<< Back to Main](../README.md)

# Assignment 2

This assignment builds on the work you have done for [Assignment 1](./assignment-1.md).

For this assignment you will be implementing the "Shoping Cart" functionality. Here is a high-level overview of what you will be doing:

* Create a "Store" object to keep track of the state of the application
* Dynamically generate the UI for products, instead of hard-coding into HTML
* Create "Add to Cart", "Remove from Cart" buttons


## Directory Structure

Same as assignment 1, except this time it will include a JavaScript file that describes your application.

```
/css/
/js/
    /app.js
/images/
/index.html
```

In the above example `app.js` will have all your JavaScript code. You should include this in your `index.html` as a `<script>` tag.


## Tasks

1. [JS] Define a constructor function with the signature `function Store(initialStock)`, which will be used to instantiate a `Store` object. This `Store` object will keep track of the items in the store and the items in the cart. *Although we do tolerate the use of ES6 for the assignments, for this Task **do not use the ES6 `class`***.
    * A) The constructor function should initialize the following properties (1 Point):
        * `"stock"` - initialize it with `initialStock` passed as the argument to the constructor
        * `"cart"` - initialize it with an empty object (i.e. associative array)
        * `"onUpdate"` - initialize it with `null`
    * B) Define the following methods for `Store` (i.e. prototype functions) - You don't need to implement the function body yet; you will do that in Task 4 (1 Point):
        * `addItemToCart(itemName)`
        * `removeItemFromCart(itemName)`
        * `renderProduct(container, itemName)`
        * `renderProductList(container)`

2. [JS] Create a **global variable** named `products` and then assign it an associative array (i.e. an object) that will store information about the products. (1 Point)
    * The keys of this object should be the names of the product (e.g. `"Box1"`) found in the file names of the [product images](./images/) we provided in assignment 1.
    * The value corresponding to each key should be yet another associative array, storing information about a product. The object should have the following properties:
        * `"label"` - `(string)` Human friendly name of the product
        * `"imageUrl"` - `(string)` The URL of the product image
        * `"price"` - `(number)` The price of the product
        * `"quantity"` - `(number)` The quantity of the product **(initialize this to 5 for all products)**

3. [JS] Create a **global variable** named `store` and then assign a new instance of `Store` you defined in Task 1. Use the `product` object created in Task 2 as the argument. (1 Point)

4. [JS+HTML+CSS] Implement the following methods of `Store`:
    * A) `renderProduct(container, itemName)` (5 Points)
        * The first argument `container` is a DOM element *(not a query selector)*, and
        * The second argument `itemName` is the name of a product (e.g. `"Box1"`)
        * The function should generate a single product box (HTML) for the product identified by `itemName`, then **replace the contents of `container` with this new HTML**.
        * In addition to the features you hard-coded in assignment 1, the product box should also display the following when the mouse pointer is over it:
            * "Add to Cart" button with CSS class `btn-add`
            * When clicked, "Add to Cart" button should trigger `addItemToCart(itemName)` method of the store instance.
            * "Remove from Cart" button with CSS class `btn-remove`
            * When clicked, "Remove from Cart" button should trigger `removeItemFromCart(itemName)` method of the store instance.
            * Cart symbol on top of the product image. The user should still be able to see the product in the background. You can use your own cart image or [this image](./cart.png) provided for you.

        ![product.png](./product.png?raw=true "Add to Cart, Remove from Cart")

    * B) `renderProductList(container)` (2 Points)
        * The first argument `container` is a DOM element *(not a query selector)*
        * The function should generate the product list (HTML) you hard-coded in assignment 1, and then **replace the contents of `container` with this new HTML.**
        * Use the `renderProduct` function you created in Task 4A to generate the individual product boxes.
        * Don't forget to assign the CSS class `.product` to the individual product boxes.

5. [JS] Remove the hard-coded product list (i.e. ul#productList) from assignment 1 and in its place put a placeholder `<div>` with id `productView`. Then somewhere in your code, invoke `renderProductList` method of the `store` object (from Task 3) to populate this DIV. (1 Point)

6. [JS] Implement the following methods of `Store`:
    * A) `addItemToCart(itemName)` - this function should accept a string argument `itemName`. If the cart object already has a value corresponding to this key, increment it. If not, set it to 1. Decrement the quantity in the stock accordingly. Handle cases where the stock does not have the item anymore. After the stock and the cart are updated, invoke the function assigned to the `onUpdate` property of the store instance (you will assign this function in Task 7). (1 Point)
    * B) `removeItemFromCart(itemName)` - this function should accept a string argument `itemName`. If the cart object has a value corresponding to this key, decrement it. If the quantity in the cart becomes 0, delete the entry in the cart. After the stock and the cart are updated, invoke the function assigned to the `onUpdate` property of the store instance (you will assign this function in Task 7). (1 Point)

7. [JS] Finally, assign a function with no arguments to the `onUpdate` property of the `store` object. This function is invoked every time `store`'s state is updated (as you have implemented in Task 6). In this function, call `renderProductList` with the appropriate container object. The high-level idea here is that any time an item is added to or removed from cart (state of the model is changed), you will update the html (change the view). (1 Point)


* Bonus. [JS+HTML] Implement a function with the signature `showCart(cart)`, which **invokes an `alert` to display the contents of the given cart object** as shown below. Then create a "Show Cart" button somewhere in your HTML, which, when clicked, will invoke the `showCart` function with the appropriate cart object. (1 Point)

```
Box1 : 3
Jeans : 1
Keyboard : 2
```


## Testing

**To test your code, insert the following script tags within the head tag of your page**
```
<script src="http://ece.ubc.ca/~kumseok/src/cpen400a/jquery-3.3.1.min.js" type="text/javascript"></script>
<script src="http://ece.ubc.ca/~kumseok/src/cpen400a/test-2.js" type="text/javascript"></script>
```
You will see a red button on the top-right corner of your web page. Click it to test your code.
Watch out for the alert messages which tell you any missing components/functionalities. You are responsible for ensuring that all the functionalities above are implemented correctly - the tests are only there to help you. We reserve the right to test your code with other test cases than the above.


## Marking

There are 7 tasks for this assignment:
* Task 1:
  * A: 1 Point
  * B: 1 Point
* Task 2: 1 Point
* Task 3: 1 Point
* Task 4:
  * A: 5 Points
  * B: 2 Points
* Task 5: 1 Point
* Task 6:
  * A: 1 Point
  * B: 1 Point
* Task 7: 1 Point
* Bonus: 1 Point

**Bonus mark does not carry over to the next assignment - it is used only to make up for marks lost in this assignment**


## Submission instructions:

* Create a branch called `assignment-2`.
* Update the code to reflect the changes for this assignment.
* Make sure you commit and push your changes before the due date - late submissions will not be accepted.


### Deadlines:

These deadlines will be strictly enforced; we won't be looking at any commits done after this time-stamp.

* L1A & L1B - Monday, October 8, 2018 23:59:59 PST


## Labs are mandatory on the week of assignment submission:

* If you cannot attend the lab to demo your assignment for any reason, you need to notice Instructors on Piazza ahead of at least 24 hours before the lab section starts. Otherwise, you will be recorded as no attendance and will have marks deducted.
