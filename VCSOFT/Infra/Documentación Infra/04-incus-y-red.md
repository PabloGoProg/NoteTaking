# Incus, redes y almacenamiento

## Rol de Incus en este repo

**Incus** es el runtime que gestiona contenedores de sistema (**LXC**) en hosts remotos. Terraform habla con Incus a través del provider `lxc/incus` y crea **redes**, **pools de almacenamiento** e **instancias** con CPU, memoria, discos y perfiles de red.

Conceptualmente:

- **Remoto Incus** = endpoint API TLS (p. ej. sedes en Bogotá, Armenia, Ionos) definido en `infra/environments/prod/providers.tf`.
- **Red bridge** = red virtual con rango IPv4, NAT, DNS y rutas DHCP según el diseño de la empresa (`networks.tf` vía módulo `networks`).
- **Storage pool** = dónde viven los volúmenes de las instancias (`storage_pools.tf` vía módulo `storage_pools`).
- **Instancia** = contenedor con perfiles de recurso y volúmenes adjuntos (`instances.tf` vía módulo `incus_instance`).

## Redes

El módulo `networks` recibe un mapa de redes con nombre lógico (p. ej. `main_net`, `dns_net`, `dmz_net`, `mgmt_net`). Cada entrada define:

- Nombre en Incus (p. ej. `vc-main`, `vc-dns`).
- Configuración: `ipv4.address`, `ipv4.nat`, `dns.nameservers`, `ipv4.dhcp.routes` para encaminar tráfico hacia otras subredes o salidas.

Los detalles numéricos están en `infra/environments/prod/networks.tf`. Al leerlo, fíjate en **qué red usa cada tipo de carga** (correo, DNS, DMZ, gestión) para entender el modelo de zonas, no para memorizar IPs.

## Almacenamiento

`storage_pools.tf` delega en el módulo `storage_pools` la creación de pools que luego referencian las instancias (por ejemplo `main_pool` en definiciones de `storage_devices`).

## Instancias

`instances.tf` define un mapa de instancias (claves como `email`, `training`, `dns-davivienda`, etc.) con:

- CPU y memoria.
- Usuario LXC y descripción.
- `network_devices` (interfaz, red lógica, IP fija).
- `storage_devices` (root, home, docker-data, …).
- `extra_config` de Incus (p. ej. `security.nesting` para Docker dentro del LXC).

Ese archivo es la **tabla operativa** de qué servicios viven en qué contenedores; coordina con Ansible, que asume hosts accesibles según el inventario.

## Relación con Ansible

Terraform crea el **contenedor y la red**; Ansible suele **instalar y configurar** software dentro del host. Si añades una instancia nueva, normalmente hará falta **entrada en inventario** y **playbook/rol** acorde.
