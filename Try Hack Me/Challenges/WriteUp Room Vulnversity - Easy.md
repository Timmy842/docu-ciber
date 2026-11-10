Lo primero, nos conectamos a la **VPN** de **TryHackMe**, y comprobamos que tengamos conexión con la maquina.

![](Pasted%20image%2020260225192143.png)

## Reconocimiento

Ahora, tocaria hacer una fase de reconocimiento, para ello usaremos **Nmap**. Usamos `-sS` para hacer el escaneo mas silencioso, ya que lanzamos un reset como tercer paquete, y `-sCV` para listar y sacar informacion mas detallada de los servicios y posible vulnerabilidades.

![](Pasted%20image%2020260225193117.png)

Tras el escaneo, obserbamos que tiene el servicio de **Samba** abierto, un **Squid proxy**, y una web alojada en el puerto **3333**, vamos a visitarla.

![](Pasted%20image%2020260225194118.png)

## Enumeración Web

Esta es la web que es se muestra, antes de nada, probariamos a observar que directorios tiene publicos y ver si alguno nos llama la atencion, para ello usaremos **Gobuster**, para asi poder enumerar los directorios de la web.

![](Pasted%20image%2020260225195423.png)

Con el siguiente comando ponemos la opcion de `dir` para enumerar directorios, la url que queremos enumerar, y la lista de directorios, al lanzarlo, podemos observar un directorio que nos llama la curiosidad, `/internal`, vamos a ver que podemos encontrar.

![](Pasted%20image%2020260225195622.png)

## Explotación

Vemos un formulario en el que podemos subir ficheros al servidor, por lo que es interesante. 
A continuacion, probamos a subir archivos con extensiones como `.txt` o `.php` pero vemos que nos dice que la operacion no esta permitida:

![](Pasted%20image%2020260225201017.png)

Vamos a usar **Burpsuite** y vamos a usar el **Intruder**. Para empezar, vamos a usar una wordlist con las siguientes extensiones:

![](Pasted%20image%2020260225200004.png)

Vale,  una vez interceptemos la peticion con **Burpsuite**, podemos mandarla al **Intruder** para usar la lista con las siguientes extensiones:

![](Pasted%20image%2020260225203217.png)

Para realizar el ataque, le damos a *Start Attack* y podemos observar que se nos abre una ventana con las peticiones:

![](Pasted%20image%2020260225203314.png)

Aqui observamos un detalle importante, las respuestas de todas las extension son o 774 o 773 de Length menos una que es notablemente menor: `.phtml` que tiene 759, y si vemos la response, vemso que pone el mensaje de Success:

![](Pasted%20image%2020260225203439.png)

Vale, ya tenemos la extension que necesitamos saber para pasarle un archivo al servidor, ahora, vamos a crear una revershell en PHP para tener una linea de comandos.

![](Pasted%20image%2020260225230500.png)

Nos creamos este archivo `reverse.phtml`, con este one-line, para poder ganar una revershell. Ahora, guardamos este archivo que nos dara una bash en la ip de nuestra maquina atacante en el puerto que queramos, y subimos el archivo a la web.

![](Pasted%20image%2020260225230707.png)

Ahora, por lo general estos archivos se guardan en la carpeta `/uploads` dentro del servidor, si no fuera el caso, tendriamos que enumerar para ver donde se ubican. En esta maquina si es el caso:

![](Pasted%20image%2020260225231004.png)

Como se puede observar, aqui estan los archivos que hemos subido. Ahora vamos a ponernos en escucha por el puerto **6666** que es el que hemos determinado en la revershell:

![](Pasted%20image%2020260225231142.png)

## Acceso Inicial

Para entrar dentro de la maquina, por asi decirlo, en la url, ponemos `reverse.phtml` y ya debera darnos acceso:

![](Pasted%20image%2020260225231401.png)

Y como podeis observar, ya estamos dentro de el servidor, ahora para saber quien es el que administra el servidor, simplemente haciendo este comando ya nos devuelve los usuarios con una bash:

![](Pasted%20image%2020260225231756.png)

Podemos observar que el usuario es **bill**, ahora, para encontrar la flag tenemos que irnos a la raiz, `cd /` ir a la home y a la carpeta bill, y hacer un `cat user.txt`

![](Pasted%20image%2020260225232053.png)

## Escalada de Privilegios

Ahora, para escalar privilegios, vamos a aprovecharnos de ficheros con permisos **SUID**, para listarlos usaremos el sigueinte comando: 

![](Pasted%20image%2020260225233713.png)

![](Pasted%20image%2020260225233851.png)

De todos estos, el que nos interesa y nos llama la atencion es `/bin/systemctl`. Nos vamos a `/tmp` y cremamos el archivo `root.service` con lo siguiente:

![](Pasted%20image%2020260225235503.png)

Ahora habilitamos el servicio, nos ponemos en escucha por el puerto **9999** y ejecutamos el servicio para acceder a la maquina;

![](Pasted%20image%2020260225235818.png)

![](Pasted%20image%2020260226000001.png)

Ahora ya, nos metemos en la carpeta `/root` y hacemos un `cat` de `root.txt` para encontrar la flag:

![](Pasted%20image%2020260226000103.png)

## Conclusión

Despues de todos estos pasos, podemos dar por completada la room de Vulnversity. Muchas gracias y hasta la proxima maquina!!
