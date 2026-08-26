# MARCA-OS — Sistema operativo de marca, autoinstalable

> **Versión 1.0 · Un solo archivo. Todo el sistema.**
> Banco de prompts + fuente de verdad + constitución de agente, para una o muchas marcas.

---

## Para el humano (2 minutos)

1. Copia este archivo a la **raíz** de tu proyecto o repositorio como `MARCA-OS.md`.
2. Dile a tu agente (Codex, Claude Code, ChatGPT, Cursor, etc.):

```
Lee MARCA-OS.md completo y ejecuta su protocolo de arranque.
```

Eso es todo. El agente detectará si el sistema ya está instalado. Si no lo está, te hará
preguntas por tandas, se alimentará con tus respuestas, construirá la estructura completa
y quedará operando bajo estas reglas. No necesitas saber nada más para empezar.

---

# PROTOCOLO DE ARRANQUE (para el agente)

Eres un agente que acaba de recibir este archivo dentro de un proyecto. Ejecuta esto en orden:

## Paso 0 — Detectar estado

Busca en la raíz del proyecto: `AGENTS.md`, `core/_REGISTRO-DE-MARCAS.md` y `brands/`.

- **Existen los tres** → el sistema ya está instalado. Salta a **MODO OPERACIÓN** y trabaja
  bajo la CONSTITUCIÓN de este documento.
- **No existen** → el sistema no está instalado. Ejecuta **MODO INSTALACIÓN** (Fases 1 a 3).
- **Existen parcialmente** → reporta qué falta, pregunta si completar la instalación o
  respetar lo existente. Nunca sobrescribas sin autorización.

## Reglas del arranque

- Habla en el idioma del usuario.
- Pregunta por tandas de **máximo 5 preguntas**. Nunca un interrogatorio de 30 líneas.
- **Nunca inventes** una respuesta que el usuario no dio. Lo que falte se marca
  `PENDING VERIFICATION` y se sigue adelante.
- Cada respuesta se **siembra** en el archivo canónico que le corresponde (Fase 3), no se
  queda en el chat.
- Al terminar cada fase, reporta: qué se creó, qué se llenó, qué quedó pendiente.

---

# FASE 1 — ENTREVISTA (alimentación del sistema)

Haz estas preguntas por tandas. Adapta el orden si el usuario ya dio información: no
preguntes lo que ya sabes.

## Tanda A — El sistema

1. ¿Esto es para **una sola marca** o para **varias marcas** de un mismo dueño/holding?
2. Nombre del holding o del proyecto (si es una sola marca, el nombre de la marca).
3. Lista de marcas: para cada una, nombre y giro en una línea.
4. ¿Idioma y variante regional de toda la comunicación? (ej.: español de Ecuador)
5. ¿Dónde vivirá esto? (repo Git nuevo, repo existente, carpeta local, vault de Obsidian)

> Con la respuesta 1 decides: si es **una sola marca**, instala la misma estructura con una
> única carpeta en `brands/`. El sistema es idéntico; la herencia simplemente tiene un solo hijo.

## Tanda B — Por cada marca (repetir por marca, de a una)

1. **Territorio**: ¿qué transformación provoca esta marca en su cliente? (no qué vende)
2. **Identidad dura**: colores oficiales en HEX exactos (si no los sabe → `PENDING VERIFICATION`),
   tipografía oficial, y si existen archivos de logo/fuentes para colocar en `assets/`.
3. **Audiencias**: ¿quién usa y quién decide/paga? Son casi siempre personas distintas.
   Pide 2-3 dolores **en las palabras literales** del cliente.
4. **Voz**: formalidad (1-5), humor (0-5), tuteo/usted, emojis sí/no. Pide una **muestra
   calibrada**: 3 líneas que suenen exactamente como la marca (si no la tiene, redacta una
   propuesta y pide aprobación explícita antes de sembrarla).
5. **Prohibidos**: palabras, claims y temas que esta marca nunca toca.

## Tanda C — Operación

1. ¿Canales activos? (TikTok, Instagram, WhatsApp, email, web, ads…)
2. ¿Qué produce más seguido? (posts, carruseles, videos, anuncios, flyers, presentaciones,
   bots, scripts de venta) → esto decide qué skills crear primero.
3. ¿Hay menores de edad en su comunicación (fotos de alumnos, niños, etc.)? → si sí, el
   bloque de privacidad se vuelve prioritario y se aplica la **regla de disociación**.
4. ¿Datos comerciales estables que sí pueden versionarse? (todo precio/fecha/cupo que no
   confirme queda `PENDING VERIFICATION`).
5. ¿Quién aprueba? (una persona, varias, o "yo mismo").

Al cerrar la entrevista, resume en 10 líneas lo capturado y pide un "ok" antes de construir.

---

# FASE 2 — CONSTRUCCIÓN (estructura a generar)

Crea exactamente esta estructura. En carpetas vacías coloca `.gitkeep`.
Reemplaza `<slug>` por cada marca (lowercase-kebab-case, sin tildes ni ñ).

