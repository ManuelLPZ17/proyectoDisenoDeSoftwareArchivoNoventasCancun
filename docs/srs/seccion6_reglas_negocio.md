# Sección 6: Reglas de Negocio (RN)

- **RN-01:** Toda locación registrada en el sistema debe contar obligatoriamente con un nombre identificador único, una descripción general y coordenadas geográficas válidas.
- **RN-02:** Todo documento publicado en el archivo de una locación debe estar integrado por al menos una imagen (`.jpg`, `.png`, `.webp`) con año de procedencia histórica asignado acompañada de su texto descriptivo, por un texto con valor artístico propio (sin fecha histórica asociada), o bien constituir un documento PDF indivisible (`.pdf`).
- **RN-03:** Una propuesta de aporte debe transitar estrictamente por el ciclo de vida de estados en orden: se crea como `Pendiente`, pasa a `Revisada` al ser abierta por el administrador, y finalmente solo puede ser dictaminada a `Aprobada` (incorporando el documento al archivo de la locación) o a `Rechazada` (especificando obligatoriamente un motivo de rechazo).
- **RN-04:** La vista de línea del tiempo cronológica interactiva solo se habilita y genera para aquellas locaciones cuyo archivo contenga dos o más documentos aprobados con fechas de procedencia distintas.
- **RN-05:** La descarga masiva en formato `.zip` solo se permite para locaciones cuyo archivo cuente con al menos un documento publicado y cuyo peso total acumulado no supere los $100\text{ MB}$.
