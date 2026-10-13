# Sección 1: Alcance y Glosario

## 1.1 Declaración del Problema y Beneficiarios
La memoria del desarrollo urbano y social de Cancún se encuentra dispersa en archivos personales físicos, colecciones desarticuladas y publicaciones digitales efímeras, careciendo de anclaje espacial. Esta dispersión dificulta que locales, investigadores y entusiastas comprendan la evolución cronológica y geográfica de la ciudad desde sus orígenes. **ArchivoNoventasCancún** intentará resolver esta problemática centralizando y catalogando recursos históricos (fotografías, recortes de prensa, documentos y textos) georreferenciados sobre un mapa interactivo. El sistema beneficia a los ciudadanos locales, cronistas e investigadores culturales al ofrecer acceso público y contextualizado a dicho patrimonio, a la vez que proporciona a los administradores del archivo una plataforma centralizada para curar, organizar y preservar este acervo colectivo.

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

1. **Locación:** Entidad geográfica delimitada dentro del municipio de Benito Juárez (Cancún) definida por un par de coordenadas (latitud y longitud) y un nombre identificador (ej. *Supermanzana 30*, *Playa Delfines*). Posee un único *Archivo* asociado.
2. **Archivo:** Contenedor documental único perteneciente a una *Locación* que reúne, organiza cronológicamente y permite empaquetar en `.zip` todos los *Documentos* históricos vinculados a ese punto geográfico. Se diferencia de *Documento* en que el *Archivo* es la colección completa del lugar, mientras que el *Documento* es cada entrada individual dentro de dicha colección.
3. **Documento:** Unidad de publicación dentro del *Archivo* de una locación, conformada por una o más *Imágenes* fechadas históricamente acompañadas de su *Texto* descriptivo (tipo *caption*), o bien por un *Texto* con valor artístico propio.
4. **Documento PDF:** Tipo especializado de *Documento* que almacena un expediente paginado e indivisible en formato `.pdf` (ej. un plan de contingencia de protección civil como Wilma 2004, un decreto oficial o un fanzine compilatorio), el cual se consulta y descarga íntegro sin descomponerse en imágenes y textos sueltos.
5. **Imagen:** Recurso visual estático (`.jpg`, `.png`, `.webp`) que reproduce una fotografía análoga, postal o recorte de época. Posee sentido testimonial por sí sola, porta el año o fecha de procedencia histórica y se integra dentro de un *Documento*.
6. **Texto:** Escrito asociado a un *Documento* (redactado en el presente, por lo que carece de fecha de procedencia histórica) que cumple la función de reseña o pie de foto (*caption*) para contextualizar las *Imágenes*, y que no tiene sentido aislado salvo cuando posee valor artístico o literario propio.
7. **Propuesta de Aporte:** Solicitud formal de contribución enviada por un usuario visitante que contiene material aspirante a integrarse como *Documento* en el *Archivo* de una locación, sujeta al flujo de moderación del administrador (`Pendiente`, `Revisada`, `Aprobada`, `Rechazada`).
8. **Línea del Tiempo (Timeline):** Vista secuencial generada a partir del *Archivo* de una locación que ordena ascendentemente sus *Documentos* por fecha de procedencia histórica para contrastar transformaciones urbanas a través de los años.