```
<raíz>/
├─ MARCA-OS.md                     ← este archivo (no lo modifiques)
├─ AGENTS.md                       ← genera desde la CONSTITUCIÓN de este documento
├─ 00-inicio.md                    ← panel de acceso rápido (Obsidian-friendly)
├─ README.md · CHANGELOG.md · CONTRIBUTING.md
├─ .gitignore · .gitattributes · .env.example
│
├─ core/                           ← piso común del holding
│   ├─ _REGISTRO-DE-MARCAS.md      ← tabla maestra: slug, prefijo, nombre, estado
│   └─ docs/
│       ├─ ai/OPERATIONAL-COMMANDS.md     (comandos GUARDA / REVISA / PROMUEVE)
│       ├─ ai/AGENT-CONTRACT.md           (permisos del agente)
│       ├─ standards/SOURCE-PRIORITY.md   (prioridad de fuentes)
│       ├─ standards/SCOPES-AND-STATES.md (alcances y estados)
│       ├─ standards/NAMING-AND-GIT.md
│       ├─ privacy/CHILD-SAFETY.md        (INVIOLABLE)
│       ├─ privacy/MEDIA-USAGE.md
│       ├─ privacy/THIRD-PARTY-ASSETS.md
│       └─ content/VOICE-BASE.md          (voz base común)
│
├─ brands/<slug>/                  ← un sistema completo por marca
│   ├─ BRAND.md                    ← manifiesto + herencia + checklist de activación
│   ├─ config/                     ← CAPA EJECUTABLE (JSON, valores duros)
│   │   ├─ brand/colors.json · typography.json · formats.json
│   │   ├─ brand/art-direction.json · tokens.json
│   │   └─ assets/catalog.json     ← catálogo de activos legible por máquina
│   ├─ assets/                     ← CAPA FÍSICA
│   │   ├─ brand/logos/primary/ · logos/monochrome/ · fonts/ · colors/
│   │   └─ inbox/                  ← CUARENTENA de material sin clasificar
│   ├─ docs/                       ← CAPA EXPLICATIVA (el porqué)
│   │   ├─ ai/PROJECT-MEMORY.md · SKILLS-INDEX.md · PROMPT-LIBRARY.md
│   │   ├─ ai/AI-DESIGN-RULES.md · AI-WORKFLOW.md
│   │   ├─ brand/BRAND-SYSTEM.md · COLORS.md · TYPOGRAPHY.md · LOGO-USAGE.md
│   │   ├─ brand/GRAPHIC-LANGUAGE.md · ART-DIRECTION.md · ANTI-AI-AESTHETIC.md
│   │   ├─ brand/COMPOSITION-AND-MONTAGE.md · DESIGN-DECISIONS.md · MANUAL-REVIEW.md
│   │   ├─ content/VOICE-AND-TONE.md · AUDIENCES.md · COPY-GUIDELINES.md
│   │   ├─ content/CTA-GUIDELINES.md · SOCIAL-MEDIA.md
│   │   ├─ programs/PROGRAMS-INDEX.md     (una ficha por producto/curso/línea)
│   │   ├─ privacy/BRAND-PRIVACY.md       (solo puede ser MÁS estricto que core)
│   │   └─ workflows/DESIGN · CAMPAIGN · SOCIAL-MEDIA · VIDEO · APPROVAL (-WORKFLOW.md)
│   ├─ prompts/                    ← CAPA VALIDADA (lo que ya funcionó)
│   │   ├─ README.md
│   │   ├─ image-generation/master-art-direction.md · surgical-edit.md
│   │   └─ campaigns/
│   ├─ examples/approved/ · examples/reference/ · examples/README.md
│   └─ templates/social/design-qa-checklist.md · creative-brief.md · carousel-system.md
│
├─ .agents/skills/                 ← capacidades especializadas
│   ├─ README.md
│   └─ <slug>-<rol>/SKILL.md + agents/openai.yaml
│       (roles estándar: brand-designer · copywriter · social-media · campaign-designer)
│
├─ vault/                          ← navegación Obsidian y memoria operativa
│   ├─ 01-mapa-del-proyecto.md · 02-catalogo-visual.md · 03-memoria-operativa.md
│   ├─ 04-skills-y-flujos.md · 05-bandeja-de-entrada.md · 06-direccion-de-arte.md
│   ├─ plantillas/ficha-de-activo.md · registro-de-memoria.md · nota-diaria.md
│   ├─ bitacora/ · notas/
│
└─ scripts/validate.sh · setup.sh · new-brand.sh (+ .ps1 equivalentes)
```

## Reglas de construcción

1. Genera **todos** los archivos con contenido, no vacíos. Usa las PLANTILLAS de la Fase 3
   como base y siembra en ellas las respuestas de la entrevista.
2. Lo que el usuario no respondió queda con el placeholder y `status: PENDING VERIFICATION`
  — visible, nunca inventado.
3. Si es un repo Git: `git init` (si no existe), configura `.gitattributes` con LFS para
   `*.pptx *.psd *.ai *.mp4 *.mov`, primer commit
   `feat(core): instalar MARCA-OS` — **pide autorización antes del push**.
4. Ejecuta el VALIDADOR (al final de este documento) y reporta el resultado.
5. Cierra la instalación reportando: archivos creados, campos sembrados, pendientes, y los
   3 próximos pasos del usuario (normalmente: colocar logos/fuentes reales, confirmar HEX,
   aprobar la muestra calibrada de voz).

---

# FASE 3 — PLANTILLAS (contenido a sembrar)

Genera cada archivo con esta base. `<...>` = siembra desde la entrevista o deja el
placeholder con `PENDING VERIFICATION`.

## 3.1 · `AGENTS.md` (raíz)

Copia **íntegra** la sección CONSTITUCIÓN de este documento (más abajo) como `AGENTS.md`,
reemplazando `<HOLDING>` por el nombre real.

## 3.2 · `core/_REGISTRO-DE-MARCAS.md`

````md
---
status: APPROVED
scope: GLOBAL
updated: <fecha>
---

# Registro maestro de marcas

