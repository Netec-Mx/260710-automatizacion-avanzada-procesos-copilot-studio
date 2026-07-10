# Práctica 5 — Crear un workflow como herramienta para registrar una revisión y devolver confirmación o alertar excepción

## 1. Metadatos

| Campo | Detalle |
|---|---|
| **Duración estimada** | 20 minutos |
| **Complejidad** | Alta |
| **Nivel de Bloom** | Crear |
| **Práctica número** | 5 de 7 |
| **Prerequisito inmediato** | Lab 04 completado (tablas de Dataverse y conocimiento configurado) |

---

## 2. Descripción General

En esta práctica construirás un **agent flow** directamente desde Copilot Studio que actúa como herramienta de registro para el agente de auditoría interna. El flujo recibirá los siete parámetros capturados en la conversación (proceso, control, periodo, responsable, nivel de riesgo, estado de cumplimiento y evidencia), los registrará en la tabla **Revisiones** de Dataverse for Teams, evaluará si la revisión constituye una excepción y devolverá al agente un mensaje contextualizado de confirmación o alerta. Al finalizar, verificarás el funcionamiento completo mediante el historial de ejecución de Power Automate con al menos dos escenarios de prueba.

---

## 3. Objetivos de Aprendizaje

Al completar esta práctica serás capaz de:

- [ ] Crear un agent flow desde el lienzo de Copilot Studio usando el desencadenador *"Run a flow from Copilot"* y configurar sus parámetros de entrada y salida.
- [ ] Implementar una acción **Agregar fila** sobre la tabla *Revisiones* de Dataverse for Teams, mapeando correctamente los siete parámetros recibidos del agente.
- [ ] Construir una condición de evaluación que detecte excepciones (estado *No Cumple* o riesgo *Alto*) y genere el mensaje de respuesta apropiado para cada rama.
- [ ] Conectar el flujo al tema *Revisión de Control* del agente y mapear las variables de salida para continuar la conversación con contexto actualizado.
- [ ] Validar la trazabilidad del flujo ejecutando dos escenarios de prueba y revisando el historial de ejecución en Power Automate.

---

## 4. Prerrequisitos

### Conocimientos previos

| Área | Nivel requerido |
|---|---|
| Copilot Studio: temas, variables, nodo "Llamar a una acción" | Intermedio (Labs 2 y 3 completados) |
| Power Automate: conectores, acciones, condiciones | Básico |
| Dataverse for Teams: tablas, columnas, tipos de dato | Básico (Lab 4 completado) |
| Estructura de la tabla *Revisiones* (columnas y tipos) | Conocido desde Lab 4 |

### Acceso y configuración

| Recurso | Estado requerido |
|---|---|
| Licencia Microsoft 365 Copilot o Copilot Studio standalone | ✅ Activa |
| Agente de auditoría creado en Copilot Studio (Lab 2) | ✅ Publicado o en borrador |
| Tema *Revisión de Control* con variables definidas (Lab 3) | ✅ Completo |
| Tabla *Revisiones* en Dataverse for Teams (Lab 4) | ✅ Creada y accesible |
| Dataverse for Teams activado en el equipo de Teams del curso | ✅ Activo |
| Conexión de Power Automate a Dataverse for Teams | ✅ Autorizada |

> **⚠️ Nota crítica:** Si la tabla *Revisiones* no existe o no tiene las columnas correctas, detente y solicita al instructor el artefacto de solución del Lab 4 antes de continuar. Este flujo depende directamente de esa estructura.

---

## 5. Entorno de Laboratorio

### Hardware recomendado

| Componente | Mínimo | Recomendado |
|---|---|---|
| Procesador | Intel Core i5 8ª gen / AMD Ryzen 5 | Intel Core i7 / AMD Ryzen 7 |
| Memoria RAM | 8 GB | 16 GB |
| Resolución de pantalla | 1366 × 768 | 1920 × 1080 |
| Ancho de banda | 10 Mbps | 25 Mbps |
| Almacenamiento libre | 2 GB | 5 GB |

### Software requerido

| Herramienta | Versión | URL de acceso |
|---|---|---|
| Microsoft Copilot Studio | Experiencia actual 2024-2025 | https://copilotstudio.microsoft.com |
| Microsoft Power Automate | Cloud 2024-2025 | https://make.powerautomate.com |
| Microsoft Teams | Desktop o Web actual | https://teams.microsoft.com |
| Microsoft Edge o Chrome | Edge 120+ / Chrome 120+ | — |

