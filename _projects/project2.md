---
layout: default
title: Project 2
description: Detección de Intentos de Fuerza Bruta en SSH con Suricata + Hydra
link: https://github.com/villacisJimmy/project2
---

# Project 2 🚀

## S (Situación)

Durante el monitoreo de un entorno de laboratorio, se identificó actividad sospechosa consistente en múltiples intentos de conexión SSH fallidos hacia los puertos 22. 
Este comportamiento es característico de ataques de fuerza bruta, donde un atacante intenta adivinar credenciales por repetición de intentos. 
Detectar este tipo de actividad es crítico para prevenir accesos no autorizados y compromisos del sistema.

Instalación Ubuntu Server & Kali Linux

<img src="{{ '/assets/img/project2/ubuntukali.png' | relative_url }}" alt="Ubuntu Kali - Suricata" width="600">

Instalacion Suricata
```
sudo apt update && sudo apt upgrade -y
sudo apt install software-properties-common
sudo add-apt-repository ppa:oisf/suricata-stable
sudo apt-get install suricata
sudo apt install suricata jq
```
Network Ubuntu, Suricata version y estatus
```
suricata -V
ip add
sudo systemctl status suricata

```
<img src="{{ '/assets/img/project2/1.suricataversionip.png' | relative_url }}" alt="Ubuntu Kali - Suricata" width="600">


<img src="{{ '/assets/img/project2/suricataservice.png' | relative_url }}" alt="Ubuntu Kali - Suricata" width="600">

Network Kali
```
ifconfig
```
<img src="{{ '/assets/img/project2/3.networkkali.png' | relative_url }}" alt="Ubuntu Kali - Suricata" width="600">

## T (Tarea)

Implementar y validar reglas personalizadas en Suricata

- Habilitar IPS con NFQUEUE (inline).
- Cargar y activar reglas (incluyendo una regla local de “brute force” SSH).
- Probar con Hydra desde Kali y ver drops en los logs de Suricata.

El objetivo fue comprobar que el IPS bloquea intentos de conexion bajo los parametros establecidos de fuerza bruta.

## A (Acción)

Preparar modo IPS con NFQUEUE, haciendo uso de "nftables" con queue bypass

```
sudo apt install -y nftables
sudo systemctl enable --now nftables
sudo nft add table inet suri
sudo nft add chain inet suri input '{ type filter hook input priority 0 ; policy accept ; }'
```
<img src="{{ '/assets/img/project2/6.png' | relative_url }}" alt="Ubuntu Kali - Suricata" width="600">

Encolar solo SSH hacia el server (puerto 22 en enp0s1)

```
# Encolar a NFQUEUE 0 con bypass:
sudo nft add rule inet suri input iif "enp0s1" tcp dport 22 queue num 0 bypass

# Ver reglas:
sudo nft list ruleset
```
<img src="{{ '/assets/img/project2/7.png' | relative_url }}" alt="Ubuntu Kali - Suricata" width="600">

Activar NFQUEUE en Suricata `/etc/suricata/suricata.yaml`

```
sudo nano /etc/suricata/suricata.yaml

vars:
  address-groups:
    HOME_NET: "[192.168.64.4]" --> IP Ubuntu Server
```
<img src="{{ '/assets/img/project2/8.png' | relative_url }}" alt="Ubuntu Kali - Suricata" width="600">

Añadir la sección nfqueue
```
nfqueue:
  - id: 0
    fail-open: yes
```
<img src="{{ '/assets/img/project2/9.png' | relative_url }}" alt="Ubuntu Kali - Suricata" width="600">

Asegúrate de incluir custom.rules en rule-files::
```
rule-files:
  - suricata.rules
  - local.rules
```
Forzar Suricata a arrancar con -q 0 (NFQUEUE)
```
sudo systemctl edit suricata

[Service]
ExecStart=
ExecStart=/usr/bin/suricata -c /etc/suricata/suricata.yaml -q 0

```
<img src="{{ '/assets/img/project2/10.png' | relative_url }}" alt="Ubuntu Kali - Suricata" width="600">

Guardar y luego
```
sudo systemctl daemon-reload
sudo systemctl enable --now suricata
sudo systemctl status suricata --no-pager
```
<img src="{{ '/assets/img/project2/11.png' | relative_url }}" alt="Ubuntu Kali - Suricata" width="600">

Carga del modulo
```
sudo modprobe nfnetlink_queue
lsmod | grep nfnetlink_queue
```
<img src="{{ '/assets/img/project2/12.png' | relative_url }}" alt="Ubuntu Kali - Suricata" width="600">

Reglas (ET Open + regla local de brute force)
Descargar/actualizar reglas de la comunidad
```
sudo suricata-update
sudo systemctl reload suricata
```
<img src="{{ '/assets/img/project2/13.png' | relative_url }}" alt="Ubuntu Kali - Suricata" width="600">

Crear una regla local para fuerza bruta SSH

Contaremos SYN repetidos hacia 22/tcp desde la misma IP y drop a partir de N intentos en una ventana de tiempo.
Edita `/etc/suricata/rules/custom.rules` y añade:
```
# Dropea brute force SSH (6+ SYN en 60s hacia 22/tcp)
drop tcp $EXTERNAL_NET any -> $HOME_NET 22 (msg:"LOCAL SSH brute force - demasiados intentos"; flags:S; detection_filter:track by_src, count 6, seconds 60; classtype:attempted-recon; sid:1000001; rev:3;)
```
<img src="{{ '/assets/img/project2/14.png' | relative_url }}" alt="Ubuntu Kali - Suricata" width="600">

Guardar y recargar suricata 
```
sudo systemctl reload suricata
```

Prueba de bloqueo con Kali (Hydra)
```
ping -c 2 192.168.64.4
nmap -p22 192.168.64.4

# Ataque de prueba (usuario "root" de ejemplo; ajusta a tu caso)
hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://192.168.64.4 -t 4 -s 22

```
<img src="{{ '/assets/img/project2/15.png' | relative_url }}" alt="Ubuntu Kali - Suricata" width="600">

Verificación de “drops” en Ubuntu
```
sudo tail -f /var/log/suricata/eve.json
```
<img src="{{ '/assets/img/project2/16.png' | relative_url }}" alt="Ubuntu Kali - Suricata" width="600">

## R — Resultados esperados

- Suricata 8.0.0 corriendo en modo IPS con NFQUEUE.
- Tráfico a SSH (22/tcp) encolado y analizado inline.
- Regla local que bloquea (drop) SYN repetidos (indicativo de fuerza bruta).
- Desde Kali (192.168.64.8), Hydra deja de avanzar y se observan drops en eve.json con la firma "LOCAL SSH brute force - demasiados intentos".


[🔗 Ver en GitHub](https://github.com/villacisJimmy/project1)

[← Volver al inicio]({{ "/" | relative_url }})
