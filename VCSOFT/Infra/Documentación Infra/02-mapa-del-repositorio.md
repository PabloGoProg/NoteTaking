# Mapa del repositorio

## Vista rápida

```
vcsoft-infra/
├── 00-setup-terraform/     # Stack Terraform: k0s, Helm, recursos K8s (p. ej. Backstage)
├── infra/
│   └── environments/
│       └── prod/           # Stack Terraform: Incus, redes, instancias, Jenkins (Helm), Infisical
├── ansible/                # Playbooks, inventario, roles y colección vcsoft.infra
├── backstage/
│   └── backstage-vcsoft/   # Aplicación Backstage (Node/Yarn)
├── requirements.yml        # Colecciones Ansible externas
├── catalog-info.yaml        # Entrada de catálogo Backstage (System)
└── README.md
```

## Tabla carpeta → responsabilidad

| Ruta | Responsabilidad |
|------|-----------------|
| `00-setup-terraform/` | Terraform Cloud workspace **VCSOFT-Interno**: `k0sctl_config`, releases Helm (MetalLB, ingress-nginx), manifiestos Kubernetes para Backstage/Postgres, etc. Ver `provider.tf`, `main.tf`, `backstage.tf`. |
| `infra/environments/prod/` | Terraform Cloud workspace **Infra-interna**: módulos `secrets` (Infisical), `networks`, `storage_pools`, `incus_instance`, `automation` (Jenkins). Archivos como `networks.tf`, `instances.tf`, `automation.tf`, `infisical.tf`. |
| `infra/environments/prod/modules/` | Módulos reutilizables con README generados (terraform-docs) donde aplique. |
| `infra/environments/prod/helm/jenkins/` | Valores Helm para Jenkins (referenciados desde el módulo `automation`). |
| `ansible/playbooks/` | Playbooks por dominio (`vc_email.yml`, `vc_dns.yml`, `vc_security.yml`, …). |
| `ansible/inventory/production/` | Inventario de hosts (p. ej. `hosts.yml`). |
| `ansible/roles/` | Roles “sueltos” (p. ej. tutor, mailcow). |
| `ansible/ansible_collections/vcsoft/infra/` | Colección interna: roles `base`, `vpn_gateway`, `wazuh_agent`, `podman`, `quadlet_service`, `backup`, etc. |
| `backstage/backstage-vcsoft/` | Código fuente del portal Backstage; el despliegue en clúster se gestiona desde `00-setup-terraform/`. |

## Archivos en la raíz útiles para orientarse

| Archivo | Uso |
|---------|-----|
| `requirements.yml` | Colecciones Ansible requeridas (`community.general`, `community.docker`, …). |
| `catalog-info.yaml` | Metadatos del sistema para Backstage (Terraform org/workspaces). |

## Dónde profundizar

- Terraform prod: `infra/environments/prod/README.md` (tabla de módulos vía terraform-docs).  
- Módulos: `infra/environments/prod/modules/<nombre>/README.md`.  
