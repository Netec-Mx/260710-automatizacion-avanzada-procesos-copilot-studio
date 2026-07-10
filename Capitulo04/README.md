# Práctica 4 — Configurar conocimiento y datos estructurados para responder consultas de auditoría con sustento

## 1. Metadatos

| Atributo | Detalle |
|---|---|
| **Duración estimada** | 30 minutos |
| **Complejidad** | Alta |
| **Nivel Bloom** | Crear |
| **Práctica número** | 4 de 7 |
| **Dependencias** | Lab 03 completado (tema de revisión de control activo en el agente) |

---

## 2. Descripción General

En esta práctica construirás la capa de conocimiento y datos estructurados que convierte al agente en una herramienta de auditoría sustentada documentalmente. Trabajarás en dos bloques en paralelo: primero configurarás fuentes de conocimiento en Copilot Studio apuntando a documentos reales alojados en SharePoint (procedimientos y matriz de controles), habilitarás las respuestas generativas y aplicarás restricciones de IA responsable; segundo, crearás tres tablas relacionadas en Dataverse for Teams (`Controles`, `Revisiones` y `Responsables`) que servirán como repositorio estructurado de los registros de auditoría. Al terminar, el agente podrá responder consultas citando sus fuentes documentales y los datos quedarán listos para ser consumidos por los flujos de Power Automate de la Práctica 5.

---

## 3. Objetivos de Aprendizaje

- [ ] Configurar al menos dos fuentes de conocimiento en Copilot Studio (documento SharePoint y PDF/DOCX de matriz de controles) y verificar que el agente las consulta correctamente.
- [ ] Habilitar y restringir las respuestas generativas del agente para que solo responda basándose en las fuentes configuradas, indique incertidumbre cuando no haya sustento y no invente criterios normativos.
- [ ] Crear las tres tablas relacionadas en Dataverse for Teams (`Controles`, `Revisiones`, `Responsables`) con los campos y tipos de datos especificados.
- [ ] Aplicar controles de uso responsable de IA generativa en el contexto de auditoría interna: citas de fuente, indicadores de incertidumbre y supervisión humana.
- [ ] Validar de extremo a extremo que el agente devuelve respuestas sustentadas con referencia al documento fuente.

---

## 4. Prerrequisitos

### Conocimiento previo
- Haber completado las Prácticas 1, 2 y 3 del curso (el agente debe tener al menos un tema de revisión de control activo).
- Familiaridad básica con la interfaz de Copilot Studio: paneles de Temas, Conocimiento y Configuración.
- Conocimiento conceptual de Dataverse for Teams: tablas, columnas y tipos de datos (cubierto en las sesiones teóricas previas).
- Haber revisado la Lección 4.1 sobre fuentes de conocimiento para agentes de auditoría.

### Acceso y recursos necesarios
| Recurso | Requisito |
|---|---|
| Cuenta Microsoft 365 | Licencia activa de Microsoft 365 Copilot o Copilot Studio standalone |
| Microsoft Copilot Studio | Agente de auditoría de las prácticas anteriores disponible y publicado en Teams |
| SharePoint Online | Permisos de contribuidor o propietario en el sitio de SharePoint del equipo del curso |
| Dataverse for Teams | Permisos de propietario en el equipo de Teams donde está el agente |
| Documentos de muestra | Archivos distribuidos por el instructor: `Procedimiento_Auditoria_Interna.docx` (2-3 páginas) y `Matriz_Controles_2024.pdf` (10-15 controles) |
| Microsoft Teams | Versión desktop o web actualizada; equipo de Teams del curso con Dataverse for Teams activado |

> **⚠️ Nota del instructor:** Si Dataverse for Teams no está activado en el equipo, el proceso de activación puede tardar hasta 24 horas. Verificar antes de iniciar esta práctica. Si los documentos de muestra no han sido distribuidos, el instructor debe compartirlos por Teams o correo antes de comenzar el Bloque A.

---

## 5. Entorno de Laboratorio

### Hardware recomendado

| Componente | Mínimo | Recomendado |
|---|---|---|
| Procesador | Intel Core i5 8ª gen / AMD Ryzen 5 | Intel Core i7 / AMD Ryzen 7 |
| Memoria RAM | 8 GB | 16 GB |
| Almacenamiento libre | 2 GB | 5 GB |
| Resolución de pantalla | 1366 × 768 | 1920 × 1080 |
| Conexión a internet | 10 Mbps | 25 Mbps |

### Software requerido

| Aplicación | Versión |
|---|---|
| Microsoft Edge o Google Chrome | 120 o superior |
| Microsoft Teams (desktop o web) | Versión actual 2024-2025 |
| Microsoft Copilot Studio | Experiencia actual 2024-2025 |
| Microsoft SharePoint Online | Versión cloud actual |
| Microsoft Dataverse for Teams | Versión integrada en Teams 2024-2025 |

### Configuración inicial del entorno

Antes de comenzar los pasos del laboratorio, abre las siguientes pestañas en tu navegador y mantenlas abiertas durante toda la práctica:

