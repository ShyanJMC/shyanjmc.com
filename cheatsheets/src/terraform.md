# Terraform

Es una herramienta de IaC (Infraestructure as Code).

Tiene conectividad dependiendo de los módulos que tenga instalados.

## Estructura

- Archivo principal;

> ./main.tf

- Carpeta con los módulos;

> ./terraform/modules

> ./modules

- Archivos con las variables

> ./variables.tf

- Proveedores, backend remoto y versión de terraform a usar;

> ./terraform.tf

## Comandos

- Iniciar workspace

> terraform init

El argumento "-upgrade" permite actualizar las versiones de los módulos.

- Validar configuración

> terraform validate

- Mostrar cambios antes de hacerlos

> terraform plan -out "[terraform_plan_file]"

- Mostrar cambios para destruir

> terraform plan -destroy -out "[terraform_plan_destroy_file]"

- Aplicar cambios

aplicar usando el main.tf

> terraform apply

aplicar usando el plan

> terraform apply "[terraform_plan_file]"

- Mostrar plan

> terraform show "[terraform_plan_file]"

- Destruir todos los recursos manejados por este workspace

> terraform destroy

## Archivos

- variables.tf

```json
variable "secret_key" {
  type        = string
  sensitive   = true
  description = "Secret key for hello module"
}

variable "region" {
  type = string
  sensitive = false
  description = "Region to rise resources"
}
```

- terraform.tfvars

```json
region = "us-east-1"
secret_key = "007_linuxrules"
```

- main.tf

```json
provider "aws" {
  region = var.region
}

provider "random" {}

provider "time" {}

data "aws_ami" "ubuntu" {
  most_recent = true

  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-bionic-18.04-amd64-server-*"]
  }

  filter {
    name   = "virtualization-type"
    values = ["hvm"]
  }

  owners = ["099720109477"] # Canonical
}

resource "random_pet" "instance" {
  length = 2
}

resource "aws_instance" "main" {
  count = 3

  ami           = data.aws_ami.ubuntu.id
  instance_type = "t2.micro"

  tags = {
    Name  = "${random_pet.instance.id}-${count.index}"
    Owner = "${var.project_name}-tutorial"
  }
}

resource "aws_s3_bucket" "example" {
  tags = {
    Name  = "Example Bucket"
    Owner = "${var.project_name}-tutorial"
  }
}
```

- terraform.tf
```json
terraform {
  required_version = "~> 1.6"
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "5.7.0"
    }
    random = {
      source  = "hashicorp/random"
      version = "3.5.1"
    }
  }
## ...
}
```
