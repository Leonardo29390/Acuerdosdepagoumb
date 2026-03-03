\# Planificación del DOM  
\## Sistema de Inscripción para Estudiantes con Acuerdo de Pago - UMB  
<br/>\---  
<br/>\## Resumen  
<br/>Este documento presenta la planificación del Document Object Model (DOM) para el Sistema de Inscripción de la UMB dirigido a estudiantes con acuerdo de pago. Se define una estructura base común utilizando etiquetas semánticas de HTML5 que garantizan accesibilidad, mantenibilidad y optimización SEO. Asimismo, se detallan las vistas específicas según el rol del usuario (Estudiante, Coordinador Académico, Área Financiera y Administrador), estableciendo la jerarquía del DOM en cada caso.  
<br/>El documento también contempla el uso de atributos ARIA para mejorar la accesibilidad, así como la manipulación dinámica del DOM mediante JavaScript para actualizar información en tiempo real sin recargar la página. Finalmente, se incluyen consideraciones de usabilidad y accesibilidad basadas en buenas prácticas y estándares como WCAG, asegurando que el sistema sea inclusivo, eficiente y escalable.  
<br/>\---  
<br/>\## 1. Introducción al DOM en el contexto del proyecto  
<br/>El Document Object Model (DOM) es la representación estructurada de una página web que permite a los lenguajes de programación (como JavaScript) interactuar con el contenido, la estructura y el estilo de un documento HTML. En nuestro sistema de inscripción para estudiantes con acuerdo de pago, el DOM será la base sobre la cual se construirá la interfaz de usuario (capa de presentación). Una correcta planificación del DOM garantiza:  
<br/>\- \*\*Accesibilidad:\*\* lectores de pantalla y otras tecnologías asistivas pueden interpretar correctamente la información.  
\- \*\*Mantenibilidad:\*\* una estructura clara facilita modificaciones futuras.  
\- \*\*SEO:\*\* los motores de búsqueda pueden indexar mejor el contenido relevante.  
\- \*\*Interactividad:\*\* la manipulación dinámica del DOM permitirá actualizar estados, mostrar notificaciones y responder a las acciones del usuario sin recargar la página.  
<br/>\*\*Justificación:\*\*  
<br/>Elegimos trabajar con el DOM porque es la forma estándar en que los navegadores interpretan el HTML y nos permite hacer páginas interactivas sin tener que recargarlas constantemente. Además, al planificarlo bien desde el principio, nos aseguramos de que el código sea más fácil de entender y modificar más adelante, y también ayudamos a que personas con discapacidad puedan usar el sistema gracias a la accesibilidad.  
<br/>\---  
<br/>\## 2. Estructura general del DOM (base común)  
<br/>Todas las páginas del sistema compartirán una estructura base que garantice consistencia y usabilidad:  
<br/>\`\`\`html  
&lt;!DOCTYPE html&gt;  
&lt;html lang="es"&gt;  
&lt;head&gt;  
&lt;meta charset="UTF-8"&gt;  
&lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;  
&lt;title&gt;Sistema de Inscripción UMB&lt;/title&gt;  
&lt;!-- hojas de estilo, scripts, etc. --&gt;  
&lt;/head&gt;  
&lt;body&gt;  
<br/>&lt;header&gt;  
&lt;!-- Logo, nombre de la universidad, menú de usuario (foto, cerrar sesión) --&gt;  
&lt;/header&gt;  
<br/>&lt;nav&gt;  
&lt;!-- Menú de navegación principal según el rol --&gt;  
&lt;/nav&gt;  
<br/>&lt;main&gt;  
&lt;!-- Contenido específico de cada vista --&gt;  
&lt;/main&gt;  
<br/>&lt;aside&gt;  
&lt;!-- Panel de notificaciones o información complementaria --&gt;  
&lt;/aside&gt;  
<br/>&lt;footer&gt;  
&lt;!-- Información institucional, contacto, derechos --&gt;  
&lt;/footer&gt;  
<br/>&lt;/body&gt;  
&lt;/html&gt;

Esta estructura utiliza etiquetas semánticas de HTML5 para definir claramente cada región de la página, mejorando la legibilidad del código y la experiencia de usuarios con lectores de pantalla.

**Justificación:**

Decidimos usar esta estructura base porque es limpia y separa bien las partes comunes de todas las páginas (como el header y el footer) del contenido principal. Así los usuarios siempre saben dónde encontrar el menú o la información de contacto, y nosotros podemos reutilizar el mismo layout en todas las vistas sin repetir código.

## 3\. Vistas específicas y su jerarquía DOM

### 3.1 Vista del Estudiante

**Objetivo:** Permitir al estudiante consultar el estado de su solicitud, seleccionar materias y enviar la solicitud.

**Estructura DOM:**

&lt;header&gt;: contiene el logo de la UMB, el nombre del estudiante y un botón para cerrar sesión.

&lt;nav&gt;: enlaces a "Inicio", "Solicitar materias", "Historial de solicitudes", "Mi perfil".

&lt;main&gt;: sección principal dividida en:

- &lt;section class="estado-solicitud"&gt;: muestra el estado actual de la solicitud (pendiente, aprobada, rechazada) y mensajes relevantes.
- &lt;section class="seleccion-materias"&gt; (visible solo si puede solicitar):
  - &lt;h2&gt;: "Selecciona tus materias"
  - &lt;form id="form-solicitud"&gt;
  - &lt;fieldset&gt; agrupando materias por semestre o programa.
  - Cada materia con &lt;input type="checkbox"&gt;, &lt;label&gt; con nombre, horario y código.
  - Botón &lt;button type="submit"&gt;Enviar solicitud&lt;/button&gt;.
- &lt;section class="mensajes"&gt;: notificaciones automáticas sobre cambios en el estado.

&lt;aside&gt;: muestra información adicional como fechas importantes, créditos restantes, o publicidad institucional.

&lt;footer&gt;: contiene enlaces a políticas y contacto.

**Justificación:**

Para el estudiante, lo más importante es que pueda ver rápido su estado y luego seleccionar materias sin confusiones. Por eso separamos en secciones claras y usamos un formulario con checkboxes, que es fácil de entender. Además, el aside lo dejamos para información extra que no es prioritaria, pero puede ser útil, como fechas límite.

### 3.2 Vista del Coordinador Académico

**Objetivo:** Visualizar solicitudes pendientes, aprobar/rechazar y ajustar materias.

**Estructura DOM:**

&lt;header&gt; y &lt;nav&gt; similares, con opciones específicas: "Solicitudes pendientes", "Historial", "Reportes".

&lt;main&gt;:

- &lt;section class="solicitudes-pendientes"&gt;
  - &lt;h2&gt;: "Solicitudes por revisar"
  - &lt;ul&gt; o &lt;table&gt; con cada solicitud: datos del estudiante, materias seleccionadas, estado financiero.
  - Botones: "Aprobar", "Rechazar" (con campo para motivo), "Ajustar materias".
- &lt;section class="detalle-solicitud"&gt; que se despliega al seleccionar una solicitud.

&lt;aside&gt;: estadísticas rápidas (número de solicitudes pendientes).

&lt;footer&gt;.

**Interactividad:**  
Al hacer clic en "Ajustar materias", se desplegará un formulario dinámico que permite agregar o quitar materias; estos cambios se reflejarán en el DOM antes de enviar la actualización al servidor.

**Justificación:**

El coordinador necesita ver todas las solicitudes de un vistazo y poder actuar rápido. Por eso usamos una lista o tabla clara, y los botones de acción están a la mano. Además, el panel de detalles que se despliega evita recargar la página y hace más ágil la revisión.

### 3.3 Vista del Área Financiera

**Objetivo:** Validar acuerdos de pago y actualizar estado financiero.

**Estructura DOM:**

&lt;main&gt; contiene una tabla con estudiantes que tienen solicitudes pendientes de validación financiera.

Cada fila muestra: identificación, nombre, estado del acuerdo (activo/inactivo) y un botón "Validar" que actualiza el estado vía AJAX y modifica el DOM para reflejar la nueva condición.

**Justificación:**

Para el área financiera, lo más eficiente es una tabla donde puedan ver rápidamente qué estudiantes necesitan validación. El botón "Validar" actualiza todo sin recargar, ahorrando tiempo.

### 3.4 Vista del Administrador

**Objetivo:** Gestionar usuarios, roles, periodos y reglas de inscripción.

**Estructura DOM:**

Paneles con pestañas (usando &lt;nav&gt; interna) para cada función: Usuarios, Roles, Periodos, Reglas.

Formularios para crear/editar entradas, con validación en el lado del cliente que se refleja en el DOM (mensajes de error, resaltado de campos).

**Justificación:**

El administrador maneja muchas opciones diferentes, por eso organizamos todo en pestañas para no saturar la pantalla. Los formularios con validación en cliente evitan errores antes de enviar al servidor, y los mensajes de error aparecen justo al lado del campo, lo cual es más claro.

## 4\. Uso de etiquetas semánticas y su impacto en el DOM

| **Etiqueta** | **Uso específico** |
| --- | --- |
| &lt;header&gt; | Cabecera de página y también cabeceras de secciones dentro de &lt;article&gt; o &lt;section&gt;. |
| &lt;nav&gt; | Menús de navegación principal y secundaria. |
| &lt;main&gt; | Contenido único de cada página. |
| &lt;article&gt; | Contenido autocontenido, como una solicitud individual. |
| &lt;section&gt; | Agrupación temática de partes de la página. |
| &lt;aside&gt; | Información complementaria. |
| &lt;footer&gt; | Información de contacto y legal. |

Además, se utilizarán atributos ARIA para mejorar la accesibilidad:

- role="alert" en mensajes de notificación.
- aria-labelledby para asociar secciones con sus títulos.

**Justificación:**

Las etiquetas semánticas organizan mejor el código y ayudan a motores de búsqueda y lectores de pantalla a interpretar correctamente la estructura del documento.

## 5\. Manipulación dinámica del DOM

Se utilizará JavaScript para:

- Actualizar el estado de la solicitud sin recargar la página.
- Mostrar notificaciones en tiempo real.
- Validar formularios en cliente.
- Cargar dinámicamente horarios al seleccionar una materia.

Las operaciones se realizarán mediante querySelector, modificación de atributos y creación dinámica de nodos.

**Justificación:**

La manipulación dinámica del DOM permite que el sistema sea rápido, moderno y eficiente, mejorando significativamente la experiencia del usuario.

## 6\. Consideraciones de accesibilidad y usabilidad

- Jerarquía adecuada de &lt;h1&gt; a &lt;h6&gt;.
- Uso de atributo alt en imágenes.
- Cumplimiento de pautas WCAG.
- Navegación por teclado con foco visible.

**Justificación:**

Se busca garantizar inclusión y accesibilidad para toda la comunidad universitaria.

## 7\. Conclusión

La planificación del DOM en este proyecto garantiza que la interfaz sea accesible, mantenible y escalable. La estructura semántica y la manipulación dinámica permiten una experiencia de usuario fluida y eficiente, alineada con los requerimientos del sistema. Este documento servirá como guía para los desarrolladores front-end durante la implementación.