### Verificación del entorno antes de comenzar

Abre una terminal o el navegador y confirma acceso a los siguientes servicios. No es necesario ejecutar comandos; basta con verificar que las URL cargan correctamente con tu cuenta del curso:

```
1. https://copilotstudio.microsoft.com       → Agente de auditoría visible
2. https://make.powerautomate.com            → Entorno del equipo de Teams seleccionado
3. https://teams.microsoft.com               → Equipo del curso visible con Dataverse activo
```

> **💡 Consejo:** Trabaja con Copilot Studio y Power Automate en pestañas separadas del mismo navegador. Esto agiliza el proceso de creación del flujo desde Copilot Studio y su edición en Power Automate.

---

## 6. Instrucciones Paso a Paso

---

### Paso 1 — Verificar la estructura de la tabla *Revisiones* en Dataverse for Teams

**Objetivo:** Confirmar que la tabla *Revisiones* tiene las columnas necesarias antes de crear el flujo, evitando errores de mapeo.

#### Instrucciones

1. Abre **Microsoft Teams** en el navegador o aplicación de escritorio.
2. Navega al equipo del curso y haz clic en la pestaña **Power Apps** (o busca la aplicación *Power Apps* dentro del equipo).
3. En el panel izquierdo de Power Apps for Teams, selecciona **Compilar** → busca la tabla **Revisiones**.
4. Confirma que la tabla contiene las siguientes columnas con los tipos indicados:

| Nombre de columna | Tipo de dato | Obligatorio |
|---|---|---|
| `Proceso` | Texto (línea única) | Sí |
| `Control` | Texto (línea única) | Sí |
| `Periodo` | Texto (línea única) | Sí |
| `Responsable` | Texto (línea única) | Sí |
| `NivelRiesgo` | Texto (línea única) | Sí |
| `EstadoCumplimiento` | Texto (línea única) | Sí |
| `Evidencia` | Texto (área de texto) | No |
| `FechaRegistro` | Fecha y hora | No |

5. Si alguna columna falta, agrégala ahora haciendo clic en **+ Agregar columna** y configurando el tipo correspondiente.
6. Guarda los cambios si realizaste modificaciones.

#### Resultado esperado

La tabla *Revisiones* muestra las ocho columnas listadas en la vista de diseño de Power Apps for Teams.

#### Verificación

Haz clic en **Ver datos** sobre la tabla *Revisiones*. Debe aparecer la cuadrícula vacía (o con datos de pruebas anteriores) mostrando todas las columnas configuradas.

---

### Paso 2 — Abrir el tema *Revisión de Control* y agregar el nodo de acción

**Objetivo:** Localizar el punto correcto dentro del tema donde se invocará el agent flow, inmediatamente después de capturar todos los datos de la revisión.

#### Instrucciones

1. Abre **Microsoft Copilot Studio** en `https://copilotstudio.microsoft.com`.
2. Selecciona tu agente de auditoría interna.
3. En el panel izquierdo, haz clic en **Temas** y abre el tema **Revisión de Control** (creado en el Lab 3).
4. Desplázate hasta el final del flujo conversacional del tema, después del último nodo de captura de datos (donde se registra la variable de evidencia o confirmación final del auditor).
5. Haz clic en el botón **+** para agregar un nodo nuevo.
6. Selecciona **Llamar a una acción** → **Crear un flujo de Power Automate**.

> **💡 Nota:** La opción *"Crear un flujo de Power Automate"* abrirá automáticamente Power Automate en una nueva pestaña con el desencadenador *"Run a flow from Copilot"* ya configurado. Mantén ambas pestañas abiertas durante todo el paso siguiente.

#### Resultado esperado

Power Automate se abre en una nueva pestaña mostrando un flujo nuevo con dos bloques predeterminados:
- **Run a flow from Copilot** (desencadenador)
- **Respond to Copilot** (respuesta)

#### Verificación

Confirma que la URL de Power Automate contiene el parámetro del entorno de Teams (no el entorno predeterminado). El entorno correcto aparece en el selector de entorno en la esquina superior derecha de Power Automate.

---

### Paso 3 — Configurar los parámetros de entrada en el desencadenador

**Objetivo:** Definir los siete parámetros que el agente enviará al flujo, correspondientes a las variables capturadas en la conversación.

