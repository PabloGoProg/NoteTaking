# Herramientas operativas: Jenkins y Backstage

## Jenkins

La automatización de CI en Kubernetes se modela con el módulo `automation` en `infra/environments/prod/automation.tf`:

- Chart oficial de Jenkins (`charts.jenkins.io`), versión fijada en el bloque `jenkins_chart_basic_info`.
- Namespace `jenkins`.
- Valores renderizados con `templatefile` desde `helm/jenkins/values.yaml`, inyectando credenciales desde `module.secrets` (claves OAuth o similares bajo el secreto `general` en Infisical).
- Volumen persistente vía configuración de PV (p. ej. `local-path`, host path `/data/jenkins-volume` en el ejemplo del módulo).

El `kube_config_path` apunta al fichero kubeconfig local (`~/.kube/config`), coherente con un apply desde una máquina que ya tenga acceso al clúster donde corre Jenkins.

**Para desarrolladores:** los pipelines concretos suelen vivir en Jenkins o en repos de aplicación; este repo define **cómo se instala** Jenkins en el clúster, no el contenido de cada job.

## Backstage

### Portal

Backstage es el **portal de desarrolladores**: catálogo de servicios, documentación, plugins (Kubernetes, etc.). La instancia desplegada en el clúster se describe en `00-setup-terraform/backstage.tf` (imagen, variables de entorno, ingress).

### Código del producto

El monorepo bajo `backstage/backstage-vcsoft/` contiene la aplicación (frontend `packages/app`, backend `packages/backend`), plantillas de ejemplo y configuración (`app-config.yaml`, `catalog-info.yaml` local al proyecto).

### Catálogo y este repositorio

- En la **raíz** del repo, `catalog-info.yaml` registra el **System** de la plataforma Terraform para Backstage (owner, dominio, anotaciones de workspaces).
- Los equipos suelen añadir `catalog-info.yaml` por componente en sus repos; aquí se documenta la **plataforma** como tal.

### Integración Kubernetes

Los ejemplos en `backstage/backstage-vcsoft/catalog-info.yaml` muestran anotaciones como `backstage.io/kubernetes-cluster` y selectores de labels para enlazar entidades con cargas en el clúster; la configuración efectiva depende de plugins habilitados en `app-config`.

## Resumen

| Herramienta | Definida principalmente en | Notas |
|-------------|---------------------------|--------|
| Jenkins | `infra/environments/prod/` (módulo `automation`, `helm/jenkins/values.yaml`) | CI en clúster; secretos vía Infisical |
| Backstage | `00-setup-terraform/backstage.tf` + código `backstage/backstage-vcsoft/` | Portal; catálogo raíz en `catalog-info.yaml` |
