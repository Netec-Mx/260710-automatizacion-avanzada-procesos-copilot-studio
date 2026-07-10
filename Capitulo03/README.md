# Crear un tema de revisión de control con variables, entidades, condiciones y rutas de excepción

## Metadatos

| Campo | Detalle |
|---|---|
| **Duración estimada** | 20 minutos |
| **Complejidad** | Alta |
| **Nivel Bloom** | Crear (*Create*) |
| **Módulo** | Módulo 3 — Temas, entidades, variables y condiciones en Copilot Studio |
| **Práctica** | Práctica 3 de 7 |

---

## Descripción General

En esta práctica construirás el tema central del agente auditor: **"Revisión de Control Interno"**. Aplicarás directamente los conceptos de la Lección 3.1 —estructura de temas orientados a procesos, nodos de conversación, capas de validación y excepción— para modelar el flujo de revisión de un control interno de forma conversacional. Crearás entidades personalizadas para el dominio de auditoría, implementarás variables de tema y globales para conservar el contexto entre turnos, y construirás al menos tres rutas de condición que dirijan la conversación según el estado de cumplimiento detectado, incluyendo el manejo de datos incompletos y excepciones críticas.

---

## Objetivos de Aprendizaje

Al finalizar esta práctica serás capaz de:

- [ ] Diseñar y construir en Copilot Studio un tema de validación de controles internos con flujo de preguntas guiadas, variables y condiciones.
- [ ] Crear entidades personalizadas aplicadas al dominio de auditoría (`Nivel de Riesgo` y `Estado de Cumplimiento`) y aplicarlas en nodos de pregunta.
- [ ] Implementar variables de tema y variables globales para conservar el contexto de la revisión a lo largo de la conversación.
- [ ] Construir tres rutas de condición diferenciadas: cumplimiento normal, no cumplimiento con excepción, y validación incompleta por datos faltantes.
- [ ] Verificar el funcionamiento del tema completo mediante el panel de pruebas de Copilot Studio.

---

## Prerrequisitos

### Conocimiento previo requerido

- Haber completado la **Práctica 2** con el agente base creado, probado y funcionando en Copilot Studio.
- Comprensión básica de lógica condicional y variables en entornos low-code (Power Automate, Power Apps o similar).
- Familiaridad con el concepto de control interno y los estados de cumplimiento usados en auditoría (cumple, no cumple, cumple parcialmente).
- Haber revisado el contenido de la **Lección 3.1**: estructura de temas, tipos de nodos y arquitectura de tres capas para agentes de auditoría.

### Acceso requerido

- Cuenta de Microsoft 365 activa con licencia de **Microsoft Copilot Studio** (standalone o incluida en M365 Copilot).
- Acceso al agente de auditoría creado en la Práctica 2 dentro de Copilot Studio.
- Navegador Microsoft Edge 120+ o Google Chrome 120+ con sesión iniciada en el tenant del curso.
- Conexión a internet estable (mínimo 10 Mbps recomendado).

> **⚠️ Nota importante:** Si no completaste la Práctica 2, solicita al instructor el artefacto de solución antes de continuar. Este laboratorio es acumulativo y requiere el agente base como punto de partida.

---

## Entorno de Laboratorio

### Hardware recomendado

| Componente | Mínimo | Recomendado |
|---|---|---|
| Procesador | Intel Core i5 8ª gen / AMD Ryzen 5 | Intel Core i7 / AMD Ryzen 7 |
| Memoria RAM | 8 GB | 16 GB |
| Resolución de pantalla | 1366 × 768 | 1920 × 1080 |
| Almacenamiento libre | 500 MB | 2 GB |
| Conexión a internet | 10 Mbps | 25 Mbps |

### Software requerido

| Software | Versión | Uso en esta práctica |
|---|---|---|
| Microsoft Copilot Studio | Actual (2024-2025) | Editor de temas, entidades, variables, condiciones |
| Microsoft Edge o Chrome | 120 o superior | Acceso al portal de Copilot Studio |
| Microsoft Teams | Actual desktop o web | Verificación opcional al final |

### Configuración inicial del entorno

Antes de comenzar los pasos del laboratorio, verifica que tu entorno esté listo:

```
1. Abre el navegador (Edge o Chrome).
2. Navega a: https://copilotstudio.microsoft.com
3. Inicia sesión con tu cuenta del curso.
4. Confirma que puedes ver el agente creado en la Práctica 2.
5. Abre el agente y verifica que el panel de temas esté accesible.
```

> **💡 Consejo de productividad:** Para esta práctica se recomienda trabajar con la ventana del navegador a pantalla completa (F11) o con una resolución de al menos 1920×1080. El editor de temas de Copilot Studio muestra mejor el lienzo de nodos con mayor espacio horizontal.

---

## Instrucciones Paso a Paso

---

### Paso 1: Crear la entidad personalizada "Nivel de Riesgo"

**Objetivo:** Definir una entidad de lista cerrada que permita al agente reconocer y validar las respuestas del auditor cuando se le pregunte por el nivel de riesgo de un control, evitando entradas de texto libre no controladas.

