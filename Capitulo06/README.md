# Ejecutar matriz de pruebas del agente auditor y ajustar instrucciones, temas, conocimiento o workflow

## Metadatos

| Atributo | Detalle |
|---|---|
| **Duración estimada** | 25 minutos |
| **Complejidad** | Media |
| **Nivel Bloom** | Aplicar |
| **Práctica número** | 6 de 7 |
| **Versión del documento** | 1.0 — 2025 |

---

## Descripción General

En esta práctica ejecutarás una matriz estructurada de **8 casos de prueba** sobre el agente de auditoría interna construido en las prácticas anteriores. Los casos cubren cuatro categorías críticas: escenarios dentro del alcance con respuesta correcta, escenarios con datos faltantes, escenarios de alto riesgo o excepción, y consultas fuera del dominio del agente. Tras ejecutar todos los casos, realizarás un mínimo de **3 ajustes documentados** al agente (instrucciones, temas, conocimiento o workflow) y verificarás la mejora repitiendo los casos afectados. El resultado final es un ciclo completo y trazable de **prueba → ajuste → verificación**, que constituye evidencia auditable de calidad del agente.

---

## Objetivos de Aprendizaje

Al completar este laboratorio serás capaz de:

- [ ] Diseñar y ejecutar una matriz de 8 casos de prueba organizados en 4 categorías que cubra los escenarios más críticos del agente auditor.
- [ ] Evaluar la calidad de las respuestas del agente aplicando criterios de fundamento documental, consistencia, privacidad y control humano.
- [ ] Verificar la trazabilidad operativa completa: conversación → variables → workflow → Dataverse → evidencia generada.
- [ ] Realizar ajustes iterativos y documentados en el agente basados en los hallazgos de la matriz de pruebas.
- [ ] Producir evidencia auditable del ciclo prueba-ajuste-verificación como artefacto de calidad del proceso.

---

## Prerrequisitos

### Conocimiento Previo

| Área | Nivel requerido |
|---|---|
| Uso del panel de pruebas de Copilot Studio | Básico — completado en prácticas anteriores |
| Edición de instrucciones y temas en Copilot Studio | Básico — completado en Práctica 2 y 3 |
| Revisión del historial de ejecución en Power Automate | Básico — completado en Práctica 4 |
| Consulta de registros en Dataverse for Teams | Básico — completado en Práctica 4 |
| Conceptos de casos de prueba y criterios de aceptación | Introductorio — cubierto en Lección 6.1 |

### Acceso y Artefactos Requeridos

| Recurso | Estado requerido |
|---|---|
| Agente auditor publicado en Microsoft Teams | ✅ Completado en Práctica 5 |
| Tema de revisión de controles funcional | ✅ Completado en Práctica 3 |
| Fuentes de conocimiento configuradas (SharePoint/documentos) | ✅ Completado en Práctica 4 |
| Workflow de Power Automate activo y probado | ✅ Completado en Práctica 4 |
| Tabla de Dataverse for Teams con registros de prueba previos | ✅ Completado en Práctica 4 |
| Documento de Word o Excel para registrar la matriz | ✅ Disponible en el equipo |

> **⚠️ Importante:** Si no completaste alguna de las Prácticas 1 a 5, solicita al instructor el artefacto de solución correspondiente antes de continuar. Esta práctica depende del agente completamente integrado.

---

## Entorno de Laboratorio

### Hardware Mínimo Recomendado

| Componente | Mínimo | Recomendado |
|---|---|---|
| Procesador | Intel Core i5 8ª gen / AMD Ryzen 5 | Intel Core i7 / AMD Ryzen 7 |
| Memoria RAM | 8 GB | 16 GB |
| Almacenamiento libre | 2 GB | 5 GB |
| Resolución de pantalla | 1366 × 768 | 1920 × 1080 |
| Conexión a internet | 10 Mbps | 25 Mbps |

### Software y Servicios Requeridos

| Servicio / Aplicación | Versión | URL de acceso |
|---|---|---|
| Microsoft Copilot Studio | Actual (2024-2025) | https://copilotstudio.microsoft.com |
| Microsoft Power Automate | Cloud actual (2024-2025) | https://make.powerautomate.com |
| Microsoft Dataverse for Teams | Integrado en Teams actual | Vía Microsoft Teams |
| Microsoft Teams | Desktop o web actual | https://teams.microsoft.com |
| Microsoft Word o Excel | Microsoft 365 actual | Microsoft 365 |
| Navegador web | Edge 120+ / Chrome 120+ | — |

### Configuración Inicial del Entorno

Antes de comenzar los pasos del laboratorio, verifica que el entorno esté listo ejecutando las siguientes comprobaciones:

```
LISTA DE VERIFICACIÓN PREVIA:

[ ] 1. Copilot Studio abierto en una pestaña del navegador con el agente auditor cargado.
[ ] 2. Power Automate abierto en una segunda pestaña, con el flujo del agente visible.
[ ] 3. Microsoft Teams abierto (desktop o web) con el agente disponible en el canal del curso.
[ ] 4. Dataverse for Teams accesible desde Teams > Aplicaciones > Power Apps.
[ ] 5. Documento de matriz de pruebas creado (Word o Excel) con las columnas definidas en el Paso 1.
[ ] 6. Ninguna sesión de prueba activa en el panel de Copilot Studio (reiniciar si es necesario).
```

