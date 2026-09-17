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
### 2.5.1.1. Candidate Context Discovery

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