



# Tornado



## Database



install python MongoDB in ubuntu https://docs.mongodb.com/manual/tutorial/install-mongodb-enterprise-on-ubuntu/



Start templeate,

```shell
wangzhui@WorkStation:/data/Introduction-to-Tornado/databases/bookstore$ python burts_books_rwdb_single.py 
[I 190902 14:24:55 web:2162] 304 GET /recommended/ (192.168.10.117) 7.74ms
[I 190902 14:24:55 web:2162] 200 GET /static/css/style.css?v=4d8518eee282f88f1f37f52f0b1da8c3 (192.168.10.117) 9.65ms
[I 190902 14:24:55 web:2162] 200 GET /static/js/recommended.js?v=4680706fcd8ff59d99f5cc31e7773e5b (192.168.10.117) 1.85ms

```



[![n0g3xs.png](https://s2.ax1x.com/2019/09/12/n0g3xs.png)](https://imgchr.com/i/n0g3xs)
[![n0gGMn.png](https://s2.ax1x.com/2019/09/12/n0gGMn.png)](https://imgchr.com/i/n0gGMn)



```
wangzhui@WorkStation:mongodb
> db.books.find()
{ "_id" : ObjectId("5d6c7e5529ad41c4df9cb0e8"), "date_released" : "2019-03-04", "subtitle" : "read for", "description" : "For more information about our selection, hours or events, please email us aFor more information about our selection, hours or events, please email us aFor more information about our selection, hours or events, please email us aFor more information about our selection, hours or events, please email us aFor more information about our selection, hours or events, please email us aFor more information about our selection, hours or events, please email us aFor more information about our selection, hours or events, please email us aFor more information about our selection, hours or events, please email us aFor more information about our selection, hours or events, please email us a", "title" : "1", "image" : "", "author" : "had", "isbn" : "1", "date_added" : 1567391317 }
{ "_id" : ObjectId("5d6c7e7029ad41c4df9cb0e9"), "subtitle" : "read for", "description" : "For more information about our selection, hours or events, please email us a", "author" : "had", "image" : "", "title" : "1", "date_added" : 1567391344, "isbn" : "1", "date_released" : "2019-03-04" }
{ "_id" : ObjectId("5d6c7e7629ad41c4df9cb0ea"), "subtitle" : "read for", "description" : "For more information about our selection, hours or events, please email us a", "author" : "had", "image" : "", "title" : "1", "date_added" : 1567391350, "isbn" : "hdskagtuq", "date_released" : "2019-03-04" }
{ "_id" : ObjectId("5d6cbaa2c6feecdbfb84c20e"), "subtitle" : "read for", "description" : "For more information about our selection, hours or eve", "author" : "had", "image" : "", "title" : "Tronado blog test this is tornado blog for test", "date_added" : 1567406754, "isbn" : "Rstful", "date_released" : "2019-03-04" }


```



## mongDB

```
wangzhui@WorkStation:/data/Introduction-to-Tornado/databases/bookstore$ python2.7 
Python 2.7.12 (default, Nov 12 2018, 14:36:49) 
[GCC 5.4.0 20160609] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import pymongo
>>> conn = pymongo.MongoClient('localhost', 27017)
>>> pymongo.version
'3.8.0'
>>> db=conn.bookstore
>>> db.collection_names()
[u'books']
>>> 
>>> widgets = db.widgets
>>> db.collection_names()
[u'books']
>>> widgets.insert({"foo":"bar"})
ObjectId('5d6cc4a8e94a640de43897d8')
>>> db.collection_names()
[u'widgets', u'books']
>>> 
>>> widgets.insert({"name": "flibnip", "description": "grade-A industrial flibnip", "quantity": 3})
ObjectId('5d6cc4c3e94a640de43897d9')
>>> widgets.find_one({"name":"flibnip"})
{u'description': u'grade-A industrial flibnip', u'_id': ObjectId('5d6cc4c3e94a640de43897d9'), u'name': u'flibnip', u'quantity': 3}
>>> 
>>> widgets.find_one({"foo":"bar"})
{u'_id': ObjectId('5d6cc4a8e94a640de43897d8'), u'foo': u'bar'}

>>> doc = db.widgets.find_one({"name":"flibnip"})
>>> print(doc)
{u'description': u'grade-A industrial flibnip', u'_id': ObjectId('5d6cc4c3e94a640de43897d9'), u'name': u'flibnip', u'quantity': 3}
>>> type(doc)
<type 'dict'>
>>> print doc['name']
flibnip
>>> doc['quantity'] = 4
>>> db.widget.save(doc)
ObjectId('5d6cc4c3e94a640de43897d9')
>>> doc = db.widgets.find_one({"name":"flibnip"})
>>> db.widgets.find_one({"name":"flibnip"})
{u'description': u'grade-A industrial flibnip', u'_id': ObjectId('5d6cc4c3e94a640de43897d9'), u'name': u'flibnip', u'quantity': 3}
>>> 

--- in mongdb shell
> db.widgets.find()
{ "_id" : ObjectId("5d6cc4a8e94a640de43897d8"), "foo" : "bar" }
{ "_id" : ObjectId("5d6cc4c3e94a640de43897d9"), "quantity" : 3, "name" : "flibnip", "description" : "grade-A industrial flibnip" }
---
```

