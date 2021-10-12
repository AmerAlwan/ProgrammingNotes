# POSTing and Receiving Files

To better understand this exercise, lets make a URL at `/receive_requests` 

## Receive Requests URL

### `receive_requests.h` File

![image-20210616125804568](C:\Users\amera\AppData\Roaming\Typora\typora-user-images\image-20210616125804568.png)

### `receive_requests.tmpl` file

![image-20210616125953453](C:\Users\amera\AppData\Roaming\Typora\typora-user-images\image-20210616125953453.png)

### Dispatcher and Mapper

![image-20210616130031596](C:\Users\amera\AppData\Roaming\Typora\typora-user-images\image-20210616130031596.png)

`main.cpp` - `rq` function

```cpp
#include <cppcms/http_request.h>
...
void rq () {
          RQ::rq r;
          if (request ().request_method () == "POST") {
          std::vector < booster::shared_ptr < cppcms::http::file > > files = request ().files ();
          for (int i = 0; i < files.size (); i++) {
              booster::shared_ptr < cppcms::http::file > file_tmp = files[i];
              std::string file_name = file_tmp->filename ();
              file_tmp->save_to ("./uploads/" + file_name);
		}  
              // Optional: Return some response
              response().out() << "Successfully Uploaded Files";
	}
}
```

### Request

CPPCMS mainly uses the `request()` function to do operations on any received requests. 

You can view what commands `request()` has here: http://cppcms.com/cppcms_ref/latest/classcppcms_1_1http_1_1request.html

## Config

To configure request and file limits, add the following to `config.js`

**NOTE: ** Sizes are in KB

![image-20210616132149206](C:\Users\amera\AppData\Roaming\Typora\typora-user-images\image-20210616132149206.png)

To view other config settings, go to http://cppcms.com/wikipp/en/page/cppcms_1x_config

## POSTing Request

On the client machine, cd to the location of the file and run the following curl command:

```bash
curl -i -X POST -H "Content-Type: multipart/form-data" -F "data=@file_name" http://192.168.0.120:8080/receive_requests
```

#### POSTing Multiple Files

```bash
curl -i -X POST -H "Content-Type: multipart/form-data" -F "data=@file_0" -F "data=@File_1" -F "data=@file_2" http://192.168.0.120:8080/receive_requests
```



