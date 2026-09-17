# Capítulo II: Requirements Development and Software Solution Design
## 2.1. Competidores
### 2.1.1. Análisis competitivo
### 2.1.2. Estrategias y tácticas frente a competidores
## 2.2. Entrevistas
### 2.2.1. Diseño de entrevistas
### 2.2.2. Registro de entrevistas
### 2.2.3. Análisis de entrevistas
## 2.3. Needfinding
### 2.3.1. User Personas
### 2.3.2. User Task Matrix
### 2.3.3. User Journey Mapping
### 2.3.4. Empathy Mapping
### 2.3.5. Big Picture EventStorming
### 2.3.6. Ubiquitous Language
## 2.4. Requirements specification
### 2.4.1. User Stories
### 2.4.2. Impact Mapping
### 2.4.3. Product Backlog
## 2.5. Strategic-Level Domain-Driven Design
### 2.5.1. EventStorming

### 5.2.5.1. Candidate Context Discovery

Se aplicaron las tres estrategias indicadas en el enunciado para identificar los bounded contexts a partir del EventStorm de Rutana.

#### 3.1 Estrategia: Start-with-Value

Se identificaron las partes del dominio con mayor valor para el negocio (core). El sistema tiene como propósito principal la planificación y ejecución de rutas de distribución, gestionando flota, clientes y ubicaciones asociadas.

| Módulo | Valor de Negocio | Tipo de Dominio |
|:----|:----|:----|
| Planning | Creación, publicación y ejecución de rutas — núcleo del sistema | Core Domain |
| Fleet | Registro y disponibilidad de vehículos para las rutas | Core Domain |
| CRM | Gestión de clientes y ubicaciones de entrega | Core Domain |
| Suscriptions | Habilita el acceso a la plataforma según plan contratado | Supporting Domain |
| IAM | Autenticación, organizaciones y gestión de sesiones | Generic Domain |



#### 3.2 Estrategia: Start-with-Simple

Se descompuso el timeline del EventStorm en steps secuenciales para identificar modelos simples con propósito claro. Cada módulo tiene actores y flujos definidos, lo que permite establecer límites claros entre contextos.

| Contexto | Actores Involucrados | Flujo Principal |
|:----|:----|:----|
| IAM | Usuario, Administrador | Registrar cuenta → Iniciar sesión → Crear organización → Invitar usuario |
| Suscriptions | Administrador | Crear organización → Crear suscripción → Realizar pago → Suscripción activada |
| Fleet | Administrador, Despachador | Registrar vehículo → Habilitar vehículo → Actualizar estado operacional |
| CRM | Administrador, Despachador | Registrar cliente → Registrar ubicación → Actualizar posición de ubicación |
| Planning | Despachador | Crear borrador de ruta → Agregar ubicaciones → Asignar vehículo → Publicar ruta → Iniciar ruta → Completar ruta |


#### 3.3 Estrategia: Look-for-Pivotal-Events

Se identificaron los eventos clave del negocio que indican cruces entre diferentes partes del proceso. Estos eventos actúan como fronteras naturales entre bounded contexts.

| Pivotal Event | Contexto Origen | Contexto Destino |
|:----|:----|:----|
| Organization Created | IAM | Suscriptions (creación de suscripción) |
| Subscription Activated | Suscriptions | CRM, Fleet, Planning (habilita uso de la plataforma) |
| Vehicle Registered | Fleet | Planning (Vehicle Assigned to Route) |
| Client Registered | CRM | Planning (asociación de ubicaciones a rutas) |
| Location Created | CRM | Planning (Location Added to Route) |
| Route Published | Planning | Fleet (Dispatcher/Vehicle Assigned) |
| Route Started | Planning | CRM (Location Completed en tiempo real) |


Con estas estrategias pudimos identificar los bounded contexts que obtuvimos en el Event Storming: **IAM**, **Suscriptions**, **Fleet**, **CRM** y **Planning**.

### 2.5.1.2. Domain Message Flows Modeling

Para el desarrollo del Message Flow Modeling utilizamos la técnica de **Domain Storytelling**, un modelado colaborativo en el que los expertos de dominio narran su trabajo. El modelador escucha y registra estas historias usando un lenguaje pictográfico que combina: **Actores** (personas o sistemas de software) • **Objetos de trabajo** (documentos, datos, mensajes) • **Actividades** (flechas numeradas que indican el flujo secuencial) • **Anotaciones** (escenarios alternativos o condiciones de error).