#### Instrucciones

1. Desde el portal de Copilot Studio (`https://copilotstudio.microsoft.com`), abre tu agente de auditoría creado en la Práctica 2.

2. En el panel de navegación izquierdo, localiza y selecciona la sección **"Configuración"** o busca directamente la opción **"Entidades"** (*Entities*) en el menú lateral. En la experiencia actual de Copilot Studio (2024-2025), las entidades se encuentran dentro del menú lateral bajo la categoría **"Configuración" → "Entidades"**.

3. Haz clic en el botón **"+ Nueva entidad"** (*+ New entity*) en la parte superior de la página.

4. Selecciona el tipo **"Lista cerrada"** (*Closed list*) cuando se te solicite elegir el tipo de entidad.

5. En el campo **"Nombre de la entidad"**, escribe exactamente:
   ```
   NivelDeRiesgo
   ```

6. En la sección de ítems de la lista, agrega los siguientes valores uno por uno usando el botón **"+ Agregar ítem"**:

   | Ítem | Sinónimos sugeridos |
   |---|---|
   | `Alto` | `alto riesgo`, `riesgo alto`, `crítico`, `crítica` |
   | `Medio` | `riesgo medio`, `moderado`, `moderada` |
   | `Bajo` | `riesgo bajo`, `bajo riesgo`, `mínimo`, `mínima` |

   > **💡 Importante:** Los sinónimos ayudan al motor de lenguaje natural a reconocer variaciones de la misma respuesta. Agrégalos haciendo clic en el ícono de sinónimos junto a cada ítem.

7. Activa la opción **"Coincidencia inteligente"** (*Smart matching*) si está disponible, para mejorar el reconocimiento de variantes ortográficas.

8. Haz clic en **"Guardar"** (*Save*).

#### Resultado esperado

La entidad `NivelDeRiesgo` aparece en la lista de entidades del agente con tres ítems (Alto, Medio, Bajo) y sus sinónimos configurados. El estado debe mostrar **"Guardado"** o un ícono de verificación verde.

#### Verificación

- [ ] La entidad `NivelDeRiesgo` aparece en la lista de entidades personalizadas del agente.
- [ ] Los tres ítems (Alto, Medio, Bajo) están presentes con al menos un sinónimo cada uno.
- [ ] No hay errores de validación en la pantalla de la entidad.

---

### Paso 2: Crear la entidad personalizada "Estado de Cumplimiento"

**Objetivo:** Definir la segunda entidad de dominio auditor que capturará el resultado de la revisión del control, con cuatro estados posibles que cubren todos los escenarios del proceso de auditoría.

#### Instrucciones

1. Desde la sección **"Entidades"**, haz clic nuevamente en **"+ Nueva entidad"**.

2. Selecciona el tipo **"Lista cerrada"** (*Closed list*).

3. En el campo **"Nombre de la entidad"**, escribe exactamente:
   ```
   EstadoDeCumplimiento
   ```

4. Agrega los siguientes cuatro ítems con sus sinónimos:

   | Ítem | Sinónimos sugeridos |
   |---|---|
   | `Cumple` | `cumple totalmente`, `sí cumple`, `conforme`, `aprobado`, `ok` |
   | `Cumple Parcialmente` | `cumple parcial`, `parcialmente`, `cumplimiento parcial`, `en proceso` |
   | `No Cumple` | `no cumple`, `incumple`, `incumplimiento`, `no conforme`, `rechazado` |
   | `No Aplica` | `no aplica`, `n/a`, `no corresponde`, `exento` |

5. Haz clic en **"Guardar"** (*Save*).

#### Resultado esperado

La entidad `EstadoDeCumplimiento` aparece en la lista de entidades con cuatro ítems configurados. Junto con la entidad anterior, ahora tienes dos entidades personalizadas de dominio auditor disponibles para usar en los nodos de pregunta del tema.

#### Verificación

- [ ] La entidad `EstadoDeCumplimiento` aparece en la lista de entidades personalizadas.
- [ ] Los cuatro ítems están presentes: Cumple, Cumple Parcialmente, No Cumple, No Aplica.
- [ ] Ambas entidades (`NivelDeRiesgo` y `EstadoDeCumplimiento`) son visibles en la lista de entidades del agente.

---

### Paso 3: Crear el tema "Revisión de Control Interno"

**Objetivo:** Crear el tema principal del agente auditor con sus frases desencadenantes, estableciendo la estructura base del flujo de conversación que se poblará en los pasos siguientes.

#### Instrucciones

1. En el panel de navegación izquierdo, selecciona **"Temas"** (*Topics*).

2. Haz clic en **"+ Nuevo tema"** → selecciona **"Desde cero"** (*From blank*).

3. En la parte superior del lienzo del tema, haz clic en el campo del nombre y escribe:
   ```
   Revisión de Control Interno
   ```

