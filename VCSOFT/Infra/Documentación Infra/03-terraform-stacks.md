# Stacks de Terraform

Este repositorio usa **HashiCorp Terraform Cloud** con **dos workspaces distintos**, cada uno con su propio estado y proveedores. No mezclar configuración entre carpetas sin entender qué workspace la ejecuta.

## Resumen

| Carpeta | Workspace (Terraform Cloud) | Organización |
|---------|----------------------------|--------------|
| `00-setup-terraform/` | `VCSOFT-Interno` | `VCSOFT` |
| `infra/environments/prod/` | `Infra-interna` | `VCSOFT` |

Definición en código:

- `00-setup-terraform/provider.tf` → bloque `terraform { cloud { ... } }` con workspace `VCSOFT-Interno`.
- `infra/environments/prod/providers.tf` → bloque `terraform { cloud { ... } }` con workspace `Infra-interna`.

## Stack `00-setup-terraform` (clúster y apps en Kubernetes)

**Enfoque:** orquestador **k0s** vía recurso `k0sctl_config` (proveedor Mirantis `k0sctl`), luego **Helm** y **Kubernetes**.

Proveedores relevantes en `provider.tf`:

- `k0sctl` — aprovisionamiento del clúster k0s.
- `helm` — charts (p. ej. MetalLB, ingress-nginx).
- `kubernetes` — Deployments, Services, Ingress, Secrets, PVCs, RBAC (p. ej. Backstage y Postgres en `backstage.tf`).
- `kubectl` — declarado para uso eventual con manifiestos.
- `backstage` — provider opcional para integración con API de Backstage (URL base en `provider.tf`).

Archivos clave:

- `main.tf` — k0sctl, releases Helm, comentarios sobre CRDs/MetalLB.
- `backstage.tf` — namespace `backstage`, Postgres, despliegue Backstage, ingress, service account y secretos (revisar que **no haya secretos reales** en claro en el repositorio; usar variables y gestores de secretos).

## Stack `infra/environments/prod` (Incus y automatización)

**Enfoque:** hipervisor / contenedores de sistema **Incus** (LXC) y secretos vía **Infisical**.

Proveedores en `providers.tf`:

- `incus` (source `lxc/incus`) — remotos por sede (`vc-main-bogota`, `vc-main-armenia`, `vc-ionos`, etc.) con direcciones HTTPS internas.
- `infisical` — autenticación universal con `client_id` / `client_secret` (variables sensibles del workspace).

Módulos invocados desde archivos dedicados (no depender solo de `main.tf`, que puede contener bloques comentados):

- `infisical.tf` — `module "secrets"`.
- `networks.tf` — `module "networks"`.
- `storage_pools.tf` — `module "storage_pools"`.
- `instances.tf` — `module "incus_instance"`.
- `automation.tf` — `module "automation"` (Jenkins en Kubernetes usando `kube_config_path`).

Documentación autogenerada por módulo: `infra/environments/prod/modules/*/README.md` y `infra/environments/prod/README.md`.

## Buenas prácticas al trabajar

1. **Ejecutar `terraform plan`** desde el directorio correcto y con el workspace adecuado en Terraform Cloud.
2. **Variables sensibles** (Infisical, tokens Incus) deben cargarse vía Terraform Cloud o entorno seguro, no commiteadas.
3. Los **módulos** encapsulan redes, pools, instancias y secretos: cambiar inputs en `variables.tf` o en los `.tf` que llaman al módulo según el patrón existente.
