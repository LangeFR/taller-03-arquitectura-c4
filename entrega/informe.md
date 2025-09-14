## 🔖 Nombre del Taller
_Taller 4 - Mapa de Infraestructura y Diagnóstico Técnico_

## 👥 Integrantes del equipo
- Diego Ramírez - diegorate@unisabana.edu.co  
- Carlos Sánchez - carlossanlo@unisabana.edu.co
- Mateo Vanegas - mateovaco@unisabana.edu.co

## 🧠 Descripción general del trabajo
Technologies mediante un mapa lógico que refleja cómo se despliegan y conectan los recursos que soportan sus operaciones. El objetivo del taller fue identificar, con base en el estado AS-IS de la organización, cuáles son los nodos de cómputo, servicios externos y repositorios de datos que conforman la arquitectura vigente, para posteriormente diagnosticar sus debilidades, cuellos de botella y oportunidades de mejora.

La actividad se desarrolló tomando como punto de partida los hallazgos de ejercicios previos (C1 y C2 del modelo C4) y trasladando los contenedores allí identificados hacia un esquema de despliegue realista. En este contexto, se representaron los portátiles del equipo como el núcleo de operación, los servicios SaaS externos (ERP Sigo, portales de banco, clientes y aliados) y el uso del correo electrónico como repositorio de facto de documentos. El resultado es un diagrama que evidencia la simplicidad y fragilidad de la infraestructura actual, así como su dependencia de procesos manuales y de servicios externos no integrados

## 🔧 Proceso de desarrollo
1. **Revisión de insumos previos:** Se analizaron los entregables del taller anterior (diagramas C1 y C2) para identificar los actores, contenedores y flujos de información críticos que debían trasladarse a un nivel de infraestructura. Esto permitió establecer qué debía representarse como nodo lógico o físico y qué debía modelarse como servicio externo.

2. **Identificación de nodos principales:** Se decidió agrupar los recursos de cómputo internos en un único *pool de laptops del equipo*, ya que Tekton no cuenta con servidores dedicados ni infraestructura centralizada. También se incluyeron explícitamente los servicios SaaS con los que la empresa interactúa (ERP Sigo, portales de clientes y aliados, portal bancario y MTA de correo).

3. **Asignación de artefactos a nodos:** A cada nodo se le asoció la funcionalidad o repositorio que actualmente soporta. En los portátiles se ubicó el *Backoffice Tekton* (procesos manuales de ofimática y correo) y las *planillas locales*. En el servicio de correo se señaló el datastore de buzones y adjuntos, considerado repositorio de facto.

4. **Definición de conexiones:** Se trazaron las relaciones de uso entre los nodos, especificando los protocolos o medios de interacción más frecuentes (SMTP/IMAP/HTTPS para correo, descargas manuales de extractos bancarios, portales web para facturación y conciliación, intercambio de archivos vía email).

5. **Iteración y simplificación:** Se realizaron varios ajustes para evitar sobrecargar el diagrama. En lugar de modelar cada portátil individualmente, se representó un único nodo con multiplicidad. De igual forma, se agruparon todos los servicios externos bajo un boundary común. Esto mantuvo el mapa comprensible y al mismo tiempo realista.

6. **Herramientas utilizadas:** El modelado se llevó a cabo en *draw.io*, manteniendo la notación UML de despliegue y siguiendo las prácticas de C4-Deployment para expresar nodos, artefactos y límites de sistema. La documentación se preparó en Markdown para facilitar la colaboración y el control de versiones.


Herramientas: **draw.io** para diagramas y Markdown para documentación colaborativa.

## 🧩 Análisis del modelo propuesto

### Cómo se estructura el modelo entregado
El modelo se organiza en tres agrupaciones principales: la **Oficina Bogotá**, donde se encuentra el pool de laptops del equipo con los artefactos Backoffice Tekton y planillas locales; el **Proveedor de Correo SaaS**, que actúa como repositorio de facto para documentos y adjuntos; y los **Servicios Externos**, que incluyen ERP Sigo, portales bancarios, portales de clientes y portales de aliados. Las conexiones se describen con los medios de interacción predominantes (correo electrónico, descargas manuales, portales web), reflejando el carácter manual y descentralizado de la infraestructura. 

