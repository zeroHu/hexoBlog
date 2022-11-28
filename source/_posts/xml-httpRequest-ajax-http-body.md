---
title: ajax-http-body
date: 2018-02-08 16:35:29
tags: XMLHttpRequest
keywords: http请求， x-www-form-urlencoded， form-data，application/json
---
### 常见的post提交数据格式 <br>form-data,x-www-form-urlencoded,application/json,text/xml

> 其中个人觉得在工作中用得多的是 from-data, x-www-form-urlencoded

#### http
> http请求分为3个部分：状态行，请求头，消息主题

```
<method> <request-URL> <version>
<headers>
<entity-body>
```
服务器端解析是根据请求中的headers 中的 Content-Type 字段来获知请求中的消息主体是用何种方式编码，再对主题进行解析。
**postman 中的 raw 和 binary解释**:
binary:相当于Content-Type:application/octet-stream,从字面意思得知，只可以上传二进制数据，通常用来上传文件，由于没有键值，所以，一次只能上传一个文件。
raw:可以上传任意格式的文本，可以上传text、json、xml、html等

#### application/x-www-form-urlencoded
> 这是最常见的post 提交数据的方式，浏览器的原生form 表单 在不设置 `enctype`的情况下就是使用 `application/x-wwww-form-urlencoded`方式提交数据.

```
POST http://www.example.com http/1.1
Content-Type: application/x-www-form-urlencoded;charset=utf-8

key1=val1&key2=val2&key3=val3
```
**默认的jQuery 中的AJAX 默认值就是「application/x-www-form-urlencoded;charset=utf-8」**

#### multipart/form-data
> 也是一种常见的post提交方式，form表单如果要以这种方式提交需要添加`enctype=multipart/form-data`

```
POST http://www.example.com http/1.1
------WebKitFormBoundaryIuMF45zoLrsAIvdj
Content-Disposition: form-data; name="types"

resume
------WebKitFormBoundaryIuMF45zoLrsAIvdj
Content-Disposition: form-data; name="file"; filename="test.pdf"
Content-Type: application/pdf


------WebKitFormBoundaryIuMF45zoLrsAIvdj--
```
**解析**:首先生成一个`boundary`用于分割不同的字段，为了避免与正文重复，boundary 很长很复杂，然后`Content-Type`里指明数据是`multipart/form-data` 来编码，每部分是以`--boundary`开始,紧接着是内容描述信息，然后是回车，最后是字段具体的内容（文本或二进制）。如果传输的是文件，还要包含文件名和文件类型信息。消息主体最后以`--boundary--`结尾**这种方式一般用于上传文件**，各大服务器都对这个有良好的支持

#### application/json
> 这个Content-Type作为响应头大家肯定都很熟悉了，实际上很多人也把这个作为请求头，告诉服务器消息主体是`序列化后的JSON字符串`

```
POST http://www.example.com http/1.1
Content-Type: application/json; charset=utf-8
{"title": "test", "sub": [1, 2, 3]}
```

#### text/xml
> 比较古老的一种请求方式了，但是支持度还是蛮高的

```
POST http://www.example.com HTTP/1.1
Content-Type: text/xml
<?xml version="1.0"?>

<methodCall>
    <methodName>examples.getStateName</methodName>
    <params>
        <param>
            <value><i4>41</i4></value>
        </param>
    </params>
</methodCall>
```
#### 地址
> [原文链接](https://imququ.com/post/four-ways-to-post-data-in-http.html)