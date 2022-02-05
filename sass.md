# This is Sass and SCSS


## How to use
SCSS and CSS can use same syntax.

```SCSS
.button{
	padding:10px;
	font-size:20px;
}

```
following syintax is studied from  https://sass-lang.com/documentation/style-rules


### Nesting
SCSS can nest structure.

```SCSS
h2 {
	ul {
	margin:0;
	padding:0;
	}
}

```

### Selector lists

```SCSS
.class1, .class2 {
	ul, p {
	margin:0;
	padding:0;
	}
}
```
then
```css
ul.class1, p.class1, ul.class2, p.class2{...}

```

### Selector combination

```SCSS
ul>{
	li{
	margin:0;
	}
}

h3 {
	+ p {
	font-size:10px;
	}
}

p {
	~ {
		span {
		font-color:blue;
		}
	}
}

```

### Interpolation 
replacement from mixin to include.
mixin variable and include variable against one by one.

```SCSS
@mixin define-content($name, $glyph){
	span.class-#{$name}{
		font-size:10px;
		content:$glyph;
	}
}

@include define-content("classname","++");

```
```css
span.class-classname{
	font-size:10px;
	content:"++";
}
```

Link: https://sass-lang.com/documentation/style-rules/declarations

## Property declarations

```SCSS
.class {
	$size: 100px;
	width:$size;
	height: $size;
	border-radius:$size * 0.5;
}
```

### inaterpolation

```SCSS
// @each is same as for in python.
@mixin prefix($property, $value, $prefixes){
	@each $prefix in $prefixes{
		-#{$prefix}-#{$property}:$value;
	}
	#{$property}:$value;
}

// array is separated by space.
.gray{
	@include prefix(filter, grayscale(50%), moz webkit)
}

```
### Property nesting

```SCSS
.class{
	font-size:10px;
	transition:{
		property:font-size;
		duration:4s;
		delay:2s;
	}
	// connect suffix uses "&"
	&:hover{font-size:36px;}
}
```
```css
.class {
  font-size: 10px;
  transition-property: font-size;
  transition-duration: 4s;
  transition-delay: 2s;
}
.class:hover {
  font-size: 36px;
}
```

Shorthands nesting

```SCSS
.class{
	margin:auto{
		top:10px;
		bottom:0px;
	}
}
```

```css
.class{
	margin:auto;
	margin-top:10px;
	margin-bottom:0px;
}

```

### hidden declaration
You need unnecessary using property.

```SCSS
$round-edge: false;
.class {
	border: 1px solid blue;
	border-radius: if ($round-edge, 10px, null); // cannot convert to css
}

```

### custom property

variable shall use #{ variable }

```SCSS
$variable1: #818181;
$variable2: blue;
$variable3: #000000;

:root{
	--primary:#{variable1};
	--accent:#{variable2};
	--warn:#{variable3};

	--consumed-by-js:$variable1; // Error. You shall use #{ variable } phrase.
}

```
## Parent selector

"&" symbol can be replaced from parent.

```SCSS
.class{
	&:hover{
		font-size:10px;
	}
	[dir=rtl] & {
		margin-left:0;
		margin-right:10px;
	}

	:not(&){
		opacity:0.5;
	}

}

```

### Adding suffixes

You can easily add suffix when you use "&" symbol.

```SCSS
.class{
	padding:10px;
	&__copy{
		margin:10px;
		width:10%;
	}

	&--open{
		display:block;
	}
}

```

Link: https://sass-lang.com/documentation/style-rules/placeholder-selectors

## Placeholder Selectors

"%" symbol uses prefix.
if you use "%", selector, parameter, and etc. are not included in CSS.

```SCSS
.alert:hover, %.class{
	font-weight:bold;
}
// .class does not generate in CSS.

%.class:hover{
	font-size:10px;
}
// .class:hover does not generat in CSS.

```

```SCSS
%toolbelt{
	padding:10px;
	
	&:hover{
		border:2px blue solid;
	}
}

.action-buttons{
	@extend %toolbelt;
	color:blue;
}

```

extend can use replacement.
CSS is

```css
.action-buttons{
	padding:10px;
}

.action-buttons:hover{
	border:2px blue solid;
}

.action-buttons{
	color:blue;
}

```

Link: https://sass-lang.com/documentation/variables


## variables

### definition

Top level definition SCSS file.
```SCSS
@use 'url-library.scss' with{
	$black:#222, // you use "," in variable list.
	$border-radius: 0.1 rem
}
```
Child css "/library.scss" 
```SCSS
$black:#000 !default;
$border-radius:0.5rem !default;
$box-shadow: 0 0.5rem 1rem rgba($black, 0.15) !default;
// default is replaced from top level definition SCSS when it is defined variable.

code{
	border-radius: $border-radius;
	box-shadow: $box-shadow;
}

```

Generated css is

```css
code{
	border-radius:0.1rem;
	box-shadow:0 0.5rem 1rem rgba(34, 34, 34, 0.15);
}
```

### Valrable scopes

```SCSS
$global-variable:global value;
// Global variable is defined out of selector.

.class{
	$local-variable:local value;
	font-size:$global-value;
	color:$local-variable;
}

.class1{
	font-size:$global-value;
	// color:$local-valiable  ... this is fail. local variable cannot defined from selector.
}

.class2{
	$gloval-variable:local value;
	color:$gloval-variable; // css out put is local value. local variable is strogner than gloval variable. You can replace value when accident condition.
	$local-variable:glovbal value !global; // Gloval variable is defined in local area when it uses !global.
}

.class3{
	value: $local-valiable; // css output is global value.
}

```
## At rule

Link: https://sass-lang.com/documentation/at-rules/use

### @use

```SCSS
// in foundation/_code.scss
code{
	padding:10px;
	line-height:10px;
}

// in foundation/_list.scss
ul, ol {
	test-align:left;

	& & {
		padding:{
			bottom:0px;
			left:0px;
		}
	}
}

// in style.css
@use 'foundation/code';
@use 'foundation/lists';

```
### Loading memmbers

```SCSS
// src/_corners.scss
$radius:3px;

@mixin rounded{
	border-radius:$radius;
}

// style.scss
@use "src/corners";

.button{
	@include corners.rounded;
	padding:5px + corners.$radius;
}

// same as following method
// style.scss
@use "src/corners" as c;

.button{
	@include c.rounded;
	padding:5px + c.$radius;
}

```

### @import

```scss
// in foundation/_code.scss
code{
	padding:10px;
	line-height:10px;
}

// in foundation/_list.scss
ul, ol {
	test-align:left;

	& & {
		padding:{
			bottom:0px;
			left:0px;
		}
	}
}

// in style.css
@import 'foundation/code';
@import 'foundation/lists';


```