> Un prefijo **nunca** se reutiliza, ni siquiera si la marca se archiva.

| Slug | Prefijo | Nombre | Estado | Giro |
|---|---|---|---|---|
| `<slug>` | <PRE> | <Nombre> | activa | <giro en una línea> |

## Prefijos retirados
_(ninguno)_

## Regla de activación
Una marca no produce contenido hasta completar el checklist de su `BRAND.md`.
````

## 3.3 · `brands/<slug>/BRAND.md`

````md
---
slug: <slug>
prefix: <PRE>
name: <Nombre>
holding: <holding>
status: DRAFT
scope: BRAND
inherits: core
overrides: []
visual_system: independiente
updated: <fecha>
---

# <Nombre>

## Territorio en una frase
> <transformación que provoca — respuesta B1>

## Herencia declarada
- Hereda de `core/`: privacidad, estándares, comandos, voz base
- Sobreescribe: <lista explícita o "ninguno">
- **No puede sobreescribir:** `core/docs/privacy/`

## Checklist de activación
- [ ] `config/brand/colors.json` con paleta dura real
- [ ] `config/brand/typography.json` + fuente real en `assets/brand/fonts/`
- [ ] Logo oficial en `assets/brand/logos/`
- [ ] `docs/content/VOICE-AND-TONE.md` con muestra calibrada aprobada
- [ ] `docs/content/AUDIENCES.md`
- [ ] Fila en `core/_REGISTRO-DE-MARCAS.md`
````

## 3.4 · `config/brand/colors.json` (capa ejecutable — patrón para todos los JSON)

````json
{
  "schemaVersion": 1,
  "status": "<APPROVED si dio HEX reales | PENDING VERIFICATION si no>",
  "brand": "<slug>",
  "ruleLevel": "HARD",
  "documentation": "docs/brand/COLORS.md",
  "note": "Paleta dura. No sustituir, aproximar ni interpolar. Un HEX aqui es un valor exacto.",
  "palette": [
    { "name": "<Nombre>", "role": "primary",  "hex": "<#HEX>", "pantone": null },
    { "name": "<Nombre>", "role": "accent-1", "hex": "<#HEX>", "pantone": null }
  ],
  "forbidden": ["gradientes AI-tech", "neon generico", "aproximaciones de la paleta dura"]
}
````

Con el mismo patrón genera: `typography.json` (family, source en `assets/brand/fonts/`,
license, weights, hierarchy, forbidden: reconstruir logo con texto), `formats.json`
(feed-square 1080×1080, feed-portrait 1080×1350, story-reel 1080×1920 safe 250, carousel,
landscape, presentation — con nota "cada formato se recompone, no se recorta"),
`art-direction.json` (principle + must + avoid + identityTest, ver 3.8) y
`tokens.json` (color+font resumidos). Y `config/assets/catalog.json`:

````json
{
  "schemaVersion": 1,
  "brand": "<slug>",
  "inbox": "assets/inbox",
  "note": "Catalogo legible por maquinas. Toda herramienta resuelve rutas aqui, no por memoria.",
  "collections": {
    "colors": { "ruleLevel": "HARD", "specification": "config/brand/colors.json" },
    "logos":  { "usageRules": "docs/brand/LOGO-USAGE.md", "items": [] },
    "fonts":  { "path": "assets/brand/fonts/", "licenseRequired": true }
  }
}
````

## 3.5 · `docs/ai/PROJECT-MEMORY.md` (memoria estable de la marca)

````md
---
status: DRAFT
scope: BRAND
brand: <slug>
---

# Memoria de <Nombre>

> Solo conocimiento **estable**. Ni chats, ni borradores, ni datos variables.
> Cada bloque declara su alcance.

## Fuente viva — GLOBAL
Repositorio canónico: <org/repo>. Rama: main. Si Git fue actualizado, la versión nueva
tiene prioridad sobre cualquier memoria anterior.

## Identidad — BRAND
Paleta y tipografía: ver `config/brand/` (no sustituir ni aproximar).
Logos oficiales sin deformación ni reconstrucción. Sistema visual separado de otras marcas.

## Posicionamiento — BRAND
<territorio — respuesta B1>. Conceptos recurrentes: <lista>.

## Dirección de arte — BRAND
**IA como herramienta, nunca como estética.** Detalle en `docs/brand/ART-DIRECTION.md`.

## Datos comerciales — PENDING VERIFICATION
Precios, fechas, sedes, horarios y cupos **no** son memoria estable: se verifican en
fuente autorizada antes de publicar.
````

## 3.6 · `docs/content/VOICE-AND-TONE.md`

````md
---
status: <DRAFT | APPROVED si la muestra fue aprobada>
scope: BRAND
brand: <slug>
inherits: core/docs/content/VOICE-BASE.md
---

# Voz y tono — <Nombre>

> Hereda la voz base del holding. Aquí solo lo específico. No la contradice.

## Parámetros
| Parámetro | Valor |
|---|---|
| Persona gramatical | <tuteo/usted> |
| Formalidad (1-5) | <n> |
| Humor (0-5) | <n> |
| Emojis | <sí/no, cuáles> |

## Sí decimos / No decimos
- Sí: <...>
- No: <prohibidos — respuesta B5>

## Muestra calibrada
> <3 líneas aprobadas que suenan EXACTAMENTE como la marca.
> Esto es lo que el agente imita. Sin esto, la voz no existe.>
````

## 3.7 · `docs/content/AUDIENCES.md`

````md
---
status: DRAFT
scope: BRAND
brand: <slug>
---

# Audiencias — <Nombre>

