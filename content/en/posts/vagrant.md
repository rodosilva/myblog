+++
date = '2024-12-15T22:11:59-05:00'
title = 'Vagrant'
+++

En este laboratorio crearemos un entorno con dos servidores Ubuntu utilizando
la herramienta de Vagrant.

¿Por qué Vagrant?
Dada la velocidad cambiante de tecnología, necesitamos tener espacios de infraestructura que nos ayude a probar, construir y practicar en un entorno seguro, ágil y fácilmente manejable.

Con Vagrant, tenemos la seguridad de que cualquier cosa que se malogre, será fácilmente reemplazable y así poder empezar desde cero en uno o varios servidores en blanco. 


## Capítulo 1: Requerimientos

- VirtualBox: [Instalación](https://www.virtualbox.org/wiki/Linux_Downloads)
- Vagrant: [Instalación](ttps://developer.hashicorp.com/vagrant/install)

## Capítulo 2: Mi Primer Vagrantfile

Vamos a iniciar creando una máquina virtual utilizando solamente código.
Para ello, crearemos un nuevo documento dentro de cualquier carpeta destinada para nuestro proyecto

El docuento deberá llamarse `vagrantfile`

Lo primero que debemos elegir es la versión de la configuración que estaremos utilizando.
La última versión que se tiene `2`

Dado que nuestro proyecto se basa en 2 servidores Ubuntu, procederemos con elegir nuestro `Vagrant Box` desde el  [catálogo](https://portal.cloud.hashicorp.com/vagrant/discover/ubuntu?prev=ChRXeUozYVd4NU16SXRhblZxZFNKZA%3D%3D)

Finalmente, crearemos un nuevo bloque para nuestro primer `host` que llamaremos `labServer01` y le asignaremos una `IP estática` de `192.168.56.10` 

```bash
Vagrant.configure("2") do |config|
  
    ## Definir el OS de forma global
    config.vm.box = "ubuntu/trusty64"
    config.vm.box_version = "20191107.0.0"
    
    ## Definir Un Nuevo Bloque
  
    config.vm.define "labServer01" do |host|
      ## Definir Maquina virtual dentro de este Bloque
      host.vm.network "private_network", ip:"192.168.56.10"
    end
end
```