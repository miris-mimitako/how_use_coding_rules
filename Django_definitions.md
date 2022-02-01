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


