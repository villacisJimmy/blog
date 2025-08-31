---
layout: default
title: Project 3
description: ARP Spoofing and MiTM Attack
link: https://github.com/villacisJimmy/project1
---

# Project 3 🚀

## S (Situación)

ARP Spoofing and MiTM Attack

Este laboratorio tiene como objetivo demostar el uso de un conjunto de herramientas para generar un ataque ARP Spoofing y el robo de credenciales en sitios sin tecnología SSL y TLS. Como cualquier reto de seguridad informática tenemos que tener en consideración la primera fase [reconocimiento].
[Reconocimiento]: No se puede atacar lo que no se conoce, de ahí tan famosa frase "conoce a tu enemigo y conócete a ti mismo" de Sun Tzu. Pues bien debemos identificar que dispositivo va a ser nuestra victima. 
Para este laboratorio hemos preparado un entorno con 2 máquinas virtuales. La primera [kali linux] quién asume el rol de atacar, la segunda Windows11 quien sera la victima y un tercer dispositivo sera el Router.

[Consideración 1]: Este es un ataque que se realizará desde dentro de la red objetivo.
[Consideracion 2]: Una red real tiene implementado mecanismos de seguridad que hacen fácilmente identificar estos ataques, ya que estas herramientas en su uso por defecto generar mucho ruido. Un entorno empresarial es un escenario con mayor complejidad lo que implica mas tiempo y estudio para no ser detectado.
[Consideración 3]: La información dinámica de la tabla ARP es eliminada en un transcurso de tiempo establecido, pero la información ingresada manualmente (estática) se mantiene hasta que se cumplan ciertas condiciones.

[Descripción del ataque]:
- Un atacante [Kali] con direccion IP [1.1.1.1] y MAC [01-01-01-01-01-01], tiene como objetivo interponerse en la comunicacion del sistema [Windows11] con IP [2.2.2.2] y MAC [02-02-02-02-02-02] y el router con IP [3.3.3.3] y MAC [03-03-03-03-03-03].
- La maquina Kali envia tramas [ARP Reply] a cada uno de ellos. Kali le indica a windows11 que la IP del router se corresponde con su MAC. Al equipo router le indica que la IP de windows11 se corresponde con su MAC
- Cuando ambos sistemas reciban la información y lo almacenen en sus tablas ARP se encontrarán ya engañados. El sistema Windows creerá que se esta comunicando con la IP del router pero estará enviandole la información a la máquina Kali.

Para qué el ataque sea exitoso, se deben cumplir ciertos criterios:
- Que el atacante este dentro del mismo segmento que la víctima.
- Que el engaño sea mantenido durante el tiempo que sea necesario para realizar el ataque.
    - Para esto la máquina atacante debe enviar cada cierto tiempo tramas ARP reply falsas.
    - De esta manera logramos que la victima no trate de obtener la información de la tabla por sus propios medios.

[Tools]: Bettercap, Nmap, Wireshark

[Nmap]: Es una herramienta muy versátil, con muchas funcionalidades y principalmente usada en la fase de reconocimiento ya que nos permite identificar equipos, servicios, sistemas opertativos entre otros. 
[Bettercap]: Es un framework de auditoria de red, con muchas funcionalidades.
[Wireshark]: Wireshark is a network protocol analyzer.


## T (Tarea)
- Objetivo principal: Interponerse en la comunicación entre Windows11 y el router, logrando capturar tráfico web en texto claro.
- Subtareas:
  - Identificar direcciones IP y MAC activas en la red (fase de reconocimiento).
  - Enviar respuestas ARP falsas para engañar a la víctima y al router.
  - Mantener la suplantación activa durante toda la sesión.
  - Usar herramientas de auditoría de red para analizar el tráfico interceptado.


## A (Acción)

1. Verificar direccionamiento IP 

<img src="{{ '/assets/img/project3/ipkali.png' | relative_url }}" alt="ARP Spoofing and MiTM Attack" width="600">
<img src="{{ '/assets/img/project3/ipwondows.png' | relative_url }}" alt="ARP Spoofing and MiTM Attack" width="600">

