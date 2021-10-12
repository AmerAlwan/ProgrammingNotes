# Templates

Instead of returning just text, the website can be made nicer by returning templates, which are programmed with HTML and CSS

## HTML and Templates in Flask

### Creating and Using a Template

First, an HTML file is created in the **templates** folder of the flask project.

![image-20210311051243239](C:\Users\amera\AppData\Roaming\Typora\typora-user-images\image-20210311051243239.png)

The file will end with `.html`, program then the webpage using HTML code:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h1> Header 1 </h1>
    <p> Paragraph 1 </p>
</body>
</html>
```

Inside the `main.py` file, import `render_template` from `flash`. Then, inside the appropriate route, return the `render_remplate()` method with the HTML file's name in the parameter

```python
from flask import Flask, render_template
# ...
@app.route("/")
def home():
    return render_template("home.html")
```

The Final Result...

![image-20210311051905005](C:\Users\amera\AppData\Roaming\Typora\typora-user-images\image-20210311051905005.png)

### Using Variables

In order to use a variable from the `main.py` file, it has to be passed as a parameter into the `render_template()` function

```python
from flask import render_template
@app.route('/welcome/')
@app.route('/welcome/<name>')
def welcome(name=None):
    return render_template("home.html", name=name)
```

Inside `home.html`, the `name` variable can now be used

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    {% if name %}
        <h1>Welcome {{name}}!</h1>
    {% else %}
        <h1>Welcome!</h1>
    {% endif %}
</body>
</html>
```

### Inheritance

Inheritance can be used with multiple templates to create a common template that is used in all child templates that inherit the parent template. Example of this can include a parent template that has a header/website logo, or hyperlinks to the other pages.

In the parent template, include the HTML code for whatever is to be shared with all child templates, then include the lines `{% block content %}` and `{% end block%}` for where the code of the child templates will go

```html
<!PARENT TEMPLATE>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    {% if name %}
        <h1>Welcome {{name}}!</h1>
    {% else %}
        <h1>Welcome!</h1>
    {% endif %}
    {% block content %}
    {% endblock %}
</body>
</html>
```

Then, in the child templates, include the line `{% extends "parent.html" %}` inside the `<body>`. Then, include the line `{% block content %}` inside the `<body>` followed by the code for that child template. Finally, add `{% endblock %}`.

```html
<!CHILD TEMPLATE>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    {% extends "parent.html" %}
    {% block content %}
    	<p>This is the Child</p>
    {% endblock %}
</body>
</html>
```

In the `main.py` file, the child template can be returned with the `render_template()` function and elements from the parent template will be included

```python
@app.route('/welcome/')
@app.route('/welcome/<name>')
def welcome(name=None):
    return render_template("home.html", name=name)
```

#### Example with http://127.0.0.1:5000/welcome/Amer%20Alwan

![image-20210311061546757](C:\Users\amera\AppData\Roaming\Typora\typora-user-images\image-20210311061546757.png)