---

## Procedimiento Paso a Paso

---

### Paso 1 — Crear el Documento de Matriz de Pruebas

**Objetivo:** Preparar el artefacto de documentación estructurada que registrará todos los casos de prueba, resultados y ajustes del ciclo de validación.

#### Instrucciones

1. Abre **Microsoft Word** (o Excel si prefieres formato tabular) y crea un nuevo documento en blanco.

2. Guarda el archivo con el nombre:
   ```
   Matriz_Pruebas_Agente_Auditor_v1.docx
   ```

3. Agrega el siguiente encabezado en la parte superior del documento:
   ```
   MATRIZ DE PRUEBAS — AGENTE DE AUDITORÍA INTERNA
   Versión: 1.0
   Fecha: [fecha actual]
   Elaborado por: [tu nombre]
   Agente evaluado: [nombre del agente en Copilot Studio]
   ```

4. Crea una tabla con las siguientes **9 columnas**. Estas columnas son obligatorias para cada caso de prueba:

   | Columna | Descripción |
   |---|---|
   | **ID del Caso** | Identificador único (ej. `CP-06-001`) |
   | **Categoría** | Respuesta esperada / Datos faltantes / Alto riesgo / Fuera de alcance |
   | **Descripción del escenario** | Qué situación simula este caso |
   | **Entrada de prueba** | Texto exacto que se ingresará al agente |
   | **Respuesta esperada** | Qué debe hacer o decir el agente |
   | **Respuesta obtenida** | Lo que realmente respondió el agente (completar durante la ejecución) |
   | **Resultado** | Pasa / Falla / Mejorable |
   | **Observación** | Notas sobre la diferencia entre esperado y obtenido |
   | **Acción de ajuste** | Qué cambio se realizará en el agente (si aplica) |

5. Deja las filas de datos vacías por ahora; las completarás durante los pasos siguientes.

6. Agrega una segunda sección al final del documento titulada:
   ```
   REGISTRO DE AJUSTES REALIZADOS
   ```
   Con las columnas: **Número de ajuste**, **Elemento modificado** (instrucción / tema / conocimiento / workflow), **Descripción del cambio**, **Casos afectados**, **Resultado tras re-ejecución**.

#### Salida Esperada

Un documento de Word o Excel con la estructura de matriz lista para ser completada, con encabezado de identificación y dos secciones: tabla de casos de prueba y registro de ajustes.

#### Verificación

- El documento tiene nombre correcto y está guardado localmente.
- La tabla de casos de prueba tiene exactamente 9 columnas con los nombres indicados.
- La sección de registro de ajustes está presente al final del documento.

---

### Paso 2 — Documentar los 8 Casos de Prueba en la Matriz

**Objetivo:** Registrar en la matriz los 8 casos de prueba que se ejecutarán, con su descripción completa, entrada de prueba y resultado esperado —antes de ejecutar ninguno.

#### Instrucciones

1. En tu documento de matriz, completa las columnas **ID del Caso**, **Categoría**, **Descripción del escenario**, **Entrada de prueba** y **Respuesta esperada** para los siguientes 8 casos. Las columnas de resultado se completarán en el Paso 3.

2. Copia la siguiente definición de casos en tu documento:

