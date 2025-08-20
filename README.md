# Instalación de Odoo 18 y Monitoreo con Wazuh + Elastic Stack

Este repositorio contiene scripts automatizados para instalar **Odoo 18** en Ubuntu 20.04 y configurar un sistema de monitoreo completo usando **Wazuh 4.5.4** con **Elastic Stack 7.17.13**, incluyendo **Wazuh Agent** para supervisar los logs de Odoo.  

Los scripts trabajan juntos para montar un entorno de ERP con monitoreo centralizado.

---

## Contenido del repositorio

- `install_odoo18.sh` – Instala y configura Odoo 18 con PostgreSQL, entorno virtual y servicio systemd.  
- `install_wazuh_manager.sh` – Instala Wazuh Manager, Elasticsearch, Kibana y Filebeat, incluyendo certificados TLS y generación automática de contraseñas.  
- `install_wazuh_agent.sh` – Instala y configura Wazuh Agent para supervisar los logs de Odoo y enviarlos al manager.

---

## Requisitos

- Ubuntu 20.04 LTS
- Usuario con privilegios sudo
- Conexión a Internet
- Puertos abiertos: **1514 TCP** (Wazuh) y **8069 TCP** (Odoo)
- Instalación limpia recomendada

---

## Instalación

Dar permisos de ejecución y ejecutar los scripts en orden:

```bash
chmod +x install_odoo18.sh install_wazuh_manager.sh install_wazuh_agent.sh
./install_odoo18.sh
./install_wazuh_manager.sh
./install_wazuh_agent.sh
```
## Qué hacen los scripts

- Odoo 18

Proporciona un ERP para gestionar ventas, inventario, contabilidad y proyectos.

Crea logs en /var/log/odoo/odoo.log para auditoría y monitoreo.

Configura servicio systemd para iniciar automáticamente.

- Wazuh Manager + Elastic Stack

Centraliza la seguridad y el monitoreo del sistema.

Elasticsearch almacena eventos, Kibana visualiza dashboards y Filebeat envía logs de Odoo al manager.

Genera contraseñas automáticas para el usuario elastic.

- Wazuh Agent

Supervisa logs locales de Odoo y del sistema operativo.

Envía eventos al Wazuh Manager a través del puerto 1514 TCP.

## Función general del sistema

Odoo: Núcleo operativo donde se gestionan los datos de la empresa.

Wazuh Agent: Recolecta logs y eventos de los servidores.

Wazuh Manager + Elastic Stack: Centraliza, almacena y visualiza la información para monitoreo y auditoría en tiempo real.

## Verificación de los servicios 

- sudo systemctl status odoo18
- sudo systemctl status wazuh-manager
- sudo systemctl status filebeat
- sudo systemctl status kibana
- sudo systemctl status elasticsearch
- sudo systemctl status wazuh-agent

## Consideraciones

Scripts diseñados para Ubuntu 20.04 limpio.
Guardar la contraseña generada para el usuario elastic.
Para cambios, editar los archivos .conf y reiniciar los servicios correspondientes.

## Autor

Odoo Script: Angelo
Wazuh Manager + Elastic Stack: Yeltsin
Wazuh Agent: Angelo
