# with Tomcat

[rurumimic/apache-tomcat](https://github.com/rurumimic/apache-tomcat)
[Fronting Tomcat with Apache via mod_proxy_ajp](https://confluence.sakaiproject.org/display/~steve.swinsburg/Fronting+Tomcat+with+Apache+via+mod_proxy_ajp)

## mod_proxy_ajp

`/private/etc/apache2/httpd.conf`

```conf
LoadModule proxy_module libexec/apache2/mod_proxy.so
LoadModule proxy_ajp_module libexec/apache2/mod_proxy_ajp.so

# Virtual hosts
Include /private/etc/apache2/extra/httpd-vhosts.conf
```

`/private/etc/apache2/extra/httpd-vhosts.conf`

```conf
# Required modules: mod_log_config

<VirtualHost *:80>
  ServerName localhost
  ProxyPass / ajp://localhost:8009/
</VirtualHost>
```