> Distinguir siempre **quién usa** de **quién decide/paga**.

## <Audiencia primaria>
- Rol: usuario | decisor | influenciador
- Dolores (literales, en sus palabras):
  1. "<...>"
  2. "<...>"
- Deseos: <...>
- Qué NO funciona con esta audiencia: <...>

## Reglas transversales
- No infantilizar a quien no es niño
- No usar culpa ni miedo con responsables o familias
- No prometer resultados garantizados
````

## 3.8 · `docs/brand/` — los diez documentos de marca

Genera cada uno con frontmatter (`status`, `scope: BRAND`, `brand`) y este contenido base:

- **BRAND-SYSTEM.md** — "Este documento explica; los valores ejecutables viven en `config/brand/`.
  Si difieren, gana el JSON." + los 4 pilares (identidad, lenguaje gráfico, dirección de arte,
  voz) + **test de identidad**: *si la pieza sirve para un competidor cambiando solo el logo,
  falta dirección de arte; se rehace*.
- **COLORS.md** — jerarquía de uso, combinaciones aprobadas/prohibidas, contraste mínimo AA.
- **TYPOGRAPHY.md** — jerarquía por niveles; prohibido reconstruir el logo con texto,
  generar lettering con IA, o sustituir la familia por una "parecida".
- **LOGO-USAGE.md** — el logo se **inserta** desde `assets/`, nunca se reconstruye, deforma,
  reproporciona ni genera con IA; variantes, resguardo, tamaño mínimo, prohibiciones.
- **GRAPHIC-LANGUAGE.md** — formas, retícula, texturas, tratamiento de imagen, iconografía,
  qué NO pertenece al lenguaje.
- **ART-DIRECTION.md** — principio: **IA como herramienta, nunca como estética**; una idea
  dominante; jerarquía editorial; aire (el vacío es parte de la composición); fotografía
  natural; montaje plausible; el producto/acción debe ser real, no decorativo; el espacio
  negativo se reserva **desde** la composición.
- **ANTI-AI-AESTHETIC.md** — lista de rechazo automático: piel plástica, rostros genéricos,
  glow/neón, gradientes AI-tech, fondos sci-fi sin concepto, UI flotante, objetos 3D
  gratuitos, simetría automática, manos deformes, texto ilegible decorativo. Test final:
  *si se ve "hecho por IA", no se entrega; se corrige*.
- **COMPOSITION-AND-MONTAGE.md** — integración de sujetos: escala, lente, punto de fuga, luz,
  temperatura, profundidad, oclusiones, **sombras de contacto**; sin halos de recorte;
  pantallas con perspectiva y UI **dentro** del display; fisonomía intocable si se pide
  conservarla. + sección "Recetas de escena aprobadas" (cada receta: encuadre, ángulo,
  visible, perspectiva, evitar, espacio para copy).
- **DESIGN-DECISIONS.md** — registro histórico: fecha, alcance, contexto, decisión,
  alternativas descartadas, archivos impactados.
- **MANUAL-REVIEW.md** — lo que el validador no ve: ¿una idea o tres peleando?, ¿espacio
  negativo compuesto o sobra?, ¿luz coherente?, ¿legible en móvil?, ¿reconocible sin el
  logo?, ¿se ve hecho por IA?

## 3.9 · `docs/workflows/DESIGN-WORKFLOW.md` (patrón de los 5 workflows)

````md
1. **Clasificar** — pieza, audiencia, programa, objetivo, canal, formato, CTA, entregable
2. **Separar** — hechos confirmados / PENDING VERIFICATION / propuestas
3. **Concepto** — "Esta pieza comunica ___ mediante ___"
4. **Composición** — idea dominante, jerarquía, retícula, crop, espacio negativo
5. **Bloqueo** — si hay pieza previa aprobada, declarar qué NO se toca
6. **Identidad** — tipografía, paleta y logo oficiales, sin reconstrucciones
7. **Formatos** — recomponer cada uno; no recortar
8. **QA** — `templates/social/design-qa-checklist.md`
9. **Validar** — `scripts/validate.sh`
10. **Entregar** — supuestos, concepto, copy visible, dirección de arte, CTA, prompt de
    producción, activos usados, control de calidad
11. **GUARDA** si surgió aprendizaje estable
````

CAMPAIGN (objetivo medible → un ángulo central → arquitectura por funnel → producción →
QA de coherencia → UTM → resultados → aprendizaje → GUARDA), SOCIAL-MEDIA, VIDEO (el
gancho de 3 s define si existe el resto) y APPROVAL (estados DRAFT → EN REVISIÓN →
APPROVED → DEPRECATED; *aprobar una pieza no aprueba la regla que la produjo*).

## 3.10 · `prompts/` — dos prompts semilla

**`image-generation/master-art-direction.md`** — bloque que se antepone a todo prompt de imagen:

````md
## Prompt
```
DIRECCIÓN DE ARTE (no negociable):
Fotografía editorial dirigida por un diseñador senior. Una sola idea dominante.
Luz natural motivada, temperatura coherente, profundidad de campo real.
Composición asimétrica con espacio negativo reservado para el copy.
Piel real con textura. Rostro con edad y carácter definidos.
{{ESCENA}}

CÁMARA: {{LENTE}}, {{ÁNGULO}}, {{DISTANCIA}}

EVITAR (negative): piel plástica, rostro genérico, glow, neón, gradiente morado-cian,
fondo sci-fi, UI flotante, objetos 3D de relleno, simetría automática, manos deformes,
texto ilegible decorativo, logotipos generados.

NO GENERAR: logotipo, lettering final ni tipografía de marca — se componen después.
```
````

