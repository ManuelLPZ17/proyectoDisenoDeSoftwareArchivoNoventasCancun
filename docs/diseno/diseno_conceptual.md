# Paso 2: Diseño Conceptual Preliminar
## 4.1 Identificación de clases

Para identificar las clases del sistema se revisaron los sustantivos utilizados en los requerimientos funcionales, las reglas de negocio y el glosario. Después se evaluó si cada candidato necesita conservar información propia, si es un atributo de otra entidad, si representa una interfaz, si es un sinónimo o si corresponde a un sistema externo.

### Sustantivos identificados

- **En los RF:** <u>usuario</u>, <u>mapa</u>, <u>marcador</u>, <u>locación</u>, <u>archivo</u>, <u>documento</u>, <u>administrador</u>, <u>propuesta</u>, <u>imagen</u>, <u>texto</u>, <u>coordenadas</u>, <u>línea del tiempo</u>, <u>ZIP</u> e <u>hipervínculo</u>.
- **En las RN:** <u>locación</u>, <u>nombre</u>, <u>descripción</u>, <u>coordenadas</u>, <u>documento</u>, <u>imagen</u>, <u>texto</u>, <u>PDF</u>, <u>propuesta de aporte</u>, <u>estado</u>, <u>línea del tiempo</u> y <u>archivo ZIP</u>.
- **En el glosario:** <u>Locación</u>, <u>Archivo</u>, <u>Documento</u>, <u>Documento PDF</u>, <u>Imagen</u>, <u>Texto</u>, <u>Propuesta de Aporte</u> y <u>Línea del Tiempo</u>.

### Evaluación de candidatos