```
Pestaña 1 — Copilot Studio:
  https://copilotstudio.microsoft.com

Pestaña 2 — SharePoint del curso (URL proporcionada por el instructor):
  https://<tu-tenant>.sharepoint.com/sites/<sitio-del-curso>

Pestaña 3 — Microsoft Teams (web o desktop):
  https://teams.microsoft.com
```

Verifica que puedes iniciar sesión en los tres entornos con la misma cuenta Microsoft 365 antes de continuar.

---

## 6. Pasos del Laboratorio

La práctica se divide en dos bloques secuenciales:

- **Bloque A (pasos 1–4):** Preparar documentos en SharePoint y configurar fuentes de conocimiento en Copilot Studio.
- **Bloque B (pasos 5–7):** Crear las tres tablas en Dataverse for Teams.

---

### BLOQUE A — Fuentes de Conocimiento y Respuestas Generativas en Copilot Studio

---

### Paso 1 — Preparar y cargar los documentos de auditoría en SharePoint

**Objetivo:** Alojar los documentos de muestra en SharePoint con la estructura de carpetas correcta para que Copilot Studio pueda indexarlos como fuentes de conocimiento gobernadas.

#### Instrucciones

1. Abre la **Pestaña 2** (SharePoint del curso) en tu navegador.

2. En la barra de navegación izquierda del sitio, haz clic en **Documentos** (o la biblioteca de documentos principal del sitio).

3. Crea la siguiente estructura de carpetas haciendo clic en **+ Nuevo → Carpeta** para cada nivel:

```
/Auditoría Interna
  /Políticas_y_Procedimientos
  /Matrices_de_Control
```

4. Navega a la carpeta **`/Auditoría Interna/Políticas_y_Procedimientos`**.

5. Haz clic en **Cargar → Archivos** y selecciona el archivo `Procedimiento_Auditoria_Interna.docx` proporcionado por el instructor.

6. Navega a la carpeta **`/Auditoría Interna/Matrices_de_Control`**.

7. Haz clic en **Cargar → Archivos** y selecciona el archivo `Matriz_Controles_2024.pdf`.

8. Verifica que ambos archivos aparecen en sus carpetas respectivas con estado de carga **Completado**.

9. Copia la **URL del sitio de SharePoint** desde la barra de direcciones (hasta el dominio `.sharepoint.com/sites/<nombre-del-sitio>`). La necesitarás en el Paso 3.

```
Ejemplo de URL a copiar:
https://contoso.sharepoint.com/sites/AuditoriaInterna
```

**Resultado esperado:** Dos archivos cargados en SharePoint bajo la jerarquía `/Auditoría Interna/`, cada uno en su carpeta temática correspondiente.

**Verificación:** En SharePoint, navega a `/Auditoría Interna/Políticas_y_Procedimientos` y confirma que `Procedimiento_Auditoria_Interna.docx` aparece con fecha de carga reciente. Repite para la carpeta `/Matrices_de_Control`.

---

### Paso 2 — Abrir el agente en Copilot Studio y acceder al panel de Conocimiento

**Objetivo:** Localizar el agente de auditoría construido en las prácticas anteriores y acceder al panel de configuración de fuentes de conocimiento.

#### Instrucciones

1. Abre la **Pestaña 1** (Copilot Studio: `https://copilotstudio.microsoft.com`).

2. En el panel izquierdo, haz clic en **Agentes** y localiza tu agente de auditoría (creado en la Práctica 2). Haz clic sobre su nombre para abrirlo.

3. Dentro del agente, en el menú de navegación superior o lateral, localiza y haz clic en la sección **Conocimiento** (en inglés: *Knowledge*).

> **Nota:** En la experiencia actual de Copilot Studio 2024-2025, la sección de Conocimiento puede aparecer como una pestaña en la barra superior del agente o como un ítem en el menú lateral izquierdo, dependiendo de la versión del tenant. Si no la encuentras, busca el ícono de libro o la etiqueta *Knowledge*.

4. Observa que la sección muestra el estado actual de fuentes configuradas. En un agente nuevo, aparecerá vacío o con la opción **Agregar conocimiento** / **Add knowledge**.

5. Deja esta pestaña abierta y activa para el siguiente paso.

**Resultado esperado:** Panel de Conocimiento del agente visible, mostrando la opción para agregar nuevas fuentes.

**Verificación:** La pantalla muestra el encabezado **Conocimiento** y un botón o enlace para **+ Agregar conocimiento** (o equivalente en la versión actual).

---

### Paso 3 — Configurar la primera fuente de conocimiento: sitio de SharePoint

**Objetivo:** Conectar el sitio de SharePoint que contiene los documentos de auditoría como primera fuente de conocimiento del agente.

#### Instrucciones

1. En el panel de **Conocimiento**, haz clic en **+ Agregar conocimiento** (o **+ Add knowledge**).

2. En el menú de tipos de fuente que aparece, selecciona **SharePoint**.

