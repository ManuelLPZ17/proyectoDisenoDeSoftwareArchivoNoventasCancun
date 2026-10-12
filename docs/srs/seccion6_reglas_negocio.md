# Sección 6: Reglas de Negocio (RN)

Una regla de negocio es una política o directriz rectora que el sistema debe respetar en todo momento. Cada regla describe la condición obligatoria que rige sobre las operaciones del dominio:

- **RN-01:** Toda locación registrada en el sistema debe contar obligatoriamente con un nombre identificador único, una descripción general y coordenadas geográficas válidas (latitud entre $-90$ y $90$, longitud entre $-180$ y $180$).
- **RN-02:** Todo archivo histórico publicado debe estar forzosamente asociado a al menos una locación existente, poseer un formato admitido (`.jpg`, `.png`, `.webp` o `.pdf`) y tener asignado un año de procedencia histórica comprobable.
- **RN-03:** Una propuesta de aporte debe transitar estrictamente por el ciclo de vida de estados en orden: se crea como `Pendiente`, pasa a `Revisada` al ser abierta por el administrador, y finalmente solo puede ser dictaminada a `Aprobada` (incorporando el archivo al acervo oficial) o a `Rechazada` (especificando obligatoriamente un motivo de rechazo).
- **RN-04:** La vista de línea del tiempo cronológica interactiva solo se habilita y genera para aquellas locaciones que contengan dos o más archivos históricos aprobados con fechas de procedencia distintas.
- **RN-05:** La descarga masiva en formato `.zip` solo se permite para locaciones que cuenten con al menos un archivo histórico publicado y cuyo peso total acumulado no supere los $150\text{ MB}$.