4. En el nodo **"Desencadenador"** (*Trigger*) que aparece automáticamente al inicio del lienzo, haz clic en **"Editar frases desencadenantes"** y agrega las siguientes frases, una por una (presiona Enter o haz clic en el botón de agregar después de cada una):

   ```
   revisar control interno
   ```
   ```
   validar control
   ```
   ```
   iniciar revisión de control
   ```
   ```
   auditar control
   ```
   ```
   levantamiento de control
   ```
   ```
   quiero revisar un control
   ```

5. Haz clic fuera del editor de frases para confirmar.

6. Guarda el tema haciendo clic en el botón **"Guardar"** (*Save*) en la barra superior.

#### Resultado esperado

El tema `Revisión de Control Interno` aparece en la lista de temas personalizados del agente con estado **"Activado"** (*On*) y las seis frases desencadenantes configuradas. El lienzo muestra únicamente el nodo de desencadenador como punto de partida.

#### Verificación

- [ ] El tema aparece en la lista de temas con el nombre correcto.
- [ ] Al menos 5 frases desencadenantes están configuradas.
- [ ] El tema está en estado "Activado".

---

### Paso 4: Construir el flujo de preguntas guiadas y configurar variables de tema

**Objetivo:** Poblar el tema con los nodos de mensaje y pregunta que capturan los seis datos clave del proceso de revisión de control, configurando variables de tema para cada respuesta capturada.

#### Instrucciones

**4.1 — Mensaje de bienvenida al tema**

1. Dentro del lienzo del tema `Revisión de Control Interno`, haz clic en el botón **"+"** debajo del nodo de desencadenador y selecciona **"Enviar un mensaje"** (*Send a message*).

2. En el nodo de mensaje, escribe el siguiente texto:
   ```
   Iniciaremos el levantamiento de información para la revisión de un control interno. 
   Por favor responde las siguientes preguntas con la mayor precisión posible. 
   Esta información quedará registrada como evidencia de auditoría.
   ```

---

**4.2 — Pregunta 1: Nombre del proceso auditado**

1. Haz clic en **"+"** debajo del nodo de mensaje anterior y selecciona **"Hacer una pregunta"** (*Ask a question*).

2. En el campo de texto de la pregunta, escribe:
   ```
   ¿Cuál es el nombre del proceso que estás auditando? 
   (Ejemplo: Compras y Pagos, Nómina, Cierre Contable)
   ```

3. En la sección **"Identificar"** (*Identify*), selecciona el tipo de respuesta: **"Respuesta completa del usuario"** (*Entire response from user*) — esto captura texto libre.

4. En la sección **"Guardar respuesta como"** (*Save response as*), haz clic en el campo de variable y selecciona **"Crear nueva variable"** (*Create new variable*). Nómbrala:
   ```
   var_ProcesoAuditado
   ```
   Tipo: `String`

---

**4.3 — Pregunta 2: Identificador del control**

1. Agrega un nuevo nodo de pregunta debajo del anterior.

2. Texto de la pregunta:
   ```
   Ingresa el identificador del control que vas a revisar. 
   (Ejemplo: CTR-001, CTR-FIN-023)
   ```

3. Tipo de respuesta: **"Respuesta completa del usuario"**.

4. Variable: Crea una nueva variable llamada:
   ```
   var_IDControl
   ```
   Tipo: `String`

---

**4.4 — Pregunta 3: Descripción del control**

1. Agrega un nuevo nodo de pregunta.

2. Texto de la pregunta:
   ```
   Describe brevemente el objetivo o función del control bajo revisión.
   ```

3. Tipo de respuesta: **"Respuesta completa del usuario"**.

4. Variable:
   ```
   var_DescripcionControl
   ```
   Tipo: `String`

---

**4.5 — Pregunta 4: Período de revisión**

1. Agrega un nuevo nodo de pregunta.

2. Texto de la pregunta:
   ```
   ¿Cuál es el período bajo revisión? 
   (Ejemplo: Enero 2025, Q1 2025, 01/01/2025 - 31/03/2025)
   ```

3. Tipo de respuesta: **"Respuesta completa del usuario"**.

4. Variable:
   ```
   var_PeriodoRevision
   ```
   Tipo: `String`

---

**4.6 — Pregunta 5: Responsable del control**

1. Agrega un nuevo nodo de pregunta.

2. Texto de la pregunta:
   ```
   ¿Quién es el responsable del control? 
   Indica nombre completo y cargo si es posible.
   ```

3. Tipo de respuesta: **"Respuesta completa del usuario"**.

4. Variable:
   ```
   var_ResponsableControl
   ```
   Tipo: `String`

---

**4.7 — Pregunta 6: Nivel de riesgo (usando la entidad personalizada)**

1. Agrega un nuevo nodo de pregunta.

2. Texto de la pregunta:
   ```
   ¿Cuál es el nivel de riesgo asociado a este control?
   ```

3. En la sección **"Identificar"**, selecciona la entidad personalizada que creaste:
   ```
   NivelDeRiesgo (entidad personalizada)
   ```
   > Si no aparece directamente, busca en la lista desplegable de entidades bajo la categoría "Personalizadas".