### Cómo representa las necesidades del cliente
El modelo refleja con fidelidad el estado actual de Tekton, evidenciando que la operación depende de un conjunto limitado de laptops personales, del correo electrónico como canal principal y de servicios SaaS sin integración formal. Esta representación permite entender por qué la empresa enfrenta problemas de trazabilidad, control y estandarización: no existe un CRM ni un repositorio central, la conciliación se realiza con planillas, y la facturación se gestiona manualmente a través de portales. El mapa deja en claro las carencias de la infraestructura actual frente a los objetivos estratégicos de Tekton (centralización, automatización, visibilidad operativa).

### Supuestos tomados
- Se asumió que el **pool de laptops** representa a todos los empleados y que en ellos conviven tanto funciones administrativas como operativas.  
- Se modeló el **correo electrónico** como un nodo SaaS independiente con datastore, dado que allí se concentra la mayoría de los documentos críticos.  
- Se consideró que los **servicios externos (ERP Sigo, bancos, portales)** se consumen exclusivamente vía portales web, sin integración API nativa.  
- No se incluyeron otros elementos de red (firewall, switches) por no tener evidencia en los insumos, manteniendo el modelo en un nivel lógico simplificado.  


## 📈 Diagrama final entregado

- `entrega/Diagrama-Infraestructura-Tekton.drawio.png` — Diagrama Infraestructura Tekton.  

![Infraestructura Tekton](Diagrama-Infraestructura-Tekton.drawio.png)



## 🔍 Investigación complementaria
### Tema investigado:
Automatización de Backoffice e integración API-first en organizaciones B2B.

### Resumen:
En el ecosistema C4, la Deployment view sirve para ilustrar cómo instancias de software (sistemas o contenedores del C2) se mapean a nodos de infraestructura dentro de un ambiente específico (producción, staging, etc.). Esta vista hereda conceptos de UML Deployment y pone el foco en qué se despliega dónde y cómo se conectan esos elementos; no en componentes internos ni código. Esto la hace ideal para complementar nuestros C1/C2 con un mapa lógico/físico realista del AS-IS. 
C4 model

Para profundizar la capa tecnológica, ArchiMate 3.1 aporta un vocabulario formal de infraestructura: Node (recurso de TI que hospeda artefactos), Device (recurso físico), System software (entorno de ejecución) y Artifact (unidad desplegable). Estos elementos permiten describir con precisión dónde residen aplicaciones y datos, y qué relaciones existen entre los recursos (p. ej., caminos de comunicación). Usar esta semántica enriquece la lectura del mapa y facilita el diagnóstico de riesgos de infraestructura y dependencias. 
www.opengroup.org

Aplicado a Tekton, nuestro diagrama modela el pool de laptops como un Node que ejecuta los Artifacts “Backoffice Tekton” y “Planillas”; el MTA/Email como Node externo que actúa como datastore de facto; y los SaaS (ERP Sigo, banco, portales) como nodos externos conectados vía HTTPS/SMTP/IMAP. Separar los boundaries (oficina vs. servicios externos) y explicitar medios/protocolos sigue las guías de la Deployment view de C4 y permite razonar sobre disponibilidad, trazabilidad y puntos únicos de falla en el estado actual.

## 📚 Referencias
- [1] S. Brown, “Deployment diagram – C4 model,” c4model.com, 2024. [Online]. Available: https://c4model.com/diagrams/deployment
- [2] The Open Group, “ArchiMate® 3.1 Specification,” 2019. [Online]. Available: https://www.opengroup.org/sites/default/files/docs/downloads/n190p_5.pdf


---

_Este documento hace parte de la entrega del taller 3 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
