# Ansible

## Rol frente a Terraform

- **Terraform** (en este repo) define Incus, redes, pools y despliegues en Kubernetes desde el estado deseado remoto.
- **Ansible** aplica configuración **sobre hosts ya existentes**: paquetes, servicios systemd, Podman/Quadlet, backups, agentes de seguridad, VPN, etc.

Ambos pueden tocar el mismo servidor (Terraform crea el LXC; Ansible lo configura); conviene coordinar **orden** y **ownership** de cada capa.

## Inventario y variables globales

- Inventario de producción: `ansible/inventory/production/hosts.yml`.
- Variables comunes: `ansible/playbooks/group_vars/all.yml` (incluye valores cifrados con **Ansible Vault** — requiere clave o archivo vault para editar).

No abras ni copies secretos del vault en documentación; solo documenta **qué categorías** existen (DNS, Cloudflare, saltos SSH, etc.).

## Dependencias de colecciones

`requirements.yml` en la raíz declara colecciones de Ansible Galaxy, por ejemplo:

- `community.general`
- `community.docker`
- `community.crypto`
- `middleware_automation.keycloak` (versión fijada)

Instalación típica: `ansible-galaxy collection install -r requirements.yml` (ajustar entorno virtual o política interna).

## Playbooks en `ansible/playbooks/`

Playbooks orientados a dominios (lista actual):

| Playbook | Uso probable (inferido del nombre) |
|----------|--------------------------------------|
| `vc_base.yml` | Baseline de servidor |
| `vc_ntp.yml` | Sincronización de tiempo |
| `vc_dns.yml` | DNS |
| `vc_email.yml` | Correo |
| `vc_backup_mail.yml` / `vc_cloud_backup.yml` | Copias de seguridad |
| `vc_security.yml` | Endurecimiento / seguridad |
| `vc_reverse_proxy.yml` | Proxy inverso |
| `vc_vpn.yml` | VPN |
| `vc_subnet_router.yml` | Enrutado entre subredes |
| `vc_remote.yml` | Acceso remoto |
| `vc_invoice.yml` | Servicio de facturación |
| `vc_training.yml` | Entornos de formación |
| `vc_automation.yml` | Automatización (CI u orquestación en host) |
| `incus_host.yml` | Nodos Incus |
| `rotate.yml` | Rotación de credenciales o claves |

Confirma con el equipo el alcance exacto de cada uno antes de ejecutarlos en producción.

## Roles en `ansible/roles/`

Roles de aplicación concretos (p. ej. `tutor`, `mailcow`, `notifications`) coexisten con la lógica reutilizable en la colección interna.

## Colección `vcsoft.infra`

Ruta: `ansible/ansible_collections/vcsoft/infra/roles/`.

Roles incluidos (entre otros):

| Rol | Función típica |
|-----|----------------|
| `base` | Paquetes y baseline |
| `incus_server` | Ajustes en host Incus |
| `podman` | Instalación/redes/volúmenes Podman |
| `quadlet_service` | Servicios systemd con Quadlet |
| `vpn_gateway` | VPN (incl. tareas Tailscale/Headscale según tareas) |
| `wazuh_agent` | Agente Wazuh |
| `rclone` | Sincronización/copias |
| `ntp_client` | Cliente NTP |
| `backup` | Rutinas de backup |

Cada rol puede tener `defaults/`, `tasks/`, `templates/`; la fuente de verdad es el YAML.

## Operación segura

1. Probar en entorno no productivo cuando exista.
2. Usar `--check` / `--diff` cuando sea compatible.
3. Respetar Vault y políticas de acceso SSH/bastion definidas en `group_vars`.
