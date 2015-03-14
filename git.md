## Git

En git, la configuracion se lleva a cabo de la siguiente manera : 

```
git config --global http.proxy http://user:password@proxyapp.unal.edu.co:8080/proxy.pac
git config --global https.proxy http://user:password@proxyapp.unal.edu.co:8080/proxy.pac
```

Para remover la configuracion


```
git config --global --unset http.proxy
git config --global --unset https.proxy
```
