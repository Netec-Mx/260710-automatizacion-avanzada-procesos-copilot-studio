---LAB_START---
LAB_ID: 01-00-01
---MARKDOWN---
# Definir usuarios, entradas, salidas, reglas y alcance del agente auditor

## 1. Metadatos

| Atributo | Valor |
|---|---|
| **Duración estimada** | 15 minutos |
| **Complejidad** | Fácil |
| **Nivel de Bloom** | Crear |
| **Modalidad** | Analítica y documental (sin construcción técnica) |
| **Práctica número** | 1 de 7 |

---

## 2. Descripción General

En esta práctica, el estudiante realizará un ejercicio de análisis y diseño previo a cualquier construcción técnica en Copilot Studio. Utilizando una plantilla estructurada denominada **Ficha de Agente**, documentará el caso base del curso: un agente conversacional para la validación de controles internos en Microsoft Teams. El resultado de esta práctica —la Ficha de Agente completada— servirá como referencia de diseño obligatoria para todas las prácticas posteriores del curso, por lo que su correcta elaboración es fundamental.

Esta práctica está directamente fundamentada en los cuatro casos de uso de agentes en auditoría interna estudiados en la Lección 1.1: validaciones de controles, recopilación de evidencias, identificación de hallazgos y seguimiento de compromisos.

---

## 3. Objetivos de Aprendizaje

Al completar esta práctica, el estudiante será capaz de:

- [ ] Identificar y documentar los casos de uso específicos de un agente conversacional para auditoría interna, distinguiendo entre validaciones, evidencias, hallazgos y seguimiento.
- [ ] Definir con precisión los perfiles de usuario, entradas esperadas, salidas requeridas y reglas de negocio del agente auditor en la Ficha de Agente.
- [ ] Delimitar el alcance operativo del agente, especificando explícitamente qué puede y qué no puede hacer en el contexto de Copilot Studio.
- [ ] Producir un documento de diseño base completo que sirva como referencia técnica y conceptual para las prácticas 2 a 7 del curso.

---

## 4. Prerrequisitos

### Conocimientos previos requeridos

| Área | Nivel requerido |
|---|---|
| Microsoft 365 y Teams | Básico — saber iniciar sesión, navegar y crear documentos |
| Auditoría interna y controles | Nocional — comprensión de qué es un control interno y su ciclo de validación |
| Agentes conversacionales | Conceptual — haber completado la Lección 1.1 del curso |
| Microsoft Copilot Studio | Ninguno técnico aún — solo comprensión conceptual de sus capacidades |

### Acceso requerido

| Recurso | Estado requerido |
|---|---|
| Cuenta de Microsoft 365 activa | ✅ Obligatorio — misma cuenta que se usará en todo el curso |
| Acceso a Microsoft Teams | ✅ Obligatorio — para acceder al equipo del curso |
| Acceso a SharePoint Online | ✅ Obligatorio — como referencia de fuentes de conocimiento |
| Microsoft Word o editor de texto | ✅ Obligatorio — para completar la Ficha de Agente |
| Plantilla de Ficha de Agente | ✅ Obligatorio — distribuida por el instructor antes de esta práctica |

> **Nota para el instructor:** La plantilla de Ficha de Agente debe distribuirse a los estudiantes antes del inicio de esta práctica, ya sea a través del canal del equipo de Teams del curso o mediante un enlace de SharePoint. El archivo puede ser un documento Word (.docx) o un formulario editable.

---

## 5. Entorno de Laboratorio

### Hardware recomendado

| Componente | Mínimo | Recomendado |
|---|---|---|
| Procesador | Intel Core i5 8ª gen / AMD Ryzen 5 | Intel Core i7 10ª gen o superior |
| Memoria RAM | 8 GB | 16 GB |
| Almacenamiento libre | 500 MB (para esta práctica) | 2 GB (para todo el curso) |
| Resolución de pantalla | 1366 × 768 | 1920 × 1080 |
| Conexión a internet | 10 Mbps | 25 Mbps |

### Software requerido

| Software | Versión | Uso en esta práctica |
|---|---|---|
| Microsoft Edge o Chrome | 120 o superior | Acceso a Teams y SharePoint |
| Microsoft Teams | Versión actual (desktop o web) | Acceso al equipo del curso y descarga de plantilla |
| Microsoft Word | Microsoft 365 o compatible | Completar la Ficha de Agente |
| Microsoft SharePoint Online | Versión cloud actual | Referencia de fuentes de conocimiento disponibles |

### Configuración inicial (sin comandos técnicos)

Esta práctica no requiere instalación de software adicional ni configuración de entornos cloud. Antes de comenzar, el estudiante debe:

