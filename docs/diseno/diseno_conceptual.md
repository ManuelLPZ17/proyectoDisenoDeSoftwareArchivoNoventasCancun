# Paso 2: Diseño Conceptual Preliminar

Esta sección transforma los requerimientos del SRS (RF, RN y Glosario) en el modelo conceptual de clases del sistema.

---

## 4.1 Identificación de Clases

Se realizó la extracción de sustantivos a partir de los RFs, las RNs y el glosario. Cada sustantivo fue evaluado con la matriz formal de preguntas y criterios de decisión de la guía:

| Sustantivo Candidato | ¿Guarda info propia y puede haber varios? | ¿Es solo un dato de otra cosa? | ¿Es el sistema mismo o pantalla? | ¿Es sinónimo de otra clase? | ¿Es sistema externo? | Decisión | Justificación |
| :--- | :---: | :---: | :---: | :---: | :---: | :--- | :--- |
| **Locacion** | **Sí** | No | No | No | No | **Es Clase** | Almacena coordenadas, nombre, historia y agrupa recursos (RF-01, RF-02, RN-01). |
| **ArchivoHistorico** | **Sí** | No | No | No | No | **Es Clase** | Entidad central que almacena metadatos, ruta física, tipo y año de procedencia (RF-02, RF-03, RN-02). |
| **PropuestaAporte** | **Sí** | No | No | No | No | **Es Clase** | Cambia de estado (`Pendiente`, `Revisada`, `Aprobada`, `Rechazada`), guarda dictamen y archivo aportado (RF-04, RF-06, RN-03). |
| **Administrador** | **Sí** | No | No | No | No | **Es Clase** | Actor con identidad persistente, credenciales y métodos de curaduría (RF-05, RF-06, RF-09). |
| **LineaTiempo** | **Sí** | No | No | No | No | **Es Clase** | Agregación cronológica estructurada con lógica de ordenamiento y filtrado temporal (RF-07, RN-04). |
| *PaqueteDescarga* | **Sí** | No | No | No | No | **Es Clase** | Gestiona la compresión de archivos binarios, cálculo de peso total y entrega de ZIP (RF-08, RN-05). |
| *UsuarioVisitante* | No | No | No | No | No | **Se descarta** | El visitante no tiene cuenta ni guarda estado persistente en base de datos; actúa de forma anónima enviando formularios (Glosario, RF-04). |
| *Google Maps* | No | No | No | No | **Sí** | **Se descarta** | Sistema externo tratado estrictamente como caja negra vía API (RST-02, DEP-01). |
| *Fecha / Año* | No | **Sí** | No | No | No | **Es Atributo** | Dato cronológico perteneciente a `ArchivoHistorico` y `PropuestaAporte`. |
| *Coordenadas* | No | **Sí** | No | No | No | **Es Atributo** | Par latitud/longitud perteneciente a `Locacion`. |
| *Mapa / Menú* | No | No | **Sí** | No | No | **Se descarta** | Componentes visuales de la interfaz de usuario en el cliente. |
| *Documento / Imagen* | — | — | — | **Sí** | — | **Se une / Atributo** | Son tipos/modalidades de la clase base `ArchivoHistorico` (manejados por atributo `tipoArchivo` o herencia según necesidad). |

**Resultado:** 6 clases de dominio identificadas (supera el mínimo exigido de 5 clases).

---

## 4.2 Tarjetas CRC de las Clases Principales

Se seleccionaron las 3 clases con mayor comportamiento y cambio de estado del sistema:
1. `PropuestaAporte` (gestiona el ciclo de vida y máquina de estados).
2. `Locacion` (núcleo geográfico que coordina archivos, cronologías y límites de descarga).
3. `ArchivoHistorico` (entidad testimonial que valida formatos, navegación y descarga).