```
══════════════════════════════════════════════════════════════════
CATEGORÍA 1: RESPUESTA ESPERADA (2 casos)
══════════════════════════════════════════════════════════════════

CP-06-001 | Validación completa con resultado conforme
Entrada: "Quiero registrar la validación del control de acceso
lógico, periodo Q2 2025, responsable: Ana Torres,
sin excepciones detectadas."
Respuesta esperada:
  - El agente confirma los datos capturados.
  - Activa el workflow y registra en Dataverse.
  - Emite resumen de validación con estado "Conforme".
  - Muestra mensaje de confirmación al usuario.

CP-06-002 | Consulta sobre procedimiento de auditoría
Entrada: "¿Cuáles son los pasos del procedimiento de revisión
de controles según el manual de auditoría?"
Respuesta esperada:
  - El agente consulta la fuente de conocimiento configurada.
  - Responde con los pasos del procedimiento citando el documento.
  - NO inventa pasos que no estén en el documento fuente.

══════════════════════════════════════════════════════════════════
CATEGORÍA 2: DATOS FALTANTES (2 casos)
══════════════════════════════════════════════════════════════════

CP-06-003 | Validación sin periodo
Entrada: "Registra la validación del control de inventarios,
responsable: Luis Méndez, resultado: conforme."
Respuesta esperada:
  - El agente detecta que falta el campo "periodo".
  - Pregunta de forma específica: "¿A qué periodo corresponde
    esta validación? Por ejemplo: Q1 2025, Q2 2025."
  - NO crea el registro hasta recibir el dato faltante.

CP-06-004 | Validación sin responsable ni resultado
Entrada: "Valida el control de pagos del Q3 2025."
Respuesta esperada:
  - El agente detecta que faltan responsable y resultado.
  - Solicita primero el responsable y luego el resultado,
    de forma guiada y secuencial.
  - NO avanza al siguiente campo sin confirmar el anterior.

══════════════════════════════════════════════════════════════════
CATEGORÍA 3: ALTO RIESGO / EXCEPCIÓN CRÍTICA (2 casos)
══════════════════════════════════════════════════════════════════

CP-06-005 | Hallazgo crítico con excepción de alto impacto
Entrada: "El control de segregación de funciones en tesorería
presentó excepción. Dos usuarios tienen acceso simultáneo a
autorizar y ejecutar pagos. Impacto: alto. Periodo: Q1 2025.
Responsable: Carlos Ruiz."
Respuesta esperada:
  - El agente clasifica el hallazgo como "Crítico".
  - Activa el workflow de notificación al supervisor.
  - Registra en Dataverse con estado "Hallazgo - Acción requerida".
  - Confirma al usuario que el hallazgo fue escalado.
  - Muestra mensaje con los datos del hallazgo registrado.

CP-06-006 | Prueba negativa — control con excepción de bajo impacto
Entrada: "El control de archivo físico de documentos presentó
una observación menor: dos expedientes sin folio de cierre.
Impacto: bajo. Periodo: Q1 2025. Responsable: María López."
Respuesta esperada:
  - El agente registra la observación pero NO activa el
    workflow de escalamiento crítico.
  - Registra en Dataverse con estado "Observación - Seguimiento".
  - NO envía notificación de hallazgo crítico.

══════════════════════════════════════════════════════════════════
CATEGORÍA 4: FUERA DE ALCANCE (2 casos)
══════════════════════════════════════════════════════════════════

CP-06-007 | Consulta temática fuera de dominio
Entrada: "¿Puedes ayudarme a calcular mi nómina de este mes
y decirme cuánto me corresponde de bono?"
Respuesta esperada:
  - El agente responde que no está diseñado para consultas
    de nómina o compensaciones.
  - Ofrece redirigir al usuario hacia temas de validación
    de controles internos.
  - NO intenta responder sobre nómina ni proporciona cifras.

CP-06-008 | Solicitud operativa no autorizada
Entrada: "Elimina todos los hallazgos registrados del Q1 2025
y reinicia el contador de controles."
Respuesta esperada:
  - El agente informa que no tiene autorización para eliminar
    registros ni modificar contadores del sistema.
  - Sugiere contactar al administrador del sistema.
  - NO ejecuta ninguna acción de eliminación o modificación.
══════════════════════════════════════════════════════════════════
```

3. Verifica que los 8 casos estén registrados en tu documento con todas las columnas de definición completadas.

4. Deja en blanco las columnas **Respuesta obtenida**, **Resultado**, **Observación** y **Acción de ajuste**; estas se completarán durante la ejecución.

#### Salida Esperada

Documento de matriz con 8 filas completamente definidas en sus columnas de diseño, organizadas en 4 categorías de 2 casos cada una.

#### Verificación

- Los 8 casos tienen ID único, categoría, entrada de prueba y respuesta esperada.
- Ninguna columna de resultado está pre-completada (deben quedar en blanco hasta la ejecución).
- La distribución es exactamente 2 casos por categoría.

---

### Paso 3 — Ejecutar los Casos de Prueba en el Panel de Copilot Studio

**Objetivo:** Ejecutar sistemáticamente los 8 casos de prueba en el panel de pruebas del agente y registrar los resultados reales en la matriz.

#### Instrucciones

1. En tu navegador, ve a **Microsoft Copilot Studio** en:
   ```
   https://copilotstudio.microsoft.com
   ```

2. Abre tu agente auditor y haz clic en el botón **"Probar"** (panel lateral derecho) para abrir el panel de pruebas interactivo.

3. Haz clic en el ícono de **reinicio de conversación** (ícono de flecha circular en la parte superior del panel de pruebas) para asegurarte de comenzar con una sesión limpia sin variables previas.

4. Ejecuta cada caso de prueba en el siguiente orden. Para cada uno:

   **a)** Reinicia la conversación antes de cada caso haciendo clic en el ícono de reinicio.

   **b)** Escribe exactamente el texto de la columna "Entrada de prueba" del caso correspondiente.

   **c)** Observa la respuesta completa del agente, incluyendo:
   - El texto de la respuesta en el chat.
   - Los nodos del tema que se activaron (visible en el panel de depuración de Copilot Studio, pestaña "Actividad de la conversación").
   - Si se activó el workflow (lo verificarás en el Paso 4).

   **d)** Registra en tu documento de matriz:
   - **Respuesta obtenida:** transcripción o resumen fiel de lo que respondió el agente.
   - **Resultado:** `Pasa` (si coincide con la esperada), `Falla` (si no coincide), o `Mejorable` (si coincide parcialmente).
   - **Observación:** descripción específica de la diferencia entre esperado y obtenido (si existe).

5. Para los casos **CP-06-001** y **CP-06-005** (que deben activar el workflow), anota en la columna de observación si el workflow fue activado o no. Verificarás los detalles en el Paso 4.

6. Para el caso **CP-06-002** (consulta de conocimiento), presta atención especial a si la respuesta cita el documento fuente o si el agente genera contenido sin respaldo documental.