Para cada flujo se identificaron: el actor iniciador, los bounded contexts involucrados, la secuencia de mensajes intercambiados y los escenarios alternativos.

<br>

#### DS-01: Administrador registra su organización y activa una suscripción

**Historia:** El administrador se registra en el sistema, crea una organización y contrata una suscripción. El sistema procesa el pago y activa el acceso a la plataforma.

**DS-01: Administrador registra su organización y activa una suscripción**
*Bounded Contexts: IAM · Suscriptions*

![DS-01 - Registro de organización y activación de suscripción](assets/images/readme/ds-01-registro-organizacion-suscripcion.png)

**Bounded Contexts Involucrados:**
1. IAM — registra al usuario y crea la organización
2. Suscriptions — gestiona el plan, el pago y la activación del acceso

**Flujo Principal:**

|#|Actor|Mensaje / Acción|Destino|Resultado|
|:--:|:----|:----|:----|:----|
|1|Administrador|Se registra en el sistema|IAM|Usuario registrado|
|2|Administrador|Crea una organización|IAM|Organización creada|
|3|IAM|Notifica creación al módulo de suscripciones|Suscriptions|Organización disponible para suscripción|
|4|Administrador|Crea una suscripción y realiza el pago|Suscriptions|Suscripción creada|
|5|Suscriptions|Procesa el pago mediante pasarela de pago|Suscriptions|Pago exitoso|
|6|Suscriptions|Activa la suscripción|Suscriptions|Suscripción activada|

**Escenarios Alternativos:**

|Escenario Alternativo|Respuesta del Sistema|
|:----|:----|
|Registro de usuario fallido|IAM rechaza el registro → Muestra error de validación|
|Pago rechazado|Suscriptions no activa la suscripción → Notifica error de pago|
|Suscripción vencida|Suscriptions marca la suscripción como expirada → Restringe acceso a módulos|

<br>

#### DS-02: Despachador registra un cliente y su ubicación de entrega

**Historia:** El despachador registra un nuevo cliente en el sistema y, a continuación, registra la ubicación asociada a ese cliente para futuras entregas.

**DS-02: Despachador registra un cliente y su ubicación**
*Bounded Contexts: CRM*

![DS-02 - Registro de cliente y ubicación](assets/images/readme/ds-02-registro-cliente-ubicacion.png)

**Bounded Contexts Involucrados:**
1. IAM — autentica al despachador
2. CRM — gestiona el registro del cliente y sus ubicaciones

**Flujo Principal:**

|#|Actor|Mensaje / Acción|Destino|Resultado|
|:--:|:----|:----|:----|:----|
|1|Despachador|Inicia sesión en el sistema|IAM|Sesión iniciada|
|2|Despachador|Registra un nuevo cliente|CRM|Cliente registrado|
|3|Despachador|Registra la ubicación del cliente|CRM|Ubicación creada|
|4|CRM|Consulta coordenadas mediante Google Maps API|Google Maps API|Ubicación geolocalizada|
|5|CRM|Habilita la ubicación para su uso en rutas|CRM|Ubicación habilitada|

**Escenarios Alternativos:**

|Escenario Alternativo|Respuesta del Sistema|
|:----|:----|
|Datos de cliente incompletos|CRM rechaza el registro → Muestra error de validación|
|Dirección no encontrada en Google Maps|CRM marca la creación de ubicación como fallida → Solicita corrección manual|
|Cliente desactivado previamente|CRM impide registrar nuevas ubicaciones para ese cliente|

<br>

#### DS-03: Despachador planifica y publica una ruta con vehículo asignado

**Historia:** El despachador crea un borrador de ruta, agrega las ubicaciones que debe visitar, asigna un vehículo disponible y publica la ruta para su ejecución.

**DS-03: Despachador planifica y publica una ruta**
*Bounded Contexts: Planning · Fleet · CRM*

![DS-03 - Planificación y publicación de ruta](assets/images/readme/ds-03-planificacion-publicacion-ruta.png)