#### Instrucciones

1. En Power Automate, haz clic sobre el bloque **Run a flow from Copilot** para expandirlo.
2. Haz clic en **+ Agregar una entrada** y crea cada uno de los siguientes parámetros. Para cada uno, selecciona el tipo **Texto** (*Text*) salvo indicación contraria:

| N° | Nombre del parámetro | Tipo | Descripción |
|---|---|---|---|
| 1 | `Proceso` | Text | Nombre del proceso auditado |
| 2 | `Control` | Text | Código o nombre del control |
| 3 | `Periodo` | Text | Período de la revisión (ej. Q2-2025) |
| 4 | `Responsable` | Text | Nombre del responsable del control |
| 5 | `NivelRiesgo` | Text | Alto / Medio / Bajo |
| 6 | `EstadoCumplimiento` | Text | Cumple / No Cumple / Parcial |
| 7 | `Evidencia` | Text | Descripción o referencia de la evidencia |

3. Para agregar cada parámetro:
   - Haz clic en **+ Agregar una entrada**.
   - Selecciona **Texto**.
   - Escribe el nombre exacto del parámetro (respeta mayúsculas y sin espacios).
   - El campo de descripción es opcional pero recomendado.

4. Repite hasta tener los siete parámetros configurados.

```
// Esquema de parámetros de entrada esperado en el desencadenador
{
  "Proceso":             "<texto>",
  "Control":             "<texto>",
  "Periodo":             "<texto>",
  "Responsable":         "<texto>",
  "NivelRiesgo":         "<texto>",
  "EstadoCumplimiento":  "<texto>",
  "Evidencia":           "<texto>"
}
```

#### Resultado esperado

El bloque *Run a flow from Copilot* muestra los siete parámetros de entrada listados, cada uno de tipo *Text*.

#### Verificación

Pasa el cursor sobre cada parámetro para confirmar que el tipo de dato aparece como **String** en el tooltip de Power Automate.

---

### Paso 4 — Agregar la acción para crear un registro en Dataverse

**Objetivo:** Insertar la acción que escribirá los datos de la revisión en la tabla *Revisiones* de Dataverse for Teams.

#### Instrucciones

1. Haz clic en el botón **+** entre el desencadenador y el bloque *Respond to Copilot*.
2. Selecciona **Agregar una acción**.
3. En el buscador, escribe `Dataverse` y selecciona el conector **Microsoft Dataverse**.
4. Elige la acción **Agregar una nueva fila** (*Add a new row*).
5. En el campo **Nombre de tabla**, selecciona **Revisiones** (la tabla de tu entorno de Teams).

> **⚠️ Importante:** Asegúrate de que el entorno seleccionado en la conexión de Dataverse corresponde al entorno de Teams donde se creó la tabla, no al entorno predeterminado de Power Platform.

6. Mapea cada campo de la tabla con el parámetro de entrada correspondiente. Haz clic en el campo de cada columna y selecciona el token dinámico del desencadenador:

| Campo en Dataverse | Valor / Token dinámico |
|---|---|
| `Proceso` | `Proceso` (token del desencadenador) |
| `Control` | `Control` (token del desencadenador) |
| `Periodo` | `Periodo` (token del desencadenador) |
| `Responsable` | `Responsable` (token del desencadenador) |
| `NivelRiesgo` | `NivelRiesgo` (token del desencadenador) |
| `EstadoCumplimiento` | `EstadoCumplimiento` (token del desencadenador) |
| `Evidencia` | `Evidencia` (token del desencadenador) |
| `FechaRegistro` | Expresión: `utcNow()` |

7. Para el campo `FechaRegistro`, haz clic en el campo y luego en la pestaña **Expresión** del panel de contenido dinámico. Escribe:
   ```
   utcNow()
   ```
   y haz clic en **Aceptar**.

#### Resultado esperado

El bloque *Agregar una nueva fila* muestra todos los campos mapeados con sus tokens dinámicos correspondientes y la expresión `utcNow()` en el campo de fecha.

#### Verificación

Verifica que ningún campo obligatorio muestre el indicador de error (borde rojo). Si aparece alguno, revisa que el nombre de la columna en Dataverse coincida exactamente con el que configuraste en el Paso 1.

---

### Paso 5 — Implementar la condición de detección de excepciones

