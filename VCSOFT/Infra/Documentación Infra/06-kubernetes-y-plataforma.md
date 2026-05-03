# Kubernetes (k0s) y plataforma en clúster

## Qué cubre este bloque

El directorio `00-setup-terraform/` describe un **clúster Kubernetes ligero k0s**, desplegado con el proveedor **k0sctl**, y encima instala componentes con **Helm** y recursos nativos de **Kubernetes**.

## k0s y k0sctl

- En `main.tf`, el recurso `k0sctl_config` define hosts (roles, IPs privadas, SSH) y la versión de k0s.
- Provisioners remotos copian scripts y generan `kubeconfig` en el entorno esperado para que los providers `helm` y `kubernetes` usen `~/.kube/config` (según `provider.tf`).

Para operar el clúster fuera de Terraform necesitarás `kubectl` y acceso de red/SSH según las políticas del equipo.

## Helm

Ejemplos en `main.tf`:

- **MetalLB** — balanceador de cargas para servicios tipo LoadBalancer.
- **ingress-nginx** — dos releases (`ingress-nginx`, `ingress-nginx-two`) con values distintos bajo `values/nginx/`, usados para exponer servicios HTTP/HTTPS con diferentes clases o configuraciones.

Hay comentarios sobre orden de aplicación (p. ej. CRDs de MetalLB); si falla un apply, revisar dependencias entre recursos.

## Backstage y Postgres en el clúster

El archivo `backstage.tf` declara:

- Namespace `backstage`.
- Secretos (Postgres, GitHub, token de clúster, etc.).
- PVC con `storage_class_name` acorde al entorno (p. ej. `ceph-filesystem`).
- Deployment de Postgres y Deployment de Backstage con imagen desde **registro interno** (`registry.vc-soft.com:5000/...`) y digest fijado.
- Service e **Ingress** con TLS y hosts internos/públicos según variables (`var.vcsoft-internal-stackhost`, `var.vcsoft-public-stackhost`), clase `nginx-two`.

### Código fuente vs imagen desplegada

- El **código** de la aplicación Backstage vive en `backstage/backstage-vcsoft/` (monorepo Yarn, paquetes `app` y `backend`).
- El **despliegue** que corre en Kubernetes usa la imagen construida y publicada en el registry; cambios en el portal requieren **pipeline de build/push** y actualizar la referencia de imagen en Terraform si no está automatizado.

## Seguridad

- Cualquier secreto en manifiestos debe migrarse a **Secret** gestionado de forma segura o a un sistema externo; evitar valores de ejemplo en Git.
- El ServiceAccount de Backstage tiene **ClusterRoleBinding** al rol `view` para lectura del API server; ajustar RBAC según principio de mínimo privilegio cuando evolucione el producto.

## Lecturas cruzadas

- [03-terraform-stacks.md](03-terraform-stacks.md) — workspace `VCSOFT-Interno`.
- [08-herramientas-operativas.md](08-herramientas-operativas.md) — papel de Backstage como portal.