4. Activa las **opciones de respuesta múltiple** (*Multiple choice options*) para mostrar botones al usuario. Configura las opciones visibles como:
   - `Alto`
   - `Medio`
   - `Bajo`

5. Variable:
   ```
   var_NivelRiesgo
   ```
   Tipo: Entidad `NivelDeRiesgo`

---

**4.8 — Pregunta 7: Evidencia disponible**

1. Agrega un nuevo nodo de pregunta.

2. Texto de la pregunta:
   ```
   ¿Qué evidencia está disponible para soportar esta revisión? 
   (Ejemplo: reportes del sistema, actas de aprobación, registros físicos, capturas de pantalla)
   Escribe "ninguna" si no hay evidencia disponible en este momento.
   ```

3. Tipo de respuesta: **"Respuesta completa del usuario"**.

4. Variable:
   ```
   var_Evidencia
   ```
   Tipo: `String`

---

**4.9 — Pregunta 8: Estado de cumplimiento (usando la entidad personalizada)**

1. Agrega un nuevo nodo de pregunta.

2. Texto de la pregunta:
   ```
   Basándote en la revisión realizada, ¿cuál es el estado de cumplimiento del control?
   ```

3. En la sección **"Identificar"**, selecciona la entidad personalizada:
   ```
   EstadoDeCumplimiento (entidad personalizada)
   ```

4. Activa las opciones de respuesta múltiple con los cuatro valores:
   - `Cumple`
   - `Cumple Parcialmente`
   - `No Cumple`
   - `No Aplica`

5. Variable:
   ```
   var_EstadoCumplimiento
   ```
   Tipo: Entidad `EstadoDeCumplimiento`

6. Haz clic en **"Guardar"** (*Save*) en la barra superior.

#### Resultado esperado

El lienzo del tema muestra una cadena lineal de 9 nodos (1 mensaje + 8 preguntas) con variables correctamente asignadas a cada nodo de pregunta. Las preguntas 7 y 9 muestran las entidades personalizadas como tipo de reconocimiento, y las preguntas con opciones múltiples muestran los botones de selección configurados.

#### Verificación

- [ ] Los 8 nodos de pregunta están presentes en el lienzo.
- [ ] Cada pregunta tiene una variable de tema asignada con el nombre correcto.
- [ ] Las preguntas de `NivelDeRiesgo` y `EstadoDeCumplimiento` usan las entidades personalizadas creadas en los Pasos 1 y 2.
- [ ] Las preguntas con entidades muestran opciones de botones configuradas.

---

### Paso 5: Configurar variables globales para conservar contexto entre temas

**Objetivo:** Elevar dos variables de tema a variables globales, de modo que el proceso auditado y el responsable del control queden disponibles para ser consultados desde cualquier otro tema del agente (por ejemplo, temas de excepción o de resumen).

#### Instrucciones

1. Con el tema `Revisión de Control Interno` abierto en el lienzo, localiza el nodo de la **Pregunta 1** (la que captura `var_ProcesoAuditado`).

2. Haz clic en la variable `var_ProcesoAuditado` en el campo **"Guardar respuesta como"** del nodo.

3. En el panel de propiedades de la variable que se abre a la derecha (o en el cuadro de edición de variable), busca la sección **"Alcance de la variable"** (*Variable scope*) o **"Uso"** y cambia el tipo de `Tema` (*Topic*) a **`Global`**.

   > **Nota técnica:** En Copilot Studio (experiencia 2024-2025), las variables globales se crean directamente desde el panel de edición de variable cambiando su alcance. El nombre de la variable global resultante seguirá el patrón `Global.var_ProcesoAuditado` en el sistema, aunque en el lienzo puede verse simplificado.

4. Confirma el cambio. La variable debe mostrar un ícono diferente (generalmente un globo o símbolo de alcance global) en el nodo.

5. Repite el proceso para la variable `var_ResponsableControl` (Pregunta 5): cámbiala de alcance `Tema` a **`Global`**.

6. Guarda el tema.

#### Resultado esperado

Las variables `var_ProcesoAuditado` y `var_ResponsableControl` muestran el ícono de variable global en sus respectivos nodos de pregunta. Las demás variables (`var_IDControl`, `var_DescripcionControl`, `var_PeriodoRevision`, `var_NivelRiesgo`, `var_Evidencia`, `var_EstadoCumplimiento`) permanecen como variables de tema.

#### Verificación

- [ ] `var_ProcesoAuditado` tiene alcance global.
- [ ] `var_ResponsableControl` tiene alcance global.
- [ ] Las demás 6 variables permanecen como variables de tema (alcance local).
- [ ] El tema se guardó sin errores.

---

### Paso 6: Construir las tres rutas de condición

**Objetivo:** Implementar la lógica de bifurcación del tema basada en el estado de cumplimiento detectado y la presencia de evidencia, creando tres rutas diferenciadas: cumplimiento normal, excepción por no cumplimiento y validación incompleta.