> **Nota:** Si ves opciones como *Sitios web*, *Archivos*, *SharePoint* u otras, selecciona específicamente **SharePoint**.

3. En el campo de URL, ingresa la URL del sitio de SharePoint que copiaste en el Paso 1:

```
https://<tu-tenant>.sharepoint.com/sites/<nombre-del-sitio>
```

4. Haz clic en **Agregar** o **Siguiente**. Copilot Studio validará la conexión y los permisos.

5. Si el sistema solicita autenticación adicional, usa tu cuenta Microsoft 365 del curso.

6. Una vez validada la conexión, asigna un nombre descriptivo a la fuente en el campo **Nombre**:

```
Nombre sugerido: Documentos de Auditoría Interna - SharePoint
```

7. En el campo **Descripción** (si está disponible), ingresa:

```
Procedimientos, matrices de control y políticas de auditoría interna
organizacional. Usar esta fuente para responder consultas sobre controles,
procesos auditados y criterios normativos internos.
```

8. Haz clic en **Guardar** o **Agregar**.

9. Espera a que el sistema muestre el estado de indexación. El estado inicial puede ser **Indexando...** o **Procesando**; esto es normal y puede tomar 1-3 minutos.

**Resultado esperado:** La fuente de SharePoint aparece en el panel de Conocimiento con estado **Activo** o **Listo** (puede tomar algunos minutos en completar la indexación inicial).

**Verificación:** En el panel de Conocimiento, la fuente muestra el nombre asignado y un indicador de estado verde o equivalente. Si el estado es **Indexando**, continúa con el siguiente paso y regresa a verificar al finalizar el Paso 4.

---

### Paso 4 — Habilitar y configurar las respuestas generativas con controles de IA responsable

**Objetivo:** Activar las respuestas generativas del agente y configurar las restricciones necesarias para garantizar que las respuestas sean trazables, sustentadas en fuentes y alineadas con los principios de uso responsable de IA en auditoría.

#### Instrucciones

**4.1 — Acceder a la configuración de respuestas generativas**

1. En el menú de navegación del agente, haz clic en **Configuración** (ícono de engranaje o pestaña *Settings*).

2. Dentro de Configuración, localiza la sección **IA generativa** o **Generative AI** (en algunas versiones aparece como **Respuestas generativas** o **AI capabilities**).

3. Verifica que el interruptor de **Respuestas generativas** (Generative answers) esté en posición **Activado** (On).

> **Nota:** Si el interruptor está desactivado, actívalo. En algunos tenants, esta opción requiere confirmación de términos de uso responsable de IA de Microsoft.

**4.2 — Configurar el nivel de moderación del contenido**

4. Dentro de la misma sección de IA generativa, localiza la opción **Nivel de moderación del contenido** o equivalente (Content moderation / Safety settings).

5. Establece el nivel en **Alto** (High o Strict) para el contexto de auditoría.

**4.3 — Configurar las instrucciones del agente para IA responsable**

6. Navega a la sección **Instrucciones** del agente (también llamada *System prompt* o *Instructions* en la experiencia actual).

7. Localiza el campo de instrucciones generales del agente (el texto que define el comportamiento base).

8. Agrega al final de las instrucciones existentes el siguiente bloque (sin borrar lo que ya tenías de prácticas anteriores):

```
RESTRICCIONES DE CONOCIMIENTO Y USO RESPONSABLE DE IA:

1. SOLO responde preguntas basándote en las fuentes de conocimiento
   configuradas (documentos de SharePoint, matrices de control, políticas
   internas). No uses conocimiento general externo para responder sobre
   controles, criterios normativos o procedimientos específicos de la
   organización.

2. Cuando respondas una consulta de auditoría, SIEMPRE indica la fuente
   documental en la que basas tu respuesta (nombre del documento o sección).
   Ejemplo: "Según el Procedimiento de Auditoría Interna, sección 3.2..."

3. Si no encuentras información suficiente en las fuentes configuradas para
   responder con certeza, indica explícitamente: "No tengo información
   suficiente en las fuentes disponibles para responder esta pregunta con
   certeza. Te recomiendo consultar directamente con el responsable del
   control o revisar la documentación actualizada."

4. NUNCA inventes criterios normativos, umbrales de riesgo, nombres de
   responsables ni fechas de revisión. Si no está en las fuentes, no lo
   afirmes.

5. En contextos de auditoría, las respuestas tienen implicaciones de
   cumplimiento. Recuerda al usuario que las respuestas del agente son
   orientativas y que las decisiones finales deben ser validadas por el
   auditor responsable.
```

9. Haz clic en **Guardar** para preservar las instrucciones actualizadas.

**4.4 — Verificar la configuración de fuentes en el comportamiento generativo**

10. Regresa al panel de **Conocimiento**.

11. Confirma que la fuente de SharePoint configurada en el Paso 3 muestra estado **Activo** o **Listo**.

