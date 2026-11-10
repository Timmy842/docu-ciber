Es una herramienta diseñada en python, que se utiliza para enumerar subdominios de webs. Ayuda a los pentesters a recopilar y reunir subdominios para el dominio que están atacando. También enumera subdominios utilizando muchos motores de búsqueda como Google, Yahoo, Bing, Baidu y Ask, e incluso enumera subdominios utilizando Netcraft, Virustotal, ThreatCrowd, DNSdumpster y ReverseDNS.

Para instalarlo, usamamos el comando sudo apt-get install sublist3r, ya que forma parte del repositorio de Kali. Una vez instalado, ejecutamos este comando para descargar los requerimientos: sudo pip install -r requirements.txt

Para su uso, tenemos estas opciones que nos explican para que sirve cada una y como usarlas:

-d 	--domain 	Domain name to enumerate subdomains of
-b 	--bruteforce 	Enable the subbrute bruteforce module
-p 	--ports 	Scan the found subdomains against specific tcp ports
-v 	--verbose 	Enable the verbose mode and display results in realtime
-t 	--threads 	Number of threads to use for subbrute bruteforce
-e 	--engines 	Specify a comma-separated list of search engines
-o 	--output 	Save the results to text file
-h 	--help 	show the help message and exit

Por ejemplo, si queremos listar un subdominio de un dominio en especifico usariamos sublist3r -d nombre_del_dominio

![[Pasted image 20251123112143.png]]