```
================================================================================
CLASE: PropuestaAporte
================================================================================
Responsabilidades (qué sabe y qué hace)              | Colaboradores
----------------------------------------------------+---------------------------
1. Conoce sus datos de aporte, archivo temporal,    | Locacion
   folio, fecha de recepción y estado actual        | Administrador
   (RF-04, RN-03).                                  | ArchivoHistorico
                                                    |
2. Se crea en estado Pendiente al enviarse por      |
   un usuario visitante (RF-04, RN-03).             |
                                                    |
3. Cambia a estado Revisada al ser abierta en       |
   panel administrativo (RN-03).                    |
                                                    |
4. Se dictamina como Aprobada e instruye la         |
   creación de un ArchivoHistorico público          |
   asociado a la locación (RF-06, RN-03).           |
                                                    |
5. Se dictamina como Rechazada registrando el       |
   motivo obligatorio de descarte (RF-06, RN-03).   |
================================================================================
```

```
================================================================================
CLASE: Locacion
================================================================================
Responsabilidades (qué sabe y qué hace)              | Colaboradores
----------------------------------------------------+---------------------------
1. Conoce su nombre, coordenadas geográficas y      | ArchivoHistorico
   reseña histórica descriptiva (RF-01, RN-01).     | LineaTiempo
                                                    | PaqueteDescarga
2. Valida y actualiza sus datos geográficos         |
   respetando rangos de latitud/longitud (RF-09,    |
   RN-01).                                          |
                                                    |
3. Agrupa y administra el catálogo de archivos       |
   históricos vinculados (RF-02, RN-02).            |
                                                    |
4. Genera su LineaTiempo interactiva si cuenta con  |
   al menos 2 archivos de fechas distintas (RF-07,  |
   RN-04).                                          |
                                                    |
5. Prepara el conjunto de archivos para compresión  |
   en PaqueteDescarga validando el límite de        |
   150 MB (RF-08, RN-05).                           |
================================================================================
```

```
================================================================================
CLASE: ArchivoHistorico
================================================================================
Responsabilidades (qué sabe y qué hace)              | Colaboradores
----------------------------------------------------+---------------------------
1. Conoce su título, ruta de almacenamiento físico, | Locacion
   tipo (imagen, documento, texto), año de          | PaqueteDescarga
   procedencia y estado de publicación (RF-02,      |
   RN-02).                                          |
                                                    |
2. Valida la integridad del archivo y que el año    |
   histórico esté asignado (RN-02, RNF-05).         |
                                                    |
3. Provee su enlace y flujo binario para descarga   |
   individual directa (RF-03).                      |
                                                    |
4. Gestiona hipervínculos de referencia cruzada     |
   hacia otras locaciones o archivos (RF-11).       |
================================================================================
```

---

## 4.3 Atributos y Métodos

Siguiendo las restricciones de la guía, cada clase posee al menos 3 atributos tipados. No se incluyen constructores ni getters/setters. Cada método se justifica con su RF o RN correspondiente:

