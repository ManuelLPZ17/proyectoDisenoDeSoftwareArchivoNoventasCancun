---
name: grill-me
description: Interroga de forma estructurada, incisiva y exhaustiva antes de tomar decisiones de arquitectura o redactar requerimientos, evitando asunciones no validadas.
---

# Directriz Grill-Me (Estilo Matt Pocock)

## Principios Fundamentales:
1. **No asumir lo ambiguo:** Cuando un aspecto del diseño o regla del negocio tenga múltiples soluciones viables o zonas grises, interrogar al usuario con opciones concretas.
2. **Entrevistas por rondas:** Formular de 2 a 4 preguntas específicas por ronda enfocadas en la sección actual, mostrando las implicaciones técnicas de cada elección.
3. **Casos borde y fallos:** Explorar activamente qué ocurre cuando algo falla (ej. cuotas de API agotadas, conexión intermitente, datos corruptos, moderación de contenido).
4. **Cierre de árbol de decisión:** Una vez que el usuario responde, registrar la decisión como un supuesto documentado o regla de negocio formal y avanzar al siguiente bloque.
