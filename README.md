# apache-httpd

[Apache HTTP Server](https://httpd.apache.org/)

## Ref.

[맥에서 아파치 웹서버 실행하기](https://xho95.github.io/macos/apache/webserver/mod_wsgi/2016/10/02/Apache-WebServer.html)

## Download

[Download](https://httpd.apache.org/download.cgi)

## macOS

```bash
apachectl -v

Server version: Apache/2.4.34 (Unix)
Server built:   Aug 17 2018 18:35:43
```

```bash
ls /Library/WebServer/Documents

PoweredByMacOSX.gif		index.html.en
PoweredByMacOSXLarge.gif	index.html.en~orig
```

```bash
sudo apachectl start
```

[`localhost`](http://localhost)

`It works!`

## configuration

```bash
cd /private/etc/apache2
ls -al

total 176
drwxr-xr-x   11 root  wheel    352  9 27 20:59 .
drwxr-xr-x  119 root  wheel   3808 12 14 07:02 ..
drwxr-xr-x   25 root  wheel    800  9 27 20:59 extra
-rw-r--r--    1 root  wheel  21150  9 27 20:47 httpd.conf
-rw-r--r--    1 root  wheel  21084  7 16  2017 httpd.conf.pre-update
-rw-r--r--    1 root  wheel  21084 10 26  2017 httpd.conf~previous
-rw-r--r--    1 root  wheel  13077  8 18 08:32 magic
-rw-r--r--    1 root  wheel  61118  8 18 08:32 mime.types
drwxr-xr-x    4 root  wheel    128  8 18 08:32 original
drwxr-xr-x    3 root  wheel     96  8 18 08:32 other
drwxr-xr-x    3 root  wheel     96  9 27 20:54 users
```

`httpd.conf` 수정

```conf
LoadModule userdir_module libexec/apache2/mod_userdir.so

...

DocumentRoot "/Library/WebServer/Documents"
<Directory "/Library/WebServer/Documents">

...

# User home directories
Include /private/etc/apache2/extra/httpd-userdir.conf
```

`extra/httpd-userdir.conf` 수정

```bash
sudo vi /private/etc/apache2/extra/httpd-userdir.conf

Include /private/etc/apache2/users/*.conf
```

***UserDir 다음에 오는 디렉터리 위치를 username의 하위 주소를 써야 한다. (예: username/path/to/Sites UserDir path/to/Sites)***

`users/username.conf` 생성

```conf
<Directory "/Users/username/Sites/">
  Options Indexes MultiViews
  AllowOverride None
  Require all granted
</Directory>
```

***Directory 경로를 한 번 더 확인한다***

```bash
cd ~
mkdir Sites
```

## Run

```bash
sudo apachectl restart
```

`http://localhost/~username`
