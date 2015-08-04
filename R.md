###Configuracion en R
En la carpeta /home/user , cree un archivo .Renviron
coloque lo siguiente en el archivo

```
http_proxy=$http_proxy
https_proxy=$https_proxy
```

Asegurese de iniciar R despues de haber asignado estas variables.


Tambien se puede utilizar el paquete httr

```
library(httr)
set_config(use_proxy(url="proxyapp.unal.edu.co", port=8080, username="user", password="pass"))
```
