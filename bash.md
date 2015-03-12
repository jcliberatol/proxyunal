
##Consola de Linux

En la consola de linux se pueden agregar las siguientes funciones al archivo .bashrc o .zshrc , dependiendo del shell
Estas habilitan el proxy y preguntan por el nombre de usuario y contraseña


Para habilitar el proxy ejecute
```
proxy_on
```

Igualmente para deshabilitarlo 

```
proxy_off
```
Luego de cambiar el .zshrc o el .bashrc hay que ejecutar el script , use :

```
cd
source .bashrc
```

```
function proxy_on() {
    export no_proxy="localhost,127.0.0.1,localaddress,.localdomain.com"

    if (( $# > 0 )); then
        valid=$(echo $@ | sed -n 's/\([0-9]\{1,3\}.\)\{4\}:\([0-9]\+\)/&/p')
        if [[ $valid != $@ ]]; then
            >&2 echo "Invalid address"
            return 1
        fi

        export http_proxy="http://$1/"
        export https_proxy=$http_proxy
        export ftp_proxy=$http_proxy
        export rsync_proxy=$http_proxy
        echo "Proxy environment variable set."
        return 0
    fi

    echo -n "username: "; read username
    if [[ $username != "" ]]; then
        echo -n "password: "
        read -s password
        local pre="$username:$password@"
    fi
    echo $pre
    local server="proxyapp.unal.edu.co"
    local ftp=""
    local port="8080"
    export http_proxy="http://$pre$server:$port/"
    export https_proxy=$http_proxy
    export ftp_proxy=$http_proxy
    export rsync_proxy=$http_proxy
    export HTTP_PROXY=$http_proxy
    export HTTPS_PROXY=$http_proxy
    export FTP_PROXY=$http_proxy
    export RSYNC_PROXY=$http_proxy
}

function proxy_off(){
    unset http_proxy
    unset https_proxy
    unset ftp_proxy
    unset rsync_proxy
    echo -e "Proxy environment variable removed."
}
```


###Notas :
El metodo propuesto fue modificado a partir del de la wiki de arch : https://wiki.archlinux.org/index.php/proxy_settings
