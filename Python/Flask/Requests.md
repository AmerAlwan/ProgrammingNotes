# Requests

```python
from flask import request
```

### Identifying Request Type

To identify the request type, use the `method` variable from `request`

```python
request.method
```

## Accessing Form Data

To access form data transmitted from a `POST` or `PUT` request, the `form` attribute is used

```python
@app.route('/login', methods=['POST', 'GET'])
def login():
    if request.method == 'POST':
        if valid_login(request.form['username'], request.form['password']):
            pass
        else:
            return "Invalid UserName/Password"
	else:
        return render_template('login.html')
```

If the key in the `form` does not exist, they a `KeyError` is raised.

### Accessing from URL Parameters

To access parameters submitted in the URL (`?key=value`), you can use the `args` attribute:

```python
searchword = request.args.get('key', '')
```





