# Balanceador de Carga con Vagrant, Apache y Nginx

Este proyecto crea 3 máquinas virtuales usando Vagrant y VirtualBox:

- **web1**: Servidor Apache con contenido personalizado.
- **web2**: Otro servidor Apache con contenido diferente.
- **loadbalancer**: Servidor Nginx que distribuye peticiones entre `web1` y `web2`.

## Especificaciones

- Cada VM tiene 1 CPU y 512MB de RAM.
- Se utilizan IPs privadas:
  - `web1`: 192.168.56.11
  - `web2`: 192.168.56.12
  - `loadbalancer`: 192.168.56.13

## Acceso

Una vez las máquinas estén arriba, accede a:
http://192.168.56.13


Y verás cómo el contenido se alterna entre los servidores web.

## Autor

Axel
