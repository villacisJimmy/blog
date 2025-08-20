---
layout: default
title: Project 1
description: Detección de escaneo Nmap y conexiones SSH en puertos 22 y 2222 mediante el uso de IDS SNORT
link: https://github.com/villacisJimmy/project1
---

# Project 1 🚀

## S (Situación)

Durante las prácticas en un entorno de laboratorio de seguridad, se configuró Snort sobre Ubuntu Server como sistema de detección de intrusos (IDS) para monitorear conexiones sospechosas en servicios críticos.  

El foco estuvo en SSH (puerto 22 y alternativo 2222) y en la identificación de escaneos con Nmap, herramienta comúnmente utilizada en la fase de reconocimiento por atacantes.

Instalación Ubuntu Server & Kali Linux

<img src="{{ '/assets/img/project1/ubuntukali.png' | relative_url }}" alt="Ubuntu Kali - IDS Snort" width="600">

Instalacion SNORT
```
sudo apt update && sudo apt upgrade -y
sudo apt install snort -y
```

<img src="{{ '/assets/img/project1/instalacionsnort.png' | relative_url }}" alt="Ubuntu Kali - IDS Snort" width="600">

Network Ubuntu
```
ifconfig
```
<img src="{{ '/assets/img/project1/networkubuntu.png' | relative_url }}" alt="Ubuntu Kali - IDS Snort" width="600">

Network Kali
```
ifconfig
```
<img src="{{ '/assets/img/project1/networkkali.png' | relative_url }}" alt="Ubuntu Kali - IDS Snort" width="600">

Ejecutando Snort en modo escucha
```
sudo snort -i enp0s1 -A console -c /etc/snort/snort.conf
```
<img src="{{ '/assets/img/project1/snortinicializado.png' | relative_url }}" alt="Ubuntu Kali - IDS Snort" width="600">


## T (Tarea)

Implementar y validar reglas personalizadas en Snort (`local.rules`) para:

- Detectar intentos de conexión al puerto SSH 22.  
- Detectar intentos de conexión al puerto SSH alternativo 2222.  
- Detectar posibles escaneos con Nmap (SYN scan) sobre esos puertos.  

El objetivo fue comprobar que el IDS emite alertas claras y diferenciadas para cada evento.

## A (Acción)

Se editaron las reglas en `/etc/snort/rules/local.rules`:


```snort
Sintaxis básica regla Snort
alert <PROTOCOLO> <IP_ORIGEN> <PUERTO_ORIGEN> -> <IP_DESTINO> <PUERTO_DESTINO> (opciones)

# Conexión a SSH estándar
alert tcp any any -> any 22 (msg:"ALERTA: Conexión a puerto SSH 22"; sid:100001; rev:1;)

# Conexión a SSH alternativo
alert tcp any any -> any 2222 (msg:"ALERTA: Conexión a puerto SSH 2222"; sid:100002; rev:1;)

# Escaneo Nmap detectado en puerto 22
alert tcp any any -> any 22 (msg:"POSIBLE ESCANEO NMAP - puerto 22"; flags:S; sid:100003; rev:1;)

# Escaneo Nmap detectado en puerto 2222
alert tcp any any -> any 2222 (msg:"POSIBLE ESCANEO NMAP - puerto 2222"; flags:S; sid:100004; rev:1;)

```

- alert → acción de la regla (podría ser drop, reject, etc. si quieres bloquear).
- tcp → protocolo (SSH usa TCP).
- any any → cualquier IP y puerto de origen.
- -> → dirección del tráfico (de origen a destino).
- any 22 o any 2222 → cualquier IP de destino pero específicamente esos puertos.
- msg → mensaje que aparecerá en la alerta.
- sid → identificador único de regla (empieza desde 1000000 en tus reglas locales).
- rev → versión de la regla (incrementa si haces cambios).

<img src="{{ '/assets/img/project1/snortrules.png' | relative_url }}" alt="Ubuntu Kali - IDS Snort" width="600">

```
Guardar y verificar sintaxis:
sudo snort -T -c /etc/snort/snort.conf

Correr Snort en modo IDS con salida en consola:
sudo snort -A console -q -c /etc/snort/snort.conf -i enp0s1
```


```
Se simularon ataques y accesos:
Escaneo con Nmap:
nmap -p 22,2222 <IP_OBJETIVO>

Conexión SSH estándar:
ssh usuario@<IP_OBJETIVO> -p 22
```

<img src="{{ '/assets/img/project1/nmapscan.png' | relative_url }}" alt="Ubuntu Kali - IDS Snort" width="600">
<img src="{{ '/assets/img/project1/sshkali.png' | relative_url }}" alt="Ubuntu Kali - IDS Snort" width="600">


Snort generó alertas diferenciadas según el tipo de conexión o escaneo.

<img src="{{ '/assets/img/project1/nmapscanrulesnort.png' | relative_url }}" alt="Ubuntu Kali - IDS Snort" width="600">
<img src="{{ '/assets/img/project1/port22.png' | relative_url }}" alt="Ubuntu Kali - IDS Snort" width="600">
<img src="{{ '/assets/img/project1/port2222.png' | relative_url }}" alt="Ubuntu Kali - IDS Snort" width="600">


## R (Resultado)
- Se implementaron reglas personalizadas que detectan tráfico en puertos críticos de SSH (22 y 2222).
- El IDS discriminó entre conexiones legítimas y posibles escaneos Nmap.
- El laboratorio demostró cómo un SOC Analyst puede ajustar firmas en Snort para responder a escenarios específicos.
- Conclusión: el sistema de detección es efectivo para reconocimiento temprano de accesos y escaneos, permitiendo accionar medidas de seguridad proactivas.


[🔗 Ver en GitHub](https://github.com/villacisJimmy/project1)

[← Volver al inicio]({{ "/" | relative_url }})
