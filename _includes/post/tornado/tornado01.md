

# Tornado



## What is Tornado ?

Tornado是使用Python编写的一个**强大的、可扩展**的Web服务器。它在处理严峻的网络流量时表现得足够强健，但却在创建和编写时有着足够的**轻量级**，

Tornado在设计之初就考虑到了性能因素，旨在解决**C10K问题**，这样的设计使得其成为一个拥有非常高性能的框架

> ​	C10k Problem
>
> ​	基于线程的服务器，如Apache，为了传入的连接，维护了一个操作系统的线程池。Apache会为每个HTTP连接分配线程池中的一个线程，如果所有的线程都处于被占用的状态并且尚有内存可用时，则生成一个新的线程。Apache的架构在大负载下变得不可预测，为每个打开的连接维护一个大的线程池等待数据极易迅速耗光服务器的内存资源。
>
> ​	异步服务器在这一场景中的应用相对较新，但他们正是被设计用来减轻基于线程的服务器的限制的。当负载增加时，诸如Node.js，lighttpd和Tornodo这样的服务器使用协作的多任务的方式进行优雅的扩展。也就是说，如果当前请求正在等待来自其他资源的数据（比如数据库查询或HTTP请求）时，一个异步服务器可以明确地控制以挂起请求。



## Hello Tornado 

```python
import tornado.httpserver
import tornado.ioloop
import tornado.options
import tornado.web

from tornado.options import define, options
define("port", default=8000, help="run on the given port", type=int)

class IndexHandler(tornado.web.RequestHandler):
    def get(self):
        greeting = self.get_argument('greeting', 'Hello')
        self.write(greeting + ', friendly user!')

if __name__ == "__main__":
    tornado.options.parse_command_line()
    app = tornado.web.Application(handlers=[(r"/", IndexHandler)])
    http_server = tornado.httpserver.HTTPServer(app)
    http_server.listen(options.port)
    tornado.ioloop.IOLoop.instance().start()
```

```shell
$ python hello.py --port=8000
```

Tornado包括了一个有用的模块（tornado.options）来从命令行中读取设置。我们在这里使用这个模块指定我们的应用监听HTTP请求的端口。它的工作流程如下：如果一个与define语句中同名的设置在命令行中被给出，那么它将成为全局options的一个属性。如果用户运行程序时使用了`--help`选项，程序将打印出所有你定义的选项以及你在define函数的help参数中指定的文本。如果用户没有为这个选项指定值，则使用default的值进行代替。

```shell
Usage: hello.py [OPTIONS]

Options:

  --help                           show this help information

/home/wangzhui/.local/lib/python2.7/site-packages/tornado/log.py options:

  --log-file-max-size              max size of log files before rollover
                                   (default 100000000)
  --log-file-num-backups           number of log files to keep (default 10)
  --log-file-prefix=PATH           Path prefix for log files. Note that if you
                                   are running multiple tornado processes,
                                   log_file_prefix must be different for each
                                   of them (e.g. include the port number)
  --log-rotate-interval            The interval value of timed rotating
                                   (default 1)
  --log-rotate-mode                The mode of rotating files(time or size)
                                   (default size)
  --log-rotate-when                specify the type of TimedRotatingFileHandler
                                   interval other options:('S', 'M', 'H', 'D',
                                   'W0'-'W6') (default midnight)
  --log-to-stderr                  Send log output to stderr (colorized if
                                   possible). By default use stderr if
                                   --log_file_prefix is not set and no other
                                   logging is configured.
  --logging=debug|info|warning|error|none 
                                   Set the Python log level. If 'none', tornado
                                   won't touch the logging configuration.
                                   (default info)

hello.py options:

  --port                           run on the given port (default 8888)
```

```python
class IndexHandler(tornado.web.RequestHandler):
    def get(self):
        greeting = self.get_argument('greeting', 'Hello')
        self.write(greeting + ', friendly user!')
```

`IndexHandler`继承`tornado.web.RequestHandler`,并且将其实例化，该实例只定义了一个get方法

`Tornado`的`RequestHandler`类有一系列有用的内建方法，包括`get_argument`，我们在这里从一个查询字符串中取得参数greeting的值

```http
http://192.168.10.111:8888/?greeting=wuwukai
```
`greeting=wuwukai`

`RequestHandler`的另一个有用的方法是`write`，它以一个字符串作为函数的参数，并将其写入到HTTP响应中。在这里，我们使用请求中greeting参数提供的值插入到greeting中，并写回到响应中

```
wuwukai, friendly user!
```



