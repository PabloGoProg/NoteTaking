Amazon tiene su propia solución integrada de [[API Gateway]], el cual es un servicio totalmente gestionado de AWS que te permite **crear, publicar, mantener, monitorear y asegurar APIs** a cualquier escala. Especialmente, esta solución provee facilidades para realizar una integración directa con otros servicios de AWS que provean recursos (endpoints), tales como Lambda, servidores backend (EC2, ECS, EKS), AWS Step Functions, DynamoDB, S3 e incluso conexión con servicios privados en VPC Link.

Entre las funcionalidades de AWS API Gateway se encuentran:

1. Soporte para distintos tipos de APIs:
	1. HTTP APIs:
	2. REST APIs:
	3. WebSockets APIs:
2. Servicios de Seguridad Integrada:
	1. Autenticación y Autorización con AWS IAM o AWS Cognito.
	2. Rate Limit.
		1. API Keys y Planes de Uso.
	3. Web Application Firewall.
3. Monitoreo y Logging a nivel de requests:
	1. CloudWatch para la integración de métricas, logs y alertas en un Dashboard UI.
4. Escalabilidad Automática para manejar millones de solicitudes por segundo. Alta disponibilidad sin necesidad de gestión de servidores o balanceadores.
5. Sistema de Versionado y Stages:
	1. Soporte de multiples stages (dev, staging, QA, prod).
	2. Versionamiento y despliegue de cambios sobre el Gateway.

![[Screenshot 2025-07-08 083818.png]]