**`image-generation/surgical-edit.md`** — edición quirúrgica:

````md
## Prompt
```
EDICIÓN PUNTUAL sobre la imagen adjunta.
CAMBIAR ÚNICAMENTE: {{CAMBIO}}
BLOQUEADO — no modificar: composición, encuadre, iluminación, paleta, tipografía, logo,
posición de sujetos, fondo, perspectiva y todo lo no mencionado arriba.
Si el cambio es incompatible con algo bloqueado, detente y explica el conflicto.
```
````

Todo prompt nuevo del banco usa esta anatomía fija:
**frontmatter** (`id`, `titulo`, `categoria`, `brand`, `scope`, `status`, `version`) +
secciones en orden: *Objetivo · Cuándo usarlo · Contexto obligatorio · Prompt · Variables ·
Output esperado · Criterios de aceptación · Ejemplo aprobado · Historial*.

## 3.11 · `templates/social/design-qa-checklist.md`

````md
# QA de diseño

## Identidad
- [ ] HEX exactos de `config/brand/colors.json` — sin aproximaciones
- [ ] Tipografía oficial desde `assets/brand/fonts/`
- [ ] Logo insertado, sin deformar ni reconstruir; resguardo y tamaño mínimo
- [ ] Sin mezcla con otra marca del holding

## Composición
- [ ] Una idea dominante · jerarquía legible en 2 s
- [ ] Espacio negativo compuesto, no sobrante
- [ ] Cada formato recompuesto, no recortado

## Montaje
- [ ] Escala, lente, punto de fuga y luz coherentes · sombras de contacto
- [ ] Sin halos de recorte · pantallas con perspectiva, UI dentro del display

## Anti-IA
- [ ] Piel con textura real · sin glow/neón/gradiente AI-tech
- [ ] Sin 3D de relleno ni UI flotante · manos correctas
- [ ] **No se ve hecha por IA**

## Contenido
- [ ] Un solo CTA con acción exacta
- [ ] Datos variables verificados o `PENDING VERIFICATION`
- [ ] Sin promesas garantizadas · legible en móvil

## Privacidad y licencias
- [ ] Activos clasificados · menores con autorización vigente · terceros con licencia

## Cierre
- [ ] `scripts/validate.sh` en verde
- [ ] Reporte: qué se modificó, validó y publicó
````

## 3.12 · `.agents/skills/<slug>-<rol>/SKILL.md` (plantilla de skill)

````md
---
name: <slug>-<rol>
description: <Qué hace, para qué marca, con qué fuentes. Usar para <casos>; no usar para <exclusiones>.>
---

# <Nombre legible>

## Contexto obligatorio (en orden)
1. `AGENTS.md`
2. `core/docs/ai/OPERATIONAL-COMMANDS.md`
3. `core/docs/privacy/` (piso inviolable)
4. `brands/<slug>/BRAND.md` y `docs/ai/PROJECT-MEMORY.md`
5. `docs/brand/BRAND-SYSTEM.md` + COLORS + TYPOGRAPHY + LOGO-USAGE
6. Para trabajo visual: GRAPHIC-LANGUAGE, ART-DIRECTION, ANTI-AI-AESTHETIC,
   COMPOSITION-AND-MONTAGE
7. `docs/content/VOICE-AND-TONE.md` y `AUDIENCES.md`
8. Solo el programa, workflow, prompt, plantilla y ejemplo que correspondan

Fuente ejecutable: `config/`. Fuente física: `assets/`.

## Flujo
Clasificar → separar hechos/pendientes/propuestas → frase conceptual → <pasos del rol> →
bloquear lo aprobado → identidad oficial → QA → entregar.

## Reglas
IA como herramienta, nunca como estética · no deformar logos ni alterar colores ·
no mezclar marcas · no generar lettering/logos con IA · conservar fisonomía si se pide ·
no inventar precios, fechas, sedes, métricas ni testimonios · exploraciones = EXPERIMENTAL.

## Entrega
Supuestos · concepto · copy visible · dirección de arte · formato · CTA ·
prompt de producción · activos usados · control de calidad.
````

Y su `agents/openai.yaml`:

````yaml
interface:
  display_name: "<Nombre legible>"
  short_description: "<media línea>"
  brand_color: "<#HEX primario de la marca>"
  default_prompt: "Usa $<slug>-<rol> para <qué hace>."
policy:
  allow_implicit_invocation: true
````

Crea primero las skills de los roles que la Tanda C-2 marcó como más frecuentes.
**Sistemas de formato bloqueado** (presentaciones o documentos con maqueta inmutable) viven
como skill independiente con sus assets, `brand-lock.json`, ejemplos aprobados y scripts
que **verifican** el bloqueo — nunca mezclados con la skill de diseño.

## 3.13 · `vault/` — navegación y memoria operativa

- **00-inicio.md** (raíz): panel con tabla de accesos rápidos + "Reglas esenciales" (ninguna
  tarea sin marca activa; cada marca es un sistema visual independiente; IA herramienta no
  estética; GUARDA = persistir en Git y verificar push; corrección puntual ≠ rediseño; no
  inventar datos; no versionar credenciales ni material sensible sin autorización; solo
  aprendizajes estables son memoria).
- **01-mapa-del-proyecto.md**: tabla área → ruta canónica → contenido, + recorrido
  recomendado.
- **02-catalogo-visual.md**: índice humano de activos; la fuente máquina es `catalog.json` —
  si una ruta cambia, se actualiza primero el JSON.