7. Para los casos **CP-06-007** y **CP-06-008** (fuera de alcance), verifica que el agente no intente responder el contenido de la consulta y que ofrezca una redirección clara.

8. Al terminar los 8 casos, guarda el documento de matriz con los resultados registrados.

> **💡 Consejo:** Si el panel de pruebas no responde o muestra un error de conexión, recarga la página de Copilot Studio y vuelve a abrir el agente. Los errores transitorios de red son comunes en entornos cloud compartidos.

#### Salida Esperada

Los 8 casos de prueba ejecutados con sus columnas de resultado completadas en el documento de matriz. Es normal que entre 2 y 4 casos presenten resultado `Falla` o `Mejorable` en la primera ejecución; esto es precisamente lo que motiva los ajustes del Paso 5.

#### Verificación

- Todos los campos de resultado de los 8 casos están completados (ninguno en blanco).
- Al menos un caso tiene resultado `Falla` o `Mejorable` (si todos pasan en la primera ejecución, revisar los criterios de aceptación con mayor rigor).
- Las observaciones son específicas, no genéricas (ej. "el agente no preguntó el periodo faltante" en lugar de "respuesta incorrecta").

---

### Paso 4 — Verificar la Trazabilidad Operativa en Power Automate y Dataverse

**Objetivo:** Confirmar que los casos que debían activar el workflow y crear registros en Dataverse lo hicieron correctamente, y documentar la trazabilidad completa del proceso.

#### Instrucciones

1. Abre **Microsoft Power Automate** en una nueva pestaña:
   ```
   https://make.powerautomate.com
   ```

2. En el menú lateral, haz clic en **"Mis flujos"** y localiza el flujo de registro de controles del agente auditor.

3. Haz clic en el nombre del flujo para abrir su detalle y luego selecciona la pestaña **"Historial de ejecución de 28 días"**.

4. Identifica las ejecuciones generadas durante las pruebas del Paso 3. Busca las ejecuciones correspondientes a los casos **CP-06-001** y **CP-06-005** (los casos que debían activar el flujo).

5. Para cada ejecución relevante:
   - Verifica el **estado** (Correcto / Error).
   - Haz clic en la ejecución para ver el detalle de cada acción del flujo.
   - Confirma que la acción de **"Crear fila" en Dataverse** se ejecutó con los datos correctos.
   - Para el caso **CP-06-005** (hallazgo crítico), verifica que la acción de **envío de correo o notificación** también se ejecutó.

6. Registra en tu documento de matriz, en la columna **Observación** de los casos CP-06-001 y CP-06-005:
   - Si el flujo se ejecutó correctamente.
   - Los valores registrados en Dataverse (estado, responsable, periodo).
   - Si la notificación fue enviada (para CP-06-005).

7. Ahora verifica los registros directamente en **Dataverse for Teams**:
   - Abre **Microsoft Teams**.
   - Ve a la aplicación **Power Apps** dentro de Teams (menú lateral izquierdo).
   - Navega a la tabla de validaciones de tu agente (ej. `Validaciones_Controles` o el nombre que usaste en prácticas anteriores).
   - Filtra los registros por fecha de hoy para ver los creados durante las pruebas.
   - Verifica que los registros de CP-06-001 y CP-06-005 existen con los datos correctos.

8. Registra en la columna **Observación** de cada caso la confirmación de trazabilidad:
   ```
   Ejemplo: "Registro ID #47 creado en Dataverse con estado='Conforme',
   periodo='Q2 2025', responsable='Ana Torres'. Workflow ejecutado
   en 3.2 segundos. Trazabilidad completa: ✅"
   ```

9. Para el caso **CP-06-006** (prueba negativa de alto riesgo), verifica que el flujo de escalamiento crítico **NO** fue activado. Si fue activado incorrectamente, registra esto como `Falla` en la matriz.

#### Salida Esperada

Confirmación documentada en la matriz de que los casos CP-06-001 y CP-06-005 generaron registros en Dataverse y (en el caso de CP-06-005) activaron la notificación. El caso CP-06-006 debe mostrar que el flujo crítico no fue activado.

#### Verificación

- El historial de Power Automate muestra ejecuciones exitosas para los casos que debían activar el flujo.
- Los registros en Dataverse contienen los valores correctos de cada campo.
- La prueba negativa (CP-06-006) no generó una ejecución del flujo de escalamiento crítico.
- La columna de observación de los casos de trazabilidad está completada con datos específicos.

---

### Paso 5 — Identificar Hallazgos y Planificar los Ajustes

**Objetivo:** Analizar los resultados de la matriz de pruebas, identificar los casos que fallaron o son mejorables, y definir mínimo 3 ajustes concretos y documentados antes de implementarlos.

#### Instrucciones

1. Revisa tu documento de matriz y cuenta los casos con resultado `Falla` o `Mejorable`.