**Objetivo:** Agregar la lógica condicional que evalúa si la revisión constituye una excepción (estado *No Cumple* o nivel de riesgo *Alto*) y prepara el mensaje de respuesta apropiado.

#### Instrucciones

1. Haz clic en el botón **+** después del bloque *Agregar una nueva fila*.
2. Selecciona **Agregar una acción** → busca y selecciona **Control** → **Condición**.
3. En la condición, configura la evaluación combinada. La lógica debe ser: *"Si el estado es No Cumple **O** el nivel de riesgo es Alto, entonces es una excepción"*.

**Rama izquierda de la condición (primer criterio):**
- Haz clic en el campo de valor izquierdo → selecciona el token dinámico **EstadoCumplimiento**.
- Operador: **es igual a** (*is equal to*).
- Valor derecho: escribe `No Cumple` (texto exacto, respeta mayúsculas).

4. Haz clic en **+ Agregar** → **Agregar fila** para agregar el segundo criterio con operador **O** (*Or*):
- Valor izquierdo: token dinámico **NivelRiesgo**.
- Operador: **es igual a**.
- Valor derecho: `Alto`.

```
// Lógica de la condición
IF (EstadoCumplimiento == "No Cumple") OR (NivelRiesgo == "Alto")
  THEN → Rama "Sí" (excepción detectada)
  ELSE → Rama "No" (cumplimiento normal)
```

5. En la **rama "Sí"** (excepción):
   - Haz clic en **Agregar una acción** dentro de la rama *Sí*.
   - Selecciona **Variables** → **Inicializar variable** (o usa **Establecer variable** si ya fue inicializada).
   - Nombre de variable: `MensajeRespuesta`
   - Tipo: **Cadena** (*String*)
   - Valor:
     ```
     ⚠️ EXCEPCIÓN DETECTADA: La revisión del control @{triggerBody()?['Control']} en el proceso @{triggerBody()?['Proceso']} ha sido registrada como excepción. Estado: @{triggerBody()?['EstadoCumplimiento']} | Riesgo: @{triggerBody()?['NivelRiesgo']}. Se requiere atención inmediata del responsable @{triggerBody()?['Responsable']}.
     ```

6. En la **rama "No"** (cumplimiento normal):
   - Haz clic en **Agregar una acción** dentro de la rama *No*.
   - Selecciona **Variables** → **Inicializar variable**.
   - Nombre de variable: `MensajeRespuesta`
   - Tipo: **Cadena** (*String*)
   - Valor:
     ```
     ✅ REGISTRO EXITOSO: La revisión del control @{triggerBody()?['Control']} en el proceso @{triggerBody()?['Proceso']} ha sido registrada correctamente para el período @{triggerBody()?['Periodo']}. Responsable: @{triggerBody()?['Responsable']}.
     ```

> **💡 Nota técnica:** En Power Automate, los tokens dinámicos dentro de valores de texto se insertan con el selector de contenido dinámico. La notación `@{triggerBody()?['NombreParametro']}` es la expresión equivalente que puedes usar directamente en el modo de expresión si el selector no muestra los tokens.

#### Resultado esperado

La condición muestra dos ramas correctamente configuradas:
- **Rama Sí**: variable `MensajeRespuesta` con el texto de alerta de excepción.
- **Rama No**: variable `MensajeRespuesta` con el texto de confirmación exitosa.

#### Verificación

Revisa que ambas ramas de la condición tengan exactamente una acción cada una (la inicialización de la variable `MensajeRespuesta`) y que los tokens dinámicos estén correctamente insertados (aparecen como píldoras de color, no como texto plano).

---

### Paso 6 — Configurar la respuesta de retorno al agente

**Objetivo:** Definir los parámetros de salida que el flujo devolverá al agente para que la conversación continúe con el mensaje contextualizado.

#### Instrucciones

1. Haz clic en el bloque **Respond to Copilot** (que ya existe al final del flujo).
2. Haz clic en **+ Agregar una salida** y configura los siguientes parámetros de salida:

| N° | Nombre del parámetro de salida | Tipo | Valor |
|---|---|---|---|
| 1 | `MensajeRespuesta` | Text | Variable `MensajeRespuesta` (token dinámico) |
| 2 | `EsExcepcion` | Text | Expresión condicional (ver instrucción 3) |

