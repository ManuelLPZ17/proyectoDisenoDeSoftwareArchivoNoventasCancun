# Sección 2: Contexto y Actores

## 2.1 Situación Actual y Cambio Propuesto
Actualmente, el rescate de la memoria fotográfica y documental de Cancún ocurre de forma fragmentada en redes sociales, repositorios fotográficos sin catalogación sistemática o álbumes familiares inaccesibles al público general. Las plataformas cartográficas comerciales existentes (como Google Maps) priorizan establecimientos comerciales activos, opiniones mercantiles y rutas viales, omitiendo la dimensión histórica y evolutiva de los espacios urbanos. Aquellas personas o investigadores que poseen documentos relevantes no disponen de un canal formal ni georreferenciado para contribuir con sus registros. **ArchivoNoventasCancún** transforma esta situación proporcionando una plataforma web interactiva donde el territorio urbano de Cancún se reinterpreta como un circuito histórico digital: cada punto en el mapa despliega su memoria documental en orden cronológico, y cualquier usuario puede proponer material fotográfico y documental para ser curado y publicado por administradores del archivo.

---

## 2.2 Diagrama de Contexto del Sistema

```mermaid
flowchart TD
    subgraph ActoresHumanos ["Actores Humanos"]
        U["Usuario (Visitante / Colaborador)"]
        A["Administrador (Curador del Archivo)"]
    end

    SYS["Sistema ArchivoNoventasCancún\n(Caja Negra)"]

    subgraph SistemasExternos ["Sistemas Externos"]
        GM["API de Google Maps\n(Proveedor Cartográfico)"]
    end

    %% Interacciones Usuario
    U -->|"1. Solicitud de visualización de mapa\n2. Consulta de locación o documento\n3. Envío de propuesta de aporte\n4. Petición de descarga individual o ZIP"| SYS
    SYS -->|"1. Renderizado de interfaz y marcadores\n2. Archivo de locación, documentos y línea de tiempo\n3. Notificación de folio de propuesta\n4. Entrega de documento o paquete ZIP"| U

    %% Interacciones Administrador
    A -->|"1. Credenciales de autenticación\n2. Alta/edición de locaciones y documentos\n3. Dictamen de propuestas (aprobar/rechazar)"| SYS
    SYS -->|"1. Acceso a consola de administración\n2. Lista de propuestas pendientes\n3. Confirmación de operaciones de catálogo"| A

    %% Interacciones Sistema Externo
    SYS -->|"1. Petición de carga de capas de mapa y estilos\n2. Solicitud de renderizado de marcadores (lat, lng)"| GM
    GM -->|"1. Mosaicos cartográficos renderizados\n2. Eventos de interacción sobre el mapa (clic, zoom)"| SYS
```

---

## 2.3 Tabla de Actores y Sistemas Externos

| Actor / Sistema Externo | Tipo | Qué hace en el sistema | Información que envía al sistema | Información que recibe del sistema | Comportamiento si no responde / falla |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Usuario (Visitante)** | Persona (Humano) | Explora el mapa, consulta el archivo y los documentos de cada locación, visualiza líneas del tiempo, descarga documentos individuales o el archivo completo en ZIP, y envía propuestas ciudadanas de aporte. | Términos de búsqueda, selección de locaciones/documentos, datos de formulario de propuesta (archivo binario, metadatos, contacto opcional). | Vistas del mapa, archivo de la locación, previsualizaciones de documentos, paquetes ZIP de descarga, folio de confirmación de propuesta. | N/A (Es el cliente emisor). |
| **Administrador** | Persona (Humano) | Autentica su sesión, crea y actualiza locaciones, publica documentos con sus metadatos oficiales, y revisa el buzón de propuestas para aprobarlas o rechazarlas. | Credenciales de acceso (usuario y contraseña), formularios de alta de locación (nombre, coordenadas, reseña), documentos validados, dictámenes de moderación. | Tablero de control administrativo, cola de propuestas con estado actual, confirmaciones de guardado o errores de validación. | N/A (Es el operador administrativo). |
| **Google Maps JavaScript API** | Sistema Externo | Provee el motor cartográfico, mosaicos de satélite/mapa urbano, estilos visuales y la capa interactiva sobre la cual se proyectan los marcadores geográficos. | Mosaicos de mapa generados, eventos de interacción en el canvas (clic en coordenadas, cambio de nivel de zoom). | Clave de API (*API Key*), coordenadas base de Cancún, configuraciones de estilo gráfico, coordenadas de marcadores de locaciones. | **Política de degradación:** Si la API no responde, agota su cuota de peticiones o devuelve error de red, el sistema oculta el contenedor del mapa y despliega un banner de contingencia con una **vista alternativa en catálogo/tabla cronológica**. Esta vista permite a los usuarios continuar buscando locaciones, visualizando expedientes y descargando archivos sin interrumpir la operación principal. |
