Naming conventions for unit tests
=====


The following guide is intended to standardize the creation and definition of IDs names for elements and components for e-commerce projects in I2B Technologies and  theunit tests that should be done once created their functionality. 

It relies on the [Frontend Code Guide](frontend-guide_EN.md) and on [MutableCSS](mutable-css_EN.md) for it's conception and implementation.

---

**Base pattern:** 

For every [component](mutable-css_EN.md#components) (individual functionality that contains a set of elements):
- lowerCamelCased
- en english
- the first word lowercase and singular and represents the function of the component
- second word is `Box`
- Broad components should not be necessarily it's sub-components named, eg. *products page* or *products filters options*. Just name the main component (shown in this document with a 👓).

Eg: `loginBox`, `registerBox`, `cartBox`, `filterBox`

For any [element](mutable-css_EN.md#elements) (indivisible elements that have specific function within your component):
- lowercase
- in english
- no spaces
- the first word inherits the functionality of the component in which it resides
- the second word is the element's action
- the third corresponds to the selector or type of element

Ej: `loginsubmitbutton`, `recoveryerrormessage`

---

## Login
```
#loginBox
    #loginusernameinput
    #loginpasswordinput
    #loginsubmitbutton
    #logincancelbutton
    #loginerrormessage
```

![loginBox](images/loginBox.png)

## Forgotten password
```
#recoveryBox
    #recoveryemailinput
    #recoverysubmitbutton
    #recoverycancelbutton
    #recoveryerrormessage
```

![recoveryBox](images/recoveryBox.png)

## Register
```
#registerBox
    #registerfirstnameinput
    #registerlastnameinput
    #registerpasswordinput
    #registerrepeatpasswordinput
    #registertermsconditionscheckbox
    #registersubmitbutton
    #registercancelbutton
    #registererrormessage
```

![registerBox](images/registerBox.png)

## Shopping cart

```
#cartBox
    #cartemptybutton
    #cartpaybutton
```

![cartBox](images/cartBox.png)

## Search
```
#searchBox
    #searchtextinput
    #searchsubmitbutton
```

![searchBox](images/searchBox.png)

## Paginator 👓
```
#paginationBox
```

## Discount coupon
```
#couponBox
    #couponcodeinput
    #couponsubmitbutton
```

![couponBox](images/couponBox.png)

## Filters

![filters](images/filters.png)

### Price
```
#filterPriceBox 👓
```

### Brand 👓
```
#filterBrandBox
```

### Color 👓
```
#filterColorBox
```

### Product quantity 👓
```
#productsquantityselect
```

![productsQuantitySelect](images/productsQuantitySelect.png)

### Products order 👓
```
#productsorderselect
```

![productsOrderSelect](images/productsOrderSelect.png)

## Products

For every individual product container shall be taken as a unique identifier to the nomenclature the suffix product's [SKU] and UPPERCASED.

### Product overview 👓

For every page that contains a list of products, the format should include the following standard components:

```
#productBox[SKU]
```

![productBox[SKU]](images/productBox[SKU].png)

### Single product

```
#productSingleBox
    #productbuybutton
    #productaddtocartbutton
    #productzoombutton
```

![productSingleBox](images/productSingleBox.png)

### Checkout

```
#checkoutBox
    #checkoutproductbox[SKU]
```

![checkoutBox](images/checkoutBox.png)

### Shipping

```
#shippingCheckoutBox
    #shippingcheckout[option]
```

![shippingCheckoutBox](images/shippingCheckoutBox.png)

### Purchase summary 👓

```
#checkoutResumeBox
```

### Payment method

```
#paymentCheckoutBox
	#paymentcheckout[option]
```

### Confirm payment

```
#paymentConfirmBox
	#paymentconfirmbutton
	#paymentcancelbutton
```

### Successful payment 👓

```
#paymentSuccessBox
```

### Rejected payment 👓

```
#paymentRejectBox
```
