# Ejecutar una revisión completa desde Teams con consulta de conocimiento, registro automatizado y salida final

## Metadatos del Laboratorio

| Atributo | Detalle |
|---|---|
| **Duración estimada** | 20 minutos |
| **Complejidad** | Media |
| **Nivel Bloom** | Aplicar (*Apply*) |
| **Práctica número** | 7 de 7 |
| **Prerequisito inmediato** | Lab 06 completado con agente validado mediante matriz de pruebas |

---

## Descripción General

En esta práctica final pondrás en operación real el agente de auditoría interna construido a lo largo del curso. Publicarás el agente en el canal de Microsoft Teams configurado para el curso, ejecutarás un flujo de trabajo de auditoría de extremo a extremo directamente desde la interfaz de Teams —incluyendo captura conversacional de datos, consulta a fuentes de conocimiento, respuesta generativa fundamentada, registro automático en Dataverse y confirmación en la conversación— y validarás los resultados verificando los registros creados. Finalmente, documentarás un plan de mantenimiento del agente con las consideraciones operativas necesarias para su uso sostenido en el equipo auditor.

---

## Objetivos de Aprendizaje

Al finalizar esta práctica serás capaz de:

- [ ] Publicar el agente auditor en Microsoft Teams y configurar los parámetros de canal, usuarios autorizados y permisos de acceso desde Copilot Studio y el Centro de Administración de Teams.
- [ ] Ejecutar un flujo de trabajo de auditoría completo de extremo a extremo desde Teams: captura conversacional, consulta de conocimiento, respuesta generativa, ejecución del workflow y registro en Dataverse.
- [ ] Validar la experiencia del equipo auditor en Teams verificando usabilidad, precisión de respuestas, generación de evidencia y correcta escritura de registros en Dataverse.
- [ ] Documentar un plan de mantenimiento del agente con al menos cinco consideraciones operativas para garantizar su operación sostenida y segura.

---

## Prerrequisitos

### Conocimiento previo requerido

| Área | Nivel requerido |
|---|---|
| Copilot Studio: publicación y configuración de canales | Intermedio (cubierto en lección 7.1) |
| Microsoft Teams: instalación y uso de aplicaciones | Básico |
| Power Automate: verificación de ejecuciones de flujos | Básico |
| Dataverse for Teams: consulta de registros en tablas | Básico (cubierto en práctica 4) |
| Diseño conversacional: temas, variables, condiciones | Intermedio (cubierto en prácticas 2–6) |

### Acceso y permisos requeridos

| Recurso | Permiso necesario | Estado esperado |
|---|---|---|
| Microsoft Copilot Studio | Propietario del agente o Maker | ✅ Activo desde práctica 2 |
| Microsoft Teams (desktop o web) | Usuario miembro del equipo del curso | ✅ Activo |
| Centro de Administración de Teams (`admin.teams.microsoft.com`) | Administrador de Teams o Global Admin | ✅ Coordinado con instructor |
| Dataverse for Teams | Propietario o miembro del equipo con acceso a la tabla `RevisionesControl` | ✅ Activo desde práctica 4 |
| Power Automate | Propietario del flujo de registro | ✅ Activo desde práctica 5 |
| SharePoint Online | Lector del sitio de fuentes de conocimiento | ✅ Activo desde práctica 4 |

> **⚠️ Nota importante:** Si no completaste la Práctica 6, solicita al instructor el artefacto de solución antes de iniciar este laboratorio. Este lab es secuencial y requiere el agente validado de la práctica anterior.

---

## Entorno de Laboratorio

### Hardware recomendado

| Componente | Mínimo | Recomendado |
|---|---|---|
| Procesador | Intel Core i5 8ª gen / AMD Ryzen 5 | Intel Core i7 / AMD Ryzen 7 |
| Memoria RAM | 8 GB | 16 GB |
| Almacenamiento libre | 500 MB (capturas y documentos) | 2 GB |
| Resolución de pantalla | 1366 × 768 | 1920 × 1080 |
| Conexión a internet | 10 Mbps | 25 Mbps |

### Software y servicios

| Herramienta | Versión / Acceso | Uso en esta práctica |
|---|---|---|
| Microsoft Copilot Studio | Experiencia actual 2024-2025 | Publicación del agente y configuración de canal Teams |
| Microsoft Teams | Desktop o web, versión actual | Canal de despliegue e interfaz de conversación |
| Microsoft Dataverse for Teams | Integrado en Teams, versión actual | Verificación de registros generados |
| Microsoft Power Automate | Cloud, versión actual | Verificación de ejecuciones del workflow |
| Microsoft SharePoint Online | Cloud, versión actual | Fuentes de conocimiento consultadas |
| Microsoft Edge 120+ / Chrome 120+ | Versión actual | Navegación entre portales |

### Configuración previa al inicio

Antes de comenzar, verifica que los siguientes elementos estén en estado correcto:

```
Lista de verificación pre-laboratorio:
[ ] El agente de la Práctica 6 está en estado "Publicado" en Copilot Studio
    (si no, publicarlo ahora: Copilot Studio → [Tu agente] → Publicar)
[ ] Microsoft Teams está abierto y sesión activa con la cuenta del curso
[ ] Tienes acceso a admin.teams.microsoft.com (coordinar con instructor si no)
[ ] La tabla RevisionesControl en Dataverse for Teams tiene registros previos
    de las prácticas anteriores (confirmar que la tabla existe)
[ ] El flujo de Power Automate de registro está activo (estado: Activado)
[ ] Tienes acceso al sitio de SharePoint con los documentos de auditoría
```

---

## Pasos del Laboratorio

---

### Paso 1: Verificar el estado de publicación del agente y habilitar el canal de Teams

**Objetivo:** Confirmar que el agente está publicado con la versión más reciente y habilitar el canal de Microsoft Teams en Copilot Studio para generar el manifiesto de aplicación.