**Bounded Contexts Involucrados:**
1. Planning — gestiona el borrador, las ubicaciones y la publicación de la ruta
2. CRM — provee las ubicaciones disponibles del cliente
3. Fleet — provee los vehículos disponibles para la asignación

**Flujo Principal:**

|#|Actor|Mensaje / Acción|Destino|Resultado|
|:--:|:----|:----|:----|:----|
|1|Despachador|Crea un borrador de ruta|Planning|Borrador de ruta creado|
|2|Despachador|Consulta ubicaciones registradas del cliente|CRM|Ubicaciones obtenidas|
|3|Despachador|Agrega ubicaciones al borrador de ruta|Planning|Ubicación agregada a la ruta|
|4|Despachador|Consulta vehículos disponibles|Fleet|Vehículos obtenidos|
|5|Despachador|Asigna un vehículo a la ruta|Planning|Vehículo asignado a la ruta|
|6|Despachador|Publica la ruta|Planning|Ruta publicada|

**Escenarios Alternativos:**

|Escenario Alternativo|Respuesta del Sistema|
|:----|:----|
|Vehículo no disponible|Planning notifica asignación fallida → Solicita elegir otro vehículo|
|Ubicación eliminada del borrador|Planning remueve la ubicación de la ruta y recalcula el recorrido|
|Publicación fallida por datos incompletos|Planning rechaza la publicación → Indica campos pendientes|

<br>

#### DS-04: Conductor ejecuta la ruta y completa las entregas

**Historia:** El despachador inicia la ejecución de la ruta publicada y el sistema va marcando cada ubicación como completada conforme se realizan las entregas, hasta finalizar la ruta.

**DS-04: Ejecución de ruta y completado de entregas**
*Bounded Contexts: Planning · CRM*

![DS-04 - Ejecución de ruta y completado de entregas](assets/images/readme/ds-04-ejecucion-ruta-entregas.png)

**Bounded Contexts Involucrados:**
1. Planning — gestiona el inicio, avance y finalización de la ruta
2. CRM — refleja el estado de las ubicaciones visitadas

**Flujo Principal:**

|#|Actor|Mensaje / Acción|Destino|Resultado|
|:--:|:----|:----|:----|:----|
|1|Despachador|Inicia la ruta publicada|Planning|Ruta iniciada|
|2|Planning|Marca la primera ubicación en tránsito|Planning|Ubicación en curso|
|3|Despachador|Confirma la entrega en la ubicación|Planning|Ubicación completada|
|4|Planning|Actualiza el estado de la ubicación en CRM|CRM|Estado de ubicación sincronizado|
|5|Planning|Repite el ciclo para cada ubicación de la ruta|Planning|Todas las ubicaciones procesadas|
|6|Planning|Finaliza la ruta|Planning|Ruta completada|

**Escenarios Alternativos:**

|Escenario Alternativo|Respuesta del Sistema|
|:----|:----|
|Cliente rechaza la entrega|Planning marca la ubicación como rechazada → Registra el motivo|
|Pérdida de conexión durante la ruta|Planning almacena los cambios localmente → Sincroniza al recuperar señal|
|Cancelación de ruta en curso|Planning marca la ruta como cancelada → Libera el vehículo asignado|

<br>

Con estas historias de dominio se evidencia cómo colaboran los bounded contexts **IAM**, **Suscriptions**, **CRM**, **Fleet** y **Planning** para resolver los principales casos de uso del negocio en Rutana.


### 2.5.1.3. Bounded Context Canvases
## 2.5.2. Context Mapping
## 2.5.3. Software Architecture
### 2.5.3.1. Software Architecture Context Level Diagrams
### 2.5.3.2. Software Architecture Container Level Diagrams
### 2.5.3.3. Software Architecture Deployment Diagrams
## 2.6. Tactical-Level Domain-Driven Design
### 2.6.x. Bounded Context: 
### 2.6.x.1. Domain Layer
### 2.6.x.2. Interface Layer
### 2.6.x.3. Application Layer
### 2.6.x.4 Infrastructure Layer
### 2.6.x.5. Bounded Context Software Architecture Component Level Diagrams
### 2.6.x.6. Bounded Context Software Architecture Code Level Diagrams
### 2.6.x.6.1. Bounded Context Domain Layer Class Diagrams
### 2.6.x.6.2. Bounded Context Database Design Diagram