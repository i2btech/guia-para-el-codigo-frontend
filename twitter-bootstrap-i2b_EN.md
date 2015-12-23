# Bootstrap Components for I2B

This document was build to normalize the naming conventions to build web interfaces using HTML, CSS and JavaScript based on *Twitter's Bootstrap Framework* (v3) and it's [Twitter Boostrap Components Documentation](http://getbootstrap.com/components/).

---

## Tabs
**CSS Class:** `.nav-tabs`

**Example:**
```
<ul class="nav nav-tabs">
  <li class="active"><a href="#">...</a></li>
  <li><a href="#">...</a></li>
  <li><a href="#">...</a></li>
</ul>
```
**Requirement:** [Togglable tabs tab.js](http://getbootstrap.com/javascript/#tabs)

## Navbar
**CSS Class:** `.navbar`

**Example:**

```
<nav class="navbar navbar-default">
   ...
</nav>
```
**Requirement:** [Collapse collapse.js](http://getbootstrap.com/javascript/#collapse)

## Brand image
**CSS Class:** `.navbar-brand`

**Example:**
```
<a class="navbar-brand" href="#">
   <img alt="Brand" src="...">
</a>
```

## Forms
**CSS Class:** `.navbar-form`

**Example:** 
```
<form class="navbar-form">
  <div class="form-group">
    <input type="text" class="form-control" placeholder="Search">
  </div>
  <button type="submit" class="btn btn-default">Submit</button>
</form>
```

## Button
**CSS Class:** `.btn`

**Example:** 
```
<a class="btn btn-default" href="#">Link</a>
<input class="btn btn-default" type="button" value="Input">
<input class="btn btn-default" type="submit" value="Submit">
<button class="btn btn-default" type="submit">Button</button>
```

### Button group
**CSS Class:** `.btn-group`

**Example:** 
```
<div class="btn-group">
  <button type="button" class="btn">Left</button>
  <button type="button" class="btn">Middle</button>
  <button type="button" class="btn">Right</button>
</div>
```

### Button toolbar
**CSS Class:** `.btn-toolbar`

**Example:** 
```
<div class="btn-toolbar">
  <div class="btn-group">...</div>
  ...
</div>
```

## Input
**CSS Class:** `.form-control`

**Example:** `<input type="text" class="form-control" placeholder="Text field">`

### Input group
**CSS Class:** `.input-group`

**Example:**
```
<div class="input-group">
  <span class="input-group-addon" id="basic-addon1">@</span>
  <input type="text" class="form-control" placeholder="Username">
</div>
```

## Checkbox & radio 
**CSS Class:** `.input-group`

**Example:**
```
<div class="input-group">
  <input type="checkbox" class="input-checkbox">
  <label for="">hola</label>
</div>
<div class="input-group">
  <input type="radio" class="input-radio">
  <label for="">hola</label>
</div>
```
**Requirement:** TODO

## Select
**CSS Class:** `.input-group`

**Example:**
```
<div class="input-group">
  <select class="input-select">
    <option>...</option>
    <option>...</option>
    <option>...</option>
  </select>
</div>
```
**Requirement:** [bootstrap-select](https://silviomoreto.github.io/bootstrap-select/)

## Breadcrumbs
**CSS Class:** `.breadcrumb`

**Example:**
```
<ol class="breadcrumb">
  <li><a href="#">Home</a></li>
  <li><a href="#">Page 1</a></li>
  <li class="active">Page 2</li>
</ol>
```

## Pagination
**CSS Class:** `.pagination`

**Example:**
```
<nav>
  <ul class="pagination">
    <li class="disabled"><a href="#"><span>&laquo;</span></a></li>
    <li class="active"><a href="#">1</a></li>
    <li><a href="#">2</a></li>
    <li><a href="#">3</a></li>
    <li><a href="#"><span>&raquo;</span></a></li>
  </ul>
</nav>
```

## Page header
**CSS Class:** `.page-header`

**Example:**
```
<div class="page-header">
  <h1>Page header <small>Subtext</small></h1>
</div>
```

## Thumbnails
**CSS Class:** `.thumbnail`

**Example:**
```
<div class="row">
  <div class="col-xs-6 col-md-3">
    <a href="#" class="thumbnail">
      <img src="..." alt="...">
    </a>
  </div>
  ...
</div>
```

## Alerts
**CSS Class:** `.alert`

**Example:**
```
<div class="alert alert-success">Success!</div>
```

### Links in alerts
**CSS Class:** `.alert-link`

**Example:**
```
<div class="alert alert-success">
   Success!
   <a href="#" class="alert-link">...</a>
</div>
```

## Progress bars
**CSS Class:** `.progress` y `.progress-bar`

**Example:**
```
<div class="progress">
   <div class="progress-bar" style="width: 60%;">60%</div>
</div>
```

## Media object
**CSS Class:** `.media` y `.media-object`

**Example:**
```
<div class="media">
  <div class="media-left">
    <a href="#">
      <img class="media-object" src="..." alt="...">
    </a>
  </div>
  <div class="media-body">
    <h4 class="media-heading">Media heading</h4>
    <p>...</p>
  </div>
</div>
```

## List linked group
**CSS Class:** `.list-group`

**Example:**
```
<nav class="list-group">
  <a href="#" class="list-group-item active">
  	<span class="badge">14</span>
  	...
  </a>
  ...
</nav>
```

## Tables
**CSS Class:** `.table`

**Example:**
```
<table class="table">
  ...
</table>
```

## Images (responsive)
**CSS Class:** `.img-responsive`

**Example:**
```
<img src="..." class="img-responsive" alt="...">
```

## Modal windows
**CSS Class:** `.modal`

**Example:**
```
<div class="modal fade">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal"><span>&times;</span></button>
        <h4 class="modal-title">...</h4>
      </div>
      <div class="modal-body">
        <p>...</p>
      </div>
    </div><!-- /.modal-content -->
  </div><!-- /.modal-dialog -->
</div><!-- /.modal -->
```
**Requirement:** [modal.js](http://getbootstrap.com/javascript/#modals)

## Popover
**CSS Class:** `.btn-popover`

**Example:**
```
<button type="button" class="btn btn-default btn-popover" data-toggle="popover" title="Popover title" data-content="And here's some amazing content. It's very engaging.">Popover</button>
```
**Requirement:** [popover.js](http://getbootstrap.com/javascript/#popovers)

## Collapsible / Accordion
**CSS Class:** `.collapse` and/or '.panel-collapse`

**Example:**
```
<a class="btn btn-primary" data-toggle="collapse" href="#collapseExample">
  Collapsible
</a>
<div class="collapse" id="collapseExample">
  ...
</div>
```
**Requirement:** [collapse.js](http://getbootstrap.com/javascript/#collapse)

## Carousel
**CSS Class:** `.carousel`

**Example:**
```
<div id="carousel-example" class="carousel slide" data-ride="carousel">
   <div class="carousel-inner" role="listbox">
	   <div class="item active">
	      <img src="..." alt="...">
	  	</div>
	  	...
	</div>
	...
</div>
```
**Requirement:** [carousel.js](http://getbootstrap.com/javascript/#carousel)


