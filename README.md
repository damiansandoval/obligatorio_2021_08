# Obligatorio Taller de Servidores Linux

_El siguiente proyecto se trata de automatizar un despliegue de un stack LAMP (Linux, Apache, MySQL, PHP).
El mismo está pensado en servidores RedHat y derivados, así como también en Debian y derivados._

### Pre-requisitos 📋

_A continuación se detallan los prerrequisitos necesarios para el correcto despliegue de la solución_

En el equipo Host:
* Visual Studio Code
* VirtualBox o similar
* WSL en caso de usar un bastión sobre un host Windows
* Maquinas Virtuales con Derivados de RedHat y Debian (Para las pruebas se utilizó CentOS 8 y Ubuntu Server 20.04)
* Copiar las Llaves públicas a los host destino para poder ejecutar los comandos por SSH sin necesidad de contraseña

En las maquinas Virtuales:
* usuario ansible con configuración para poder ejecturar comandos sudo sin necesidad de utilizar la contraseña, para esto se agrega la siguiente linea al archivo **/etc/sudoers**

```
ansible ALL=(ALL) NOPASSWD:ALL
```

### Despliegue ⚙️

_Luego de haber completado los prerrequisitos se deberá de ejecturar las siguientes tareas_

* Dentro de Visual studio, conectarse al ambiente **WSL** o al equipo bastión por **ssh** y clonarse el repo:

```
git clone https://github.com/damiansandoval/obligatorio_2021_08
```

_luego de esto cambiarse a la carpeta **obligatorio_2021_08**_

```
cd obligatorio_2021_08
```

_Por último ejecutar el playbook de la siguiente manera_

```
ansible-playbook lamp/site.yml
```

## Prueba de Ejecucíon ⚙️

![Prueba](https://github.com/damiansandoval/obligatorio_2021_08/blob/main/images/playbook-exec.gif)

## Construido con 🛠️

_Para el proyecto se utilizaron las siguientes herramientas_

* [Visual Studio Code](http://www.dropwizard.io/1.0.2/docs/) - IDE
* [Ansible](https://www.ansible.com/) - Automatizacion de tareas
* [Apache](https://httpd.apache.org/) - Servidor Web
* [MySQL](https://www.mysql.com/) - Base de Datos
* [MariaDB](https://mariadb.org/) - Base de Datos
* [PHP](https://www.php.net/) - Desarrollo Web
* [CentOS](https://www.centos.org/) - SO Destino
* [Ubuntu](https://ubuntu.com) - SO Destino


## Versionado 📌

Usamos [Git](http://https://git-scm.com/) para el versionado. y como repositorio se utilizó [GitHub](https://github.com/)

## Autores ✒️

* **Enrique Verdes** - *Codigo Inicial* - [emverdes](https://github.com/emverdes)
* **Ricardo Sanchez** - *Codigo, Pruebas y Documentación* - [ricardosanchezr96](https://github.com/ricardosanchezr96)
* **Damian Sandoval** - *Codigo, Pruebas y Documentación* - [damiansandoval](https://github.com/damiansandoval)
* **Martin Pacheco** - *Codigo, Pruebas y Documentación* - [mrtn90](https://github.com/mrtn90)

## Licencia 📄

Este proyecto está bajo la Licencia [GPLv3](https://www.gnu.org/licenses/gpl-3.0.html)
