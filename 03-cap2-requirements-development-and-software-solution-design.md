# Capítulo II: Requirements Development and Software Solution Design
## 2.1. Competidores
### 2.1.1. Análisis competitivo
<table style="width:100%; border-collapse:collapse; table-layout:fixed;" border="1" align="center">
  <!-- Título principal -->
  <tr>
    <th colspan="6" align="center">Competitive Analysis Landscape</th>
  </tr>
  <!-- Justificación -->
  <tr>
    <td rowspan="2" align="center"><b>¿Por qué llevar a cabo este análisis?</b></td>
    <td colspan="5" align="center">
      Identificar fortalezas, debilidades y estrategias de los principales competidores en logística de última milla (SimpliRoute, Beetrack, FarEye) para posicionar nuestra aplicación web.
    </td>
  </tr>
  <tr>
    <td colspan="5">
      <b>Objetivo:</b> Determinar cómo diferenciar nuestro producto frente a competidores consolidados en LATAM y globales. <br> 
    </td>
  </tr>
  <!-- Encabezados con logos -->
  <tr>
    <th colspan="2" style="width:20%">(En la cabecera colocar por cada competidor nombre y logo)</th>
    <th style="width:20%">
      <img src="./assets/images/Cap 2/Logo_rutana.png" alt="Rutana" width="100" height="100">
    </th>
    <th style="width:20%">
      <img src="./assets/images/Cap 2/Logo_simpliroute.png" alt="SimpliRoute" width="100" height="100">
    </th>
    <th style="width:20%">
      <img src="./assets/images/Cap 2/Logo_beetrack.png" alt="Beetrack" width="100" height="100">
    </th>   
    <th style="width:20%">
      <img src="./assets/images/Cap 2/Logo_fareye.png" alt="FarEye" width="100" height="100">
    </th>
  </tr>
  <!-- PERFIL -->
  <tr>
    <td rowspan="2" align="center"><b>Perfil</b></td>
    <td><b>Overview</b></td>
    <td> Solución tecnológica desarrollada para el mercado peruano que fusiona IoT y GPS para garantizar el seguimiento en vivo, la mejora de rutas y la supervisión de mercancías en tránsito. Está diseñada específicamente para mitigar los retos locales de transporte, tales como la congestión vehicular, los cierres de vías y las variaciones climatológicas. </td>
    <td> Plataforma chilena con fuerte presencia en LATAM; optimización de rutas y seguimiento en tiempo real. </td>
    <td> Fundada en Chile, adquirida por DispatchTrack; fuerte en trazabilidad de última milla. </td>
    <td> Empresa multinacional de origen indio especializada en orquestación de entregas, visibilidad de envíos y gestión inteligente de devoluciones. </td>
  </tr>
  <tr>
    <td><b>Ventaja competitiva:<br>¿Qué valor ofrece a los clientes?</b></td>
    <td> Ofrece en una sola solución: seguimiento en vivo, validación automatizada de pedidos y alertas inteligentes. Está pensada para pymes peruanas, ayudándolas a reducir errores de entrega, evitar pérdidas y mejorar la puntualidad. </td>
    <td> Reducción de costos logísticos hasta 30% con algoritmos de optimización. </td>
    <td> Experiencia de usuario robusta y alta penetración en empresas medianas/grandes de LATAM. </td>
    <td> Escalabilidad global y capacidad de integración con grandes retailers y 3PL. </td>
  </tr>
  <!-- PERFIL DE MARKETING -->
  <tr>
    <td rowspan="2" align="center"><b>Perfil de Marketing</b></td>
    <td><b>Mercado objetivo</b></td>
    <td> Pequeñas y medianas empresas de transporte y distribución en Perú, con foco inicial en Lima y ciudades con alta informalidad logística como las empresas de provincia también.</td>
    <td> Pymes y grandes empresas de distribución en LATAM. </td>
    <td> Retail, consumo masivo y distribución en varios países de LATAM. </td>
    <td> Retailers, e-commerce y logística global (Asia, Europa, LATAM). </td>
  </tr>
  <tr>
    <td><b>Estrategias de marketing</b></td>
    <td> Evidenciar beneficios cuantitativos (menos errores, más puntualidad) mediante pilotos locales, campañas digitales y casos de éxito adaptados a la realidad peruana.</td>
    <td> Casos de éxito locales, métricas de reducción de costos y demos personalizadas. </td>
    <td> Branding fuerte en trazabilidad y seguridad de entregas; foco en confiabilidad. </td>
    <td> Posicionamiento como solución integral global; alianzas con grandes corporativos. </td>
  </tr>
  <!-- PERFIL DE PRODUCTO -->
  <tr>
    <td rowspan="3" align="center"><b>Perfil de Producto</b></td>
    <td><b>Productos & Servicios</b></td>
    <td> Incluye monitoreo IoT en tiempo real, registro automático de pedidos, panel de control para administradores y alertas de desvíos o incidencias.</td>
    <td> Optimización de rutas, seguimiento en vivo, gestión de flota y analítica. </td>
    <td> PlannerPro (rutas), LastMile (seguimiento), notificaciones y prueba de entrega. </td>
    <td> Administración total de la cadena de distribución, control de logística inversa y trazabilidad instantánea de los envíos. </td>
  </tr>
  <tr>
    <td><b>Precios & Costos</b></td>
    <td> Planes de suscripción flexible y escalonada (básico, estándar y corporativo) adaptados al ecosistema peruano. Permiten iniciar operaciones con un presupuesto reducido y expandir las capacidades conforme la empresa crece. </td> 
    <td> Modelo SaaS flexible según volumen de entregas. </td>
    <td> Suscripción mensual adaptada al tamaño de la operación. </td>
    <td> Tarifas empresariales escalables para operaciones globales. </td>
  </tr>
  <tr>
    <td><b>Canales de distribución<br>(Web y/o Móvil)</b></td>
    <td> El sistema será accesible a través de plataforma web para administradores y conductores, garantizando sincronización en tiempo real entre ambos segmentos. </td>
    <td> Web y app móvil para conductores y administradores. </td>
    <td> Web, app móvil y APIs de integración. </td>
    <td> Plataforma web, apps móviles, integraciones con ERP/CRM. </td>
  </tr>
  <!-- SWOT -->
  <tr>
    <td rowspan="4" align="center"><b>Análisis SWOT</b></td>
    <td><b>Fortalezas</b></td>
    <td> Integración de IoT y validaciones automatizadas que ofrecen una trazabilidad superior a competidores regionales. </td>
    <td> Alta adopción en LATAM; soporte local. </td>
    <td> Reconocimiento de marca y respaldo de DispatchTrack. </td>
    <td> Cobertura global, escalabilidad y capacidad de integración. </td>
  </tr>
  <tr>
    <td><b>Debilidades</b></td>
    <td> Al ser una solución nueva, carece todavía de base de clientes consolidados y casos de éxito reales. </td>
    <td> Menos reconocimiento fuera de LATAM. </td>
    <td> Dependencia de adaptación tras adquisición. </td>
    <td> Puede resultar costosa y compleja para pymes locales. </td>
  </tr>
  <tr>
    <td><b>Oportunidades</b></td>
    <td> Aprovechar el crecimiento acelerado del e-commerce y la digitalización logística en LATAM para posicionarse como alternativa innovadora. </td>
    <td> Crecimiento del e-commerce en LATAM. </td>
    <td> Sinergias con la expansión global de DispatchTrack. </td>
    <td> Expansión en mercados emergentes con alto crecimiento digital. </td>
  </tr>
  <tr>
    <td><b>Amenazas</b></td>
    <td> Competidores consolidados como Beetrack y SimpliRoute ya cuentan con reconocimiento de marca y clientes en el mercado. </td>
    <td> Aparición de nuevos SaaS locales más económicos. </td>
    <td> Competencia fuerte de soluciones globales más completas. </td>
    <td> Regulaciones locales y adaptación cultural en LATAM. </td>
  </tr>
