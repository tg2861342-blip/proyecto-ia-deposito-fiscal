# proyecto-ia-deposito-fiscal
Sistema de detección de mails logísticos con IA
# 📦 Sistema de Detección de Mails Logísticos con IA
### Proyecto Integrador — Curso de Inteligencia Artificial

---

## 📋 Descripción del Proyecto

Este proyecto implementa un sistema basado en Inteligencia Artificial para la detección automática de correos electrónicos de solicitud de traslado de contenedores desde el puerto hacia un depósito fiscal. El objetivo es eliminar el riesgo de pérdidas operativas causadas por la no lectura oportuna de estos correos.

---

## 🏢 Contexto Corporativo

| Campo | Detalle |
|---|---|
| **Organización** | Depósito Fiscal |
| **Área** | Coordinación de Contenedores |
| **Problema** | No detección oportuna de mails de solicitud de traslado |
| **Impacto** | Pérdidas por demora portuaria (storage/demurrage) |
| **Solución** | Sistema de IA para monitoreo y clasificación de bandeja de entrada |

---

## 🎯 Objetivos

1. Detectar el 100% de los mails de solicitud de traslado dentro de los 15 minutos de recibidos.
2. Clasificar los mails por urgencia (fecha de retiro, tipo de contenedor).
3. Reducir pérdidas operativas por demora portuaria no gestionada.

---

## 📅 Cronograma del Proyecto

| Semana | Fase |
|---|---|
| Semana 1 | Relevamiento: tipos de mails, patrones de lenguaje, casos críticos |
| Semana 2 | Diseño del Prompt Maestro e Instrucciones Base |
| Semana 3 | Producción multimodal (imágenes del flujo + audio explicativo) |
| Semana 4 | Auditoría ética + compilación del README |

---

## ⚙️ Fase 1 — Co-Creación con LLM

El problema corporativo, los objetivos y el cronograma fueron definidos en sesión colaborativa con un LLM (Claude de Anthropic). Durante el proceso se refinaron:

- El alcance del sistema (detección, no solo filtrado)
- Las palabras clave críticas del dominio logístico (DTA, MIC, booking, etc.)
- Los niveles de urgencia adaptados a la operatoria portuaria argentina

---

## 🧠 Fase 2 — Configuración del Sistema

### Instrucciones Base (System Prompt)

```
Sos un asistente especializado en logística de depósitos fiscales argentinos.
Tu función es monitorear correos electrónicos entrantes y detectar aquellos
que correspondan a solicitudes de traslado de contenedores desde el puerto
hacia el depósito.

Comportamiento esperado:
- Analizá el asunto y cuerpo de cada mail recibido
- Identificá si el mail contiene una solicitud de traslado, retiro o coordinación de contenedor
- Extraé los datos clave: nombre del cliente, número de contenedor, fecha solicitada,
  puerto de origen, tipo de carga
- Clasificá la urgencia en:
    🔴 URGENTE (retiro en menos de 24hs)
    🟡 PRÓXIMO (2-3 días)
    🟢 PROGRAMADO (+3 días)
- Si el mail es ambiguo o incompleto, indicalo y sugerí qué dato falta
- Nunca ignorés un mail que contenga: contenedor, retiro, traslado, despacho,
  DTA, MIC, puerto, booking

Tono: Técnico, directo, sin rodeos.
```

### Prompt Maestro

```
Analizá el siguiente correo electrónico recibido en la bandeja del depósito fiscal.

1. Clasificación: ¿Es un mail de solicitud de traslado de contenedor? (Sí / No / Dudoso)
2. Datos extraídos:
   - Cliente:
   - N° de contenedor:
   - Fecha de retiro solicitada:
   - Puerto de origen:
   - Observaciones especiales:
3. Nivel de urgencia: 🔴 / 🟡 / 🟢 — Justificá brevemente
4. Acción recomendada: ¿Qué debe hacer el coordinador ahora mismo?
5. ¿Falta información crítica? Sí / No — ¿Cuál?

---
MAIL A ANALIZAR:
[PEGAR CONTENIDO DEL MAIL AQUÍ]
```

---

## 🖼️ Fase 3 — Producción Multimodal

### Imágenes generadas

> Herramienta utilizada: **Microsoft Copilot (Bing Image Creator)**
> Modelo subyacente: DALL·E 3

| # | Descripción | Prompt utilizado |
|---|---|---|
| Imagen 1 | Flujo operativo del sistema | "Diagrama profesional que muestra un sistema de monitoreo de correos con inteligencia artificial para un depósito fiscal. Estilo flowchart: correo entrante → detección por IA → clasificación por urgencia → alerta al coordinador. Diseño corporativo limpio, colores azul y blanco, íconos de contenedores y puerto." |
| Imagen 2 | Interfaz de alertas | "Dashboard UI mockup for a logistics coordinator showing email alerts classified by urgency: red, yellow and green indicators. Container numbers, client names and pickup dates visible. Modern flat design, dark mode." |
| Imagen 3 | Contexto logístico | "Aerial view of a fiscal warehouse next to a port in Argentina. Shipping containers being moved by trucks. Professional corporate photography style, golden hour lighting." |

*(Reemplazar con las imágenes generadas una vez subidas al repositorio)*

---

### Audios generados

> Herramienta utilizada: **ElevenLabs**
> Voz: Español latino — tono profesional

| # | Descripción | Texto del prompt |
|---|---|---|
| Audio 1 | Presentación del sistema | "Este sistema utiliza inteligencia artificial para detectar automáticamente los correos de solicitud de traslado de contenedores, eliminando el riesgo de pérdidas operativas por no lectura. Cada mail es clasificado por urgencia y el coordinador recibe una alerta inmediata." |
| Audio 2 | Alerta tipo al coordinador | "Atención coordinador: se detectó un nuevo pedido de retiro de contenedor con urgencia alta. Cliente: Importadora del Sur. Retiro solicitado para mañana a las ocho horas. Por favor, confirmar disponibilidad de transporte." |

*(Reemplazar con los archivos de audio una vez subidos al repositorio)*

---

## 🔍 Fase 4 — Auditoría Ética

| # | Riesgo identificado | Categoría | Probabilidad | Impacto | Mitigación aplicada |
|---|---|---|---|---|---|
| 1 | El modelo no detecta un mail por redacción inusual | Falso negativo | Media | Alto | Palabras clave obligatorias en instrucciones base |
| 2 | El modelo clasifica como urgente un mail que no lo es | Falso positivo | Baja | Medio | Validación humana antes de actuar |
| 3 | Exposición de datos sensibles del cliente en el prompt | Privacidad | Media | Alto | No se almacenan mails procesados; operación en sesión activa |
| 4 | Sesgo hacia ciertos remitentes o formatos | Sesgo algorítmico | Baja | Medio | El prompt evalúa contenido, no remitente ni formato |
| 5 | Dependencia total del sistema sin supervisión humana | Riesgo operativo | Media | Muy alto | El sistema es de apoyo; la decisión final es humana |

**Conclusión ética:** El sistema fue diseñado como herramienta de asistencia que reduce el error humano por omisión, manteniendo siempre al coordinador como responsable final de la operación.

---

## 🛠️ Tecnologías Utilizadas

| Herramienta | Uso |
|---|---|
| Claude (Anthropic) | Co-creación, definición del problema, generación de prompts |
| Microsoft Copilot | Generación de imágenes (modelo DALL·E 3) |
| ElevenLabs | Generación de clips de audio en español |

---

## 👤 Autor

**Tomás**
Proyecto Integrador — Curso de Inteligencia Artificial