3. Para el parámetro `EsExcepcion`, haz clic en el campo de valor → pestaña **Expresión** y escribe:
   ```
   if(or(equals(triggerBody()?['EstadoCumplimiento'], 'No Cumple'), equals(triggerBody()?['NivelRiesgo'], 'Alto')), 'true', 'false')
   ```
   Haz clic en **Aceptar**.

4. Para el parámetro `MensajeRespuesta`, selecciona el token dinámico de la variable `MensajeRespuesta` creada en el Paso 5.

```
// Esquema de parámetros de salida hacia Copilot Studio
{
  "MensajeRespuesta": "<texto dinámico según la rama ejecutada>",
  "EsExcepcion":      "true" | "false"
}
```

5. Asigna un nombre descriptivo al flujo. En la barra superior de Power Automate, reemplaza el nombre predeterminado por:
   ```
   RegistrarRevisionAuditoria
   ```

6. Haz clic en **Guardar** en la esquina superior derecha.

7. Espera a que el flujo se guarde correctamente. Deberías ver el mensaje *"El flujo se guardó correctamente"*.

#### Resultado esperado

El flujo **RegistrarRevisionAuditoria** está guardado y muestra la estructura completa:
1. Run a flow from Copilot (7 parámetros de entrada)
2. Agregar una nueva fila → Dataverse → Revisiones
3. Condición (EstadoCumplimiento == "No Cumple" OR NivelRiesgo == "Alto")
   - Rama Sí: Inicializar variable MensajeRespuesta (alerta)
   - Rama No: Inicializar variable MensajeRespuesta (confirmación)
4. Respond to Copilot (2 parámetros de salida)

#### Verificación

En Power Automate, ve a **Mis flujos** y confirma que **RegistrarRevisionAuditoria** aparece en la lista con estado **Activo** (no en borrador ni desactivado).

---

### Paso 7 — Conectar el flujo al tema en Copilot Studio y mapear variables

**Objetivo:** Regresar a Copilot Studio para seleccionar el flujo recién creado en el nodo de acción y mapear correctamente las variables del tema con los parámetros del flujo.

#### Instrucciones

1. Regresa a la pestaña de **Copilot Studio** donde tienes abierto el tema *Revisión de Control*.
2. Localiza el nodo **Llamar a una acción** que agregaste en el Paso 2. Si Power Automate se abrió en una nueva pestaña y el nodo quedó pendiente de selección, haz clic en el nodo y selecciona **Actualizar** para que aparezca el flujo recién guardado.
3. En el selector de flujos, busca y selecciona **RegistrarRevisionAuditoria**.
4. El nodo mostrará los siete campos de entrada del flujo. Mapea cada uno con la variable de tema correspondiente:

| Parámetro del flujo | Variable del tema (Lab 3) |
|---|---|
| `Proceso` | `Topic.Proceso` |
| `Control` | `Topic.Control` |
| `Periodo` | `Topic.Periodo` |
| `Responsable` | `Topic.Responsable` |
| `NivelRiesgo` | `Topic.NivelRiesgo` |
| `EstadoCumplimiento` | `Topic.EstadoCumplimiento` |
| `Evidencia` | `Topic.Evidencia` |

> **⚠️ Atención:** Los nombres de las variables del tema pueden variar según cómo las definiste en el Lab 3. Usa los nombres exactos de tus variables. Si usaste nombres diferentes (por ejemplo `Topic.ProcesoAuditado`), mapéalos con el parámetro correspondiente del flujo.

5. Después del nodo de acción, verifica que Copilot Studio haya creado automáticamente las variables de salida. Deberían aparecer disponibles como:
   - `RegistrarRevisionAuditoria.MensajeRespuesta`
   - `RegistrarRevisionAuditoria.EsExcepcion`

6. Agrega un nodo de **Mensaje** después del nodo de acción con el siguiente contenido:
   ```
   {RegistrarRevisionAuditoria.MensajeRespuesta}
   ```

7. Opcionalmente, agrega una condición después del mensaje para bifurcar la conversación según `EsExcepcion`:
   - **Si** `RegistrarRevisionAuditoria.EsExcepcion` **es igual a** `true` → mensaje adicional: *"Se ha generado una alerta para el equipo de supervisión. Un responsable se pondrá en contacto contigo."*
   - **Si no** → mensaje: *"¿Deseas registrar otra revisión o tienes alguna otra consulta?"*

8. Haz clic en **Guardar** en Copilot Studio.

#### Resultado esperado

