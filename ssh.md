###Configuracion de SSH

## Debian/Fedora
-Añadir esta linea en `/etc/ssh/ssh_config`
```
ProxyCommand connect-proxy -H usuario_unal@proxyapp.unal.edu.co:8080 %h %p
```
_________________________
##Arch/Mac y en general cualquier Unix based que no le funcione la anterior forma

*Instalar corkscrew
*Crear un archivo plano (authfile) el cual contenga unicamente:
` usuario_unal:password_unal `
-Poner la siguiente linea en `/etc/ssh/ssh_config`
```
ProxyCommand corkscrew proxyapp.unal.edu.co 8080 %h %p /path/to/authfile
```
_________________________

Y para conectarse via SSH y que no se le cierre la conexion (se cierra porque -H es proxy http y sin un `keepalive` se cierra)
`ssh -o ServerAliveInterval=30 myuser@mydns`

Nota: en caso que arreglen proxysocks (que lo dudo porque la DNIC no sirve para nada) quedaría así:
```
ProxyCommand connect-proxy -S usuario_unal@proxysocks.unal.edu.co:1080 %h %p
```
Con proxysocks no sería necesario el keepalive.


Contribucion gracias a Miguel Diaz.