| Sustantivo candidato | ¿Guarda información propia y puede haber varios? | ¿Es solo un dato de otra cosa? | ¿Es el sistema mismo o una pantalla? | ¿Es sinónimo de otra clase? | ¿Es sistema externo? | Decisión | Justificación |
| :--- | :---: | :---: | :---: | :---: | :---: | :--- | :--- |
| **Locacion** | **Sí** | No | No | No | No | **Clase** | Representa un lugar histórico con identificador, nombre único, descripción y coordenadas. Cada locación tiene un `Archivo` asociado. (RF-01, RF-02, RF-09, RN-01, Glosario). |
| **Archivo** | **Sí** | No | No | No | No | **Clase** | Es la colección documental de una locación. Agrupa `Documento` y permite consultar el acervo, generar su línea del tiempo y preparar la descarga conjunta cuando cumple las reglas aplicables. (RF-02, RF-07, RF-08, RN-04, RN-05, Glosario). |
| **Documento** | **Sí** | No | No | No | No | **Clase** | Representa una publicación histórica individual dentro de un `Archivo`. Puede estar formada por imágenes con texto descriptivo; el caso de los expedientes PDF se representa mediante su especialización `DocumentoPDF`. (RF-02, RF-03, RF-10, RN-02, Glosario). |
| **DocumentoPDF** | **Sí** | No | No | No | No | **Clase (subclase de `Documento`)** | Representa un documento histórico en formato `.pdf`, con información propia del expediente, que se consulta y descarga íntegro sin dividirlo en imágenes y textos independientes. (RF-03, RF-10, RN-02, Glosario). |
| **Imagen** | **Sí** | No | No | No | No | **Clase** | Conserva información del recurso visual, como su ubicación digital, formato y fecha histórica. Una publicación basada en imágenes debe incluir al menos una imagen acompañada de texto descriptivo. (RF-02, RF-03, RN-02, Glosario). |
| **Texto** | **Sí** | No | No | No | No | **Clase** | Contiene el escrito descriptivo que contextualiza las imágenes de un `Documento`; puede almacenar contenido propio, pero no constituye una publicación independiente dentro del alcance actual. (RF-02, RF-11, RN-02, Glosario). |
| **PropuestaAporte** | **Sí** | No | No | No | No | **Clase** | Conserva la información de una contribución ciudadana y su estado. Sigue el ciclo `Pendiente` → `Revisada` → `Aprobada` o `Rechazada`, sujeto a las condiciones de moderación. (RF-04, RF-06, RN-03, Glosario). |
| **Administrador** | **Sí** | No | No | No | No | **Clase** | Representa al responsable de la gestión del acervo; requiere información propia para autenticarse, registrar locaciones y documentos, y dictaminar propuestas. (RF-05, RF-06, RF-09, RF-10). |
| *Usuario visitante* | No | No | No | No | No | **Se descarta como clase** | Consulta información y envía propuestas sin autenticación ni cuenta persistente. Se mantiene como actor del sistema, pero no se necesita una entidad de dominio que lo represente. (RF-01, RF-02, RF-04). |
| *Solicitud de aporte / propuesta ciudadana* | No | No | No | **Sí** | No | **Se unifica con `PropuestaAporte`** | Son denominaciones de la misma solicitud enviada por un visitante; modelarlas por separado duplicaría el concepto. (RF-04, RF-06, RN-03, Glosario). |
| *Google Maps* | No | No | No | No | **Sí** | **Se descarta como clase** | Es el proveedor cartográfico externo; el sistema consume su servicio, pero no modela internamente sus componentes. (RF-01, Sección 2: Contexto y actores). |
| *Línea del tiempo* | No | No | **Sí** | No | No | **Se descarta como clase** | Es una representación cronológica generada a partir de los documentos de un `Archivo`, no una entidad histórica independiente. (RF-07, RN-04, Glosario). |
| *Paquete ZIP* | No | No | No | No | No | **Se descarta como clase** | Es el resultado de la operación de descarga masiva de un `Archivo`, no un objeto del dominio que requiera identidad y ciclo de vida propios. (RF-08, RN-05). |
| *Marcador del mapa* | No | No | **Sí** | No | No | **Se descarta como clase** | Es una representación gráfica de una `Locacion` en el mapa; sus coordenadas y datos proceden de esa clase. (RF-01, RN-01). |
| *Mapa / panel de administración / formulario* | No | No | **Sí** | No | No | **Se descartan como clases** | Son elementos de interfaz para visualizar locaciones, gestionar el contenido o recibir propuestas; no constituyen entidades del dominio. (RF-01, RF-04, RF-05). |
| *Fecha histórica / año* | No | **Sí** | No | No | No | **Atributo** | Describe la procedencia temporal de `Imagen` o `DocumentoPDF`; según SUP-01, puede tener precisión parcial. No requiere identidad como clase independiente. (RN-02, RN-04, Glosario). |
| *Coordenadas / latitud / longitud* | No | **Sí** | No | No | No | **Atributos** | Son datos geográficos de `Locacion`, necesarios para ubicarla en el mapa y validar su registro. (RF-01, RF-09, RN-01, Glosario). |
| *Nombre / título / descripción* | No | **Sí** | No | No | No | **Atributos** | Identifican o describen entidades existentes: por ejemplo, nombre y descripción de `Locacion`, o título de `Documento`. (RF-02, RF-09, RF-10, RN-01). |
| *Estado de propuesta* | No | **Sí** | No | No | No | **Atributo de tipo enumerado** | Indica la etapa de una `PropuestaAporte`. Sus valores se representan mediante `EstadoPropuesta`, sin crear otra clase de dominio independiente. (RF-04, RF-06, RN-03). |
| *Hipervínculo* | No | **Sí** | No | No | No | **Referencia entre recursos** | Permite navegar desde un documento hacia otro documento o una locación. En el diseño actual se representa como una referencia gestionada por `Documento`, no como clase independiente. (RF-11, SUP-06). |

### Resultado

Se identificaron **8 clases principales**: `Locacion`, `Archivo`, `Documento`, `DocumentoPDF`, `Imagen`, `Texto`, `PropuestaAporte` y `Administrador`. La clase `DocumentoPDF` es una especialización de `Documento`. Por separado se utiliza `EstadoPropuesta` como tipo enumerado para describir los estados permitidos de las propuestas.

Esta clasificación distingue las entidades del dominio de sus atributos, las representaciones de interfaz, los resultados de operaciones y las dependencias externas; también mantiene la terminología utilizada en los requerimientos, las reglas de negocio y el glosario.


---

## 4.2 Tarjetas CRC de las Clases Principales

Se seleccionaron las 3 clases con mayor comportamiento y aplicación de reglas de negocio del sistema:
1. `PropuestaAporte` (gestiona el ciclo de vida y cambio de estado de las contribuciones).
2. `Archivo` (gestiona la colección documental de una locación, su línea del tiempo y la compresión `.zip`).
3. `Documento` (articula imágenes fechadas y textos validando las reglas de integridad y referencias cruzadas).

