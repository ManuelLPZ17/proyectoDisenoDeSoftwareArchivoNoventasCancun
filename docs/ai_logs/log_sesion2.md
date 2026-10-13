# Bitácora de Asistencia de IA - Sesión 2

- **Fecha:** 12 de Octubre de 2026
- **Objetivo de la sesión:** Pulir el SRS (secciones 1-7), analizar el contenido real de `@archivonoventascancun` y replantear el modelo conceptual del Paso 2.

---

## Registro de Actividades y Decisiones

| Hito / Fase | Intención del Estudiante | Aportación del Agente | Decisión / Corrección Humana |
| :--- | :--- | :--- | :--- |
| **1. Pulido del SRS** | Revisar y corregir las secciones 5, 6 y 7. | Detectó inconsistencias de formatos admitidos (`.webp` omitido en RF-03/04/10), límite ZIP (150 MB vs 100 MB) y tabla Markdown rota en RNF-02. | El estudiante fijó el límite ZIP en 100 MB y ejecutó él mismo parte de las correcciones (introducciones meta, RNF-02). |
| **2. Análisis del acervo real** | Entender qué publica `@archivonoventascancun` para dividir mejor los archivos. | Instagram bloquea lectura sin sesión; se accedió al Linktree, al Google Drive público (zines `909090`, Manifiesto 00) y al reportaje de Pie de Página. | El estudiante descartó la herencia propuesta (`Imagen`/`Documento`/`Texto` bajo `ArchivoHistorico`) y propuso un enfoque nuevo. |
| **3. Nuevo modelo conceptual** | Definir que cada locación tiene un archivo, formado por documentos (imagen + texto tipo *caption*). | Modeló `Locacion` -> `Archivo` -> `Documento` (`Imagen` + `Texto`) y `DocumentoPDF` como subclase para expedientes indivisibles. | El estudiante decidió: fecha histórica en `Imagen` y no en `Texto`; `Archivo` absorbe línea del tiempo y ZIP (8 clases). |
| **4. Integridad de términos** | Unificar `Archivo` y `Documento` en todo el SRS. | Revisó las 7 secciones y listó los usos inconsistentes. | El estudiante ajustó el Glosario y `RN-02` (eliminó el caso de texto con valor artístico propio); el agente aplicó el resto. |
| **5. Flujo de equipo (README)** | Definir cómo trabajar en equipo con GitHub, Kanban y agentes. | Un subagente redactó un `README.md` con flujo de Git, Kanban y bitácora compartida. | El estudiante descartó el enfoque por ahora: `README.md` eliminado sin commitear y `AI_DISCLOSURE.md` eliminado a propósito. |

---

## Estado al Cierre de la Sesión
- **Completado:** SRS con terminología unificada, `RN-02` y Glosario actualizados, modelo `Locacion` -> `Archivo` -> `Documento` en `diseno_conceptual.md` y en el diagrama PlantUML.
- **Pendiente para la Sesión 3:**
  1. Revisión a fondo del Paso 2, empezando por los dos primeros archivos generados: `docs/diseno/diseno_conceptual.md` y `diagramas/Equipo3_Entrega1_DiagramaClases.puml`. A partir de esa revisión se decide cómo continuar.
  2. Sincronizar la clase `Texto` con los cambios de `RN-02` y el Glosario (ya no existe el texto con valor artístico propio; revisar el atributo `tieneValorArtistico` y los métodos `validarAutonomia()` y `obtenerExtracto()`). El Glosario también asocia `Texto` a una `Imagen`, mientras el diseño lo asocia a `Documento`.
  3. Decidir si se reactiva el RNF de Seguridad (hoy comentado en la Sección 7), pues la guía sugiere cubrir desempeño, seguridad y disponibilidad.
  4. Generar el documento final de entrega (Word/PDF) con portada formal.
