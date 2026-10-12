# Sección 1: Alcance y Glosario

## 1.1 Declaración del Problema y Beneficiarios
La memoria histórica gráfica y documental del desarrollo urbano y social de Cancún se encuentra dispersa en archivos personales físicos, colecciones desarticuladas y publicaciones digitales efímeras, careciendo de anclaje espacial. Esta dispersión dificulta que habitantes, investigadores y entusiastas comprendan la evolución cronológica y geográfica de la ciudad desde sus orígenes. El sistema **ArchivoNoventasCancún** resuelve esta problemática centralizando y catalogando recursos históricos (fotografías, recortes de prensa, documentos y textos) georreferenciados sobre un mapa interactivo. El sistema beneficia a los ciudadanos locales, cronistas e investigadores culturales al ofrecer acceso público y contextualizado a dicho patrimonio, a la vez que proporciona a los administradores del archivo una plataforma centralizada para curar, organizar y preservar este acervo colectivo.

## 1.2 Delimitación del Alcance

### Dentro del Alcance
1. **Exploración cartográfica georreferenciada:** Visualización en un mapa interactivo de locaciones de interés cultural e histórico de Cancún identificadas por marcadores geográficos.
2. **Consulta y previsualización de archivos:** Despliegue de fichas técnicas y previsualizaciones multimedia (imágenes, textos transcritos y documentos PDF) vinculadas a cada locación.
3. **Línea del tiempo cronológica:** Generación de una vista cronológica interactiva para locaciones que cuenten con dos o más archivos fechados en distintos momentos históricos.
4. **Hipervínculos entre recursos:** Navegación cruzada mediante enlaces embebidos entre archivos y locaciones temáticamente vinculados.
5. **Descarga individual y masiva:** Descarga directa de archivos multimedia individuales en su formato original y descarga en lote del archivo completo de una locación comprimido en formato `.zip`.
6. **Módulo de propuestas ciudadanas:** Formulario abierto para que usuarios envíen solicitudes de nuevos archivos aportados (archivo, descripción, año propuesto y locación vinculada) sin requerir autenticación previa.
7. **Panel de curaduría y moderación administrativa:** Interfaz exclusiva para el administrador con autenticación, permitiendo crear locaciones, cargar archivos oficiales y gestionar las propuestas recibidas a través de un ciclo de vida con estados (`Pendiente`, `Revisada`, `Aprobada`, `Rechazada`).
8. **Modo degradado por contingencia:** Vista alternativa en formato de catálogo/lista tabular en caso de inoperatividad del proveedor externo de mapas.

### Fuera del Alcance
1. **Geolocalización en tiempo real y cálculo de rutas:** El sistema no obtiene ni rastrea la posición geográfica en vivo del usuario, ni ofrece navegación paso a paso o cálculo de rutas (tipo GPS/Waze).
2. **Edición colaborativa en línea y foro social:** El sistema no incluye herramientas de manipulación gráfica de imágenes, edición de texto enriquecido en línea estilo wiki, ni secciones de comentarios abiertos o calificaciones comunitarias entre usuarios.
3. **Comercialización, cobro de licencias y donaciones:** El sistema no procesa pasarelas de pago, no cobra por la descarga de acervos patrimoniales ni gestiona donaciones económicas directas en la plataforma.
4. **Digitalización y escaneo automático (OCR):** El sistema no realiza digitalización automatizada ni reconocimiento óptico de caracteres de documentos escaneados; asume que los archivos se cargan ya digitalizados en sus formatos admitidos.

---

## 1.3 Glosario de Términos del Negocio

1. **Locación:** Entidad geográfica delimitada dentro del municipio de Benito Juárez (Cancún) definida por un par de coordenadas (latitud y longitud), un nombre identificador (ej. *Supermanzana 30*, *Playa Delfines*) y una descripción histórica. Se diferencia de un simple *marcador de mapa* en que la locación contiene un expediente histórico con acervo documental agrupado.
2. **Archivo Histórico:** Registro digital individualizado (imagen fotográfica, documento en formato PDF o transcripción textual) que testimonia un suceso, estructura o aspecto de Cancún, fechado en un periodo temporal determinado y vinculado formalmente a una locación.
3. **Documento:** Modalidad de archivo histórico estructurado en formato paginado (típicamente `.pdf`) correspondiente a publicaciones de prensa, decretos oficiales, contratos, cartas o planos arquitectónicos. Se diferencia de *Imagen* en que prioriza contenido textual o normativo formal multipartes.
4. **Imagen:** Modalidad de archivo histórico visual estático (en formatos `.jpg`, `.png`, `.webp`) que reproduce una captura fotográfica, postal, tarjeta promocional o ilustración de una época específica. Se diferencia de *Documento* en que su valor testimonial primordial es iconográfico y compositivo.
5. **Texto:** Registro textual enriquecido de corta o mediana extensión que contiene crónicas orales, testimonios urbanos transcritos o ensayos analíticos sobre un hito de la ciudad, redactado directamente o cargado en el sistema sin depender de un escaneo gráfico.
6. **Propuesta de Aporte:** Solicitud formal de contribución enviada por un usuario visitante que contiene un recurso digital aspirante a integrarse al acervo, metadatos sugeridos (año aproximado, locación y contexto) y sujeta al flujo de moderación del administrador. Se diferencia de un *Archivo Histórico* en que la propuesta carece de validez pública oficial hasta ser dictaminada y aprobada.
7. **Línea del Tiempo (Timeline):** Representación secuencial horizontal de los archivos de una locación ordenados ascendentemente por su fecha de procedencia histórica, permitiendo contrastar visualmente transformaciones urbanas a través de las décadas.
