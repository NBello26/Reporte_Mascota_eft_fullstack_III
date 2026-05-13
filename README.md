# 🐾 Microservicio de Gestión de Mascotas

Este repositorio contiene el microservicio de **Mascotas**, desarrollado con Spring Boot. Es el responsable de gestionar toda la lógica de negocio relacionada con el registro, actualización, búsqueda y visualización de mascotas dentro del ecosistema. Se conecta a la base de datos central (SanosDB) para la persistencia de esta información.

## 🚀 Arquitectura y Prácticas DevOps

Como parte de una arquitectura nativa en la nube, este microservicio está diseñado para ser independiente, escalable y efímero. No requiere que los demás servicios conozcan su IP estática gracias a su integración con el Service Registry.

El flujo de despliegue está 100% automatizado mediante **GitHub Actions (CI/CD)**:
1. Compila el código Java y ejecuta pruebas.
2. Construye una imagen Docker empaquetando el artefacto `.jar`.
3. Sube la imagen a **Amazon Elastic Container Registry (ECR)**.
4. Despliega la aplicación en la instancia **EC2** correspondiente (Nodo Back 2) mediante **AWS Systems Manager (SSM)**.
5. Durante el despliegue, inyecta variables de entorno críticas (credenciales de DB, URL de Eureka, y su propia IP privada de EC2 para el auto-registro).

### 🌐 Ecosistema de Infraestructura en AWS
Este microservicio comparte recursos de cómputo en el segundo nodo de backend:

* **Nodo Web:** ApiGateway y Frontend
* **Nodo Back 1:** Eureka Server y BFF
* **Nodo Back 2:** **Microservicio de Mascotas** (Este repositorio) 📍 y Usuarios
* **Nodo Back 3:** Microservicios de Geolocalización y Notificaciones
* **Nodo Back 4:** Motor de Coincidencias
* **Base de Datos:** SanosDB (PostgreSQL)

## 🛠️ Tecnologías Principales

* **Framework:** Java 17 / Spring Boot 3
* **Persistencia:** Spring Data JPA / Hibernate
* **Cloud Native:** Spring Cloud Netflix Eureka Client
* **Contenedores:** Docker
* **CI/CD:** GitHub Actions
* **Infraestructura AWS:** EC2, ECR, SSM, IAM

## ⚙️ Descubrimiento y Redes

* **Conexión a BD:** Se comunica por la red privada de la VPC con el nodo de la base de datos (SanosDB) utilizando credenciales inyectadas por GitHub Secrets.
* **Auto-Registro (Eureka):** Al levantarse el contenedor, este servicio se registra automáticamente en el servidor Eureka bajo el nombre `MS-GESTION-MASCOTAS`. Esto permite que el API Gateway y el BFF enruten tráfico hacia él sin necesidad de conocer en qué IP o puerto específico se está ejecutando actualmente.

## 📦 Repositorios del Proyecto

Explora el resto de la infraestructura y microservicios de este ecosistema:

**Frontend y Puertas de Enlace**
* 🌐 [Frontend_eft_fullstack_III](https://github.com/NBello26/Frontend_eft_fullstack_III)
* 🚪 [ApiGateway_eft_fullstack_III](https://github.com/NBello26/ApiGateway_eft_fullstack_III)
* 🌉 [BFF_eft_fullstack_III](https://github.com/NBello26/BFF_eft_fullstack_III)

**Descubrimiento y Base de Datos**
* 🧭 [Eureka_eft_fullstack_III](https://github.com/NBello26/Eureka_eft_fullstack_III)
* 🗄️ [BD_eft_fullstack_III](https://github.com/NBello26/BD_eft_fullstack_III)

**Microservicios de Negocio**
* 🐾 [Reporte_Mascota_eft_fullstack_III](https://github.com/NBello26/Reporte_Mascota_eft_fullstack_III) *(Estás aquí)*
* 👤 [Usuarios_eft_fullstack_III](https://github.com/NBello26/Usuarios_eft_fullstack_III)
* 📍 [Geolocalizacion_eft_fullstack_III](https://github.com/NBello26/Geolocalizacion_eft_fullstack_III)
* 🔔 [Notificaciones_eft_fullstack_III](https://github.com/NBello26/Notificaciones_eft_fullstack_III)
* 🧩 [Coincidencias_eft_fullstack_III](https://github.com/NBello26/Coincidencias_eft_fullstack_III)

---
*Desarrollado como parte del proyecto final de integración de arquitectura DevOps.*
