Guía para el Código Frontend | I2B
=====
Reglas estádares para escribir y mantener código frontend para proyectos web en I2B

Versión Web: [http://i2btech.github.io/guia-para-el-codigo-frontend/](http://i2btech.github.io/guia-para-el-codigo-frontend/)

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
|	|	|	|__ mixins.jade
|	|	|	|__ variables.jade
|	|	|__ template
|	|		|__ templatename.jade
|	|
|	|__ js
|	|	|__ functions.js
|	|	|__ inc
|	|		|__ anyexternallib.js
|	|
|	|__images
|		|__ sprites
|
|__ gruntfile.js
|__ package.json
|__ bower.json
|__ .editorconfig	
|__ .gitignore
|__ .htmlhintrc
|__ .jshintrc
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
		|		|__ jquery-1.11.3.min.js
		|		|__ modernizr-detectizr.min.js
		|		|__ lt-ie-9.min.js
		|		|__ anyexternallib.min.js
		|
		|__ images
		
```

HTML
=====

###Sintaxis

- Utiliza 2 espacios (*soft tab*) / 1 tab (*hard tab*) para indentar. Se configura fácilmente, por ejemplo, en [Sublime Text](http://www.sublimetext.com/docs/2/indentation.html).
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

###Encabezado
- En todo archivo .jade que corresponda a un template de una o varias varias páginas se incluirá dentro de las primeras líneas del mismo el siguiente encabezado a modo de comentario oculto, el cual deberá ser llenado por el desarrollador a cargo del proyecto ó que esté realizando el template:

``` html
//-
 * Proyecto:
 * Fecha Inicio:
 * Email Desarrollador:
 * Descripción: 
 * Dependencias: 
 * Dónde se utiliza: 
```

###Comentarios
- Comenta grandes bloques de secciones de la siguiente manera (mayúsculas):

``` css
// SECCION
```

- Para comentarios menores, de orden local o para recordar o mencionar algo, con Jade utiliza `//-` ya que se emitirá al compilar a HTML:

``` css
//- cambio de color al :target
```

###Compatibilidad IE
- El modo **Edge** de Internet Explorer debe ser explícitamente declarado dentro de las etiquetas `<head></head>`:

``` html
head
	meta(http-equiv='X-UA-Compatible' content='IE=Edge')
	title ★★★☆☆
```
    
###Encoding
- Por defecto todos los documentos HTML utilizarán **UTF-8** como formato de encoding para renderizado estándar de caracteres.

``` html
head
	meta(charset='utf-8')
	title ★★★☆☆
```
	  
###Etiquetas inline
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

###Etiquetas con auto-cierre
- En el caso de utilizar etiquetas HTML que se cierren a sí mismas (como en el caso de `<img />` deja un espacio al final antes del `/` cierre:

``` html
// Evita:
<img src="chanfle.jpg"/>

// Prefiere:
<img src="chanfle.jpg" />
```

###Semántica y accesibilidad
- Para estructurar el contenido se utilizará como base el uso de [seccionamiento de HTML5](http://blog.teamtreehouse.com/use-html5-sectioning-elements): `section, nav, aside, article, main, header, footer`.

- Para mayor y mejor accesibilidad se agregarán [roles ARIA](http://www.paciellogroup.com/blog/2013/02/using-wai-aria-landmarks-2013/) que le agregarán sentido a áreas específicas de cada página. Más detalles en sección [WAI-ARIA](#wai-aria).

###Atributos de input accesibles
- Para ayudar la accesibilidad en dispositivos móviles, se recomienda el uso del atributo `type` para la etiqueta `<input />` con valores orientados al uso del valor de esta etiqueta, según el listado a continuación:
	- search
	- email
	- url
	- tel
	- number
	- range
	- date
	- month
	- week
	- time
	- datetime
	- color

###Favicons
- Para todo proyecto *responsive* se considerarán las siguientes etiquetas `<meta>` y tamaños para ícons/favicons:

```html
<!-- Para iPad con retina en iOS ≥ 7: -->
<link rel="apple-touch-icon-precomposed" sizes="152x152" href="/assets/images/favicon-152.png">

<!-- Para iPad con retina en iOS ≤ 6: -->
<link rel="apple-touch-icon-precomposed" sizes="144x144" href="/assets/images/favicon-144.png">

<!-- Para iPhone con retina en iOS ≥ 7: -->
<link rel="apple-touch-icon-precomposed" sizes="120x120" href="/assets/images/favicon-120.png">

<!-- Para iPhone con retina en iOS ≤ 6: -->
<link rel="apple-touch-icon-precomposed" sizes="114x114" href="/assets/images/favicon-114.png">

<!-- Para primera y segunda generación de iPad: -->
<link rel="apple-touch-icon-precomposed" sizes="72x72" href="/assets/images/favicon-72.png">

<!-- Para no-retina iPhone, iPod Touch, y Android 2.1+ devices: -->
<link rel="apple-touch-icon-precomposed" href="/assets/images/favicon-57.png">

<!-- Fallback -->
<link rel="icon" href="/assets/images/favicon-32.png" sizes="32x32">
<link rel="icon" type="image/x-icon" href="/assets/images/favicon.ico">

<!-- IE10 Metro icon (cambiar color #FFFFFF) -->
<meta name="msapplication-TileColor" content="#FFFFFF">
<meta name="msapplication-TileImage" content="/path/to/favicon-144.png">
```

Y en *.jade*:

```jade
link(rel='apple-touch-icon-precomposed', sizes='152x152', href='/assets/images/favicon-152.png')
link(rel='apple-touch-icon-precomposed', sizes='144x144', href='/assets/images/favicon-144.png')
link(rel='apple-touch-icon-precomposed', sizes='120x120', href='/assets/images/favicon-120.png')
link(rel='apple-touch-icon-precomposed', sizes='114x114', href='/assets/images/favicon-114.png')
link(rel='apple-touch-icon-precomposed', sizes='72x72', href='/assets/images/favicon-72.png')
link(rel='apple-touch-icon-precomposed', href='/assets/images/favicon-57.png')
link(rel='icon', href='/assets/images/favicon-32.png', sizes='32x32')
link(rel='icon', type='image/x-icon', href='/assets/images/favicon.ico')
meta(name='msapplication-TileColor', content='#FFFFFF')
meta(name='msapplication-TileImage', content='/path/to/favicon-144.png')
```

###Social Meta / Opengraph
- Para mejor indexación por sistemas de redes sociales, y en los proyectos que lo ameritan, se debe integrar las etiquetas `<meta>` correspondientes a [Opengraph](https://developers.facebook.com/docs/reference/opengraph/object-type/product/) y [Twitter Cards](https://dev.twitter.com/cards/types/product) y orientadas a *e-commerce* como se muestran a continuación:

```html 
<!-- Twitter Cards -->
<meta name="twitter:site" content="@TWITTER_USERNAME" />
<meta name="twitter:creator" content="@TWITTER_USERNAME" />
<meta name="twitter:card" content="product" />
<meta name="twitter:label1" content="price" />
<meta name="twitter:data1" content="$PRECIO" />
<meta name="twitter:label2" content="brand" />
<meta name="twitter:data2" content="MARCA" />
<meta name="twitter:image" content="http://URL_IMAGEN_500X500PX">
<!-- OpenGraph -->
<meta property="og:site_name" content="NOMBRE_SITIO" />
<meta property="og:url" content="http://URL_SITIO/PRODUCTO" />
<meta property="og:title" content="TITULO_PRODUCTO" />
<meta property="og:description" content="DESCRIPCION_MAX_180_ARACTERES" />
<meta property="og:image" content="http://URL_IMAGEN_500X500PX" />
<meta property="og:type" content="product" />
<meta property="og:price:amount" content="PRECIO" />
<meta property="og:price:currency" content="MONEDA" />
<meta property="og:availability" content="DISPONIBILIDAD('instock','oos','pending)" />
<meta property="fb:app_id"  content="ID_APP_FB" /> 
```
Y en *.jade*:

```jade
// Twitter Cards
meta(name='twitter:site', content='@TWITTER_USERNAME')
meta(name='twitter:creator', content='@TWITTER_USERNAME')
meta(name='twitter:card', content='product')
meta(name='twitter:label1', content='price')
meta(name='twitter:data1', content='$PRECIO')
meta(name='twitter:label2', content='brand')
meta(name='twitter:data2', content='MARCA')
meta(name='twitter:image', content='http://URL_IMAGEN_500X500PX')
// OpenGraph
meta(property='og:site_name', content='NOMBRE_SITIO')
meta(property='og:url', content='http://URL_SITIO/PRODUCTO')
meta(property='og:title', content='TITULO_PRODUCTO')
meta(property='og:description', content='DESCRIPCION_MAX_180_ARACTERES')
meta(property='og:image', content='http://URL_IMAGEN_500X500PX')
meta(property='og:type', content='product')
meta(property='og:price:amount', content='PRECIO')
meta(property='og:price:currency', content='MONEDA')
meta(property='og:availability', content="DISPONIBILIDAD('instock','oos','pending)")
meta(property='fb:app_id', content='ID_APP_FB')
```

Links:
- [Validador Twitter Cards](https://cards-dev.twitter.com/validator)
- [Facebook Debugger](https://developers.facebook.com/tools/debug/)


###Boilerplate & Workflow
- Como base para todos los nuevos proyectos web en I2B, se propone el uso de un boilerplate que contiene los elementos mínimos necesarios para iniciar el templating de cualquier proyecto y entregar soporte mínimo del browser IE8, entre ellos:

	* GruntJS
	* SCSS (CSS pre-processor)
	* Jade (HTML pre-processor)
	* mixins básicos
	* jQuery.js
	* lt-ie9.js (selectivizr.js + html5shiv.js + respond.js)
	* CSS3 Pie
	* Modernizr + Detectizr
	* estructura de carpetas estándar

El HTML generado contiene la siguiente estructura:

```html
<!DOCTYPE html(lang='es')>
<head>
  <meta charset="utf-8"/>
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/>
  <meta name="viewport" content="width=device-width"/>
  <title></title>
  <link rel="stylesheet" href="assets/css/style.css"/>
  <!--[if lt IE 8]>
  <script src="assets/js/libs/html5shiv.js"></script>
  <![endif]-->
  <script src="assets/js/libs/modernizr-detectizr.js"></script>
</head>
<body>
  ...
  
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.2/jquery.min.js"></script>
  <script>window.jQuery || document.write('<script src=assets/js/libs/jquery.js><\/script>');</script>
  <!--[if lt IE 8]>
  <script src="assets/js/libs/respond.js"></script>
  <script src="assets/js/libs/selectivizr.js"></script>
  <![endif]-->
  <script src="assets/js/functions.js"></script>
</body>
```

[I2B Frontend WorkFlow >](https://github.com/I2BTech/i2b-frontend-workflow)

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
 * Email Desarrollador:
 * ======== */
```

###Sintaxis
- Utiliza 2 espacios (*soft tab*) / 1 tab (*hard tab*) para indentar.

###Pre-processing
- Utilizamos [SCSS](http://sass-lang.com/) como pre-processor para CSS, el que es la versión 3 de **SASS**.

- Privilegia el uso de *mixins* y funciones, pero no abuses. Evita utilizar *@extend* ya que puede importar mucho código innecesario si mal utilizado.

- No indentes más de 3 niveles de especificidad.

- Guarda valores repetitivos en variables con nomenclatura clara. Recuerda que puedes crear *scope* para la misma variable.

- Agrega un salto de línea vacío antes de comenzar un nuevo elemento o declaración de elementos para mantener legibilidad en el código fuente.

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

- Si defines estilos para más de un mismo selector, usa saltos de líneas entre ellos:

``` css
selector1,
selector2 {
	propiedad: valor;
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

// Evita
padding: 0px;
```

- Omite el `0` si este se encuentra a la izquierda del valor:

``` css
// Bien
margin: .5em;

// Evita
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

// Evita
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

// Evita
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

// Evita
.grande {}
.rojo {}
```

###Media Queries
- Declara `@media` queries al final del archivo CSS, donde se definan modificaciones al comportamiento/estilo de elementos ya declarados.
- En proyectos de gran volumen con participación de más de un desarrollador frontend sobre el mismo, se recomienda utilizar diferentes hojas de estilos para cada `@media` y que cada uno trabaje sobre diferentes archivos bajo un mismo HTML compartiendo la estructura responsive:

```html
link(rel='stylesheet', media='screen and (min-width: 701px) and (max-width: 900px)', href='css/main.min.css')
```
- Para todo proyecto que requiera comportamiento responsive en su grilla, se recomienda el uso de la grilla de [Bootstrap](http://getbootstrap.com/customize/) (customizada) en su última versión disponible, la que permite soporte desde IE8 (mediante respond.js) y construcción de grillas responsive/adaptive.

###Mixins

Se incluye un archivo `src/scss/inc/mixins.scss` varios mixins y que se dividen en 2 grupos: los de prefix y el resto.

####Prefix
Ayudan al soporte de prefix de las propiedades CSS que aún las necesita para correcta visualización en browsers. Sin embargo, se debe privilegiar el uso del plugin **grunt-autoprefixer** el que está configurado para agregar prefijos (estándares) directo a los archivos CSS generados de SCSS dentro de `dist/assets/css` correspondientes a las últimas 2 versiones (la actual y una anterior) de los principales browsers y las versiones en específico de IE 8 y 9.

Toma en cuenta que Microsoft creó filtros (no estádares) los que se toman en cuenta para algunos de los mixins aquí utilizados, como por ejemplo `opacity` y `background: linear-gradient();`.

####El resto
Los otros mixins se detallan a continuación:

- **out($color:red)**: utilizado para debuguear, le agrega al selector un outline de 1px y de color a definir; rojo por defecto.

- **escondetxt()**: esconde el texto con el clásico `text-indent: -9999px; overflow: hidden;`

- **zero()**: básico y universal reseter con `margin:0; padding:0;`

- **gradient-vertical($startColor,$endColor)**: gradientes verticales más fáciles, de arriba a abajo: 

- **gradient-horizontal($startColor,$endColor)**: gradientes horizontales más fáciles, de izquierda a derecha:

###@extend e @include

- Prefiere agrupar las declaraciones `@include` en la parte superior del bloque y luego de las declaraciones `@extend`:

```scss
.selector {
	@extend .element;
	@include clearfix();
	
	width: 5em;
}
```

###Herencia de estilos

- Cuida la herencia de estilos y evita el selector de hijo directo `>` y utilízalo sólo si necesario (por ejemplo, cuando quieres alcanzar varios selectores hijos que no necesitan tener una clase declarada):

```html
<article class='article-link'>
  <div class='box-vote'>
    <button class='add'></button>
    <button class='rest'></button>
    <span class='count'></span>
  </div>

  <h3 class='title'>Article title</h3>
  <p class='count'>3 votes</p>
</article>
```

```scss
. article-link {
  .title 	{ /* ... */ }
  > .count { /* ... */ }
}
```

En este caso si no definieras `.article-link > .count` este estilo lo habría heredado `.box-vote .count`.

JavaScript
=====

###Inclusión
- El(los) archivo(s) JavaScript deben ser incluídos en las páginas HTML que correspondan a su uso lo más cerca posible del cierre de la etiqueta `</body>`, reduciendo el efecto de demoras impuesta por la carga del script y otros componentes de la página. En HTML5 ya no hay necesidad de utilizar los atributos `language` ó `type` ya que es el servidor que se encarga de determinar el correcto `MIME type`. Las excepciones a esto corresponden a librerías cuyas funcionalidades se basan en la construcción del DOM antes de su ejecución, como:
	- Modernizr + Detectizr
	- HTML5Shiv
	- Google Analytics

###Encabezado
- En todo archivo JavaScript se colocará dentro de las primeras líneas del mismo el siguiente encabezado a modo de comentario, el cual deberá ser llenado por el desarrollador a cargo del proyecto:

``` javascript
/* ===========
 * Proyecto:
 * Fecha Inicio:
 * Email Desarrollador:
 * ======== */
```

###Sintaxis
- Utiliza 2 espacios (*soft tab*) / 1 tab (*hard tab*) para indentar.
- Usa doble comilla `"` (*double quote*) para abrir y cerrar atributos, propiedades, valores, etc.

###Comentarios
- Para cada nueva función, utiliza el siguiente bloque de comentario como formato base para documentar:

``` javascript
/**
 * Nombre descriptivo
 * Funcionalidad / qué hace
 * Dónde: Dónde se utiliza (elemento, página, etc)
 * Email Desarrollador: email de quien hizo esto
 * Uso:
  	var funcion = function (
		@param1: int|bool|element|rangos|etc,
		@param2: int|bool|element|rangos|etc
	) {
		return: bool;
	};
 */
```

###Nomenclaturas

- Los archivos JavaScript creados deben tener su nombre en minúsculas, sin espacios ni caracteres especiales. Si el contenido del archivo corresponde a un plugin para jQuery, éste debe identificarse claramente como dependiente de tal librería y se permite el uso del nombre en minusculaMayuscula (*camelCase*), de la siguiente manera:

```
jquery.nombrePlugin-version.min.js
```

- Crea nombres de funciones, parámetros, métodos, variables y atributos en inglés, descriptivas al contexto y/o función que cumple el elemento, *camelCased* y sin espacio después del nombre y con espacio antes del *bracket* `{`. 

``` css
// Bien
function openModalWindow() {}

// Mal
function cerrar () {}
```

- Todas las variables deben ser declaradas antes de ser utilizadas. Prefiere que cada variable sea declarada en una nueva línea y con su comentario inline. Si dependes directamente de jQuery, utiliza `$` antes del nombre de la variable:

``` javascript
var $element, 	// this
	 $indent,	// nivel de indentación
	 $width;	// ancho del elemento sin el valor
```

- Busca por la existencia del elemento siempre antes de agregar un evento o entregarle una función:

``` javascript
if ( $element.length ){
	...
}
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

###Librerías

- Para mejor retro-compatibilidad y mayor rapidez en el desarrollo, en **I2B** utilizamos [jQuery](http://www.jquery.com/) como librería JavaScript por defecto. Prefiere el branch 1.1x que continúa con soporte a IE7+.

- Llama jQuery primero desde un **CDN** y seguido la copia local, como en el siguiente ejemplo:

``` html
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script>
<script>window.jQuery || document.write(unescape('%3Cscript src="assets/js/libs/jquery-1.11.1.min.js"%3E%3C/script%3E'))</script>
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

- Privilegiar el uso de Icon Fonts por sobre imágenes (solicitarlas al diseñador antes de iniciar el proyecto).

###Formatos

- Los formatos de imágenes soportados para web en la actualidad son: **JPG**, **PNG** y **GIF**. **SVG** es soportado con *fallback* a **PNG**.
- Nombres y formatos siempre deben ir en minúsculas.

###Temporales

- Para imágenes que se utilizarán sólo como maquetación y que no hacen parte del diseño final (banners, productos y toda imagen simulada) deben guardarse en el directorio `src/images/TEMP` para que no sean consideradas como parte de la plantilla final y puedan ser fácilmente borradas una vez en integradadas ó en producción.

###Nomenclatura

Se propone la siguiente nomenclatura de prefijos según sea el uso que tenga el tipo de imagen a ser utilizado:

- **Iconos**: **ico-**nombreimagen.formato
- **Botones**: **btn-**nombreimagen.formato
- **Logos**: **logo-**nombreimagen.formato
- **Banners**: **banner-**nombreimagen.formato
- **Fondos**: **bg-**nombreimagen.formato

Se recomienda que imágenes de tipo íconos, logos y botones estén dentro del directorio `src/images/sprites` para la generación de sprites a partir de éstas. Las otras pueden ir dentro de `src/images` para que sólo sean optimizadas por GruntJS.

###Optimización

- Toda imagen debe ser comprimida según sea el mejor método según el formato. Se recomienda aplicarlo desde GruntJS a través del plugin **grunt-contrib-imagemin** el que soporta los siguientes métodos de compresión:
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


Fuentes (Tipografías)
=====

- Se privilegiará el uso de tipografías del catálogo de [Google Fonts](http://www.google.com/fonts/) las que serán llamadas desde su CDN.
- Incluye la tipografía desde Google Fonts a través de la etiqueta `<link>` y no mediante `@import`:

```html
<link rel="stylesheet" href="//fonts.googleapis.com/css?family=Open+Sans">
```

- En el caso de necesitar más de una tipografía, concaténalas en un mismo llamado:

```html
<link rel="stylesheet" href="//fonts.googleapis.com/css?family=Open+Sans|Droid+Sans">
```

- En el caso de necesitar tipografías customizadas ó Icon Fonts, éstas serán guardadas directamente en el directorio `dist/assets/fonts` ya que no forman parte del *workflow* de GruntJS.
- Prefiere utilizar `px` como unidad para `font-size`, ya que ofrece control absoluto sobre el texto respecto al diseño esperado. 
- Prefiere no utilizar unidades para definir `line-height` ya que no hereda el valor basado en el porcentaje, sino en su unidad multiplicadora según `font-size`.
- Para webfonts locales, utilizar el siguiente orden de llamado de formatos:

```
@font-face {
  font-family: 'WebFontName';
  src: url('webfontname.eot'); /* IE9 Compat Modes */
  src: url('webfontname.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
       url('webfontname.woff2') format('woff2'), /* Super Modern Browsers */
       url('webfontname.woff') format('woff'), /* Pretty Modern Browsers */
       url('webfontname.ttf') format('truetype'), /* Safari, Android, iOS */
       url('webfontname.svg#svgWebFontName') format('svg'); /* Legacy iOS */
}
```


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

SEO es una parte esencial del marketing online y la correcta implementación de [Schema](https://schema.org/docs/documents.html) en la estrategia es un fuerte apoyo. Los datos estructurados agregan información semántica al contenido y a las páginas que no son simples de interpretar y ayudan a que sean catalogados con más exactitud. Los principales atributos que se utilizan en sitios enfocados al comercio electrónico de productos (retail) son:

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
[Structured Data Testing Tool | Google](https://developers.google.com/structured-data/testing-tool/)

[Structured data validator | Yandex](https://webmaster.yandex.com/microtest.xml)


WAI-ARIA
=====

Para mejor accesibilidad para mecanismos de ayuda para usuarios con discapacidad visual, los desarrollos web deben tener implementado **WAI-ARIA**, el estándar recomendado por la W3C para tales propósitos. [El esqueleto se puede encontrar en Github](https://github.com/I2BTech/ariabones) el cual estará en constante actualización.



Software
=====

para crear código frontend, en I2B utilizaremos 2 software los cuales la empresa dispondrá de licencias:

- Mac OS X: [Sublime Text](http://www.sublimetext.com/)
- Windows: [Sublime Text](http://www.sublimetext.com/) ó [Aptana](http://www.aptana.com/)

###Complementos

####Sublime Text packages
- [Jade.tmbundle](https://packagecontrol.io/packages/Jade)
- [Syntax Highlighting for Sass](https://packagecontrol.io/packages/Syntax%20Highlighting%20for%20Sass)
- [Emmet](https://packagecontrol.io/packages/Emmet)
- [Color Highlighter](https://packagecontrol.io/packages/Color%20Highlighter)

####Complementos Photoshop
- [CSS Hat](https://csshat.com/)


Ambiente Local
=====

- El ambiente de desarrollo local debe correr en `http://localhost/` y contempla:
	- Apache
	- MySQL
	- PHP


Enlaces
=====

- [SCSS](http://sass-lang.com/)
- [Jade](http://jade-lang.com/reference/)
- [Normalize.css](http://necolas.github.io/normalize.css/)
- [Bootstrap](http://getbootstrap.com/)
- [Schema](https://schema.org/docs/documents.html)

#####Contributor
- [Jorge Epuñan](https://github.com/juanbrujo/)