| Clase | Atributos (Nombre : Tipo) | Métodos (Firma de operación) | Justificación |
| :--- | :--- | :--- | :--- |
| **Locacion** | - `idLocacion : Integer`<br>- `nombre : String`<br>- `descripcion : String`<br>- `latitud : Float`<br>- `longitud : Float` | + `actualizarDatos(nombre: String, desc: String, lat: Float, lng: Float) : Boolean`<br>+ `vincularArchivo(archivo: ArchivoHistorico) : Void`<br>+ `generarLineaTiempo() : LineaTiempo`<br>+ `solicitarDescargaZIP() : PaqueteDescarga` | RF-01, RF-02, RF-07, RF-08, RF-09, RN-01, RN-04, RN-05 |
| **ArchivoHistorico** | - `idArchivo : Integer`<br>- `titulo : String`<br>- `tipoArchivo : TipoRecurso`<br>- `anioHistorico : Integer`<br>- `rutaAlmacenamiento : String`<br>- `pesoBytes : Long` | + `obtenerEnlaceDescarga() : String`<br>+ `agregarHipervinculo(idDestino: Integer) : Void`<br>+ `validarFormato() : Boolean` | RF-02, RF-03, RF-10, RF-11, RN-02, RNF-05 |
| **PropuestaAporte** | - `idPropuesta : Integer`<br>- `folioSeguimiento : String`<br>- `estado : EstadoPropuesta`<br>- `fechaEnvio : DateTime`<br>- `rutaArchivoTemporal : String`<br>- `motivoRechazo : String` | + `marcarEnRevision() : Void`<br>+ `aprobar(curador: Administrador) : ArchivoHistorico`<br>+ `rechazar(motivo: String) : Boolean` | RF-04, RF-06, RN-03 |
| **Administrador** | - `idAdmin : Integer`<br>- `nombreCompleto : String`<br>- `correoElectronico : String`<br>- `passwordHash : String`<br>- `ultimoAcceso : DateTime` | + `autenticar(credenciales: String) : Boolean`<br>+ `cerrarSesion() : Void`<br>+ `dictaminarPropuesta(propuesta: PropuestaAporte, aprobado: Boolean, motivo: String) : Void` | RF-05, RF-06, RF-09, RF-10, RNF-03 |
| **LineaTiempo** | - `idLineaTiempo : Integer`<br>- `fechaGeneracion : DateTime`<br>- `totalHitos : Integer`<br>- `rangoAnios : String` | + `ordenarCronologicamente() : List<ArchivoHistorico>`<br>+ `filtrarPorDecada(decada: Integer) : List<ArchivoHistorico>` | RF-07, RN-04 |
| **PaqueteDescarga** | - `idPaquete : Integer`<br>- `tamanioTotalBytes : Long`<br>- `fechaCompresion : DateTime`<br>- `rutaArchivoZip : String` | + `comprimirArchivos(archivos: List<ArchivoHistorico>) : String`<br>+ `validarLimiteTamanio(limiteMaxBytes: Long) : Boolean` | RF-08, RN-05, RNF-02 |

*Tipos enumerados auxiliares:*
- `EstadoPropuesta = { PENDIENTE, REVISADA, APROBADA, RECHAZADA }`
- `TipoRecurso = { IMAGEN, DOCUMENTO, TEXTO }`

---

## 4.4 Relaciones Entre Clases

| Clase A | Tipo de Relación | Clase B | Multiplicidad | Justificación |
| :--- | :--- | :--- | :--- | :--- |
| **Locacion** | Agregación | **ArchivoHistorico** | `1` locación — `0..*` archivos | Una locación puede albergar múltiples archivos históricos vinculados. Si una locación se elimina o archiva, los archivos históricos pueden persistir en el repositorio general (RF-02, RN-02). |
| **Locacion** | Composición | **LineaTiempo** | `1` locación — `0..1` línea de tiempo | La línea de tiempo existe exclusivamente como una vista cronológica dependiente del acervo de esa locación específica. Si la locación deja de existir, su línea de tiempo se destruye con ella (RF-07, RN-04). |
| **Locacion** | Asociación | **PropuestaAporte** | `1` locación — `0..*` propuestas | Los usuarios asocian sus propuestas a una locación específica. La locación existe independientemente de si hay propuestas o no (RF-04, RN-03). |
| **Administrador** | Asociación | **PropuestaAporte** | `1` administrador — `0..*` propuestas | El administrador revisa y dictamina múltiples propuestas a lo largo de su gestión (RF-06, RN-03). |
| **Administrador** | Asociación | **ArchivoHistorico** | `1` administrador — `0..*` archivos | El administrador da de alta y publica directamente archivos en el sistema (RF-10). |
| **Locacion** | Uso / Dependencia | **PaqueteDescarga** | `1` locación — `0..1` paquete | La locación solicita la creación de un paquete `.zip` bajo demanda al usuario para descargar su lote de archivos (RF-08, RN-05). |
| **PaqueteDescarga** | Agregación | **ArchivoHistorico** | `1` paquete — `1..*` archivos | El paquete comprimido ZIP empaqueta temporalmente una colección de archivos históricos existentes (RF-08, RN-05). |