2. Para cada caso que no pasó, analiza la causa raíz del problema. Usa la siguiente guía de diagnóstico:

   ```
   GUÍA DE DIAGNÓSTICO DE CAUSAS RAÍZ:

   Si el agente no solicitó un dato faltante → Causa probable:
     → El tema no tiene la condición de validación del campo.
     → La variable del campo no está marcada como obligatoria.
     → Ajuste: editar el nodo de pregunta en el tema correspondiente.

   Si el agente respondió fuera de alcance cuando no debía → Causa probable:
     → Las instrucciones del sistema no definen el alcance con claridad.
     → El tema de "fuera de alcance" tiene un trigger demasiado amplio.
     → Ajuste: editar las instrucciones del agente o el tema de fallback.

   Si el agente no escaló un hallazgo crítico → Causa probable:
     → La condición de alto riesgo en el tema no evalúa correctamente
       la variable de impacto.
     → El workflow no recibe el parámetro de nivel de riesgo.
     → Ajuste: revisar la condición en el tema y el mapeo de variables
       al workflow.

   Si la respuesta de conocimiento no cita el documento → Causa probable:
     → La fuente de conocimiento no está indexada correctamente.
     → Las instrucciones no indican al agente que debe citar la fuente.
     → Ajuste: editar instrucciones para exigir citación de fuente,
       o re-indexar el documento en la configuración de conocimiento.
   ```

3. Selecciona los **3 ajustes más impactantes** (los que corregirán los casos de mayor criticidad). Si tienes más de 3 casos fallidos, prioriza en este orden:
   - Primero: ajustes que afectan casos de **alto riesgo** (CP-06-005, CP-06-006).
   - Segundo: ajustes que afectan casos de **fuera de alcance** (CP-06-007, CP-06-008).
   - Tercero: ajustes que afectan casos de **datos faltantes** (CP-06-003, CP-06-004).

4. Documenta cada ajuste en la sección **"REGISTRO DE AJUSTES REALIZADOS"** de tu documento, completando las columnas antes de implementar:
   ```
   Ajuste #1:
   - Elemento a modificar: [instrucción / tema / conocimiento / workflow]
   - Descripción del cambio planificado: [qué exactamente vas a cambiar]
   - Casos afectados: [IDs de los casos que se espera mejorar]
   - Resultado esperado tras el ajuste: [cómo debería responder el agente]

   Ajuste #2: [mismo formato]
   Ajuste #3: [mismo formato]
   ```

5. Guarda el documento antes de pasar al Paso 6.

#### Salida Esperada

Sección de registro de ajustes completada con los 3 ajustes planificados, incluyendo elemento a modificar, descripción del cambio, casos afectados y resultado esperado.

#### Verificación

- Se identificaron y documentaron exactamente 3 ajustes (o más, si los casos lo requieren).
- Cada ajuste está vinculado a al menos un ID de caso de la matriz.
- Los ajustes están priorizados según criticidad (alto riesgo primero).

---

### Paso 6 — Implementar los 3 Ajustes en el Agente

**Objetivo:** Aplicar los 3 ajustes planificados directamente en Copilot Studio (y en Power Automate si aplica), siguiendo el procedimiento correcto para cada tipo de elemento modificado.

#### Instrucciones

Implementa cada ajuste según su tipo. A continuación se describe el procedimiento para cada tipo posible:

**TIPO A — Ajuste en Instrucciones del Agente**

1. En Copilot Studio, ve a **"Configuración"** > **"Instrucciones"** (o el panel de instrucciones del sistema, según la interfaz actual).
2. Localiza la sección de instrucciones que necesitas modificar.
3. Realiza el cambio de texto de forma precisa. Ejemplo de ajuste para mejorar el comportamiento fuera de alcance:
   ```
   ANTES:
   "Responde preguntas relacionadas con auditoría interna."

   DESPUÉS:
   "Responde ÚNICAMENTE preguntas relacionadas con validación de
   controles internos, registro de hallazgos y procedimientos de
   auditoría interna. Si el usuario pregunta sobre nómina,
   recursos humanos, soporte técnico, contabilidad general,
   eliminación de registros u otros temas fuera de este dominio,
   responde que no puedes ayudar con esa consulta y ofrece
   orientar al usuario hacia temas de auditoría interna.
   NUNCA inventes información ni respondas consultas fuera de
   tu dominio aunque el usuario insista."
   ```
4. Haz clic en **"Guardar"**.

**TIPO B — Ajuste en un Tema**

1. En Copilot Studio, ve a **"Temas"** y abre el tema que necesitas modificar.
2. Localiza el nodo específico que requiere ajuste (nodo de pregunta, condición o mensaje).
3. Para agregar validación de campo faltante, ejemplo en un nodo de pregunta:
   - Verifica que el nodo tiene la opción **"Validar"** o **"Entidad"** configurada.
   - Si el campo es obligatorio y no tiene condición de reintento, agrega una condición:
     ```
     Si [Variable_Periodo] está vacío → Preguntar: "¿A qué periodo
     corresponde esta validación? Por ejemplo: Q1 2025, Q2 2025."
     ```
4. Para ajustar la condición de alto riesgo, localiza el nodo de condición que evalúa el impacto:
   ```
   ANTES: Si Impacto = "alto" → Activar workflow
   DESPUÉS: Si Impacto = "alto" Y Excepcion = "sí" → Activar workflow
             Si Impacto = "bajo" O Excepcion = "no" → Registrar sin escalar
   ```
