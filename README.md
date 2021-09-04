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