#### Instrucciones

**6.1 — Agregar el nodo de condición principal**

1. Después del último nodo de pregunta (`var_EstadoCumplimiento`, Pregunta 8), haz clic en **"+"** y selecciona **"Agregar una condición"** (*Add a condition*).

2. En el nodo de condición que aparece, configura la primera rama:
   - **Condición 1:** `var_EstadoCumplimiento` **es igual a** (*is equal to*) → `Cumple`

3. Haz clic en **"+ Nueva condición"** o en el botón de agregar rama para añadir una segunda condición:
   - **Condición 2:** `var_EstadoCumplimiento` **es igual a** → `No Cumple`

4. Agrega una tercera condición:
   - **Condición 3:** `var_EstadoCumplimiento` **es igual a** → `Cumple Parcialmente`

5. Verifica que el nodo de condición tenga también la rama **"Todos los demás casos"** (*All other conditions*) — esta es la ruta por defecto que usaremos para el estado `No Aplica`.

---

**6.2 — Ruta 1: Cumplimiento normal ("Cumple")**

1. En la rama de la **Condición 1** (`Cumple`), haz clic en **"+"** y agrega un nodo de **"Condición"** anidado para verificar si hay evidencia:
   - Condición: `var_Evidencia` **no es igual a** (*is not equal to*) → `ninguna`
   - Y: `var_Evidencia` **no está vacío** (*is not blank*)

   > **Alternativa simplificada:** Si el nodo de condición anidado es complejo para el tiempo disponible, usa directamente un nodo de mensaje y continúa.

2. En la sub-rama donde hay evidencia, agrega un nodo de **"Enviar un mensaje"** con el texto:
   ```
   ✅ Registro de cumplimiento confirmado.
   
   El control [var_IDControl] del proceso [var_ProcesoAuditado] 
   presenta estado: CUMPLE para el período [var_PeriodoRevision].
   
   Evidencia documentada: [var_Evidencia]
   Responsable: [var_ResponsableControl]
   
   El registro será enviado al sistema de auditoría.
   ```
   > **Nota:** Para insertar variables en el texto del mensaje, usa el botón **"{x}"** o **"Insertar variable"** que aparece en la barra de herramientas del nodo de mensaje. Selecciona cada variable de la lista.

3. En la sub-rama donde **no** hay evidencia (o en la rama de "Todos los demás casos" del nodo anidado), agrega un nodo de mensaje:
   ```
   ⚠️ El control presenta cumplimiento, pero no se registró evidencia de soporte.
   
   Se recomienda documentar la evidencia antes de cerrar la revisión.
   ¿Deseas agregar evidencia ahora? Escribe la descripción o escribe "continuar" para registrar sin evidencia.
   ```

---

**6.3 — Ruta 2: Excepción por no cumplimiento ("No Cumple")**

1. En la rama de la **Condición 2** (`No Cumple`), agrega un nodo de **"Enviar un mensaje"**:
   ```
   🔴 ALERTA: Control con incumplimiento detectado.
   
   Proceso: [var_ProcesoAuditado]
   Control: [var_IDControl] — [var_DescripcionControl]
   Período: [var_PeriodoRevision]
   Responsable: [var_ResponsableControl]
   Nivel de riesgo: [var_NivelRiesgo]
   
   Este hallazgo requiere documentación de excepción y plan de acción correctiva.
   ```

2. Debajo de ese mensaje, agrega un nodo de **"Enviar un mensaje"** adicional:
   ```
   Se ha marcado este control para seguimiento prioritario. 
   El equipo de auditoría será notificado del hallazgo.
   
   En la siguiente práctica conectaremos este punto con el flujo de registro en Dataverse.
   ```

3. *(Opcional — si el tiempo lo permite)* Agrega un nodo de **"Redirigir a tema"** (*Redirect to topic*) apuntando a un tema llamado `Registrar Hallazgo` (que se creará en prácticas posteriores). Por ahora puedes dejarlo como comentario o configurarlo apuntando al tema de **"Fin de conversación"** del sistema.

---

**6.4 — Ruta 3: Cumplimiento parcial ("Cumple Parcialmente")**

1. En la rama de la **Condición 3** (`Cumple Parcialmente`), agrega un nodo de **"Enviar un mensaje"**:
   ```
   🟡 Control con cumplimiento parcial registrado.
   
   Proceso: [var_ProcesoAuditado]
   Control: [var_IDControl]
   Período: [var_PeriodoRevision]
   
   El cumplimiento parcial indica que el control existe pero presenta brechas de implementación.
   Se requiere documentar las observaciones específicas y establecer un plazo de regularización.
   ```

2. Agrega un segundo nodo de mensaje:
   ```
   Por favor, describe brevemente las brechas identificadas o las acciones correctivas pendientes 
   para este control. Esta información complementará el registro de auditoría.
   ```

---

**6.5 — Ruta de validación incompleta (rama "Todos los demás casos" / "No Aplica")**

