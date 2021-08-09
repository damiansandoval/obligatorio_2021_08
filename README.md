# Obligatorio Taller de Servidores Linux

_El siguiente proyecto se trata de automatizar un despliegue de un stack LAMP (Linux, Apache, MySQL, PHP).
El mismo está pensado para servidores RedHat y derivados, así como también para Debian y derivados._

### Pre-requisitos 📋

_A continuación se detallan los prerrequisitos necesarios para el correcto despliegue de la solución_

En el equipo Host:
* Visual Studio Code (recomendado)
* VirtualBox o similar
* WSL en caso de usar un bastión sobre un host Windows
* Máquinas Virtuales con derivados de RedHat y Debian (para las pruebas se utilizó CentOS 8 y Ubuntu Server 20.04)
* Copiar las Llaves Públicas a los host de destino para poder ejecutar los comandos por SSH sin necesidad de contraseña

En las Máquinas Virtuales:
* Usuario ansible configurado para poder elevar privilegios sin necesidad de utilizar la contraseña, para esto se agrega la siguiente linea al archivo **/etc/sudoers**

```
ansible ALL=(ALL) NOPASSWD:ALL
```

### Despliegue ⚙️

_Luego de haber completado los prerrequisitos se deberán ejecturar las siguientes tareas_

* Dentro de Visual Studio, conectarse al ambiente **WSL** o al equipo bastión por **ssh** y clonarse el repo:

```
git clone https://github.com/damiansandoval/obligatorio_2021_08
```

_luego de esto moverse al directorio **obligatorio_2021_08**_

```
cd obligatorio_2021_08
```

_Por último ejecutar el playbook con el siguiente comando_

```
ansible-playbook lamp/site.yml
```

## Prueba de Ejecución ⚙️

![Prueba](https://github.com/damiansandoval/obligatorio_2021_08/blob/main/images/playbook-exec.gif)

## Cambios realizados sobre el proyecto original 🛠️

_A continuacion se detallan los cambios realizados sobre el codigo original forkeado de [emverdes](https://github.com/emverdes)_

* En todas tareas se cambio el usuario de ejecucion de **root** a **ansible**
* Se agrego el parametro ```become: yes``` para permitir al usuario ansible tener privilegios elevados.
* Para los playbooks **web** y **db** se modificó el parámetro ```hosts``` para que se ejecuten en todos los equipos que contenga el inventario, independientemente de su distribución (derivados **RedHat** o **Debian**)
* Originalmente el inventario tenia 2 grupos, uno para **webservers** y otro para **dbservers**. Se cambio por **RedHat** y **Debian**, para asi correr los playbook indistinto de la distribucion de linux
* El el role **common** se quitaron las tags
* Se cambia el servicio **NTP** por **Chrony**
* Se hace uso del ```when: ansible_facts['os_family'] == "DISTRO"``` para asi poder tener bloques de codigo que se ejecuten en una distro en particular.
* En el caso de **RedHat** se agrego el repositorio **Epel**
* Para **Debian** se opto por instalar **MySQL** mientras que en **RedHat** se utilizó **MariaDB**
* Se agrega el componente **pip** para instalar las dependencias necesarias para la conexion entre python, php y las bases de datos
* Eliminacion de usuario **anonimo** en las bases de datos.
* Se unifican varios playbooks de servidor web en uno solo
* Configuraciones de Selinux y Firewall para que tanto el servidor web como la base de datos funcionen correctamente
* Se modifico la estructura de carpetas del proyecto
* Se agrega un ansible.cfg en la raiz del proyecto
* Se agrega un documento de entrega en el obligatorio
* Se modifica los playbooks para que tomen variables de entorno de ejecucion desde una carpeta, indicando que solo tome de ahi los archivos con extension **yml**
 ``` 
  - name: Incluir variables
    include_vars:
      dir: ../vars/
      extensions:
        - 'yml'
```        

## Construido con 🛠️

_Para el proyecto se utilizaron las siguientes herramientas_

* [Visual Studio Code](http://www.dropwizard.io/1.0.2/docs/) - IDE
* [Ansible](https://www.ansible.com/) - Automatización de tareas
* [Apache](https://httpd.apache.org/) - Servidor Web
* [MySQL](https://www.mysql.com/) - Servidor de Base de Datos
* [MariaDB](https://mariadb.org/) - Servidor de Base de Datos
* [PHP](https://www.php.net/) - Desarrollo Web
* [CentOS](https://www.centos.org/) - SO Destino
* [Ubuntu](https://ubuntu.com) - SO Destino
* [Pip](https://pypi.org/project/pip/) - Instalador de paquetes para Python


## Versionado 📌

Utilizamos [Git](http://https://git-scm.com/) para el versionado. y como repositorio se utilizó [GitHub](https://github.com/)

## Autores ✒️

* **Enrique Verdes** - *Código Inicial* - [emverdes](https://github.com/emverdes)
* **Ricardo Sanchez** - *Código, Pruebas y Documentación* - [ricardosanchezr96](https://github.com/ricardosanchezr96)
* **Damian Sandoval** - *Código, Pruebas y Documentación* - [damiansandoval](https://github.com/damiansandoval)
* **Martin Pacheco** - *Código, Pruebas y Documentación* - [mrtn90](https://github.com/mrtn90)

## Licencia 📄

Este proyecto está bajo la Licencia [GPLv3](https://www.gnu.org/licenses/gpl-3.0.html)
