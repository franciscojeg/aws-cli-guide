# 📚 Guía de Comandos AWS CLI

<p align="center">
  <img src="https://img.shields.io/badge/AWS-CLI%20v2-FF9900?style=for-the-badge&logo=amazon-aws&logoColor=white" alt="AWS CLI v2"/>
  <img src="https://img.shields.io/badge/Versión-Enero%202026-232F3E?style=for-the-badge" alt="Versión"/>
  <img src="https://img.shields.io/badge/Idioma-Español-red?style=for-the-badge" alt="Español"/>
  <img src="https://img.shields.io/github/license/your-username/aws-cli-guide?style=for-the-badge" alt="Licencia"/>
</p>

<p align="center">
  <b>Una guía completa de comandos esenciales de AWS CLI para debugging, monitoreo y administración.</b>
</p>

<p align="center">
  <a href="#-inicio-rápido">Inicio Rápido</a> •
  <a href="#-servicios-incluidos">Servicios</a> •
  <a href="#-descargar">Descargar</a> •
  <a href="#-contribuir">Contribuir</a> •
  <a href="./README.md">🇺🇸 English</a>
</p>

---

## 🎯 Acerca de

Esta guía recopila los comandos más importantes de AWS CLI organizados por servicio. Aunque normalmente se usa Infrastructure as Code (IaC) como Terraform o CloudFormation para aprovisionar y configurar servicios AWS, estos comandos son esenciales para:

- 🔍 **Debugging** - Resolver problemas en tiempo real
- 📊 **Monitoreo** - Verificar estado y salud de recursos
- 🧪 **Testing** - Validar configuraciones y permisos
- 🛠️ **Administración** - Tareas operacionales rápidas

## 🚀 Inicio Rápido

### Prerrequisitos

1. **Instalar AWS CLI v2**
   ```bash
   # macOS
   brew install awscli
   
   # Linux
   curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
   unzip awscliv2.zip
   sudo ./aws/install
   
   # Windows
   msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi
   ```

2. **Configurar credenciales**
   ```bash
   aws configure
   ```

3. **Verificar tu identidad**
   ```bash
   aws sts get-caller-identity
   ```

## 📋 Servicios Incluidos

| Categoría | Servicios |
|-----------|-----------|
| **Configuración** | AWS Configure, STS |
| **Compute** | EC2, Security Groups, Auto Scaling, Lambda |
| **Containers** | ECS, ECR |
| **Storage** | S3, EBS |
| **Database** | RDS, DynamoDB |
| **Networking** | VPC, ELB, Route 53, CloudFront |
| **Security** | IAM, Secrets Manager, CloudTrail |
| **Messaging** | SNS, SQS, EventBridge, API Gateway |
| **Monitoring** | CloudWatch, Systems Manager (SSM) |
| **IaC** | CloudFormation |
| **AI/ML** | Bedrock |
| **Costos** | Cost Explorer |

## 📥 Descargar

| Formato | Descripción | Enlace |
|---------|-------------|--------|
| 📄 **DOCX** | Documento completo formateado | [Descargar](./docs/Guia_AWS_CLI_Commands.docx) |
| 📖 **Markdown** | Leer en línea | [Ver](./docs/AWS_CLI_Guide.md) |

## 💡 Comandos Más Usados

### Verificar Identidad
```bash
aws sts get-caller-identity
```

### Listar Instancias EC2
```bash
aws ec2 describe-instances --query "Reservations[*].Instances[*].[InstanceId,State.Name,PublicIpAddress]" --output table
```

### Listar Buckets S3
```bash
aws s3 ls
```

### Ver Logs de CloudWatch en Tiempo Real
```bash
aws logs tail /aws/lambda/mi-funcion --follow
```

### Conectarse a EC2 vía Session Manager
```bash
aws ssm start-session --target i-0123456789abcdef0
```

## 🛠️ Tips Útiles

### Opciones Globales
| Opción | Descripción |
|--------|-------------|
| `--debug` | Activar modo debug para troubleshooting |
| `--profile nombre` | Usar un perfil específico de credenciales |
| `--region us-east-1` | Especificar región de AWS |
| `--output json\|table\|text\|yaml` | Cambiar formato de salida |
| `--query` | Filtrar resultados con JMESPath |
| `--dry-run` | Verificar permisos sin ejecutar (EC2) |

### Herramientas Complementarias
- **jq** - Procesador JSON de línea de comandos
- **aws-vault** - Gestión segura de credenciales
- **awslogs** - Visor de logs de CloudWatch

## 📁 Estructura del Repositorio

```
aws-cli-guide/
├── README.md           # Versión en inglés
├── README_ES.md        # Este archivo (Español)
├── LICENSE             # Licencia MIT
├── CONTRIBUTING.md     # Guía de contribución
└── docs/
    ├── Guia_AWS_CLI_Commands.docx    # Guía completa (DOCX)
    └── AWS_CLI_Guide.md              # Guía completa (Markdown)
```

## 🤝 Contribuir

¡Las contribuciones son bienvenidas! Por favor lee [CONTRIBUTING.md](./CONTRIBUTING.md) para conocer los detalles sobre cómo enviar pull requests.

### Formas de Contribuir
- 🐛 Reportar errores en comandos
- 💡 Sugerir nuevos comandos o servicios
- 🌐 Ayudar a traducir a otros idiomas
- 📝 Mejorar la documentación

## 📄 Licencia

Este proyecto está licenciado bajo la Licencia MIT - ver el archivo [LICENSE](./LICENSE) para más detalles.

## 👤 Autor

**Francisco Javier Escobar García**

- LinkedIn: [Conectar](https://linkedin.com/in/tu-perfil)
- GitHub: [@tu-usuario](https://github.com/tu-usuario)
- dev.to: [Artículos de AWS](https://dev.to/tu-usuario)

## ⭐ Muestra tu Apoyo

Si esta guía te fue útil, ¡considera darle una ⭐ en GitHub!

---

<p align="center">
  <b>Referencia Oficial de AWS CLI:</b> <a href="https://docs.aws.amazon.com/cli/latest/reference/">docs.aws.amazon.com/cli</a>
</p>