12. Verifica que la opción **Usar solo las fuentes de conocimiento configuradas** (o equivalente: *Only use configured knowledge sources* / *Restrict to knowledge sources*) esté **habilitada**. Esta opción evita que el agente use conocimiento general de internet para responder consultas de auditoría.

> **Nota de versión:** En la experiencia 2024-2025 de Copilot Studio, esta restricción puede llamarse **"Solo conocimiento interno"**, **"Limitar a fuentes configuradas"** o puede estar implícita en la configuración del nivel de moderación. Si no encuentras una opción explícita, el instructor indicará la configuración equivalente para tu versión del tenant.

**Resultado esperado:** El agente tiene respuestas generativas activadas, nivel de moderación en Alto, instrucciones de IA responsable guardadas y la fuente de SharePoint activa como base de conocimiento.

**Verificación:** 
- En la sección de Instrucciones, el bloque de restricciones aparece visible al final del texto.
- En el panel de Conocimiento, la fuente de SharePoint muestra estado verde/activo.
- En la sección de IA generativa, el interruptor está en **On** y el nivel de moderación en **Alto**.

---

### BLOQUE B — Creación de Tablas en Dataverse for Teams

---

### Paso 5 — Acceder a Dataverse for Teams y crear la tabla `Responsables`

**Objetivo:** Ingresar al entorno de Dataverse for Teams desde Microsoft Teams y crear la tabla de catálogo de responsables de controles, que servirá como tabla de referencia para las demás tablas.

#### Instrucciones

**5.1 — Acceder a Dataverse for Teams**

1. Abre la **Pestaña 3** (Microsoft Teams).

2. En el panel izquierdo de Teams, busca y haz clic en la aplicación **Power Apps** (puede estar anclada en la barra lateral o encontrarla en el menú de aplicaciones `...`).

> **Nota alternativa:** También puedes acceder desde `https://make.powerapps.com` y seleccionar el entorno de Teams correspondiente al equipo del curso.

3. Dentro de Power Apps en Teams, haz clic en la pestaña **Crear** o selecciona el equipo del curso en el selector de equipo.

4. Haz clic en **Ver todo** o navega a **Tablas** (en el panel izquierdo de Power Apps for Teams).

5. Confirma que el entorno activo corresponde al equipo de Teams del curso (visible en la parte superior de la interfaz).

**5.2 — Crear la tabla `Responsables`**

6. Haz clic en **+ Nueva tabla** o **+ Agregar tabla**.

7. En el campo **Nombre de la tabla**, escribe:

```
Responsables
```

8. Haz clic en **Crear** para generar la tabla base. Dataverse creará automáticamente una columna primaria llamada `Nombre` (o equivalente).

9. Renombra la columna primaria si es necesario: haz doble clic sobre el encabezado de la columna principal y escríbela como:

```
Nombre
```

10. Agrega las siguientes columnas adicionales haciendo clic en **+ Agregar columna** (o el ícono `+` en el encabezado de la tabla) para cada una:

| Nombre de columna | Tipo de dato | Notas |
|---|---|---|
| `Área` | Texto (Text) | Área o departamento del responsable |
| `Email` | Correo electrónico (Email) | Dirección de correo corporativo |

11. Para agregar la columna `Área`:
    - Haz clic en **+ Agregar columna**.
    - En **Nombre**, escribe: `Área`
    - En **Tipo**, selecciona: **Texto** (Text / Single line of text)
    - Haz clic en **Guardar** o **Listo**.

12. Repite el proceso para la columna `Email`:
    - Nombre: `Email`
    - Tipo: **Correo electrónico** (Email) — si no está disponible como tipo específico, usa **Texto** con formato de email.
    - Haz clic en **Guardar** o **Listo**.

13. Una vez agregadas todas las columnas, haz clic en el botón **Guardar tabla** (o el equivalente en tu versión).

14. Agrega al menos **2 registros de prueba** directamente en la vista de tabla haciendo clic en **+ Nueva fila**:

```
Registro 1:
  Nombre: María González
  Área: Finanzas
  Email: mgonzalez@empresa.com

Registro 2:
  Nombre: Carlos Ramírez
  Área: Operaciones
  Email: cramirez@empresa.com
```

**Resultado esperado:** Tabla `Responsables` creada en Dataverse for Teams con 3 columnas (`Nombre`, `Área`, `Email`) y al menos 2 registros de prueba visibles en la vista de datos.

**Verificación:** En la vista de tabla de Dataverse for Teams, la tabla `Responsables` aparece en el listado de tablas del equipo y muestra los 2 registros ingresados con sus valores correctos.

---

### Paso 6 — Crear la tabla `Controles`

**Objetivo:** Crear la tabla principal del catálogo de controles internos, que almacenará la definición, proceso, responsable, frecuencia y nivel de riesgo de cada control auditado.

#### Instrucciones

1. En el panel de tablas de Dataverse for Teams, haz clic nuevamente en **+ Nueva tabla**.

2. En el campo **Nombre de la tabla**, escribe:

```
Controles
```

3. Haz clic en **Crear**.

