# Inheritance

## Create Header File

Create header file for template which will inherit from `master.h`

For this example, create home:

```bash
cd data
vi home.h
```

### `home.h` File

![image-20210611114650534](C:\Users\amera\AppData\Roaming\Typora\typora-user-images\image-20210611114650534.png)

## Create Template File

For this example, create home:

```bash
cd templates
vi home.tmpl
```

### `home.tmpl` File

![image-20210611114832421](C:\Users\amera\AppData\Roaming\Typora\typora-user-images\image-20210611114832421.png)

## Building Templates

> **IMPORTANT NOTE:** When building the templates, REMEMBER to include the parent template FIRST

```bash
cd templates
cppcms_tmpl_cc master.tmpl home.tmpl -o my_skin.cpp  
```

# Routing

To better visualize routing, lets create another template `hello.h` & `hello.tmpl` which will inherit from master.

## Hello

### `hello.h` File

![image-20210611115235025](C:\Users\amera\AppData\Roaming\Typora\typora-user-images\image-20210611115235025.png)

### `hello.tmpl` File

![image-20210611115404425](C:\Users\amera\AppData\Roaming\Typora\typora-user-images\image-20210611115404425.png)

### Build Templates

```bash
cd templates
cppcms_tmpl_cc master.tmpl home.tmpl hello.tmpl -o my_skin.cpp 
```

## Configuring Routes

Inside `main.cpp`, include:

```cpp
#include <cppcms/url_dispatcher.h>
#include <cppcms/url_mapper.h>
#include "data/home.h"
#include "data/hello.h"
```

Apply following changes to `main.cpp`:

```cpp
 class Main : public cppcms::application {
 public:
     Main(cppcms::service  &srv) : cppcms::application(srv) {
         dispatcher().assign("(/?)",&Main::home,this);
         mapper().assign("home", "/");

         dispatcher().assign("/hello",&Main::hello,this);
         mapper().assign("hello","/hello");

     }
     virtual void main(std::string url) {
         cppcms::application::main(url);
     }
     
     void home() {
         Home::home h;
         h.title = "Home";
         h.description = "Home Page";
         render("home",h);
     }

     void hello () {
         Hello::hello h;
         h.title="Hello";
         h.description = "Hello World Page";
         render("hello", h);
     }     
};

```

## Compile

```bash
export LD_LIBRARY_PATH=/usr/local/lib/
g++ main.cpp templates/my_skin.cpp -o main -lcppcms -lbooster
```

## Run

```cpp
./main -c config.js
```