#### Instrucciones

1. Abre tu navegador y navega a [https://copilotstudio.microsoft.com](https://copilotstudio.microsoft.com). Inicia sesión con tu cuenta del curso.

2. En el panel izquierdo, selecciona **Mis agentes** y haz clic en el agente de auditoría interna que construiste en las prácticas anteriores (por ejemplo, **"Agente Auditoría Interna"**).

3. En la barra superior del agente, verifica que el botón **Publicar** no muestre un indicador de cambios pendientes. Si hay cambios sin publicar, haz clic en **Publicar** y espera a que el proceso finalice (aproximadamente 30–60 segundos).

   ```
   Estado esperado: "Tu agente está publicado" o "Última publicación: [fecha reciente]"
   ```

4. En el panel de navegación izquierdo del agente, haz clic en **Configuración** (ícono de engranaje).

5. En el menú de Configuración, selecciona **Canales**.

6. Localiza la tarjeta de **Microsoft Teams** y haz clic en ella.

7. Si el canal no está habilitado, haz clic en el botón **Habilitar Teams**. Si ya está habilitado (de una práctica anterior), verás el botón **Editar detalles** — continúa al paso 8.

   ```
   Ruta: Agente → Configuración → Canales → Microsoft Teams → Habilitar Teams
   ```

8. Una vez habilitado, haz clic en **Editar detalles** y completa o verifica los siguientes metadatos de la aplicación:

   | Campo | Valor a usar |
   |---|---|
   | **Nombre corto** | `Agente Auditoría Interna` |
   | **Nombre completo** | `Agente de Auditoría Interna - [Tu nombre o iniciales]` |
   | **Descripción corta** | `Agente conversacional para captura y registro de controles internos` |
   | **Descripción larga** | `Este agente asiste al equipo de auditoría interna en la captura, validación y registro de revisiones de controles internos. Consulta fuentes de conocimiento institucionales y registra los resultados automáticamente en Dataverse.` |

9. Haz clic en **Guardar** para confirmar los metadatos.

10. Verifica que la sección de autenticación esté correctamente configurada: desde **Configuración → Seguridad → Autenticación**, confirma que la opción seleccionada sea **"Autenticar con Microsoft"** y que **"Requerir inicio de sesión"** esté activado.

    ```
    Ruta: Agente → Configuración → Seguridad → Autenticación
    → "Autenticar con Microsoft" ✅
    → Requerir inicio de sesión: Activado ✅
    ```

#### Resultado esperado

El canal de Microsoft Teams aparece como **habilitado** en la sección de Canales de Copilot Studio. Los metadatos de la aplicación están completos y guardados. La autenticación está configurada con Microsoft Entra ID.

#### Verificación

- [ ] La tarjeta de Microsoft Teams en Canales muestra estado **"Habilitado"** o una marca de verificación verde.
- [ ] Al hacer clic en **Editar detalles**, los campos de nombre y descripción muestran los valores ingresados.
- [ ] En **Configuración → Seguridad → Autenticación**, la opción activa es **"Autenticar con Microsoft"**.

---

### Paso 2: Configurar permisos de acceso en el Centro de Administración de Teams

**Objetivo:** Gestionar la disponibilidad del agente como aplicación de Teams asignándola únicamente al grupo de auditores del curso, siguiendo el principio de mínimo privilegio.

> **Nota para el instructor:** Este paso requiere acceso de administrador a `admin.teams.microsoft.com`. Si los participantes no tienen este acceso, el instructor debe ejecutar los pasos 2.1 a 2.5 en modo demostración y los participantes continúan desde el paso 3. Alternativamente, el instructor puede haber preconfigurado la directiva antes del laboratorio.

#### Instrucciones

1. Abre una nueva pestaña en el navegador y navega a [https://admin.teams.microsoft.com](https://admin.teams.microsoft.com). Inicia sesión con la cuenta de administrador del tenant del curso.

2. En el menú de navegación izquierdo, expande **Aplicaciones de Teams** y haz clic en **Administrar aplicaciones**.

3. En la barra de búsqueda, escribe el nombre del agente: `Agente Auditoría Interna`. Localiza la aplicación en los resultados.

   > Si la aplicación no aparece, puede deberse a que la sincronización del canal desde Copilot Studio tarda unos minutos. Espera 2–3 minutos y recarga la página.

4. Haz clic sobre el nombre de la aplicación para abrir sus detalles. Verifica que el campo **Estado** sea **"Permitida"**. Si aparece como **"Bloqueada"**, cambia el estado a **"Permitida"** y guarda.

5. Regresa al menú principal y navega a **Aplicaciones de Teams → Directivas de configuración de aplicaciones**.

6. Haz clic en **+ Agregar** para crear una nueva directiva con los siguientes datos:

   | Campo | Valor |
   |---|---|
   | **Nombre de la directiva** | `Directiva-AuditoriaInterna-Lab` |
   | **Descripción** | `Directiva de acceso al agente de auditoría para participantes del laboratorio` |

7. En la sección **Aplicaciones instaladas**, haz clic en **+ Agregar aplicaciones** y busca `Agente Auditoría Interna`. Selecciónala y haz clic en **Agregar**.

8. En la sección **Aplicaciones ancladas** (opcional pero recomendado), agrega también la misma aplicación para que aparezca anclada en la barra lateral de Teams de los auditores.

9. Haz clic en **Guardar** para crear la directiva.

10. Una vez creada la directiva, haz clic en **Administrar usuarios** (o **Asignar directiva a usuarios/grupos**) y asigna la directiva al grupo de seguridad del curso o a los usuarios participantes del laboratorio.

    ```
    Ruta resumen:
    admin.teams.microsoft.com
    → Aplicaciones de Teams → Administrar aplicaciones → [Agente] → Permitida
    → Directivas de configuración → + Agregar → Directiva-AuditoriaInterna-Lab
    → Asignar a usuarios/grupo del curso
    ```

11. Cierra la pestaña del Centro de Administración y regresa a Microsoft Teams.

#### Resultado esperado

La aplicación del agente está en estado **"Permitida"** en el catálogo de aplicaciones corporativas. Existe una directiva de configuración llamada **"Directiva-AuditoriaInterna-Lab"** asignada a los participantes del curso. Los usuarios del grupo pueden encontrar e instalar la aplicación desde el catálogo de Teams.

#### Verificación

- [ ] La aplicación aparece en **Administrar aplicaciones** con estado **"Permitida"**.
- [ ] La directiva **"Directiva-AuditoriaInterna-Lab"** está visible en la lista de directivas de configuración.
- [ ] La directiva está asignada al grupo o usuarios del curso.

---

### Paso 3: Instalar y abrir el agente en Microsoft Teams

**Objetivo:** Instalar la aplicación del agente en el cliente de Teams del participante y verificar que se abre correctamente con autenticación activa.

#### Instrucciones

1. Abre Microsoft Teams (desktop o web). Asegúrate de estar conectado con tu cuenta del curso.

2. En la barra de navegación izquierda de Teams, haz clic en el ícono de **Aplicaciones** (cuadrícula de puntos o ícono de tienda).

3. En el cuadro de búsqueda de aplicaciones, escribe `Agente Auditoría Interna`.

4. Localiza la aplicación en los resultados (aparecerá en la sección de aplicaciones de tu organización, no en el marketplace público). Haz clic sobre ella.

5. En la ventana de detalles de la aplicación, haz clic en **Agregar** o **Abrir** (el texto varía según si ya está instalada o no).

   > Si ves el mensaje *"Esta aplicación no está disponible para ti"*, el administrador aún no ha propagado la directiva. La propagación puede tomar hasta 24 horas en algunos tenants. En ese caso, usa la opción alternativa del paso 6.

6. **Opción alternativa (si la directiva aún no propagó):** Regresa a Copilot Studio, navega a **Configuración → Canales → Microsoft Teams** y haz clic en el botón **Abrir en Teams**. Esto abrirá directamente una conversación con el agente sin necesidad de instalarlo desde el catálogo.

7. Una vez abierta la conversación con el agente en Teams, verifica que aparezca un mensaje de bienvenida del agente (el mensaje configurado en el tema de bienvenida durante las prácticas anteriores).

8. Si Teams solicita autenticación o permisos adicionales, acepta los permisos requeridos. Esto es normal la primera vez que un usuario inicia sesión con el agente.

   ```
   Flujo esperado en Teams:
   [Aplicaciones] → Buscar "Agente Auditoría Interna" → Agregar → Chat abierto
   Mensaje de bienvenida: "Hola, soy el Agente de Auditoría Interna..."
   ```

#### Resultado esperado

El agente aparece como una aplicación de chat en Teams. Al abrirlo, muestra el mensaje de bienvenida configurado en el tema de inicio. La sesión está autenticada con la cuenta del curso (el agente reconoce al usuario).

#### Verificación

- [ ] El agente aparece en el panel de chat de Teams como una aplicación instalada.
- [ ] El mensaje de bienvenida se muestra correctamente en la conversación.
- [ ] No hay mensajes de error de autenticación o permisos sin resolver.

---

### Paso 4: Ejecutar el flujo de auditoría de extremo a extremo — Escenario estándar

**Objetivo:** Ejecutar una revisión completa de control interno desde Teams, recorriendo todos los componentes del agente: captura conversacional, consulta de conocimiento, respuesta generativa y registro automático en Dataverse.

> **Contexto del escenario:** Eres un auditor interno que va a revisar el control **"Segregación de funciones en el proceso de pagos"**. El control tiene un nivel de riesgo **Medio**, el resultado de la revisión es **Cumple** y la evidencia recopilada es una captura de pantalla del sistema de pagos. Este es el escenario estándar (sin excepción).

#### Instrucciones

1. En la ventana de chat del agente en Teams, escribe el mensaje de inicio para activar el tema de revisión de controles. Usa una frase natural como:

   ```
   Quiero registrar una revisión de control
   ```

   o el disparador configurado en tu agente durante las prácticas anteriores (por ejemplo: *"iniciar revisión"*, *"nueva auditoría"*).

2. El agente debe responder con el flujo de captura de datos. Responde a cada pregunta del agente con los siguientes valores del escenario estándar:

   | Pregunta del agente | Respuesta a ingresar |
   |---|---|
   | Nombre o ID del control | `CTR-PAG-001 - Segregación de funciones en pagos` |
   | Área o proceso auditado | `Tesorería / Proceso de pagos` |
   | Fecha de revisión | `[Fecha de hoy en formato DD/MM/AAAA]` |
   | Nombre del auditor | `[Tu nombre completo]` |
   | Nivel de riesgo del control | `Medio` |
   | Resultado de la revisión | `Cumple` |
   | Evidencia recopilada | `Captura de pantalla del sistema de pagos - Segregación verificada` |
   | Observaciones adicionales | `Control operando correctamente. No se identificaron hallazgos.` |

3. Después de ingresar todos los datos, el agente debe mostrar un **resumen de la revisión** y solicitar confirmación. Revisa que los datos mostrados sean correctos y responde con la opción de confirmación (por ejemplo: *"Confirmar"*, *"Sí"*, o el botón de confirmación si el agente usa tarjetas adaptativas).

4. Tras confirmar, observa el comportamiento del agente:
   - Debe mostrar un mensaje indicando que está **procesando el registro** o **guardando la información**.
   - El agente debe activar el flujo de Power Automate para escribir el registro en Dataverse.
   - Después de unos segundos (5–15 segundos dependiendo de la velocidad del flujo), el agente debe mostrar un **mensaje de confirmación** con el número o ID del registro creado.

   ```
   Mensaje de confirmación esperado (ejemplo):
   "✅ La revisión del control CTR-PAG-001 ha sido registrada exitosamente.
   ID de registro: [número generado por Dataverse]
   Fecha y hora de registro: [timestamp]
   Puedes consultar el registro en la tabla de Revisiones de Dataverse."
   ```

5. Una vez recibida la confirmación, prueba la **consulta de conocimiento** del agente. Escribe una pregunta relacionada con los documentos de auditoría cargados como fuentes de conocimiento en la Práctica 4:

   ```
   ¿Cuáles son los criterios para clasificar un control como de alto riesgo?
   ```

   o bien:

   ```
   ¿Qué procedimiento debo seguir cuando un control no cumple?
   ```

6. Observa la respuesta del agente:
   - Debe proporcionar una **respuesta generativa** basada en los documentos de SharePoint configurados como fuentes de conocimiento.
   - La respuesta debe incluir una **referencia o cita** al documento fuente (comportamiento de IA generativa fundamentada).
   - La respuesta NO debe ser inventada; debe estar fundamentada en los documentos cargados.

7. Toma una **captura de pantalla** de la conversación completa en Teams mostrando: la captura de datos, el resumen, la confirmación de registro y la respuesta de conocimiento. Guárdala como `evidencia_escenario_estandar.png`.

#### Resultado esperado

La conversación en Teams recorrió todos los componentes del agente sin interrupciones: captura de datos, confirmación, activación del workflow, mensaje de confirmación de registro y respuesta generativa fundamentada a la consulta de conocimiento. El agente se comportó como un asistente de auditoría funcional dentro del entorno de Teams.

#### Verificación

- [ ] El agente capturó todos los campos de la revisión sin errores de conversación.
- [ ] Se recibió un mensaje de confirmación de registro con ID o referencia del registro creado.
- [ ] La respuesta a la consulta de conocimiento está fundamentada en los documentos fuente (no es una respuesta genérica sin referencia).
- [ ] La captura de pantalla `evidencia_escenario_estandar.png` está guardada.

---

### Paso 5: Ejecutar el flujo de auditoría — Escenario de excepción (alto riesgo, no cumplimiento)

**Objetivo:** Validar la ruta de excepción del agente ejecutando un escenario de control con alto riesgo y resultado de no cumplimiento, verificando que el agente active la alerta correspondiente.

> **Contexto del escenario:** Eres el mismo auditor, ahora revisando el control **"Aprobación de pagos superiores a $50,000"**. Este control tiene nivel de riesgo **Alto**, el resultado es **No Cumple** y la evidencia muestra que se realizaron 3 pagos sin la aprobación requerida. Este escenario debe activar la ruta de alerta configurada en las prácticas anteriores.

#### Instrucciones

1. En la misma ventana de chat del agente en Teams (o inicia una nueva conversación), activa nuevamente el tema de revisión de controles con el disparador configurado:

   ```
   Iniciar nueva revisión de control
   ```

2. Completa el flujo conversacional con los datos del escenario de excepción:

   | Pregunta del agente | Respuesta a ingresar |
   |---|---|
   | Nombre o ID del control | `CTR-PAG-002 - Aprobación de pagos superiores a $50,000` |
   | Área o proceso auditado | `Tesorería / Proceso de pagos` |
   | Fecha de revisión | `[Fecha de hoy en formato DD/MM/AAAA]` |
   | Nombre del auditor | `[Tu nombre completo]` |
   | Nivel de riesgo del control | `Alto` |
   | Resultado de la revisión | `No Cumple` |
   | Evidencia recopilada | `3 pagos ejecutados sin aprobación del nivel jerárquico requerido` |
   | Observaciones adicionales | `Hallazgo crítico: incumplimiento del control de aprobación. Requiere acción correctiva inmediata.` |

3. Cuando el agente muestre el resumen y solicite confirmación, confirma el registro.

4. Observa con atención el comportamiento del agente tras la confirmación:
   - Debe mostrar el mensaje de confirmación de registro (igual que en el escenario estándar).
   - **Adicionalmente**, debe mostrar un **mensaje de alerta** diferenciado por el nivel de riesgo Alto y el resultado No Cumple. Este mensaje fue configurado en la ruta de excepción de las prácticas anteriores.

   ```
   Mensaje de alerta esperado (ejemplo):
   "⚠️ ALERTA: Se ha registrado un hallazgo de ALTO RIESGO con resultado NO CUMPLE.
   Control: CTR-PAG-002
   Este hallazgo requiere notificación al Auditor Líder y acción correctiva inmediata.
   Se ha enviado una notificación automática al responsable del área."
   ```

5. Verifica que el **flujo de Power Automate** haya procesado este registro. Abre una nueva pestaña y navega a [https://make.powerautomate.com](https://make.powerautomate.com). Ve a **Mis flujos** y localiza el flujo de registro de revisiones. Haz clic en el historial de ejecuciones y confirma que hay una ejecución reciente (en los últimos 2–3 minutos) con estado **"Correcto"**.

6. Toma una **captura de pantalla** de:
   - La conversación en Teams mostrando el mensaje de alerta.
   - El historial de ejecuciones del flujo en Power Automate con las dos ejecuciones recientes (escenario estándar y escenario de excepción).

   Guárdalas como `evidencia_escenario_excepcion.png` y `evidencia_powerautomate_ejecuciones.png`.

#### Resultado esperado

El agente diferenció correctamente el escenario de excepción del estándar, mostrando un mensaje de alerta específico para hallazgos de alto riesgo con no cumplimiento. El flujo de Power Automate ejecutó correctamente para ambos escenarios y el historial muestra dos ejecuciones exitosas.

#### Verificación

- [ ] El agente mostró un mensaje de alerta diferenciado para el escenario de alto riesgo / no cumplimiento.
- [ ] El flujo de Power Automate tiene dos ejecuciones recientes con estado **"Correcto"**.
- [ ] Las capturas de pantalla de evidencia están guardadas.

---

### Paso 6: Verificar los registros creados en Dataverse for Teams

**Objetivo:** Confirmar que los dos registros de revisión creados desde Teams existen en la tabla de Dataverse for Teams con todos los campos correctamente poblados.

#### Instrucciones

1. Abre Microsoft Teams y navega al equipo del curso donde está configurado Dataverse for Teams.

2. En la barra de navegación superior del equipo, busca la pestaña o aplicación de **Power Apps** integrada en el equipo (configurada durante la Práctica 4). Si no está disponible como pestaña, usa el método alternativo del paso 3.

3. **Método alternativo:** Abre una nueva pestaña en el navegador y navega a [https://make.powerapps.com](https://make.powerapps.com). En el selector de entorno (esquina superior derecha), selecciona el entorno de Dataverse for Teams del equipo del curso (su nombre suele ser el nombre del equipo de Teams).

4. En el panel izquierdo, haz clic en **Tablas** (o **Dataverse → Tablas**).

5. Busca y selecciona la tabla **`RevisionesControl`** (o el nombre que le hayas asignado durante la Práctica 4).

6. Haz clic en **Editar** o **Ver datos** para abrir la vista de registros de la tabla.

7. Verifica que los dos registros creados desde Teams estén presentes. Para cada registro, confirma que los siguientes campos estén correctamente poblados:

   **Registro 1 — Escenario estándar:**

   | Campo | Valor esperado |
   |---|---|
   | ID Control | `CTR-PAG-001 - Segregación de funciones en pagos` |
   | Área Auditada | `Tesorería / Proceso de pagos` |
   | Nivel Riesgo | `Medio` |
   | Resultado | `Cumple` |
   | Auditor | `[Tu nombre]` |
   | Evidencia | `Captura de pantalla del sistema de pagos...` |
   | Fecha Revisión | `[Fecha de hoy]` |
   | Fecha Registro | `[Timestamp automático]` |

   **Registro 2 — Escenario de excepción:**

   | Campo | Valor esperado |
   |---|---|
   | ID Control | `CTR-PAG-002 - Aprobación de pagos superiores a $50,000` |
   | Nivel Riesgo | `Alto` |
   | Resultado | `No Cumple` |
   | Observaciones | `Hallazgo crítico...` |

8. Toma una **captura de pantalla** de la vista de tabla en Dataverse mostrando ambos registros. Guárdala como `evidencia_dataverse_registros.png`.

9. Haz clic en el registro del escenario de excepción (CTR-PAG-002) para abrir su vista de detalle. Verifica que todos los campos estén completos y que no haya campos vacíos o con valores incorrectos. Toma una captura adicional si es necesario.

#### Resultado esperado

La tabla `RevisionesControl` en Dataverse for Teams contiene los dos registros recién creados desde la conversación en Teams. Todos los campos están correctamente poblados con los valores ingresados durante la conversación, confirmando que el flujo de Power Automate escribió los datos de forma íntegra.

#### Verificación

- [ ] Ambos registros (CTR-PAG-001 y CTR-PAG-002) aparecen en la tabla `RevisionesControl`.
- [ ] Los campos de nivel de riesgo, resultado y evidencia coinciden con los valores ingresados en la conversación.
- [ ] El campo de fecha/hora de registro fue poblado automáticamente por el flujo.
- [ ] La captura de pantalla `evidencia_dataverse_registros.png` está guardada.

---

### Paso 7: Documentar el plan de mantenimiento del agente

**Objetivo:** Elaborar un documento de plan de mantenimiento del agente con al menos cinco consideraciones operativas que garanticen su operación sostenida, segura y de calidad en el equipo auditor.

#### Instrucciones

1. Abre Microsoft Word (o cualquier editor de texto compatible) y crea un nuevo documento llamado `Plan_Mantenimiento_AgenteAuditoria.docx`.

2. Usa la siguiente estructura base para el documento y completa cada sección con el contenido indicado:

```markdown
# Plan de Mantenimiento — Agente de Auditoría Interna
**Fecha de elaboración:** [Fecha de hoy]
**Elaborado por:** [Tu nombre]
**Versión del agente:** 1.0 (Post-laboratorio)

## 1. Información General del Agente
- Nombre: Agente Auditoría Interna
- Plataforma: Microsoft Copilot Studio
- Canal de despliegue: Microsoft Teams
- Entorno de datos: Dataverse for Teams — Equipo [nombre del equipo del curso]
- Flujo de automatización: Power Automate — [nombre del flujo]
- Fuentes de conocimiento: SharePoint Online — [nombre del sitio]

## 2. Consideraciones Operativas de Mantenimiento
[Incluir MÍNIMO 5 consideraciones — ver instrucciones abajo]

## 3. Calendario de Revisión Sugerido
[Completar según instrucciones]

## 4. Responsables
[Completar según instrucciones]
```

3. Para la sección **"2. Consideraciones Operativas de Mantenimiento"**, documenta **al menos 5** de las siguientes consideraciones (puedes incluir más):

   **Consideración 1 — Actualización de fuentes de conocimiento:**
   Describe con qué frecuencia se deben revisar y actualizar los documentos de SharePoint que sirven como fuente de conocimiento del agente (procedimientos, políticas, matrices de controles). Indica quién es responsable y qué ocurre si los documentos quedan desactualizados.

   **Consideración 2 — Gestión de cambios en el agente:**
   Documenta el proceso que debe seguirse cuando se necesite modificar un tema, agregar un nuevo control al flujo o cambiar una variable. Incluye la importancia de publicar el agente (`Publicar` en Copilot Studio) después de cada cambio para que los usuarios en Teams reciban la versión actualizada.

   **Consideración 3 — Monitoreo de ejecuciones de Power Automate:**
   Describe la práctica de revisar periódicamente el historial de ejecuciones del flujo de registro en Power Automate para detectar errores, flujos fallidos o registros no creados. Indica la frecuencia recomendada (semanal durante el primer mes, mensual después) y las acciones a tomar ante errores.

   **Consideración 4 — Revisión de permisos y licencias:**
   Documenta la necesidad de verificar periódicamente que todos los auditores tienen licencias activas de Copilot Studio y Power Automate, y que los permisos de conectores (Dataverse, SharePoint) siguen siendo válidos. Indica qué ocurre si una licencia expira o un permiso es revocado.

   **Consideración 5 — Alcance definitivo del agente y control de temas fuera de alcance:**
   Describe los límites del agente: qué tipos de preguntas o solicitudes debe manejar y cuáles debe rechazar o redirigir. Documenta la importancia de mantener actualizado el mensaje de "fuera de alcance" para evitar respuestas inadecuadas o hallazgos de auditoría sobre el propio agente.

   **Consideración 6 (adicional recomendada) — Trazabilidad y retención de datos:**
   Documenta la política de retención de registros en Dataverse (¿cuánto tiempo se conservan las revisiones?), la habilitación del registro de transcripciones en Copilot Studio Analytics y la periodicidad de revisión de los logs de conversación para garantizar trazabilidad en el proceso de auditoría.

   **Consideración 7 (adicional recomendada) — Seguridad y gobierno de IA:**
   Documenta la necesidad de revisar periódicamente la configuración de autenticación (Microsoft Entra ID), las políticas DLP del entorno de Power Platform y el cumplimiento con las políticas de uso responsable de IA generativa de la organización.

4. Para la sección **"3. Calendario de Revisión Sugerido"**, completa la siguiente tabla:

   | Actividad de mantenimiento | Frecuencia | Responsable sugerido |
   |---|---|---|
   | Revisión de fuentes de conocimiento en SharePoint | Trimestral | Líder de Auditoría Interna |
   | Monitoreo de ejecuciones de Power Automate | Semanal (primer mes) / Mensual | Analista de Procesos / TI |
   | Verificación de licencias y permisos | Semestral | Administrador TI |
   | Prueba funcional del agente (ciclo completo) | Mensual | Auditor designado |
   | Revisión de temas y alcance del agente | Semestral o ante cambios de proceso | Líder de Auditoría + TI |
   | Análisis de transcripciones (Copilot Studio Analytics) | Mensual | Líder de Auditoría Interna |

5. Para la sección **"4. Responsables"**, documenta los roles clave para el mantenimiento del agente en producción:

   | Rol | Responsabilidades principales |
   |---|---|
   | **Propietario del agente (Maker)** | Modificar temas, publicar cambios, gestionar fuentes de conocimiento |
   | **Administrador de TI / Power Platform** | Gestionar licencias, permisos, políticas DLP, conectores |
   | **Líder de Auditoría Interna** | Validar alcance, aprobar cambios funcionales, revisar transcripciones |
   | **Administrador de Teams** | Gestionar directivas de aplicaciones, acceso de usuarios |

6. Guarda el documento. Si tienes acceso a SharePoint Online del curso, sube el documento al sitio de documentación del laboratorio.

#### Resultado esperado

El documento `Plan_Mantenimiento_AgenteAuditoria.docx` está completo con al menos 5 consideraciones operativas documentadas, el calendario de revisión y la tabla de responsables. El documento representa un artefacto real de gobernanza que podría usarse para la operación posterior del agente en un equipo de auditoría real.

#### Verificación

- [ ] El documento contiene la sección de información general del agente completa.
- [ ] Se documentaron al menos **5 consideraciones operativas** con descripción detallada de cada una.
- [ ] El calendario de revisión tiene al menos 5 actividades con frecuencia y responsable definidos.
- [ ] La tabla de responsables tiene al menos 4 roles documentados.
- [ ] El documento está guardado en formato `.docx` o equivalente.

---

## Validación y Pruebas del Laboratorio

Una vez completados todos los pasos, realiza la siguiente validación integral para confirmar que el laboratorio fue ejecutado de forma completa y exitosa.

### Lista de Validación Final

| # | Elemento a validar | Método de verificación | Estado |
|---|---|---|---|
| 1 | Canal de Teams habilitado en Copilot Studio | Configuración → Canales → Teams → "Habilitado" | ☐ |
| 2 | Autenticación configurada con Microsoft Entra ID | Configuración → Seguridad → Autenticación | ☐ |
| 3 | Directiva de aplicación creada en Centro de Administración | `admin.teams.microsoft.com` → Directivas de configuración | ☐ |
| 4 | Agente instalado y accesible en Teams | Conversación activa en Teams sin errores | ☐ |
| 5 | Escenario estándar ejecutado con confirmación de registro | Mensaje de confirmación con ID en Teams | ☐ |
| 6 | Respuesta generativa fundamentada a consulta de conocimiento | Respuesta con referencia al documento fuente | ☐ |
| 7 | Escenario de excepción ejecutado con mensaje de alerta | Mensaje de alerta diferenciado en Teams | ☐ |
| 8 | Dos ejecuciones exitosas del flujo en Power Automate | Historial de ejecuciones → estado "Correcto" | ☐ |
| 9 | Dos registros correctos en tabla Dataverse | Vista de tabla con CTR-PAG-001 y CTR-PAG-002 | ☐ |
| 10 | Plan de mantenimiento documentado (≥5 consideraciones) | Documento `.docx` guardado | ☐ |

### Evidencias requeridas para entrega

Confirma que tienes guardadas las siguientes capturas de pantalla y documentos:

```
Carpeta de evidencias del Lab 07:
├── evidencia_escenario_estandar.png
│   (Conversación completa en Teams: captura de datos + confirmación + consulta conocimiento)
├── evidencia_escenario_excepcion.png
│   (Conversación en Teams con mensaje de alerta de alto riesgo)
├── evidencia_powerautomate_ejecuciones.png
│   (Historial de ejecuciones del flujo con 2 ejecuciones exitosas)
├── evidencia_dataverse_registros.png
│   (Vista de tabla RevisionesControl con los 2 registros creados)
└── Plan_Mantenimiento_AgenteAuditoria.docx
    (Plan de mantenimiento con ≥5 consideraciones operativas)
```

---

## Resolución de Problemas

### Problema 1: El agente no aparece en el catálogo de aplicaciones de Teams después de habilitar el canal

**Síntomas:**
- Al buscar `Agente Auditoría Interna` en Aplicaciones de Teams, no aparece ningún resultado.
- El botón **Abrir en Teams** de Copilot Studio genera un error o abre una página en blanco.
- El mensaje en Teams indica: *"Esta aplicación no está disponible para tu organización"*.

**Causa probable:**
La propagación de la directiva de configuración de aplicaciones desde el Centro de Administración de Teams puede tardar entre 2 y 24 horas en algunos tenants. Adicionalmente, si la aplicación fue subida al catálogo corporativo pero su estado en **Administrar aplicaciones** es **"Bloqueada"** (en lugar de **"Permitida"**), los usuarios no podrán verla ni instalarla. También es posible que el canal de Teams en Copilot Studio no se haya habilitado correctamente si el paso de publicación del agente no se completó antes de habilitar el canal.

**Solución paso a paso:**

```
Paso 1 — Verificar estado de la aplicación:
  admin.teams.microsoft.com → Aplicaciones de Teams
  → Administrar aplicaciones → Buscar [nombre del agente]
  → Si estado = "Bloqueada": cambiar a "Permitida" → Guardar

Paso 2 — Verificar que el agente está publicado en Copilot Studio:
  Copilot Studio → [Agente] → Barra superior
  → Si hay botón "Publicar" activo con cambios pendientes: clic en Publicar
  → Esperar confirmación de publicación exitosa

Paso 3 — Usar el método de acceso directo mientras se propaga la directiva:
  Copilot Studio → Configuración → Canales → Microsoft Teams
  → Clic en "Abrir en Teams"
  → Esto abre una URL directa que no requiere que la directiva esté propagada

Paso 4 — Si el problema persiste después de 24 horas:
  Contactar al administrador del tenant para verificar que las directivas
  de aplicaciones de Teams no tienen restricciones adicionales a nivel
  de tenant que bloqueen aplicaciones de terceros o personalizadas.
```

---

### Problema 2: El agente responde en Teams pero el registro no se crea en Dataverse (no llega mensaje de confirmación o llega mensaje de error)

**Síntomas:**
- La conversación en Teams progresa normalmente hasta la confirmación, pero después no aparece el mensaje de confirmación de registro.
- El agente muestra un mensaje genérico de error como *"Algo salió mal"* o *"No pude completar la operación"*.
- Al verificar en Dataverse, el registro del escenario no existe en la tabla `RevisionesControl`.
- En el historial de ejecuciones de Power Automate, la ejecución aparece con estado **"Error"** o **"Cancelado"**.

**Causa probable:**
Este problema generalmente tiene tres orígenes: (1) el flujo de Power Automate está **desactivado** o fue desactivado automáticamente por inactividad; (2) las **credenciales del conector** de Dataverse en el flujo han expirado o el propietario del flujo cambió; (3) hay un **error en el mapeo de variables** entre lo que el agente envía al flujo y lo que el flujo espera recibir (por ejemplo, si el nombre de un parámetro fue modificado en el agente pero no en el flujo, o viceversa).

**Solución paso a paso:**

```
Paso 1 — Verificar estado del flujo:
  make.powerautomate.com → Mis flujos
  → Localizar el flujo de registro de revisiones
  → Si estado = "Desactivado": clic en los tres puntos → "Activar"
  → Confirmar que el estado cambia a "Activado"

Paso 2 — Revisar el historial de ejecuciones para identificar el error:
  Mis flujos → [Nombre del flujo] → Historial de ejecuciones
  → Clic en la ejecución fallida → Expandir el paso que falló
  → Leer el mensaje de error específico

Paso 3a — Si el error es de autenticación/credenciales:
  Mis flujos → [Nombre del flujo] → Editar
  → Localizar el paso de Dataverse → Clic en el paso
  → En "Conexión", seleccionar "Agregar nueva conexión" o "Reparar conexión"
  → Autenticar con las credenciales del curso → Guardar el flujo

Paso 3b — Si el error es de mapeo de parámetros:
  Copilot Studio → [Agente] → Temas → [Tema de revisión de control]
  → Localizar el nodo de llamada al flujo de Power Automate
  → Verificar que los nombres de los parámetros enviados coincidan
    exactamente con los nombres de los parámetros esperados en el flujo
  → Corregir cualquier discrepancia → Guardar → Publicar el agente

Paso 4 — Probar el flujo directamente desde Power Automate:
  Mis flujos → [Nombre del flujo] → Ejecutar manualmente
  → Ingresar valores de prueba para todos los parámetros
  → Verificar que la ejecución manual crea el registro en Dataverse
  → Si la ejecución manual funciona pero desde Teams no, el problema
    está en el paso de llamada al flujo desde el agente (Paso 3b)
```

---

## Limpieza del Entorno

Al finalizar el laboratorio, realiza las siguientes acciones de limpieza para mantener el entorno ordenado y evitar costos o conflictos en futuras sesiones.

> **⚠️ Importante:** No elimines el agente ni la tabla de Dataverse. Estos artefactos son el resultado del trabajo de todo el curso y pueden ser necesarios para evaluaciones o demostraciones posteriores.

### Acciones de limpieza recomendadas

1. **Cerrar pestañas innecesarias del navegador:** Cierra las pestañas de `admin.teams.microsoft.com`, `make.powerautomate.com` y `make.powerapps.com` que abriste durante el laboratorio.

2. **Verificar que el flujo de Power Automate permanece activo:** El flujo debe quedar en estado **"Activado"** para que el agente pueda seguir funcionando en pruebas posteriores o demostraciones.

3. **Confirmar la directiva de Teams (no eliminar):** La directiva `Directiva-AuditoriaInterna-Lab` debe permanecer activa para que los participantes del curso puedan seguir accediendo al agente en Teams.

4. **Archivar las evidencias del laboratorio:** Organiza las 4 capturas de pantalla y el documento de plan de mantenimiento en una carpeta local o en OneDrive:

   ```
   Carpeta sugerida: OneDrive → CopilotStudio_Curso → Lab07_Evidencias
   ```

5. **Registrar observaciones personales (opcional pero recomendado):** Antes de cerrar el laboratorio, toma 2 minutos para escribir en el documento de plan de mantenimiento una sección adicional de **"Observaciones del laboratorio"** donde anotes:
   - ¿Qué funcionó bien en la ejecución desde Teams?
   - ¿Qué aspectos del agente necesitarían mejora para un entorno de producción real?
   - ¿Qué ajustes harías al plan de mantenimiento basándote en lo que observaste hoy?

---

## Resumen

### Logros de esta práctica

En este laboratorio ejecutaste el ciclo completo de vida de un agente de auditoría interna en Microsoft Copilot Studio, llevándolo desde el entorno de pruebas hasta una operación real en Microsoft Teams. Los hitos alcanzados fueron:

1. **Publicación y configuración de canal:** Habilitaste el canal de Teams en Copilot Studio, completaste los metadatos de la aplicación y configuraste la autenticación obligatoria con Microsoft Entra ID.

2. **Gobierno y control de acceso:** Gestionaste la disponibilidad del agente en el Centro de Administración de Teams mediante directivas de configuración asignadas al grupo de auditores, aplicando el principio de mínimo privilegio.

3. **Ejecución de extremo a extremo — Escenario estándar:** Ejecutaste una revisión completa de control interno desde Teams, recorriendo todos los componentes: captura conversacional, respuesta generativa fundamentada en fuentes de conocimiento, activación del workflow de Power Automate y confirmación de registro en Dataverse.

4. **Validación de ruta de excepción:** Ejecutaste el escenario de alto riesgo / no cumplimiento y confirmaste que el agente activa correctamente el mensaje de alerta diferenciado, demostrando que las rutas de excepción diseñadas en prácticas anteriores funcionan en el entorno de producción.

5. **Verificación de registros en Dataverse:** Confirmaste la integridad de los datos registrados en la tabla `RevisionesControl`, validando que el flujo de Power Automate escribe correctamente todos los campos capturados en la conversación.

6. **Plan de mantenimiento:** Elaboraste un documento de gobernanza con al menos cinco consideraciones operativas que guiarán el uso sostenido y seguro del agente en el equipo auditor.

### Conceptos clave aplicados

| Concepto | Dónde se aplicó |
|---|---|
| Publicación de agente en canal Teams | Paso 1 — Copilot Studio → Canales |
| Control de acceso por grupos de seguridad | Paso 2 — Centro de Administración de Teams |
| Autenticación con Microsoft Entra ID | Paso 1 — Copilot Studio → Seguridad |
| Ejecución conversacional de extremo a extremo | Pasos 4 y 5 — Teams |
| Respuesta generativa fundamentada | Paso 4 — Consulta de conocimiento en Teams |
| Verificación de trazabilidad en Dataverse | Paso 6 — Tabla RevisionesControl |
| Gobierno de IA y mantenimiento de agentes | Paso 7 — Plan de mantenimiento |

### Felicitaciones

Has completado las **7 prácticas del curso**. El agente de auditoría interna que construiste desde cero — con temas conversacionales, entidades, variables, condiciones, rutas de excepción, fuentes de conocimiento, flujos de automatización y publicación en Teams — es un artefacto funcional que representa la integración de múltiples tecnologías de Microsoft 365 al servicio de un proceso real de auditoría interna.

### Recursos adicionales

| Recurso | URL |
|---|---|
| Publicar agente en Microsoft Teams — Copilot Studio | [https://learn.microsoft.com/es-es/microsoft-copilot-studio/publication-add-bot-to-microsoft-teams](https://learn.microsoft.com/es-es/microsoft-copilot-studio/publication-add-bot-to-microsoft-teams) |
| Administrar aplicaciones en Centro de Administración de Teams | [https://learn.microsoft.com/es-es/microsoftteams/manage-apps](https://learn.microsoft.com/es-es/microsoftteams/manage-apps) |
| Directivas de configuración de aplicaciones en Teams | [https://learn.microsoft.com/es-es/microsoftteams/teams-app-setup-policies](https://learn.microsoft.com/es-es/microsoftteams/teams-app-setup-policies) |
| Configurar autenticación de usuarios en Copilot Studio | [https://learn.microsoft.com/es-es/microsoft-copilot-studio/configuration-end-user-authentication](https://learn.microsoft.com/es-es/microsoft-copilot-studio/configuration-end-user-authentication) |
| Políticas DLP en Power Platform | [https://learn.microsoft.com/es-es/power-platform/admin/wp-data-loss-prevention](https://learn.microsoft.com/es-es/power-platform/admin/wp-data-loss-prevention) |
| Analíticas y transcripciones en Copilot Studio | [https://learn.microsoft.com/es-es/microsoft-copilot-studio/analytics-overview](https://learn.microsoft.com/es-es/microsoft-copilot-studio/analytics-overview) |

---
