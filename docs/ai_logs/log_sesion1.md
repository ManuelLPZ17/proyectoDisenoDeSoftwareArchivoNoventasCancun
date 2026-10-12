# Bitácora de Asistencia de IA - Sesión 1

- **Fecha:** 11 de Octubre de 2026
- **Objetivo de la sesión:** Setup del proyecto, control de versiones (Git), definición metodológica (Unslop + Grill-me) y borrador completo de Entrega 1 (SRS Secciones 1-7 y Diseño Conceptual 4.1-4.5).

---

## Registro de Actividades y Decisiones

| Hito / Fase | Intención del Estudiante | Aportación del Agente | Decisión / Corrección Humana |
| :--- | :--- | :--- | :--- |
| **1. Lectura del PDF y Word** | Solicita revisar si el agente puede leer el documento base `.docx`. | Inspeccionó el XML del `.docx`, comparó contra las restricciones del PDF de la materia (2 actores, 1 sistema externo, elemento con cambio de estado, 10-15 RF). | Validación de la idea central: ArchivoNoventasCancún como circuito histórico cartográfico. |
| **2. Metodología y Herramientas** | Solicita incorporar Git/GitHub, directriz anti-slop y grill-me. | Inicializó repositorio Git local (`main`), creó `.gitignore` para Office/SO, configuró skills locales `unslop` y `grill-me`. | Aprobó el plan de trabajo modular en Markdown antes de compilar el documento final. |
| **3. Grill-Me: Alcance y Casos Borde** | Responder a preguntas de diseño del sistema formuladas por el agente. | Interrogó sobre tipo de acceso de usuarios, políticas de descarga ZIP y contingencia ante fallos de Google Maps API. | Decidió: Usuarios anónimos (sin registro), descarga ZIP hasta 150 MB, y modo degradado obligatorio a vista tabular si Maps cae. |
| **4. Redacción del SRS (Sec 1 a 7)** | Formalización técnica de requerimientos. | Redactó Secciones 1 a 7 con métricas cuantificables (RNF), priorización MoSCoW (50% Must <= 60%) y reglas de negocio RN-01 a RN-05. | El estudiante ajustó redacción en supuestos (SUP-03 de 1 a 50 archivos) y dejó Sección 3 (Restricciones) como "No aplica" con propuestas en comentarios HTML. |
| **5. Diseño Conceptual (Paso 2)** | Modelar clases a partir del SRS. | Generó matriz de sustantivos (6 clases), tarjetas CRC de las 3 clases principales, tabla de métodos/atributos tipados y archivo PlantUML. | Aprobó jerarquía conceptual entre Archivo, Documento, Imagen y Texto. |

---

## Estado al Cierre de la Sesión
- **Completado:** Repositorio estructurado, Secciones 1-7 del SRS en Markdown, Diseño conceptual preliminar en Markdown, Diagrama PlantUML (`.puml`), marco `AI_DISCLOSURE.md`.
- **Pendiente para la Sesión 2:**
  1. Revisión y pulido humano de las secciones 5, 6 y 7 del SRS.
  2. Aplicar la herencia de `ArchivoHistorico` (`ImagenHistorica`, `DocumentoHistorico`, `TextoHistorico`) en el diagrama UML si se desea profundizar.
  3. Vincular repositorio remoto en GitHub (`git remote add origin`).
  4. Generar el documento final para entrega (Word/PDF) con portada formal.