2. Suponiendo que no conocemos la dirección IP de windows, el primer paso es realizar un reconocimiento en la red para ver que equipos se encuentran vivos.
  - Realizamos un mapeo con la herramienta [nmap] a la [red], parametro obtenido en el paso 1 apartado [netmask: 255.255.255.0]
<img src="{{ '/assets/img/project3/nmapnetwork.png' | relative_url }}" alt="ARP Spoofing and MiTM Attack" width="600">

  - Primero debemos instalar bettercap en el sistema Kali
'''
sudo apt install bettercap
'''
<img src="{{ '/assets/img/project3/betterinstall.png' | relative_url }}" alt="ARP Spoofing and MiTM Attack" width="600">
  
  - Podemos ver el menu de ayuda con la palabra clave 'help'
<img src="{{ '/assets/img/project3/bettermenu2.png' | relative_url }}" alt="ARP Spoofing and MiTM Attack" width="600">

  - Utilizamos el framework Bettercap para realizar la misma tarea de reconocimiento en la red.
'''
net.recon on
net.probe on
net.show
'''
<img src="{{ '/assets/img/project3/betterrecon.png' | relative_url }}" alt="ARP Spoofing and MiTM Attack" width="600">

La interfaz es mucho mas fácil de interpretar y podemos ver claramente los dispositivos del laboratorio

  - Realizamos el ataque con las siguientes instrucciones
'''
set arp.spoof.fullduplex true
set arp.spoof.targets [192.168.64.10]   -> IP Windows
arp.spoof on
net.sniff on
'''
<img src="{{ '/assets/img/project3/betterattack.png' | relative_url }}" alt="ARP Spoofing and MiTM Attack" width="600">

Con eso ya somos capaces de interceptar el trafico que genera la maquina Windows

Como parte del laboratorio tiene como finalidad demostrar la captura de credenciales sobre el protocolo HTTP, seguimos con las siguientes instrucciones

  - Realizar login dentro de [testfire.net/login.jsp] este es un sitio web vulnerable utilizado para practicar de pentesting.

<img src="{{ '/assets/img/project3/windowslogin.png' | relative_url }}" alt="ARP Spoofing and MiTM Attack" width="600">

Una vez el usurio ingresa sus credenciales y haya realizado el login, en nuetra máquina Kali somos capaces de ver las credenciales en texto plano. Esto como consecuencia del uso de HTTP.

<img src="{{ '/assets/img/project3/bettercredentials.png' | relative_url }}" alt="ARP Spoofing and MiTM Attack" width="600">


Hasta acá ya hemos podido demostrar como es posible realizar un ataque que MiTM ayudandonos del protocolo ARP. Ahora vamos a poceder a realizar un poco de verificación y ver un poco como actuó este ataque detrás de escena.

  - Procedemos en la maquina windows a verificar la tabla ARP. Dentro de la terminal o powershell
'''
arp -a
'''
<img src="{{ '/assets/img/project3/arplast.png' | relative_url }}" alt="ARP Spoofing and MiTM Attack" width="600">

Vemos la direccion IP del router [192.168.64.1] asocianda a su dirección MAC [a2-78-17-b6-59-64]

Ahora vamos a ver la comparacion entre la tabla antes y después del ataque con bettercap

<img src="{{ '/assets/img/project3/arpwindows.png' | relative_url }}" alt="ARP Spoofing and MiTM Attack" width="600">

Haciendo uso de wireshark analizamos el tráfico al momento que el ataque fue realizado.

<img src="{{ '/assets/img/project3/wireshark.png' | relative_url }}" alt="ARP Spoofing and MiTM Attack" width="600">
<img src="{{ '/assets/img/project3/wireshark2.png' | relative_url }}" alt="ARP Spoofing and MiTM Attack" width="600">



## R (Resultado)

- El ataque fue exitoso: Kali logró posicionarse como intermediario en la comunicación entre Windows11 y el router.
- Se capturó tráfico sensible en texto claro, evidenciando usuario y contraseña en un sitio HTTP sin cifrado.
- El laboratorio demostró:
  - La vulnerabilidad de protocolos sin cifrado.
  - La importancia de implementar TLS/HTTPS y medidas de detección (IDS/IPS).





[🔗 Ver en GitHub](https://github.com/villacisJimmy/project3)

[← Volver al inicio]({{ "/" | relative_url }})
