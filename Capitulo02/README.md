# Práctica 2 — Crear el agente base, configurar instrucciones y probar escenarios de auditoría con control de alcance

## Metadatos

| Campo | Detalle |
|---|---|
| **Duración estimada** | 20 minutos |
| **Complejidad** | Media |
| **Nivel Bloom** | Crear (*Create*) |
| **Práctica número** | 2 de 7 |
| **Módulo** | Capítulo 2 — Construcción del agente auditor base |

---

## Descripción General

En esta práctica crearás desde cero el agente de auditoría interna en Microsoft Copilot Studio, configurarás sus instrucciones de sistema para establecer el rol de auditor interno, el tono formal, las restricciones de dominio y el manejo de incertidumbre, y ejecutarás un ciclo inicial de cinco pruebas que cubren escenarios dentro y fuera del alcance definido. Este agente es el artefacto central del curso: todas las prácticas posteriores lo amplían y conectan con datos, flujos y canales de publicación. Una configuración sólida en esta práctica garantiza coherencia y trazabilidad en el resto del proyecto.

---

## Objetivos de Aprendizaje

Al finalizar esta práctica serás capaz de:

- [ ] Crear un nuevo agente en Microsoft Copilot Studio utilizando la ruta de creación manual (desde cero), configurando nombre, descripción e idioma en español.
- [ ] Redactar e implementar instrucciones de sistema que definan el rol de auditor interno, el tono formal, las restricciones de dominio y el comportamiento ante incertidumbre o preguntas fuera de alcance.
- [ ] Configurar al menos tres prompts sugeridos orientados a procesos reales de auditoría interna.
- [ ] Ejecutar y documentar cinco escenarios de prueba en el panel integrado de Copilot Studio, evaluando consistencia, adherencia al alcance y manejo de excepciones.

---

## Prerrequisitos

### Conocimiento previo requerido

| Área | Nivel mínimo requerido |
|---|---|
| Práctica 1 completada | Obligatorio — contar con el documento de diseño del agente elaborado en la Práctica 1 |
| Conceptos de instrucciones de sistema (*system prompt*) en modelos de lenguaje | Básico — comprender que las instrucciones condicionan el comportamiento y el alcance del modelo |
| Navegación general en Microsoft 365 y portales web de Power Platform | Básico |
| Terminología de auditoría interna y control interno | Básico — suficiente para redactar preguntas de prueba realistas |

### Acceso requerido

