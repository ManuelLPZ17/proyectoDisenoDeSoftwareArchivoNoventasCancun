# Sección 1: Alcance y Glosario

## 1.1 Declaración del Problema y Beneficiarios
La memoria del desarrollo urbano y social de Cancún se encuentra dispersa en archivos personales físicos, colecciones desarticuladas y publicaciones digitales efímeras, careciendo de anclaje espacial. Esta dispersión dificulta que locales, investigadores y entusiastas comprendan la evolución cronológica y geográfica de la ciudad desde sus orígenes. **ArchivoNoventasCancún** intentará resolver esta problemática centralizando y catalogando recursos históricos (fotografías, recortes de prensa, documentos y textos) georreferenciados sobre un mapa interactivo. El sistema beneficia a los ciudadanos locales, cronistas e investigadores culturales al ofrecer acceso público y contextualizado a dicho patrimonio, a la vez que proporciona a los administradores del archivo una plataforma centralizada para curar, organizar y preservar este acervo colectivo.

## 1.2 Delimitación del Alcance

### Dentro del Alcance
1. **Exploración cartográfica georreferenciada:** Visualización en un mapa interactivo de locaciones de interés cultural e histórico de Cancún identificadas por marcadores geográficos.
2. **Consulta del archivo y previsualización de documentos:** Despliegue del archivo de cada locación y previsualización de sus documentos vinculados (imágenes con su texto descriptivo y documentos PDF).
3. **Línea del tiempo cronológica:** Generación de una vista cronológica interactiva para locaciones cuyo archivo cuente con dos o más documentos fechados en distintos momentos históricos.
4. **Hipervínculos entre recursos:** Navegación cruzada mediante enlaces embebidos entre documentos y locaciones temáticamente vinculados.
5. **Descarga individual y masiva:** Descarga directa de documentos individuales en su formato original y descarga en lote del archivo completo de una locación comprimido en formato `.zip`.
6. **Módulo de propuestas ciudadanas:** Formulario abierto para que usuarios envíen solicitudes de nuevos documentos aportados (imagen, texto descriptivo, año propuesto y locación vinculada) sin requerir autenticación previa.
7. **Panel de curaduría y moderación administrativa:** Interfaz exclusiva para el administrador con autenticación, permitiendo crear locaciones, publicar documentos oficiales y gestionar las propuestas recibidas a través de un ciclo de vida con estados (`Pendiente`, `Revisada`, `Aprobada`, `Rechazada`).
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
3. **Documento:** Unidad de publicación dentro del *Archivo* de una locación, conformada por una o más *Imágenes* fechadas históricamente acompañadas de su *Texto* descriptivo (tipo *caption*).
4. **Documento PDF:** Tipo especializado de *Documento* que almacena un expediente paginado e indivisible en formato `.pdf` (ej. un plan de contingencia de protección civil como Wilma 2004), el cual se consulta y descarga íntegro sin descomponerse en imágenes y textos sueltos.
5. **Imagen:** Recurso visual estático (`.jpg`, `.png`, `.webp`) que puede ser una fotografía análoga, postal o un recorte de época. Posee sentido testimonial por sí sola, porta el año o fecha de procedencia histórica y se integra dentro de un *Documento*.
6. **Texto:** Escrito asociado a una *Imagen* que cumple la función de pie de foto (*caption*) para contextualizar las *Imágenes*, y que no tiene sentido aislado.
7. **Propuesta de Aporte:** Solicitud formal de contribución enviada por un usuario visitante que contiene material aspirante a integrarse como *Documento* en el *Archivo* de una locación, sujeta al flujo de moderación del administrador (`Pendiente`, `Revisada`, `Aprobada`, `Rechazada`).
8. **Línea del Tiempo (Timeline):** Vista secuencial generada a partir del *Archivo* de una locación que ordena ascendentemente sus *Documentos* por fecha de procedencia histórica.
    