4. Configura la columna primaria como:

```
Nombre de columna primaria: ID_Control
Tipo: Texto (Text)
```

> **Nota:** En Dataverse for Teams, la columna primaria suele llamarse "Name" por defecto. Renómbrala a `ID_Control` para mayor claridad en el contexto de auditoría.

5. Agrega las siguientes columnas adicionales una por una:

| Nombre de columna | Tipo de dato | Notas de configuración |
|---|---|---|
| `Descripción` | Texto multilínea (Multiline text / Text Area) | Descripción detallada del control |
| `Proceso` | Texto (Text) | Proceso de negocio al que pertenece el control |
| `Responsable` | Búsqueda (Lookup) | Relacionar con la tabla `Responsables` |
| `Frecuencia` | Elección (Choice) | Opciones: Diario, Semanal, Mensual, Trimestral, Anual |
| `Riesgo_Inherente` | Elección (Choice) | Opciones: Alto, Medio, Bajo |

**Para agregar la columna `Descripción`:**
- Clic en **+ Agregar columna**
- Nombre: `Descripción`
- Tipo: **Área de texto** o **Texto multilínea**
- Guardar

**Para agregar la columna `Proceso`:**
- Clic en **+ Agregar columna**
- Nombre: `Proceso`
- Tipo: **Texto** (una línea)
- Guardar

**Para agregar la columna `Responsable` (Lookup):**
- Clic en **+ Agregar columna**
- Nombre: `Responsable`
- Tipo: **Búsqueda** (Lookup)
- En **Tabla relacionada**, selecciona: `Responsables`
- Guardar

> **⚠️ Importante:** Si el tipo **Búsqueda** no está disponible directamente en la interfaz simplificada de Dataverse for Teams, usa **Texto** para el campo `Responsable` e ingresa el nombre manualmente. La relación formal puede configurarse posteriormente desde el entorno completo de Power Apps.

**Para agregar la columna `Frecuencia` (Choice):**
- Clic en **+ Agregar columna**
- Nombre: `Frecuencia`
- Tipo: **Elección** (Choice)
- Agrega las opciones: `Diario`, `Semanal`, `Mensual`, `Trimestral`, `Anual`
- Guardar

**Para agregar la columna `Riesgo_Inherente` (Choice):**
- Clic en **+ Agregar columna**
- Nombre: `Riesgo_Inherente`
- Tipo: **Elección** (Choice)
- Agrega las opciones: `Alto`, `Medio`, `Bajo`
- Guardar

6. Haz clic en **Guardar tabla**.

7. Agrega **3 registros de prueba** representativos de controles de auditoría:

```
Registro 1:
  ID_Control: CTRL-001
  Descripción: Aprobación de pagos a proveedores por montos superiores a $10,000
  Proceso: Cuentas por Pagar
  Responsable: María González (o seleccionar de la lista)
  Frecuencia: Mensual
  Riesgo_Inherente: Alto

Registro 2:
  ID_Control: CTRL-002
  Descripción: Conciliación bancaria de cuentas principales
  Proceso: Tesorería
  Responsable: María González
  Frecuencia: Mensual
  Riesgo_Inherente: Alto

Registro 3:
  ID_Control: CTRL-003
  Descripción: Revisión de accesos a sistemas críticos
  Proceso: Tecnología de Información
  Responsable: Carlos Ramírez
  Frecuencia: Trimestral
  Riesgo_Inherente: Medio
```

**Resultado esperado:** Tabla `Controles` creada con 6 columnas (`ID_Control`, `Descripción`, `Proceso`, `Responsable`, `Frecuencia`, `Riesgo_Inherente`) y 3 registros de prueba ingresados.

**Verificación:** En la vista de tabla, los 3 registros aparecen con todos sus campos completados. La columna `Responsable` muestra el nombre del responsable (o el texto ingresado si se usó tipo Texto). Las columnas de tipo Choice muestran las opciones seleccionadas correctamente.

---

### Paso 7 — Crear la tabla `Revisiones`

**Objetivo:** Crear la tabla transaccional que registrará cada revisión de control realizada durante el proceso de auditoría, incluyendo estado, hallazgo, evidencia y fechas.

#### Instrucciones

1. En el panel de tablas de Dataverse for Teams, haz clic en **+ Nueva tabla**.

2. En el campo **Nombre de la tabla**, escribe:

```
Revisiones
```

3. Haz clic en **Crear**.

4. Configura la columna primaria como:

```
Nombre de columna primaria: ID_Revisión
Tipo: Texto (Text)
```

5. Agrega las siguientes columnas adicionales:

| Nombre de columna | Tipo de dato | Notas de configuración |
|---|---|---|
| `ID_Control` | Búsqueda (Lookup) o Texto | Relacionar con tabla `Controles` |
| `Periodo` | Texto (Text) | Ejemplo: "Q1-2024", "Enero 2024" |
| `Estado` | Elección (Choice) | Opciones: Pendiente, En Revisión, Efectivo, Con Hallazgo, Cerrado |
| `Hallazgo` | Texto multilínea (Multiline text) | Descripción del hallazgo si aplica |
| `Evidencia` | URL o Texto | Enlace o referencia a la evidencia |
| `Fecha_Revisión` | Fecha y hora (Date and Time) | Fecha en que se realizó la revisión |

