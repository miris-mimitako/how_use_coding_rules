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
mixin valiable and include valiable against one by one.

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

Valiable shall use #{ valiable }

```SCSS
$valiable1: #818181;
$valiable2: blue;
$valiable3: #000000;

:root{
	--primary:#{valiable1};
	--accent:#{valiable2};
	--warn:#{valiable3};

	--consumed-by-js:$valiable1; // Error. You shall use #{ valiable } phrase.
}

```





### 





