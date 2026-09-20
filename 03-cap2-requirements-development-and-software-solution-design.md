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
### 2.5.1.2. Domain Message Flows Modeling
### 2.5.1.3. Bounded Context Canvases
## 2.5.2. Context Mapping
## 2.5.3. Software Architecture
### 2.5.3.1. Software Architecture Context Level Diagrams
### 2.5.3.2. Software Architecture Container Level Diagrams
### 2.5.3.3. Software Architecture Deployment Diagrams
## 2.6. Tactical-Level Domain-Driven Design
### 2.6.1. Bounded Context: IAM

El bounded context **IAM (Identity & Access Management)** corresponde a un *Generic Domain* dentro de Rutana, encargado de la autenticación, la gestión de identidad de los usuarios y la administración de invitaciones a organizaciones. A continuación se detallan los términos clave de su lenguaje ubicuo:

| Término | Definición |
|:----|:----|
| **User** | Representa la identidad de un usuario dentro del sistema, incluyendo sus credenciales y su rol. |
| **Profile** | Contiene los datos personales asociados a un usuario (nombre, teléfono, avatar). |
| **Invitation** | Representa la invitación enviada a un correo electrónico para unirse a una organización con un rol asignado. |
| **Role** | Define el conjunto de permisos que posee un usuario dentro de una organización. |

<br>

#### 2.6.1.1. Domain Layer

En esta capa se modelan las clases de categoría como **Entities**, **Value Objects**, **Aggregates**, **Factories** y **Domain Services**, o abstracciones representadas por interfaces como en el caso de los **Repositories**.

- **Aggregate Root:** `User` — encapsula la identidad, credenciales y estado del usuario, y actúa como raíz de consistencia junto con `Profile`.
- **Entities:** `Profile`, `Invitation`.
- **Value Objects:** `Email`, `Role`.
- **Domain Services:** `AuthenticationService` — valida credenciales y aplica las políticas de autorización.
- **Factories:** `UserFactory` — encapsula la creación de un `User` válido a partir de datos de registro.
- **Repositories (interfaces):** `UserRepository`, `InvitationRepository`.

<br>

#### 2.6.1.2. Interface Layer

En esta sección se introduce y presenta las clases que forman parte de la Interface/Presentation Layer, como clases del tipo **Controllers** o **Consumers**.

- **Controllers:**
  - `AuthController` — expone los endpoints de inicio de sesión y registro.
  - `UserController` — expone las operaciones sobre el perfil del usuario.
  - `InvitationController` — expone las operaciones de invitación a una organización (crear, aceptar, cancelar).

<br>