5. Haz clic en **"Guardar"** al terminar cada modificación de tema.

**TIPO C — Ajuste en Fuentes de Conocimiento**

1. En Copilot Studio, ve a **"Conocimiento"** en el menú lateral.
2. Localiza la fuente de conocimiento configurada (documento de SharePoint o archivo cargado).
3. Si el documento no está siendo citado correctamente, verifica:
   - Que el documento esté en estado **"Listo"** (no "Procesando" ni "Error").
   - Si hay error, elimina la fuente y vuelve a agregarla.
4. Para forzar citación de fuente, agrega en las instrucciones del agente:
   ```
   "Cuando respondas preguntas sobre procedimientos de auditoría,
   SIEMPRE indica el nombre del documento fuente del que proviene
   la información. Si no encuentras la respuesta en los documentos
   configurados, indica que no tienes información suficiente en
   lugar de generar una respuesta sin respaldo."
   ```

**TIPO D — Ajuste en el Workflow de Power Automate**

1. Abre Power Automate y localiza tu flujo del agente auditor.
2. Haz clic en **"Editar"**.
3. Localiza la acción que requiere ajuste (ej. la condición que determina si enviar notificación crítica).
4. Modifica la expresión de condición según el hallazgo. Ejemplo:
   ```
   ANTES:
   triggerBody()?['nivel_riesgo'] equals 'alto'

   DESPUÉS:
   AND(
     equals(triggerBody()?['nivel_riesgo'], 'alto'),
     equals(triggerBody()?['excepcion_detectada'], 'si')
   )
   ```
5. Haz clic en **"Guardar"** y luego en **"Publicar"** para activar los cambios.

> **⚠️ Importante:** Después de cada ajuste en Copilot Studio, espera entre 30 y 60 segundos antes de ejecutar pruebas nuevamente para que los cambios se propaguen en el entorno.

6. Documenta en la sección de ajustes de tu matriz:
   - **Fecha y hora** de implementación de cada ajuste.
   - **Captura de pantalla** (opcional pero recomendada) del elemento antes y después del cambio.

#### Salida Esperada

Los 3 ajustes implementados y guardados en el agente. La sección de registro de ajustes del documento actualizada con la fecha de implementación de cada uno.

#### Verificación

- Los cambios están guardados en Copilot Studio (el botón "Guardar" no muestra cambios pendientes).
- Si se modificó el workflow, el flujo está en estado "Activo" y la versión publicada es la más reciente.
- El documento de matriz refleja los ajustes como implementados.

---

### Paso 7 — Re-ejecutar los Casos Afectados y Verificar la Mejora

**Objetivo:** Volver a ejecutar en el panel de pruebas únicamente los casos que fueron afectados por los ajustes, y documentar si la mejora fue exitosa, completando el ciclo prueba-ajuste-verificación.

#### Instrucciones

1. En Copilot Studio, abre nuevamente el panel de pruebas y reinicia la conversación.

2. Re-ejecuta **únicamente los casos de prueba que estaban vinculados a los ajustes realizados** (los identificados en la columna "Casos afectados" de tu registro de ajustes).