El tema *Revisión de Control* muestra el nodo de acción conectado a **RegistrarRevisionAuditoria** con los siete parámetros mapeados y un nodo de mensaje que usa la variable de salida `MensajeRespuesta`.

#### Verificación

Pasa el cursor sobre el nodo de acción en Copilot Studio. Debe mostrar el nombre del flujo **RegistrarRevisionAuditoria** y la cantidad de parámetros configurados (7 entradas, 2 salidas).

---

### Paso 8 — Prueba de escenario 1: Cumplimiento normal

**Objetivo:** Verificar que el flujo registra correctamente una revisión sin excepción y devuelve el mensaje de confirmación al agente.

#### Instrucciones

1. En Copilot Studio, haz clic en **Probar** (panel de prueba en la esquina derecha).
2. Si el panel de prueba no está visible, haz clic en el ícono de chat en la barra superior.
3. Escribe una frase de activación del tema, por ejemplo:
   ```
   Quiero registrar una revisión de control
   ```
4. Responde a cada pregunta del agente con los siguientes valores de prueba (escenario de cumplimiento normal):

| Pregunta del agente | Respuesta de prueba |
|---|---|
| ¿Cuál es el proceso? | `Cuentas por Pagar` |
| ¿Cuál es el control? | `CTR-AP-001` |
| ¿Cuál es el período? | `Q2-2025` |
| ¿Quién es el responsable? | `Ana García` |
| ¿Cuál es el nivel de riesgo? | `Medio` |
| ¿Cuál es el estado de cumplimiento? | `Cumple` |
| ¿Cuál es la evidencia? | `Facturas aprobadas con doble firma` |

5. Observa el mensaje final del agente. Debe contener el texto de confirmación exitosa con los datos del control.

#### Resultado esperado

```
✅ REGISTRO EXITOSO: La revisión del control CTR-AP-001 en el proceso 
Cuentas por Pagar ha sido registrada correctamente para el período 
Q2-2025. Responsable: Ana García.
```

#### Verificación

1. Ve a **Microsoft Teams** → equipo del curso → pestaña **Power Apps**.
2. Abre la tabla **Revisiones** y confirma que existe una nueva fila con los datos de la prueba.
3. Verifica que el campo `FechaRegistro` contiene la fecha y hora del momento de la prueba.

---

### Paso 9 — Prueba de escenario 2: Excepción detectada

**Objetivo:** Verificar que el flujo identifica correctamente una excepción y devuelve el mensaje de alerta apropiado.

#### Instrucciones

1. En el panel de prueba de Copilot Studio, haz clic en **Reiniciar conversación** (ícono de actualización en el panel de prueba).
2. Escribe nuevamente la frase de activación:
   ```
   Registrar revisión de control
   ```
3. Responde con los siguientes valores de prueba (escenario de excepción):

| Pregunta del agente | Respuesta de prueba |
|---|---|
| ¿Cuál es el proceso? | `Tesorería` |
| ¿Cuál es el control? | `CTR-TES-003` |
| ¿Cuál es el período? | `Q2-2025` |
| ¿Quién es el responsable? | `Carlos Mendoza` |
| ¿Cuál es el nivel de riesgo? | `Alto` |
| ¿Cuál es el estado de cumplimiento? | `No Cumple` |
| ¿Cuál es la evidencia? | `Transferencias sin autorización del nivel 2` |

4. Observa el mensaje final del agente. Debe contener el texto de alerta de excepción.

#### Resultado esperado

```
⚠️ EXCEPCIÓN DETECTADA: La revisión del control CTR-TES-003 en el 
proceso Tesorería ha sido registrada como excepción. Estado: No Cumple 
| Riesgo: Alto. Se requiere atención inmediata del responsable 
Carlos Mendoza.
```

#### Verificación

1. Ve a la tabla **Revisiones** en Dataverse for Teams y confirma que existe una segunda fila con los datos de la prueba de excepción.
2. Ambas filas deben ser visibles: la del Escenario 1 y la del Escenario 2.

---

## 7. Validación y Pruebas de Trazabilidad

### Revisión del historial de ejecución en Power Automate

Una vez completadas las dos pruebas, valida la trazabilidad completa del flujo:

#### Instrucciones

