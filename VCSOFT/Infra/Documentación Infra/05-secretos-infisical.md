# Secretos e Infisical

## Por qué aparece Infisical

En `infra/environments/prod`, Terraform necesita credenciales que **no deben estar en Git**: token de Incus, contraseñas de Ansible, claves SSH públicas en contextos sensibles, client IDs de integraciones, etc. Esas credenciales se centralizan en **Infisical** y se consumen en tiempo de plan/aplicación mediante el provider oficial `infisical/infisical`.

## Autenticación del provider

En `providers.tf`, el bloque `provider "infisical"` usa:

- `host` — URL del servidor Infisical de la organización.
- `auth.universal` — `client_id` y `client_secret` que vienen de **variables de Terraform** (`var.infisical_client_id`, `var.infisical_client_secret`), típicamente inyectadas por Terraform Cloud como variables sensibles.

## Módulo `secrets`

El archivo `infisical.tf` instancia `module "secrets"` desde `./modules/infisical`, con:

- `workspace_id` — espacio de trabajo en Infisical (valor fijado en el `.tf`; si cambia el proyecto, actualizar aquí).
- `env_slug` — p. ej. `prod`.
- Lista `secrets` — carpetas lógicas en Infisical (`folder_path`) agrupadas por nombre (`name`) para exponerlas al resto de módulos como `module.secrets.secrets["incus"]`, `["ansible"]`, `["general"]`, etc.

El módulo usa `data "infisical_secrets"` y, para valores efímeros, `ephemeral "infisical_secret"` (ver comentarios en `modules/infisical/main.tf` y la documentación del provider en el Registry).

## Flujo típico

1. Los secretos viven en Infisical, organizados por carpetas (`/incus`, `/Ansible`, `/General`, …).
2. Terraform lee el workspace y el entorno indicados.
3. Otros módulos reciben valores vía `module.secrets.secrets[...]` (p. ej. token Incus en el provider `incus`, contraseña Ansible en `incus_instance`, credenciales para plantillas Jenkins).

## Buenas prácticas

- **Nunca** pegar secretos en archivos `.tf` o `.tfvars` versionados.
- Rotar **client_id / client_secret** de la identidad de máquina según política de Infisical.
- Revisar periódicamente qué carpetas consume `infisical.tf` y alinear con el equipo de seguridad.
- Tras el plan de Terraform, validar que los recursos efímeros no dejen rastros indebidos en logs de CI.