1. En la rama **"Todos los demás casos"** (*All other conditions*) del nodo de condición principal, agrega un nodo de **"Condición"** adicional para verificar si el estado es `No Aplica`:
   - Condición: `var_EstadoCumplimiento` **es igual a** → `No Aplica`

2. En la sub-rama `No Aplica`, agrega un mensaje:
   ```
   ℹ️ Control marcado como No Aplica.
   
   El control [var_IDControl] del proceso [var_ProcesoAuditado] 
   ha sido excluido del alcance de la revisión para el período [var_PeriodoRevision].
   
   Responsable confirmado: [var_ResponsableControl]
   
   Se registrará la justificación de exclusión en el archivo de auditoría.
   ```

3. En la rama de "Todos los demás casos" del nodo anidado (cuando `var_EstadoCumplimiento` no tiene valor o está vacío), agrega el mensaje de **validación incompleta**:
   ```
   ⚠️ No se pudo completar el registro de la revisión.
   
   Algunos datos requeridos están incompletos o no fueron reconocidos correctamente.
   
   Por favor verifica:
   • Estado de cumplimiento del control
   • Evidencia disponible
   • Identificador del control
   
   Puedes reiniciar la revisión escribiendo "revisar control" 
   o contactar al administrador del sistema si el problema persiste.
   ```

4. Guarda el tema completo haciendo clic en **"Guardar"** (*Save*).

#### Resultado esperado

El lienzo del tema muestra el nodo de condición principal con cuatro ramas claramente diferenciadas, cada una con su propio mensaje de respuesta. La arquitectura visual del tema refleja la lógica de auditoría: ruta verde para cumplimiento, ruta roja para incumplimiento, ruta amarilla para cumplimiento parcial y ruta gris/informativa para no aplica y datos faltantes.

#### Verificación

- [ ] El nodo de condición principal tiene al menos 3 ramas configuradas con condiciones sobre `var_EstadoCumplimiento`.
- [ ] Cada ruta tiene un mensaje de respuesta diferenciado con variables insertadas.
- [ ] La ruta de "No Cumple" incluye alerta visual (emoji 🔴 o texto equivalente) y mención de seguimiento prioritario.
- [ ] La ruta de validación incompleta incluye instrucciones para reiniciar el proceso.
- [ ] El tema se guardó sin errores de validación.

---

### Paso 7: Agregar el cierre del tema y nodo de fin de conversación

**Objetivo:** Completar el flujo del tema con un nodo de cierre que ofrezca continuidad al auditor y un nodo de fin de conversación correctamente configurado en cada ruta.

#### Instrucciones

1. Al final de la **Ruta 1** (Cumple — con evidencia), después del mensaje de confirmación, agrega un nodo de **"Enviar un mensaje"**:
   ```
   ¿Deseas revisar otro control interno? 
   Escribe "revisar control" para iniciar una nueva revisión 
   o "menú principal" para volver al inicio.
   ```

2. Debajo de ese mensaje, agrega un nodo de **"Fin de conversación"** (*End conversation*) — búscalo en las opciones de nodo como **"Finalizar"** o **"Fin del tema"** (*End topic*).

3. Repite el paso del nodo de fin en las demás rutas (Ruta 2, Ruta 3, y rutas de No Aplica e incompleta). Cada rama debe terminar con un nodo de fin de tema para que el flujo esté completo y no quede abierto.

4. Guarda el tema.

#### Resultado esperado

Todas las ramas del tema terminan con un nodo de fin de conversación o fin de tema. El lienzo no muestra ramas sin terminar (nodos con el botón "+" sin conectar a un nodo de fin).

#### Verificación

- [ ] Todas las ramas del nodo de condición terminan con un nodo de fin.
- [ ] Al menos la Ruta 1 incluye un mensaje de oferta de continuidad antes del fin.
- [ ] El tema no muestra advertencias de flujo incompleto en el lienzo.

---

## Validación y Pruebas

### Prueba 1: Escenario de cumplimiento normal

**Objetivo:** Verificar que el flujo completo funciona correctamente cuando el auditor reporta un control en cumplimiento con evidencia disponible.

#### Instrucciones

1. Abre el panel de pruebas de Copilot Studio haciendo clic en **"Probar agente"** (*Test your agent*) en la esquina inferior izquierda o en la barra superior.

2. En el chat de pruebas, escribe:
   ```
   quiero revisar un control
   ```

3. Responde las preguntas del agente con los siguientes datos de prueba:

   | Pregunta | Respuesta de prueba |
   |---|---|
   | Proceso auditado | `Compras y Pagos a Proveedores` |
   | Identificador del control | `CTR-CP-001` |
   | Descripción del control | `Aprobación de órdenes de compra por nivel de autorización` |
   | Período de revisión | `Q1 2025` |
   | Responsable del control | `María González, Gerente de Compras` |
   | Nivel de riesgo | Selecciona el botón `Alto` |
   | Evidencia disponible | `Reporte de OC aprobadas del sistema ERP, período enero-marzo 2025` |
   | Estado de cumplimiento | Selecciona el botón `Cumple` |