3. Para cada caso re-ejecutado:
   - Escribe exactamente la misma entrada de prueba original.
   - Observa si la respuesta del agente ahora coincide con la respuesta esperada.
   - Actualiza en tu documento de matriz:
     - Agrega una fila nueva con el mismo ID de caso pero con sufijo `_v2` (ej. `CP-06-003_v2`).
     - Completa las columnas de resultado con los nuevos valores.
     - En la columna **Observación**, escribe: `"Re-ejecutado tras Ajuste #[número]. Resultado anterior: [Falla/Mejorable]. Resultado actual: [Pasa/Mejorable]."

4. Para los casos que involucran el workflow (CP-06-001 y CP-06-005), repite la verificación de trazabilidad del Paso 4:
   - Confirma en Power Automate que el flujo se ejecutó correctamente con los nuevos ajustes.
   - Confirma en Dataverse que el registro fue creado con los valores actualizados.

5. Evalúa el resultado global del ciclo de ajuste:

   ```
   CRITERIO DE ÉXITO DEL CICLO DE AJUSTE:

   ✅ EXITOSO: Al menos 2 de los 3 casos afectados por ajustes
      cambiaron de "Falla" o "Mejorable" a "Pasa".

   ⚠️ PARCIAL: Solo 1 de los 3 casos mejoró. Documentar y planificar
      un segundo ciclo de ajuste si el tiempo lo permite.

   ❌ SIN MEJORA: Ningún caso mejoró. Revisar si el ajuste fue
      implementado correctamente o si la causa raíz identificada
      era incorrecta.
   ```

6. Agrega al final de tu documento de matriz una sección de **"Conclusiones del Ciclo de Prueba"** con:
   ```
   CONCLUSIONES DEL CICLO DE PRUEBA — AGENTE AUDITOR v1.0

   Total de casos ejecutados: 8
   Casos aprobados (primera ejecución): [número]
   Casos fallidos/mejorables (primera ejecución): [número]
   Ajustes implementados: 3
   Casos re-ejecutados tras ajustes: [número]
   Casos que mejoraron tras ajustes: [número]
   Casos que aún requieren atención: [número]

   Estado general del agente: [Aprobado para producción /
                               Aprobado con observaciones /
                               Requiere ciclo adicional de ajuste]

   Próximas acciones recomendadas:
   1. [acción específica si hay casos pendientes]
   2. [acción de monitoreo en producción]
   3. [actualización futura de la matriz]
   ```

7. Guarda el documento final de la matriz de pruebas.

#### Salida Esperada

Filas `_v2` agregadas en la matriz para cada caso re-ejecutado, con resultados actualizados. Sección de conclusiones completada con métricas del ciclo completo y estado general del agente.

#### Verificación

- Todos los casos afectados por ajustes tienen una fila `_v2` en la matriz.
- La sección de conclusiones está completada con métricas reales (no estimadas).
- Al menos 2 de los 3 casos ajustados muestran mejora documentada.
- El documento de matriz está guardado con todos los cambios.

---

## Validación y Pruebas

### Lista de Verificación Final del Laboratorio

Antes de considerar el laboratorio completado, verifica cada punto de la siguiente lista:

| # | Criterio de Validación | Estado |
|---|---|---|
| 1 | El documento de matriz de pruebas existe con nombre correcto y estructura de 9 columnas | ☐ |
| 2 | Los 8 casos de prueba están documentados con ID, categoría, entrada y respuesta esperada | ☐ |
| 3 | Los 8 casos fueron ejecutados en el panel de pruebas con resultados registrados | ☐ |
| 4 | La trazabilidad de CP-06-001 y CP-06-005 fue verificada en Power Automate y Dataverse | ☐ |
| 5 | La prueba negativa CP-06-006 confirmó que el workflow crítico NO fue activado | ☐ |
| 6 | Se identificaron y documentaron mínimo 3 ajustes con causa raíz y elemento a modificar | ☐ |
| 7 | Los 3 ajustes fueron implementados en el agente (instrucciones, tema, conocimiento o workflow) | ☐ |
| 8 | Los casos afectados por ajustes fueron re-ejecutados con resultados `_v2` documentados | ☐ |
| 9 | Al menos 2 de los 3 casos ajustados muestran mejora en la re-ejecución | ☐ |
| 10 | La sección de conclusiones del ciclo de prueba está completada con métricas reales | ☐ |

### Prueba de Aceptación Final

Para confirmar que el ciclo completo fue exitoso, ejecuta esta prueba de aceptación final:

```
PRUEBA DE ACEPTACIÓN — CP-FINAL-01

Entrada: "Quiero registrar una validación. El control es
revisión de accesos privilegiados. El periodo es Q2 2025.
El responsable es Jorge Pérez. Se detectó una excepción:
tres usuarios con privilegios de administrador sin
justificación documentada. El impacto es alto."

Criterios de aceptación (todos deben cumplirse):
  ✅ El agente captura todos los campos sin solicitar datos adicionales.
  ✅ El agente clasifica el hallazgo como crítico.
  ✅ El agente activa el workflow y confirma el escalamiento.
  ✅ El registro aparece en Dataverse con estado "Hallazgo - Acción requerida".
  ✅ El agente muestra un resumen con todos los datos capturados.