1. Ve a **Power Automate** → **Mis flujos** → selecciona **RegistrarRevisionAuditoria**.
2. En la sección **Historial de ejecución de 28 días**, deberías ver dos ejecuciones recientes.
3. Haz clic en la **primera ejecución** (Escenario 1 - Cumplimiento normal):
   - Verifica que el estado sea ✅ **Correcto** (succeeded).
   - Expande el bloque **Run a flow from Copilot** → confirma que los 7 parámetros de entrada muestran los valores correctos.
   - Expande el bloque **Agregar una nueva fila** → confirma que el registro se creó en Dataverse.
   - Expande el bloque **Condición** → confirma que se ejecutó la **rama No** (cumplimiento normal).
   - Expande el bloque **Respond to Copilot** → confirma el valor de `MensajeRespuesta`.

4. Haz clic en la **segunda ejecución** (Escenario 2 - Excepción):
   - Verifica que el estado sea ✅ **Correcto**.
   - Expande el bloque **Condición** → confirma que se ejecutó la **rama Sí** (excepción detectada).
   - Verifica que `EsExcepcion` tiene el valor `true`.

#### Lista de verificación de trazabilidad

| Elemento | Escenario 1 | Escenario 2 |
|---|---|---|
| Ejecución exitosa en historial | ☐ | ☐ |
| 7 parámetros de entrada visibles | ☐ | ☐ |
| Registro creado en tabla Revisiones | ☐ | ☐ |
| Rama correcta de condición ejecutada | ☐ (Rama No) | ☐ (Rama Sí) |
| MensajeRespuesta correcto devuelto | ☐ (Confirmación) | ☐ (Alerta) |
| EsExcepcion con valor correcto | ☐ (false) | ☐ (true) |

---

## 8. Solución de Problemas

---

### Problema 1: El flujo no aparece en el selector de Copilot Studio tras guardarlo

**Síntoma:** Al regresar a Copilot Studio y hacer clic en el nodo *Llamar a una acción*, el flujo **RegistrarRevisionAuditoria** no aparece en la lista de flujos disponibles, o aparece en estado *No disponible*.

**Causa:** El flujo fue guardado en un entorno de Power Automate diferente al entorno de Teams asociado al agente. Copilot Studio solo muestra flujos del mismo entorno donde está publicado el agente. También puede ocurrir si el flujo fue guardado pero no está en estado *Activo*.

**Solución:**
1. En Power Automate, ve a **Mis flujos** y confirma el entorno activo en el selector de entorno (esquina superior derecha). Debe ser el entorno de Teams del curso, no el entorno *Default*.
2. Si el flujo está en el entorno incorrecto, deberás recrearlo: ve a Power Automate → cambia al entorno de Teams → crea un nuevo flujo con el mismo diseño.
3. Si el flujo existe pero no aparece en Copilot Studio, haz clic en **Actualizar** en el selector de flujos del nodo de acción. Espera 30 segundos y vuelve a intentarlo.
4. Como verificación adicional, confirma que el flujo usa el desencadenador **Run a flow from Copilot** (no otro tipo de desencadenador); de lo contrario, no será visible en Copilot Studio.

---

### Problema 2: El flujo se ejecuta pero no crea el registro en Dataverse (error en la acción *Agregar una nueva fila*)

**Síntoma:** En el historial de ejecución de Power Automate, la ejecución aparece como **Fallida** (failed) y el error se origina en el bloque *Agregar una nueva fila*. El mensaje de error indica algo similar a: *"The entity 'cr123_revisiones' does not exist"* o *"Connection not authorized"*.

**Causa 1 — Entorno incorrecto:** La acción de Dataverse está apuntando al entorno equivocado (Default en lugar del entorno de Teams). La tabla *Revisiones* solo existe en el entorno de Teams.

**Causa 2 — Conexión no autorizada:** La conexión al conector de Dataverse no está autenticada con la cuenta correcta o la cuenta no tiene permisos sobre la tabla.

**Solución:**
1. Abre el flujo en Power Automate en modo edición.
2. Haz clic en el bloque **Agregar una nueva fila** → verifica el campo *Entorno* (Environment). Debe mostrar el nombre del equipo de Teams, no *Default*.
3. Si el entorno es incorrecto, haz clic en el campo de entorno y selecciona el entorno de Teams correcto. La tabla *Revisiones* debería aparecer en el selector de tablas.
4. Si el problema es de conexión, haz clic en los tres puntos del bloque → **Agregar nueva conexión** → autentica con tu cuenta del curso (la misma que usas en Teams).
5. Guarda el flujo y ejecuta una prueba nuevamente desde Copilot Studio.

