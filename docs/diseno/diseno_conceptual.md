# Paso 2: Diseño Conceptual Preliminar

---

## 4.1 Identificación de Clases

| Sustantivo Candidato | ¿Guarda info propia y puede haber varios? | ¿Es solo un dato de otra cosa? | ¿Es el sistema mismo o pantalla? | ¿Es sinónimo de otra clase? | ¿Es sistema externo? | Decisión | Justificación |
| :--- | :---: | :---: | :---: | :---: | :---: | :--- | :--- |
| **Locacion** | **Sí** | No | No | No | No | **Es Clase** | Punto geográfico de Cancún que almacena coordenadas, nombre, reseña y posee su propio `Archivo` (RF-01, RF-02, RN-01). |
| **Archivo** | **Sí** | No | No | No | No | **Es Clase** | Contenedor documental de una `Locacion` que agrupa sus `Documento`s, genera la línea del tiempo y comprime el paquete `.zip` (RF-02, RF-07, RF-08, RN-04, RN-05). |
| **Documento** | **Sí** | No | No | No | No | **Es Clase** | Unidad de publicación histórica dentro de un `Archivo` que articula `Imagen`(es) y `Texto` descriptivo o artístico (RF-02, RF-10, RF-11, RN-02, Glosario). |
| **DocumentoPDF** | **Sí** | No | No | No | No | **Es Clase (Subclase)** | Especialización de `Documento` para expedientes paginados indivisibles (`.pdf`) como planes oficiales o zines (RF-03, RF-10, RN-02, Glosario). |
| **Imagen** | **Sí** | No | No | No | No | **Es Clase** | Recurso visual estático (`.jpg`, `.png`, `.webp`) con sentido testimonial propio que forma parte de un `Documento` (RF-02, RF-03, RN-02, Glosario). |
| **Texto** | **Sí** | No | No | No | No | **Es Clase** | Escrito descriptivo (*caption*) dependiente de un `Documento`, o relato con valor artístico propio (RF-02, RN-02, Glosario). |
| **PropuestaAporte** | **Sí** | No | No | No | No | **Es Clase** | Solicitud ciudadana que cambia de estado (`Pendiente`, `Revisada`, `Aprobada`, `Rechazada`) y origina un `Documento` al aprobarse (RF-04, RF-06, RN-03). |
| **Administrador** | **Sí** | No | No | No | No | **Es Clase** | Actor con credenciales persistentes encargado de curar propuestas y publicar documentos (RF-05, RF-06, RF-09, RF-10). |
| *UsuarioVisitante* | No | No | No | No | No | **Se descarta** | El visitante consulta y envía propuestas de forma anónima sin cuenta ni estado persistente (RF-04). |
| *Google Maps* | No | No | No | No | **Sí** | **Se descarta** | Sistema externo tratado como caja negra vía API (DEP-01). |
| *Línea del Tiempo / ZIP* | No | No | **Sí** | No | No | **Se descarta (Operación)** | Son representaciones y paquetes generados directamente por la clase `Archivo` a partir de sus documentos (RF-07, RF-08). |
| *Fecha / Año* | No | **Sí** | No | No | No | **Es Atributo** | Dato cronológico histórico perteneciente a `Imagen` (y `DocumentoPDF`), no a `Texto`. |
| *Coordenadas* | No | **Sí** | No | No | No | **Es Atributo** | Par latitud/longitud perteneciente a `Locacion`. |
| *Mapa / Menú* | No | No | **Sí** | No | No | **Se descarta** | Componentes visuales de la interfaz de usuario. |

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