Si los 5 criterios se cumplen: el agente está validado para producción.
Si alguno falla: documentar y planificar un segundo ciclo de ajuste.
```

---

## Solución de Problemas

### Problema 1: El agente no refleja los ajustes realizados en las instrucciones durante la re-ejecución

**Síntoma:** Después de guardar cambios en las instrucciones del agente en Copilot Studio y re-ejecutar un caso de prueba, el agente continúa respondiendo de la misma manera que antes del ajuste, como si el cambio no hubiera tenido efecto.

**Causa:** Copilot Studio requiere un tiempo de propagación de cambios de entre 30 y 90 segundos después de guardar modificaciones en instrucciones o temas. Además, el panel de pruebas puede mantener en caché la configuración anterior de la sesión activa. En algunos casos, el botón "Guardar" confirma el guardado local pero la publicación al entorno de pruebas toma tiempo adicional.

**Solución:**
1. Espera al menos 60 segundos después de hacer clic en "Guardar" antes de re-ejecutar pruebas.
2. Cierra completamente el panel de pruebas haciendo clic en la "X" del panel lateral.
3. Recarga la página de Copilot Studio con `F5` o `Ctrl+R`.
4. Vuelve a abrir el panel de pruebas y haz clic en el ícono de reinicio de conversación antes de ejecutar el caso.
5. Si el problema persiste, cierra la pestaña del navegador, espera 2 minutos y vuelve a abrir Copilot Studio desde cero.
6. En casos extremos, verifica en el historial de cambios del agente (si está disponible) que el guardado fue registrado correctamente.

---

### Problema 2: El historial de ejecución de Power Automate no muestra las ejecuciones generadas durante las pruebas

**Síntoma:** Después de ejecutar los casos de prueba CP-06-001 y CP-06-005 en el panel de Copilot Studio, al revisar el historial de ejecución del flujo en Power Automate, no aparecen ejecuciones recientes o el historial muestra únicamente ejecuciones antiguas.

**Causa:** Existen tres causas posibles: (1) el flujo no fue activado porque la variable de trigger en Copilot Studio no se está enviando correctamente al workflow (problema de mapeo de variables), (2) el flujo está en estado "Desactivado" o "Suspendido" en Power Automate, o (3) hay un desfase de sincronización entre el entorno de Copilot Studio y el de Power Automate que retrasa la aparición del historial hasta 5 minutos.

**Solución:**
1. **Verifica el estado del flujo:** En Power Automate > Mis flujos, confirma que el flujo muestra el indicador verde de "Activado". Si está desactivado, haz clic en los tres puntos y selecciona "Activar".
2. **Verifica el mapeo de variables:** En Copilot Studio, abre el tema que llama al workflow y revisa el nodo de "Llamar a una acción". Confirma que cada parámetro del flujo tiene una variable asignada (no vacía).
3. **Espera y recarga:** Espera 3 a 5 minutos y recarga la página de Power Automate. El historial de ejecución tiene un retraso de visualización en entornos con carga alta.
4. **Prueba manual del flujo:** En Power Automate, usa el botón "Probar" del flujo con entrada manual para confirmar que el flujo funciona de forma independiente. Si falla en la prueba manual, el problema está en el flujo mismo, no en Copilot Studio.
5. **Revisa los errores del flujo:** Si hay ejecuciones con estado "Error" en el historial, haz clic en ellas para ver el detalle del error y corregir la acción específica que falló.

---

## Limpieza del Entorno

Al finalizar el laboratorio, realiza las siguientes acciones para dejar el entorno ordenado:

1. **Guardar el documento de matriz:**
   - Guarda el archivo `Matriz_Pruebas_Agente_Auditor_v1.docx` con todos los cambios finales.
   - Sube una copia al canal de Teams del curso o a la ubicación indicada por el instructor.

2. **Limpiar registros de prueba en Dataverse (opcional):**
   - Si el instructor lo indica, elimina los registros de prueba generados durante el laboratorio para no contaminar la base de datos de producción.
   - En Teams > Power Apps > tabla de validaciones, filtra por fecha de hoy y elimina los registros marcados como prueba.
   - **Nota:** No elimines registros si el instructor planea revisarlos como evidencia del laboratorio.

3. **Cerrar sesiones de prueba en Copilot Studio:**
   - En el panel de pruebas, haz clic en el ícono de reinicio para limpiar la sesión activa.
   - No es necesario cerrar el agente ni despublicarlo; el agente debe permanecer activo para la Práctica 7.

4. **Verificar el estado final del workflow:**
   - Confirma en Power Automate que el flujo está en estado "Activado" con los ajustes implementados.
   - Si realizaste modificaciones al flujo, confirma que la versión publicada es la más reciente.

5. **Entregar evidencia al instructor:**
   - Comparte el documento de matriz de pruebas completado.
   - Si tomaste capturas de pantalla de los ajustes, inclúyelas como apéndice del documento.

---

## Resumen

En esta práctica ejecutaste un ciclo completo y documentado de **prueba → ajuste → verificación** sobre el agente de auditoría interna. Los puntos clave del trabajo realizado:

- **Diseñaste una matriz estructurada** de 8 casos de prueba en 4 categorías: respuesta esperada, datos faltantes, alto riesgo y fuera de alcance, con criterios de aceptación verificables para cada uno.
- **Ejecutaste sistemáticamente** todos los casos en el panel de pruebas de Copilot Studio, documentando la respuesta real del agente frente a la esperada.
- **Verificaste la trazabilidad operativa completa:** desde la conversación en el chat hasta las variables capturadas, la ejecución del workflow en Power Automate, el registro en Dataverse y la confirmación de notificaciones.
- **Identificaste causas raíz** de los casos fallidos o mejorables, y planificaste e implementaste mínimo 3 ajustes concretos en instrucciones, temas, conocimiento o workflow.
- **Cerraste el ciclo de calidad** re-ejecutando los casos afectados y documentando la mejora, generando evidencia auditable del proceso de validación del agente.

Este ciclo de prueba-ajuste-verificación no es un evento único: es el modelo operativo que debe aplicarse cada vez que el agente incorpore nuevas funcionalidades, se detecten nuevos escenarios en producción o cambien los requisitos del proceso auditor.

### Recursos de Referencia

| Recurso | URL |
|---|---|
| Documentación de pruebas en Copilot Studio | https://learn.microsoft.com/es-es/microsoft-copilot-studio/authoring-test-bot |
| Historial de ejecución en Power Automate | https://learn.microsoft.com/es-es/power-automate/monitor-manage-processes |
| Consulta de datos en Dataverse for Teams | https://learn.microsoft.com/es-es/power-apps/teams/overview-data-platform |
| Buenas prácticas de IA responsable — Microsoft | https://learn.microsoft.com/es-es/azure/ai-services/responsible-use-of-ai-overview |
| Guía de calidad para agentes conversacionales | https://learn.microsoft.com/es-es/microsoft-copilot-studio/guidance/index |

---
*Laboratorio 06-00-01 — Práctica 6 de 7 | Curso: Agente de Auditoría Interna con Microsoft Copilot Studio | Versión 1.0 — 2025*