```python
if __name__ == "__main__":
    tornado.options.parse_command_line()
    app = tornado.web.Application(handlers=[(r"/", IndexHandler)])
```

首先，我们使用Tornado的options模块来解析命令行。然后我们创建了一个Tornado的`Application`类的实例。传递给Application类`__init__`方法的最重要的参数是`handlers` `handlers=[(r"/", IndexHandler)]`。它告诉Tornado应该用哪个类来响应请求

这里的参数handlers非常重要，值得我们更加深入的研究。它应该是一个**元组组成的列表**，其中每个元组的第一个元素是一个用于匹配的**正则表达式**，第二个元素是一个**`RequestHanlder`类**



```python
http_server = tornado.httpserver.HTTPServer(app)
http_server.listen(options.port)
tornado.ioloop.IOLoop.instance().start()
```

从这里开始的代码将会被反复使用：一旦Application对象被创建`app`，我们可以将其传递给Tornado的HTTPServer对象，然后使用我们在命令行指定的端口进行监听（通过options对象取出。`option.port()`）最后，在程序准备好接收HTTP请求后，我们创建一个Tornado的IOLoop的实例`IOLoop.instance().start()`。



## String Service

```python
import textwrap

import tornado.httpserver
import tornado.ioloop
import tornado.options
import tornado.web

from tornado.options import define, options
define("port", default=8000, help="run on the given port", type=int)

class ReverseHandler(tornado.web.RequestHandler):
    def get(self, input):
        self.write(input[::-1])

class WrapHandler(tornado.web.RequestHandler):
    def post(self):
        text = self.get_argument('text')
        width = self.get_argument('width', 40)
        self.write(textwrap.fill(text, int(width)))
        
if __name__ == "__main__":
    tornado.options.parse_command_line()
    app = tornado.web.Application(
        handlers=[
            (r"/reverse/(\w+)", ReverseHandler),
            (r"/wrap", WrapHandler)
        ]
    )
    http_server = tornado.httpserver.HTTPServer(app)
    http_server.listen(options.port)
    tornado.ioloop.IOLoop.instance().start()
```
测试结果
```shell
wangzhui@workstation:~$ curl http://localhost:8000/wrap -d text=Lorem+ipsum+dolor+sit+amet,+consectetuer+adipiscing+elit
Lorem ipsum dolor sit amet, consectetuer
adipiscing elit
```



```
app = tornado.web.Application(handlers=[
    (r"/reverse/(\w+)", ReverseHandler),
    (r"/wrap", WrapHandler)
])
```

在上面的代码中，Application类在"handlers"参数中实例化了两个RequestHandler类对象。第一个引导Tornado传递路径匹配下面的**正则表达式的请求**：

```
/reverse/(\w+)
```

正则表达式告诉Tornado匹配任何以字符串/reverse/开始并紧跟着一个或多个字母的路径。**括号的含义是让Tornado保存匹配括号里面表达式的字符串**，并将其作为**请求方法的一个参数**传递给`RequestHandler`类。让我们检查ReverseHandler的定义来看看它是如何工作的：

```python
class ReverseHandler(tornado.web.RequestHandler):
    def get(self, input):
        self.write(input[::-1])
```



```python
class WrapHandler(tornado.web.RequestHandler):
    def post(self):
        text = self.get_argument('text')
        width = self.get_argument('width', 40)
        self.write(textwrap.fill(text, int(width)))
```

`get_argument('text')`text表示url中的text参数

```shell
wangzhui@workstation:~$ curl http://localhost:8888/wrap -d text=w+dsaj+dskjhe+skajle+sdjak,+fdhaeh+dhsew+fhq+d
w dsaj
dskjhe
skajle
sdjak,
fdhaeh
dhsew fhq
```



## HTTP Methods

但是，在同一个处理函数中定义多个方法是可能的，并且是有用的。把概念相关的功能绑定到同一个类是一个很好的方法。比如，你可能会编写一个处理函数来处理数据库中某个特定ID的对象，既使用GET方法，也使用POST方法。想象GET方法来返回这个部件的信息，而POST方法在数据库中对这个ID的部件进行改变

```python
# matched with (r"/widget/(\d+)", WidgetHandler)
class WidgetHandler(tornado.web.RequestHandler):
    def get(self, widget_id):
        widget = retrieve_from_db(widget_id)
        self.write(widget.serialize())

    def post(self, widget_id):
        widget = retrieve_from_db(widget_id)
        widget['foo'] = self.get_argument('foo')
        save_to_db(widget)
```

to be continue...