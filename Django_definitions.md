# For Django user

## Variables on HTML

{{ Variable name }} <!-- Variable name is defined in Django -->

### How to use

In views.py
```Python

def view_function(request):
    template_name = "sample.html"
    sample_text = "hello mimitako"
    context = {"text": sample_text} # text is variable in HTML
    return render(request, template_name, context)

```

In sample.html
```html
~~~
<body>
    <p>{{ text }}</p> <!-- same views.py variable name. then replacement "hello mimitako"-->
</body>
~~~
```

## Template tag(if phrase)
### How to use

In sample.html
```html
~~~
<body>
    {% if formula %} <!--  -->
        <>out put</> <!-- perform this process when formula is True -->
    {% elif formula2 %}
        <>out put2</> <!-- perform this process when formula2 is True -->
    {% else %}
        <>out put3</> <!-- perform this process when formula and formula2 are False -->
    {% endif %} <!-- This sentence must be used in HTML -->
</body>
~~~
```

## Template tag(for phrase)
### How to use

```html
~~~
<body>
    {% for valiable in iterable_object %} <!--  -->
       <>process</>
    {% endfor %} <!-- This sentence must be used in HTML -->
</body>
~~~
```

## Template tag(block phrase)
block frase replaces from child html file etc.
Mainly use base.html and etc. that are template html.

### How to use


```html
~~~
<head>
    <title>{% block title_name}Main title{% endblock %}</title>
</head>
<body>
    {% block content %} <!--  -->
       <p>Main content</p>
    {% endblock %} <!-- This sentence must be used in HTML -->
</body>
~~~
```

## Template tag(include)
Insert same item on HTML.
Icons, js, css etc.

### How to use

```html
<!-- part.html -->
<script src = "xxx.js"></script>

```
Defined base item.


```html
~~~
<head>
    ~~~
    {{% include "part.html" %}}
</head>
<body>
    {% block content %} <!--  -->
       <p>Main content</p>
    {% endblock %} <!-- This sentence must be used in HTML -->
</body>
~~~
```


## Template Tag(extends)
html frame uses extends tag.
It is easy to use and build html file.

```html
{% extends "base.html" %}


```
Extends code imports from "base.html".
Extends can call multiply times unless same name calling.
Extends can use inheritance. 

