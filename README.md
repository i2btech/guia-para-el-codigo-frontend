Guía para el Código Frontend | I2B
=====
Reglas estádares para escribir y mantener código frontend para proyectos web en I2B

Introducción
-----

Esta guía ha sido formulada con mucho cariño con el propósito de normalizar el código fuente realizado para los proyectos y clientes en [I2B](http://www.i2btech.com/), a través de herramientas que ayuden a acelerar y mejorar el proceso de creación de código web como lo son **Jade**, **Handlebars** y **SCSS**. Se siguen convenciones estándares de HTML y CSS pero se optimizan y normalizan varias reglas implícitas, dejando lugar al uso de criterio de cada integrante del equipo de desarrollo web.


Estructura de Archivos
=====
- Para una mejor semántica se propone separar los archivos base (*source*) de los procesados y finales (*dist*). La estructura de archivos se muestra a continuación y dependerá del uso de las tecnologías:

```
proyecto/
|__ src
|	|__ scss
|	|	|__ scss
|	|	|__ inc
|	|		|__ mixins.scss
|	|		|__ normalize.scss
|	|		|__ colors.scss
|	|		|__ variables.scss
|	|
|	|__ jade
|	|	|__ page.jade
|	|	|__ inc
|	|		|__ mixins.jade
|	|
|	|__ handlebars
|	|	|__ template.handlebars
|	|	|__ inc
|	|		|__ data.json
|	|
|	|__ js
|	|	|__ functions.js
|	|
|	|__images
|		|__ sprites
|
|__ gruntfile.js
|__ package.json
|__ bower.json
|__ .editorconfig
|__ .jshintrc
|__ .ftppass
|
|__ dist
	|__ page.html
	|__ assets
		|__ css
		|	|__ style.min.css
		|	|__ libs
		|		|__ anyexternallib.min.css
		|__ js
		|	|__ functions.min.js
		|	|__ libs
		|		|__ jquery-1.11.1.min.js
		|		|__ selectivizr.min.js
		|		|__ modernize.min.js
		|		|__ html5shiv.min.js
		|		|__ anyexternallib.min.js
		|
		|__ images
		
```

HTML
=====

###Sintaxis

- Utiliza 2 espacios (*soft tab*) / 1 tab (*hard tab*) para indentar. Se configuran en [Sublime Text](http://www.sublimetext.com/docs/2/indentation.html), [Textmate](http://manual.macromates.com/en/working_with_text), [Emacs](http://www.emacswiki.org/emacs/NoTabs).
- El doctype por defecto será HTML5: `doctype html`
- Usa doble comilla `"` (*double quote*) para abrir y cerrar atributos, aunque el estándar no lo requiera.
- Prefiere atributos simples en los que su valor sea el mismo del atributo, por ejemplo:

``` html
// Evita:
<input required="required" />

// Prefiere:
<input required />
```

- Agrega un salto de línea vacío antes de comenzar un nuevo bloque de elementos que sean importantes para mantener legibilidad en el código fuente.

``` html
doctype html
html(lang='es')

	head
		meta(charset='utf-8')
		meta(name='viewport', content='width=device-width, initial-scale=1')

		link(rel='stylesheet', href='css/main.min.css')
```
    
###Encoding
- Por defecto todos los documentos HTML utilizarán **UTF-8** como formato de encoding para renderizado estándar de caracteres.

``` html
head
	meta(charset='utf-8')
	title ★★★☆☆
```
	  
###Atributos
- Al utilizar *Jade* y de ser necesario colocar texto dentro de etiquetas, comúnmente se utizan barras `|` (*pipes*) para separar texto plano de etiquetas inline anidadas (como *strong* ó *em*). En lo posible evitar el uso de estas barras colocando el texto seguido de la etiqueta bloque que la contenga y utilizando HTML para etiquetas inline, como en el siguiente ejemplo:

``` css
// Incorrecto
p 
	| Lorem ipsum 
	strong dolor si amet.
	  
// Correcto
	p Lorem ipsum <strong> dolor si amet.</strong>
```

###Clases y concatenación
- Clases CSS serán concatenadas inmediatamente unas luego de otras.

``` css
a.list-item.active(href='')
```

###Semántica y accesibilidad
- Para estructurar el contenido se utilizará como base el uso de [seccionamiento de HTML5](http://blog.teamtreehouse.com/use-html5-sectioning-elements): `section, nav, aside, article, main, header, footer`.

- Para mayor y mejor accesibilidad se agregarán [roles ARIA](http://www.paciellogroup.com/blog/2013/02/using-wai-aria-landmarks-2013/) que le agregarán sentido a áreas específicas de cada página. Más detalles en sección [WAI-ARIA](#wai-aria).

###HTML Boilerplate
- Como base para todos los nuevos proyectos web en I2B, se propone el uso de un boilerplate que contiene los elementos mínimos necesarios para iniciar el templating de cualquier proyecto, entre ellos:

	* GruntJS
	* SCSS (CSS pre-processor)
	* Jade (HTML pre-processor)
	* jQuery.js
	* html5shiv.js
	* selectivizr.js
	* mixins básicos
	* estructura de carpetas estándar

[HTML Boilerplate >](#)

CSS
=====

###Inclusión
- El(los) archivo(s) CSS debe(n) ser incluído(s) en las páginas HTML que correspondan a su uso lo más cerca posible del cierre de la etiqueta `</head>`. En HTML5 ya no hay necesidad de utilizar el atributo `type` ya que es el servidor que se encarga de determinar el correcto `MIME type`.

###Encabezado
- En todo archivo CSS base se colocará dentro de las primeras líneas del mismo el siguiente encabezado a modo de comentario, el cual deberá ser llenado por el desarrollador a cargo del proyecto:

``` css
/* ===========
 * Proyecto:
 * Fecha Inicio:
 * Desarrollador:
 * ======== */
```

###Sintaxis
- Utiliza 2 espacios (*soft tab*) / 1 tab (*hard tab*) para indentar.

###Pre-processing
- Utilizamos [SCSS](http://sass-lang.com/) como pre-processor para CSS, el que es la versión 3 de **SASS**.

- Privilegia el uso de *mixins* y funciones, pero no abuses. Evita utilizar *@entend*.

- No indentes más de 3 niveles de especificidad.

- Guarda valores repetitivos en variables con nomenclatura clara. Recuerda que puedes crear *scope* para la misma variable.

- Agrega un salto de línea vacío antes de comenzar un nuevo elementos o declaración de elementos para mantener legibilidad en el código fuente.

``` css
selector {
	propiedad: valor;
}

otroselector {
	propiedad1: valor1;
	propiedad2: valor2;
}
```

- Si defines estilos para más de un selector hijo, sepáralos con un salto de línea

``` css
selector {
	propiedad: valor;
	  
	.selector-hijo {
		selector2 {
			propiedad1: valor1;
			propiedad2: valor2;

			&:hover {
				propiedad: valor;
			}
		}
	}
}
```

###Declaraciones
- Privilegia el orden de tus declaraciones en el siguiente orden:
	 * display / modelo de caja
	 * posicionamiento
	 * fuente/tipografía
	 * colores
	 * otros

``` css
selector {
	display: block;
	width: 100px;
	height: 100px;
	position: absolute;
	top: 0;
	left: 0;
	font-family: sans-serif;
	line-height: 1.5em;
	background: black;
	cursor: pointer;
}
```

###Unidades y colores
- Omite la unidad si el valor es `0`:

``` css
// Bien
padding: 0;

// Omite
padding: 0px;
```

- Omite el `0` si este se encuentra a la izquierda del valor:

``` css
// Bien
margin: .5em;

// Omite
margin: 0.5em;
```

- Define todos los colores como variables y sus matices con operaciones como `darken()` y `lighten()`, por ejemplo:

```css
$alerta: #f00; // rojo
$alertaHover: darken($alerta, 20%); // 20% más rojo oscuro
```

- En caso de tener colores en hexacromía prefiere resumirlos con sólo 3 caracteres:

``` css
// Bien
color: #f00;

// Omite
color: #ff0000;
```

###Comentarios
- Comenta grandes bloques de secciones de la siguiente manera (mayúsculas):

``` css
/* -----------
 * HOME
 * -------- */
```

- Para comentarios menores, de orden local o para recordar algo, con pre-processors utiliza `//` ya que se emitirá al compilar a CSS:

``` css
// cambio de color al :target
```

###Especificidad
- Utiliza la menor cantidad de selectores requeridos para darle estilo a un elemento; privilegia el uso de clases.

- Si utilizas clases o ID's, evita agregar el selector:

``` css
// Bien
.clase {}

// Omite
selector.clase {}
```

###Nomenclatura de clases y ID's
- Para nombres compuestos utiliza guión `-`, no guión bajo `_` (*underscore*). Nunca comiences con un dígito.

- Si manipulas elementos HTML con JavaScript, utiliza el atributo HTML5 `data-` para identificarlo y definir/guardar su valor. Si prefieres utilizar clases, utiliza el prefijo `js-` sólo si se utilizarán para tal propósito y no para darle estilo.

``` html
// Bien
<etiqueta data-value="value" />
<etiqueta class="js-abrirmodal" />
```

- Crea nombre de clases que sean descriptivas al contexto y/o función que cumple el elemento más que en su apariencia.

``` css
// Bien
.modal {}
.titulo {}

// Mal
.grande {}
.rojo {}
```

###Media Queries
- Declara `@media` queries al final del archivo CSS, donde se definan modificaciones al comportamiento/estilo de elementos ya declarados.

###Mixins

TODO


JavaScript
=====

###Inclusión
- El(los) archivo(s) JavaScript deben ser incluídos en las páginas HTML que correspondan a su uso lo más cerca posible del cierre de la etiqueta `</body>`, reduciendo el efecto de demoras impuesta por la carga del script y otros componentes de la página. En HTML5 ya no hay necesidad de utilizar los atributos `language` ó `type` ya que es el servidor que se encarga de determinar el correcto `MIME type`.

### Encabezado
- En todo archivo JavaScript se colocará dentro de las primeras líneas del mismo el siguiente encabezado a modo de comentario, el cual deberá ser llenado por el desarrollador a cargo del proyecto:

``` javascript
/* ===========
 * Proyecto:
 * Fecha Inicio:
 * Desarrollador:
 * ======== */
```

### Sintaxis
- Utiliza 2 espacios (*soft tab*) / 1 tab (*hard tab*) para indentar.
- Usa doble comilla `"` (*double quote*) para abrir y cerrar atributos, propiedades, valores, etc.

### Comentarios
- Para cada nueva función, utiliza el siguiente bloque de comentario como formato base para documentar:

``` javascript
/**
 * Nombre descriptivo
 * Funcionalidad / qué hace
 * Lugar: Dónde se utiliza (elemento, página, etc)
 * Desarrollador: Nombre de quien hizo esto
 * Uso:
  	var funcion = function (
		@param1: int|bool|element|rangos|etc,
		@param2: int|bool|element|rangos|etc
	) {
		return: bool;
	};
 */
```

### Nomenclaturas
- Los archivos JavaScript creados deben tener su nombre en minúsculas, sin espacios ni caracteres especiales. Si el contenido del archivo corresponde a un plugin para jQuery, éste debe identificarse claramente como dependiente de tal librería y se permite el uso del nombre en minusculaMayuscula (*camelCase*), de la siguiente manera:

```
jquery.nombrePlugin-version.min.js
```

- Crea nombres de funciones, parámetros, métodos, variables y atributos que sean descriptivas al contexto y/o función que cumple el elemento. 

``` css
// Bien
function ventanaModal(){}

// Mal
function cerrar(){}
```

- Todas las variables deben ser declaradas antes de ser utilizadas. Prefiere que cada variable sea declarada en una nueva línea y con su comentario inline. Si dependes directamente de jQuery, utiliza `$` antes del nombre de la variable:

``` javascript
var $elemento, 	// this
	 $indent,	// nivel de indentación
	 $ancho;	// ancho del elemento sin el valor
```

- El uso de variables globales debe ser sólo si realmente necesarias. Si la declaras, utiliza MAYUSCULA en su nombre para identificarla claramente.

- if/else, switch, for, try, catch deben responder al siguiente formato de espaciado para mejor lectura y ordenamiento:

``` javascript
if ( condicion ) {
	//
} else if ( condicion ) {
	//
} else {
	//
}

switch ( expresion ) {
	case expresion:
		//
	default:
		//
}
```
- Siempre coloca 1 espacio antes y después de operadores:

``` javascript
var x = (y + z) * w;

for (i = 0; i < 10; i++) {
    x += i;
}
```

### Librerías

- Para mejor retro-compatibilidad y mayor rapidez en el desarrollo, en I2B utilizamos [jQuery](http://www.jquery.com/) como librería JavaScript por defecto. Prefiere el branch 1.1x que continúa con soporte a IE7+.

- Llama jQuery primero desde un **CDN** y seguido la copia local, como en el siguiente ejemplo:

``` html
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script>
<script>window.jQuery || document.write(unescape('%3Cscript src="js/libs/jquery-1.11.1.min.js"%3E%3C/script%3E'))</script>
```

URL's
=====

- Prefiere URL's relativas si linkeas archivos CSS, Javascript e imágenes.
- Si tienes enlaces externos (por ejemplo librerías JavaScript, tipografías a través de un CDN) evita el uso del protocolo en la URL:


``` css
// Bien
<script src="//www.dominio.com

// Evita
<script src="http://www.dominio.com
```


Imágenes
=====

- Los formatos de imágenes soportados para web en la actualidad son: **JPG**, **PNG** y **GIF**. **SVG** es soportado con *fallback* a **PNG**.
- Toda imagen debe ser comprimida según sea el mejor método según el formato. Se recomienda aplicarlo desde GruntJS a través del plugin **grunt-image** el que soporta los siguientes métodos de compresión:
	- pngquant
   - optipng
   - advpng
   - zopflipng
   - pngcrush
   - pngout
   - mozjpeg
   - jpegRecompress
   - jpegoptim
   - gifsicle
   - svgo
- Se debe priorizar el uso de sprites para todo tipo de imágenes que sean linkeadas a través de hojas de estilos CSS como íconos, logos. La única excepción son imágenes de fondo que funcionen como un patrón. Para la generación automática de sprites se deben guardar en `src/images/sprites`:

```
proyecto/
|__ src
	|__images
		|__ sprites
```

Y un archivo `sprites.png` y `sprites.scss` serán automáticamente generados en:

```
|__ scss
|	|	|__ scss
|	|	|__ inc
|	|		|__ sprites.scss
|	|
|__ dist
	|__ assets
		|__ images/sprites.png
		
```

Lenguajes Server-Side
=====

TODO

SEO/Métricas
=====

###Google Analytics

Utiliza el siguiente código antes del cierre de `</head>`, reemplazando **UA-XXXX-Y** por el de la cuenta de Analytics final:

```html
<!-- Google Analytics -->
<script>
(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
})(window,document,'script','//www.google-analytics.com/analytics.js','ga');
ga('create', 'UA-XXXX-Y', 'auto');
ga('send', 'pageview');
</script>
<!-- End Google Analytics -->
```

###Google Tag Manager

Utiliza el siguiente código luego de abierto la etiqueta `<body>`, reemplazando **GTM-XXXX** por el de la cuenta de Tag Manager final:

```html
<!-- Google Tag Manager -->
<noscript><iframe src="//www.googletagmanager.com/ns.html?id=GTM-XXXX"
height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
'//www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
})(window,document,'script','dataLayer','GTM-XXXX');</script>
<!-- End Google Tag Manager -->
```

###Schema

SEO es una parte esencial del marketing online y la correcta implementación de Schema en la estrategia es un fuerte apoyo. Los datos estructurados agregan información semántica al contenido y a las páginas que no son simples de interpretar y ayudan a que sean catalogados con más exactitud. Los principales atributos que se utilizan en sitios enfocados al comercio electrónico de productos (retail) son:

- Product rating
- brands model
- Offers & reviews
- Product ID

Y su implementación en una caja de producto, mediante código HTML (a modo de ejemplo):

```html
<div class="producto" itemscope itemtype="http://schema.org/Product">   
  <img src="samsung-tv-led-42.jpg" itemprop="image">
  <h1>
    <span itemprop="brand">Samsung</span>
    <span itemprop="name">TV LED 42 pulgadas</span>
    <span itemprop="sku">506246</span>
  </h1>
  <div itemprop="aggregareRating" itemscope itemtype="http://schema.org/aggregateRating">
    <span itemprop="ratingvalue">8</span> de <span itemprop="bestRating">10</span> basado en <span itemprop="ratingCount">87</span> opiniones de usuarios.
  </div>
  <div itemprop="offers" itemscope itemtype="http://schema.org/aggregateOffers">
    Antes: <span itemprop="highPrice">$189.990</span>
    Oferta: <span itemprop="lowPrice">$149.990</span>
  </div>
</div>
```

WAI-ARIA
=====

Para mejor accesibilidad para mecanismos de ayuda para usuarios con discapacidad visual, los desarrollos web deben tener implementado **WAI-ARIA**, el estándar recomendado por la W3C para tales propósitos. [El esqueleto se puede encontrar en Github](https://github.com/I2BTech/ariabones) el cual estará en constante actualización.

Herramientas
=====

* [SCSS](http://sass-lang.com/)
* [Jade](http://jade-lang.com/reference/)
* [Emmet](http://emmet.io/)
* [CSS Hat](https://csshat.com/)
* [Normalize.css](http://necolas.github.io/normalize.css/)
* [Handlebars](http://handlebarsjs.com/)
* [Jeet Grid System](http://jeet.gs/)

