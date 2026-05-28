# inventory-sync
# Inventory Sync Service 📦🔄

Este proyecto es una solución backend basada en una arquitectura de microservicios diseñada para automatizar la sincronización de inventarios, stock y catálogos entre un proveedor mayorista (`supplier-api`) y una tienda online o comercio electrónico (`store-api`). 

El objetivo principal es eliminar los procesos manuales y los errores humanos, garantizando que el stock de la tienda se actualice en tiempo real o de forma programada mediante el consumo de APIs REST.

## 🚀 Características Clave

* **Arquitectura de Microservicios:** Dos servicios totalmente desacoplados e independientes que se comunican de forma eficiente mediante peticiones HTTP REST.
* **Sincronización Automatizada (Scheduler):** El módulo de la tienda incluye tareas programadas nativas de Spring que consultan de forma periódica los endpoints del proveedor para actualizar la base de datos local.
* **Validación de Datos Robusta:** Implementación de reglas de negocio estrictas mediante `Spring Boot Starter Validation` para asegurar la integridad de los datos de inventario recibidos.
* **Entorno Contenerizado:** Configuración lista para producción mediante **Docker** y **Docker Compose**, lo que permite levantar toda la infraestructura (servicios + bases de datos) con un único comando.

## 🛠️ Stack Tecnológico

* **Backend:** Java, Spring Boot (Spring Web, Spring Data JPA, Spring Boot Scheduler)
* **Gestión de Dependencias:** Maven
* **Base de Datos:** PostgreSQL / MySQL (Configurada en contenedores independientes)
* **Herramientas de Desarrollo:** Lombok (Código limpio), Spring Boot DevTools, Postman (Testing de endpoints)
* **Despliegue e Infraestructura:** Docker, Docker Compose

## 📁 Estructura del Proyecto

```text
inventory-sync/
├── supplier-api/                  # Servicio del proveedor (Expone el catálogo y stock)
│   └── src/main/java/com/supplier/
│       ├── controller/            # Endpoints REST expuestos
│       ├── service/               # Lógica de negocio e integración
│       ├── repository/            # Capa de acceso a datos (JPA Repositories)
│       └── model/                 # Entidades de la base de datos del proveedor
│
├── store-api/                     # Servicio de la tienda (Consume datos y sincroniza)
│   └── src/main/java/com/store/
│       ├── controller/            # Endpoints de gestión interna de la tienda
│       ├── scheduler/             # Tareas programadas de sincronización automática
│       └── service/               # Lógica de procesamiento y actualización de stock
│
└── docker-compose.yml             # Orquestación de los microservicios y bases de datos
