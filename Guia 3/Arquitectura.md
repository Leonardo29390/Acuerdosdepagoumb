# Documento de Arquitectura - Sistema de Inscripción de Materias (UMB)

## 1. Contexto y Necesidad
El proyecto busca solucionar la problemática actual en la inscripción de materias para estudiantes con acuerdo de pago en la Universidad Manuela Beltrán. El proceso manual es lento, 
propenso a errores y afecta a estudiantes, docentes y administrativos. Se requiere un sistema eficiente, escalable y seguro que soporte alta concurrencia y permita mantenibilidad a futuro.

## 2. Descripción de la Arquitectura: Modelo de 3 Capas en la Nube
La arquitectura seleccionada es el **modelo de 3 capas (presentación, lógica de negocio y datos)** desplegado en la nube, extendiendo el modelo cliente-servidor tradicional con las ventajas de 
la computación en la nube.

### Capa de Presentación (Front-End)
- **Función:** Interfaz de usuario para estudiantes, coordinadores, área financiera y administradores.
- **Tecnologías:** HTML5, CSS3, JavaScript, React o Vue.js.
- **Características:** Interfaz responsiva, accesible y optimizada para completar solicitudes en menos de 5 minutos.

### Capa de Lógica de Negocio (Back-End)
- **Función:** Procesa solicitudes, ejecuta reglas de negocio (validaciones, aprobaciones), se comunica con la BD y retorna respuestas.
- **Tecnologías:** Node.js con Express, Python (Django/Flask), Java Spring Boot.
- **Características:** APIs RESTful o GraphQL, centraliza la lógica, consumible por múltiples clientes (web, móvil).

### Capa de Datos (Base de Datos)
- **Función:** Almacena información persistente: usuarios, materias, solicitudes, estados financieros, historial.
- **Tecnologías:** PostgreSQL, MySQL o MongoDB.
- **Despliegue en la nube:** Servicios administrados como Amazon RDS, Azure SQL Database o MongoDB Atlas.

## 3. Despliegue en la Nube
La infraestructura se alojará en un proveedor cloud (AWS, Azure, Google Cloud) para aprovechar:
- **Escalabilidad automática:** Aumento dinámico de recursos en períodos críticos de inscripción.
- **Alta disponibilidad:** Operación 24/7 con redundancia en múltiples zonas.
- **Seguridad:** Autenticación gestionada, cifrado y firewalls.
- **Mantenimiento simplificado:** Actualizaciones sin afectar disponibilidad.
- **Comunicación segura:** APIs sobre HTTPS.

## 4. Justificación de la Arquitectura
| Requerimiento | Cómo lo satisface la arquitectura |
| :--- | :--- |
| **RNF1, RNF2, RNF3 (Usabilidad)** | Capa de presentación independiente permite interfaces intuitivas y optimizadas para completar solicitudes rápidamente. |
| **RNF4, RNF5, RNF6 (Seguridad)** | Separación aísla datos sensibles. Autenticación y autorización en back-end con roles y cifrado en tránsito (HTTPS) y en reposo. |
| **RNF7, RNF8 (Rendimiento)** | Back-end escala horizontalmente en la nube para múltiples usuarios. Respuestas en < 3 segundos mediante optimización y balanceo de carga. |
| **RNF9 (Disponibilidad)** | Infraestructura cloud con SLAs de alta disponibilidad (99.9%) y replicación multi-región. |
| **RNF10 (Mantenibilidad)** | Separación de capas permite actualizar reglas de negocio sin afectar interfaz o BD. Despliegue continuo facilitado por la nube. |
| **RNF11, RNF12 (Notificaciones y seguimiento)** | Back-end se integra con servicios de notificaciones y logging (correo, SMS, AWS CloudWatch). |

Además, la arquitectura cumple con los principios de **separación de responsabilidades**:
- **Mantenibilidad:** Evolución independiente de cada capa.
- **Escalabilidad:** Soporte para múltiples clientes simultáneos.
- **Seguridad:** Datos sensibles nunca llegan al cliente.
- **Reutilización:** Back-end puede servir a futuras aplicaciones móviles o integraciones.

## 5. Diagrama de Arquitectura Propuesto
# Arquitectura del Sistema

[Clientes]  
&nbsp;&nbsp;&nbsp;&nbsp;| (HTTPS)  
&nbsp;&nbsp;&nbsp;&nbsp;v  
[Balanceador de carga (Cloud Load Balancer)]  
&nbsp;&nbsp;&nbsp;&nbsp;|  
&nbsp;&nbsp;&nbsp;&nbsp;v  
[Servidores de aplicación (Back-End)] <--> [Base de datos (RDS / Cloud SQL)]  
&nbsp;&nbsp;&nbsp;&nbsp;| (consultas)  
&nbsp;&nbsp;&nbsp;&nbsp;v  
[Servicios de caché (Redis)]  
&nbsp;&nbsp;&nbsp;&nbsp;|  
&nbsp;&nbsp;&nbsp;&nbsp;v  
[Servicios de notificaciones (SES / Push)]  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| (almacenamiento)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;v  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Almacenamiento de archivos (S3 / Blob Storage)]
**Componentes:**
- **Balanceador de carga:** Distribuye tráfico entre instancias del back-end.
- **Back-End:** Ejecuta lógica de negocio, validaciones y orquestación.
- **Base de datos:** Almacena datos estructurados.
- **Caché:** Mejora rendimiento en consultas frecuentes.
- **Almacenamiento de archivos:** Guarda documentos o evidencias.
- **Notificaciones:** Servicio externo para envío de correos/mensajes.

## 6. Conclusión
La arquitectura de 3 capas en la nube proporciona la base técnica para resolver los problemas actuales del proceso de inscripción. Permite automatizar flujos, reducir la carga manual, 
dar seguimiento en tiempo real y garantizar disponibilidad en momentos críticos. Al estar basada en estándares web y servicios cloud, asegura un sistema escalable, seguro y fácil de mantener, 
alineado con los objetivos del proyecto y las necesidades de todos los actores.
