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



