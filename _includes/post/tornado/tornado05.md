

# Tornado



## 异步的web请求

**阻塞性质的web请求**也就是说当一个请求被处理时，这个进程就会被挂起直至请求完成。再请求足够快，没有任何问题，但是当web需要时间去操作（外部API，大数据库），**这意味着应用程序被有效的锁定直至处理结束**

Tornado给了我们更好的方法来处理这种情况。**应用程序在等待第一个处理完成的过程中，让I/O循环打开以便服务于其他客户端**，**直到处理完成时启动一个请求并给予反馈**，而不再是等待请求完成的过程中挂起进程。



### 从同步开始



```python
client = tornado.httpclient.HTTPClient()
response = client.fetch("http://search.twitter.com/search.json?" + \
        urllib.urlencode({"q": query, "result_type": "recent", "rpp": 100}))
body = json.loads(response.body)
```

这里我们实例化了一个Tornado的HTTPClient类，然后调用结果对象的fetch方法。fetch方法的同步版本使用要获取的URL作为参数。这里，我们构建一个URL来抓取Twitter搜索API的相关搜索结果（rpp参数指定我们想获得搜索结果首页的100个推文，而result_type参数指定我们只想获得匹配搜索的最近推文）。fetch方法会返回一个HTTPResponse对象，其 body属性包含我们从远端URL获取的任何数据。Twitter将返回一个JSON格式的结果，所以我们可以使用Python的json模块来从结果中创建一个Python数据结构。

fetch方法返回的HTTPResponse对象允许你访问HTTP响应的任何部分，不只是body。可以在[官方文档](http://www.tornadoweb.org/en/stable/httpclient.html)[1]阅读更多相关信息。

处理函数的其余部分关注的是计算每秒推文数。我们使用搜索结果中最旧推文与最新推文时间戳之差来确定搜索覆盖的时间，然后使用这个数值除以搜索取得的推文数来获得我们的最终结果。最后，我们编写了一个拥有这个结果的简单HTML页面给浏览器。

```shell
siege http://localhost:8000/?q=pants -c10 -t10s
```

![图5-2](http://demo.pythoner.com/itt2zh/static/images/Figure5-2.jpg)

### 基础的异步调用

```python
client = tornado.httpclient.AsyncHTTPClient()
client.fetch("http://search.twitter.com/search.json?" + »
urllib.urlencode({"q": query, "result_type": "recent", "rpp": 100}),
        callback=self.on_response)
```

![图5-3](http://demo.pythoner.com/itt2zh/static/images/Figure5-3.jpg)



### 异步生成器

```python
client = tornado.httpclient.AsyncHTTPClient()
response = yield tornado.gen.Task(client.fetch,
        "http://search.twitter.com/search.json?" + \
        urllib.urlencode({"q": query, "result_type": "recent", "rpp": 100}))
body = json.loads(response.body)
```



### 异步操作总结
尽管不是所有的处理都能从异步中受益--并且实际上尝试整个程序非阻塞会迅速使事情变得复杂-- **但Tornado的非阻塞功能可以非常方便的创建依赖于缓慢查询或外部服务的Web应用。**





## 使用Tornado进行长轮询

Tornado异步架构的另一个优势是它能够轻松处理HTTP长轮询。**这是一个处理实时更新的方法，它既可以应用到简单的数字标记通知，也可以实现复杂的多用户聊天室**。

部署提供实时更新的Web应用对于Web程序员而言是一项长期的挑战。更新用户状态、发送新消息提醒、或者任何一个需要在初始文档完成加载后由服务器向浏览器发送消息方法的全局活动。一个早期的方法是浏览器以一个固定的时间间隔向服务器轮询新请求。这项技术带来了新的挑战：轮询频率必须足够快以便通知是最新的，但又不能太频繁，当成百上千的客户端持续不断的打开新的连接会使HTTP请求面临严重的扩展性挑战。频繁的轮询使得Web服务器遭受"凌迟"之苦。

所谓的"服务器推送"技术允许**Web应用实时发布更新，同时保持合理的资源使用以及确保可预知的扩展**。对于一个可行的服务器推送技术而言，它必须在现有的浏览器上表现良好。最流行的技术是让浏览器发起连接来模拟服务器推送更新。这种方式的HTTP连接被称为*长轮询*或*Comet请求*。



### 长轮询的好处

HTTP长轮询的主要吸引力在于其极大地减少了Web服务器的负载。相对于客户端制造大量的短而频繁的请求（以及每次处理HTTP头部产生的开销），服务器端只有当其接收一个初始请求和再次发送响应时处理连接。大部分时间没有新的数据，连接也不会消耗任何处理器资源。

长轮询如此流行的一个原因是它改善了应用的用户体验：访客不再需要不断地刷新页面来获取最新的内容。



### 实时库存报告



### 长轮询的缺陷

正如我们所看到的，HTTP长轮询在站点或特定用户状态的高度交互反馈通信中非常有用。但我们也应该知道它的一些缺陷。

当使用长轮询开发应用时，**记住对于浏览器请求超时间隔无法控制是非常重要的**。由浏览器决定在任何中断情况下重新开启HTTP连接。**另一个潜在的问题是许多浏览器限制了对于打开的特定主机的并发请求数量**。当有一个连接保持空闲时，剩下的用来下载网站内容的请求数量就会有限制。

此外，你还应该明白请求是怎样影响服务器性能的。再次考虑购物车应用。由于在库存变化时所有的推送请求*同时*应答和关闭，使得在浏览器重新建立连接时服务器受到了新请求的猛烈冲击。对于像用户间聊天或消息通知这样的应用而言，只有少数用户的连接会同时关闭，这就不再是一个问题了。

