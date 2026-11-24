# Caso-Pr-ctico-Gesti-n-de-infraestructura-como-c-digo-IaC-y-ambientes-de-nube-AWS

Introducción
Este repositorio contiene la solución propuesta para los distintos escenarios planteados en la evaluación técnica de Deuna!. El objetivo es demostrar conocimientos en arquitectura cloud sobre AWS, observabilidad, FinOps, infraestructura como código utilizando Terraform y gestión de incidentes en entornos productivos.

Objetivos
La solución aborda los siguientes temas:

Monitoreo y alertamiento de microservicios desplegados en Amazon ECS.
Identificación de servicios que alcanzan su límite máximo de escalamiento.
Cálculo del costo aproximado por transacción monetaria y no monetaria.
Implementación de infraestructura segura mediante Terraform.
Gestión y respuesta ante incidentes críticos en producción.

-------------------Tarea 1: Monitoreo de Escalamiento en ECS--------------------

La propuesta permite detectar cuándo un servicio de ECS llega a su capacidad máxima configurada y ya no puede continuar escalando, aunque la carga siga aumentando.

Componentes principales
Amazon ECS
Application Auto Scaling
Amazon EventBridge
AWS Lambda
CloudWatch Logs
Plataforma externa de observabilidad
Flujo
ECS intenta escalar un servicio.
El servicio alcanza el límite configurado en maxCapacity.
EventBridge detecta el evento.
Lambda recopila información adicional del servicio.
El evento se registra en CloudWatch Logs.
La plataforma de observabilidad genera alertas y dashboards.
Beneficios
Detección temprana de saturación.
Menor riesgo de degradación de servicio.
Integración con herramientas de monitoreo existentes.
Reducción de ruido mediante agrupación de alertas.

------------------Tarea 2: Costeo por Transacción-----------------------------

La solución permite estimar el costo asociado a operaciones monetarias y no monetarias.

Clasificación
Monetarias

Pagos
Transferencias
Recargas
Retiros
No monetarias

Onboarding
Actualización de perfil
Consultas de saldo
Estrategia
Se combinan:

Costos directos identificables por servicio.
Costos compartidos distribuidos según utilización.
Servicios considerados
ECS
Lambda
API Gateway
Aurora PostgreSQL
SQS
S3
Herramientas AWS utilizadas
AWS Cost and Usage Report (CUR)
Amazon S3
AWS Glue
Amazon Athena
AWS Cost Explorer
Resultado esperado
Obtención del costo promedio por transacción y visibilidad del gasto por categoría para áreas técnicas, financieras y de producto.

---------------Tarea 3: Infraestructura como Código---------------------------------

La infraestructura se implementa utilizando Terraform, siguiendo buenas prácticas de modularidad, seguridad y reutilización.

Estructura del repositorio
deuna-tf-data-platform/
├── README.md
├── modules/
│   ├── kms/
│   ├── s3/
│   ├── aurora/
│   └── secrets/
└── envs/
    ├── dev/
    └── prod/
Componentes
KMS
Llave de cifrado administrada por AWS.
Rotación automática.
Acceso restringido mediante IAM.
S3
Bucket privado.
Versionado habilitado.
Cifrado con KMS.
Políticas para impedir acceso público.
Aurora PostgreSQL
Base de datos desplegada en subredes privadas.
Backups automáticos.
Monitoreo habilitado.
Cifrado con KMS.
Secrets Manager
Almacenamiento seguro de credenciales.
Rotación automática.
Sin contraseñas expuestas en el código.

-----Tarea 4: Gestión de Incidentes--------------

Se define un procedimiento para responder a incidencias que afecten servicios críticos como payments-processor.

Proceso de diagnóstico
Verificar el impacto en usuarios.
Revisar métricas y logs.
Validar estado de ECS y Auto Scaling.
Analizar CPU y memoria.
Revisar Aurora PostgreSQL.
Verificar dependencias externas.
Correlacionar cambios recientes.
