# USO

**Nota**:
Antes de compilar el código, debes tanto en el archivo proxy_server.c como en final_client.c editar la ip del servidor o máquina donde se esté ejecutando el Servidor Proxy Invertido HTTP (proxy_server.c).

Línea de código donde se debe cambiar la ip donde se encuentra el Servidor Proxy Invertido HTTP (proxy_server.c) en el archivo proxy_server.c:
![image](https://github.com/MateoRamirezRubio1/proxyInversoBalanceadorCarga/assets/100296963/18770262-5219-4420-af7b-d127931c2dcc)

Línea de código donde se debe cambiar la ip donde se encuentra el Servidor Proxy Invertido HTTP (proxy_server.c) en el archivo final_client.c:
![image](https://github.com/MateoRamirezRubio1/proxyInversoBalanceadorCarga/assets/100296963/a44ab87c-2777-4261-a824-697a71746334)


## Compilación y/o ejecución Servidor HTTP Proxy + balanceador de carga
Para compilar el Servidor Proxy Invertido HTTP ubíquese en la carpeta server,
<br>
Ejemplo: ![image](https://github.com/MateoRamirezRubio1/proxyInversoBalanceadorCarga/assets/100296963/d318b681-b604-46bf-8c44-8cc370f13e98)
<br>
y compile el código fuente utilizando GCC con el makefile proporcionado, ejecute los siguientes comandos:

```
gcc -c cache/manejoCache.c -o cache/manejoCache.o

gcc -c proxy_server.c -o proxy_server.o -Icache

gcc -o proxy_server proxy_server.o cache/manejoCache.o -lpthread -lcrypto
```

Para iniciar el Servidor Proxy HTTP, ubíquese en la carpeta server y ejecute el siguiente comando:
<p align="center"><strong>./proxy_server &lt;ttl&gt; &lt;port&gt; logProxyServer.log</strong></p>
•	./proxy_server: es el ejecutable de la aplicación.
<br>
•	Ttl: Tiempo TTL en segundos para los recursos de cache.
<br>
•	port: es el puerto en el cual se escucharán las peticiones por parte de los clientes. Para efectos de este proyecto debe ser el puerto 8080.
<br>
•	logProxyServer.log:  representa la ruta y nombre del archivo que almacena el log.
<br>
<br>
Ejemplo:
<br>
./proxy_server 60 8080 logProxyServer.log


## Compilación y/o ejecución Cliente:
Para compilar el Cliente ubíquese en la carpeta CLIENT,
<br>
Ejemplo: ![image](https://github.com/MateoRamirezRubio1/proxyInversoBalanceadorCarga/assets/100296963/593ceb6d-3943-466e-8202-3f91d6e971b3)
<br>
y compile el código fuente utilizando GCC con el makefile proporcionado, ejecute los siguientes comandos:

```
gcc -c cache/manejoCacheClient.c -o cache/manejoCacheClient.o

gcc -c final_client.c -o final_client.o -Icache

gcc -o final_client final_client.o cache/manejoCacheClient.o -lpthread -lcrypto
```

Para iniciar el cliente, ubíquese en la carpeta CLIENT y ejecute el siguiente comando:
<p align="center"><strong>./final_client logClient.log &lt;url:port&gt;</strong></p>
•	./final_client: es el nombre del archivo ejecutable.
<br>
•	logClient.log: representa la ruta y nombre del archivo que almacena el log.
<br>
•	url:port: URL y puerto donde se localiza el recurso a solicitar.
<br>
<br>
Ejemplo:
<br>
./final_client logClient.log example.com:80/
<br>
<br>
<p><strong>Nota importante:</strong></p>
En la parte de url:port después del port (en el ejemplo :80) siempre se debe ingresar con un / al final si no vas a una página en específico como por ejemplo el home.
