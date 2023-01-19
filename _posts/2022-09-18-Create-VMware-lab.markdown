---
title: VMware lab
author: nf4ll
date: 2022-09-25 10:43:00 +0000
categories: [Tutorial]
tags: [VMware, Lab]
math: true
mermaid: true
image:
  path: /assets/img/posts/vmwareLab/vmware.png
  width: 934
  height: 720
---
# Crear un laboratorio de pruebas con VMware 16 

La virtualización consiste en crear ordenadores virutales que usan el hardware del ordenador anfitrión (ordenador físico). VMware es la herramienta de virtualización elegida para crear el laboratorio. El laboratorio va a consistir en conectar 2 máquinas virtuales entre ellas. Estos laboratorios se suelen utilizar para realizar pruebas de diferentes tipos. En mi caso es para probar herramientas de hacking y/o diferentes técnicas, con el fin de realizar las pruebas en un entorno controlado, ya que si existe un problema con la máquina virutal, siempre puedes crear una nueva. 

El laboratorio que he creado se basa en 3 máquinas virutales: una máquina virtual que hace de router y dos máquinas, una máquina atacante (Parrot) y una máquina víctima. El "router" se va a encargar de dar conexión a internet a esta LAN, además de que actuará como firewall, por lo que tendremos estas máquinas más aisladas.

![Desktop View](/assets/img/posts/vmwareLab/esquema.PNG)

## Paso 1: Obtener la ISO
Para ello vamos a dirigirnos a <https://www.pfsense.org/download/> y seleccionamos la arquiectura. Para las otras máquinas virtuales realizamos la misma operación con el sistema operativo que se elija.

![Desktop View](/assets/img/posts/vmwareLab/download.PNG)

## Paso 2: Configurar el router virtual
Una vez hemos descargado la ISO ahora vamos a crear la máquina virtual. Una vez hemos creado la máquina nos dirigimos a la configuración (click derecho > settings). En la configuración nos dirigimos al apartado de adaptadores de red y seleccionamos NAT. 

Ahora tenemos que crear un segmento LAN, por lo que nos dirigimos a la opción **LAN Segments** y seleccionamos la opción de añadir y posteriormente OK.

![Desktop View](/assets/img/posts/vmwareLab/configLan.PNG)

Después añadimos una configuración y seleccionamos Network Adapter.

![Desktop View](/assets/img/posts/vmwareLab/configNa.PNG)

Por último seleccionamos el adaptador de red que acabamos de crear y en seleccionamos en la configuración de conexión red segmento LAN. Dentro de esta opción, seleccionamos el segmento que hayamos creado. Nos tendría que quedar la configuración de red como en la siguiente imagen:

![Desktop View](/assets/img/posts/vmwareLab/router.PNG)

## Paso 3: Configurar las máquinas virtuales
Ahora vamos a configurar las máquinas. En la configuración de las máquinas nos dirigimos a Network Adapter y seleccionamos la conexión LAN con el segmento de LAN que hemos creado previamente. Una vez hemos terminado, guardamos los cambios y repetimos el proceso con la otra u otras máquinas que se quieran confiruar en la red local.

![Desktop View](/assets/img/posts/vmwareLab/máquina.PNG)

## Prueba
En mi caso voy a realizar la demostración con el laboratorio creado. Este laboratorio esta formado por el router virtual (pfSense), una máquina con sistema operativo Parrot y por último tenemos una máquina con Windows XP. Desde la máquina parrot vamos a realizar un escaneo del segmento de red con `nmap 192.168.1.0/24`. Como resultado tenemos las 3 máquinas que forman la red.

![Desktop View](/assets/img/posts/vmwareLab/Escaneo.PNG)

## Conclusión
Esta forma de conexión es muy útil para realizar pruebas e investigación, ya que siempre que una máquina pueda romperse, se crea otra con la misma configuración y no existe ninguna pérdida. Personalmente yo lo recomiendo en el ámbito del hacking, para practicar con máquinas como Metasploitable 2 o 3, además de practicar a explotar manualmente ciertos CVE conocidos que pueden tener grandes impactos en la máquina.