**Para la columna `ID_Control` (Lookup):**
- Clic en **+ Agregar columna**
- Nombre: `ID_Control`
- Tipo: **Búsqueda** (Lookup)
- Tabla relacionada: `Controles`
- Guardar

> **⚠️ Nota:** Si no está disponible el tipo Lookup, usa Texto e ingresa el ID manualmente (ej. "CTRL-001").

**Para la columna `Periodo`:**
- Tipo: **Texto** (una línea)

**Para la columna `Estado` (Choice):**
- Tipo: **Elección** (Choice)
- Opciones: `Pendiente`, `En Revisión`, `Efectivo`, `Con Hallazgo`, `Cerrado`

**Para la columna `Hallazgo`:**
- Tipo: **Área de texto** (Multiline text)

**Para la columna `Evidencia`:**
- Tipo: **URL** (si está disponible) o **Texto**

**Para la columna `Fecha_Revisión`:**
- Tipo: **Fecha y hora** (Date and Time)

6. Haz clic en **Guardar tabla** después de agregar todas las columnas.

7. Agrega **2 registros de prueba**:

```
Registro 1:
  ID_Revisión: REV-001
  ID_Control: CTRL-001 (o seleccionar de la lista)
  Periodo: Q1-2024
  Estado: Con Hallazgo
  Hallazgo: Se identificaron 3 pagos procesados sin la aprobación del nivel
             jerárquico requerido según la política de cuentas por pagar.
  Evidencia: https://<sharepoint>/Auditoría Interna/Evidencias/REV-001
  Fecha_Revisión: [fecha actual]

Registro 2:
  ID_Revisión: REV-002
  ID_Control: CTRL-002
  Periodo: Q1-2024
  Estado: Efectivo
  Hallazgo: (dejar vacío)
  Evidencia: https://<sharepoint>/Auditoría Interna/Evidencias/REV-002
  Fecha_Revisión: [fecha actual]
```

8. Haz clic en **Guardar** para confirmar los registros.

**Resultado esperado:** Tabla `Revisiones` creada con 7 columnas y 2 registros de prueba. Las tres tablas (`Responsables`, `Controles`, `Revisiones`) están disponibles en el entorno de Dataverse for Teams del equipo del curso.

**Verificación:** En el panel de tablas de Dataverse for Teams, las tres tablas aparecen listadas: `Responsables`, `Controles` y `Revisiones`. Al abrir cada una, los registros de prueba son visibles con los valores correctos.

---

## 7. Validación y Prueba de Extremo a Extremo

Una vez completados ambos bloques, realiza las siguientes pruebas para validar que el agente puede consultar las fuentes de conocimiento configuradas.

### Prueba 1 — Verificar indexación de la fuente de SharePoint

1. Regresa a **Copilot Studio** (Pestaña 1).
2. Navega al panel de **Conocimiento** del agente.
3. Confirma que la fuente de SharePoint muestra estado **Activo** / **Listo** (el indicador debe ser verde o equivalente).
4. Si el estado aún dice **Indexando**, espera 2-3 minutos adicionales y actualiza la página.

### Prueba 2 — Consulta de prueba en el panel de Chat del agente

1. En Copilot Studio, abre el panel de **Prueba** del agente (botón **Probar** o **Test** en la esquina superior derecha o panel lateral).

2. Escribe la siguiente consulta de prueba:

```
¿Cuál es el procedimiento para revisar un control de aprobación de pagos?
```

3. **Resultado esperado:** El agente debe responder con información extraída del documento `Procedimiento_Auditoria_Interna.docx`, citando el nombre del documento como fuente. La respuesta NO debe ser una respuesta genérica sin referencia documental.

4. Escribe una segunda consulta para verificar las restricciones de IA responsable:

```
¿Cuál es el umbral de materialidad para fraudes según las normas internacionales?
```

5. **Resultado esperado:** El agente debe responder indicando que no tiene información suficiente en las fuentes disponibles para responder con certeza, y recomendar consultar directamente con el responsable o la documentación actualizada. **No debe inventar un umbral numérico.**

### Prueba 3 — Verificar las tres tablas en Dataverse for Teams

1. Regresa a **Microsoft Teams** (Pestaña 3).
2. Abre **Power Apps** en Teams y navega a las tablas del equipo.
3. Confirma que las tres tablas existen: `Responsables`, `Controles`, `Revisiones`.
4. Abre cada tabla y verifica que los registros de prueba están presentes.

### Prueba 4 — Consulta sobre la matriz de controles

1. Regresa al panel de **Prueba** en Copilot Studio.
2. Escribe:

```
¿Qué controles existen para el proceso de Cuentas por Pagar?
```