4. Verifica que el agente responde con el mensaje de la **Ruta 1** (confirmación de cumplimiento con evidencia).

**Resultado esperado:** El agente muestra el mensaje de confirmación con el ícono ✅, incluyendo los datos ingresados interpolados en el texto (proceso, control, período, evidencia, responsable).

### Prueba 2: Escenario de no cumplimiento (excepción)

1. Reinicia el chat de pruebas haciendo clic en el ícono de **"Reiniciar conversación"** (generalmente un ícono de recarga circular en el panel de pruebas).

2. Escribe nuevamente:
   ```
   auditar control
   ```

3. Responde con datos de prueba para un control en incumplimiento:

   | Pregunta | Respuesta de prueba |
   |---|---|
   | Proceso auditado | `Nómina y Pagos al Personal` |
   | Identificador del control | `CTR-NOM-005` |
   | Descripción | `Revisión de cálculo de deducciones legales` |
   | Período | `Enero 2025` |
   | Responsable | `Carlos Mendoza, Jefe de Nómina` |
   | Nivel de riesgo | Selecciona `Medio` |
   | Evidencia | `No se encontraron registros de revisión para el período` |
   | Estado de cumplimiento | Selecciona `No Cumple` |

4. Verifica que el agente responde con el mensaje de la **Ruta 2** (alerta 🔴 de incumplimiento).

**Resultado esperado:** El agente muestra el mensaje de alerta con el ícono 🔴, los datos del control y la mención de seguimiento prioritario.

### Prueba 3: Escenario de validación incompleta

1. Reinicia el chat de pruebas.

2. Escribe:
   ```
   iniciar revisión de control
   ```

3. Responde las primeras 5 preguntas normalmente, pero cuando llegues a la pregunta de **Estado de cumplimiento**, escribe texto libre que no coincida con ninguna opción válida:
   ```
   pendiente de evaluación
   ```

4. Verifica que el agente activa la ruta de validación incompleta con el mensaje de advertencia ⚠️ y las instrucciones para reiniciar.

> **Nota:** Dependiendo de la configuración de reconocimiento de entidades, el agente puede pedir al usuario que seleccione una opción válida antes de continuar. Esto es comportamiento correcto. Si el agente no llega a la ruta de validación incompleta porque la entidad fuerza la selección, documenta ese comportamiento como resultado esperado del diseño de la entidad.

**Resultado esperado:** El agente muestra el mensaje de validación incompleta con instrucciones claras, o bien solicita al usuario que elija una opción válida de la lista (comportamiento igualmente correcto).

---

## Solución de Problemas

### Problema 1: Las entidades personalizadas no aparecen en el selector de tipo de respuesta de los nodos de pregunta

**Síntoma:** Al configurar el campo **"Identificar"** en un nodo de pregunta, la entidad `NivelDeRiesgo` o `EstadoDeCumplimiento` no aparece en la lista desplegable de opciones.

**Causa probable:** La entidad fue creada pero no guardada correctamente, o existe un retraso de sincronización entre el módulo de entidades y el editor de temas en el portal de Copilot Studio. También puede ocurrir si la entidad fue creada en un agente diferente al que se está editando.

**Solución:**
1. Navega a **Configuración → Entidades** y verifica que ambas entidades aparecen en la lista con estado guardado.
2. Si las entidades existen, cierra el tema actual sin guardar y vuelve a abrirlo (esto fuerza la recarga del contexto del editor).
3. Si el problema persiste, realiza un **hard refresh** del navegador (`Ctrl + Shift + R` en Edge/Chrome) y vuelve a abrir el tema.
4. Como alternativa temporal, usa el tipo de respuesta **"Opciones múltiples"** (*Multiple choice*) sin entidad personalizada y configura manualmente las opciones (Alto/Medio/Bajo o los cuatro estados). Esto permite continuar el laboratorio aunque no uses la entidad como reconocedor.

---

### Problema 2: Las variables no aparecen disponibles para insertar en los mensajes de las rutas de condición

**Síntoma:** Al intentar insertar una variable (como `var_ProcesoAuditado` o `var_IDControl`) en el texto de un nodo de mensaje dentro de una rama de condición, la variable no aparece en la lista del botón `{x}` o aparece como indefinida/vacía durante las pruebas.

**Causa probable:** Existe una inconsistencia de alcance de variables. Las variables de tema solo están disponibles dentro del mismo tema, pero si el nodo de mensaje está dentro de una rama de condición muy anidada, puede haber un problema de visibilidad en el editor. También puede ocurrir si el nombre de la variable fue escrito con diferencias de mayúsculas/minúsculas en distintos nodos.