1. Iniciar sesión en [https://teams.microsoft.com](https://teams.microsoft.com) con la cuenta del curso.
2. Verificar que puede acceder al canal del equipo del curso donde el instructor publicó la plantilla.
3. Descargar la plantilla **Ficha de Agente Auditor v1.0** al equipo local.
4. Abrir el archivo en Microsoft Word o en el editor de texto de preferencia.

---

## 6. Instrucciones Paso a Paso

---

### Paso 1: Revisar el escenario base y los casos de uso del agente

**Objetivo:** Comprender el contexto operativo del agente que se diseñará, identificando los cuatro casos de uso de la Lección 1.1 que aplican al escenario del curso.

#### Instrucciones

1. Lee detenidamente el siguiente escenario base que se usará durante todo el curso:

   > **Escenario del curso — Empresa ficticia: Financiera Andina S.A.**
   >
   > Financiera Andina S.A. es una empresa de servicios financieros con 450 empleados. Su departamento de Auditoría Interna está compuesto por cuatro auditores y un coordinador. Trimestralmente, el equipo debe validar 120 controles internos distribuidos en seis procesos críticos: Tesorería, Crédito, Cumplimiento Normativo, Tecnología, Recursos Humanos y Contabilidad. El ciclo actual de validación toma seis semanas y depende de correos electrónicos, hojas de cálculo y reuniones presenciales. La gerencia ha solicitado reducir este ciclo a dos semanas y mejorar la trazabilidad de evidencias.

2. Con base en la Lección 1.1, identifica cuáles de los cuatro casos de uso aplican al escenario de Financiera Andina S.A. Utiliza la siguiente tabla de referencia para orientar tu análisis:

   | Caso de uso (Lección 1.1) | ¿Aplica al escenario? | Justificación breve |
   |---|---|---|
   | Validaciones de controles | | |
   | Recopilación de evidencias | | |
   | Identificación de hallazgos | | |
   | Seguimiento de compromisos | | |

3. Completa la tabla anterior en tu cuaderno o en la sección **"Sección 0 — Análisis de casos de uso"** de la Ficha de Agente.

#### Resultado esperado

Una tabla de análisis completada donde los cuatro casos de uso estén marcados como aplicables, con una justificación de una a dos oraciones para cada uno basada en el escenario de Financiera Andina S.A.

#### Verificación

✅ Los cuatro casos de uso están identificados como aplicables.
✅ Cada justificación hace referencia explícita a un elemento del escenario (ciclo de seis semanas, 120 controles, cuatro auditores, etc.).
✅ El lenguaje utilizado es consistente con la terminología de auditoría interna de la Lección 1.1.

---

### Paso 2: Definir los perfiles de usuario del agente

**Objetivo:** Identificar y documentar los tres perfiles de usuario que interactuarán con el agente auditor, describiendo el rol, las necesidades y el nivel de acceso de cada uno.

#### Instrucciones

1. Abre la **Sección 1 — Perfiles de Usuario** de la Ficha de Agente.

2. Para cada uno de los tres perfiles indicados a continuación, completa los campos solicitados en la plantilla:

   **Perfil 1: Auditor Interno**
   - **Rol en la organización:** Miembro del equipo de Auditoría Interna de Financiera Andina S.A.
   - **Interacción principal con el agente:** Recibe notificaciones de hallazgos críticos, revisa resúmenes de validaciones y accede a reportes consolidados.
   - **Necesidad principal:** Visibilidad en tiempo real del estado de validaciones sin necesidad de enviar correos de seguimiento.
   - **Nivel de acceso esperado:** Lectura de todos los registros; recepción de alertas automáticas.

   **Perfil 2: Responsable de Proceso**
   - **Rol en la organización:** Empleado responsable de ejecutar y documentar un control interno específico (ej.: jefe de Tesorería, coordinador de Cumplimiento).
   - **Interacción principal con el agente:** Responde preguntas del agente sobre la ejecución de controles, carga evidencias y confirma información.
   - **Necesidad principal:** Proceso de validación ágil que no interrumpa su trabajo operativo diario.
   - **Nivel de acceso esperado:** Lectura y escritura solo de los controles asignados a su proceso.

   **Perfil 3: Coordinador de Auditoría**
   - **Rol en la organización:** Responsable de la planificación, seguimiento y cierre del ciclo auditor trimestral.
   - **Interacción principal con el agente:** Configura los periodos de validación, revisa el avance global y aprueba el cierre de hallazgos.
   - **Necesidad principal:** Panel de control del estado de avance de las 120 validaciones trimestrales.
   - **Nivel de acceso esperado:** Acceso completo a todos los registros, configuración del agente y aprobación de cierres.

3. Añade en la plantilla una columna adicional titulada **"Canal de interacción"** y especifica para cada perfil el canal principal a través del cual interactuará con el agente. Considera: Microsoft Teams (chat directo), canal de Teams del equipo auditor, o correo electrónico de notificación.

4. Reflexiona y responde en la plantilla: ¿Existe algún perfil de usuario que **no** debería tener acceso al agente? Justifica tu respuesta con al menos una razón de seguridad o confidencialidad.

#### Resultado esperado

La Sección 1 de la Ficha de Agente completada con los tres perfiles, sus necesidades, niveles de acceso y canales de interacción. La pregunta de reflexión respondida con al menos dos oraciones.

#### Verificación

✅ Los tres perfiles están documentados con todos los campos requeridos.
✅ El canal de interacción para cada perfil es coherente con las capacidades de Microsoft Teams y Copilot Studio.
✅ La reflexión sobre exclusión de acceso menciona al menos un principio de confidencialidad o control de acceso (ej.: separación de funciones, need-to-know).

---

### Paso 3: Documentar las entradas esperadas del agente

**Objetivo:** Definir con precisión los cinco tipos de entrada que el agente recibirá durante una conversación de validación de controles, especificando el formato, el origen y el carácter obligatorio u opcional de cada una.

#### Instrucciones

1. Abre la **Sección 2 — Entradas del Agente** de la Ficha de Agente.

2. Para cada una de las cinco entradas listadas a continuación, completa todos los campos de la tabla en la plantilla:

   | # | Nombre de la entrada | Descripción | Tipo de dato | ¿Obligatoria? | Ejemplo de valor |
   |---|---|---|---|---|---|
   | 1 | Nombre del proceso | Proceso organizacional al que pertenece el control | Texto (lista cerrada) | Sí | "Tesorería" |
   | 2 | Control a validar | Identificador o descripción del control específico | Texto (alfanumérico) | Sí | "CTR-TES-007: Conciliación bancaria mensual" |
   | 3 | Periodo de validación | Mes y año al que corresponde la validación | Fecha (MM/AAAA) | Sí | "03/2025" |
   | 4 | Responsable del control | Nombre o correo del empleado responsable de ejecutar el control | Texto / correo electrónico | Sí | "maria.garcia@financieraandina.com" |
   | 5 | Evidencia disponible | Archivo o referencia documental que soporta la ejecución del control | Archivo adjunto / URL | No (pero requerida para clasificar como "Conforme") | Archivo PDF: "Conciliacion_Marzo2025.pdf" |

3. Agrega una fila adicional en la tabla para una **sexta entrada** que consideres relevante para el escenario de Financiera Andina S.A. Justifica su inclusión en la columna de descripción.

   > **Sugerencia:** Considera entradas como: observaciones adicionales del responsable, fecha real de ejecución del control, o indicador de si el control fue ejecutado por un suplente.

4. Para cada entrada, indica en una columna adicional **"Fuente de validación"** cómo el agente podría verificar que el valor recibido es correcto. Por ejemplo: lista de valores predefinidos, formato de fecha, dominio de correo corporativo, etc.

#### Resultado esperado

La Sección 2 de la Ficha de Agente con seis entradas documentadas, incluyendo tipo de dato, carácter obligatorio, ejemplo de valor y fuente de validación para cada una.

#### Verificación

✅ Las cinco entradas base están documentadas correctamente.
✅ La sexta entrada propuesta tiene una justificación coherente con el escenario de auditoría.
✅ La columna "Fuente de validación" demuestra pensamiento sobre cómo el agente garantizará la calidad de los datos capturados.
✅ Los tipos de dato son específicos (no solo "texto" para todo), lo que refleja comprensión de las capacidades de Copilot Studio.

---

### Paso 4: Definir las salidas requeridas del agente

**Objetivo:** Documentar los tres tipos de salida que el agente debe producir como resultado de una conversación de validación, especificando el destinatario, el canal y el contenido mínimo de cada una.

#### Instrucciones

1. Abre la **Sección 3 — Salidas del Agente** de la Ficha de Agente.

2. Completa la tabla de salidas con la información de los tres tipos principales:

   **Salida 1: Confirmación de cumplimiento**
   - **Descripción:** Mensaje al responsable del proceso confirmando que la validación fue registrada exitosamente y clasificada como conforme.
   - **Destinatario:** Responsable del proceso (Perfil 2).
   - **Canal de entrega:** Mensaje de chat en Microsoft Teams.
   - **Contenido mínimo requerido:** Nombre del control validado, periodo, clasificación ("Conforme"), fecha y hora del registro, número de referencia del registro en Dataverse.
   - **Ejemplo de mensaje:** *"✅ Validación registrada. Control: CTR-TES-007 | Periodo: 03/2025 | Clasificación: Conforme | Referencia: VAL-2025-0342. Gracias por su respuesta."*

   **Salida 2: Alerta de excepción**
   - **Descripción:** Notificación automática al auditor interno cuando el agente detecta un control no ejecutado o ejecutado con deficiencias.
   - **Destinatario:** Auditor Interno (Perfil 1) y Coordinador de Auditoría (Perfil 3).
   - **Canal de entrega:** Mensaje en canal de Teams del equipo auditor + correo electrónico automático (vía Power Automate).
   - **Contenido mínimo requerido:** Nombre del proceso, control afectado, periodo, responsable, clasificación ("No conforme" o "Conforme con observación"), descripción de la excepción detectada.
   - **Ejemplo de mensaje:** *"⚠️ ALERTA DE EXCEPCIÓN — Control CTR-TES-007 (Tesorería) | Periodo: 03/2025 | Responsable: M. García | Clasificación: No conforme | Motivo: Control no ejecutado durante el período. Acción requerida."*

   **Salida 3: Resumen de hallazgo**
   - **Descripción:** Documento o registro estructurado que consolida la información de una excepción detectada para su análisis y seguimiento posterior.
   - **Destinatario:** Coordinador de Auditoría (Perfil 3).
   - **Canal de entrega:** Registro en tabla de Dataverse for Teams + resumen en formato texto en el canal de Teams.
   - **Contenido mínimo requerido:** Todos los campos de la Salida 2 + evidencias adjuntas (o indicación de ausencia), fecha de detección, auditor responsable del seguimiento, estado inicial del hallazgo ("Abierto").

3. Para cada salida, añade una columna **"Disparador"** que indique qué condición o evento de la conversación activa esa salida. Por ejemplo: respuesta del responsable = "No", ausencia de evidencia adjunta, clasificación automática = "No conforme".

4. Reflexiona y documenta: ¿Qué sucede si el responsable del proceso no responde al agente en un plazo de 48 horas? ¿Qué salida debería generar el agente en ese caso? Añade esta como **Salida 4 (opcional)** en tu Ficha de Agente.

#### Resultado esperado

La Sección 3 de la Ficha de Agente con tres salidas principales documentadas con todos sus campos, la columna de disparadores completada, y una propuesta para la Salida 4 de no-respuesta.

#### Verificación

✅ Las tres salidas principales están documentadas con destinatario, canal, contenido mínimo y ejemplo.
✅ La columna "Disparador" es específica y no genérica (no dice solo "cuando hay un problema").
✅ La Salida 4 propuesta demuestra comprensión del ciclo de vida de una validación y la importancia del seguimiento.
✅ Los canales de entrega son coherentes con las herramientas del ecosistema Microsoft 365 (Teams, Power Automate, Dataverse).

---

### Paso 5: Establecer las reglas de respuesta del agente

**Objetivo:** Definir las reglas de comportamiento del agente que garantizarán un tono adecuado, restricción al dominio de auditoría, escalamiento correcto de excepciones y uso responsable de IA generativa.

#### Instrucciones

1. Abre la **Sección 4 — Reglas de Respuesta** de la Ficha de Agente.

2. Documenta las siguientes cinco reglas de respuesta en la plantilla, añadiendo para cada una una justificación de por qué es necesaria en el contexto de auditoría interna:

   **Regla 1: Tono formal y profesional**
   - **Descripción:** El agente siempre utilizará un tono formal, en tercera persona o con tratamiento de usted, sin emojis en mensajes de excepción ni lenguaje coloquial.
   - **Justificación:** *(Completa en la plantilla — mínimo dos oraciones)*
   - **Ejemplo de aplicación:** El agente no debe responder "¡Genial! Ya guardé tu info 😊" sino "La información ha sido registrada correctamente. Referencia: VAL-2025-0342."

   **Regla 2: Restricción al dominio de auditoría interna**
   - **Descripción:** El agente solo responderá preguntas relacionadas con validaciones de controles, evidencias, hallazgos y seguimiento. Cualquier pregunta fuera de este dominio debe ser redirigida con un mensaje estándar.
   - **Justificación:** *(Completa en la plantilla — mínimo dos oraciones)*
   - **Mensaje estándar de fuera de dominio:** *"Esta consulta está fuera del alcance del Agente Auditor de Financiera Andina. Para otras consultas, contacte al área correspondiente."*

   **Regla 3: Escalamiento ante excepciones críticas**
   - **Descripción:** Cuando el agente detecte un control no ejecutado por tres o más periodos consecutivos, o cuando el responsable reporte un riesgo de fraude, el agente debe escalar inmediatamente al Coordinador de Auditoría sin esperar el cierre de la conversación.
   - **Justificación:** *(Completa en la plantilla — mínimo dos oraciones)*
   - **Criterio de escalamiento crítico:** Control no ejecutado ≥ 3 periodos consecutivos | Mención de fraude, irregularidad o pérdida no autorizada.

   **Regla 4: Confirmación antes de registrar**
   - **Descripción:** Antes de guardar cualquier validación en Dataverse, el agente debe presentar un resumen de los datos capturados y solicitar confirmación explícita del responsable.
   - **Justificación:** *(Completa en la plantilla — mínimo dos oraciones)*
   - **Ejemplo de mensaje de confirmación:** *"Por favor confirme los siguientes datos antes de registrar: [resumen]. ¿Es correcto? Responda SÍ para confirmar o NO para corregir."*

   **Regla 5: Transparencia sobre el uso de IA generativa**
   - **Descripción:** Cuando el agente utilice respuestas generativas (no scripted), debe indicarlo con una leyenda estándar al final del mensaje.
   - **Justificación:** *(Completa en la plantilla — mínimo dos oraciones)*
   - **Leyenda estándar:** *"⚠️ Esta respuesta fue generada por IA. Verifique con el equipo de Auditoría Interna ante cualquier duda."*

3. Añade al menos **una regla adicional** (Regla 6) que consideres relevante para el contexto específico de Financiera Andina S.A. como empresa de servicios financieros. Considera aspectos como: confidencialidad de datos, regulación financiera, o manejo de información sensible.

#### Resultado esperado

La Sección 4 de la Ficha de Agente con seis reglas de respuesta documentadas, cada una con descripción, justificación, ejemplo o criterio de aplicación.

#### Verificación

✅ Las cinco reglas base están documentadas con justificación completa (mínimo dos oraciones cada una).
✅ La Regla 6 propuesta es específica para el sector financiero y no es una repetición de las anteriores.
✅ Las reglas son operacionalizables: están descritas de manera que un diseñador de Copilot Studio podría implementarlas en instrucciones del sistema o condiciones de flujo.
✅ La Regla 5 sobre transparencia de IA refleja comprensión de las buenas prácticas de IA responsable.

---

### Paso 6: Delimitar el alcance del agente

**Objetivo:** Producir la sección de alcance de la Ficha de Agente, definiendo explícitamente qué puede hacer el agente, qué no puede hacer, y cuáles son las restricciones técnicas y de dominio aplicables en el contexto de Copilot Studio.

#### Instrucciones

1. Abre la **Sección 5 — Alcance del Agente** de la Ficha de Agente.

2. Completa las tres sub-secciones de alcance:

   **Sub-sección A: Lo que el agente SÍ puede hacer**

   Documenta al menos ocho capacidades concretas del agente. Usa la siguiente lista de partida y añade al menos dos propias:

   - ✅ Iniciar conversaciones de validación con responsables de proceso en Microsoft Teams.
   - ✅ Formular preguntas estructuradas sobre la ejecución de controles internos.
   - ✅ Capturar respuestas de texto, selección de opciones y confirmaciones del usuario.
   - ✅ Solicitar y recibir archivos de evidencia adjuntos en la conversación.
   - ✅ Clasificar automáticamente las validaciones como Conforme, Conforme con observación o No conforme.
   - ✅ Registrar los resultados de validación en una tabla de Dataverse for Teams.
   - ✅ Enviar alertas automáticas al equipo auditor mediante Power Automate cuando detecta excepciones.
   - ✅ Responder preguntas frecuentes sobre el proceso de validación de controles.
   - ✅ *(Añade tu primera capacidad adicional aquí)*
   - ✅ *(Añade tu segunda capacidad adicional aquí)*

   **Sub-sección B: Lo que el agente NO puede hacer (restricciones)**

   Documenta al menos seis restricciones. Usa la siguiente lista de partida y añade al menos dos propias:

   - ❌ No puede tomar decisiones de auditoría autónomas ni emitir opiniones de auditoría formales.
   - ❌ No puede acceder a sistemas externos fuera del ecosistema Microsoft 365 sin una integración explícita mediante conectores de Power Automate.
   - ❌ No puede garantizar la autenticidad de las evidencias adjuntas (solo registra su existencia).
   - ❌ No puede reemplazar el juicio profesional del auditor en la evaluación de riesgos complejos.
   - ❌ No puede procesar información en idiomas distintos al español sin configuración adicional.
   - ❌ No puede enviar comunicaciones fuera del tenant de Microsoft 365 de Financiera Andina S.A.
   - ❌ *(Añade tu primera restricción adicional aquí)*
   - ❌ *(Añade tu segunda restricción adicional aquí)*

   **Sub-sección C: Condiciones de operación**

   Documenta las condiciones mínimas que deben cumplirse para que el agente funcione correctamente:

   | Condición | Descripción | Responsable de garantizarla |
   |---|---|---|
   | Licencia activa | El usuario debe tener licencia de Microsoft 365 Copilot o Copilot Studio | Administrador de TI |
   | Dataverse for Teams activo | La tabla de registros debe estar creada y accesible | Coordinador de Auditoría / TI |
   | Conexión a Teams | El usuario debe estar conectado a Teams durante la conversación | Usuario final |
   | Permisos de rol | El usuario debe tener el perfil correcto asignado en el agente | Coordinador de Auditoría |
   | *(Añade una condición adicional)* | | |

3. Cierra la Sección 5 con un párrafo de **"Declaración de alcance"** de tres a cinco oraciones que resuma de manera ejecutiva qué es y qué no es el agente auditor de Financiera Andina S.A. Este párrafo debe poder ser leído por un gerente no técnico y ser completamente comprensible.

#### Resultado esperado

La Sección 5 de la Ficha de Agente completada con las tres sub-secciones: capacidades (mínimo 10), restricciones (mínimo 8), condiciones de operación (mínimo 5) y la Declaración de alcance.

#### Verificación

✅ Las capacidades adicionales propuestas son técnicamente realizables en Copilot Studio según lo aprendido en la Lección 1.1.
✅ Las restricciones adicionales son específicas y no son reformulaciones de las ya listadas.
✅ La Declaración de alcance es comprensible para un lector no técnico y no contiene jerga de programación.
✅ La tabla de condiciones de operación tiene al menos cinco filas con responsables identificados.

---

### Paso 7: Revisar y consolidar la Ficha de Agente

**Objetivo:** Realizar una revisión final de coherencia y completitud de la Ficha de Agente antes de entregarla como artefacto del laboratorio.

#### Instrucciones

1. Completa la **Sección 0 — Información General** de la Ficha de Agente con los siguientes metadatos del documento:

   | Campo | Valor a completar |
   |---|---|
   | **Nombre del agente** | Agente Auditor — Financiera Andina S.A. |
   | **Versión del documento** | 1.0 |
   | **Fecha de creación** | *(fecha de hoy)* |
   | **Elaborado por** | *(tu nombre completo)* |
   | **Revisado por** | *(nombre del instructor o "Pendiente de revisión")* |
   | **Propósito del documento** | Ficha de diseño base para la construcción del agente auditor en Microsoft Copilot Studio |
   | **Estado** | Borrador — Práctica 1 |

2. Utiliza la siguiente lista de verificación de completitud para asegurarte de que ninguna sección esté incompleta antes de entregar:

   - [ ] Sección 0 — Información general: todos los campos completados.
   - [ ] Sección 0 — Análisis de casos de uso: cuatro casos documentados con justificación.
   - [ ] Sección 1 — Perfiles de usuario: tres perfiles + reflexión de exclusión.
   - [ ] Sección 2 — Entradas: seis entradas con todos los campos, incluyendo fuente de validación.
   - [ ] Sección 3 — Salidas: tres salidas principales + Salida 4 de no-respuesta.
   - [ ] Sección 4 — Reglas: seis reglas con justificaciones completas.
   - [ ] Sección 5 — Alcance: capacidades, restricciones, condiciones y Declaración de alcance.

3. Guarda el documento con el nombre de archivo: `FichaAgente_[TuApellido]_Lab01.docx`

4. Sube el archivo al canal del equipo de Teams del curso en la carpeta **"Entregables — Práctica 1"** según las indicaciones del instructor.

5. Comparte brevemente con un compañero (o en el chat del canal) **una sola decisión de diseño** que tomaste en la Ficha de Agente que consideres especialmente importante para el éxito del agente. Explica en dos a tres oraciones por qué esa decisión importa.

#### Resultado esperado

El archivo `FichaAgente_[TuApellido]_Lab01.docx` subido al canal de Teams del curso, con todas las secciones completadas según la lista de verificación. Un comentario de reflexión publicado en el canal.

#### Verificación

✅ El nombre del archivo sigue la convención indicada.
✅ El archivo está subido en la carpeta correcta del canal de Teams.
✅ Todas las casillas de la lista de verificación de completitud están marcadas.
✅ El comentario de reflexión está publicado en el canal y menciona una decisión de diseño específica.

---

## 7. Validación y Prueba del Entregable

Al finalizar la práctica, el estudiante y el instructor deben verificar que la Ficha de Agente cumple con los siguientes criterios de calidad antes de avanzar a la Práctica 2:

### Criterios de aceptación del entregable

| Criterio | Indicador de cumplimiento | ¿Cumple? |
|---|---|---|
| **Completitud** | Las siete secciones de la Ficha de Agente están documentadas sin campos en blanco | ☐ |
| **Coherencia interna** | Los perfiles de usuario (Sección 1) son consistentes con los destinatarios de las salidas (Sección 3) | ☐ |
| **Especificidad técnica** | Las entradas (Sección 2) tienen tipos de dato específicos, no solo "texto" para todas | ☐ |
| **Operacionalización de reglas** | Las reglas (Sección 4) están descritas de manera que pueden implementarse en Copilot Studio | ☐ |
| **Alcance realista** | Las capacidades del agente (Sección 5A) son realizables con las herramientas del curso | ☐ |
| **Restricciones honestas** | Las restricciones (Sección 5B) reflejan comprensión real de las limitaciones de Copilot Studio | ☐ |
| **Declaración ejecutiva** | La Declaración de alcance puede ser comprendida por un gerente no técnico | ☐ |
| **Formato y entrega** | El archivo sigue la convención de nombre y está en la carpeta correcta de Teams | ☐ |

> **Para el instructor:** La Ficha de Agente completada en esta práctica debe ser revisada antes de la Práctica 2. Un diseño deficiente en esta etapa (especialmente en entradas, salidas y reglas) generará problemas técnicos en las prácticas 3, 4 y 5. Se recomienda una revisión rápida de cinco minutos por participante al final de la sesión o antes de la siguiente práctica.

### Prueba de consistencia cruzada

Realiza la siguiente prueba mental de consistencia antes de entregar:

> **Escenario de prueba:** El responsable de Tesorería abre Teams, el agente le envía un mensaje preguntando si ejecutó el control CTR-TES-007 en marzo 2025. El responsable responde que no lo ejecutó porque hubo un cambio de sistema. El agente debe registrar esta excepción y notificar al equipo auditor.

Verifica que tu Ficha de Agente responde correctamente a estas preguntas:
- ¿Qué perfil de usuario es el responsable de Tesorería? → Sección 1
- ¿Qué entradas captura el agente en este escenario? → Sección 2
- ¿Qué salidas genera el agente al detectar la excepción? → Sección 3
- ¿Qué regla de escalamiento aplica? → Sección 4
- ¿Esta situación está dentro del alcance del agente? → Sección 5

Si tu Ficha de Agente no puede responder alguna de estas preguntas, revisa y completa la sección correspondiente antes de entregar.

---

## 8. Solución de Problemas

### Problema 1: El estudiante no puede acceder a la plantilla de Ficha de Agente en el canal de Teams

**Síntoma:** Al intentar abrir el canal del equipo del curso en Teams, el estudiante recibe el mensaje "No tienes acceso a este equipo" o no encuentra el archivo de plantilla en la carpeta de entregables.

**Causa probable:** El estudiante no ha sido añadido como miembro del equipo de Teams del curso, o la carpeta de archivos no tiene los permisos correctos configurados. Esto ocurre frecuentemente cuando el estudiante usa una cuenta diferente a la registrada por el instructor, o cuando el equipo de Teams fue creado recientemente y la sincronización de membresía aún no se completó.

**Solución:**
1. Verificar que la cuenta con la que se inicia sesión en Teams es la misma cuenta del curso (debe terminar con el dominio del tenant del curso, no con @outlook.com o @gmail.com).
2. Solicitar al instructor que reenvíe la invitación al equipo de Teams usando la dirección de correo correcta.
3. Si el problema persiste, el instructor puede compartir la plantilla directamente por mensaje privado de Teams o por correo electrónico mientras se resuelve el acceso al equipo.
4. Como alternativa temporal, el instructor puede compartir un enlace de descarga directa del archivo desde SharePoint Online con la opción "Compartir con personas específicas".

---

### Problema 2: El estudiante tiene dificultad para distinguir entre "entradas" y "salidas" del agente, completando ambas secciones con el mismo tipo de información

**Síntoma:** En la Sección 2 (Entradas) y la Sección 3 (Salidas) de la Ficha de Agente, el estudiante documenta información similar o intercambia los conceptos, por ejemplo, listando "confirmación de cumplimiento" como una entrada o "nombre del proceso" como una salida.

**Causa probable:** Confusión conceptual entre el flujo de información que entra al agente (datos que el usuario proporciona) y el flujo de información que sale del agente (acciones o mensajes que el agente genera). Esta confusión es común en estudiantes sin experiencia previa en diseño de sistemas conversacionales o flujos de proceso.

**Solución:**
1. Recordar al estudiante la distinción fundamental: las **entradas** son datos que el agente recibe del usuario o del sistema para poder procesar una solicitud; las **salidas** son acciones o mensajes que el agente genera como resultado de ese procesamiento.
2. Usar la analogía de un formulario de auditoría tradicional: las entradas son los campos que el auditado llena; las salidas son el acuse de recibo, la notificación al auditor y el registro en el sistema.
3. Pedir al estudiante que trace una línea de tiempo simple: primero ocurre X (entrada), luego el agente procesa, luego ocurre Y (salida). Si algo está en el lado "primero", es una entrada; si está en el lado "luego", es una salida.
4. Revisar juntos el escenario de prueba del Paso 7 (responsable de Tesorería y control CTR-TES-007) y mapear explícitamente qué es entrada y qué es salida en ese escenario concreto.

---

## 9. Limpieza del Entorno

Esta práctica es completamente documental y no modifica ningún entorno técnico de Microsoft 365. Sin embargo, se recomiendan las siguientes acciones de orden al finalizar:

1. **Guardar versión final del documento:** Asegúrate de que el archivo `FichaAgente_[TuApellido]_Lab01.docx` esté guardado con todos los cambios antes de cerrar Word.

2. **Verificar la subida al canal de Teams:** Confirma que el archivo subido al canal de Teams es la versión final (no un borrador intermedio). Si subiste varias versiones, elimina las versiones anteriores del canal para evitar confusión.

3. **Cerrar documentos de referencia:** Cierra cualquier pestaña del navegador que hayas abierto durante la práctica (Teams, SharePoint, documentación de referencia) para liberar memoria del navegador antes de la siguiente práctica.

4. **No se requiere eliminar ningún recurso cloud:** Esta práctica no crea ningún recurso en Copilot Studio, Dataverse, Power Automate ni SharePoint. No hay nada que desprovisionar.

> **Nota:** La Ficha de Agente completada en esta práctica es un artefacto permanente del curso. **No la elimines.** La necesitarás como referencia en todas las prácticas posteriores, especialmente en la Práctica 2 (construcción del agente) y la Práctica 4 (integración con Dataverse).

---

## 10. Resumen

### Lo que aprendiste en esta práctica

En esta práctica realizaste el ejercicio de diseño más importante de todo el curso: antes de escribir una sola línea de configuración en Copilot Studio, definiste con precisión **quién** usará el agente, **qué información** le proporcionará, **qué resultados** producirá, **bajo qué reglas** operará y **cuáles son sus límites**. Este trabajo analítico previo es lo que separa a los agentes bien diseñados de los que fallan en producción.

Los conceptos clave que aplicaste:

| Concepto | Aplicación en esta práctica |
|---|---|
| **Cuatro casos de uso de agentes en auditoría** | Analizaste cuáles aplican al escenario de Financiera Andina S.A. |
| **Perfiles de usuario** | Definiste auditor, responsable de proceso y coordinador con sus necesidades y accesos |
| **Entradas estructuradas** | Documentaste seis entradas con tipo de dato, carácter obligatorio y fuente de validación |
| **Salidas diferenciadas** | Distinguiste entre confirmación, alerta y resumen según el resultado de la validación |
| **Reglas de comportamiento** | Estableciste tono, restricción de dominio, escalamiento y transparencia de IA |
| **Alcance explícito** | Delimitaste capacidades, restricciones y condiciones de operación del agente |

### Conexión con las prácticas siguientes

La Ficha de Agente que completaste hoy es el mapa que guiará cada decisión técnica del resto del curso:

- **Práctica 2:** Usarás los perfiles de usuario y las reglas de respuesta para configurar las instrucciones del sistema del agente en Copilot Studio.
- **Práctica 3:** Las entradas documentadas en la Sección 2 se convertirán en variables y entidades del agente.
- **Práctica 4:** Las salidas de la Sección 3 se implementarán como acciones de Power Automate y registros en Dataverse.
- **Práctica 5:** El alcance de la Sección 5 guiará la configuración de las respuestas generativas y los temas fuera de dominio.
- **Prácticas 6 y 7:** Las reglas de la Sección 4 serán el criterio de evaluación durante las pruebas de extremo a extremo.

### Recursos de referencia

| Recurso | Enlace | Relevancia |
|---|---|---|
| Documentación oficial de Microsoft Copilot Studio | [learn.microsoft.com/es-es/microsoft-copilot-studio](https://learn.microsoft.com/es-es/microsoft-copilot-studio/fundamentals-what-is-copilot-studio) | Capacidades técnicas del agente |
| Marco Internacional de Auditoría Interna (IIA) | [theiia.org/standards](https://www.theiia.org/en/standards/2024-standards/global-internal-audit-standards/) | Fundamento de los casos de uso de auditoría |
| Microsoft Power Automate — Introducción | [learn.microsoft.com/es-es/power-automate](https://learn.microsoft.com/es-es/power-automate/getting-started) | Contexto de las salidas automatizadas |
| Microsoft Dataverse — Descripción general | [learn.microsoft.com/es-es/power-apps/maker/data-platform](https://learn.microsoft.com/es-es/power-apps/maker/data-platform/data-platform-intro) | Contexto del almacenamiento de registros |
| ISACA — Uso de IA en Auditoría Interna | [isaca.org/resources](https://www.isaca.org/resources/isaca-journal/issues/2023/volume-1/using-ai-in-internal-audit) | Buenas prácticas y consideraciones éticas |

---

> **Recordatorio final:** La calidad de todo lo que construirás en las prácticas 2 a 7 depende directamente de la calidad de la Ficha de Agente que completaste hoy. Si tienes dudas sobre alguna sección, resuélvelas con tu instructor antes de avanzar. Un diseño sólido ahora evitará horas de corrección técnica más adelante.

---
LAB_END---