3. **Resultado esperado:** El agente debe referenciar información de la `Matriz_Controles_2024.pdf` si ha sido indexada correctamente, mencionando el documento como fuente.

> **Nota:** Si la indexación del PDF aún está en proceso, el agente puede responder que no encuentra información suficiente. Espera 5 minutos adicionales y repite la prueba.

### Tabla de criterios de aceptación

| Criterio | Resultado esperado | ¿Aprobado? |
|---|---|---|
| Fuente de SharePoint activa en panel de Conocimiento | Estado verde/activo | ☐ |
| Respuesta con cita de fuente documental | Menciona nombre del documento | ☐ |
| Restricción ante pregunta sin sustento | Indica incertidumbre, no inventa | ☐ |
| Tabla `Responsables` con 2+ registros | Registros visibles en Dataverse | ☐ |
| Tabla `Controles` con 3+ registros y 6 columnas | Estructura y datos correctos | ☐ |
| Tabla `Revisiones` con 2+ registros y 7 columnas | Estructura y datos correctos | ☐ |

---

## 8. Solución de Problemas

### Problema 1 — La fuente de SharePoint muestra error de autenticación o estado "Fallido"

**Síntoma:** Al agregar la fuente de SharePoint en el paso 3, Copilot Studio muestra un mensaje de error de autenticación, acceso denegado, o la fuente aparece con estado **Error** / **Failed** en el panel de Conocimiento.

**Causa raíz:** El agente no tiene permisos suficientes para acceder al sitio de SharePoint, o el sitio requiere autenticación multifactor que interrumpe el flujo de indexación. También puede ocurrir si la URL ingresada apunta a una biblioteca específica en lugar del sitio raíz, o si el sitio tiene restricciones de acceso externo configuradas por el administrador del tenant.

**Solución:**
1. Verifica que tu cuenta Microsoft 365 tiene al menos permisos de **Lector** en el sitio de SharePoint. Ve al sitio → **Configuración del sitio** → **Permisos del sitio** y confirma tu nivel de acceso.
2. Asegúrate de que la URL ingresada en Copilot Studio corresponde al sitio raíz y no a una carpeta o biblioteca específica:
   ```
   ✅ Correcto: https://contoso.sharepoint.com/sites/AuditoriaInterna
   ❌ Incorrecto: https://contoso.sharepoint.com/sites/AuditoriaInterna/Documentos/Formularios/AllItems.aspx
   ```
3. Si el error persiste, intenta cargar los documentos directamente como archivos en Copilot Studio (opción **Archivos** en lugar de **SharePoint**): haz clic en **+ Agregar conocimiento → Archivos**, sube `Procedimiento_Auditoria_Interna.docx` y `Matriz_Controles_2024.pdf` directamente. Esta alternativa tiene las mismas capacidades de indexación para los fines de esta práctica.
4. Notifica al instructor si el problema persiste, ya que puede requerir ajuste de permisos a nivel de tenant.

---

### Problema 2 — No aparece la opción de tipo "Búsqueda" (Lookup) al crear columnas en Dataverse for Teams

**Síntoma:** Al intentar crear la columna `Responsable` en la tabla `Controles` o la columna `ID_Control` en la tabla `Revisiones`, el tipo de dato **Búsqueda** (Lookup) no aparece en el menú de tipos disponibles, o al seleccionarlo no muestra la tabla relacionada como opción.

**Causa raíz:** La interfaz simplificada de Dataverse for Teams dentro de Power Apps for Teams en algunos tenants no expone el tipo Lookup directamente en la vista de edición rápida de tabla. El tipo Lookup completo con relaciones formales requiere acceder al entorno de Power Apps completo (make.powerapps.com) seleccionando el entorno de Teams, o bien que las tablas relacionadas ya estén guardadas y publicadas antes de crear la columna de búsqueda.

**Solución:**
1. **Solución inmediata (para continuar el laboratorio):** Usa el tipo **Texto** para las columnas de relación (`Responsable` en `Controles`, `ID_Control` en `Revisiones`) e ingresa los valores como texto libre (ej. "María González", "CTRL-001"). Esta solución funcional permite completar la práctica y la relación formal puede configurarse después.

2. **Solución completa (para configurar el Lookup correctamente):**
   - Abre un navegador y ve a `https://make.powerapps.com`.
   - En el selector de entornos (esquina superior derecha), selecciona el entorno que corresponde a tu equipo de Teams (aparece con el nombre del equipo).
   - Ve a **Tablas** en el panel izquierdo.
   - Abre la tabla `Controles` → haz clic en **Columnas** → **+ Agregar columna**.
   - En el tipo, selecciona **Búsqueda** y en la tabla relacionada selecciona `Responsables`.
   - Guarda los cambios. Los cambios se reflejarán automáticamente en la vista de Teams.

---

## 9. Limpieza del Entorno

> **⚠️ Importante:** Las tablas de Dataverse for Teams y las fuentes de conocimiento configuradas en esta práctica son **necesarias para las Prácticas 5, 6 y 7**. **No elimines ningún artefacto creado en este laboratorio.** La limpieza descrita aquí es solo para elementos temporales o de prueba.

