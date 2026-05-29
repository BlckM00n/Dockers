# 🎯 FirstHacking - DockerLabs

## 📋 Descripción
Máquina DockerLabs **Muy Fácil** - Explota backdoor en vsftpd 2.3.4 (CVE-2011-2523). Acceso directo como root.

## 🕵️ Fase 1 - Enumeración

**Escaneo de puertos:**
`sudo nmap -p- --open -sS -n -Pn 172.17.0.2`

![[Nmap3.png]]

**Escaneo de versiones:**
`sudo nmap -sV -p 21 172.17.0.2`

![[Nmap3.2.png]]

> [!danger] Vulnerabilidad
> vsftpd 2.3.4 tiene un backdoor remoto (CVE-2011-2523)

## 🚀 Fase 2 - Explotación

### Script Python (guardar como exploit.py)

![[Python3.png]]

**Ejecutar:**
`python3 exploit.py 172.17.0.2`

![[Root3.png]]

## ✅ Fase 3 - Verificación

Comandos dentro de la shell:

`whoami`
`# root`

`id`  
`# uid=0(root) gid=0(root)`

`ls -la /root`

## 📸 Evidencias clave

**Nmap detectando vsftpd 2.3.4:**
`21/tcp open  ftp     vsftpd 2.3.4`

**Shell root obtenida:**
`$ whoami`
`root`

## 🧠 Lecciones aprendidas

- vsftpd 2.3.4 tiene backdoor con payload `:)`
- Backdoor abre shell en puerto **6200**
- No siempre hay que escalar privilegios

## 🔗 Referencias

- CVE-2011-2523
- Exploit-DB: 49757
- DockerLabs: FirstHacking