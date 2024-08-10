# DataDog

- Alternativa paga a Prometheus y Grafana
- Parece que tiene mala documentación
- SaaS, hecho en Go
- Monitorización, alertas y métricas (con logs) de servidores, BBDD, tools, networking y servicios
- Cumple las mismas funciones que Jira y Confluence
- AWS, Azure, GCP, Openshift y OpenStack
- Ayuda a ver toda la infra completa en un solo lugar
- Utiliza operadores como agentes para analizar y monitorizar
- Cada usuario puede tener su propio dashboard personalizado
- Soporta una amplia gama de productos a integrar por defecto mediante los agentes
- Soporta análisis de código (con Code Analysis) en GitHub o editor de texto
- CoScreen
- Quality Gates; QA para código de software soporta: Tests, Pipelines, Static Analysis y Software Composition Analysis
- User simil test; Synthetic Monitoring
- El agente completo es datadog-agent y dogstatsd es un módulo especializado para métricas

   Otros módulos son el datadog-trace-agent (para la performance y trousbleshoot de las apps) y el datadog-process-agent para los procesos y contenedores

   Usa los puertos 5000-5002 y 8125
- Service y binario del agent; datadog-agent
- Configuración del angent; /etc/datadog-agent/datadog.yaml
- Configuración para integraciones del agent; /etc/datadog-agent/conf.d/
- Log del agent; /var/log/datalog
