Primero compruebo si tengo conectividad con la victima.
![[Pasted image 20250727225919.png]]
Luego de comprobar la conectividad, hago un escaneo general de la red.
sudo nmap -p- -sS -sC -sV --min-rate=5000 -n -vvv -Pn 172.17.0.2 -oN puertos.
![[Pasted image 20250727230449.png]]Identifico que los puertos abiertos son  el 80 HTTP y el 22 SHH.

