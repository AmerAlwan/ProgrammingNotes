# Routing And URLs

The `route()` decorator in Flask is used to bind a function to a URL

```python
@app.route('/')
def index():
    return 'Index Page'
@app.route('/hello')
def hello():
    return 'Hello World!'
```

## Variable Rules

You can add variable sections to a URL by marking sections with `<variable_name>`. The function then receives the `<variable_name>` as a keyword argument. 

```python
@app.route('/user/<username>')
def show_user_profile(username):
    return 'User', username
```

### Convertor

You can use a convertor to specify the type of argument: `<convertor:variable_name>`

```python
@app.route('/post/<int:post_id>')
def show_post(post_id):
    return 'Post %d' % post_id
```

#### Convertor Types

`string`: (default) accepts any text without slashes

`int`: accepts *positive* integers

`float`: accepts *positive* floating point values

`path`: like `string` but also accepts slashes (like a sub path)

```python
@app.route('/path/<path:subpath>')
def show_subpath(subpath):
    return 'Subpath ' , subpath
```

`uuid`: accepts UUID strings

## Unique URLs / Redirection Behavior

### Trailing Slash

```python
@app.route('/projects/')
def projects():
    return 'The Project Page'
```

The above canonical URL has a trailing slash. If you access the URL without a trailing slash, Flask redirects you to the URL with the trailing slash

### No Trailing Slash

```python
@app.route('/projects')
def projects():
    return 'The Project Page'
```

The above URL does not have a trailing slash. Accessing the URL with a trailing slash will produce a `404 Not Found` error.

## URL Building

To build a URL to a specific function, the `url_for()` function is used. It takes the name of the function as the first argument and the rest of arguments correspond to a variable part of the URL rule. Unknown variable parts are appended to the URL as query parameters

### Why URL Building?

Why use URL Building using the URL reversing function `url_for()` instead of hard-coding them into your template

1. Reversing is often more descriptive than hard coding the URLs
2. You can change a URL instantly instead of needing to remember to manually change hard coded URLs
3. URL building handles escaping of special characters and Unicode data transparently
4. The generated paths are always absolute, avoiding unexpected behavior of relative paths in browsers
5. If your application is placed outside the URL root, for example `/myapplication` instead of `/`, then `url_for()` properly handles that

### Example

```python
@app.route('/')
def index():
    pass
@app.route('/login')
def login():
    pass
@app.route('/user/<username>')
def profile(username):
    pass
with app.test_request_context():
    print(url_for('index')) # >> /
    print(url_for('login')) # >> /login
    print(url_for('login', next='/')) # >> /login?next=/
    print(url_for('profile', username='Amer Alwan')) # >> /user/Amer%20Alwan
```

## HTTP Methods

Web applications use different HTTP methods when accessing URLs. By default, a route answers to GET requests. using the `methods` argument of the `route()` decorate allows handling of different HTTP methods

```python
@app.route('/login', methods=['GET','POST'])
def login():
    if request.method == 'POST':
        return do_the_login()
    else:
        return show_the_login_form()
```

## Static Files

![image-20210311042201572](C:\Users\amera\AppData\Roaming\Typora\typora-user-images\image-20210311042201572.png)

