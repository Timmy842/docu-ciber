Vamos a usar https://overthewire.org para aprender tanto comandos de Linux como Bash.
- Bandit 0
Nos conectamos por ssh a bandit0 para sacar la flag del readme: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If

- Bandit 1
Para superarlo, hay que abrir el archivo - que contiene la contraseña, una forma de abrirlo es ```
 ```
 cat ./- cat /home/bandit1/-
 ```
La contraseña es la siguiente: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx

- Bandit2
Para esta, pide que saques la contraseña de --spaces in this filename--, para esto usamos cat "--spaces in this filename--" y listamos la contraseña: MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

- Bandit3
Para esta, nos metemos en el directorio de inhere, y hacemos cat de ...Hidding You, para sacar la contraseña que es: 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

- Bandit4
Para esto, buscamos con el siguiente comando: *find . -type f | grep "\-file" | xargs file*
La contraseña es esta, usando este comando: *find . -type f | grep "\-file" | xargs file | grep ASCII | awk -F: '{print $1}' | xargs cat* para sacar la contraseña: 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw

- Bandit5
Para buscar la contraseña, usaremos el comando sigueiente: *find . -type f ! -executable -size 1033c | xargs cat | xargs* para obtener la contraseña: HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

- Bandit6
Para sacar la contraseña, nos vamos al directorio raiz, ya que es en alguna parte del sistema, y ejecutamos este comando *find . -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null | xargs cat*, con esto, sacamos la contraseña: morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

- Bandit7
Para sacar la contraseña, usamos este comando por ejemplo: *cat data.txt | grep "millionth" | awk 'NF{print $NF}'* para sacar la contraseña que es la siguiente: dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

- Bandit8
Para obtener la contraseña usamos este comando: *sort data.txt | uniq -u* y obtenemos la contraseña: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM

- Bandit9