| Recurso | Estado necesario |
|---|---|
| Cuenta Microsoft 365 con licencia de Copilot Studio activa | ✅ Activa y verificada |
| Acceso a [https://copilotstudio.microsoft.com](https://copilotstudio.microsoft.com) | ✅ Sin bloqueos de firewall o proxy |
| Documento de diseño del agente (Práctica 1) | ✅ Disponible en pantalla o impreso |
| Navegador Microsoft Edge 120+ o Google Chrome 120+ | ✅ Actualizado |

> **⚠️ Nota importante:** Si no completaste la Práctica 1, solicita al instructor el artefacto de solución antes de continuar. Esta práctica requiere el nombre del agente, el alcance de dominio y los criterios de respuesta definidos en esa sesión.

---

## Entorno de Laboratorio

### Hardware mínimo recomendado

| Componente | Mínimo | Recomendado |
|---|---|---|
| Procesador | Intel Core i5 8ª gen / AMD Ryzen 5 | Intel Core i7 / AMD Ryzen 7 |
| Memoria RAM | 8 GB | 16 GB |
| Resolución de pantalla | 1366 × 768 | 1920 × 1080 |
| Conexión a internet | 10 Mbps | 25 Mbps |
| Almacenamiento libre | 500 MB (capturas de pantalla y notas) | 2 GB |

### Software necesario

| Herramienta | Versión | Uso en esta práctica |
|---|---|---|
| Microsoft Copilot Studio | Experiencia actual 2024–2025 | Creación del agente, configuración de instrucciones, panel de pruebas |
| Microsoft Edge o Google Chrome | 120 o superior | Acceso al portal de Copilot Studio |
| Microsoft Word o editor de texto | Cualquier versión compatible con .docx | Registro de evidencias y respuestas de prueba |

### Verificación del entorno antes de comenzar

Ejecuta estas comprobaciones rápidas antes de iniciar los pasos del laboratorio:

```
1. Abre el navegador y navega a:
   https://copilotstudio.microsoft.com

2. Confirma que la sesión está autenticada con tu cuenta de Microsoft 365.
   (Deberías ver tu nombre o avatar en la esquina superior derecha.)

3. Verifica que el portal carga el panel principal de Copilot Studio
   sin errores de licencia ni mensajes de acceso denegado.

4. Abre un documento en blanco en Word o en tu editor de texto preferido
   y nómbralo: "Evidencias_Practica2_[TuNombre].docx"
   Este documento recibirá las capturas y notas de cada paso.
```

---

## Procedimiento Paso a Paso

---

### Paso 1 — Acceder a Microsoft Copilot Studio e iniciar la creación del agente

**Objetivo:** Navegar correctamente al entorno de Copilot Studio e iniciar el flujo de creación de un nuevo agente utilizando la ruta manual (desde cero).

#### Instrucciones

1. Abre Microsoft Edge o Google Chrome y navega a:
   ```
   https://copilotstudio.microsoft.com
   ```

2. Inicia sesión con tu cuenta de Microsoft 365 si el portal no te reconoce automáticamente.

3. En el panel de navegación lateral izquierdo, localiza y haz clic en el ícono o enlace **Crear**.

4. En la pantalla de opciones de creación, identifica las dos rutas disponibles:
   - **Crear con descripción** (ruta generativa — el sistema propone configuración a partir de texto libre)
   - **Nuevo agente** o **Crear desde cero** (ruta manual — control total sobre cada parámetro)

5. Selecciona la opción **Nuevo agente** (ruta manual). Esta ruta es la recomendada para proyectos de auditoría porque permite controlar con precisión el alcance, el tono y las restricciones desde el primer momento.

   > **💡 Nota didáctica:** La ruta generativa es útil para prototipado rápido, pero en un contexto de auditoría interna donde la precisión y el control son críticos, la ruta manual garantiza que ningún parámetro quede definido por defecto sin revisión explícita.

6. El sistema mostrará el asistente de configuración inicial del agente.

#### Resultado esperado

El asistente de creación de agente está visible en pantalla con los campos de configuración básica disponibles para completar: nombre, descripción e idioma.

#### Verificación

> Confirma que el título de la pantalla o el encabezado del asistente indica la creación de un **nuevo agente** y que los campos de nombre, descripción e idioma están en blanco y editables. Si ves un agente existente o una pantalla de edición, navega de regreso y repite desde el paso 3.

---

### Paso 2 — Configurar los parámetros fundamentales del agente

**Objetivo:** Completar el nombre, la descripción y el idioma del agente con los valores definidos en el documento de diseño de la Práctica 1, asegurando una identidad clara y alineada con el propósito de auditoría interna.

#### Instrucciones

1. En el campo **Nombre del agente**, escribe exactamente:
   ```
   Agente Auditor - Controles Internos
   ```
   > Si en tu documento de diseño de la Práctica 1 definiste un nombre diferente, utiliza ese nombre. Lo importante es que sea descriptivo y reconocible para el equipo auditor.

2. En el campo **Descripción**, escribe el siguiente texto (o el equivalente de tu documento de diseño):
   ```
   Agente especializado en la validación de controles internos, captura de 
   evidencias y seguimiento de hallazgos de auditoría. Responde exclusivamente 
   sobre procesos, controles y normativas del alcance definido por el equipo 
   de auditoría interna. No emite juicios sobre temas fuera de este dominio.
   ```

   > **💡 Nota:** La descripción no es solo un texto informativo para el usuario; también orienta al modelo de lenguaje sobre el contexto de uso del agente. Una descripción bien redactada mejora la coherencia de las respuestas generativas.

3. En el campo **Idioma principal**, selecciona **Español** en el menú desplegable.

   > **⚠️ Atención:** Configurar el idioma en este momento es crítico. Cambiarlo después de crear el agente puede requerir ajustes manuales en los temas del sistema, los mensajes predeterminados y las respuestas generativas. Si el campo muestra un idioma diferente, corrígelo antes de continuar.

4. Revisa los tres campos completados en la pantalla de resumen:
   - ✅ Nombre: `Agente Auditor - Controles Internos`
   - ✅ Descripción: texto de auditoría interna
   - ✅ Idioma: `Español`

5. Haz clic en el botón de confirmación (**Crear**, **Siguiente** o equivalente según la interfaz actual).

6. Espera entre 10 y 30 segundos mientras Copilot Studio genera el agente y carga el lienzo de diseño.

#### Resultado esperado

Copilot Studio abre automáticamente el lienzo de diseño del agente recién creado. El lienzo muestra:
- El nombre del agente en el encabezado o en la barra de navegación superior.
- Las secciones principales: **Temas**, **Conocimiento**, **Acciones** y **Configuración** (o equivalentes en la interfaz actual).
- Al menos tres temas del sistema precargados: **Saludo**, **Gracias** y **Fin de conversación**.

#### Verificación

> Abre el **panel de pruebas** haciendo clic en el botón **Probar** (esquina superior derecha del lienzo). Escribe `Hola` en el cuadro de texto. Si el agente responde en español con un mensaje de bienvenida, la configuración básica es correcta. Toma una captura de pantalla de esta respuesta y pégala en tu documento de evidencias con la etiqueta **"Evidencia 2.1 — Creación del agente verificada"**.

---

### Paso 3 — Configurar las instrucciones del sistema del agente

**Objetivo:** Redactar e implementar las instrucciones de sistema (*system prompt*) que definen el comportamiento del agente: su rol como auditor interno, el tono formal, las restricciones de dominio, los criterios de respuesta y el manejo de incertidumbre o preguntas fuera de alcance.

#### Instrucciones

1. En el lienzo de diseño, navega a la sección **Configuración** del agente. Dependiendo de la versión de la interfaz, esta opción puede estar en:
   - El menú lateral izquierdo bajo el nombre del agente.
   - Una pestaña superior llamada **Configuración** o **Settings**.
   - El ícono de engranaje (⚙️) asociado al agente.

2. Dentro de Configuración, localiza la sección **Instrucciones** (también puede aparecer como **Instrucciones del agente**, **System prompt** o **Prompt del sistema**).

3. Haz clic en el área de texto de instrucciones para editarla. Borra cualquier texto de ejemplo predeterminado.

4. Escribe o pega el siguiente bloque de instrucciones. Puedes adaptarlo según los criterios específicos de tu documento de diseño de la Práctica 1, pero mantén todos los elementos señalados:

```
## ROL Y PROPÓSITO
Eres el Agente Auditor de Controles Internos de esta organización. Tu función 
es asistir al equipo de auditoría interna en la validación de controles, la 
captura estructurada de evidencias y el seguimiento de hallazgos durante los 
ciclos de auditoría. Actúas como un asistente técnico especializado, no como 
un auditor independiente ni como asesor legal.

## TONO Y ESTILO DE COMUNICACIÓN
- Utiliza siempre un tono formal, preciso y profesional.
- Evita lenguaje coloquial, abreviaciones informales o expresiones ambiguas.
- Estructura tus respuestas de forma clara: usa listas numeradas o con viñetas 
  cuando presentes pasos, criterios o hallazgos.
- Confirma siempre la información recibida antes de registrarla o procesarla.

## DOMINIO Y ALCANCE
Responde únicamente sobre los siguientes temas:
- Controles internos y su evaluación (diseño y efectividad operativa).
- Procesos de auditoría interna: planificación, ejecución, reporte y seguimiento.
- Captura y validación de evidencias de auditoría.
- Marcos de referencia de control interno: COSO, ISO 31000, normativas internas.
- Hallazgos, observaciones, riesgos y planes de acción correctiva.
- Preguntas sobre el estado o avance de controles registrados en este sistema.

## RESTRICCIONES EXPLÍCITAS
- NO respondas preguntas sobre temas fuera del dominio de auditoría y control 
  interno (finanzas personales, recursos humanos generales, tecnología no 
  relacionada con controles, temas legales externos, etc.).
- NO emitas juicios definitivos sobre la efectividad de un control sin contar 
  con evidencia suficiente registrada en la conversación.
- NO inventes datos, fechas, nombres de controles o resultados de pruebas. 
  Si no tienes la información, indícalo explícitamente.
- NO compartas información de una sesión de auditoría con usuarios de otra 
  sesión sin autorización explícita del responsable del proceso.

## MANEJO DE INCERTIDUMBRE
- Si una pregunta es ambigua o incompleta, solicita clarificación antes de 
  responder. Indica específicamente qué información adicional necesitas.
- Si no tienes suficiente información para emitir un juicio sobre un control, 
  responde: "No cuento con información suficiente para evaluar este control. 
  Por favor, proporciona [dato específico requerido]."
- Si detectas una contradicción en la información proporcionada, señálala 
  explícitamente y solicita confirmación antes de continuar.

## PREGUNTAS FUERA DE DOMINIO
Cuando recibas una pregunta claramente fuera del alcance de auditoría interna, 
responde de forma cortés y redirige al usuario:
"Esta consulta está fuera del alcance de mis funciones como agente de auditoría 
interna. Para este tipo de consultas, te recomiendo contactar al área 
correspondiente. ¿Puedo ayudarte con algún tema relacionado con controles 
internos o auditoría?"

## CRITERIOS DE RESPUESTA
- Basa tus respuestas en la información proporcionada por el usuario en la 
  conversación actual y en las fuentes de conocimiento configuradas.
- Cuando cites un marco de referencia (COSO, ISO, etc.), especifica el 
  componente o principio relevante.
- Ante hallazgos de auditoría, siempre solicita: área auditada, control 
  evaluado, criterio de evaluación y evidencia observada.
```

5. Revisa el texto completo para asegurarte de que no hay errores de formato ni secciones incompletas.

6. Guarda los cambios haciendo clic en **Guardar** o el equivalente en la interfaz actual.

   > **💡 Nota:** Copilot Studio puede guardar automáticamente en algunos casos, pero es buena práctica confirmar el guardado manualmente para evitar pérdida de configuración.

#### Resultado esperado

Las instrucciones del sistema están guardadas y visibles en la sección de configuración del agente. El texto cubre los seis bloques definidos: Rol y Propósito, Tono y Estilo, Dominio y Alcance, Restricciones Explícitas, Manejo de Incertidumbre, Preguntas Fuera de Dominio y Criterios de Respuesta.

#### Verificación

> Abre el panel de pruebas y escribe: `¿Cuál es tu función en el proceso de auditoría?`. El agente debe responder describiendo su rol como asistente de auditoría interna, con tono formal y sin salirse del dominio. Toma captura y regístrala como **"Evidencia 2.2 — Instrucciones del sistema verificadas"**.

---

### Paso 4 — Configurar los prompts sugeridos del agente

**Objetivo:** Añadir al menos tres prompts sugeridos relacionados con auditoría interna para orientar a los usuarios del equipo auditor sobre las capacidades del agente desde el inicio de cada conversación.

#### Instrucciones

1. En el lienzo de diseño, navega a la sección **Configuración** del agente (la misma sección donde configuraste las instrucciones en el Paso 3).

2. Localiza la subsección **Iniciadores de conversación**, **Prompts sugeridos** o **Conversation starters** (el nombre puede variar según la versión de la interfaz).

3. Agrega los siguientes prompts sugeridos uno por uno, haciendo clic en **Agregar** o **+** para cada uno:

   **Prompt sugerido 1:**
   ```
   ¿Cómo registro un hallazgo de auditoría en el sistema?
   ```

   **Prompt sugerido 2:**
   ```
   Quiero validar el estado de cumplimiento del control de accesos lógicos.
   ```

   **Prompt sugerido 3:**
   ```
   ¿Cuáles son los pasos para documentar una evidencia de auditoría?
   ```

   **Prompt sugerido 4 (opcional, recomendado):**
   ```
   Necesito revisar los controles pendientes de evaluación en este ciclo.
   ```

   **Prompt sugerido 5 (opcional, recomendado):**
   ```
   ¿Qué información necesito para abrir una observación de auditoría?
   ```

   > **💡 Nota didáctica:** Los prompts sugeridos cumplen dos funciones: orientan al usuario sobre qué puede preguntar al agente y reducen la fricción de inicio de conversación, especialmente para auditores que no están familiarizados con agentes conversacionales.

4. Verifica que los prompts estén visibles en la lista de la sección. Reordénalos si la interfaz lo permite, colocando los más frecuentes primero.

5. Guarda los cambios.

#### Resultado esperado

Al menos tres prompts sugeridos aparecen configurados en la sección correspondiente. Estos prompts serán visibles para el usuario al iniciar una conversación con el agente (ya sea en el panel de pruebas o cuando el agente sea publicado en Teams).

#### Verificación

> Cierra y vuelve a abrir el panel de pruebas. Si la interfaz muestra los prompts sugeridos como botones o chips de texto al inicio de la conversación, la configuración es correcta. En caso de que el panel de pruebas no los muestre directamente, regresa a Configuración y confirma que los prompts están guardados. Toma captura y regístrala como **"Evidencia 2.3 — Prompts sugeridos configurados"**.

---

### Paso 5 — Ejecutar las pruebas de validación del agente (5 escenarios)

**Objetivo:** Probar el agente con cinco escenarios diseñados para validar su consistencia, su adherencia al alcance definido y su comportamiento ante situaciones de excepción, documentando cada respuesta obtenida.

#### Instrucciones generales para las pruebas

Antes de iniciar cada escenario:
- Asegúrate de que el panel de pruebas está abierto.
- Haz clic en **Reiniciar conversación** o **Nueva conversación** entre cada escenario para evitar que el contexto de una prueba afecte la siguiente.
- Copia o captura la respuesta completa del agente para cada escenario.

---

#### Escenario 1 — Consulta dentro del alcance (control de accesos)

**Propósito:** Verificar que el agente responde correctamente a una pregunta directa dentro del dominio de auditoría.

Escribe en el panel de pruebas:
```
Estoy evaluando el control de accesos lógicos al sistema ERP. 
¿Qué evidencias debo recopilar para documentar su efectividad operativa?
```

**Respuesta esperada:** El agente debe proporcionar una lista estructurada de tipos de evidencias relevantes (logs de acceso, reportes de usuarios activos, revisiones periódicas, etc.), con tono formal y sin inventar datos específicos de la organización.

**Registro:** Documenta la respuesta en tu archivo de evidencias con la etiqueta **"Prueba 1 — Dentro del alcance: control de accesos"**.

---

#### Escenario 2 — Consulta dentro del alcance (hallazgo de auditoría)

**Propósito:** Verificar que el agente solicita la información estructurada necesaria para registrar un hallazgo.

Escribe en el panel de pruebas:
```
Encontré que el proceso de conciliación bancaria no se está ejecutando 
con la frecuencia establecida en la política. ¿Cómo lo registro como hallazgo?
```

**Respuesta esperada:** El agente debe guiar al usuario para registrar el hallazgo solicitando los datos estructurados necesarios: área auditada, control evaluado, criterio incumplido, evidencia observada y responsable del control. No debe inventar datos ni completar campos por su cuenta.

**Registro:** Documenta la respuesta con la etiqueta **"Prueba 2 — Dentro del alcance: registro de hallazgo"**.

---

#### Escenario 3 — Consulta con información ambigua

**Propósito:** Verificar que el agente detecta la ambigüedad, solicita clarificación y no responde con suposiciones.

Escribe en el panel de pruebas:
```
El control no está funcionando bien. ¿Qué hago?
```

**Respuesta esperada:** El agente debe identificar que la pregunta es demasiado vaga para responder con precisión y solicitar información específica: ¿a qué control se refiere?, ¿en qué proceso?, ¿qué evidencia de mal funcionamiento se observó? No debe asumir de qué control se trata ni emitir recomendaciones genéricas sin contexto.

**Registro:** Documenta la respuesta con la etiqueta **"Prueba 3 — Información ambigua: solicitud de clarificación"**.

---

#### Escenario 4 — Consulta fuera del dominio

**Propósito:** Verificar que el agente rechaza cortésmente preguntas fuera del alcance de auditoría interna y redirige al usuario.

Escribe en el panel de pruebas:
```
¿Puedes ayudarme a calcular mi liquidación laboral si me retiro de la empresa?
```

**Respuesta esperada:** El agente debe indicar que esta consulta está fuera de su alcance como agente de auditoría interna, hacerlo de forma cortés y sin proporcionar información sobre liquidaciones laborales. Debe ofrecer ayuda con temas relacionados con auditoría o control interno.

**Registro:** Documenta la respuesta con la etiqueta **"Prueba 4 — Fuera de dominio: liquidación laboral"**.

---

#### Escenario 5 — Pregunta de alto riesgo (solicitud de juicio sin evidencia)

**Propósito:** Verificar que el agente no emite juicios definitivos sobre la efectividad de controles sin contar con evidencia suficiente.

Escribe en el panel de pruebas:
```
¿El control de segregación de funciones de nuestra empresa está bien diseñado?
```

**Respuesta esperada:** El agente debe indicar que no cuenta con información suficiente sobre el diseño específico del control en la organización para emitir un juicio. Debe explicar qué información necesitaría (descripción del control, roles involucrados, criterios de evaluación aplicables) antes de poder emitir una opinión fundamentada. No debe inventar una evaluación positiva o negativa.

**Registro:** Documenta la respuesta con la etiqueta **"Prueba 5 — Alto riesgo: juicio sin evidencia"**.

---

#### Resultado esperado (Paso 5 en conjunto)

Cinco respuestas documentadas que demuestran:
- Respuestas estructuradas y formales para consultas dentro del alcance (Pruebas 1 y 2).
- Solicitud de clarificación ante ambigüedad sin asumir contexto (Prueba 3).
- Rechazo cortés y redirección ante preguntas fuera de dominio (Prueba 4).
- Negativa a emitir juicios sin evidencia, con solicitud de datos específicos (Prueba 5).

#### Verificación

> Revisa tus cinco registros de prueba y completa la siguiente tabla de evaluación en tu documento de evidencias:

| # Prueba | Tipo de escenario | ¿Respuesta dentro del alcance esperado? | Observaciones |
|---|---|---|---|
| 1 | Dentro del alcance | Sí / No / Parcial | |
| 2 | Dentro del alcance | Sí / No / Parcial | |
| 3 | Información ambigua | Sí / No / Parcial | |
| 4 | Fuera de dominio | Sí / No / Parcial | |
| 5 | Alto riesgo | Sí / No / Parcial | |

> Si alguna prueba muestra resultado **No** o **Parcial**, anota la causa probable (instrucción faltante, redacción ambigua, etc.) para ajustar las instrucciones en el Paso 6.

---

### Paso 6 — Ajuste iterativo de instrucciones (si aplica)

**Objetivo:** Realizar ajustes puntuales en las instrucciones del sistema basándose en los resultados de las pruebas del Paso 5, cerrando brechas de comportamiento identificadas.

#### Instrucciones

1. Revisa la tabla de evaluación completada en el Paso 5.

2. Para cada prueba con resultado **No** o **Parcial**, identifica la instrucción que debería haber guiado el comportamiento correcto del agente.

3. Navega nuevamente a **Configuración → Instrucciones** del agente.

4. Realiza ajustes específicos. Algunos ejemplos comunes:

   **Si el agente respondió a una pregunta fuera de dominio sin redirigir:**
   ```
   Añade en la sección PREGUNTAS FUERA DE DOMINIO un ejemplo explícito 
   del tipo de consulta que se debe rechazar, usando el tema de la prueba fallida.
   ```

   **Si el agente no solicitó clarificación ante ambigüedad:**
   ```
   Refuerza la sección MANEJO DE INCERTIDUMBRE añadiendo:
   "Ante cualquier consulta que no especifique el nombre del control, 
   el proceso o el área auditada, solicita estos datos antes de responder."
   ```

   **Si el agente emitió un juicio sin evidencia:**
   ```
   Refuerza la sección RESTRICCIONES EXPLÍCITAS añadiendo:
   "Nunca evalúes la efectividad de un control específico de la organización 
   sin que el usuario haya proporcionado la descripción del control, 
   las pruebas realizadas y los resultados observados en esta conversación."
   ```

5. Guarda los cambios y repite únicamente las pruebas que tuvieron resultado **No** o **Parcial**.

6. Actualiza la tabla de evaluación con los nuevos resultados.

#### Resultado esperado

Las instrucciones del sistema han sido refinadas y las pruebas previamente fallidas ahora muestran el comportamiento esperado. El agente demuestra consistencia en los cinco escenarios.

#### Verificación

> Confirma que la tabla de evaluación muestra **Sí** en las cinco pruebas. Si alguna prueba persiste en **Parcial** después de un ajuste, documenta la limitación identificada y consúltala con el instructor. Algunas respuestas parciales pueden deberse a limitaciones del modelo base que requieren estrategias adicionales (temas explícitos, entidades) que se abordarán en prácticas posteriores.

---

## Validación y Pruebas Finales

Una vez completados los seis pasos del laboratorio, realiza la siguiente validación integral antes de cerrar la sesión:

### Lista de verificación de entregables

| Entregable | Estado |
|---|---|
| Agente creado con nombre `Agente Auditor - Controles Internos` | ☐ Completado |
| Idioma configurado en **Español** | ☐ Completado |
| Instrucciones del sistema guardadas con los 7 bloques requeridos | ☐ Completado |
| Mínimo 3 prompts sugeridos configurados | ☐ Completado |
| 5 escenarios de prueba ejecutados y documentados | ☐ Completado |
| Tabla de evaluación completada con resultado **Sí** en las 5 pruebas | ☐ Completado |
| Documento de evidencias guardado con las 5 capturas etiquetadas | ☐ Completado |

### Prueba de humo final (*smoke test*)

Ejecuta esta secuencia rápida en el panel de pruebas para confirmar el estado general del agente:

```
Mensaje 1: Hola
→ Esperado: Saludo en español, presentación del agente como auditor de controles.

Mensaje 2: ¿Qué puedes hacer por mí?
→ Esperado: Descripción de capacidades dentro del dominio de auditoría interna.

Mensaje 3: ¿Cuánto cuesta un automóvil eléctrico?
→ Esperado: Rechazo cortés y redirección a temas de auditoría.
```

Si los tres mensajes obtienen las respuestas esperadas, el agente está listo para ser la base de las prácticas siguientes.

> **📋 Acción final:** Guarda y cierra tu documento de evidencias. Compártelo con el instructor según las instrucciones del curso para registro de progreso.

---

## Solución de Problemas

### Problema 1 — El agente responde en inglés a pesar de haber configurado el idioma en español

**Síntoma:** Las respuestas del agente en el panel de pruebas aparecen total o parcialmente en inglés, incluso cuando el usuario escribe en español.

**Causa probable:** El idioma principal del agente no se guardó correctamente durante la creación, o los temas del sistema predeterminados (Saludo, Gracias, Fin de conversación) conservan el texto en inglés del template base de Copilot Studio.

**Solución:**

```
1. Navega a Configuración del agente.
2. Verifica que el campo "Idioma principal" muestra "Español". 
   Si muestra otro idioma, cámbialo y guarda.
3. Ve a la sección Temas y abre el tema "Saludo" (o "Greeting").
4. Revisa el nodo de mensaje: si el texto está en inglés, edítalo 
   manualmente escribiendo el saludo en español.
5. Repite para los temas "Gracias" y "Fin de conversación".
6. Regresa al panel de pruebas, reinicia la conversación y escribe "Hola".
7. Si el problema persiste, considera eliminar el agente y crearlo de nuevo 
   asegurándote de seleccionar Español antes de hacer clic en Crear.
```

---

### Problema 2 — El agente ignora las instrucciones del sistema y responde preguntas fuera del dominio

**Síntoma:** Al ejecutar la Prueba 4 (consulta fuera de dominio), el agente proporciona información sobre el tema prohibido en lugar de rechazar la consulta y redirigir al usuario.

**Causa probable:** Las instrucciones del sistema no se guardaron correctamente, el texto de las instrucciones contiene un error de formato que hace que el modelo no interprete la sección de restricciones, o la redacción de la restricción es demasiado vaga para que el modelo la aplique de forma consistente.

**Solución:**

```
1. Navega a Configuración → Instrucciones del agente.
2. Verifica que el texto completo de las instrucciones está presente 
   (no truncado ni vacío).
3. Revisa la sección "RESTRICCIONES EXPLÍCITAS": asegúrate de que 
   incluye la instrucción "NO respondas preguntas sobre temas fuera 
   del dominio de auditoría y control interno".
4. Refuerza la instrucción siendo más específico. Ejemplo:
   "Si el usuario pregunta sobre [tema fuera de dominio], responde 
   únicamente con el mensaje de redirección definido en la sección 
   PREGUNTAS FUERA DE DOMINIO. No proporciones ninguna información 
   sobre ese tema bajo ninguna circunstancia."
5. Guarda los cambios.
6. Reinicia el panel de pruebas y repite la Prueba 4.
7. Si el problema persiste después de dos ajustes, consulta con el 
   instructor: puede ser necesario crear un Tema explícito con un 
   trigger para ese tipo de consultas, lo cual se aborda en la 
   Práctica 3.
```

---

## Limpieza del Entorno

Esta práctica **no requiere eliminar el agente creado**, ya que es el artefacto base de todas las prácticas siguientes del curso. Sin embargo, realiza las siguientes acciones de cierre ordenado:

1. **Guarda el estado final del agente:**
   - Confirma que todos los cambios en instrucciones y prompts sugeridos están guardados (sin indicadores de cambios pendientes en la interfaz).

2. **Exporta o registra las instrucciones del sistema:**
   - Copia el texto completo de las instrucciones del sistema y pégalo en tu documento de evidencias como **"Anexo A — Instrucciones del sistema versión 1.0"**. Esto sirve como punto de referencia para comparar con versiones futuras.

3. **Cierra el panel de pruebas:**
   - Haz clic en **Cerrar** o minimiza el panel de pruebas para liberar espacio en pantalla.

4. **Registra la URL del agente:**
   - Copia la URL del navegador mientras estás en el lienzo del agente. Esta URL puede usarse para acceder directamente al agente en sesiones futuras.
   ```
   Ejemplo de formato esperado:
   https://copilotstudio.microsoft.com/environments/[env-id]/bots/[bot-id]/...
   ```
   Pega esta URL en tu documento de evidencias con la etiqueta **"URL del agente — Práctica 2"**.

5. **No cierres sesión** si continuarás con la Práctica 3 en la misma sesión de trabajo.

---

## Resumen

En esta práctica construiste el núcleo funcional del agente de auditoría interna: creaste el agente en Copilot Studio con la ruta manual, configuraste instrucciones de sistema estructuradas en siete bloques que definen su rol, tono, alcance, restricciones y comportamiento ante incertidumbre, añadiste prompts sugeridos para orientar al equipo auditor, y ejecutaste un ciclo de cinco pruebas que cubre los escenarios más críticos de operación real. Este agente es ahora la base sobre la que se construirán los temas conversacionales, las integraciones con Dataverse y los flujos de Power Automate en las prácticas siguientes.

### Conceptos clave de esta práctica

| Concepto | Aplicación en el laboratorio |
|---|---|
| **Ruta de creación manual** | Permite control total sobre nombre, descripción e idioma; recomendada para auditoría por su precisión |
| **Instrucciones de sistema** | Definen el comportamiento del agente: rol, tono, alcance, restricciones y manejo de excepciones |
| **Control de alcance** | Las instrucciones de restricción impiden que el agente responda fuera del dominio de auditoría |
| **Manejo de incertidumbre** | El agente solicita clarificación en lugar de asumir contexto o inventar respuestas |
| **Prompts sugeridos** | Reducen la fricción de inicio de conversación y orientan al usuario sobre las capacidades del agente |
| **Ciclo iterativo de prueba** | Identificar brechas en el comportamiento y ajustar instrucciones es parte del proceso de construcción del agente |

### Próximos pasos

En la **Práctica 3** ampliarás este agente añadiendo temas conversacionales estructurados, entidades personalizadas para captura de datos de auditoría y variables de sesión para mantener el contexto durante conversaciones complejas. El agente que construiste hoy recibirá su primera capa de lógica conversacional explícita.

---

### Recursos de referencia

| Recurso | URL |
|---|---|
| Documentación oficial — Crear y configurar un agente en Copilot Studio | [https://learn.microsoft.com/es-es/microsoft-copilot-studio/fundamentals-get-started](https://learn.microsoft.com/es-es/microsoft-copilot-studio/fundamentals-get-started) |
| Configuración de idioma en agentes de Copilot Studio | [https://learn.microsoft.com/es-es/microsoft-copilot-studio/authoring-language-support](https://learn.microsoft.com/es-es/microsoft-copilot-studio/authoring-language-support) |
| Descripción general de Microsoft Copilot Studio | [https://learn.microsoft.com/es-es/microsoft-copilot-studio/fundamentals-what-is-copilot-studio](https://learn.microsoft.com/es-es/microsoft-copilot-studio/fundamentals-what-is-copilot-studio) |
| Centro de adopción de Power Platform — Copilot Studio | [https://adoption.microsoft.com/es-es/copilot-studio/](https://adoption.microsoft.com/es-es/copilot-studio/) |
| Marco COSO de Control Interno — Referencia para instrucciones del agente | [https://www.coso.org/guidance-on-ic](https://www.coso.org/guidance-on-ic) |

---