```
================================================================================
CLASE: PropuestaAporte
================================================================================
Responsabilidades (qué sabe y qué hace)              | Colaboradores
----------------------------------------------------+---------------------------
1. Conoce sus datos de aporte, archivo temporal,    | Locacion
   folio, fecha de recepción y estado actual        | Administrador
   (RF-04, RN-03).                                  | Documento
                                                    |
2. Se crea en estado Pendiente al enviarse por      |
   un usuario visitante (RF-04, RN-03).             |
                                                    |
3. Cambia a estado Revisada al ser abierta en       |
   el panel administrativo (RN-03).                 |
                                                    |
4. Se dictamina como Aprobada e instruye la         |
   creación de un Documento público dentro del      |
   Archivo de la locación (RF-06, RN-03).           |
                                                    |
5. Se dictamina como Rechazada registrando el       |
   motivo obligatorio de descarte (RF-06, RN-03).   |
================================================================================
```

```
================================================================================
CLASE: Archivo
================================================================================
Responsabilidades (qué sabe y qué hace)              | Colaboradores
----------------------------------------------------+---------------------------
1. Conoce la colección de documentos históricos     | Locacion
   de su locación, el conteo total y el peso        | Documento
   acumulado en bytes (RF-02, RN-05).               |
                                                    |
2. Incorpora nuevos documentos aprobados o          |
   publicados por el administrador (RF-06, RF-10).  |
                                                    |
3. Genera la línea del tiempo cronológica si        |
   contiene al menos 2 registros con fechas         |
   históricas distintas (RF-07, RN-04).             |
                                                    |
4. Valida que el peso acumulado no supere los       |
   100 MB antes de empaquetar en lote (RF-08,       |
   RN-05).                                          |
                                                    |
5. Comprime y entrega el paquete .zip con todos     |
   los documentos de la locación (RF-08, RNF-02).   |
================================================================================
```

```
================================================================================
CLASE: Documento
================================================================================
Responsabilidades (qué sabe y qué hace)              | Colaboradores
----------------------------------------------------+---------------------------
1. Conoce su título, crédito de cortesía, texto     | Archivo
   e imágenes fechadas asociadas (RF-02, RN-02,     | Imagen
   Glosario).                                       | Texto
                                                    |
2. Valida que cuente con al menos una Imagen (con   |
   año histórico) y su Texto descriptivo, o bien    |
   un Texto con valor artístico propio (RN-02).     |
                                                    |
3. Agrega y administra las imágenes que componen    |
   la publicación histórica (RF-02, RF-10).         |
                                                    |
4. Gestiona hipervínculos internos hacia otros      |
   documentos o locaciones relacionadas (RF-11).    |
================================================================================
```

---

## 4.3 Atributos y Métodos

