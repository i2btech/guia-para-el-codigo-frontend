Convenciones de nomenclatura para tests unitarios
=====

La siguiente guía tiene el fin de normalizar la creación y definición de nombres de ID's para componentes y elementos para proyectos de e-commerce en I2B Technologies y los tests unitarios que se deban hacer una vez creadas las funcionalidades. 

Se apoya en la [Guía para el Código Frontend](README.md) y en [MutableCSS](mutable-css_ES.md) para su concepción e implementación.

---

**Patrón base:** 

Para todo [componente](mutable-css_ES.md#componentes) (funcionalidad individual y que contiene un conjunto de elementos):
- lowerCamelCased
- en inglés
- la primera palabra en minúscula y singular y representa la función del componente
- la segunda palabra `Box`
- Componentes que son muy amplios no necesariamente tendrá sus subcomponentes o elementos marcados, por ej. *página de productos* ó *filtros de productos*. Bastará con marcar el componente principal (están marcados en este documento con un 👓).

Ej: `loginBox`, `registerBox`, `cartBox`, `filterBox`

Para todo [elemento](mutable-css_ES.md#elementos) (elementos indivisibles que tienen función específica dentro de su componente):
- lowercase
- en inglés
- sin espacios
- la primera palabra hereda la funcionalidad del componente en que reside
- la segunda palabra la acción del elemento
- la tercera corresponde a su selector ó tipo de elemento

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

![loginBox](https://raw.githubusercontent.com/I2BTech/guia-para-el-codigo-frontend/master/images/loginBox.png)

## Olvidaste tu clave
```
#recoveryBox
    #recoveryemailinput
    #recoverysubmitbutton
    #recoverycancelbutton
    #recoveryerrormessage
```

![recoveryBox](https://raw.githubusercontent.com/I2BTech/guia-para-el-codigo-frontend/master/images/recoveryBox.png)

## Registro
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

![registerBox](https://raw.githubusercontent.com/I2BTech/guia-para-el-codigo-frontend/master/images/registerBox.png)

## Carro de Compras

```
#cartBox
    #cartemptybutton
    #cartpaybutton
```

![cartBox](https://raw.githubusercontent.com/I2BTech/guia-para-el-codigo-frontend/master/images/cartBox.png)

## Buscador
```
#searchBox
    #searchtextinput
    #searchsubmitbutton
```

![searchBox](https://raw.githubusercontent.com/I2BTech/guia-para-el-codigo-frontend/master/images/searchBox.png)

## Paginador 👓
```
#paginationBox
```

## Cupón descuento
```
#couponBox
    #couponcodeinput
    #couponsubmitbutton
```

![couponBox](https://raw.githubusercontent.com/I2BTech/guia-para-el-codigo-frontend/master/images/couponBox.png)

## Filtros

![filters](https://raw.githubusercontent.com/I2BTech/guia-para-el-codigo-frontend/master/images/filters.png)

### Precio
```
#filterPriceBox 👓
```

### Marca 👓
```
#filterBrandBox
```

### Color 👓
```
#filterColorBox
```

### Cantidad Productos 👓
```
#productsquantityselect
```

![productsQuantitySelect](https://raw.githubusercontent.com/I2BTech/guia-para-el-codigo-frontend/master/images/productsQuantitySelect.png)

### Ordenamiento Productos 👓
```
#productsorderselect
```

![productsOrderSelect](https://raw.githubusercontent.com/I2BTech/guia-para-el-codigo-frontend/master/images/productsOrderSelect.png)

## Productos

Para todo contenedor individual de producto, se tomará como sufijo identificador único a la nomenclatura el [SKU] del producto (UPPERCASED).

### Resumen de producto 👓

Para toda página que contenga una lista de productos, el formato debe contemplar el siguiente patrón de componente:

```
#productBox[SKU]
```

![productBox[SKU]](https://raw.githubusercontent.com/I2BTech/guia-para-el-codigo-frontend/master/images/productBox[SKU].png)

### Ficha de producto

```
#productSingleBox
    #productbuybutton
    #productaddtocartbutton
    #productzoombutton
```

![productSingleBox](https://raw.githubusercontent.com/I2BTech/guia-para-el-codigo-frontend/master/images/productSingleBox.png)

### Checkout

```
#checkoutBox
    #checkoutproductbox[SKU]
```

![checkoutBox](https://raw.githubusercontent.com/I2BTech/guia-para-el-codigo-frontend/master/images/checkoutBox.png)

### Envío

```
#shippingCheckoutBox
    #shippingcheckout[option]
```

![shippingCheckoutBox](https://raw.githubusercontent.com/I2BTech/guia-para-el-codigo-frontend/master/images/shippingCheckoutBox.png)

### Resumen de compra 👓

```
#checkoutResumeBox
```

### Método de pago

```
#paymentCheckoutBox
	#paymentcheckout[option]
```

### Confirmar compra

```
#paymentConfirmBox
	#paymentconfirmbutton
	#paymentcancelbutton
```

### Compra exitosa 👓

```
#paymentSuccessBox
```

### Compra rechazada 👓

```
#paymentRejectBox
```