---

## 9. Limpieza del Entorno

> **⚠️ Importante:** Este laboratorio es parte de una secuencia acumulativa. **No elimines** el flujo *RegistrarRevisionAuditoria* ni los registros creados en la tabla *Revisiones*, ya que serán necesarios para las Prácticas 6 y 7.

### Acciones de limpieza opcionales

Si necesitas limpiar datos de prueba sin afectar la estructura:

1. **Eliminar filas de prueba en Dataverse** (opcional, solo si el instructor lo indica):
   - Ve a Teams → Power Apps → tabla *Revisiones*.
   - Selecciona las filas de prueba creadas durante este lab.
   - Haz clic en **Eliminar registros**.
   - Confirma que la tabla queda vacía o con solo los registros que el instructor indique mantener.

2. **Cerrar pestañas adicionales del navegador:**
   - Cierra la pestaña de Power Automate si ya no la necesitas.
   - Mantén abierta la pestaña de Copilot Studio para la siguiente práctica.

3. **Guardar capturas de evidencia:**
   - Toma una captura de pantalla del historial de ejecución de Power Automate mostrando las dos ejecuciones exitosas.
   - Toma una captura de la tabla *Revisiones* con los dos registros creados.
   - Guarda estas capturas en tu carpeta de evidencias del curso (mínimo 2 GB disponibles en disco).

---

## 10. Resumen

### Lo que construiste en esta práctica

En esta práctica de nivel **Crear**, diseñaste e implementaste un **agent flow** completo que extiende las capacidades del agente de auditoría interna más allá de la conversación. El flujo **RegistrarRevisionAuditoria** actúa como herramienta de integración entre la conversación en Copilot Studio y el sistema de registro en Dataverse for Teams.

### Conceptos clave aplicados

| Concepto | Aplicación en esta práctica |
|---|---|
| **Agent flow con desencadenador Copilot** | Flujo invocado directamente desde el tema *Revisión de Control* |
| **Parámetros de entrada** | 7 variables del tema mapeadas al flujo |
| **Acción Dataverse: Agregar fila** | Registro persistente de cada revisión auditada |
| **Condición de excepción** | Lógica OR: *No Cumple* o *Alto* → alerta |
| **Parámetros de salida** | `MensajeRespuesta` y `EsExcepcion` devueltos al agente |
| **Trazabilidad** | Verificación en historial de ejecución de Power Automate |

### Arquitectura del flujo construido

```
[Copilot Studio: Tema Revisión de Control]
        │
        │ 7 parámetros de entrada
        ▼
[Power Automate: RegistrarRevisionAuditoria]
        │
        ├─► Agregar fila → Dataverse: tabla Revisiones
        │
        ├─► Condición: EstadoCumplimiento == "No Cumple" OR NivelRiesgo == "Alto"
        │       ├─ Sí → MensajeRespuesta = "⚠️ EXCEPCIÓN DETECTADA..."
        │       └─ No → MensajeRespuesta = "✅ REGISTRO EXITOSO..."
        │
        └─► Respond to Copilot: MensajeRespuesta + EsExcepcion
                │
                │ 2 parámetros de salida
                ▼
[Copilot Studio: Mensaje dinámico al auditor]
```

### Conexión con la siguiente práctica

En la **Práctica 6**, utilizarás el parámetro `EsExcepcion` devuelto por este flujo para implementar una ruta de escalamiento dentro del agente: cuando se detecte una excepción, el agente iniciará un flujo de notificación adicional hacia el equipo supervisor. El flujo que construiste hoy es la base de ese mecanismo de escalamiento.

---

### Recursos de referencia

| Recurso | URL |
|---|---|
| Documentación oficial: Uso de flujos en Copilot Studio | https://learn.microsoft.com/es-es/microsoft-copilot-studio/advanced-flow |
| Desencadenador "Run a flow from Copilot" | https://learn.microsoft.com/es-es/power-automate/run-flow-from-copilot |
| Conector Dataverse en Power Automate | https://learn.microsoft.com/es-es/connectors/commondataserviceforapps/ |
| Variables y parámetros en temas de Copilot Studio | https://learn.microsoft.com/es-es/microsoft-copilot-studio/authoring-variables |
| Creación de agent flows: guía paso a paso | https://learn.microsoft.com/es-es/microsoft-copilot-studio/advanced-flow-create |

---
