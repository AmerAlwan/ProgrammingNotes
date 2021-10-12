# General

## Project Setup and Structure

Download and extract in main project folder: https://sourceforge.net/projects/cppcms/files/

```bash
tar -xjf cppcms-1.0.4.tar.bz2  
```

Run the following commands inside main project folder:

```bash
mkdir build
cd build
cmake ..
make
make test
make install
```

Make `data` and `templates` folders and `main.cpp` and `config.js` files in main folder

```bash
mkdir data
mkdir tempaltes
vi main.cpp
vi config.js
```

Result Main Folder:

![image-20210611111758359](C:\Users\amera\AppData\Roaming\Typora\typora-user-images\image-20210611111758359.png)

Result Build Folder:

![image-20210611111855441](C:\Users\amera\AppData\Roaming\Typora\typora-user-images\image-20210611111855441.png)

### `config.js` File

![image-20210611112214529](C:\Users\amera\AppData\Roaming\Typora\typora-user-images\image-20210611112214529.png)

### Make Main Header File

```bash
cd data
vi master.h
```

#### `master.h` File

![image-20210627091610751](C:\Users\amera\AppData\Roaming\Typora\typora-user-images\image-20210627091610751.png)

### Make Main Template File

```bash
cd template
vi master.tmpl
```

#### `master.tmpl` File

```cpp
<% c++ #include "../data/master.h" %>
<% skin my_skin %>
<% view master uses Master::master %>
<% template title() %> <%= title %> <%end%>
<% template description() %> <%= description %> <%end%>
<% template page_content() %>PAGE CONTENT<% end %>
<% template render() %>
<html>
    <head>
        <meta charset="utf-8" />
        <title><% include title() %></title>
        <meta name="description" content="<% include description() %>" />
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">
    </head>
    <body>
      <div id="HEADER_CONTENT" style="background-color: #181a1b">
	  </div>
      <div id="PAGE_CONTENT" style="background-color: #181a1b">
        <% include page_content() %>
      </div>
    </body>
</html>
<% end template %>
<% end view %>
<% end skin %>
```

### Make Main CPP File

#### `main.cpp` File

```cpp
#include <cppcms/application.h>
#include <cppcms/applications_pool.h>
#include <cppcms/service.h>
#include <cppcms/http_response.h>
#include <cppcms/url_dispatcher.h>
#include <cppcms/url_mapper.h>
#include <iostream>
#include "data/master.h"

class Main : public cppcms::application {
public:
     Main(cppcms::service  &srv) : cppcms::application(srv) {}
     virtual void main(std::string url) {}
}

int main(int argc, char ** argv) {
    try {
        cppcms::service srv(argc, argv);
        srv.applications_pool().mount(cppcms::applications_factory<Main>());
        srv.run();
    } catch (std::exception const &e) {
        std::cerr << e.what() << std::endl;
    }
}

```

## Building

### Building Templates

Templates must always be built before compiling and running the project. 

> **IMPORTANT NOTE**: If multiple templates which inherit from the master template are being built, the master template MUST be put FIRST in the building command

```bash
cd templates
cppcms_tmpl_cc master.tmpl [other templates after] -o my_skin.cpp  
```

## Compiling

The C++ must be compiled with the `my_skin.cpp` file created when building the templates.

In addition, make sure to export the `LD_LIBRARY_PATH` before compiling

Run the following commands in the main project folder:

```bash
export LD_LIBRARY_PATH=/usr/local/lib/
g++ main.cpp templates/my_skin.cpp -o main -lcppcms -lbooster  
```

### With Chrono

To measure time, use this compile command so chrono would work

```bash
export LD_LIBRARY_PATH=/usr/local/lib/
g++ main.cpp templates/my_skin.cpp -o main -std=c++0x -lcppcms -lbooster 
```

## Starting Website

Run the following command in the main project folder:

```bash
./main -c config.js
```

## Curl

### Single File

```bash
curl -i -X POST -H "Content-Type: multipart/form-data" -F "data=@file_0" http://192.168.0.120:8080/receive_requests
```

### Multiple Files

```bash
curl -i -X POST -H "Content-Type: multipart/form-data" -F "data=@file_0" -F "data=@file_1" http://192.168.0.120:8080/receive_requests
```

## Create File

```bash
truncate -s 5M ostechnix.txt
```

## View Uploaded Files with size in MB

```bash
ls uploads/ -l --block-size=M
```

## Debugging

### `config.js`

Add the following to the config file to activate debugging

![image-20210618093301519](C:\Users\amera\AppData\Roaming\Typora\typora-user-images\image-20210618093301519.png)

### `main.cpp`

The equivalent of `cout` in CPPCMS is:

```cpp
BOOSTER_DEBUG("app_name") << "message";
```

