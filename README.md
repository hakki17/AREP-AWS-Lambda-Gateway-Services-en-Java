# AWS Lambda & API Gateway - Tutorial Java

Tutorial básico de microservicios con Java utilizando AWS Lambda y AWS API Gateway.

**Autor**: María Paula Sánchez Macías

## Descripción

Este proyecto implementa un servicio REST simple que calcula el cuadrado de un número entero, demostrando cómo crear, desplegar y exponer funciones Lambda a través de API Gateway.

## Requisitos

- Java
- Maven
- NetBeans (o cualquier IDE Java)
- Cuenta de AWS (AWS Academy o cuenta regular)

## Video demostrativo

https://youtu.be/rz6SKZBVchc

## Arquitectura del Servicio

El servicio consta de tres componentes principales:

1. **Función Java**: Clase que implementa la lógica de negocio
2. **AWS Lambda**: Función serverless que ejecuta el código
3. **API Gateway**: Expone la función Lambda como endpoint REST

## Implementación

### 1. Clase Java - MathServices

<image src="img/MathServicesclass.png">

Clase simple que contiene el método estático `square`:


### 2. Configuración de AWS Lambda

- Crear función Lambda desde cero
- Runtime: Java 8
- Handler: `co.edu.escuelaing.services.MathServices::square`
- Role: LabRole (AWS Academy) o rol personalizado

**Prueba de la función:**

<image src="img/pruebaexitosa1.png">

<image src="img/pruebaexitosa2.png">

### 3. Configuración de API Gateway

<image src="img/apigatewayGET.png">

#### Pasos de configuración:

1. Crear nueva API REST (tipo regional)
2. Crear método GET
3. Integrar con función Lambda
4. Configurar parámetro `value` en Query String

#### Mapping Template

Configurar el template para pasar el parámetro:
```
$input.params("value")
```

### 4. Seguridad y Validación

<image src="img/SecurityUtilsclass.png">

<image src="img/Userclass.png">

<image src="img/Securitytestaws.png">

### 5. Estructura del Proyecto

<image src="img/tree.png">

### 6. Despliegue

Desplegar la API en un stage (Beta, Production, etc.)

**URL de ejemplo:**
```
https://24uiyf4bn6.execute-api.us-east-1.amazonaws.com/Beta?value=14
```

**Resultado esperado:**
```
196
```

![Pretty print](Pretty-print.png)

## Tipos de Datos Soportados

AWS Lambda con Java soporta:

- **Tipos primitivos**: String, int, Integer, etc.
- **Eventos predefinidos**: Clases de `aws-lambda-java-events`
- **POJOs personalizados**: AWS Lambda serializa/deserializa automáticamente JSON

## Mapping Templates

Las plantillas de mapeo permiten transformar:
- Mensajes de entrada a la función Lambda
- Mensajes de salida de la función Lambda

Documentación: [API Gateway Mapping Template Reference](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-mapping-template-reference.html)
