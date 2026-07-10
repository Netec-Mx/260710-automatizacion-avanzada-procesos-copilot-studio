# Automatización Avanzada de Procesos con Microsoft Copilot Studio

Capacitación práctica orientada al diseño, construcción, prueba y publicación de un agente en Microsoft Copilot Studio aplicado a procesos de auditoría. El curso se enfoca en crear agentes con instrucciones controladas, temas conversacionales, variables, entidades, fuentes de conocimiento, respuestas generativas sustentadas, automatización mediante agent flows / workflows como herramientas, trazabilidad y despliegue en Microsoft Teams.

## Estructura

- `CapituloXX/README.md`: guía de laboratorio por capítulo.

## Lista de laboratorios

### Capítulo 1

- [Definir usuarios, entradas, salidas, reglas y alcance del agente auditor](Capitulo01/README.md#definir-usuarios-entradas-salidas-reglas-y-alcance-del-agente-auditor)
  - Descripción: Los participantes diseñarán el canvas funcional del agente auditor, estableciendo el proceso de auditoría a automatizar, los controles a revisar, la evidencia esperada, los posibles resultados, las restricciones de uso y los recursos iniciales que servirán como base para la construcción del agente.
  - Duración estimada: 15 min

### Capítulo 2

- [Crear el agente base, configurar instrucciones y probar escenarios de auditoría con control de alcance](Capitulo02/README.md#crear-el-agente-base-configurar-instrucciones-y-probar-escenarios-de-auditoría-con-control-de-alcance)
  - Descripción: Los participantes crearán el agente base en Copilot Studio, definirán instrucciones orientadas al rol auditor, establecerán límites de respuesta, configurarán fuentes o conocimiento inicial y ejecutarán pruebas para validar que el agente responda dentro del alcance definido.
  - Duración estimada: 20 min

### Capítulo 3

- [Crear un tema de revisión de control con variables, entidades, condiciones y rutas de excepción](Capitulo03/README.md#crear-un-tema-de-revisión-de-control-con-variables-entidades-condiciones-y-rutas-de-excepción)
  - Descripción: Los participantes crearán un tema conversacional para guiar una revisión de control interno, solicitando datos como proceso, control, periodo, responsable, riesgo y evidencia. También configurarán condiciones para manejar cumplimiento, excepciones, datos incompletos o necesidad de escalamiento.
  - Duración estimada: 20 min

### Capítulo 4

- [Configurar conocimiento y datos estructurados para responder consultas de auditoría con sustento](Capitulo04/README.md#configurar-conocimiento-y-datos-estructurados-para-responder-consultas-de-auditoría-con-sustento)
  - Descripción: Los participantes incorporarán fuentes de conocimiento como procedimientos, matrices de control, políticas, documentos o tablas estructuradas. El agente será probado con consultas sobre criterios de revisión, evidencia, posibles hallazgos y observaciones preliminares.
  - Duración estimada: 30 min

### Capítulo 5

- [Crear un workflow como herramienta para registrar una revisión y devolver confirmación o alertar excepción](Capitulo05/README.md#crear-un-workflow-como-herramienta-para-registrar-una-revisión-y-devolver-confirmación-o-alertar-excepción)
  - Descripción: Los participantes crearán o conectarán un workflow que reciba información capturada por el agente, registre una revisión, comunique una excepción o devuelva una confirmación al usuario. Se validará el paso de variables, la ejecución del flujo y la respuesta final en la conversación.
  - Duración estimada: 20 min

### Capítulo 6

- [Ejecutar matriz de pruebas del agente auditor y ajustar instrucciones, temas, conocimiento o workflow](Capitulo06/README.md#ejecutar-matriz-de-pruebas-del-agente-auditor-y-ajustar-instrucciones-temas-conocimiento-o-workflow)
  - Descripción: Los participantes ejecutarán escenarios de prueba para validar consistencia, fundamento de respuesta, manejo de excepciones, trazabilidad, ejecución del workflow y calidad de las respuestas generativas. Con base en los resultados, ajustarán instrucciones, temas, conocimiento o automatizaciones.
  - Duración estimada: 25 min

### Capítulo 7

- [Ejecutar una revisión completa desde Teams con consulta de conocimiento, registro automatizado y salida final](Capitulo07/README.md#ejecutar-una-revisión-completa-desde-teams-con-consulta-de-conocimiento-registro-automatizado-y-salida-final)
  - Descripción: Los participantes probarán el agente desde Teams, simulando una revisión completa: captura de información, consulta de conocimiento, generación de respuesta sustentada, ejecución del workflow, registro o alerta automatizada y entrega de una salida final para el usuario auditor.
  - Duración estimada: 20 min

## Flujo de colaboración

- Trabajar en `changes_course`.
- Crear Pull Request hacia `main`.
- Merge por `Squash and merge`.
