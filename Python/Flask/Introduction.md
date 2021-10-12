# Introduction

Flask is a web development framework for creating web applications in python.

## Basic Application

A minimal Flaks applications looks like:

```python
from flask import Flask
app = Flask(__name__)

#Tells Flask what URL should trigger the function (In this case, nothing)
@app.route('/')
def hello_world():
    return "Hello World!"
@app.route('/name')
def name():
    return "Amer Alwan"
```

When run, this looks like:

![image-20210311031317283](C:\Users\amera\AppData\Roaming\Typora\typora-user-images\image-20210311031317283.png)

## Running App

In a terminal, type `set FLASK_APP=C:\ .. \AppName.py`. 

Then, type the command `flask run` to start the app. To view the website, go to the URL: http://127.0.0.1:5000/

### Making the website public

The website is currently only accessible on the machine it is run on. To make it accessible on all devices in the network, type `flask run --host=0.0.0.0`, which tells the operating system to listen on all public IPs

### Debug Mode

As of now, any changes made to the code only updates after the website is restarted manually. If debug mode is enable, the server will reload itself when changes to code are made.

 To enable the debugger:

`set FLASK_ENV=development`
`flask run`

## Test Request Context

The `test_request_context()` method of tells Flask to behave as though it's handling a request even while the Python shell is used

```python
@app.route('/index')
def index():
    return 'Index'
with app.test_request_context():
    print(url_for('index')) # >> /index
```

