# Visión general

## Qué es este repositorio

**vcsoft-infra** concentra recursos para **definir, provisionar y operar** la infraestructura de VCSOFT: máquinas lógicas sobre Incus (LXC), un clúster Kubernetes basado en k0s, automatización con Ansible sobre los hosts, y el portal de desarrolladores Backstage. No es una única herramienta, sino un **conjunto de capas** que conviene ver por separado y luego como sistema.

## Público objetivo

Personas de **plataforma / infraestructura / SRE** que deben entender dónde vive cada pieza y cómo encajan los cambios. El código asume familiaridad gradual con Terraform, redes y Linux; el [roadmap](ROADMAP-APRENDIZAJE.md) ordena temas si estás empezando.

## Cómo se reparten los roles

| Capa | Herramienta típica | Rol en este repo |
|------|-------------------|------------------|
| Estado deseado de recursos cloud / plataforma | **Terraform** | Incus (instancias, redes, pools), integración con Infisical; en otro stack, k0s + Helm + manifiestos Kubernetes |
| Configuración y paquetes **dentro** de los servidores | **Ansible** | Playbooks y roles que aplican políticas, servicios (correo, DNS, seguridad, backups, etc.) |
| Catálogo y experiencia de desarrollador | **Backstage** | Código en `backstage/`, despliegue referenciado desde Terraform del clúster; metadatos del sistema en la raíz |

Terraform responde a **“qué existe y con qué forma”** (API declarativa). Ansible responde a **“cómo queda el SO y los servicios encima”** (imperativo idempotente). Backstage es **portal y catálogo**, no sustituye a Terraform ni a Ansible.

## Catálogo de software (Backstage)

En la raíz del repo, `catalog-info.yaml` declara un **System** de Backstage que apunta a la plataforma Terraform (Anotaciones `terraform/organization` y `terraform/workspaces`). Sirve para enlazar documentación y ownership en el portal corporativo; los detalles exactos deben mantenerse alineados con Terraform Cloud y el equipo propietario (`spec.owner`).

## Lectura recomendada en orden

1. [02-mapa-del-repositorio.md](02-mapa-del-repositorio.md) — dónde está cada cosa  
2. [03-terraform-stacks.md](03-terraform-stacks.md) — los dos workspaces  
3. [05-secretos-infisical.md](05-secretos-infisical.md) — cómo se inyectan secretos en prod  
4. [07-ansible.md](07-ansible.md) — operación sobre hosts  
