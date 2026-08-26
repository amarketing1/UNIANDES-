# Workflow de match y gobernanza de memoria

Actualización: 25 de agosto de 2026.

## Objetivo

Mantener GitHub como memoria viva y ordenada del proyecto UNIANDES, evitando duplicados, contradicciones y pérdida de decisiones aprobadas.

## Flujo recomendado para cada nueva conversación

1. Identificar si el pedido pertenece a una serie, campaña, plantilla o sistema existente.
2. Buscar la regla específica más cercana en GitHub.
3. Comparar con la instrucción más reciente del usuario.
4. Aplicar la jerarquía de decisión de `docs/00_memoria_maestra.md`.
5. Producir la pieza/prompt.
6. Si el usuario aprueba una nueva decisión reutilizable, actualizar GitHub.

## Qué merece entrar a GitHub

Sí versionar:

- prompts maestros;
- reglas repetidas;
- plantillas aprobadas;
- lineamientos de composición;
- copies finales reutilizables;
- criterios de fotografía/edición;
- inventario de activos;
- campañas/eventos como archivo histórico;
- convenciones de formatos y entrega.

No versionar automáticamente:

- cada microcorrección aislada;
- datos personales innecesarios;
- prompts descartados sin valor histórico;
- contraseñas/tokens;
- archivos de fuentes sin licencia;
- imágenes privadas en un repositorio público.

## Estados

Cada decisión importante debe poder clasificarse como:

- `VIGENTE`
- `APROBADO`
- `HISTÓRICO`
- `REFERENCIA`
- `PENDIENTE DE VERIFICACIÓN`
- `PENDIENTE BINARIO`

## Resolución de contradicciones

Ejemplo:

- Memoria antigua: “usar águila”.
- Pedido actual: “elimina el águila”.

Resultado: se elimina el águila. La memoria describe una posibilidad creativa, no una obligación.

Ejemplo:

- Serie aprobada usa fondo azul.
- Usuario pide versión verde sustentabilidad.

Resultado: verde prevalece para esa pieza. Si la variante se repite y se aprueba, documentarla como sublínea.

## Naming sugerido

### Documentación

`docs/NN_tema.md`

### Prompts

`prompts/NN_nombre_prompt.md`

### Series

`series/nombre_serie.md`

### Activos futuros

Si el repositorio recibe archivos binarios autorizados:

- `assets/logos/`
- `assets/eagle/`
- `assets/campus/`
- `assets/hoodie/`
- `assets/referencias/`

No guardar fuentes comerciales en `assets/fonts/` salvo permiso/licencia explícitos.

## Match de archivos

Antes de crear un archivo nuevo:

1. comprobar si el concepto ya existe;
2. actualizar el archivo existente cuando sea una ampliación natural;
3. crear uno nuevo solo si mejora navegación y separación conceptual;
4. no duplicar el mismo prompt con nombres distintos.

## Match de prompts

Un prompt maestro debe separar:

- objetivo;
- formato;
- sujeto/acción;
- composición;
- fondo;
- iluminación;
- paleta;
- elementos obligatorios;
- elementos prohibidos;
- nivel de realismo;
- preservaciones exactas.

## Control de calidad visual

Antes de considerar una pieza alineada con UNIANDES:

- ¿se entiende el tema/carrera sin leer demasiado?
- ¿la persona/objeto principal tiene protagonismo correcto?
- ¿la piel, manos y bordes se ven naturales?
- ¿hay espacio útil para información si el arte lo requiere?
- ¿la paleta responde a la campaña y no solo a una costumbre?
- ¿se preservaron literalmente los elementos solicitados?
- ¿la composición soporta el formato final sin deformación?

## Revisión periódica

Cuando la memoria crezca:

- fusionar reglas duplicadas;
- mover campañas cerradas a histórico;
- promover patrones repetidos a `VIGENTE`;
- marcar activos binarios faltantes;
- actualizar README con nuevos índices.

## Fuente de verdad

GitHub funciona como memoria operativa versionada. Sin embargo, ante una discrepancia, **la instrucción explícita más reciente del usuario tiene prioridad**.