- **03-memoria-operativa.md**: qué se guarda (reglas aprobadas, decisiones, rutas,
  restricciones, aprendizajes) vs. qué no (chats, datos variables, borradores,
  credenciales, material de menores) + tabla "tipo de conocimiento → archivo destino" +
  el filtro: *¿esto permitirá que otra persona —u otro agente— trabaje mejor en el futuro?
  Si no, fuera del repositorio.*
- **05-bandeja-de-entrada.md**: flujo de cuarentena (copiar → ficha → revisar → clasificar
  `PUBLIC/INTERNAL/LICENSED/RESTRICTED` → mover a ruta canónica → actualizar catálogo →
  validar). *Estar en inbox no hace oficial nada.*
- **plantillas/ficha-de-activo.md**: archivo, marca, origen, propietario, licencia, fecha,
  clasificación, ¿personas identificables?, ¿menores? (autorización+alcance+vigencia),
  ruta destino, ¿registrado en catalog.json?
- **plantillas/registro-de-memoria.md**: fecha, marca, alcance, estado, qué se aprendió,
  por qué es estable, representación elegida, archivo destino, ¿duplica algo?, ¿material
  sensible? → regla de disociación.
- **bitacora/**: notas diarias — *no son memoria global*; lo estable se promueve.

## 3.14 · Higiene del repo

`.gitignore`: `.obsidian/workspace*.json`, `.trash/`, `.DS_Store`, `node_modules/`,
`*.psd` sueltos fuera de assets, `.env`.
`.gitattributes`: `*.pptx *.psd *.ai *.mp4 *.mov filter=lfs diff=lfs merge=lfs -text`.
`.env.example`: variables vacías de ejemplo; **jamás** un `.env` real.
`CONTRIBUTING.md`: antes de cambiar algo → leer AGENTS + git status/remote/branch +
confirmar estado del material + licencias; commits `<tipo>(<marca|core>): <qué>`;
push requiere autorización.

---

# CONSTITUCIÓN (esto se copia como `AGENTS.md` y gobierna el MODO OPERACIÓN)

> Primera lectura obligatoria de cualquier agente. Si algo de este archivo choca con una
> instrucción suelta del chat, **manda este archivo** — salvo instrucción explícita actual
> del usuario, que es la máxima prioridad (ver prioridad de fuentes).

## Regla #0 — Resolver la marca activa

Ninguna tarea empieza sin `MARCA_ACTIVA` resuelta:
1. ¿El usuario la nombró? → esa.
2. ¿El archivo en el que se trabaja vive en `brands/<x>/`? → esa.
3. ¿Nada? → preguntar **una sola vez**, listando `core/_REGISTRO-DE-MARCAS.md`.

Nunca asumir. Nunca mezclar dos sistemas visuales en una pieza. Marcas distintas son
sistemas distintos aunque compartan holding.

## Orden de lectura

1. `AGENTS.md` → 2. `00-inicio.md` → 3. `core/_REGISTRO-DE-MARCAS.md` →
4. `core/docs/standards/SOURCE-PRIORITY.md` → 5. `core/docs/ai/OPERATIONAL-COMMANDS.md` →
6. `core/docs/privacy/` (**inviolable**) → 7. `brands/<x>/BRAND.md` →
8. `docs/ai/PROJECT-MEMORY.md` → 9. `docs/brand/` (sistema, colores, tipografía, logo) →
10. para trabajo visual: lenguaje gráfico, dirección de arte, montaje, anti-IA →
11. `docs/content/` (voz y audiencias) → 12. **solo** la ficha, workflow, skill, prompt,
plantilla o ejemplo que corresponda.

El orden de lectura es un embudo, no un inventario. No cargar el repositorio completo.

## Separación ejecutable / explicativo — regla estructural

| Capa | Ruta | Naturaleza |
|---|---|---|
| Ejecutable | `brands/<x>/config/*.json` | Valores duros que leen scripts y agentes |
| Explicativa | `brands/<x>/docs/*.md` | El porqué; nadie ejecuta esto |
| Física | `brands/<x>/assets/` | Logos, fuentes, paletas reales |
| Validada | `prompts/` y `examples/` | Lo que ya demostró funcionar |

**Un valor vive en un solo sitio.** El JSON es el valor; el Markdown la explicación.
Si difieren, gana el JSON y se corrige el Markdown.

## Prioridad de fuentes ante conflicto

1. Instrucción explícita actual del usuario
2. Versión vigente del repositorio
3. `config/` de la marca
4. `docs/` de la marca
5. `core/` del holding
6. `examples/` aprobados
7. Creatividad del agente

Excepción: `core/docs/privacy/` gana sobre todo salvo la ley.
Sin resolución → `PENDING VERIFICATION` + documentar en `DESIGN-DECISIONS.md`.

## Herencia

`core/` (piso común) → `BRAND.md` (manifiesto: qué hereda, qué sobreescribe) →
`config/` (valores duros) → `docs/` (explicación).
**Inviolable:** ninguna marca relaja `core/docs/privacy/`; solo puede ser más estricta.
**Promoción:** si tres marcas documentan la misma regla, sube a `core/`.

## Clasificación obligatoria — alcance y estado

Todo conocimiento declara ambos en su frontmatter. Sin ellos, no se guarda.

**Alcance:** `GLOBAL` · `BRAND` · `PROGRAM` · `CAMPAIGN` · `PIECE` · `EXPERIMENTAL` · `DEPRECATED`
**Estado:** `APPROVED` · `DRAFT` · `PENDING VERIFICATION` · `EXPERIMENTAL` · `DEPRECATED` · `ARCHIVED`

> Una aprobación puntual **no** se convierte automáticamente en regla global.
> Subir de alcance es una decisión explícita (comando `PROMUEVE`), nunca una inercia.

## Identidad — reglas duras

- Paleta dura: HEX exactos de `config/brand/colors.json`. Nunca "un color parecido".
- Tipografía: el archivo real desde `assets/brand/fonts/`, no una sustituta.
- Logo: se **inserta** el archivo oficial. No se reconstruye con texto, no se deforma,
  no se reproporciona, no se genera con IA.
- Exploraciones de identidad = `EXPERIMENTAL`.

## Dirección de arte — regla transversal

**Usar IA como herramienta, nunca como estética.** Toda pieza debe sentirse dirigida por
un diseñador senior humano: concepto concreto, **una** idea dominante, jerarquía editorial,
aire, fotografía natural, montaje plausible.

Evitar por defecto: piel plástica, rostros genéricos, glow/neón, gradientes AI-tech,
fondos sci-fi sin concepto, UI flotante, objetos 3D gratuitos, simetría automática,
layouts de plantilla.

**Test de identidad:** si la pieza sirve para un competidor cambiando solo el logo,
falta dirección de arte. Se rehace.

## Edición quirúrgica

Instrucción puntual ("quita el CTA", "cambia solo el rostro") = modificar **solo lo pedido**.
Todo lo no mencionado queda **bloqueado**, salvo imposibilidad física evidente.
Una corrección puntual no autoriza rediseñar una pieza aprobada.

## Montaje, fisonomía y perspectiva

Conservar fisonomía si se pide (identidad facial, edad aparente, estructura). Integrar
sujetos respetando escala, lente, punto de fuga, luz, temperatura, profundidad, oclusiones
y sombras de contacto. Sin halos de recorte. Pantallas con perspectiva; la UI vive dentro
del display. Espacio negativo reservado **desde** la composición.

## Comunicación y datos

Identificar siempre: programa, audiencia, objetivo, canal, CTA, y qué dato es estable vs.
temporal. **No inventar** edades, precios, fechas, horarios, sedes, cupos, promociones,
métricas ni testimonios. Dato sin fuente vigente = `PENDING VERIFICATION`, no una estimación.
No prometer resultados garantizados. No usar culpa ni miedo. Sin urgencia falsa.

## Seguridad, privacidad y activos — piso inviolable

- Jamás versionar secretos, credenciales, cookies, sesiones, claves, `.env` reales.
- Fotos/videos de **menores** = material sensible: autorización escrita del representante,
  con alcance y vigencia, **antes** de versionar. Sin datos identificables de menores en
  piezas públicas.
- **Regla de disociación:** si una pieza sensible enseña una composición útil, se persiste
  el **patrón** (composición, crop, luz, prompt, restricciones, jerarquía) y **no** el
  archivo. El aprendizaje se guarda; el material sensible no.
- Terceros: nada sin licencia comprobable, registrada junto al archivo.
- Clasificar todo activo: `PUBLIC` · `INTERNAL` · `LICENSED` · `RESTRICTED`.
- `assets/inbox/` es cuarentena: estar ahí no hace oficial ni publicable nada.

## Archivos y Git

`lowercase-kebab-case` · conservar editables útiles · nada de `final-final` ni backups ZIP ·
antes de editar: status/remote/branch · antes de publicar: diff + secretos + licencias +
privacidad · prohibido force-push, `reset --hard` y limpiezas destructivas ·
**sin commit/push no autorizado** (única excepción: `GUARDA`) · binarios pesados → Git LFS ·
commits `<tipo>(<marca|core|skill>): <qué>`.

## Memoria

Aprendizajes repetibles → documentación, prompts y ejemplos curados. **Nunca** transcripciones
de chat. Filtro: *¿esto permitirá que otra persona —u otro agente— trabaje mejor en el
futuro?* Si no, fuera del repositorio.

## Contrato del agente

**Puede sin preguntar:** leer fuentes canónicas; producir piezas/copy/prompts siguiendo el
orden de lectura; auditar (`REVISA`); proponer mejoras como `DRAFT`.
**No puede sin autorización:** modificar `core/docs/privacy/` ni `config/brand/`; borrar
material `APPROVED` (solo `DEPRECATED`); dar de alta marcas; promover alcances; commit/push
(salvo `GUARDA`); inventar datos comerciales.
**Estilo:** idioma del usuario, directo, sin preámbulos; entregables listos; si falta un
dato canónico, **una** pregunta concreta y avanzar marcando `PENDING VERIFICATION`.
**Cierre:** qué se modificó · qué se validó · qué se publicó · qué quedó pendiente.

## Condición de entrega

1. `scripts/validate.sh` (o `.ps1`)
2. Revisar a tamaño real **y** reducido a móvil
3. Confirmar identidad, legibilidad, CTA, perspectiva, montaje, licencias, privacidad, datos
4. `design-qa-checklist.md` cuando aplique
5. Si se ve "hecho por IA" → corregir antes de entregar
6. Actualizar memoria solo si hay conocimiento estable
7. Reportar con precisión

---

# COMANDOS PERSISTENTES

## `GUARDA` — persistir en Git, no recordar en el chat

Cuando el usuario diga **"guarda" / "guárdalo" / "guarda esto"** sobre algo **aprobado**
(diseño, prompt, montaje, carrusel, copy, regla, decisión), es autorización explícita para
persistirlo en el repositorio canónico y publicarlo.

Flujo obligatorio:
1. Resolver `MARCA_ACTIVA`.
2. Identificar exactamente qué fue aprobado.
3. Revisar la versión vigente del repo y hacer *match* con lo existente.
4. **Complementar, no duplicar.**
5. Clasificar alcance y estado.
6. Elegir la representación correcta:
   regla/decisión → `docs/` · valor duro → `config/` · prompt → `prompts/` ·
   patrón de montaje → `COMPOSITION-AND-MONTAGE.md` · ejemplo → `examples/` ·
   asset real → `assets/` **solo** si licencia/privacidad/consentimiento lo permiten.
7. Menores o material sensible → **regla de disociación** (guardar el patrón, no el archivo).
8. Verificar que no entren secretos ni material sin permiso.
9. `scripts/validate.sh`.
10. Commit + push a la rama canónica.
11. **Releer el remoto y verificar el hash publicado** antes de afirmar "guardado".

Regla de precisión: no decir "guardado en Git" sin verificar el commit remoto. Si no hay
acceso de escritura o el remoto falla: decirlo explícitamente; nunca sustituir en silencio
la persistencia por memoria de conversación.

Objetivo: que una aprobación hecha desde escritorio, móvil u otro chat quede disponible
para cualquier agente futuro. Git es la memoria compartida; todo agente revisa el repo
antes de trabajar.

| El usuario dice | El agente persiste |
|---|---|
| "Este diseño quedó perfecto, guarda" | composición + prompt + decisión; el asset solo si es seguro |
| "Este prompt funcionó, guarda" | lo integra en `prompts/` tras hacer match |
| "Así debe ir siempre X, guarda" | promueve la regla al alcance correcto y la documenta |
| "Guarda este carrusel de referencia" | secuencia, narrativa, composición y restricciones |

## `REVISA`
Auditar una pieza o documento contra las fuentes canónicas **sin modificarlo**. Devuelve:
qué cumple, qué falla, qué está `PENDING VERIFICATION` y qué archivo canónico resuelve
cada duda.

## `PROMUEVE`
Subir de alcance un aprendizaje (`PIECE`→`BRAND`, `BRAND`→`GLOBAL`). Requiere justificación
y entrada en `DESIGN-DECISIONS.md`. Nunca automático.

## `NUEVA MARCA <slug> <PREFIJO> "<Nombre>"`
1. Verificar en `_REGISTRO-DE-MARCAS.md` que el prefijo no esté usado ni retirado.
2. Copiar la estructura de marca (Fase 2) a `brands/<slug>/` y sembrar slug/prefijo/nombre.
3. Correr la **Tanda B** de la entrevista para esa marca.
4. Añadir la fila al registro + entrada en `DESIGN-DECISIONS.md`.
5. Recordar: la marca no produce contenido hasta completar su checklist de activación.

## `INSTALA`
Re-ejecutar el protocolo de arranque (útil si la instalación quedó a medias).

---

# VALIDADOR

Genera `scripts/validate.sh` con estos chequeos (y un `.ps1` equivalente). Falla con error
si algo no cumple:

1. **Estructura global:** existen `AGENTS.md`, `00-inicio.md`, `README.md`, `CHANGELOG.md`,
   `CONTRIBUTING.md`, `.gitignore`, `.gitattributes`, `.env.example`,
   `core/_REGISTRO-DE-MARCAS.md`, `core/docs/ai/OPERATIONAL-COMMANDS.md`,
   `core/docs/standards/{SOURCE-PRIORITY,SCOPES-AND-STATES,NAMING-AND-GIT}.md`,
   `core/docs/privacy/{CHILD-SAFETY,MEDIA-USAGE,THIRD-PARTY-ASSETS}.md`,
   `vault/{01-mapa-del-proyecto,03-memoria-operativa}.md`.
2. **Por marca** (todas las carpetas de `brands/` excepto plantillas): existen `BRAND.md`,
   los 6 JSON de `config/`, `docs/ai/PROJECT-MEMORY.md`,
   `docs/brand/{BRAND-SYSTEM,COLORS,TYPOGRAPHY,LOGO-USAGE}.md`,
   `docs/content/{VOICE-AND-TONE,AUDIENCES}.md`; la marca aparece en el registro;
   los JSON parsean; si `colors.json` está `APPROVED`, no contiene HEX placeholder.
3. **Skills:** cada carpeta de `.agents/skills/` tiene `SKILL.md` con frontmatter `name:`
   y `agents/openai.yaml`.
4. **LFS:** `.gitattributes` cubre `pptx psd ai mp4 mov`.
5. **Secretos:** no existen `.env`, `*.pem`, `*.key`, `*.p12`, `*.pfx` en el árbol.
6. **Whitespace:** `git diff --check` limpio.

Instala también un hook `pre-commit` que ejecute el validador (`scripts/setup.sh`).

---

# CIERRE DE LA INSTALACIÓN (guion del agente)

Al terminar, reporta exactamente:

1. **Creado:** árbol generado (resumen por carpeta, no archivo por archivo).
2. **Sembrado:** qué respuestas de la entrevista quedaron en qué archivos.
3. **Pendiente:** lista `PENDING VERIFICATION` (HEX reales, logos, fuentes, muestra de voz
   aprobada, datos comerciales).
4. **Próximos 3 pasos del usuario.**
5. Frase final: *"El sistema está operando. Di `GUARDA` cuando algo quede aprobado,
   `REVISA` para auditar, `NUEVA MARCA` para crecer. Yo leo el repositorio antes de cada
   tarea: el repo es la memoria, no este chat."*
