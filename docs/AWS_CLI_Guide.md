# Guía de Comandos AWS CLI

**Autor:** Francisco Javier Escobar García  
**Versión:** Enero 2026 | AWS CLI v2  
**Referencia oficial:** https://docs.aws.amazon.com/cli/latest/reference/

---

## Tabla de Contenidos

1. [Configuración y Autenticación](#1-configuración-y-autenticación)
2. [Compute](#2-compute)
3. [Containers](#3-containers)
4. [Storage](#4-storage)
5. [Database](#5-database)
6. [Networking](#6-networking)
7. [Security & Identity](#7-security--identity)
8. [Messaging & Integration](#8-messaging--integration)
9. [Monitoring & Management](#9-monitoring--management)
10. [Infrastructure as Code](#10-infrastructure-as-code)
11. [AI/ML Services](#11-aiml-services)
12. [Cost Management](#12-cost-management)
13. [Tips y Mejores Prácticas](#13-tips-y-mejores-prácticas)

---

## 1. Configuración y Autenticación

### 1.1 AWS Configure

```bash
# Configuración interactiva inicial
aws configure

# Configurar un perfil específico
aws configure --profile mi-perfil

# Listar todos los perfiles configurados
aws configure list-profiles

# Ver configuración de un perfil
aws configure list --profile mi-perfil

# Establecer región para un perfil
aws configure set region us-east-1 --profile mi-perfil

# Obtener un valor específico de configuración
aws configure get aws_access_key_id --profile mi-perfil
```

### 1.2 STS (Security Token Service)

```bash
# Verificar identidad actual (usuario/rol/cuenta)
aws sts get-caller-identity

# Asumir un rol IAM
aws sts assume-role --role-arn arn:aws:iam::123456789012:role/MiRol --role-session-name mi-sesion

# Obtener token de sesión temporal
aws sts get-session-token --duration-seconds 3600

# Decodificar mensaje de error de autorización
aws sts decode-authorization-message --encoded-message <mensaje>
```

---

## 2. Compute

### 2.1 EC2 (Elastic Compute Cloud)

```bash
# Listar todas las instancias EC2
aws ec2 describe-instances

# Listar solo instancias en ejecución
aws ec2 describe-instances --filters "Name=instance-state-name,Values=running"

# Obtener ID, estado e IP pública de una instancia
aws ec2 describe-instances --instance-ids i-0123456789abcdef0 --query "Reservations[*].Instances[*].[InstanceId,State.Name,PublicIpAddress]"

# Iniciar una instancia
aws ec2 start-instances --instance-ids i-0123456789abcdef0

# Detener una instancia
aws ec2 stop-instances --instance-ids i-0123456789abcdef0

# Reiniciar una instancia
aws ec2 reboot-instances --instance-ids i-0123456789abcdef0

# Terminar una instancia
aws ec2 terminate-instances --instance-ids i-0123456789abcdef0

# Verificar salud y alcanzabilidad de instancias
aws ec2 describe-instance-status --include-all-instances

# Obtener logs del sistema para diagnosticar problemas de arranque
aws ec2 get-console-output --instance-id i-0123456789abcdef0

# Ejecutar con modo debug activado
aws ec2 describe-instances --debug
```

### 2.2 Security Groups

```bash
# Listar todos los Security Groups
aws ec2 describe-security-groups

# Describir un Security Group específico
aws ec2 describe-security-groups --group-ids sg-0123456789abcdef0

# Agregar regla de entrada (HTTPS)
aws ec2 authorize-security-group-ingress --group-id sg-0123456789abcdef0 --protocol tcp --port 443 --cidr 0.0.0.0/0

# Eliminar regla de entrada (SSH)
aws ec2 revoke-security-group-ingress --group-id sg-0123456789abcdef0 --protocol tcp --port 22 --cidr 0.0.0.0/0

# Crear un Security Group
aws ec2 create-security-group --group-name mi-sg --description "Mi Security Group" --vpc-id vpc-0123456789abcdef0
```

### 2.3 Auto Scaling

```bash
# Listar Auto Scaling Groups
aws autoscaling describe-auto-scaling-groups

# Listar instancias en Auto Scaling
aws autoscaling describe-auto-scaling-instances

# Cambiar capacidad deseada
aws autoscaling set-desired-capacity --auto-scaling-group-name mi-asg --desired-capacity 3

# Actualizar límites de capacidad
aws autoscaling update-auto-scaling-group --auto-scaling-group-name mi-asg --min-size 1 --max-size 5

# Ver actividades de escalado recientes
aws autoscaling describe-scaling-activities --auto-scaling-group-name mi-asg
```

### 2.4 Lambda

```bash
# Listar funciones Lambda
aws lambda list-functions

# Obtener detalles de una función
aws lambda get-function --function-name MiFuncion

# Crear una función Lambda
aws lambda create-function --function-name MiFuncion --runtime python3.12 --role arn:aws:iam::123456789012:role/MiRol --handler mi_funcion.handler --zip-file fileb://funcion.zip

# Actualizar código de una función
aws lambda update-function-code --function-name MiFuncion --zip-file fileb://nueva-funcion.zip

# Invocar función con payload
aws lambda invoke --function-name MiFuncion --payload '{"key": "value"}' output.json

# Ver logs en tiempo real de una función Lambda
aws logs tail /aws/lambda/MiFuncion --follow

# Listar triggers de una función
aws lambda list-event-source-mappings --function-name MiFuncion
```

---

## 3. Containers

### 3.1 ECS (Elastic Container Service)

```bash
# Listar clusters de ECS
aws ecs list-clusters

# Describir un cluster
aws ecs describe-clusters --clusters MiCluster

# Listar servicios en un cluster
aws ecs list-services --cluster MiCluster

# Describir un servicio
aws ecs describe-services --cluster MiCluster --services MiServicio

# Listar tareas en un cluster
aws ecs list-tasks --cluster MiCluster

# Describir una tarea específica
aws ecs describe-tasks --cluster MiCluster --tasks arn:aws:ecs:region:account:task/id

# Actualizar número de tareas de un servicio
aws ecs update-service --cluster MiCluster --service MiServicio --desired-count 3

# Crear un cluster de ECS
aws ecs create-cluster --cluster-name NuevoCluster

# Conectarse a un contenedor en ejecución (ECS Exec)
aws ecs execute-command --cluster MiCluster --task task-id --container mi-container --interactive --command "/bin/bash"
```

### 3.2 ECR (Elastic Container Registry)

```bash
# Listar repositorios
aws ecr describe-repositories

# Ver imágenes en un repositorio
aws ecr list-images --repository-name mi-repo

# Obtener detalles de una imagen específica
aws ecr describe-images --repository-name mi-repo --image-ids imageTag=latest

# Crear un repositorio ECR
aws ecr create-repository --repository-name mi-repo

# Autenticarse en ECR para Docker
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 123456789012.dkr.ecr.us-east-1.amazonaws.com

# Eliminar una imagen
aws ecr batch-delete-image --repository-name mi-repo --image-ids imageTag=v1.0
```

---

## 4. Storage

### 4.1 S3 (Simple Storage Service)

```bash
# Listar todos los buckets
aws s3 ls

# Listar objetos en un bucket
aws s3 ls s3://mi-bucket

# Listar recursivamente con tamaño legible y total
aws s3 ls s3://mi-bucket --recursive --human-readable --summarize

# Crear un nuevo bucket
aws s3 mb s3://mi-nuevo-bucket

# Eliminar un bucket y su contenido
aws s3 rb s3://mi-bucket --force

# Copiar archivo local a S3
aws s3 cp archivo.txt s3://mi-bucket/

# Descargar archivo de S3 a local
aws s3 cp s3://mi-bucket/archivo.txt ./

# Sincronizar directorio local con S3
aws s3 sync ./directorio s3://mi-bucket/

# Eliminar un objeto
aws s3 rm s3://mi-bucket/archivo.txt

# Generar URL pre-firmada (1 hora)
aws s3 presign s3://mi-bucket/archivo.txt --expires-in 3600

# Verificar estado de versionamiento
aws s3api get-bucket-versioning --bucket mi-bucket
```

### 4.2 EBS (Elastic Block Store)

```bash
# Listar todos los volúmenes EBS
aws ec2 describe-volumes

# Listar volúmenes en formato tabla
aws ec2 describe-volumes --query "Volumes[*].[VolumeId,Size,State,AvailabilityZone]" --output table

# Ver estado de los volúmenes
aws ec2 describe-volume-status

# Crear snapshot de un volumen
aws ec2 create-snapshot --volume-id vol-0123456789abcdef0 --description "Backup diario"

# Listar snapshots propios
aws ec2 describe-snapshots --owner-ids self

# Crear volumen de 100GB gp3
aws ec2 create-volume --availability-zone us-east-1a --size 100 --volume-type gp3
```

---

## 5. Database

### 5.1 RDS (Relational Database Service)

```bash
# Listar instancias RDS
aws rds describe-db-instances

# Ver estado y endpoint de una instancia
aws rds describe-db-instances --db-instance-identifier mi-db --query "DBInstances[0].[DBInstanceStatus,Endpoint.Address]"

# Iniciar una instancia RDS
aws rds start-db-instance --db-instance-identifier mi-db

# Detener una instancia RDS
aws rds stop-db-instance --db-instance-identifier mi-db

# Reiniciar una instancia RDS
aws rds reboot-db-instance --db-instance-identifier mi-db

# Crear snapshot manual
aws rds create-db-snapshot --db-instance-identifier mi-db --db-snapshot-identifier mi-snapshot

# Listar snapshots de una instancia
aws rds describe-db-snapshots --db-instance-identifier mi-db

# Descargar logs de error
aws rds download-db-log-file-portion --db-instance-identifier mi-db --log-file-name error/mysql-error.log --starting-token 0
```

### 5.2 DynamoDB

```bash
# Listar tablas de DynamoDB
aws dynamodb list-tables

# Describir una tabla
aws dynamodb describe-table --table-name MiTabla

# Escanear tabla (máx 10 items)
aws dynamodb scan --table-name MiTabla --max-items 10

# Obtener un item por clave
aws dynamodb get-item --table-name MiTabla --key '{"Id": {"S": "123"}}'

# Insertar un item
aws dynamodb put-item --table-name MiTabla --item '{"Id": {"S": "123"}, "Nombre": {"S": "Test"}}'

# Consultar por clave de partición
aws dynamodb query --table-name MiTabla --key-condition-expression "Id = :id" --expression-attribute-values '{":id": {"S": "123"}}'

# Eliminar un item
aws dynamodb delete-item --table-name MiTabla --key '{"Id": {"S": "123"}}'
```

---

## 6. Networking

### 6.1 VPC (Virtual Private Cloud)

```bash
# Listar VPCs
aws ec2 describe-vpcs

# Listar VPCs con nombre y CIDR
aws ec2 describe-vpcs --query "Vpcs[*].[VpcId,CidrBlock,Tags[?Key=='Name'].Value|[0]]" --output table

# Listar subnets
aws ec2 describe-subnets

# Listar subnets de una VPC específica
aws ec2 describe-subnets --filters "Name=vpc-id,Values=vpc-0123456789abcdef0"

# Listar tablas de rutas de una VPC
aws ec2 describe-route-tables --filters "Name=vpc-id,Values=vpc-0123456789abcdef0"

# Listar Internet Gateways
aws ec2 describe-internet-gateways

# Listar NAT Gateways
aws ec2 describe-nat-gateways

# Listar interfaces de red (ENIs)
aws ec2 describe-network-interfaces

# Listar NACLs de una VPC
aws ec2 describe-network-acls --filters "Name=vpc-id,Values=vpc-0123456789abcdef0"
```

### 6.2 ELB (Elastic Load Balancing)

```bash
# Listar Application/Network Load Balancers
aws elbv2 describe-load-balancers

# Listar Classic Load Balancers
aws elb describe-load-balancers

# Listar Target Groups
aws elbv2 describe-target-groups

# Ver salud de targets en un Target Group
aws elbv2 describe-target-health --target-group-arn arn:aws:elasticloadbalancing:region:account:targetgroup/mi-tg/123

# Listar listeners de un ALB
aws elbv2 describe-listeners --load-balancer-arn arn:aws:elasticloadbalancing:region:account:loadbalancer/app/mi-alb/123

# Ver salud de instancias en CLB
aws elb describe-instance-health --load-balancer-name mi-clb
```

### 6.3 Route 53

```bash
# Listar zonas hospedadas
aws route53 list-hosted-zones

# Listar registros DNS de una zona
aws route53 list-resource-record-sets --hosted-zone-id Z0123456789ABCDEFGHIJ

# Obtener detalles de una zona
aws route53 get-hosted-zone --id Z0123456789ABCDEFGHIJ

# Listar health checks
aws route53 list-health-checks

# Ver estado de un health check
aws route53 get-health-check-status --health-check-id check-id

# Crear/actualizar registros DNS desde archivo JSON
aws route53 change-resource-record-sets --hosted-zone-id Z0123456789ABCDEFGHIJ --change-batch file://cambios.json
```

### 6.4 CloudFront

```bash
# Listar distribuciones CloudFront
aws cloudfront list-distributions

# Ver detalles de una distribución
aws cloudfront get-distribution --id E1234567890ABC

# Invalidar caché completa
aws cloudfront create-invalidation --distribution-id E1234567890ABC --paths "/*"

# Invalidar paths específicos
aws cloudfront create-invalidation --distribution-id E1234567890ABC --paths "/images/*" "/css/*"

# Listar invalidaciones
aws cloudfront list-invalidations --distribution-id E1234567890ABC
```

---

## 7. Security & Identity

### 7.1 IAM (Identity and Access Management)

```bash
# Listar usuarios
aws iam list-users

# Listar roles
aws iam list-roles

# Listar grupos
aws iam list-groups

# Listar políticas personalizadas
aws iam list-policies --scope Local

# Obtener detalles de un usuario
aws iam get-user --user-name mi-usuario

# Listar políticas adjuntas a un usuario
aws iam list-attached-user-policies --user-name mi-usuario

# Listar políticas adjuntas a un rol
aws iam list-attached-role-policies --role-name mi-rol

# Crear un usuario
aws iam create-user --user-name nuevo-usuario

# Adjuntar política a usuario
aws iam attach-user-policy --user-name mi-usuario --policy-arn arn:aws:iam::aws:policy/ReadOnlyAccess

# Crear access key para usuario
aws iam create-access-key --user-name mi-usuario

# Listar access keys de un usuario
aws iam list-access-keys --user-name mi-usuario
```

### 7.2 Secrets Manager

```bash
# Listar secretos
aws secretsmanager list-secrets

# Obtener valor de un secreto
aws secretsmanager get-secret-value --secret-id mi-secreto

# Obtener solo el valor del secreto
aws secretsmanager get-secret-value --secret-id mi-secreto --query SecretString --output text

# Crear un secreto
aws secretsmanager create-secret --name mi-secreto --secret-string '{"user":"admin","pass":"123"}'

# Actualizar un secreto
aws secretsmanager update-secret --secret-id mi-secreto --secret-string '{"user":"admin","pass":"456"}'

# Rotar un secreto
aws secretsmanager rotate-secret --secret-id mi-secreto
```

### 7.3 CloudTrail

```bash
# Listar trails
aws cloudtrail describe-trails

# Ver estado de un trail
aws cloudtrail get-trail-status --name mi-trail

# Iniciar logging
aws cloudtrail start-logging --name mi-trail

# Detener logging
aws cloudtrail stop-logging --name mi-trail

# Buscar eventos de login en consola
aws cloudtrail lookup-events --lookup-attributes AttributeKey=EventName,AttributeValue=ConsoleLogin --max-results 10
```

---

## 8. Messaging & Integration

### 8.1 SNS (Simple Notification Service)

```bash
# Listar tópicos SNS
aws sns list-topics

# Ver suscriptores de un tópico
aws sns list-subscriptions-by-topic --topic-arn arn:aws:sns:region:account:mi-topico

# Crear un tópico
aws sns create-topic --name mi-topico

# Suscribir email a un tópico
aws sns subscribe --topic-arn arn:aws:sns:region:account:mi-topico --protocol email --notification-endpoint mi@email.com

# Publicar mensaje en un tópico
aws sns publish --topic-arn arn:aws:sns:region:account:mi-topico --message "Mensaje de prueba"

# Publicar mensaje JSON desde archivo
aws sns publish --topic-arn arn:aws:sns:region:account:mi-topico --message file://mensaje.json --message-structure json
```

### 8.2 SQS (Simple Queue Service)

```bash
# Listar colas
aws sqs list-queues

# Ver atributos de una cola
aws sqs get-queue-attributes --queue-url https://sqs.region.amazonaws.com/account/mi-cola --attribute-names All

# Crear una cola estándar
aws sqs create-queue --queue-name mi-cola

# Crear una cola FIFO
aws sqs create-queue --queue-name mi-cola.fifo --attributes FifoQueue=true

# Enviar mensaje
aws sqs send-message --queue-url https://sqs.region.amazonaws.com/account/mi-cola --message-body "Hola Mundo"

# Recibir hasta 5 mensajes
aws sqs receive-message --queue-url https://sqs.region.amazonaws.com/account/mi-cola --max-number-of-messages 5

# Eliminar mensaje procesado
aws sqs delete-message --queue-url https://sqs.region.amazonaws.com/account/mi-cola --receipt-handle <handle>

# Purgar todos los mensajes de una cola
aws sqs purge-queue --queue-url https://sqs.region.amazonaws.com/account/mi-cola
```

### 8.3 EventBridge

```bash
# Listar buses de eventos
aws events list-event-buses

# Listar reglas
aws events list-rules

# Describir una regla
aws events describe-rule --name mi-regla

# Listar targets de una regla
aws events list-targets-by-rule --rule mi-regla

# Enviar evento personalizado
aws events put-events --entries '[{"Source":"mi-app","DetailType":"test","Detail":"{}"}]'

# Habilitar una regla
aws events enable-rule --name mi-regla

# Deshabilitar una regla
aws events disable-rule --name mi-regla
```

### 8.4 API Gateway

```bash
# Listar REST APIs
aws apigateway get-rest-apis

# Listar HTTP/WebSocket APIs (v2)
aws apigatewayv2 get-apis

# Listar stages de una API
aws apigateway get-stages --rest-api-id abc123

# Listar deployments
aws apigateway get-deployments --rest-api-id abc123

# Crear deployment en stage
aws apigateway create-deployment --rest-api-id abc123 --stage-name prod

# Ver uso de un API key
aws apigateway get-usage --usage-plan-id plan123 --key-id key123 --start-date 2025-01-01 --end-date 2025-01-31
```

---

## 9. Monitoring & Management

### 9.1 CloudWatch

```bash
# Listar métricas de EC2
aws cloudwatch list-metrics --namespace AWS/EC2

# Listar alarmas
aws cloudwatch describe-alarms

# Listar solo alarmas en estado ALARM
aws cloudwatch describe-alarms --state-value ALARM

# Obtener estadísticas de CPU
aws cloudwatch get-metric-statistics --namespace AWS/EC2 --metric-name CPUUtilization --dimensions Name=InstanceId,Value=i-123 --start-time 2025-01-01T00:00:00Z --end-time 2025-01-02T00:00:00Z --period 3600 --statistics Average

# Crear alarma de CPU
aws cloudwatch put-metric-alarm --alarm-name cpu-alta --metric-name CPUUtilization --namespace AWS/EC2 --statistic Average --period 300 --threshold 80 --comparison-operator GreaterThanThreshold --dimensions Name=InstanceId,Value=i-123 --evaluation-periods 2 --alarm-actions arn:aws:sns:region:account:mi-topico

# Listar Log Groups
aws logs describe-log-groups

# Ver logs en tiempo real
aws logs tail /aws/lambda/MiFuncion --follow

# Filtrar logs por patrón
aws logs filter-log-events --log-group-name /aws/lambda/MiFuncion --filter-pattern "ERROR"
```

### 9.2 Systems Manager (SSM)

```bash
# Listar instancias administradas por SSM
aws ssm describe-instance-information

# Obtener parámetro (con descifrado)
aws ssm get-parameter --name /mi-app/config --with-decryption

# Obtener parámetros por path
aws ssm get-parameters-by-path --path /mi-app/ --recursive

# Crear parámetro
aws ssm put-parameter --name /mi-app/nuevo --value "valor" --type String

# Crear parámetro cifrado
aws ssm put-parameter --name /mi-app/secreto --value "valor" --type SecureString

# Iniciar sesión SSH vía SSM (Session Manager)
aws ssm start-session --target i-0123456789abcdef0

# Ejecutar comando remoto
aws ssm send-command --document-name "AWS-RunShellScript" --targets "Key=instanceids,Values=i-123" --parameters commands="echo hola"

# Listar comandos ejecutados
aws ssm list-commands
```

---

## 10. Infrastructure as Code

### 10.1 CloudFormation

```bash
# Listar stacks activos
aws cloudformation list-stacks --stack-status-filter CREATE_COMPLETE UPDATE_COMPLETE

# Describir un stack
aws cloudformation describe-stacks --stack-name MiStack

# Ver eventos de un stack
aws cloudformation describe-stack-events --stack-name MiStack

# Ver recursos de un stack
aws cloudformation describe-stack-resources --stack-name MiStack

# Validar sintaxis de template
aws cloudformation validate-template --template-body file://template.yaml

# Crear stack desde archivo
aws cloudformation create-stack --stack-name NuevoStack --template-body file://template.yaml --parameters ParameterKey=Env,ParameterValue=prod

# Actualizar un stack
aws cloudformation update-stack --stack-name MiStack --template-body file://template.yaml

# Eliminar un stack
aws cloudformation delete-stack --stack-name MiStack

# Obtener template de un stack existente
aws cloudformation get-template --stack-name MiStack
```

---

## 11. AI/ML Services

### 11.1 Bedrock (Generative AI)

```bash
# Listar modelos fundacionales disponibles
aws bedrock list-foundation-models

# Obtener detalles de un modelo
aws bedrock get-foundation-model --model-identifier anthropic.claude-3-sonnet-20240229-v1:0

# Invocar modelo (ejemplo básico)
aws bedrock-runtime invoke-model --model-id anthropic.claude-3-sonnet-20240229-v1:0 --content-type application/json --body '{"prompt": "Hola"}' output.json

# Listar modelos personalizados
aws bedrock list-custom-models

# Listar trabajos de personalización
aws bedrock list-model-customization-jobs
```

---

## 12. Cost Management

### 12.1 Cost Explorer

```bash
# Obtener costos del mes
aws ce get-cost-and-usage --time-period Start=2025-01-01,End=2025-01-31 --granularity MONTHLY --metrics BlendedCost

# Costos diarios agrupados por servicio
aws ce get-cost-and-usage --time-period Start=2025-01-01,End=2025-01-31 --granularity DAILY --metrics UnblendedCost --group-by Type=DIMENSION,Key=SERVICE

# Pronóstico de costos del próximo mes
aws ce get-cost-forecast --time-period Start=2025-02-01,End=2025-02-28 --metric BLENDED_COST --granularity MONTHLY

# Ver utilización de reservas
aws ce get-reservation-utilization --time-period Start=2025-01-01,End=2025-01-31

# Listar presupuestos configurados
aws budgets describe-budgets --account-id 123456789012
```

---

## 13. Tips y Mejores Prácticas

### Opciones Globales Útiles

| Opción | Descripción |
|--------|-------------|
| `--debug` | Activar modo debug para troubleshooting |
| `--profile nombre` | Usar un perfil específico de credenciales |
| `--region us-east-1` | Especificar región de AWS |
| `--output json\|table\|text\|yaml` | Cambiar formato de salida |
| `--query` | Filtrar resultados con JMESPath |
| `--dry-run` | Verificar permisos sin ejecutar (EC2) |
| `--no-paginate` | Desactivar paginación automática |

### Herramientas Complementarias

- **jq** — Procesador JSON de línea de comandos
- **aws help** — Documentación integrada (ej: `aws ec2 help`)
- **Tab completion** — Autocompletado (configurar con `aws_completer`)

### Verificación Inicial Recomendada

Antes de trabajar con AWS CLI, siempre verifica tu identidad y configuración:

```bash
# Verificar quién soy (cuenta, usuario/rol, ARN)
aws sts get-caller-identity

# Ver configuración activa actual
aws configure list
```

---

**Referencia Oficial:** https://docs.aws.amazon.com/cli/latest/reference/
