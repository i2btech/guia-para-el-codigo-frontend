Mutable CSS
=====

**CSS standard structure using <u>Regions</u>, <u>Components</u>, <u>Elements</u> and <u>Mutable</u>.**


### TL;DR

- Define **regions**, reusable zones that make up your layout and use HTML sectioning tags: `section, nav, aside, article, main, header, footer`. declare them using semantic IDs in HTML. 
- Create **components** modular components and name them with two words separated by a dash (`-`): `.screenshot-image`.
- Components contain **elements**, name them with one word: `.title`.
- Components and elements have **mutable**, variations prefixed with a dash (`-`) and with 2 types: 
	- *design* variations: `-large`, `-small` 
	- *state* variations: `-disabled`, `-active`
- Components and elements can be inherited and shouldn't have positioning and sizing properties; if necessary define them on it's context and use the regions if you need support.


Regions
---------------

Every layout is composed by global regions, which are defined by the [HTML5 sectioning recommendations](http://blog.teamtreehouse.com/use-html5-sectioning-elements). These regions are identified through the `id=""` attribute formed of a single word, which will privede access for analytics/tag manager configuration. You can rely on these `ID's` to define styles, but beware of its specificity weight as it can be harmful when misused (in doubt, better to avoid)


![Regions](https://raw.githubusercontent.com/I2BTech/MutableCSS/master/images/regiones.png)

Examples of common regions are listed below:

- `#header`
- `#content`
- `#sidebar`
- `#footer`


Components
---------------

Each piece of the interface corresponds to a single *component*. Components are named with **at least 2 words in english and separated by a dash (`-`), for example:

* A menu (`.menu-header`)
* A search form (`.form-search`)
* A user profile box (`.box-user-profile`)

![Component](https://raw.githubusercontent.com/I2BTech/MutableCSS/master/images/componente.png)

Note that the component starts with the type of component (**menu, form, box**)and the next word is the context or unique location in a region or function (**header, search, user profile**). This is to quickly and easily identify similar types of components, because as we know there will exist several `.menu-` and lots of `.box-` among others.

#### Nested components

![Nested components](https://raw.githubusercontent.com/I2BTech/MutableCSS/master/images/componente-anidado.png)

It is permited to nest components if required:

```html
<div class='box-article'>
	<div class='box-vote'>
  		...
	</div>
	<h3 class='title'>...</h3>
	<p class='meta'>...</p>
</div>
```

#### Common components

A [list of common components](common-components_EN.md) is defined for e-commerce projects which contains the necessary nomenclature for each of them. It is requested to respect this list, which will be constantly updated whenever necessary improvement.

Elements
---------------

Each component contains one or more elements. Class names for elements **have only one word**:

```scss
.form-search { // component

	.field	{ /* ... */ }	// element
	.button	{ /* ... */ }	// element
}
```

![Elements](https://raw.githubusercontent.com/I2BTech/MutableCSS/master/images/elementos.png)

**Multiple words:** When needd the use of composite names for your class, let them together without separation:

```scss
.box-user-profile {

	.firstname 	{ /* ... */ }
	.lastname 	{ /* ... */ }
	.email 		{ /* ... */ }
}
```

**Avoid selectors tags:** prefer CSS classes instead of HTML tags as selectors, for improved performance and semantics.

```scss
.box-user-profile {

	h3    		{ /* nope */ }
	.firstname 	{ /* good */ }
}
```

If you see the need for it (for example, to all styles `<p>` in a `<div class="box-content">` use the direct child selector `>`:

```scss
.box-content {

	> p { /* ok then, use it */ }
}
```

Mutable
---------------

![Mutable](https://raw.githubusercontent.com/I2BTech/MutableCSS/master/images/componente-mutable.png)

Components and elements are mutable so they can have variations of styles regarding the general definition. For this case create CSS classes to provide changes to the original styles and use a dash (`-`) as prefix to identify a mutable:

```scss
.box-user-profile {

	&.-wd { }
	&.-sm { }
}

.button {

	&.-disabled { }
}
```

The types of mutable are classified into 2 groups: design and state

#### Design
The ones that change the style of the element or component and the most common are listed below:

- wide: `.-wide`
- narrow: `.-narrow`
- big: `.-big`
- small: `.-small`
- tall: `.-tall`
- short: `.-short`
- large: `.-large`
- lower: `.-lower`
- upper: `.-upper`
- centered: `.-centered`
- bold: `.-bold`
- light: `.-light`

#### State
Those that change the state/behaviour of an element or component and common are:

- `.-disabled`
- `.-enabled`
- `.-visible`
- `.-hidden`

**Use:**

```html
<input class="button-send -disabled" />
```

It is allowed to use multiple mutable by component/element:

```html
<input class="button-send -wide -disabled" />
```

General considerations
---------------

**Fixed sizes**: avoid setting fixed width/height to components; Exceptions could be avatars, vote boxes and so.

**Avoid positioning properties**: components and elements must be created in a way that they are reusable in different contexts and must respect the grid that contains them.

Avoid:

* Positioning (`position`, `top`, `left`, `right`, `bottom`)
* Floats (`float`, `clear`)
* Margins (`margin`)
* Sizes (`width`, `height`)

And use the classes that the grid use to wrap and position the elements and it's responsive behaviour.

**Define size and position in the context not in the component:** If you need to define these properties, do it in the context of the component (or in the region that contains it) is not in the component definition:

```css
// CONTEXT
. list-article {

	.box-article {
		width: 33.3%;
		float: left;
	}
}
// REGION
#header {

	.box-article {
		width: 33.3%;
		float: left;
	}
}

// COMPONENT
.box-article {
  /* ... */
  
  // ELEMENTS
  .image 	{ /* ... */ }
  .title 	{ /* ... */ }
  .meta 	{ /* ... */ }
}
```


#### Licence:

> **Mutable CSS** is distributed under [Creative Commons Attribution-ShareAlike 4.0 International](http://creativecommons.org/licenses/by-sa/4.0/) license. 

> Copyright (c) 2015 by [Jorge Epuñan](https://github.com/juanbrujo) to [I2B Technologies](https://github.com/I2BTech)