</table>

### 2.1.2. Estrategias y tácticas frente a competidores

Nuestra estrategia frente a competidores como SimpliRoute, Beetrack y FarEye será iniciar con pymes de transporte y distribución en el mercado peruano, ofreciendo una solución accesible y adaptable. A diferencia de los competidores consolidados, priorizaremos la simplicidad de uso, el soporte local y la personalización de funciones según la realidad de cada empresa.

Implementaremos un modelo SaaS modular y escalonado que facilite a las pequeñas empresas una adopción de bajo costo, permitiéndoles expandir capacidades a la par de sus operaciones. Para consolidar la confianza en el mercado nacional, impulsaremos estrategias basadas en pruebas piloto sin costo, validación con casos de éxito locales y un soporte técnico directo y cercano.

Nuestra propuesta de valor destaca por fusionar monitoreo IoT en tiempo real, automatización en la validación de pedidos y un sistema de alertas inteligentes dentro de una plataforma ágil y ligera. Esto se traduce en una reducción drástica de costos operativos, mayor cumplimiento en los tiempos de entrega y una seguridad reforzada frente a los desafíos logísticos del contexto peruano.

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
### 2.6.x. Bounded Context: 
### 2.6.x.1. Domain Layer
### 2.6.x.2. Interface Layer
### 2.6.x.3. Application Layer
### 2.6.x.4 Infrastructure Layer
### 2.6.x.5. Bounded Context Software Architecture Component Level Diagrams
### 2.6.x.6. Bounded Context Software Architecture Code Level Diagrams
### 2.6.x.6.1. Bounded Context Domain Layer Class Diagrams
### 2.6.x.6.2. Bounded Context Database Design Diagram