**Solución:**
1. Verifica que los nombres de las variables sean exactamente iguales en todos los nodos (respeta mayúsculas y minúsculas: `var_ProcesoAuditado` ≠ `var_procesosauditado`).
2. Para las variables que deben aparecer en mensajes de rutas de condición, confirma que fueron declaradas **antes** del nodo de condición en el flujo del tema (es decir, en las preguntas que preceden al nodo de condición).
3. Si una variable global no aparece en la lista, ve a **Configuración → Variables globales** y confirma que su alcance está establecido como `Global`.
4. Durante las pruebas, si el valor aparece vacío pero la lógica de condición funciona, verifica que el usuario respondió la pregunta correspondiente antes de llegar a la condición. Usa el panel de **"Variables"** en el panel de pruebas (si está disponible) para inspeccionar los valores en tiempo real.

---

## Limpieza del Entorno

> **⚠️ Importante:** Este laboratorio es parte de una secuencia acumulativa. **NO elimines** el tema `Revisión de Control Interno`, las entidades personalizadas ni las variables globales creadas en esta práctica. Todo este trabajo es la base de las Prácticas 4, 5, 6 y 7.

### Acciones de limpieza recomendadas

1. **Cierra el panel de pruebas** haciendo clic en el botón de cierre del chat de pruebas para liberar recursos del navegador.

2. **Guarda el tema** una última vez (`Ctrl + S` o botón Guardar) para asegurarte de que todos los cambios están persistidos.

3. **Documenta el estado actual** del agente: toma una captura de pantalla del lienzo del tema mostrando el flujo completo con las ramas de condición. Guarda esta imagen como evidencia de la práctica con el nombre:
   ```
   Lab03-00-01_[TuNombre]_RevisionsControl_[Fecha].png
   ```

4. **Cierra pestañas innecesarias** del navegador para liberar memoria, manteniendo abierta únicamente la pestaña de Copilot Studio.

5. **No publiques** el agente en este punto. La publicación se realizará en la Práctica 6 después de completar la integración con Dataverse y Power Automate.

---

## Resumen

En esta práctica construiste el componente central del agente auditor: el tema **"Revisión de Control Interno"**. Aplicando directamente los conceptos de la Lección 3.1, trasladaste la lógica de un procedimiento de auditoría a una arquitectura de nodos conversacionales funcional.

### Lo que construiste

| Componente | Descripción |
|---|---|
| **2 entidades personalizadas** | `NivelDeRiesgo` (Alto/Medio/Bajo) y `EstadoDeCumplimiento` (4 estados) con sinónimos |
| **8 nodos de pregunta** | Captura estructurada de: proceso, ID control, descripción, período, responsable, riesgo, evidencia, estado |
| **6 variables de tema** | `var_IDControl`, `var_DescripcionControl`, `var_PeriodoRevision`, `var_NivelRiesgo`, `var_Evidencia`, `var_EstadoCumplimiento` |
| **2 variables globales** | `var_ProcesoAuditado` y `var_ResponsableControl` disponibles para todos los temas del agente |
| **3+ rutas de condición** | Cumplimiento normal, No cumplimiento (excepción), Cumplimiento parcial, No Aplica, Datos incompletos |
| **Mensajes diferenciados** | Cada ruta tiene un mensaje con contexto visual (emojis) y datos interpolados del proceso de revisión |

### Conceptos clave reforzados

- La **equivalencia tema ↔ procedimiento de auditoría** de la Lección 3.1 se materializó: el tema `Revisión de Control Interno` refleja fielmente los pasos de un levantamiento de información auditor.
- Las **entidades personalizadas** garantizan que las respuestas del auditor sean controladas y consistentes, eliminando ambigüedad en datos críticos como el estado de cumplimiento.
- Las **variables globales** implementan la capa de contexto persistente necesaria para que temas de excepción y seguimiento (que se construirán en prácticas posteriores) puedan acceder a los datos del proceso sin volver a preguntar.
- Las **rutas de condición** implementan la capa de **excepción/escalada** de la arquitectura de tres capas descrita en la Lección 3.1, diferenciando automáticamente los hallazgos que requieren atención prioritaria.

### Próximos pasos

En la **Práctica 4** integrarás este tema con **Dataverse for Teams** mediante un flujo de Power Automate, de modo que cada revisión de control completada quede registrada automáticamente en la base de datos de auditoría. El tema construido hoy es el punto de entrada de ese flujo: las variables capturadas serán los parámetros que se enviarán al conector de Dataverse.

### Recursos de referencia

- [Documentación oficial: Creación y edición de temas en Copilot Studio](https://learn.microsoft.com/es-es/microsoft-copilot-studio/authoring-create-edit-topics)
- [Uso de entidades y extracción de información en Copilot Studio](https://learn.microsoft.com/es-es/microsoft-copilot-studio/advanced-entities-slot-filling)
- [Variables en Copilot Studio: tipos, alcance y uso](https://learn.microsoft.com/es-es/microsoft-copilot-studio/authoring-variables)
- [Descripción general de nodos de condición y ramificación de conversaciones](https://learn.microsoft.com/es-es/microsoft-copilot-studio/authoring-topics-overview)
- [Marco COSO: Control Interno — Marco Integrado (referencia metodológica)](https://www.coso.org/guidance-on-ic)

---