| Clase | Atributos (Nombre : Tipo) | Métodos (Firma de operación) | Justificación |
| :--- | :--- | :--- | :--- |
| **Locacion** | - `idLocacion : Integer`<br>- `nombre : String`<br>- `descripcion : String`<br>- `latitud : Float`<br>- `longitud : Float` | + `actualizarDatos(nombre: String, desc: String, lat: Float, lng: Float) : Boolean`<br>+ `validarCoordenadas() : Boolean`<br>+ `obtenerArchivo() : Archivo` | RF-01, RF-02, RF-09, RF-12, RN-01 |
| **Archivo** | - `idArchivo : Integer`<br>- `totalDocumentos : Integer`<br>- `pesoAcumuladoBytes : Long`<br>- `fechaActualizacion : DateTime` | + `agregarDocumento(documento: Documento) : Void`<br>+ `generarLineaTiempo() : List<Documento>`<br>+ `validarLimiteZIP() : Boolean`<br>+ `comprimirArchivoZIP() : String` | RF-02, RF-07, RF-08, RN-04, RN-05, RNF-02 |
| **Documento** | - `idDocumento : Integer`<br>- `titulo : String`<br>- `cortesiaDe : String`<br>- `fechaPublicacion : DateTime` | + `vincularImagen(imagen: Imagen) : Void`<br>+ `validarIntegridadDocumento() : Boolean`<br>+ `agregarHipervinculo(idDestino: Integer) : Void` | RF-02, RF-10, RF-11, RN-02, Glosario |
| **DocumentoPDF** | - `rutaArchivoPdf : String`<br>- `anioHistorico : Integer`<br>- `numeroPaginas : Integer`<br>- `pesoBytes : Long` | + `obtenerEnlaceDescarga() : String`<br>+ `validarFormatoPDF() : Boolean` | RF-03, RF-10, RN-02, Glosario |
| **Imagen** | - `idImagen : Integer`<br>- `anioHistorico : Integer`<br>- `rutaImagen : String`<br>- `formatoImagen : String`<br>- `pesoBytes : Long` | + `obtenerEnlaceDescarga() : String`<br>+ `validarFormatoImagen() : Boolean` | RF-02, RF-03, RN-02, Glosario |
| **Texto** | - `idTexto : Integer`<br>- `contenido : String`<br>- `tieneValorArtistico : Boolean`<br>- `extensionPalabras : Integer` | + `validarAutonomia() : Boolean`<br>+ `obtenerExtracto() : String` | RF-02, RN-02, Glosario |
| **PropuestaAporte** | - `idPropuesta : Integer`<br>- `folioSeguimiento : String`<br>- `estado : EstadoPropuesta`<br>- `anioSugerido : Integer`<br>- `rutaArchivoTemporal : String`<br>- `motivoRechazo : String` | + `marcarEnRevision() : Void`<br>+ `aprobar(curador: Administrador) : Documento`<br>+ `rechazar(motivo: String) : Boolean` | RF-04, RF-06, RN-03 |
| **Administrador** | - `idAdmin : Integer`<br>- `nombreCompleto : String`<br>- `correoElectronico : String`<br>- `passwordHash : String`<br>- `ultimoAcceso : DateTime` | + `autenticar(credenciales: String) : Boolean`<br>+ `cerrarSesion() : Void`<br>+ `dictaminarPropuesta(propuesta: PropuestaAporte, aprobado: Boolean, motivo: String) : Void` | RF-05, RF-06, RF-09, RF-10 |

*Tipo enumerado auxiliar:*
- `EstadoPropuesta = { PENDIENTE, REVISADA, APROBADA, RECHAZADA }`

---

## 4.4 Relaciones Entre Clases

| Clase A | Tipo de Relación | Clase B | Multiplicidad | Justificación |
| :--- | :--- | :--- | :--- | :--- |
| **Locacion** | Composición | **Archivo** | `1` locación — `1` archivo | Cada locación posee un único archivo histórico que concentra todo su acervo. El archivo no existe sin su locación correspondiente (RF-02, Glosario). |
| **Archivo** | Agregación | **Documento** | `1` archivo — `0..*` documentos | El archivo de una locación agrupa cero o más documentos históricos a lo largo del tiempo (RF-02, RF-07, RN-04, RN-05). |
| **Documento** | Composición | **Texto** | `1` documento — `1` texto | Todo documento incluye su texto (caption descriptivo o texto artístico). El texto descriptivo depende existencialmente del documento que contextualiza (RF-02, RN-02, Glosario). |
| **Documento** | Agregación | **Imagen** | `1` documento — `0..*` imágenes | Un documento contiene cero imágenes (cuando su texto tiene valor artístico propio) o una/varias imágenes que tienen sentido histórico por sí solas (RF-02, RN-02, Glosario). |
| **DocumentoPDF** | Herencia | **Documento** | Subclase de `Documento` | `DocumentoPDF` es un tipo especializado de `Documento` para expedientes paginados indivisibles (`.pdf`) que hereda metadatos y comportamiento de `Documento` (RF-03, RN-02, Glosario). |
| **Locacion** | Asociación | **PropuestaAporte** | `1` locación — `0..*` propuestas | Los usuarios envían propuestas dirigidas a una locación específica (RF-04, RN-03). |
| **Administrador** | Asociación | **PropuestaAporte** | `1` administrador — `0..*` propuestas | El administrador revisa y dictamina múltiples propuestas ciudadanas (RF-06, RN-03). |
| **Administrador** | Asociación | **Documento** | `1` administrador — `0..*` documentos | El administrador registra y publica directamente documentos en el archivo de una locación (RF-10). |
