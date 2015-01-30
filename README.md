Guía para el Código Frontend | I2B
=====
Reglas estádares para escribir y mantener código frontend para proyectos web en I2B

Introducción
-----

Esta guía ha sido formulada con mucho cariño con el propósito de normalizar el código fuente realizado para los proyectos y clientes en [I2B](http://www.i2btech.com/), a través de herramientas que ayuden a acelerar y mejorar el proceso de creación de código para la web como lo son **Jade** y **Stylus**. Se siguen convenciones estándares de HTML y CSS pero se optimizan y normalizan varias reglas implícitas, dejando lugar al uso de criterio de cada integrante del equipo de desarrollo web.


Estructura de Archivos
=====
- Para una mejor semántica se propone separar los archivos base (*source*) de los procesados y finales (*dist*). La estructura de archivos se muestra a continuación:

```
proyecto/
|__ src
|	|__ styl
|	|	|__ style.styl
|	|	|__ inc
|	|		|__ mixins.styl
|	|		|__ normalize.css
|	|		|__ colors.styl
|	|		|__ variables.styl
|	|
|	|__ jade
|	|	|__ page.jade
|	|	|__ inc
|	|		|__ mixins.jade
|	|
|	|__ js
|		|__ functions.js
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
			|__ style.min.css
			|__ libs
				|__ anyexternallib.min.css
		|__ js
			|__ functions.min.js
			|__ libs
				|__ jquery-1.11.1.min.js
				|__ selectivizr.min.js
				|__ modernize.min.js
				|__ html5shiv.min.js
				|__ anyexternallib.min.js
```

HTML
=====

###Sintaxis

- Utiliza 2 espacios (*soft tab*) / 1 tab (*hard tab*) para indentar. Se configuran en [Sublime Text](http://www.sublimetext.com/docs/2/indentation.html), [Textmate](http://manual.macromates.com/en/working_with_text), [Emacs](http://www.emacswiki.org/emacs/NoTabs).

- El doctype por defecto será HTML5: `doctype html`

- Usa doble comilla `"` (*double quote*) para abrir y cerrar atributos.

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
- Al utilizar *Jade* em caso de colocar texto dentro de etiquetas, involucra agregar barras `|` (*pipes*) para separar texto plano de etiquetas inline anidadas (como strong ó em). Se requiero evitar el uso de estas barras, colocando el texto seguido de la etiqueta bloque que la contenga y utilizando HTML para etiquetas inline, como en el siguiente ejemplo.

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

- Para mayor y mejor accesibilidad se agregarán [roles ARIA](http://www.paciellogroup.com/blog/2013/02/using-wai-aria-landmarks-2013/) que le agregarán sentido a áreas específicas de cada página.

###HTML Boilerplate
- Como base para todos los nuevos proyectos web en I2B, se propone el uso de un boilerplate que contiene los elementos mínimos necesarios para iniciar el templating de cualquier proyecto, entre ellos:

	* GruntJS
	* Stylus (CSS pre-processor)
	* Jade (HTML pre-processor)
	* jQuery.js
	* html5shiv.js
	* selectivizr.js
	* mixins básicos
	* estructura de carpetas estándar


CSS
=====

###Encabezado
- En todo archivo CSS base se colocará dentro de las primeas líneas del mismo el siguiente encabezado a modo de comentario, el cual deberá ser llenado por el desarrollador a cargo del proyecto:

``` css
/* ===========
 * Proyecto:
 * Fecha Inicio:
 * Desarrollador:
 * ======== */
```

###Sintaxis
- Utiliza 2 espacios (*soft tab*) / 1 tab (*hard tab*) para indentar.

- Utiliza `:` al definir el valor de la propiedad, aunq *Stylus* permita omitirlo, y separa este valor de la propiedad con un espacio.

``` css
selector
	propiedad: valor
```

###Pre-processing
- Utilizamos [Stylus](http://learnboost.github.io/stylus/) como pre-processor para CSS.

- Privilegia el uso de *mixins* y funciones, pero no abuses.

- No indentes más de 3 niveles de especificidad.

- Guarda valores repetitios en variables con nomenclatura clara. Recuerda que puedes crear *scope* para la misma variable.

- Agrega un salto de línea vacío antes de comenzar un nuevo elementos o declaración de elementos para mantener legibilidad en el código fuente.

- Si defines estilos para más de un selector, sepáralos con un salto de línea

``` css
selector
	propiedad: valor
	  
	.selector-hijo
		selector2
			propiedad1: valor1
			propiedad2: valor2

			&:hover
				propiedad: valor
```

###Declaraciones
- Privilegia el orden de tus declaraciones en el siguiente orden:
	 * display / modelo de caja
	 * posicionamiento
	 * fuente/tipografía
	 * colores
	 * otros

``` css
selector
	display: block
	width: 100px
	height: 100px
	position: absolute
	top: 0
	left: 0
	font-family: sans-serif
	line-height: 1.5
	background: black
	cursor: pointer
```

###Unidades y colores
- Omite la unidad si el valor es `0`:

``` css
// Bien
padding: 0

// Omite
padding: 0px
```

- Omite el `0` si este se encuentra a la izquierda del valor:

``` css
// Bien
margin: .5em

// Omite
margin: 0.5em
```

- Define todos los colores como variables y sus matices con operaciones como `darken()` y `lighten()`

- En caso de tener colores en hexacromía prefiere resumirlos con sólo 3 caracteres:

``` css
// Bien
color: #f00

// Omite
color: #ff0000
```

###Comentarios
- Comenta grandes bloques de secciones de la siguiente manera:

``` css
/* -----------
 * HOME
 * -------- */
```

- Para comentarios menores, de orden local o para recordar algo, con Stylus utiliza `//` ya que se emitirá al compilar:

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

###Nomenclatura de clases
- Para nombres compuestos utiliza guión `-`, no guión bajo `_` (*underscore*).

- Si manipulas elementos HTML con JavaScript, utiliza el atributo HTML5 `data-` para identificarlo y definir/guardar su valor. Si prefieres utilizar clases, utiliza elprefijo `js-` sólo si se utilizarán para tal propósito.

``` html
// Bien
<etiqueta data-value="value" />
<etiqueta class="js-abrirmodal" />
```

- Crea nombre de clases que sean descriptivas al contexto y/o función que cumple el elemento más que en su apariencia.

``` css
// Bien
.modal {}

// Mal
.rojo {}
```

###Media Queries
- Declara `@media` queries al final del archivo CSS, donde se definan modificaciones al comportamiento/estilo de elementos ya declarados.

###Mixins


JavaScript
=====

### Encabezado

### Sintaxis

### Declaraciones

### Comentarios

### Nomenclatura

### Librerías


Herramientas
=====

* [Stylus](http://learnboost.github.io/stylus/)
* [Jade](http://jade-lang.com/reference/)
* [Emmet](http://emmet.io/)
* [CSS Hat](https://csshat.com/)
* [Normalize.css](http://necolas.github.io/normalize.css/)
* [Jeet Grid System](http://jeet.gs/)

