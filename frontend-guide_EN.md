Frontend Code Guide @ I2B
=====

Standard rules for writing and maintaining code for frontend web projects at I2B.

Web version: [http://i2btech.github.io/guia-para-el-codigo-frontend/](http://i2btech.github.io/guia-para-el-codigo-frontend/)


Introduction
-----

This guide has been made with love in order to standardize the source code made for projects of our clients in [I2B](http://www.i2btech.com/) through tools that help accelerate and improve the process of creating web code such as **Jade** and **SCSS**. HTML and CSS standards conventions continue but are optimized and standardized several implicit rules, leaving room for the use of the discretion of each member of the development team.


File Structure
=====

For better semantics it is proposed to separate the base files (*src*) from the processed and dev files (*dist*). When necessary to get final files, optimized and lightweight, a final directory is created (*build/*).

The file structure shown below and depend on the use of the chosen technology:

```
project-name/
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
|	|__ page.html
|	|__ assets
|		|__ css
|		|	|__ style.css
|		|	|__ libs
|		|		|__ anyexternallib.css
|		|__ js
|		|	|__ functions.js
|		|	|__ libs
|		|		|__ jquery-1.11.3.min.js
|		|		|__ modernizr.js
|		|		|__ detectizr.js
|		|		|__ lt-ie-9.min.js
|		|		|__ anyexternallib.js
|		|
|		|__ images
|			|__ sprites.png
|
|__ build
	|__ page.html
	|__ assets
		|__ css
		|	|__ styles.min.css
		|__ js
		|	|__ functions.min.js
		|	|__ libs
		|		|__ jquery-1.11.3.min.js
		|		|__ modernizr-detectizr.min.js
		|		|__ ie.min.js
		|		|__ plugins.min.js
		|
		|__ images
			|__ sprites.png
		
```

HTML
=====

### Syntax

- Use 2 spaces (*soft tab*) / 1 tab (*hard tab*) to indent. It is easily configurable, for example, in [Sublime Text](http://www.sublimetext.com/docs/2/indentation.html).
- The default doctype is HTML5: `doctype html`.
- Use double quotes `"` to open and close attributes, although the standard does not require it.
- Prefer simple attributes if its value is the same as the attribute name, such as:

``` html
// Avoid:
<input required="required" />

// Prefer:
<input required />
```

- Add an empty line break before starting a new block of important/groupable elements to maintain source code readability.

``` html
doctype html
html(lang='es')

	head
		meta(charset='utf-8')
		meta(name='viewport', content='width=device-width, initial-scale=1')

		link(rel='stylesheet', href='css/styles.css')
```

### Header
- In any .jade file that corresponds to a template of one or more multiple pages will be included in the first lines of the same the following header as a hidden comment, which should be completed by the developer in charge of the project or who are coding the template:

``` html
//-
 * Project name:
 * Start date:
 * Developer email:
 * Description: 
 * Dependencies: 
 * Where is used/required:
```

###Comentarios
- Comment large blocks of sections as follows (all caps):

```html
// SECTION NAME
```

- For minor comments, local ones or to remember or mention something, in Jade use `// -` because it will be ignored when compiled to HTML:

``` css
//- clearfix
```

### IE Compatibility
- **Edge** Internet Explorer mode must be explicitly stated in the labels `<head></head>`:

``` html
head
	meta(http-equiv='X-UA-Compatible' content='IE=Edge')
	title
```
    
### Encoding
- By default, all HTML documents used will be set using **UTF-8** encoding format for rendering standard characters:

``` html
head
	meta(charset='utf-8')
	title
```
	  
### Inline tags
- By using *Jade* and if necessary place text within labels, it is commonly used pipes `|` to separate plain text from tags nested (like *strong* or *em*). If possible avoid using these bars by placing the label text block containing it and use HTML tags for inline, as in the following example:

``` css
// Avoid
	p 
	| Lorem ipsum 
	strong dolor si amet.
	  
// Prefer
	p Lorem ipsum <strong> dolor si amet.</strong>
```

### Classes and concatenation
- CSS classes will be concatenated immediately after each other and before any attribute declaration:

``` css
a.listitem.active(href='')
```

### Auto-close tags
- In the case of using HTML tags that auto-close (as in the case of `<img />` keep a white space before `/` close:

``` html
// Avoid:
<img src="chanfle.jpg"/>

// Prefer:
<img src="chanfle.jpg" />
```

### Semantics and accessibility
- To structure the content it will be used the [HTML5 sectioning ](http://blog.teamtreehouse.com/use-html5-sectioning-elements) recommendations: `section, nav, aside, article, main, header, footer`.

- For better accessibility will be added [ARIA roles](http://www.paciellogroup.com/blog/2013/02/using-wai-aria-landmarks-2013/) that will added meaning to specific areas of each page. More details in [WAI-ARIA](#wai-aria) section of this same document.

### Attributes for accessible inputs
- To help accessibility on mobile devices, the use of `type` attribute within `<input />` with values oriented to the use of them, as listed below:
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

### Favicons
- For any *responsive* project the following `<meta>` and icons/favicons should be considered:

```html
<!-- iPad retina iOS ≥ 7: -->
<link rel="apple-touch-icon-precomposed" sizes="152x152" href="/assets/images/favicon-152.png">

<!-- iPad retina iOS ≤ 6: -->
<link rel="apple-touch-icon-precomposed" sizes="144x144" href="/assets/images/favicon-144.png">

<!-- iPhone retina iOS ≥ 7: -->
<link rel="apple-touch-icon-precomposed" sizes="120x120" href="/assets/images/favicon-120.png">

<!-- iPhone retina iOS ≤ 6: -->
<link rel="apple-touch-icon-precomposed" sizes="114x114" href="/assets/images/favicon-114.png">

<!-- For first and second generation iPad: -->
<link rel="apple-touch-icon-precomposed" sizes="72x72" href="/assets/images/favicon-72.png">

<!-- no-retina iPhone, iPod Touch, Android 2.1+ devices: -->
<link rel="apple-touch-icon-precomposed" href="/assets/images/favicon-57.png">

<!-- Fallback -->
<link rel="icon" href="/assets/images/favicon-32.png" sizes="32x32">
<link rel="icon" type="image/x-icon" href="/assets/images/favicon.ico">

<!-- IE10 Metro icon (change color #FFFFFF) -->
<meta name="msapplication-TileColor" content="#FFFFFF">
<meta name="msapplication-TileImage" content="/path/to/favicon-144.png">
```

And in *.jade*:

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

### Social Meta / Opengraph
- For better indexation of social networking systems must be integrated `<meta>` tags matching [Opengraph](https://developers.facebook.com/docs/reference/opengraph/object-type/product/) and [Twitter Cards](https://dev.twitter.com/cards/types/product) standards and oriented to *e-commerce* as shown below:

```html 
<!-- Twitter Cards -->
<meta name="twitter:site" content="@TWITTER_USERNAME" />
<meta name="twitter:creator" content="@TWITTER_USERNAME" />
<meta name="twitter:card" content="product" />
<meta name="twitter:label1" content="price" />
<meta name="twitter:data1" content="$PRICE" />
<meta name="twitter:label2" content="brand" />
<meta name="twitter:data2" content="BRAND" />
<meta name="twitter:image" content="http://URL_IMAGE_500X500PX">
<!-- OpenGraph -->
<meta property="og:site_name" content="SITENAME" />
<meta property="og:url" content="http://URL_SITE/PRODUCT" />
<meta property="og:title" content="TITLE_PRODUCT" />
<meta property="og:description" content="DESCRIPTION_MAX_180_CARACTS" />
<meta property="og:image" content="http://URL_IMAGE_500X500PX" />
<meta property="og:type" content="product" />
<meta property="og:price:amount" content="PRICE" />
<meta property="og:price:currency" content="CURRENCY" />
<meta property="og:availability" content="AVAILABILITY('instock','oos','pending)" />
<meta property="fb:app_id"  content="ID_APP_FB" /> 
```

And in *.jade*:

```jade
// Twitter Cards
meta(name='twitter:site', content='@TWITTER_USERNAME')
meta(name='twitter:creator', content='@TWITTER_USERNAME')
meta(name='twitter:card', content='product')
meta(name='twitter:label1', content='price')
meta(name='twitter:data1', content='$PRECIO')
meta(name='twitter:label2', content='brand')
meta(name='twitter:data2', content='MARCA')
meta(name='twitter:image', content='http://URL_IMAGE_500X500PX')
// OpenGraph
meta(property='og:site_name', content='SITE_NAME')
meta(property='og:url', content='http://URL_SITE/PRODUCT')
meta(property='og:title', content='TITLE_PRODUCT')
meta(property='og:description', content='DESCRIPCION_MAX_180_CARACTS')
meta(property='og:image', content='http://URL_IMAGE_500X500PX')
meta(property='og:type', content='product')
meta(property='og:price:amount', content='PRICE')
meta(property='og:price:currency', content='CURRENCY')
meta(property='og:availability', content="AVAILABILITY('instock','oos','pending)")
meta(property='fb:app_id', content='ID_APP_FB')
```

Links:
- [Twitter Cards Validator](https://cards-dev.twitter.com/validator)
- [Facebook Debugger](https://developers.facebook.com/tools/debug/)


### Boilerplate & Workflow
As a basis for all new web projects in I2B, the use of a boilerplate that have the minimum elements required to start the templating of any project and deliver minimum IE8 browser support:

	* GruntJS
	* SCSS (CSS pre-processor)
	* Jade (HTML pre-processor)
	* mixins básicos
	* jQuery.js
	* lt-ie9.js (selectivizr.js + html5shiv.js + respond.js)
	* CSS3 Pie
	* Modernizr + Detectizr
	* standard folder structure

The generated HTML contains the following structure:

```html
<!DOCTYPE html(lang='es')>
<head>
  <meta charset="utf-8"/>
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/>
  <meta name="viewport" content="width=device-width"/>
  <title></title>
  <link rel="stylesheet" href="assets/css/style.css"/>
  <!--[if lt IE 8]>
  <script src="assets/js/libs/lt-ie9.js"></script>
  <![endif]-->
  <script src="assets/js/libs/modernizr-detectizr.js"></script>
</head>
<body>
  ...
  
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.2/jquery.min.js"></script>
  <script>window.jQuery || document.write('<script src=assets/js/libs/jquery.js><\/script>');</script>
  <script src="assets/js/functions.js"></script>
</body>
```

[I2B Frontend WorkFlow >](https://github.com/I2BTech/i2b-frontend-workflow)

CSS
=====

### Inclusion
- The CSS files should be included in HTML pages as close as possible to the end of the `</head>`. HTML5 standard no longer a need to use the `type` attribute as it is the server that is responsible for determining the correct `MIME type`.

### Header
- In all base CSS file should be placed in the first lines the following header as CSS comments, which should be completed by the developer in charge of the project:

``` css
/* ===========
 * Project name:
 * Start date:
 * Developer email:
 * ======== */
```

###Sintaxis
- Use 2 spaces (*soft tab*) / 1 tab (*hard tab*) to indent.

###Pre-processing
- We use [SCSS](http://sass-lang.com/) as CSS pre-processor, which is the version 3 of **SASS**.

- Prefer the use of *mixins* and *functions*, but don't abuse. Avoid using *@extend* as it may add unnecessary code if misused.

- Do't indent over 3 levels of specificity.

- Save repetitive values in variables with clear nomenclature. Remember that you can create * scope* for the same variable.

- Add a blank line-break before starting a new item or statement elements to maintain source-code readability.

``` css
selector {
	property: value;
}

otherselector {
	property1: value1;
	property2: value2;
}
```

- If you define styles for more than one child selector, separate them with a line break:

``` css
selector {
	property: value;
	  
	.child-selector {
	
		selector2 {
			property1: value1;
			property2: value2;

			&:hover {
				property: value;
			}
		}
	}
}
```

- If you define the same styles for more than one selector, use line-breaks:

``` css
selector1,
selector2 {
	property: value;
}
```

### Declarations
- Prefer the order of your CSS declarations in the following order:
	 * display / box model
	 * position
	 * font/typo
	 * colors
	 * others

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

### Units and colors
- Omit the unit is value is `0`:

``` css
// Good
padding: 0;

// Avoid
padding: 0px;
```

- Skip the `0` if this is in the left of the value:

``` css
// Good
margin: .5em;

// Avoid
margin: 0.5em;
```

- Define all colors as variables and shades with operations as `darken ()` and `lighten ()`:

```css
$alert: #f00; // red
$alertHover: darken($alert, 20%); // 20% darker red
```

- Hexachrome colors prefer to summarize with only 3 characters:

``` css
// Good
color: #f00;

// Avoid
color: #ff0000;
```

###Comentarios
- Comment large blocks of sections as follows (all caps):

``` css
/* -----------
 * HOME
 * -------- */
```

- For minor comments, local or just to remember something, use `//` because pre-processors will ignore while compile to CSS:

``` css
// :target color change
```

### Specificity
- Use the least amount of selectors to style an element; prefer the use of classes.

- If you use classes or IDs, avoid adding the selector:

``` css
// Good
.classname {}

// Avoid
selector.classname {}
```

### Naming classes and IDs
- For names with more than 1 letter, use dash `-` (and not an underscore `_`). Never begin with a digit

- If you need to manipulate HTML elements with JavaScript, use the HTML5 attribute `data-` to identify and define/save its value. If you prefer using classes, use the prefix `js-` only if it is used for that purpose and not to style:

``` html
// Good
<tag data-value="value" />
<tag class="js-openmodal" />
```

- Create descriptive classnames to the context and / or role of the element rather than its appearance:

``` css
// Good
.modal {}
.title {}

// Avoid
.big {}
.red {}
```

Avoid using IDs, unless necessary for unit tests (Selenium and others). Read before the [unit tests naming guide](guia-nomenclatura-tests-unitarios_EN.md).

### Media Queries
- Declare `@media` queries at the end of the CSS file, which define the behavior modification/style elements already declared.
- In large projects involving more than one frontend developer, it is recommended to use different style sheets for each `@ media` and that each one code on different files under one the same HTML sharing the responsive structure:

```html
link(rel='stylesheet', media='screen and (min-width: 701px) and (max-width: 900px)', href='css/main.css')
```
- For any project that requires responsive grid behavior, it is recommended the use of [Bootstrap](http://getbootstrap.com/customize/) (customized) in its latest version, which allows support from IE8 (by respond.js) and construction of responsive/adaptive layouts.

### Mixins

The file 'src/sass/inc/mixins.sass` is included with several mixins which are divided into 2 groups: the prefix and the rest.

#### Prefix
Help the support of CSS prefixed properties that are still needed for proper display on browsers. However, prefer the use of **grunt-autoprefixer** plugins which is configured to add prefixes (standards) directly to the CSS files generated by SCSS  corresponding to the last 2 versions (current and previous) of the main browsers and specific versions of IE 8 and 9.

Keep in mind that Microsoft created filters (non-standard) which are included in this mixins, eg `opacity` y `background: linear-gradient();`.

#### The rest
The other mixins are detailed below:

- **out($color:red)**: used for debugging, adds to the selector a 1px outline color; (red default).

- **escondetxt()**: hides a text with the classic `text-indent: -9999px; overflow: hidden;`

- **zero()**: basic and universal reseter `margin:0; padding:0;`

- **gradient-vertical($startColor,$endColor)**: easier vertical gradients, from up to down: 

- **gradient-horizontal($startColor,$endColor)**: easier horizontal gradients, from left to right:

### @extend and @include

- Prefer group `@include` declarations at the top of the block and after the `@extend` declarations:

```scss
.selector {
	@extend .element;
	@include clearfix();
	
	width: 5em;
}
```

### Style inheritance

- Careful with style inheritance and avoid direct child selector `>`; use it only when necessary (eg. when several selectors want to reach children who do not need a declared class):

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

In this caase if you don't define `.article-link > .count` this style whould be inherited by `.box-vote .count`.

JavaScript
=====

### Inclusion
- The JavaScript files must be included in the HTML pages as close as possible to the end of the `</body>` tag, reducing the effect of delays imposed by the load script and other components of the page. HTML5 no longer need to use the attributes `type`  and/or `language` because it is the server the responsible for determining the correct `MIME type`. The exceptions to this correspond to libraries whose functionality is based on the construction of the DOM before implementation, such as:
	- Modernizr + Detectizr
	- HTML5Shiv
	- Google Analytics

### Header
- In any JavaScript file will placed in the first lines of the same the following header as comments, which should be completed by the developer in charge of the project:

``` javascript
/* ===========
 * Project name:
 * Start date:
 * Developer email:
 * ======== */
```

### Syntax
- Use 2 spaces (*soft tab*) / 1 tab (*hard tab*) to indent.
- Use double quotes `"` to open and close attributes, properties and/or values.

### Comments
- For each new feature uses the following comment block as basis for documentation:

``` javascript
/**
 * Descriptive name:
 * Functionality: / what it does
 * Where: Where used (element, page, etc)
 * Developer email: 
 * Use:
  	var myFunction = function (
		@param1: int|bool|element|ranges|etc,
		@param2: int|bool|element| ranges |etc
	) {
		return: bool;
	};
 */
```

### Naming

- The JavaScript files created should have his name in capital letters, without spaces or special characters. If the contents of the file corresponds to a jQuery plugin, it must be clearly identified as a dependent library and it is allowed the use of *camelCase* naming, as follows:

```
jquery.pluginName-version.min.js
```

- Create function names, parameters, methods, variables and attributes in English, descriptive to it's context and/or role of the element *camelCased* without space after the name and before the space *bracket* `{`. 

``` javascript
// Good
function openModalWindow() {}

// Bad
function close () {}
```

- All variables must be declared before being used. It preferred that each variable is declared in a new line and with inline comment. If it depends directly from jQuery, prefix `$` before the variable name:

``` javascript
var $element, 	// this
	 $indent,		// indentation level
	 $width;		// element's width (int)
```

- Always search for the existence of the element before adding an event or applying a function:

``` javascript
if ( $element.length ){
	...
}
```

- The use of global variables should be only if really necessary. If used, use UPPERCASE in his name to identify it clearly.

- if/else, switch, for, try, catch must meet the following format spacing for better reading and sorting:

``` javascript
if ( condition ) {
	//
} else if ( condition ) {
	//
} else {
	//
}

switch ( expression ) {
	case expression:
		//
	default:
		//
}
```
- Always place 1 space before and after operators:

``` javascript
var x = (y + z) * w;

for (i = 0; i < 10; i++) {
    x += i;
}
```

### Libraries

- For backwards compatibility and better/faster development at *I2B* we use [jQuery](http://www.jquery.com/) as default JavaScript library. Prefer branch 1.1x that still has support for IE7+.

- Call jQuery first from a **CDN** and followed the local copy, as in the following example:

``` html
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
<script>window.jQuery || document.write(unescape('%3Cscript src="assets/js/libs/jquery-1.11.3.min.js"%3E%3C/script%3E'))</script>
```

URL's
=====

- Prefer relative URLs to link CSS, JavaScript and image files.
- If you have external links (such as JavaScript libraries, fonts through a CDN) avoid the use of the protocol in the URL:


``` html
// Good
<script src="//www.dominio.com

// Avoid
<script src="http://www.dominio.com
```

Images
=====

- Prefer the use of Icon Fonts over images (request them to the designer before starting the project).

### Formats

- Supported image formats for web today are: **JPG**, **PNG** y **GIF**. **SVG** is supported with *fallback* to **PNG**.
- Names and formats should always be lowercase.

### Temporary

- For images that are used only as layout and not part of the final design (banners, products and all *simulated* image) should be stored in the `src/images/TEMP` directory to not be considered as part of the final release and be easily erased once in production or integrated with other languages.

### Naming

The following nomenclature is proposed using prefixes according the use of the image:

- **Icons**: **ico-**imagename.format
- **Buttons**: **btn-**imagename.format
- **Logos**: **logo-**imagename.format
- **Banners**: **banner-**imagename.format
- **Backgrounds**: **bg-**imagename.format

It is recommended that save the icons, logos and buttons into the `src/images/sprites` directory in order to **GruntJS** can generate sprites from them. Others images can be placed in `src/images` so they'll be optimized too but not as sprites.

### Optimization

- Every image must be compressed using the best method depending on the format. It is recommended the use of *GruntJS* plugin  named **imagemin** which supports the following compression methods:
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
- Prioritize the use of sprites for all types of images that are linkeadas through CSS styles as icons, logos. The only exception is background images that work as a pattern. For automatic generation of sprites should be stored in `src/images/sprites`:

```
project-name/
|__ src
	|__images
		|__ sprites
```

The following files will be automatically generated: `sprites.png` and `sprites.scss`:

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


Fonts (typefaces)
=====

- Prefer the use of typefaces in the [Google Fonts](http://www.google.com/fonts/) catalog and call them directly from their **CDN**.
- Include fonts from Google Fonts using the `<link>` tag and never using the `@import` CSS property:

```html
<link rel="stylesheet" href="//fonts.googleapis.com/css?family=Open+Sans">
```

- In case you need more than one font, concatenate them in the same call:

```html
<link rel="stylesheet" href="//fonts.googleapis.com/css?family=Open+Sans|Droid+Sans">
```

- In case you need customized fonts or Icon fonts, they will be stored directly in the `dist/assets/fonts` directory as their not part of **GruntJS** workflow.
- Prefer using `px` as unit for `font-size`, as it offers total control over text on the expected design. 
- Avoid using units to define `line-height` as it don't inherit the value based on the percentage value, but in its multiplier unit as `font-size`.

```css
// Good
selector {
   line-height: 1.2;
}
```

- For local web fonts, use the following formats order to call them:

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


SEO/Metrics
=====

### Google Analytics

Use the following code before the closing `</head>` and replacing **UA-XXXX-Y**:

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

### Google Tag Manager

Use the following code after the open `<body>` tag, replacing **GTM-XXXX**:

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

### Schema

SEO is an essential part of online marketing and the correct implementation of [Schema](https://schema.org/docs/documents.html) to the strategy is strong support. The main attributes that are used in e-commerce sites targeted products (retail) are:

- Product rating
- Brands model
- Offers & reviews
- Product ID

And its implementation (as example) in a box product, using HTML code :

```html
<div class="box-product" itemscope itemtype="http://schema.org/Product">   
  <img src="samsung-tv-led-42.jpg" itemprop="image">
  <h1>
    <span itemprop="brand">Samsung</span>
    <span itemprop="name">TV LED 42 pulgadas</span>
    <span itemprop="sku">506246</span>
  </h1>
  <div itemprop="aggregareRating" itemscope itemtype="http://schema.org/aggregateRating">
    <span itemprop="ratingvalue">8</span> of <span itemprop="bestRating">10</span> based in <span itemprop="ratingCount">87</span> opinions.
  </div>
  <div itemprop="offers" itemscope itemtype="http://schema.org/aggregateOffers">
    Before: <span itemprop="highPrice">$189.990</span>
    After: <span itemprop="lowPrice">$149.990</span>
  </div>
</div>
```
[Structured Data Testing Tool | Google](https://developers.google.com/structured-data/testing-tool/)

[Structured data validator | Yandex](https://webmaster.yandex.com/microtest.xml)


WAI-ARIA
=====

For better accessibility, web development must implement **WAI-ARIA**, the standard recommended by the W3C for such purpose. [The skeleton can be found on Github](https://github.com/I2BTech/ariabones) which is constantly updated.



Software
=====

In I2B we use two software which the company will provide licenses:

- Mac OS X: [Sublime Text](http://www.sublimetext.com/)
- Windows: [Sublime Text](http://www.sublimetext.com/) or [Aptana](http://www.aptana.com/)

### Complements

#### Sublime Text packages
- [Jade.tmbundle](https://packagecontrol.io/packages/Jade)
- [Syntax Highlighting for Sass](https://packagecontrol.io/packages/Syntax%20Highlighting%20for%20Sass)
- [Emmet](https://packagecontrol.io/packages/Emmet)
- [Color Highlighter](https://packagecontrol.io/packages/Color%20Highlighter)

#### Photoshop complements
- [CSS Hat](https://csshat.com/)


Local
=====

- The local development environment must run in `http://localhost/` and includes:
	- Apache
	- MySQL
	- PHP
	- NodeJS


Links
=====

- [SCSS](http://sass-lang.com/)
- [Jade](http://jade-lang.com/reference/)
- [Normalize.css](http://necolas.github.io/normalize.css/)
- [Bootstrap](http://getbootstrap.com/)
- [Schema](https://schema.org/docs/documents.html)

##### Contributor
- [Jorge Epuñan](https://github.com/juanbrujo/)
