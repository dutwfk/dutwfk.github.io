---
layout: post                                  
title: RESTful Authentication with Flask
category: 技术                                  
tags: [python,Flask]                                   
---


> [RESTful Authentication with Flask](http://blog.miguelgrinberg.com/post/restful-authentication-with-flask)  
> [中文翻译](http://www.cnblogs.com/vovlie/p/4182814.html)

* 注册

```
curl -i -X POST -H "Content-Type: application/json" -d '{"username":"ok","password":"python"}' http://127.0.0.1:5000/api/users
```

* 结果：

```
HTTP/1.0 201 CREATED
Content-Type: application/json
Content-Length: 22
Location: http://127.0.0.1:5000/api/users/1
Server: Werkzeug/0.10.1 Python/2.7.6
Date: Mon, 16 Mar 2015 07:55:07 GMT

{
  "username": "ok"
}
```

* 登陆取token

```
curl -u ok:python -i -X GET http://127.0.0.1:5000/api/token
```

* 结果：

```
HTTP/1.0 200 OK
Content-Type: application/json
Content-Length: 159
Server: Werkzeug/0.10.1 Python/2.7.6
Date: Mon, 16 Mar 2015 07:55:11 GMT

{
  "duration": 600,
  "token": "eyJhbGciOiJIUzI1NiIsImV4cCI6MTQyNjQ5MzExMSwiaWF0IjoxNDI2NDkyNTExfQ.eyJpZCI6MX0.yFnJwDhX49ZjOA6XORnmxuqooEL7mmRIJoU1qM_NQbE"
}
```

* 访问

```
curl -u eyJhbGciOiJIUzI1NiIsImV4cCI6MTQyNjQ5MzExMSwiaWF0IjoxNDI2NDkyNTExfQ.eyJpZCI6MX0.yFnJwDhX49ZjOA6XORnmxuqooEL7mmRIJoU1qM_NQbE:unused -i -X GET http://127.0.0.1:5000/api/resource
```

* 结果：

```
HTTP/1.0 200 OK
Content-Type: application/json
Content-Length: 26
Server: Werkzeug/0.10.1 Python/2.7.6
Date: Mon, 16 Mar 2015 07:56:41 GMT

{
  "data": "Hello, ok!"
}
```