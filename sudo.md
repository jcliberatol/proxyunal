##Con respecto a sudo

Para configurar el proxy bajo linux existen varias posibilidades, la recomendada dado que la configuración debe ser permanente en este caso. Se debe editar el archivo /etc/environment e incluir el siguiente contenido:
```
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games"
http_proxy=http://user:password@proxyapp.unal.edu.co:8080/
https_proxy=http://user:password@proxyapp.unal.edu.co:8080/
ftp_proxy=http://user:password@proxyftp.unal.edu.co:1080/
HTTP_PROXY=http://user:password@proxyapp.unal.edu.co:8080/
HTTPS_PROXY=http://user:password@proxyapp.unal.edu.co:8080/
FTP_PROXY=http://user:password@proxyftp.unal.edu.co:1080/
NO_PROXY="localhost,127.0.0.1,.unal.edu.co,localaddress"
no_proxy=="localhost,127.0.0.1,.unal.edu.co,localaddress"
```
Lamentablemente esas variables de entorno añadidas anteriormente ** no surtirán efecto cuando las invocamos mediante un comando sudo **, porque sudo tiene un política que por defecto resetea el environment, este comportamiento es definido en `/etc/sudoers` y una forma de decirle que no reseteé ciertas variables explícitmane es editándolo de la siguiente forma:
corra el comando `sudo visudo` y añadir la siguiente línea al final del archivo:
```
Defaults env_keep += "http_proxy https_proxy ftp_proxy proxy_socks HTTP_PROXY HTTPS_PROXY"
```

Contribucion gracias a **Juan David Uchuvo**