### Acciones de limpieza opcionales (solo si se indica)

1. **Registros de prueba en Dataverse:** Si el instructor lo indica, puedes eliminar los registros de prueba ingresados en las tablas, pero **conserva la estructura de las tablas** (columnas y configuración).

2. **Documentos en SharePoint:** Los documentos cargados en el Paso 1 deben permanecer en SharePoint para que la fuente de conocimiento siga funcionando.

3. **Instrucciones del agente:** No revertir los cambios realizados en el Paso 4 a las instrucciones del agente.

### Guardar evidencia del trabajo realizado

Antes de cerrar las sesiones, captura las siguientes pantallas como evidencia de la práctica completada:

```
Evidencia 1: Panel de Conocimiento en Copilot Studio mostrando la fuente
             de SharePoint con estado Activo.

Evidencia 2: Sección de Instrucciones del agente mostrando el bloque de
             restricciones de IA responsable agregado.

Evidencia 3: Vista de tabla de Dataverse for Teams mostrando las tres
             tablas (Responsables, Controles, Revisiones) en el listado.

Evidencia 4: Captura del panel de Prueba de Copilot Studio con la respuesta
             del agente a la consulta de prueba (Prueba 2), mostrando la
             cita de la fuente documental.
```

Guarda las capturas en la carpeta de laboratorio asignada con la nomenclatura:

```
Lab04_[TuNombre]_Evidencia[1-4].png
```

---

## 10. Resumen

En esta práctica construiste los dos pilares de conocimiento del agente de auditoría:

**Bloque A — Fuentes de conocimiento en Copilot Studio:**
- Organizaste los documentos de auditoría en SharePoint con una estructura de carpetas temática (`/Políticas_y_Procedimientos`, `/Matrices_de_Control`), siguiendo el principio de organización por dominio temático para mejorar la precisión de las respuestas.
- Conectaste el sitio de SharePoint como fuente de conocimiento activa en Copilot Studio, permitiendo al agente consultar los documentos en tiempo real mediante búsqueda semántica.
- Habilitaste las respuestas generativas y configuraste cinco restricciones de IA responsable en las instrucciones del agente: uso exclusivo de fuentes configuradas, cita obligatoria de fuente, indicador de incertidumbre, prohibición de inventar criterios normativos y recordatorio de supervisión humana.

**Bloque B — Tablas en Dataverse for Teams:**
- Creaste la tabla `Responsables` (catálogo de auditores y responsables de controles).
- Creaste la tabla `Controles` (catálogo de controles internos con ID, descripción, proceso, responsable, frecuencia y nivel de riesgo inherente).
- Creaste la tabla `Revisiones` (registro transaccional de cada revisión de control con estado, hallazgo, evidencia y fecha).

Estas tres tablas constituyen el modelo de datos estructurado que los flujos de Power Automate de la Práctica 5 utilizarán para registrar automáticamente los controles validados por el agente conversacional.

### Conceptos clave reforzados

| Concepto | Aplicación en esta práctica |
|---|---|
| Fuentes de conocimiento gobernadas | SharePoint como repositorio con ciclo de vida documental controlado |
| Búsqueda semántica en tiempo real | El agente consulta, no memoriza; las actualizaciones son inmediatas |
| Mínimo privilegio aplicado al conocimiento | Restricción a fuentes configuradas; no conocimiento general externo |
| IA responsable en auditoría | Citas de fuente, indicadores de incertidumbre, no inventar criterios |
| Modelo de datos relacional | Tres tablas con relaciones lógicas: Responsables ← Controles ← Revisiones |

### Recursos adicionales

- [Agregar conocimiento a un agente en Copilot Studio (Microsoft Learn)](https://learn.microsoft.com/es-es/microsoft-copilot-studio/knowledge-add-existing-copilot)
- [Tipos de fuentes de conocimiento compatibles con Copilot Studio](https://learn.microsoft.com/es-es/microsoft-copilot-studio/knowledge-sources-overview)
- [Usar SharePoint como fuente de conocimiento en Copilot Studio](https://learn.microsoft.com/es-es/microsoft-copilot-studio/knowledge-add-sharepoint)
- [Introducción a Dataverse for Teams (Microsoft Learn)](https://learn.microsoft.com/es-es/power-apps/teams/overview-data-platform)
- [Prácticas de IA responsable en Microsoft Copilot Studio](https://learn.microsoft.com/es-es/microsoft-copilot-studio/responsible-ai-overview)

### Preparación para la Práctica 5

En la **Práctica 5** conectarás las tablas de Dataverse for Teams con flujos de Power Automate para que el agente pueda registrar automáticamente los resultados de cada revisión de control directamente en las tablas `Revisiones` y `Controles`. Asegúrate de que las tres tablas creadas hoy tengan al menos los registros de prueba ingresados, ya que serán el punto de partida de los flujos.

---
