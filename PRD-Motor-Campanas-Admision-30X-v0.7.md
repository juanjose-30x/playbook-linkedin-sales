# PRD — Motor de Campañas de Admisión · 30X

**Estado:** Borrador v0.7 (feature NUEVO dentro del producto + canal email Y WhatsApp + Emma Closer y llamatón en desarrollo paralelo — LISTO PARA CURSAR) · **Autor/DRI (Owner de TODO):** Juan José Sarmiento (Vertical de Ventas) · **Fecha:** 2026-09-30

**Novedades v0.7:** (1) **Checkout: NO es una pieza pendiente** — los checkouts **ya están construidos por Tech** (Oracle30x/Stripe, `30x.com/checkout/linkedin`); sale Mariana Cerón del RACI, solo se integra. (2) **Llamatón = MANUAL por ahora** (equipo humano de admisiones) **mientras se desarrollan los agentes paralelos** (Agente de calls Emma de Juan Ortega); pasa al agente cuando esté listo. (3) **LinkedIn se vuelve campo OBLIGATORIO en LinkedIn Sales** → se enriquece el **100%** de las aplicaciones. (4) **Apify recalculado como costo RECURRENTE sobre el volumen total** (no un gasto único): a volumen actual de LinkedIn Sales (~1.100–1.600 apps/mes) ≈ **$340–$490/mes** (≈ $4–6k/año) — ver §3.5.3. (5) **JJ involucrado y dueño en TODOS los pasos.**

**Marco (v0.6):** este feature es una **versión 30X del flujo de admisión de Growth Rockstar** (cuya conversión real **validada es ~18%**) construida **con nuestras herramientas**. **Empezamos por desarrollo de producto** (no hay mailing externo). Aprovechamos la **mayor contactabilidad vía WhatsApp** y la **infra Emma**: **Emma Closer** (agente de closing por WhatsApp) y **Agente de calls Emma** (motor del llamatón de voz). El flujo es **aditivo**: automatiza admisión + cobro **sin tocar ni canibalizar** el pipeline actual de los closers, que hoy da buenos resultados con la **agenda calificada** (ver §2/§5/§9).
**Datos clave confirmados (Slack):** reserva = **$200** · precio LinkedIn Sales en checkout = **$1,950** (lista) / **$1.755** con 10% de dto (pago completo, opción destacada) · el **checkout YA existe** (Oracle30x sobre Stripe) · meta = **acercar nuestra conversión aplicación→pago hacia el ~18% de GR** (conversión real **validada** de Growth Rockstar), midiendo el **baseline propio** (M1). El **~3%** de 30X (lead→venta global) es de otro denominador; ver §2.4.
**Decisiones v0.4 (lo primero):** el motor de secuencias/touchpoints es un **feature NUEVO a construir DENTRO del producto** — el **módulo de "campañas" actual NO está hecho para secuencias de admisión** y **ya NO hay plataforma de mailing externa**; el motor vive en el producto, no en una herramienta externa · canal = **email Y WhatsApp** (cada touchpoint por ambos a la vez) · por **email** el toque de admisión cae en una **landing estilo VSL con video de felicitación por ser admitido** + link al checkout (reserva $200); por **WhatsApp** va el **link directo** · **Emma Closer** (WhatsApp, sobre rieles Kapso/Treble, handoff a closer humano) y **Agente de calls Emma** (Juan Ortega) van en **desarrollo paralelo** · **llamatón el propio viernes** (día de cierre) para recuperar calificados/admitidos que no pagaron: por ser IA (Agente de calls Emma) puede correr el mismo viernes; en etapa inicial lo hace una persona.
**Novedades v0.5 (alineación con el playbook):** (1) **RACI explícito** — **JJ es Owner/DRI de TODAS las piezas**; los demás son **apoyo** (Tech/Beto+Emmy, Diseño+Maca Celis, Mariana Cerón, Juan Ortega, Apelis, Emmy); ver §0.1. (2) **Orden y dependencias** del lanzamiento (qué destraba qué) en §10. (3) **Checkout con dos opciones:** **pago completo con 10% de dto = $1.755** (opción destacada, para incentivar el pago completo y no vivir persiguiendo reservas — menos cobranza) o **reserva de $200** (red de seguridad). (4) **Cadencia de touchpoints DEFINIDA** por JJ (6 toques email+WhatsApp de "aplicó" al viernes de cierre; queda pulir copy fino) — §8. (5) **Dato real de Apify** para el ROI: 952 perfiles del pipeline "Ventas con LinkedIn" ≈ **$295 una sola vez** (§3.5). (6) **Llamatón** = llevar a pago o agendar reunión con el equipo comercial, presentado al lead como **"equipo de admisiones"**.

**Piloto de lanzamiento:** programa de **Ventas con LinkedIn** (el "programa de…", el VSL y el copy se instancian para LinkedIn Sales).
**Benchmark de flujo:** **Growth Rockstar** — aplicación → revisión de perfil (LinkedIn) → admisión → reserva con anticipo (ver **Apéndice A**).
**Cómo se construyó este borrador:** 5 partes redactadas en paralelo y auditadas por agentes independientes contra el referente (PRD nivel Stripe/Linear + Guía de PRD de 30X + Metodología de ROI de 30X). Puntajes vs referente: TL;DR/Problema 93 · Objetivos+ROI 93 · Usuarios+Alcance 93 · Requisitos 92 · Diseño+Lanzamiento 95. Todo número duro está marcado como `[SUPUESTO]` o en Preguntas abiertas; nada inventado.

> Gobernanza 30X: un PRD lo cursan Danilo, Alejandra, Dilan o Andrés (o sus delegados). Este borrador se prepara para cursarlo a través de uno de ellos.

> **Nota de audiencia (v0.5):** este **PRD** se cursa por la vía de gobernanza (**Danilo / Alejandra / Dilan / Andrés**). El **playbook ejecutivo** que acompaña esta iniciativa tiene otra audiencia: es para **Dylan y Andrés**. Son dos documentos con destinatarios distintos.

---

## 0. Estado actual — lo que YA existe vs. el delta a construir
*(Fuente: revisión de Slack, sep-2026 — detalle en `HALLAZGOS-SLACK.md`.)*

**⚠️ Es un feature NUEVO a construir DENTRO del producto (esto es lo primero).** El **motor de secuencias/touchpoints de admisión vive en el producto**, no en una herramienta externa: **ya NO hay plataforma de mailing externa**, y el **módulo de "campañas" actual del producto NO está hecho para secuencias de admisión** (hay que construir el motor, no reutilizar ese módulo). Dicho esto, el feature **no arranca de cero en todo**: varias **piezas de apoyo ya existen y se reusan** (checkout Oracle30x/Stripe, Apify, scoring, el checkout con VSL). Este PRD distingue qué se **construye nuevo** (el motor de secuencias, el envío multicanal, la landing VSL con video, la integración con el Emma Closer y el llamatón) de lo que se **reusa**.

**Dueños ya asignados** (contexto histórico, DM JJ → Juan Rueda, 19-ago): **Mariana Cerón** (checkout automático) · **Juan Ortega + Emmy** (ajustar formulario + usar LinkedIn en el mensaje personalizado; filtrar por "potencial de viralidad" para que se sienta exclusivo). JJ: *"Emmy ya había montado esto."* → **Validar con Emmy antes de construir.** *(La cadencia/copy, que antes se pensaba en Cristina, la **define ahora JJ** — ver RACI §0.1.)*

### 0.1 RACI — Dueño y apoyos (fuente de verdad de responsabilidades)

**Owner / DRI de TODO = Juan José Sarmiento.** JJ es **dueño de todas las piezas** del feature; los demás roles son **APOYO** sobre una pieza concreta. Su entregable para destrabar el build es **pasar este PRD a Tech**.

| Pieza | Dueño (DRI) | Apoyo | Nota |
|---|---|---|---|
| **PRD y dirección del feature** | **JJ** | — | Owner de todo; los demás apoyan piezas. |
| **Motor de secuencias en el producto** | **JJ** | **Tech (Beto + Emmy)** | Entregable de JJ para ellos: **pasar este PRD**. Es el bloqueante/cimiento (§10). |
| **Cadencia y copy de los touchpoints** | **JJ (define)** | — | La **cadencia ya está definida** por JJ (§8); queda pulir el copy fino con Ventas/Marca. |
| **Personalización (Apify + formulario)** | **JJ** | **Tech / Emmy** | Emmy ya montó un servicio parecido antes → validar con Emmy. |
| **Emma Closer (EN DESARROLLO)** | **JJ** | **Emmy** | Por ahora vía el **connector** (producto de **Emmy**); es dependencia en desarrollo. |
| **Landing VSL** | **JJ** | **Diseño + Maca Celis** | Maca conoce las secuencias de VSL. |
| **Checkout + reserva** | **JJ** | **Tech (YA construido)** | **Los checkouts YA están hechos por Tech** (Oracle30x/Stripe, `30x.com/checkout/linkedin` + variante `-discount`). **No es una pieza pendiente ni de Mariana**: solo se integra al flujo. |
| **Llamatón de cierre** | **JJ** | **Juan Ortega (agente en desarrollo)** | **AHORA = MANUAL** (equipo humano de admisiones) **mientras los agentes paralelos se desarrollan**. El **Agente de calls Emma** (Juan Ortega) lo automatiza cuando esté listo. |
| **Métricas y dashboard** | **JJ** | **Apelis** | Medir la conversión aplicación→pago vs. baseline propio, acercándola al **~18% de GR (validado)** — §2.4. |

### 0.2 Estado y línea de tiempo (al 30-sep-2026)

**JJ es dueño/involucrado en todo.** Foto de hoy:
- **PRD:** **listo** (esta v0.6). **En espera de revisión con Tech (Beto + Emmy)** — el entregable de JJ que destraba el build es **pasarles el PRD** (§10.0, paso 0).
- **Copys de los touchpoints:** la **cadencia está definida** (§8); los **copys están en revisión** (pulido fino).
- **Landing VSL:** **en curso con Maca Celis + Diseño**; **mañana 1-oct JJ graba el video** de felicitación de la landing.
- **Checkout:** ya existe (Mariana Cerón); se integra al motor con las dos opciones ($1.755 destacado / $200).
- **Emma Closer (WhatsApp):** interino vía **connector de Emmy**; agente en desarrollo.
- **Llamatón:** Agente de calls Emma de Juan Ortega en construcción; en etapa inicial lo hace una persona.

**Lo que YA existe (reusar, no construir):**
- **Checkout end-to-end sobre Stripe:** LinkedIn Sales en `https://30x.com/checkout/linkedin` (+ variante `-discount` con 10%), capa **Oracle30x** / `checkout.30x.com` (proxy reverso bajo el dominio 30x.com), admin en `checkout.30x.com/admin`. **Reserva = $200. Precio LinkedIn Sales = $1,950.**
- **El "flow" ya se pilotó** (Sales Machine, `form.oracle30x.co`): formulario → agenda, o checkout con 10% de descuento si se omite el agendamiento. Falta **instanciarlo a LinkedIn Sales**.
- **Scraping de LinkedIn con Apify** ya en producción en el Hub (~**$0.31/perfil**; research agent genera bio/motivación/valor). Cuenta `marketing@30x.com` conectada a Claude.
- **Scoring de admisión** ya existe (formulario salesFlow: rol + investment_capacity + urgency → tag Low/Med/High → HubSpot). Calendly con **3 event types de admisiones** (Sales Machine, AI Sales, **LinkedIn Sales**).
- **Rieles de mensajería de Emma (Kapso/Treble)** sobre los que correrá el **Emma Closer en WhatsApp** — pero ese agente **NO es un riel ya listo: está en desarrollo paralelo** (ver delta abajo). **Auto-checkout con Dapta** cuando califica OK (se integra).

**El delta REAL a construir (lo que este PRD prioriza):**
1. **Construir el motor de secuencias/touchpoints de admisión DENTRO del producto** — el módulo de "campañas" actual NO sirve para esto y no hay mailing externo. Es el corazón nuevo del feature (scheduling, estados, cortes pagó/opt-out/STOP).
2. **Envío multicanal email Y WhatsApp**: cada touchpoint sale por los dos canales. Por **email**, el toque de admisión cae en una **landing estilo VSL con video de felicitación por ser admitido** + link al **checkout** (reserva $200); por **WhatsApp** va el **link directo** al checkout.
3. Instanciar la narrativa a **LinkedIn Sales** encadenando los **5–6 touchpoints** (TP1 recibimos → TP2 revisando humano → TP3 ¡admitido! personalizado con Apify/LinkedIn → TP4–6 urgencia "hasta el viernes").
4. **Personalización real del TP3** (Apify + formulario) con el criterio de **exclusividad/viralidad** de JJ, y **firma humana** en los mensajes.
5. **Integrar el Emma Closer en WhatsApp — en desarrollo paralelo** (sobre rieles Kapso/Treble; hace **handoff a un closer humano**). Es **dependencia**, no un riel listo.
6. **Llamatón el propio viernes** (día de cierre): fase de recuperación de **calificados/admitidos que aún no pagaron**, conducida por el **Agente de calls Emma de Juan Ortega** (en construcción) — por ser IA puede correr el mismo viernes (Growth Rockstar lo hace la semana siguiente); en la etapa inicial la hace una **persona** y luego pasa al agente.
7. **Arreglar el desfase de precio** (landing `30x.com/linkedin-sales` muestra $1,500 vs checkout $1,950; fallback `_tbd` a $1,650 por `start_date_30x` faltante).
8. **Kill-switch, consentimiento del scraping y medición por touchpoint.**

**Problema y meta (d@30x, 18-sep):** el embudo de 30X convierte **~3%** y **Growth Rockstar llega a ~18%**. ✅ **El ~18% es la conversión real VALIDADA de Growth Rockstar** (referencia de GR confirmada). El objetivo formal del feature es **acercar nuestra conversión aplicación→pago hacia ese ~18% de GR**, midiendo un **baseline propio** (M1). ⚠️ Ojo con el denominador: el **~3% de 30X es lead→venta global**, distinto del que mide este feature (aplicación→pago del cupo); por eso el ~18% de GR es la **referencia/meta direccional** y el baseline específico de aplicación→pago **se mide propio**. *(Las magnitudes duras —aplicaciones/semana, baseline propio de aplicación→pago— siguen pendientes de confirmar.)*

---


# PRD · Campañas de Admisión: del "aplicó" al "pagó el cupo"

**Motor de touchpoints automatizado para convertir aplicantes admitidos en cupos pagados**

| Campo | Detalle |
|---|---|
| **Título de la iniciativa** | Campañas de Admisión — flujo automatizado de touchpoints que lleva a quien aplica hasta el pago del cupo |
| **Autor / DRI** | Juan José Sarmiento |
| **Equipo** | Vertical de Ventas — 30X |
| **Fecha** | 2026-09-30 |
| **Estado** | Borrador v0.6 |
| **Aprobadores / Quién lo cursa** | En 30X un PRD solo lo cursan **Danilo, Alejandra, Dilan o Andrés** (o sus delegados). **Next step:** el DRI (JJ) lleva este borrador a los cuatro para que definan quién lo cursa — **fecha límite: `[PLACEHOLDER — fijar, sugerido: 1 semana desde hoy]`**. Hasta entonces, aprobador asignado = pendiente. |
| **Stakeholders** | Vertical de Ventas (closers/owners de admisión), Growth/Pauta (origen de aplicantes), Producto/Plataforma (app de campañas y lead magnets), Finanzas (checkout, conciliación de pagos) |

**Enlaces** (marcados como placeholders):
- Guía de PRD de 30X — `[PLACEHOLDER]`
- Metodología de Priorización y ROI de 30X — `[PLACEHOLDER]`
- Flujo borrador de touchpoints (JJ) — `[PLACEHOLDER]`
- App de campañas / lead magnets — `[PLACEHOLDER]`
- Tablero de embudo aplicación→pago — `[PLACEHOLDER]`

---

## 1. Resumen ejecutivo (TL;DR)

- **Qué:** un **motor automatizado de touchpoints NUEVO, construido dentro del producto de 30X** (el módulo de "campañas" actual no sirve para secuencias de admisión y ya no hay plataforma de mailing externa), con narrativa de "admisión a un programa" — desde que alguien **aplica** hasta que **paga el cupo**. Envío **multicanal (email Y WhatsApp)**: por email el toque de admisión cae en una **landing estilo VSL con video de felicitación**; por WhatsApp va el **link directo** al checkout.
- **Para quién:** los **aplicantes admitidos** que hoy quedan en un seguimiento manual e inconsistente, y el **equipo de ventas** que hoy los persigue a mano.
- **Por qué ahora:** la fuga entre "aplicó" y "pagó" es CAC ya gastado que se pierde; cerrarla no exige atraer más leads, solo convertir los que ya tenemos — y el seguimiento manual no escala.
- **Con qué se apoya y qué va en paralelo:** el **checkout Oracle30x/Stripe ya existe** con **dos opciones (pago completo con 10% de dto = $1.755, destacado / reserva $200)**. En **desarrollo simultáneo** van el **Emma Closer** (WhatsApp; interino vía **connector de Emmy**; handoff a closer humano) y el **Agente de calls Emma** (Juan Ortega), que habilita un **llamatón el propio viernes** para recuperar admitidos que no pagaron —llevándolos a pago o agendando con el "equipo de admisiones"— (en etapa inicial lo hace una persona).
- **Resultado esperado:** más cupos pagados por cada 100 aplicaciones, con seguimiento consistente y medible touchpoint a touchpoint, sin sumar carga manual.

*(Las cifras del embudo van marcadas como supuestos a validar; no condicionan la definición del problema.)*

---

## 2. Contexto y problema

### 2.1 El problema: la fuga entre "aplicó" y "pagó el cupo"

30X ya invierte en atraer leads y llevarlos a **aplicar** por formularios en la app de campañas. El dolor **no es conseguir aplicaciones: es que una parte de quienes aplican —incluso los admitidos— nunca completan el pago del cupo.** Esta es la fuga más cara del embudo, porque ocurre **después** de haber pagado por atraer y calificar al lead: **cada aplicante admitido que no paga es CAC ya gastado sin ingreso, y un cupo vacío.**

Entre el "aplicó" y el "pagó" hay un vacío operativo:

- **El seguimiento es manual e inconsistente.** Depende de que alguien se acuerde, tenga tiempo y escriba el mensaje correcto en el momento correcto. En picos o fuera de horario, el aplicante se enfría antes de recibir respuesta.
- **No hay narrativa de admisión sostenida.** El momento de mayor intención —recién aplicó— se desaprovecha. La persona espera una señal de que "entró"; si no llega pronto y personal, la aplicación se siente como un formulario más, no como una admisión a un programa.
- **La urgencia no se comunica de forma confiable.** Sin recordatorios estructurados con fecha límite real, el aplicante posterga; "lo hago después" se vuelve "no lo hice".
- **No se mide dónde se cae la gente.** Al ser manual, no hay trazabilidad por contacto. No se puede arreglar lo que no se mide.

**Desde el usuario (el aplicante):** aplicó, sintió intención, y luego silencio o mensajes genéricos a destiempo. No sabe si quedó, qué sigue, ni por qué decidir hoy. La experiencia no está a la altura de la promesa de un "programa".

**Desde el negocio:** es donde se decide el retorno de todo el CAC, y hoy nadie lo dueña de forma automatizada.

> **No canibaliza el pipeline actual (v0.6).** Este flujo es **aditivo**: **no lastima ni reemplaza el pipeline actual de los closers**, que hoy **da buenos resultados con la agenda calificada**. El feature automatiza la **admisión + el cobro** de los aplicantes que hoy se pierden en el seguimiento manual —CAC ya gastado—, **sin tocar** el flujo humano de cierre sobre agenda calificada. Suma conversión donde hoy hay fuga; no le quita volumen ni leads a los closers. (Ver §5 alcance y §9 riesgos.)

> Este PRD describe **el problema**, no la solución. El flujo de JJ (confirmación → revisión → "fuiste admitido" personalizado → recordatorios hasta el viernes) es un **borrador a cuestionar**, no un requisito; se aborda en alcance y requisitos.

### 2.2 Por qué ahora

- El CAC ya está incurrido en cada aplicante; **recuperar tasa de pago no requiere atraer más leads**, solo cerrar la fuga sobre los que ya tenemos. Máximo apalancamiento sobre gasto existente.
- El seguimiento manual **no escala**: a más aplicaciones, peor consistencia y mayor fuga, justo cuando más importa.
- Ya existe el **producto (app de campañas / lead magnets)** como base y varias **piezas de apoyo** (checkout, Apify, scoring); pero el **módulo de "campañas" actual NO sirve para secuencias de admisión**: el **motor de touchpoints se construye nuevo dentro del producto**. El momento es hacerlo ahora, apoyándose en lo que ya existe.

### 2.3 Coste de no hacer nada

Si no se actúa, se mantiene y se agrava:

- **Ingreso perdido recurrente y creciente:** cupos vacíos y CAC quemado cada semana; la pérdida escala con el volumen de aplicaciones.
- **Techo de crecimiento manual:** el equipo sigue gastando horas en seguimiento repetitivo (capacidad que no se convierte en cierres) y la calidad se degrada en los picos.
- **Deterioro de la experiencia de "admisión":** silencios y mensajes genéricos contradicen la promesa de programa, dañando marca y referidos.
- **Ceguera de datos:** cada semana sin medición por touchpoint es una semana sin aprender dónde ni por qué se cae la gente.

Por su costo de operación y su impacto sobre ingreso, esta iniciativa **está por encima del "piso" de la metodología de 30X** (no es un cambio de <3 días): amerita PRD.

### 2.4 Cómo se dimensiona la fuga (fórmula + supuestos a validar)

No inventamos cifras, pero sí mostramos **cómo se calculará el tamaño de la fuga** una vez haya datos. La lógica:

```
Fuga mensual (COP/USD) = Aplicaciones/mes
                       × (% admitidos)
                       × (1 − % que paga hoy)
                       × Ticket del cupo
```

Interpretación: de todas las aplicaciones, las que serían admitidas y **no** pagan, multiplicadas por el ticket, son el ingreso que se pierde al mes. La palanca del feature es **subir el `% que paga`**; el valor recuperado ≈ `Aplicaciones/mes × (% admitidos) × (Δ % que paga) × Ticket`.

Variables a llenar (**placeholders — confirmar contra HubSpot / la app de campañas, no usar hasta validar**):

| Variable | Valor | Fuente / estado |
|---|---|---|
| Aplicaciones por mes | `[SUPUESTO a validar]` | App de campañas / HubSpot |
| % de aplicantes admitidos (¿todos o por score?) | `[SUPUESTO a validar]` | Depende de la lógica de admisión |
| % que hoy paga el cupo (línea base aplicación→pago) | `[SUPUESTO a validar]` — **denominador propio, distinto del 3% global** (ver nota de baseline abajo) | Medir línea base actual del embudo aplicación→pago |
| Ticket del cupo (LinkedIn Sales, piloto) | **$1,950** (ticket completo) · **$200** (reserva que asegura el cupo) — *confirmados en Slack (§0)* | Checkout Oracle30x/Stripe (`30x.com/checkout/linkedin`) |
| Δ % que paga esperado con el feature | `[SUPUESTO a validar]` | Meta a definir en Sección 3 |
| Ventana de decisión (aplicación → cierre "viernes") | `[SUPUESTO a validar]` — el borrador asume cierre semanal el viernes | Confirmar si es fecha fija o por cohorte |
| Distribución horaria de aplicaciones (temprano/tarde) | `[SUPUESTO a validar]` | Condiciona ventanas de envío |

> Todo número duro sobre tamaño de fuga o ROI se remite a **Sección 11 (Preguntas abiertas)** hasta que exista evidencia. Regla del proyecto: no se fabrican cifras; lo que no se sabe se marca como supuesto o pregunta abierta.

**Baseline de conversión (§0):** el embudo de 30X convierte hoy **~3%** y **Growth Rockstar llega a ~18%** (d@30x, 18-sep). ✅ **El ~18% es la conversión real VALIDADA de Growth Rockstar** — es la **referencia/meta direccional** hacia la que apuntamos. ⚠️ **Precisión de denominador:** ese **~3% es lead→venta global**, distinto del que mide este feature (**aplicación→pago del cupo**). Por eso **no** se usa el ~3% como el valor de la variable `% que hoy paga` de la fórmula de arriba: la meta formal es **acercar nuestra conversión aplicación→pago hacia el ~18% de GR**, y esa línea base específica **debe medirse propia** en la ventana de baseline de §3.6 (M1 pide su propio baseline). Así el documento fija una meta anclada en el dato validado de GR sin sobre-atribuir el ~3% a un denominador que no le corresponde.

**El checkout ofrece DOS opciones (v0.5):**
- **(a) Pago completo con 10% de descuento = $1.755** ($1.950 − 10%). **OPCIÓN DESTACADA** en el checkout. Se destaca a propósito para **incentivar el pago completo y no vivir persiguiendo reservas mínimas** — beneficio operativo directo: **menos cobranza** posterior.
- **(b) Reserva de $200** = alternativa / red de seguridad para quien aún no puede pagar todo, asegura el cupo antes del cierre (viernes). La **reserva de $200 NO es reembolsable** y así **se le comunica claramente al lead** antes de pagarla.

**Por qué destacamos el pago completo — comparación Growth Rockstar vs. 30X (v0.6):**
- **Reserva:** Growth Rockstar cobra **$95**; **30X cobra $200**. *(La cifra de GR es de referencia; el Apéndice A registró un depósito observado distinto — usar el valor confirmado.)*
- **GR no incentiva el pago completo** porque su **drop-off reserva→pago completo es ~5%** (bajo): casi todos los que reservan terminan pagando, así que no necesita empujar el completo.
- En **30X ese drop-off es más alto históricamente** (más gente reserva y luego no completa) → por eso **incentivamos el pago completo con el 10% de descuento (= $1.755)**: reduce la cola de cobranza y la fuga reserva→completo.
- El **saldo / pago completo se acuerda la semana previa al inicio** del programa (quien reservó completa antes de arrancar).

**Definición de resultado (unidad de las métricas de negocio, para todo el PRD):**
- **Cupo reservado** = el aplicante **pagó la reserva de $200 (no reembolsable)** que asegura el cupo antes del cierre (viernes). Es la conversión que el motor de touchpoints cierra **dentro de su ventana** por la vía de la red de seguridad.
- **Cupo pagado completo** = el aplicante **pagó el total: $1.755 (con el 10% de dto, opción destacada) o $1.950** (precio de lista sin descuento).
- **Cupo pagado válido** (**unidad ancla** de M2, del costo por resultado verificado en §3.5.3 y del denominador de conversión aplicación→pago) = **cupo asegurado con pago confirmado por webhook, no reembolsado ni en disputa** — sea por **reserva ($200)** o por **pago completo ($1.755 / $1.950)**. *(Se cuenta el cupo asegurado porque es el resultado que este feature produce y mide de forma limpia dentro del ciclo de admisión; el patrón "reserva con anticipo" es el mismo de Growth Rockstar — Apéndice A.)*
- **Recaudo (M3):** el **pago completo ($1.755 / $1.950)** alimenta más el recaudo que la reserva; el **saldo de quien reservó se acuerda/completa la semana previa al inicio** del programa. El monto cobrado **alimenta M3** pero **no** redefine el conteo de cupos. Esta convención se usa **consistentemente** en §3.


---


# 3. Objetivos y métricas + Caso de ROI 30X

> Parte 2 de 5 · DRI de negocio: —. Referente de forma: PRD Stripe/Linear. Referente de negocio: Metodología de Priorización y ROI de 30X.
> Convención de este documento: `[SUPUESTO]` = no hay dato aún, hay que medirlo; `[APUESTA]` = no se puede calcular sin datos reales, la autorizan los fundadores. **No hay cifras inventadas presentadas como hechos.**

---

## 3.1 Objetivos (en lenguaje humano, atados a líneas de negocio)

El feature existe para convertir una aplicación en un cupo pagado sin que un humano tenga que perseguir a cada lead. Cuatro objetivos, en orden de prioridad:

1. **Subir la conversión de aplicación → pago.** Hoy, entre que alguien llena el formulario y paga el cupo hay un vacío que se cubre a mano (o no se cubre). El feature convierte ese vacío en una secuencia de admisión personalizada y con urgencia real, para que un porcentaje mayor de aplicantes llegue al checkout y pague.
2. **Llenar más cupos pagados por campaña.** No solo mejor tasa: más cupos válidos ocupados por cohorte/programa, que es la unidad que le importa al negocio.
3. **Aumentar el recaudo del canal.** Más cupos pagados y menor fuga en el checkout se traducen en más dinero efectivamente cobrado por campaña, no en "pipeline".
4. **Bajar el trabajo manual de seguimiento.** Que el equipo comercial pase de escribir mensajes uno por uno a **supervisar una máquina** (revisar excepciones, no operar la rutina). Ojo con la lectura de este objetivo: por la metodología 30X, las horas liberadas son **capacidad, no retorno** — no cuentan como plata hasta que se reasignan a producción pagada o se recorta costo real. Ver §3.7.

Alineación con líneas de negocio: (1)–(3) mueven **recaudo**; (4) mueve **margen de operación** (capacidad del equipo comercial).

---

## 3.2 Métricas de éxito (SMART)

Regla de honestidad: **hoy no hay baseline medido** de la mayoría de estas métricas. Por eso los objetivos se expresan preferentemente como **delta sobre el baseline** (un delta es SMART aunque no conozcamos el punto de partida) y los valores absolutos van marcados como `[APUESTA]`. Antes de fijar metas absolutas se corre una **ventana de baseline de 2 semanas** (ver §3.6, dependencia dura).

| # | Métrica | Valor base | Objetivo | Plazo |
|---|---------|-----------|----------|-------|
| M1 | **Conversión aplicación → cupo pagado válido** (aplicantes que aseguran el cupo —reserva o pago completo— ÷ aplicantes que entran al flujo; "cupo pagado válido" definido en §2.4) | `[SUPUESTO]` — **medir baseline propio de 2 sem.** El **~3% de §0 es lead→venta global (otro denominador)**, sirve de ancla direccional, **no** como baseline de esta métrica. | **+3 pp** sobre baseline propio, **apuntando a acercarse al ~18% de GR (conversión real validada de Growth Rockstar, §2.4)**; el valor absoluto objetivo intermedio es `[APUESTA]` | 60 días post-GA |
| M2 | **Cupos pagados válidos por campaña** (pagados y no reembolsados ni en disputa) | `[SUPUESTO]` — por cohorte actual | **+15%** vs. campaña comparable previa | 2 campañas / 60 días |
| M3 | **Recaudo cobrado atribuible al flujo** (checkout del feature, neto de reembolsos; **pagos completos $1.755/$1.950** + reservas de **$200** con sus saldos posteriores) | $0 (feature nuevo) | Umbral de éxito mínimo `[APUESTA]` a definir con fundadores; medir $ real. Precios ya fijados (§2.4: $1.950 lista / $1.755 con dto / $200 reserva); lo `[APUESTA]` es la meta de $, no el precio. | 90 días post-GA |
| M4 | **Tiempo mediano aplicación → pago** | `[SUPUESTO]` — hoy depende de seguimiento manual | **≤ 48 h** en la mediana | 60 días post-GA |
| M5 | **% de aplicaciones con TP3 ("admitido") entregado dentro de SLA** (personalizado + validado) | 0% (no existe) | **≥ 95%** dentro de la ventana definida (§4/§7) | 30 días post-GA |
| M6 | **Tasa de finalización del checkout** (llega al checkout → paga) | `[SUPUESTO]` | **+5 pp** sobre baseline del checkout actual | 60 días post-GA |
| M7 | **Toques manuales por cupo pagado** (mensajes/acciones humanas por cupo) | `[SUPUESTO]` — hoy alto | Reducir a **≤ 1** (solo excepciones/QC) | 60 días post-GA |

Notas de las metas: las metas de M1/M2/M6 (los deltas) son las **ancla de decisión**; M3 es la meta de negocio pero su valor absoluto es `[APUESTA]` hasta tener baseline y precio de cupo confirmado. M7 mide el objetivo 4, pero cuenta como eficiencia operativa, no como retorno (§3.7).

---

## 3.3 Métricas de guarda (no deben empeorar)

El feature envía mensajes automáticos, personalizados con datos scrapeados, con narrativa de "fuiste admitido". El riesgo de daño de marca y de canal es real. Estas métricas tienen **umbral rojo**: si se cruzan, se pausa el envío automático (kill-switch, ver §4/§10).

| Métrica de guarda | Umbral rojo (pausar) | Fuente |
|---|---|---|
| **Tasa de quejas de spam (email)** | > 0.10% de envíos (estándar de industria; confirmar) `[SUPUESTO umbral]` | proveedor de email |
| **Tasa de bloqueo / reporte (WhatsApp)** | > `[SUPUESTO]` — fijar con baseline del canal | proveedor de WhatsApp |
| **Tasa de baja / unsubscribe por campaña** | Aumento sostenido vs. baseline `[SUPUESTO]` | motor de campañas |
| **Deliverability (inbox placement / hard bounce)** | Bounce > 2% o caída de inbox placement `[SUPUESTO]` | proveedor de email |
| **Tasa de reembolsos / disputas de pago** | > `[SUPUESTO]` — fijar con datos de checkout | proveedor de pago |
| **% de mensajes con error de personalización detectado en QC** | > 2% de la muestra revisada `[SUPUESTO umbral]` | cola de QC (§3.6 / §7) |
| **Percepción de "spam"** (encuesta corta post-flujo / respuestas negativas) | tendencia negativa `[SUPUESTO]` | encuesta + inbox de respuestas |

Regla: la personalización con IA + scraping **no puede** mejorarse a costa de estas guardas. El costo por resultado verificado (§3.7) está definido justo para que bajar la calidad no "mejore" el número.

---

## 3.4 No-objetivos (fuera del propósito de este feature)

- **No** es un proceso de admisión académica real: "admitido" es narrativa de campaña; no evalúa mérito ni excluye por nota. (Riesgo ético/legal → ver §3.7 costo del error y §9.)
- **No** optimiza retención ni upsell **después** del pago del cupo.
- **No** rediseña el CRM ni el pipeline comercial existente.
- **No** busca "ahorrar X horas" como fin en sí mismo (es capacidad, no retorno; §3.7).
- **No** persigue un ROI porcentual espectacular; la metodología 30X lo prohíbe como métrica de decisión (§3.7).
- **No** cubre canales fuera de los definidos: los canales de v1 son **email, WhatsApp y las llamadas del llamatón del viernes** (recuperación de admitidos que no pagaron); otros canales (p. ej. SMS, llamadas salientes fuera del llamatón) quedan fuera de v1.

---

## 3.5 Caso de ROI aplicando la Metodología 30X

### 3.5.1 Chequeo del piso — ¿por qué este feature está *arriba* del piso?

La regla del piso dice: si algo lleva **< 3 días** y no es caro ni cara-al-cliente, se hace y se avisa, sin PRD. Este feature **no** aplica a esa regla, por dos razones, ambas de la metodología:

1. **Tiene costo de operación mensual recurrente.** No es un build de 3 días: cada lead consume enrichment de formulario, **scraping de LinkedIn con Apify**, generación de mensaje con IA, mensajería (WhatsApp/email) y **revisión humana**. Eso es un costo que corre todos los meses, no una sola vez.
2. **Es cara al cliente (prospecto).** Un mensaje mal personalizado, "admitir" a quien no toca, o escribirle al contacto equivocado con datos scrapeados, deja mal a 30X frente a un prospecto y a su red. Daño de marca directo.

**Conclusión:** por (1) costo de operación mensual y (2) exposición al cliente, el feature exige PRD y el análisis de ROI completo de abajo. Confirmado que está sobre el piso.

### 3.5.2 Los 4 costos que nunca están en la planilla (aplicados a ESTE feature)

La construcción es solo el **25–35%** del costo a 3 años. El grueso está aquí:

**(1) Reintentos — una instrucción = decenas de llamadas.**
Generar el TP3 ("fuiste admitido", personalizado) no es una llamada: es una cadena con reintentos en cada eslabón.
- Apify/LinkedIn: perfiles no encontrados, homónimos, rate limits, captchas, perfiles privados → reintentos y fallbacks.
- LLM de redacción: reintentos por output que no pasa validación de formato/tono.
- Verificación de datos (empresa, rol) antes de escribir.
Costo unitario real = (llamadas Apify + tokens LLM + validaciones) × factor de reintento. **Nº de llamadas por lead = `[SUPUESTO]`** — hay que medirlo en piloto; es el principal driver del costo variable.

**(2) Revisión humana — lo caro no es el modelo, es revisar excepciones.**
Pregunta clave de la metodología: **¿quién revisa lo que sale y con qué muestreo?**
- **Quién:** un rol de "revisor de admisiones" (¿SDR? ¿un editor comercial? ¿el closer del programa?) — **a definir → pregunta abierta.**
- **Muestreo propuesto:** **100% de los TP3 revisados en el piloto** (es el mensaje de mayor riesgo: personalizado + scrapeado + dice "admitido"); luego **muestreo por bandas de confianza** — 100% cuando el enrichment vino de LinkedIn/tiene datos sensibles, muestreo n% cuando el mensaje usa solo respuestas del propio formulario. TP1/TP2/recordatorios: plantilla fija, revisión mínima.
- Este es el costo que **no baja** solo con más volumen si sigue siendo por-lead. Es el que define si el feature escala (§3.5.4).

**(3) Costo del error.**
- **Personalización equivocada** (cita empresa/rol/logro errado por mal match de Apify): el prospecto siente vigilancia o descuido → daño de marca, respuesta negativa.
- **Admitir a quien no toca:** llena la narrativa de "admisión" con gente no calificada, contamina la cohorte y erosiona el cupo como cosa escasa/deseable.
- **Contacto equivocado / dato sensible mal usado:** riesgo de privacidad (habeas data / consentimiento del scraping — ver §7 y §9), no solo de marca.
- **Efecto en canal:** errores → quejas de spam → cae deliverability → se quema el dominio/número (afecta *todas* las campañas, no solo esta).
Componentes de costo: retrabajo, disculpas, posible reembolso, rollback del envío, y el costo difuso de reputación. Por eso hay kill-switch y guardas (§3.3).

**(4) Cambio de proceso del equipo comercial.**
El equipo pasa de **perseguir leads a mano** a **supervisar una máquina**: leer colas de QC, aprobar/corregir TP3, atender excepciones, confiar en el scheduling automático. Requiere: nuevo rol/turno de revisión, SLA de aprobación (para no romper la ventana de urgencia hasta el viernes), y desaprender el hábito de escribir cada mensaje. Este costo es de adopción y es real aunque no aparezca en factura.

### 3.5.3 Las dos métricas que pide 30X (no un % de retorno)

> La metodología prohíbe usar "% de retorno" y "ahorra X horas" como beneficio. Se piden estas dos:

**A) Costo por resultado verificado** — la única métrica que **no** mejora bajando la calidad.

Dos denominadores, ambos "verificados" (pasaron QC / son válidos):

```
Costo por LEAD procesado correctamente
  = Costo total mensual de operar
  ÷ Nº de leads cuyo touchpoint personalizado pasó QC sin error

Costo por CUPO PAGADO VÁLIDO
  = Costo total mensual de operar
  ÷ Nº de cupos pagados que NO fueron reembolsados ni disputados
```

**Costo total mensual de operar** (stack de costos):
- Apify / scraping: **~$0.31 por perfil** (dato real, ya en producción en el Hub — §0/Slack) **× factor de reintento `[SUPUESTO]`** (el precio unitario ya no es supuesto; lo que falta medir es cuántas llamadas efectivas por lead genera con reintentos/fallbacks)
- Tokens de IA de personalización (por lead × factor de reintento)
- Mensajería (WhatsApp + email, por envío × Nº de touchpoints)
- **Revisión humana** (horas del revisor × costo/hora ÷ leads revisados) ← suele ser el rubro dominante
- Infra/scheduling (motor de campañas, colas)
- Amortización de la construcción (build repartido en la vida útil)

> **Dato real del enriquecimiento (v0.7 — costo RECURRENTE sobre volumen total, no un gasto único):** el precio unitario está validado en **~$0.31 por perfil enriquecido** (Apify scrape + research agent con 6 búsquedas web que genera bio/motivación/valor; cuenta `marketing@30x.com` ya en producción — Diego España, 29-sep). Como **LinkedIn pasa a ser campo OBLIGATORIO en LinkedIn Sales**, se enriquece el **100% de las aplicaciones**, así que Apify deja de ser un gasto único y pasa a ser **costo mensual recurrente = (aplicaciones/mes) × $0.31**.
>
> **Volumen real de LinkedIn Sales (HubSpot, pipeline 906259304, consultado 30-sep-2026):**
>
> | Mes | Aplicaciones | Costo Apify @ $0.31 |
> |---|---|---|
> | Jul-2026 | 951 | ≈ $295 |
> | Ago-2026 | 826 | ≈ $256 |
> | Sep-2026 | 1.583 | ≈ $491 |
>
> → **Run-rate del piloto: ~1.100–1.600 aplicaciones/mes → ≈ $340–$490/mes (≈ $4.100–$5.900/año).** Cifra de planeación: **~$400/mes**. *(Antes solo el 27–30% dejaba LinkedIn y la captura se cortó en agosto; volverlo obligatorio cierra ambos huecos y hace el volumen enriquecido = volumen de aplicaciones.)*
>
> **Si a futuro se extiende el flujo a los otros programas de ventas** (AI Sales ~1.600/mes + Sales Machine ~757/mes + B2B ~119/mes, cifras de sep): +~2.500 aplicaciones/mes → total **≈ $1.250/mes (≈ $15k/año)**. Enriquecer **toda** la operación (≈ 18–20k aplicaciones/mes de todos los programas) costaría **≈ $5.600/mes**, por lo que el enriquecimiento se aplica **solo a los programas con lógica de LinkedIn**, no a todo. *(Fuente: HubSpot; totales por pipeline y mes.)*
>
> Lo único que sigue `[SUPUESTO]` es el **factor de reintento por lead** (cuántas llamadas efectivas con reintentos/fallbacks), no el precio unitario ni el volumen.

> **Ejemplo ILUSTRATIVO — solo muestra la mecánica, NO es proyección ni meta.** Todos los números son placeholders `[APUESTA]`.
> Si en un mes el costo total de operar fuera $X y salieran 800 leads bien procesados (de 1.000) y 40 cupos pagados válidos → costo por lead verificado = $X/800; costo por cupo pagado válido = $X/40. **El valor real de $X y de los denominadores es una `[APUESTA]` hasta correr el piloto.** No fabricamos $X aquí.

**B) Período de repago.**

```
Período de repago (meses)
  = Inversión de construcción
  ÷ (Margen incremental mensual atribuible − Costo mensual de operar)
```
Donde *margen incremental atribuible* = (recaudo de cupos pagados **incrementales** atribuibles al feature) × margen del programa. **Todos los términos son `[SUPUESTO]`/`[APUESTA]`** hasta tener: (i) baseline de conversión, (ii) precio del cupo confirmado, (iii) costo de operar del piloto. **Por tanto, el período de repago concreto es hoy una `[APUESTA]` → la autorizan los fundadores.**

### 3.5.4 Regla de escalado

**Escalar volumen (más aplicaciones, más campañas simultáneas) SOLO si el *costo por resultado verificado* BAJA con el volumen.**

- Si al subir volumen la **revisión humana** sigue siendo por-lead y los **reintentos** de Apify/IA crecen linealmente, el costo por resultado verificado **no baja** → **no escalar**; primero automatizar QC (subir el % que se puede muestrear en vez de revisar 100%) y reducir el factor de reintento.
- **Disparador para escalar:** el costo por cupo pagado válido de este mes < el del mes anterior, **con** las métricas de guarda (§3.3) dentro de umbral. Si el costo baja pero suben quejas/errores, **no cuenta** (estaríamos "mejorando" el número degradando calidad).

### 3.5.5 Veredicto de ROI

Con la información disponible **hoy**, el retorno neto **no se puede calcular** (faltan baseline de conversión, precio de cupo confirmado y costo de operar del piloto). Por la propia metodología, eso lo convierte en una **APUESTA que deben autorizar los fundadores** (Danilo/Alejandra/Dilan/Andrés o delegados, que además son quienes pueden cursar el PRD). La apuesta es razonable —hay costo manual actual y fuga clara aplicación→pago— pero **no se debe presentar con un ROI% ni con "ahorra X horas".** El piloto existe precisamente para convertir la apuesta en las dos métricas de §3.5.3.

---

## 3.6 Instrumentación mínima requerida (dependencia de todo lo anterior)

Para que estas métricas existan (y no sean humo), el feature debe emitir, desde el día 1:
- Evento por lead: entró al flujo, TP enviado (cuál, canal, timestamp), enrichment usado (formulario / Apify / ninguno), resultado de QC (aprobado / corregido / rechazado).
- Evento de pago: checkout iniciado, pagado, reembolsado, disputado — con atribución al flujo.
- Cola de QC con estado y muestreo, para computar M5, la guarda de error, y el denominador "verificado" de §3.5.3.
- **Ventana de baseline de 2 semanas** antes de fijar metas absolutas (M1, M3, M6).

---

## 3.7 Nota sobre "horas ahorradas" (recordatorio de la metodología)

M7 (toques manuales por cupo) mide un objetivo real, pero **las horas liberadas son capacidad, no retorno.** Solo se vuelven plata si (a) esas horas se reasignan a producción pagada, o (b) se recorta costo real de nómina. Mientras no ocurra ninguna de las dos, se reporta como **capacidad liberada**, nunca como beneficio económico. Cualquier cálculo de ROI que sume "X horas × costo/hora" como retorno queda **prohibido** en este documento.


---


## 4. Usuarios y casos de uso

### 4.1 Personas

| # | Usuario | Rol respecto al feature | Qué necesita | Qué le duele hoy |
|---|---------|-------------------------|--------------|------------------|
| **P1 — primario** | **El aplicante** (persona que se inscribe por el formulario del lead magnet) | Destinatario de la campaña; el que decide y paga el cupo | Sentir que aplicó a algo real y selectivo, entender si "quedó", saber cuánto/cómo/hasta cuándo pagar, resolver dudas rápido | Los formularios de siempre no dan sensación de proceso; el seguimiento es genérico, tardío o inexistente; no sabe si es urgente ni por qué debería pagar ahora |
| **P2 — secundario** | **Revisor / quien hace push comercial** (p. ej. Felipe) | Supervisa la cola de aplicantes, aprueba/edita el "veredicto" de admisión, empuja casos de alto valor manualmente | Ver el estado de cada aplicante, confiar en que la personalización no dice ridiculeces, poder intervenir sin romper la automatización | Hoy no hay una cola única; el push es manual y no queda trazado; no se sabe qué touchpoint recibió cada quién |
| **P3 — secundario** | **Operador de la campaña** (marketing/growth que arma y mantiene el flujo) | Configura copies, ventanas horarias, canal, reglas de admisión y de urgencia; monitorea deliverability y métricas por touchpoint | Editar copy y tiempos sin depender de ingeniería, apagar la campaña rápido, ver dónde se cae el funnel | Cambios requieren código; no hay kill-switch; no hay medición por paso |
| **P4 — secundario (soporte)** | **Agente humano / closer** que atiende cuando el aplicante pide hablar con una persona | Recibir el contexto del aplicante (respuestas, touchpoint actual, estado de pago) y una señal de "esto necesita humano" | El aplicante escribe y nadie lo ve, o lo ve tarde y sin contexto | Los "quiero hablar con alguien" se pierden entre automatizaciones |

> **Supuesto (a validar):** "Felipe" es un rol de revisor/push, no necesariamente una sola persona. El PRD lo trata como rol. **Pregunta abierta:** ¿P2 y P4 son la misma persona en la operación actual?

> **Nota v0.4 (multicanal + agentes en paralelo):** cada touchpoint sale por **email Y WhatsApp**. El **Emma Closer** (WhatsApp, sobre rieles Kapso/Treble, **en desarrollo paralelo**) atiende la conversación entrante y hace **handoff a un closer humano (P4)**. El **llamatón del viernes** lo ejecuta el **Agente de calls Emma** (Juan Ortega, en construcción) o una **persona en la etapa inicial**.

### 4.2 Historias de usuario (por momento del flujo)

**Al aplicar (TP1)**
- Como **aplicante**, quiero una confirmación inmediata y cálida de que recibieron mi aplicación, para saber que el proceso empezó y no quedé en el vacío.
- Como **operador**, quiero que el TP1 se dispare en segundos tras el envío del formulario, para que la experiencia se sienta "en vivo".

**Mientras "revisan" (TP2)**
- Como **aplicante**, quiero un mensaje humano de "estamos revisando tu aplicación", para creer que hay un proceso real de selección detrás (y no un autoresponder).
- Como **revisor (P2)**, quiero ver en una cola quién está en estado "en revisión", para intervenir en los casos de alto valor antes del veredicto.

**Al ser admitido (TP3)**
- Como **aplicante**, quiero un "¡Fuiste admitido!" personalizado con lo que dije en el formulario y con mi contexto profesional, para sentir que la admisión es específica para mí y no un mensaje masivo.
- Como **aplicante**, quiero recibir la admisión por **email y por WhatsApp**: por **email**, una **landing estilo VSL con un video de felicitación por ser admitido** + link al checkout; por **WhatsApp**, el **link directo** al checkout — para decidir con toda la información y pagar sin fricción por el canal que prefiera.
- Como **revisor (P2)**, quiero poder aprobar, editar o retener el mensaje de admisión personalizado antes (o en vez) de que salga automático, para que nunca salga algo incorrecto a un lead valioso.
- Como **revisor (P2)**, quiero que mientras estoy editando un mensaje el motor no lo envíe por su cuenta, para no arriesgar que salga la versión sin editar o dos versiones distintas (ver E16).
- Como **operador**, quiero que si falta LinkedIn o el scraping falla, el mensaje caiga a una versión personalizada solo-con-formulario, para no bloquear la admisión ni mandar campos vacíos.

**Durante la semana (recordatorios con urgencia, TP4–TP6)**
- Como **aplicante**, quiero recordatorios con una fecha límite real ("tienes hasta el viernes"), para que la urgencia sea creíble y me ayude a decidir.
- Como **aplicante que ya pagó**, quiero dejar de recibir recordatorios de urgencia de inmediato, para no sentir que la marca no sabe que ya soy cliente.
- Como **operador**, quiero medir apertura/clic/pago por cada touchpoint, para saber cuál recordatorio convierte y cuál solo quema lista.

**El llamatón del viernes (recuperación el día de cierre)**
- Como **aplicante admitido que no ha pagado**, quiero que el **viernes** (día de cierre) me contacten por llamada para resolver lo último que me frena, para no perder el cupo por una duda sin resolver.
- Como **operador**, quiero que el **llamatón del viernes** lo ejecute el **Agente de calls Emma** (o una persona en la etapa inicial) sobre la lista de admitidos que no pagaron, para recuperar cierres el mismo día del cierre.

**Consentimiento y contactabilidad (transversal)**
- Como **aplicante**, quiero que solo me contacten por los canales para los que di consentimiento y datos válidos, para no recibir mensajes donde no los autoricé (ver E14).
- Como **aplicante**, quiero poder decir "no me contacten más" (STOP) y que se detenga todo de inmediato y de forma permanente, para ejercer mi derecho a salir (ver E17).

**Operación de contenido (P3)**
- Como **operador (P3)**, quiero editar el copy y los tiempos de cada touchpoint sin depender de ingeniería, para corregir un mensaje o ajustar una ventana el mismo día sin un deploy (ver A13).

**En cualquier momento (soporte)**
- Como **aplicante**, quiero poder responder "quiero hablar con alguien" y que me atienda una persona, para resolver dudas que el flujo automático no cubre.
- Como **agente (P4)**, quiero recibir al aplicante con su contexto (respuestas, touchpoint, estado de pago), para responder sin hacerle repetir todo.

### 4.3 Casos límite (exhaustivos)

Cada caso define **disparador → comportamiento esperado → pregunta abierta** y una **severidad**: **Bloqueante** (bloquea alcance/lanzamiento; decisión de producto pendiente) · **Importante** (hay que resolverlo antes de escalar) · **Menor** (housekeeping / ya encaminado).

**Empieza por los bloqueantes.**

| # | Sev. | Caso límite | Comportamiento esperado (propuesto) | Estado |
|---|------|-------------|-------------------------------------|--------|
| **E5** | 🔴 **Bloqueante** | **No admitido: ¿existe ese camino o todos son admitidos?** | **Decisión de producto pendiente.** (a) **Todos admitidos** (la "admisión" es narrativa de conversión) → no hay rama de rechazo. (b) **Admisión por score/criterio** → hace falta camino para no-admitidos (¿lista de espera?, ¿"no esta vez"?, ¿oferta alterna?). **Integridad:** si el copy dice "admitido/rechazado" pero admite al 100%, es un claim que hay que poder sostener. | **Pregunta abierta crítica** — condiciona §5 |
| **E17** | 🔴 **Bloqueante** | **Revocación de consentimiento a mitad de campaña** ("STOP" / "no me contacten más" / baja) | **Detener TODOS los touchpoints siguientes de inmediato y de forma permanente** (no "pausar": no se reanuda). Es distinto de E10 (quiere humano) y de E7 (reembolso): aquí el aplicante retira el permiso de contacto. Registrar la baja por canal, respetarla en futuras campañas, y confirmar la baja una sola vez. Aplica a cada canal (STOP en WhatsApp ≠ baja de email, salvo que pida ambos). | Palabra(s)/gesto que cuentan como STOP y alcance por canal = **pregunta abierta** |
| **E16** | 🟠 **Importante** | **Colisión edición manual (P2) vs. envío automático** (P2 edita/retiene el TP3 justo cuando vence el timer de envío) | El acto de abrir para editar/retener debe poner un **lock/hold** sobre ese envío: mientras haya edición en curso o retención activa, el motor **no dispara**. Al soltar el lock, se envía la versión aprobada. Nunca mandar dos versiones ni la no editada. Definir expiración del lock (para que un hold olvidado no congele al aplicante para siempre). | Duración del lock y quién puede liberarlo = **pregunta abierta** |
| **E18** | 🟠 **Importante** | **Ráfaga al abrir la ventana horaria** (muchos aplicaron de madrugada; sus TP2/TP3 se liberan juntos al abrir la ventana de E1) | **Suavizar el envío** (throttle/rate-limit) al liberar la cola acumulada, para no disparar un pico que queme la reputación de envío. Cruza con RNF de escalabilidad/deliverability. Distinto de E9 (fallos individuales): esto es un pico de volumen legítimo. | Tasa máx. de envío por ventana/canal = ver RNF; **pregunta abierta** |
| **E1** | 🟠 **Importante** | **Aplicó tarde en la noche** (fuera de ventana horaria) | TP1 (confirmación) sale **siempre inmediato**, sea la hora que sea. TP2/TP3, que deben "sentirse humanos", **no** se mandan de madrugada: se encolan para la siguiente **ventana diurna permitida** (valor a definir, no fijado aquí). | Ventana exacta **y cómo se determina la zona horaria del aplicante** (código de país del teléfono / IP / campo del formulario) = **pregunta abierta** |
| **E2** | 🟠 **Importante** | **Aplicó viernes** (o jueves noche): ¿aplica la urgencia "hasta el viernes"? | El deadline **no puede ser un viernes calendario fijo** o el de viernes tendría <1 día. Regla propuesta: deadline = **N días (hábiles) desde la admisión (TP3)**; el copy muestra la fecha concreta calculada. Urgencia real para todos. | Valor de **N** y si se ancla a "viernes" del ciclo = **pregunta abierta** |
| **E19** | 🟠 **Importante** | **Aplicación tardía / la cadencia debe cumplirse siempre** (aplicó viernes tarde o fin de semana, sin semana suficiente por delante) | **La ventana de admisión se ancla a la APLICACIÓN, no a un viernes fijo del calendario.** Si al aplicar ya no queda semana suficiente, el lead entra a la **siguiente ventana de cierre (próximo viernes)** y recibe la **cadencia completa (TP1→TP6 + llamatón)**. **TP1 sale siempre al instante**, cualquier día/hora; los toques de fin de semana se corren al **siguiente día hábil** (o se suavizan). El "hasta el viernes" = el cierre de la **ventana asignada del lead**, nunca uno ya pasado. Objetivo: que ningún aplicante se quede sin cadencia por la hora/día en que aplicó. Cruza con E1/E2/E18 y se implementa en el scheduler (RF-09b). | Umbral de "semana suficiente" (cuántos días mínimos antes del viernes para asignar la ventana de esa semana) = **pregunta abierta** |
| **E4** | 🟠 **Importante** | **Apify no devuelve perfil, timeout, o devuelve el equivocado** (homónimo) | (a) Sin respuesta/error/timeout → fallback a versión solo-formulario (como E3). (b) Match dudoso (baja confianza de identidad) → **no** usar datos scrapeados; degradar. Nunca mandar TP3 con datos de otra persona. | Umbral de confianza / regla de match = **pregunta abierta** |
| **E6** | 🟠 **Importante** | **Ya pagó** (en cualquier punto del flujo) | **Detener inmediatamente** todos los touchpoints de urgencia/recordatorio pendientes. Disparar handoff a **bienvenida/onboarding** (fuera de este feature). Estado "pagó" = terminal para esta campaña. | Handoff a onboarding = dependencia |
| **E8** | 🟠 **Importante** | **Doble inscripción / mismo email (o teléfono)** | **Deduplicar** por identidad (email + teléfono normalizado). La 2ª aplicación no arranca campaña paralela; actualiza la existente. Evitar mandar dos veces "¡Fuiste admitido!". | Llave de dedup canónica = **pregunta abierta** |
| **E9** | 🟠 **Importante** | **No abre WhatsApp / número inválido / rebota el email (hard bounce)** | Si el canal primario falla → **fallback al canal alterno** (si es multicanal). Si ambos fallan → marcar **inalcanzable**, detener reintentos (no quemar reputación) y exponerlo en la cola de P2. | Depende de decisión de canal (§RF) |
| **E10** | 🟠 **Importante** | **Responde pidiendo hablar con humano** | Detectar intención → **pausar la automatización** para ese aplicante, enrutar a P4 con contexto, no seguir mandando urgencia mientras haya conversación humana abierta. Reanudar/cerrar según resultado. | Detección de intención (v1 puede ser palabra clave / manual) = **pregunta abierta** |
| **E14** | 🟠 **Importante** | **Consentimiento / dato faltante al inicio** (no aceptó términos, o dio email pero no teléfono) | Contactar **solo** por canales con consentimiento y dato válido. Sin consentimiento de un canal → no usarlo. (Distinto de E17, que es revocación *posterior*.) | Ver RNF privacidad/consentimiento |
| **E3** | 🟡 **Menor** | **LinkedIn privado / sin LinkedIn / no lo dio** | Personalización **degradada con gracia**: solo lo del formulario; el copy nunca deja tokens vacíos. Fallback de plantilla completa por defecto. | — |
| **E11** | 🟡 **Menor** | **Responde con objeción/pregunta sin pedir humano** ("¿cuánto cuesta?", "¿hay becas?") | v1: toda respuesta entrante = señal → enrutar a P4 o responder con FAQ. No dejar que hable "contra un muro" mientras salen recordatorios. | Autoresponder vs. humano = **pregunta abierta** |
| **E12** | 🟡 **Menor** | **El cupo/escasez expira** (pasó el deadline sin pagar) | Definir estado terminal "no convirtió": ¿se cierra?, ¿last-chance?, ¿pasa a nurturing? Coherencia: si "el cupo cerró" y luego reabre, se erosiona la urgencia futura. | **Pregunta abierta** |
| **E13** | 🟡 **Menor** | **Clic en el link de pago pero no completa** (checkout abandonado) | Alta intención → tratar distinto del que ni abrió: recordatorio "dejaste tu pago a medias". | Depende de instrumentación del checkout |
| **E7** | 🟡 **Menor** | **Pidió reembolso** | Sacar de la campaña (ya estaba fuera por E6). **No** reintroducir a urgencia. Notificar al rol comercial. Política de reembolso = fuera de alcance. | Ver §5 |
| **E15** | 🟡 **Menor** | **Aplicó a dos programas distintos** | Fuera de alcance v1 (§5: un solo programa). Registrar el caso; no mezclar narrativas de admisión de dos programas. | Ver §5 |

> **Nota transversal:** los caminos de fallback (E3, E4, E9) comparten el principio **"degradar, nunca romper ni mentir"**: si falta un dato, se cae a una versión más simple pero correcta; nunca se envía un mensaje con campos vacíos, datos de otra persona, o una urgencia imposible de cumplir. Los caminos de salida (E6, E7, E17) comparten el principio **"cuando el aplicante ya no debe recibir urgencia, se corta al instante"** — la diferencia es si la salida es reanudable (E10 pausa) o permanente (E17 baja).

---

## 5. Alcance

### 5.1 Dentro de alcance (v1)

| # | Incluido | Detalle |
|---|----------|---------|
| A1 | **Campaña de admisión de un (1) solo programa** | Se construye y valida para **un programa piloto**. Generalizar a otros programas es v2. |
| A2 | **Motor de touchpoints TP1→TPn — NUEVO, construido DENTRO del producto** (el módulo de "campañas" actual no sirve para secuencias de admisión; no hay mailing externo), gatillado por el envío del formulario | Secuencia: confirmación → "en revisión" → admisión personalizada con pago → recordatorios con urgencia real. (Número/secuencia exactos los fija §6 — el borrador de JJ suma ~6; "5 touchpoints" a confirmar.) |
| A3 | **Personalización del TP3 (admisión)** con respuestas del formulario **+** enriquecimiento de LinkedIn vía Apify, **con fallback** | Incluye la degradación de E3/E4. |
| A4 | **Checkout de pago del cupo + landing estilo VSL con video de felicitación** ("Fuiste aceptado a nuestro programa de …") | Por **email**, el toque de admisión cae en una **landing estilo VSL con video de felicitación por ser admitido** + link al checkout con sus **dos opciones (pago completo con 10% de dto $1.755, destacado / reserva $200)**; por **WhatsApp** va el **link directo**. El feature entrega el link y mide clic/pago; **reusa el checkout existente** (Oracle30x/Stripe, `30x.com/checkout/linkedin`) — proveedor cerrado, ver §6/§9 (no Vercel/Railway/Supabase para infra). Producir la landing/video es build nuevo (§9). |
| A5 | **Urgencia con fecha límite real** ("hasta el viernes"), calculada de forma coherente (E2) | Deadline relativo a la admisión, no un día fijo que deje sin tiempo a quien aplica tarde. |
| A6 | **Ventanas horarias y scheduling** para touchpoints que deben "sentirse humanos" (E1) | TP1 siempre inmediato; el resto respeta ventana. Incluye suavizado de ráfaga al abrir la ventana (E18). |
| A7 | **Detención por pago (E6), reembolso (E7) y revocación de consentimiento/STOP (E17)** | Estados que sacan al aplicante de la urgencia; E17 es salida permanente. |
| A8 | **Deduplicación de aplicaciones repetidas (E8)** | Una identidad = una campaña activa. |
| A9 | **Ruta a humano (E10/E11): pausar automatización y enrutar con contexto** | v1: detección puede ser simple (respuesta entrante = señal); el enrutamiento y la pausa son parte del alcance. |
| A10 | **Cola/estado para el revisor (P2)** con **aprobar/editar/retener el TP3**, y **lock que evita colisión con el envío automático (E16)** | Ver quién está en qué touchpoint; garantizar que editar retiene el envío hasta soltar el lock. |
| A11 | **Kill-switch para el operador (P3)** | Poder apagar la campaña (global o por aplicante) de inmediato. |
| A12 | **Medición por touchpoint** (entregado, abierto, clic, pago) y del funnel completo | Insumo del caso de ROI (§3) y del plan de medición (§10). |
| A13 | **Editor de copy y de tiempos/ventanas por touchpoint para P3, sin deploy** | Cierra el dolor de P3 ("cambios requieren código"). v1 incluye **editar plantillas de copy y ajustar ventanas/tiempos** de cada touchpoint desde la operación. **No** incluye A/B ni multi-idioma (ver B1, B4). **Garantía explícita:** el copy es editable en v1; lo que queda fuera es experimentar con él, no cambiarlo. |
| A14 | **Manejo de fallos de entrega (E9)**: fallback de canal e "inalcanzable" | Sin quemar reputación de envío. |
| A15 | **Envío multicanal: email Y WhatsApp** (cada touchpoint por ambos canales) | Por email → landing estilo VSL con video; por WhatsApp → link directo. La conversación de WhatsApp la atiende el **Emma Closer** (rieles Kapso/Treble), que hace handoff a closer humano — **en desarrollo paralelo (dependencia)**, ver §9. |
| A16 | **Llamatón del viernes (día de cierre)** — fase de recuperación de calificados/admitidos que no pagaron | La ejecuta el **Agente de calls Emma** (Juan Ortega, en construcción) o una **persona en la etapa inicial**. Por ser IA puede correr el mismo viernes (Growth Rockstar lo hace la semana siguiente). Ver §8/§9. |

### 5.2 Fuera de alcance (por ahora)

| # | Excluido de v1 | Por qué / cuándo |
|---|----------------|------------------|
| B1 | **Multi-idioma** | Piloto en un solo idioma (español, salvo que el programa piloto diga otra cosa). i18n = v2. |
| B2 | **Otros programas / multi-programa** | v1 valida con un programa (A1). Plantillas reusables para N programas = v2. Incluye E15 (aplicar a dos programas). |
| B3 | **Reembolsos automáticos / gestión de la política de reembolso** | v1 solo **reacciona** a un reembolso (E7). Procesar el reembolso vive en otro sistema/proceso. |
| B4 | **A/B testing de copy en v1** | v1 permite **editar** el copy (A13) pero no **experimentar** con variantes. La instrumentación deja el terreno listo; el motor de experimentación es v2. |
| B5 | **Camino de "no admitido" con lógica de score** (si se decide admisión selectiva) | Depende de resolver E5. Si v1 admite al 100%, no hay rama de rechazo/lista de espera; construirla es v2. **Bloqueado por E5.** |
| B6 | **Secuencia de onboarding post-pago / entrega del programa** | Este feature termina en el **pago del cupo**. El handoff a onboarding es dependencia (E6), no build. |
| B7 | **Nurturing de largo plazo del que no convirtió** | Qué pasa con el que dejó pasar el deadline (E12) más allá de cerrar el ciclo = v2. |
| B8 | **CRM/atribución avanzada y modelos de scoring de leads** | Se registran eventos; construir scoring o atribución multi-touch no es de este feature. |
| B9 | **Construir desde cero un chatbot conversacional propio** | La conversación de closing por WhatsApp la maneja el **Emma Closer** (rieles Kapso/Treble), **en desarrollo paralelo** — este feature **no** lo construye: **depende** de él (§9) y recibe su **handoff a un closer humano** (E10/E11). Construir un motor conversacional propio, aparte de Emma, es v2. |
| B10 | **Personalización con fuentes distintas a formulario + LinkedIn/Apify** (enriquecimiento de empresa, señales de intención) | v1 se limita a formulario + LinkedIn con fallback. |
| B11 | **Elección/soporte de múltiples proveedores de pago** | v1 usa el proveedor existente (Oracle30x/Stripe, §6/§9). Multi-PSP = v2. |
| B12 | **Segmentación avanzada de urgencia por perfil** (deadlines/ofertas distintas por segmento) | v1: una regla de urgencia para todos (E2). |
| B13 | **Construir el Agente de calls Emma del llamatón** | Lo construye **Juan Ortega** (en paralelo); este feature lo **integra/dispara** para el llamatón del viernes, no lo construye. En la etapa inicial el llamatón lo hace una **persona**. |
| B14 | **Tocar / rediseñar el pipeline humano actual de los closers** (agenda calificada) | El flujo es **aditivo y NO canibaliza** el pipeline actual, que ya da buenos resultados con la agenda calificada (§2.1). Este feature automatiza admisión + cobro de los aplicantes que hoy se pierden; **no reasigna ni le quita leads** al flujo humano de cierre. Cualquier cambio a ese pipeline es fuera de alcance. |

> **Regla de oro del alcance:** todo lo que quede en la columna "fuera" y alguien asuma como incluido, es un malentendido garantizado. Si un stakeholder necesita algo de la columna B para el piloto, es un cambio de alcance que revisa quien cursa el PRD (Danilo, Alejandra, Dilan o Andrés, o delegado).

> **Supuestos/decisiones abiertas que condicionan el alcance:** (1) admisión 100% vs. por score (E5) — bloquea B5; (2) número exacto de touchpoints (§6) — condiciona A2; (3) criterio de exclusividad/viralidad, baseline propio de aplicación→pago y legalidad del scraping (§11). **Cerrado en v0.4:** el **canal es email Y WhatsApp** (ambos, no "elegir"); el fallback entre canales (A14/E9) opera dentro de ese multicanal. **Dependencias en paralelo** que condicionan A15/A16: Emma Closer y Agente de calls Emma (Juan Ortega). Todos los abiertos, en §11 (Preguntas abiertas).


---


# 6. Requisitos funcionales (MoSCoW)

> **Convención.** Cada requisito es observable y verificable. Prioridad MoSCoW: **Must** = sin esto no hay MVP; **Should** = alto valor, no bloquea el MVP; **Could** = deseable si sobra capacidad; **Won't (por ahora)** = fuera de esta versión, registrado para no re-discutirlo.
> El MVP conservador es el subconjunto **Must**: **motor de secuencias NUEVO construido dentro del producto** (RF-00); **envío multicanal email Y WhatsApp** (RF-35); admisión abierta ("admitir a todos") con **ruta alternativa por defecto para no-admitidos** (RF-15b); personalización por respuestas del formulario (sin LinkedIn); **configuración de la secuencia sin desplegar código** (RF-11); **landing estilo VSL con video de felicitación** (email) + **link directo** (WhatsApp) al checkout existente (RF-22); cortes por pago/opt-out; **freno manual de campaña** (RF-33); **sincronización de estado con el CRM** (RF-38b); instrumentación básica; y **backup/DR** de registros y consentimientos (RNF-05b). El **Emma Closer** y el **Agente de calls Emma del llamatón (Juan Ortega)** son dependencias en desarrollo paralelo (RF-35b/RF-35d); mientras no estén, WhatsApp y el llamatón operan con **persona/manual**. Este subconjunto Must es autoconsistente: cada capacidad "configurable" que otros Must asumen está garantizada por un Must (RF-11), y toda alerta operativa tiene una palanca de respuesta en el MVP (RF-33).
> Las decisiones no cerradas quedan marcadas **[PREGUNTA ABIERTA]** y remiten a §11. No se fijan cifras (horas exactas, umbrales de score, precios) que no estén confirmadas; van como parámetros configurables.

## 6.1 Disparo e ingreso a la campaña

| ID | Requisito | Prioridad | Criterio de aceptación |
|----|-----------|-----------|------------------------|
| RF-00 | El **motor de secuencias/touchpoints de admisión se construye como feature NUEVO dentro del producto de 30X**. El **módulo de "campañas" actual del producto NO se reutiliza** para esto (no está hecho para secuencias de admisión) y **no** se usa una plataforma de mailing externa. El motor orquesta scheduling, estados, cortes y envío multicanal. | **Must** | El scheduling, la máquina de estados (§6.7) y el envío multicanal (RF-35) corren dentro del producto; no dependen del módulo de campañas legado ni de una herramienta de mailing externa. Las piezas de apoyo que sí se reusan (checkout, Apify, scoring, auto-checkout Dapta) se **integran**, no se reconstruyen. |
| RF-01 | Al **enviarse un formulario de aplicación** válido, el sistema inscribe al lead en la campaña de admisión y crea un registro de campaña con su estado inicial. | **Must** | Dado un submit válido, dentro de la **latencia de inscripción** (SLA configurable; valor por defecto documentado como supuesto, p. ej. ≤1 min) existe un registro con `estado=INSCRITO`, `lead_id`, `formulario_id`, `timestamp_aplicacion` y `zona_horaria` resueltos. Un submit duplicado del mismo lead (misma aplicación) **no** crea un segundo registro. |
| RF-01b | El formulario de aplicación **captura explícitamente el consentimiento de enriquecimiento de datos** (autorización a consultar/enriquecer con fuentes públicas como LinkedIn), como campo separado del consentimiento de contacto (RNF-01). Amarra RNF-02. **[PREGUNTA ABIERTA: base — ¿consentimiento del formulario o interés legítimo? → §11].** | **Must** | El registro guarda `consentimiento_enriquecimiento` (valor y timestamp del formulario) como campo independiente de `consentimiento_contacto`; sin base legal registrada, el enriquecimiento LinkedIn (RF-17) no se ejecuta para ese lead aunque el flag global esté activo. |
| RF-02 | El sistema **deduplica** inscripciones: un lead ya activo en la campaña no reinicia la secuencia ni recibe touchpoints repetidos. | **Must** | Si un lead con registro `ACTIVO` vuelve a aplicar, el sistema conserva el registro existente y lo deja auditado; no se duplican envíos. |
| RF-03 | Cada registro de campaña captura la **carga de personalización**: respuestas del formulario normalizadas y datos de contacto (según canal). | **Must** | El registro contiene las respuestas del formulario en estructura consultable y el/los identificadores de contacto requeridos por el canal activo; si falta un dato obligatorio de contacto, el registro se marca `NO_CONTACTABLE` y no entra al scheduler. |
| RF-04 | El sistema **captura la hora local de aplicación** (o una zona horaria por defecto configurable) para alimentar las ventanas horarias del scheduler. | **Must** | Cada registro guarda `hora_local_aplicacion`; si no se puede determinar la zona, usa la zona por defecto del programa y lo deja marcado en el registro. |

## 6.2 Motor de scheduling y ventanas horarias

| ID | Requisito | Prioridad | Criterio de aceptación |
|----|-----------|-----------|------------------------|
| RF-05 | Un **motor de scheduling** calcula y encola la fecha/hora de cada touchpoint por lead a partir de reglas configurables (offsets relativos a la aplicación y a touchpoints previos). | **Must** | Para un lead inscrito, el motor genera el plan completo de touchpoints con `hora_programada` por cada uno; el plan es inspeccionable antes de ejecutarse. |
| RF-06 | **TP1 se envía de forma inmediata** ("Recibimos tu aplicación") tras la inscripción. | **Must** | El intento de envío de TP1 ocurre ≤5 min después de `INSCRITO` (offset configurable, valor por defecto documentado como supuesto). |
| RF-07 | **TP2 respeta la ventana del mismo día vs. mañana siguiente**: si la aplicación llega **temprano** se envía el mismo día; si llega **tarde** se difiere a la mañana siguiente. Los umbrales "temprano/tarde" y la ventana horaria permitida de envío son **parámetros configurables**. | **Must** | Configurada una ventana (ej. envíos solo entre `hora_inicio`–`hora_fin` local): una aplicación dentro del corte "temprano" agenda TP2 el mismo día; una fuera de ese corte agenda TP2 al inicio de la ventana del día siguiente. Ningún envío cae fuera de la ventana horaria configurada. |
| RF-08 | **TP3 ("¡Fuiste admitido!") se envía "unas horas después"** de TP2, con el offset como parámetro configurable (no cifra fija). | **Must** | TP3 se agenda a `offset_TP3` de TP2 (por defecto un rango documentado como supuesto); respeta la ventana horaria de envío. |
| RF-09 | Los **recordatorios (TP4–TP(n)) se agendan a lo largo de la semana con urgencia real hasta el viernes**; el sistema deja de agendar/enviar recordatorios pasada la fecha de **expiración del cupo (viernes)**. | **Must** | Ningún recordatorio se agenda con `hora_programada` posterior a la expiración del cupo; el último recordatorio cae antes del cierre del viernes configurado. |
| RF-09b | El scheduler **ancla la ventana de admisión a la fecha de aplicación, no a un viernes fijo del calendario** (E19). Si al aplicar **no queda semana suficiente** antes del viernes (umbral configurable), el lead se asigna a la **siguiente ventana de cierre** y recibe la **cadencia completa** (TP1→TP6 + llamatón). El "hasta el viernes" siempre es el cierre de **la ventana asignada del lead**, nunca uno ya pasado. | **Must** | Dado un lead que aplica sin días suficientes antes del viernes vigente, el motor le asigna el **viernes siguiente** como expiración y agenda los 6 touchpoints (y el llamatón) dentro de esa ventana; **TP1 sale igualmente inmediato**; ningún lead queda sin cadencia por su hora/día de aplicación. El umbral de "semana suficiente" es configurable sin desplegar código (RF-11). |
| RF-10 | El motor es **idempotente y tolerante a reinicios**: cada touchpoint se envía **exactamente una vez** aun ante reintentos del worker. | **Must** | Ante reejecución del job de un touchpoint ya enviado, el sistema no genera un segundo envío (control por clave idempotente `registro+touchpoint`). |
| RF-11 | Las reglas de secuencia (offsets, ventanas, umbrales temprano/tarde, día de expiración) son **configurables sin desplegar código**. Es la capacidad-base que hace realizables RF-05/RF-07/RF-08/RF-09 y RF-26 como "configurables"; sin ella serían hardcode. | **Must** | Un operador autorizado puede cambiar un offset/ventana y los nuevos leads adoptan la regla sin release; queda auditado quién y cuándo. |
| RF-12 | Soporte de **días hábiles / festivos / fines de semana** en el cálculo de ventanas (p. ej. no enviar en domingo, o correr la expiración). | **Could** | Configurado un calendario, el motor omite los días excluidos y recalcula las horas programadas en consecuencia. |

## 6.3 Lógica de admisión

| ID | Requisito | Prioridad | Criterio de aceptación |
|----|-----------|-----------|------------------------|
| RF-13 | El sistema aplica una **lógica de admisión** que decide si un lead recibe la narrativa de "admitido" (TP3+) o una ruta alternativa. El requisito se implementa como **regla configurable**; la **política MVP es "admitir a todos"** (la decisión de activar score es pregunta abierta, ver RF-14 y §11). | **Must** | Existe un punto de decisión `admision(lead) → {ADMITIDO, NO_ADMITIDO}` configurable; con la política MVP "todos admitidos", el 100% de inscritos válidos avanza a TP3. El resultado de la decisión queda registrado por lead. |
| RF-14 | Si la política pasa a **admisión por score**, el sistema calcula un score a partir de respuestas del formulario y admite según **umbral configurable**; los no admitidos siguen la ruta alternativa (RF-15b) sin recibir "fuiste admitido". | **Should** | Con score activo: leads ≥ umbral → `ADMITIDO`; leads < umbral → `NO_ADMITIDO` y ruta alternativa (RF-15b); el score y el umbral aplicado quedan auditados por lead. |
| RF-15 | La lógica de admisión **no debe fabricar un "admitido" para quien no cumple la política** (integridad de la narrativa). | **Must** | Ningún lead marcado `NO_ADMITIDO` recibe un touchpoint con mensaje de admisión ni link de pago del cupo de admisión. |
| RF-15b | **Ruta alternativa para `NO_ADMITIDO`**: todo lead no admitido tiene un tratamiento definido y no queda "en el limbo". Como la política de admisión es pregunta abierta, **el MVP fija la ruta por defecto = "cierre respetuoso sin touchpoints de admisión ni recordatorios de pago"**; las variantes (mensaje de no-selección, nutrición a otra campaña, lista de espera) quedan **[PREGUNTA ABIERTA → §11]**. | **Must** | Un lead `NO_ADMITIDO` transita a un estado terminal/alternativo auditado y **no** recibe TP3+ ni recordatorios de cupo; la ruta aplicada (por defecto "cierre respetuoso") queda registrada. Cambiar la ruta es configurable sin desplegar código (RF-11). |

## 6.4 Personalización del TP3 (formulario + Apify/LinkedIn)

| ID | Requisito | Prioridad | Criterio de aceptación |
|----|-----------|-----------|------------------------|
| RF-16 | TP3 se **personaliza con las respuestas del formulario** (nombre, rol, objetivo declarado, etc.) mediante plantillas con variables. | **Must** | Dado un lead con respuestas, TP3 renderiza las variables correspondientes; una variable sin dato usa un **fallback** definido y **nunca** deja placeholders crudos ("Hola {nombre}") ni texto vacío roto. |
| RF-17 | El sistema puede **enriquecer el perfil vía scraping de LinkedIn con Apify** para profundizar la personalización de TP3, **solo cuando existe base legal/consentimiento (ver §7)** y hay URL/identificador de LinkedIn disponible. | **Should** | Cuando el enriquecimiento está habilitado y hay LinkedIn del lead, el sistema obtiene los campos definidos vía Apify y los deja disponibles para la plantilla, con `fuente=apify` y `timestamp` registrados. |
| RF-18 | **Fallback de personalización sin LinkedIn**: si no hay LinkedIn, el enriquecimiento falla, expira (timeout) o el consentimiento no aplica, TP3 se genera **solo con datos del formulario** sin degradar la calidad ni retrasar el envío más allá de un tope configurable. | **Must** | Simulando "sin LinkedIn"/error de Apify: TP3 se envía a tiempo usando la ruta de formulario; el registro marca `enriquecimiento=OMITIDO/FALLIDO` con motivo. El envío no se bloquea por la dependencia de Apify. |
| RF-19 | El enriquecimiento con Apify tiene **timeout y control de costo/tasa**: no puede demorar la secuencia ni disparar llamadas ilimitadas. | **Should** | Superado el `timeout_enriquecimiento`, el sistema procede con fallback (RF-18); las llamadas a Apify respetan un límite de tasa/costo configurable y se contabilizan por lead. |
| RF-20 | La personalización avanzada (redacción asistida del mensaje a partir de formulario + LinkedIn) es **revisable/QC** antes de escalar volumen. | **Could** | Existe modo en que una muestra de TP3 personalizados pasa por revisión humana antes del envío masivo; el % revisado es configurable. |

## 6.5 Checkout, VSL y expiración del cupo

| ID | Requisito | Prioridad | Criterio de aceptación |
|----|-----------|-----------|------------------------|
| RF-21 | TP3 incluye un **link de pago del cupo** único por lead que lleva al **checkout YA EXISTENTE de LinkedIn Sales** (`30x.com/checkout/linkedin` + variante `-discount`), capa **Oracle30x sobre Stripe** (`checkout.30x.com`, admin en `checkout.30x.com/admin`). **El proveedor NO es pregunta abierta: se reusa/integra el checkout existente** (§0). El checkout expone **dos opciones: (a) pago completo con 10% de dto = $1.755 (opción destacada) y (b) reserva de $200** (§2.4). La **reserva de $200 es NO reembolsable** y se comunica claramente al lead antes de pagar; el **saldo/pago completo se acuerda la semana previa al inicio** del programa. Restricción org: no Vercel/Railway/Supabase. | **Must** | Cada lead admitido recibe un link del checkout existente asociado a su `registro`; al abrirlo puede elegir **pago completo ($1.755, destacado) o reserva ($200)**; el checkout **muestra explícitamente que la reserva no es reembolsable** antes de cobrarla; el link identifica inequívocamente al lead (para atribución y cortes) y el sistema registra cuál opción tomó (reservó vs. pagó completo). Coordinar la integración con **Mariana Cerón** (dueña del checkout automático). |
| RF-22 | Existe una **landing estilo VSL con un video de felicitación por ser admitido** ("Fuiste aceptado a nuestro programa de …") ligada al flujo de admisión/checkout. **Por email**, el TP3 lleva a esta landing; **por WhatsApp**, el TP3 lleva el **link directo** al checkout. | **Must** | El lead admitido que llega por **email** accede a la landing con el **video de felicitación** y el llamado a pagar el cupo; el que llega por **WhatsApp** recibe el **link directo** al checkout. La landing es **responsive en los dispositivos objetivo definidos** (mobile + desktop; el borrador asume mobile-first, supuesto a validar) y alcanza un **umbral de performance configurable** (p. ej. LCP ≤ Xs en conexión objetivo; X documentado como supuesto). Cada apertura registra un evento `visita_vsl` con `lead_id` y `timestamp`. |
| RF-23 | El **cupo expira el viernes** (fecha/hora configurable): tras la expiración, el link de pago queda **no pagable** o muestra estado de cupo vencido. | **Must** | Pasada la expiración, intentar pagar por el link devuelve un estado "cupo expirado" y no completa el cobro; el registro pasa a `EXPIRADO` si no hubo pago. |
| RF-24 | El sistema **confirma el pago** (webhook/estado del proveedor) y registra `PAGADO` con `timestamp` y monto. | **Must** | Al completarse un pago, dentro de la **latencia de confirmación** (SLA configurable; valor por defecto documentado como supuesto, p. ej. ≤5 min) el registro pasa a `PAGADO` con datos del cobro; sirve de disparador de cortes (RF-30). |
| RF-25 | **Extensión/reapertura de cupo** (caso límite) manejada explícitamente por configuración, no ad-hoc. | **Could** | Un operador autorizado puede extender la expiración de un lead/cohorte; el cambio queda auditado y recalcula los cortes de recordatorios. |
| RF-25b | **Consistencia de precio landing↔checkout**: el precio que ve el lead en la landing (`30x.com/linkedin-sales`) y en el mensaje/TP3 debe coincidir con el que cobra el checkout. Hoy hay **desfase conocido: landing muestra $1,500 vs. checkout cobra $1,950** (Emmy, 4-sep), y un **fallback `_tbd` a $1,650** cuando falta `start_date_30x` en la cohorte aunque el form promete $1,950 (Emmy, 16-sep). El precio vigente de LinkedIn Sales en checkout = **$1,950** (lista) y **$1.755** para el **pago completo con 10% de dto** (opción destacada, §2.4). | **Must** | Un chequeo automatizado (o de release) verifica que landing, TP3 y checkout muestran los **mismos** precios (**$1.950 lista / $1.755 con 10% de dto / $200 reserva**); ninguna cohorte activa queda con el fallback `_tbd` a $1,650 por `start_date_30x` faltante (se valida que la fecha exista antes de publicar la cohorte). Cualquier discrepancia dispara alerta y bloquea el envío del TP3 con precio inconsistente. Validar con **Emmy** (montó la versión previa) y **Mariana Cerón** (checkout). |

## 6.6 Touchpoints: conteo y secuencia configurable

| ID | Requisito | Prioridad | Criterio de aceptación |
|----|-----------|-----------|------------------------|
| RF-26 | La secuencia de touchpoints **TP1…TP(n) es configurable en número, orden, contenido y canal**. **La cadencia de arranque está DEFINIDA por JJ (v0.5) en 6 touchpoints + llamatón** (§8.2/§8.4); la configurabilidad se conserva para **iterar/A/B** (p. ej. 2 vs. 3 recordatorios, §10.3), no porque el número esté abierto. | **Must** | El motor ejecuta la cadencia definida de **6 touchpoints** (con su copy, offset y canal email+WhatsApp) más el llamatón; un operador puede ajustar número/offset/copy para un A/B sin desplegar código; la campaña ejecuta exactamente la secuencia configurada. |
| RF-27 | Cada touchpoint tiene **contenido versionado** (copy/plantilla) para permitir iteración y A/B futuro sin perder trazabilidad de qué versión recibió cada lead. | **Should** | El registro de cada envío guarda el `id/versión de plantilla` usada; se puede saber qué copy recibió cada lead. |
| RF-28 | Soporte de **variantes A/B** por touchpoint. | **Could** | Configurada una prueba A/B, los leads se reparten según proporción definida y la variante queda registrada para medición. |

## 6.7 Estados, cortes, opt-out y reintentos

| ID | Requisito | Prioridad | Criterio de aceptación |
|----|-----------|-----------|------------------------|
| RF-29 | El registro de campaña mantiene una **máquina de estados** explícita (p. ej. `INSCRITO → ACTIVO → {ADMITIDO → {PAGADO / EXPIRADO} / NO_ADMITIDO → RUTA_ALT} / OPTOUT / NO_CONTACTABLE`). | **Must** | Toda transición de estado queda auditada con timestamp y causa; **todo lead termina en un estado terminal definido** (incluido `NO_ADMITIDO`, RF-15b); no existen estados ambiguos ni leads "en el limbo" sin estado. |
| RF-30 | **Corte por pago**: cuando un lead paga (`PAGADO`), el sistema **cancela todos los touchpoints pendientes** (no más recordatorios). | **Must** | Tras `PAGADO`, ningún touchpoint posterior se envía a ese lead; los jobs pendientes quedan cancelados y auditados. |
| RF-31 | **Opt-out / baja**: el lead puede solicitar no recibir más mensajes; el sistema detiene todos los envíos y lo marca `OPTOUT`. | **Must** | Recibida una señal de opt-out (palabra clave en WhatsApp / enlace de baja en email, según canal), en el próximo ciclo no se envía nada más a ese lead y queda `OPTOUT`; se respeta en futuras campañas. |
| RF-32 | **Manejo de rebotes/fallos de entrega**: si un touchpoint **rebota** o falla, el sistema aplica **reintentos con backoff** y, agotados, marca el canal como fallido y (si aplica) intenta canal alternativo o `NO_CONTACTABLE`. | **Must** | Ante un fallo transitorio, hay reintentos limitados con espera creciente; ante fallo permanente (hard bounce / número inválido), no se reintenta indefinidamente y el registro queda marcado con la causa. |
| RF-33 | **Freno global / pausa de campaña**: un operador autorizado puede pausar o detener la campaña (o una cohorte) sin perder estado. Es la palanca para **actuar sobre las alertas de RNF-18** (rebotes/quejas altos, riesgo de baneo de RNF-08/09); sin este freno en el MVP, una alerta no tiene respuesta. | **Must** | Al pausar, ningún envío nuevo sale; al reanudar, el motor retoma los planes pendientes sin duplicar envíos ya realizados. El pausado manual por operador está en el MVP; el auto-pausado por umbral lo cubre RNF-07. |
| RF-34 | **Tope anti-fatiga**: límite configurable de mensajes por lead por ventana para no saturar. El tope aplica **global por lead a través de todas las campañas de admisión activas de 30X** (un lead en dos campañas simultáneas no recibe el doble), no solo por campaña. **[PREGUNTA ABIERTA: confirmar alcance global vs por-campaña y si incluye campañas fuera del feature de admisión → §11].** | **Should** | Configurado un tope, el conteo de mensajes por lead **agrega todas las campañas de admisión activas** en la ventana definida; el sistema nunca supera ese número por lead y los excedentes se difieren o descartan según regla. |

## 6.8 Canal(es)

| ID | Requisito | Prioridad | Criterio de aceptación |
|----|-----------|-----------|------------------------|
| RF-35 | La campaña envía **cada touchpoint por email Y por WhatsApp** (multicanal, los dos a la vez). Por **email** el TP3 lleva a la **landing estilo VSL con video** (RF-22); por **WhatsApp** lleva el **link directo** al checkout. El envío/conversación por WhatsApp corre sobre el **Emma Closer** (rieles Kapso/Treble), **en desarrollo paralelo** (dependencia, RF-35b/§9). | **Must** | El MVP entrega la secuencia completa **por email y por WhatsApp**; cada touchpoint tiene su render por canal (email → landing VSL, WhatsApp → link directo). La abstracción de canal permite operar ambos sin reescribir el motor. Mientras el Emma Closer no esté listo, la conversación de WhatsApp se cubre con la ruta manual (P4). |
| RF-35b | El **Emma Closer** (WhatsApp) atiende la conversación entrante del lead y hace **handoff a un closer humano** cuando corresponde. Corre sobre los **rieles de Emma (Kapso/Treble)** y está **en desarrollo paralelo**: es **dependencia**, no build de este feature. | **Should** (depende de disponibilidad del agente) | Cuando el agente está disponible, las respuestas del lead por WhatsApp las atiende el Emma Closer, que escala a un closer humano con contexto (E10/E11); mientras no lo esté, la ruta a humano (§4 P4) opera manual. El feature **integra** el agente, no lo construye. |
| RF-35d | **Llamatón del viernes (día de cierre)**: el sistema dispara una **fase de recuperación por llamada** dirigida a los **calificados/admitidos que no han pagado** al llegar el cierre (viernes). Su objetivo tiene **dos salidas: (1) llevar a pago** o **(2) agendar una reunión con el equipo comercial, presentado al lead como "equipo de admisiones"**. La ejecuta el **Agente de calls Emma** (Juan Ortega, en construcción — **dependencia**) o una **persona en la etapa inicial**. | **Should** | Al llegar el viernes, el sistema produce la **lista de admitidos sin `PAGADO`** y la entrega al Agente de calls Emma (o a la persona) para el llamatón; los resultados de la llamada (contactado / pagó / **agendó con "equipo de admisiones"** / no contesta / opt-out) se registran y respetan los cortes (RF-30/RF-31). Por ser IA puede correr el **mismo viernes**. |
| RF-36 | **Coordinación multicanal**: como cada touchpoint sale por email **y** WhatsApp por diseño, el sistema coordina ambos envíos (mismo contenido/intención por canal, sin condiciones de carrera), respeta el **consentimiento y el opt-out por canal** (STOP en WhatsApp ≠ baja de email, E17), y evita reenvíos no intencionales. | **Must** | Con ambos canales activos, cada touchpoint sale una vez por canal según su render; un opt-out de un canal detiene ese canal sin afectar el otro; no hay envíos duplicados por reintentos (idempotencia por `registro+touchpoint+canal`). |

## 6.9 Instrumentación por touchpoint

| ID | Requisito | Prioridad | Criterio de aceptación |
|----|-----------|-----------|------------------------|
| RF-37 | El sistema **instrumenta cada touchpoint** con el embudo mínimo: **enviado → entregado → abierto → click → pagado** (los eventos disponibles dependen del canal; los no soportados se marcan "N/A" explícitamente). | **Must** | Por cada touchpoint y lead se registran los eventos disponibles con timestamp; se puede reconstruir el embudo por touchpoint y agregado por cohorte. WhatsApp registra al menos enviado/entregado/leído+click; email al menos enviado/entregado/abierto/click. |
| RF-38 | Los eventos permiten calcular **atribución del pago al touchpoint/link** que lo originó (para el caso de ROI y §2). | **Must** | Un `PAGADO` puede vincularse al link/touchpoint desde el que se originó; se puede reportar pagos por touchpoint y por cohorte. |
| RF-38b | **Sincronización de estado con el CRM (HubSpot, fuente de verdad comercial)**: el estado del registro de campaña (`INSCRITO/ADMITIDO/NO_ADMITIDO/PAGADO/EXPIRADO/OPTOUT`), el pago y los touchpoints clave se escriben de vuelta en el contacto/deal del CRM. Sin esto, la atribución del pago (RF-38) vive aislada del embudo comercial. **[PREGUNTA ABIERTA: campos/objetos exactos y sentido del sync (uni/bidireccional) → §11].** | **Must** | Un cambio de estado del lead se refleja en su registro del CRM dentro de una **ventana de frescura configurable** (valor por defecto documentado como supuesto); un `PAGADO` y un `OPTOUT` quedan visibles en HubSpot con su timestamp. El opt-out capturado en HubSpot se respeta en la campaña (coherencia bidireccional mínima). |
| RF-39 | Métricas expuestas en un **tablero/consulta operativa** (aunque sea mínima) para monitorear la campaña en vivo. | **Should** | Existe una vista con conteos de estados y embudo por touchpoint actualizada de forma incremental; no requiere consultar la base a mano. |
| RF-40 | **Costo por resultado verificado** medible: el sistema registra costos operativos atribuibles (envíos, Apify, pago) suficientes para calcular costo ÷ pagos confirmados que pasaron QC. | **Should** | Se puede obtener, por cohorte, el numerador (costos operativos del período) y el denominador (pagos verificados) para el indicador de §2; ver RNF de costo. |

## 6.10 Fuera de alcance de esta versión (Won't – por ahora)

| ID | Requisito | Prioridad | Nota |
|----|-----------|-----------|------|
| RF-41 | Enriquecimiento con fuentes distintas a Apify/LinkedIn (Lusha, Clearbit, etc.). | **Won't** | Registrado; no en MVP. |
| RF-42 | Optimización automática de horarios de envío por ML (send-time optimization). | **Won't** | Depende de datos que aún no existen; futura iteración. |
| RF-43 | Personalización de la **VSL** por lead (video dinámico). | **Won't** | La VSL de felicitación es única/segmentada, no individualizada, en esta versión. |
| RF-44 | Negociación/planes de pago o descuentos automáticos en el checkout. | **Won't** | El cupo tiene un precio y una expiración; no hay lógica de descuentos automáticos en MVP. |

---

# 7. Requisitos no funcionales

> Cada RNF es verificable. Se prioriza igual con MoSCoW. Se marcan supuestos y preguntas abiertas donde falta dato; **no se inventan cifras**. **Restricción de organización: no proponer Vercel, Railway ni Supabase como stack ni como infraestructura.**

## 7.1 Privacidad, consentimiento y legalidad (scraping LinkedIn + mensajería)

| ID | Requisito | Prioridad | Criterio de aceptación |
|----|-----------|-----------|------------------------|
| RNF-01 | **Base legal para contactar**: solo se envían touchpoints a leads que dieron su dato de contacto en el formulario con aviso de que serán contactados por ese canal; existe y se registra el **consentimiento** por canal. | **Must** | Cada registro guarda evidencia del consentimiento (texto y timestamp del formulario) para el/los canales usados; sin consentimiento válido para un canal, no se envía por ese canal. |
| RNF-02 | **Legalidad del enriquecimiento con LinkedIn vía Apify**: el scraping/enriquecimiento se realiza solo bajo una **base legal revisada** (interés legítimo/consentimiento, según jurisdicción) y respetando los Términos aplicables; **[PREGUNTA ABIERTA: validación legal del scraping de LinkedIn con Apify → §11]**. Hasta contar con luz verde legal, el enriquecimiento LinkedIn permanece **desactivado** (el MVP conservador corre sin él, RF-18). La base legal se amarra a la captura del formulario en **RF-01b**. | **Must** | El enriquecimiento LinkedIn está detrás de un flag que solo se activa con aprobación legal documentada; con el flag apagado, la campaña opera completa sin datos de LinkedIn. Aun con el flag activo, un lead sin base legal registrada (RF-01b) no se enriquece. Se registra la fuente y la base legal de cada dato enriquecido. |
| RNF-03 | **Cumplimiento de mensajería**: WhatsApp respeta las políticas de la plataforma (plantillas aprobadas, ventana de sesión, opt-out); email cumple requisitos anti-spam (identificación del remitente, enlace de baja funcional). | **Must** | Los envíos de WhatsApp usan plantillas conformes y honran opt-out; todo email incluye baja funcional e identificación del remitente. Un opt-out se respeta en ≤1 ciclo (ver RF-31). |
| RNF-04 | **Derechos del titular / minimización**: se recolecta y conserva solo el dato necesario; existe forma de atender solicitudes de acceso/borrado (DSAR) dentro de un plazo definido. | **Should** | Se puede localizar y borrar/anonimizar los datos de un lead a solicitud **dentro de un plazo configurable de atención de DSAR** (valor por defecto documentado como supuesto; **[PREGUNTA ABIERTA: plazo legal aplicable por jurisdicción → §11]**); el enriquecimiento guarda solo los campos definidos, no volcados completos innecesarios. |
| RNF-05 | **Retención**: los datos personales y de enriquecimiento se conservan por un periodo definido y luego se purgan/anonimizan. **[PREGUNTA ABIERTA: periodo de retención → §11].** | **Should** | Configurado un periodo, los datos vencidos se purgan/anonimizan de forma verificable. |
| RNF-05b | **Backup y recuperación ante desastre (DR)** de la base de registros, estados y **consentimientos** (RNF-01/RF-01b, evidencia legal): existen respaldos periódicos y un procedimiento de restauración probado ante pérdida de infraestructura (no solo reinicio de worker, que cubre RNF-13). | **Must** | Están definidos **RPO y RTO como parámetros configurables** (valores por defecto documentados como supuesto, sin inventar cifra); una **prueba de restauración** recupera registros, estados y evidencia de consentimiento sin pérdida más allá del RPO acordado. |

## 7.2 Deliverability (evitar spam)

| ID | Requisito | Prioridad | Criterio de aceptación |
|----|-----------|-----------|------------------------|
| RNF-06 | **Higiene de entregabilidad de email**: dominio con SPF, DKIM y DMARC configurados; envíos desde dominio/subdominio con reputación gestionada. | **Must** | Un chequeo de autenticación de un email de prueba muestra SPF/DKIM/DMARC en `pass`; los envíos no salen desde dominios sin autenticar. |
| RNF-07 | **Control de reputación y tasa de queja/rebote**: se monitorean bounces y quejas; superado un umbral, la campaña alerta y frena el canal afectado. | **Must** | Definidos umbrales (supuesto documentado), al superarse se dispara alerta y pausa automática del canal; los hard bounces no se reintentan (RF-32). |
| RNF-08 | **WhatsApp sin patrón de spam**: uso de plantillas aprobadas, respeto de ventanas y del tope anti-fatiga (RF-34) para no arriesgar el número/cuenta. | **Must** | Ningún lead recibe más mensajes que el tope configurado; los envíos fuera de ventana de sesión usan plantilla aprobada. Un simulacro no genera bloqueos por patrón de abuso. |
| RNF-09 | **Warm-up / rampa de volumen**: al escalar, el volumen de envíos crece gradualmente para proteger reputación. | **Should** | Configurada una rampa, el sistema no supera el volumen diario permitido para la fase de warm-up vigente. |

## 7.3 Rendimiento y escalabilidad (bandas de volumen)

| ID | Requisito | Prioridad | Criterio de aceptación |
|----|-----------|-----------|------------------------|
| RNF-10 | **Puntualidad del scheduler**: los touchpoints se ejecutan dentro de una tolerancia respecto a su `hora_programada`. | **Must** | ≥95% de los touchpoints se disparan dentro de ±X min de su hora programada (X configurable; valor por defecto documentado como supuesto); TP1 inmediato cumple ≤5 min (RF-06). |
| RNF-11 | **Escalabilidad por bandas de volumen**: el sistema se dimensiona y se cotiza por **bandas de volumen** de inscritos/envíos, no por costo fijo. **[PREGUNTA ABIERTA: bandas y volúmenes objetivo → §11].** | **Must** | Documentadas al menos 3 bandas (p. ej. baja/media/alta) con su comportamiento esperado; una prueba de carga en la banda objetivo del MVP procesa el volumen sin perder envíos ni violar RNF-10. |
| RNF-12 | **Degradación controlada de dependencias**: si Apify, el proveedor de pago o el canal fallan, la campaña sigue operando con fallback y encolado, sin perder leads. | **Must** | Simulada la caída de una dependencia, no se pierden registros; los envíos se difieren/encolan y se reanudan al recuperarse; el enriquecimiento cae a fallback (RF-18). |
| RNF-13 | **Sin pérdida de mensajes bajo reinicio**: la cola de touchpoints es durable. | **Must** | Reiniciando el worker con jobs en cola, todos los touchpoints pendientes se ejecutan una sola vez tras el reinicio (idempotencia RF-10). |

## 7.4 Costo por resultado verificado (requisito operativo)

| ID | Requisito | Prioridad | Criterio de aceptación |
|----|-----------|-----------|------------------------|
| RNF-14 | El sistema permite calcular el **costo por resultado verificado** = costo total de operar (envíos + Apify + fees de pago + revisión humana) ÷ **pagos de cupo confirmados que pasaron QC**, por cohorte. | **Must** | Para una cohorte cerrada se obtiene el indicador con numerador y denominador trazables; el denominador cuenta solo pagos confirmados (no clicks ni promesas). |
| RNF-15 | El indicador de costo por resultado verificado debe **poder bajar al aumentar el volumen** (condición para escalar según el marco 30X); se reporta por banda de volumen. | **Should** | Se puede comparar el costo por resultado verificado entre bandas; si no baja con el volumen, se marca como señal de "no escalar aún" y se reporta como tal. |
| RNF-16 | Se registra información suficiente para el **período de repago**; si no puede calcularse con datos reales, el feature se declara **APUESTA** (autorización de fundadores), sin fabricar números. | **Should** | El reporte incluye costos y pagos reales del periodo; ante datos insuficientes, el estado del caso de negocio se marca explícitamente "APUESTA" en lugar de estimar cifras inventadas. |

## 7.5 Observabilidad y monitoreo

| ID | Requisito | Prioridad | Criterio de aceptación |
|----|-----------|-----------|------------------------|
| RNF-17 | **Logs y auditoría por lead y por touchpoint**: cada envío, transición de estado, decisión de admisión y llamada a dependencia queda registrada con timestamp y resultado. | **Must** | Dado un lead, se puede reconstruir su historia completa (qué recibió, cuándo, por qué canal, con qué plantilla, con qué resultado). |
| RNF-18 | **Alertas operativas**: fallos de envío por encima de umbral, caída de dependencias, rebotes/quejas altos y scheduler retrasado disparan alerta a un canal operativo. | **Must** | Simulados esos eventos, se genera la alerta correspondiente en el canal definido dentro de una ventana de tiempo acordada. |
| RNF-19 | **Métricas de salud del sistema** (throughput, backlog de cola, tasa de error de Apify/pago/canal) visibles para operación. | **Should** | Existe un panel/consulta con estas métricas cuya **frescura no supera una ventana configurable** (valor por defecto documentado como supuesto, p. ej. ≤5 min de retraso); permite ver el backlog de la cola dentro de esa ventana. |

## 7.6 Seguridad de datos personales

| ID | Requisito | Prioridad | Criterio de aceptación |
|----|-----------|-----------|------------------------|
| RNF-20 | **Cifrado en tránsito y en reposo** de datos personales y de contacto. | **Must** | Todo tráfico usa TLS; los datos personales en almacenamiento están cifrados en reposo. |
| RNF-21 | **Control de acceso mínimo (least privilege)**: solo roles autorizados acceden a datos de leads, configuran campañas o cursan cambios; acciones sensibles auditadas. | **Must** | Un usuario sin rol no puede ver PII ni cambiar la configuración; cambios de configuración quedan atribuidos a un usuario. |
| RNF-22 | **Gestión segura de secretos**: credenciales de Apify, proveedor de pago y canales se guardan en un gestor de secretos, nunca en código ni en el cliente. | **Must** | No hay secretos en el repositorio ni expuestos al navegador; la rotación de una credencial no requiere cambiar código. |
| RNF-23 | **Seguridad del checkout/pago**: el manejo del pago cumple los estándares del proveedor (no se almacenan datos sensibles de tarjeta en sistemas propios). | **Must** | El flujo de pago delega los datos de tarjeta al proveedor; los sistemas propios solo guardan referencias/estados del cobro, no PAN/CVV. |
| RNF-24 | **Aislamiento de PII en enriquecimiento y logs**: los datos de LinkedIn/Apify y la PII no se filtran en logs, mensajes de error ni telemetría de terceros. | **Should** | Una revisión de logs de muestra no contiene PII en claro ni tokens; los errores registran identificadores, no datos personales completos. |

---

### Notas de trazabilidad a otras secciones
- **Preguntas abiertas** referenciadas (RF-01b base legal de enriquecimiento, RF-13 política de admisión, RF-15b variantes de ruta alternativa, RF-25b consistencia de precio landing↔checkout, RF-26 n exacto de touchpoints, RF-34 alcance del tope anti-fatiga, RF-38b campos/sentido del sync con CRM, RNF-02 legalidad del scraping, RNF-04 plazo DSAR, RNF-05 retención, RNF-05b RPO/RTO, RNF-11 bandas de volumen): consolidar en **§11**. *(RF-21 proveedor de pago: **CERRADO** en v0.3 — se reusa el checkout existente Oracle30x/Stripe. RF-35 canal: **CERRADO en v0.4 — email Y WhatsApp (multicanal)**; abierto solo el cronograma del **Emma Closer** (RF-35b) y del **Agente de calls Emma del llamatón** (RF-35d), ambos en desarrollo paralelo.)*
- **Decisiones marcadas como configurables** (offsets de scheduling, n de touchpoints, canal, umbral de admisión, expiración): alimentan **§8 Diseño/experiencia** y **§9 Dependencias/riesgos/supuestos**.
- **RNF-14/15/16 (costo por resultado verificado y repago)**: son la contraparte técnica del **caso de ROI 30X (§2)**.
- **Restricción de organización** (no Vercel/Railway/Supabase): vinculante para **§8/§9** al definir infraestructura.


---


## 8. Diseño y experiencia

### 8.1 Principio rector de diseño

La experiencia se juzga contra una sola vara: **¿se siente como una admisión real a un programa, o como una secuencia de marketing automatizada?** Todo lo demás (canal, timing, copy) se subordina a eso. El aplicante debe percibir *revisión humana, criterio y escasez legítima* — no un embudo. Esto tiene una consecuencia de diseño dura: **el sistema nunca promete lo que no cumple** (no dice "un humano revisó" si nadie revisó), porque la promesa de admisión se rompe la primera vez que suena a robot (ver riesgo #1 en §9).

### 8.2 La secuencia de touchpoints (flujo completo)

El flujo modela un **ciclo de admisión**: recibimos → evaluamos → decidimos → invitamos a asegurar el cupo → cerramos con fecha límite real. Cada touchpoint (TP) tiene un único objetivo; si un TP no mueve al aplicante hacia el pago o hacia sentirse admitido, sobra.

> **Convención:** los tiempos "T+" son relativos al evento `aplicó` (envío del formulario). El **canal está decidido: email Y WhatsApp** (cada TP sale por ambos; por email el toque de admisión cae en una **landing estilo VSL con video de felicitación**, por WhatsApp va el **link directo** al checkout). **La cadencia está DEFINIDA por JJ (v0.5):** son **6 touchpoints de "aplicó" al viernes de cierre** + **llamatón el viernes**, con los momentos de abajo. Lo que queda por afinar es el **copy fino** (ejemplo ilustrativo, no definitivo — revisado por Ventas/Marca, §11 #12) y los **umbrales horarios exactos** (parámetros configurables). La **ventana se ancla a la aplicación, no a un viernes fijo del calendario** (ver caso límite E19 en §4.3 y RF-09b): quien aplica cuando ya no queda semana suficiente entra a la **siguiente ventana de cierre** y recibe la **cadencia completa**. La *lógica de admisión* (todos vs. por score) sigue abierta (§11).

| TP | Momento | Canal (email + WhatsApp) | Objetivo | Contenido / tono |
|---|---|---|---|---|
| **TP1 — Recibimos tu aplicación** | Inmediato (T+0, < 2 min) | Email + WhatsApp (ambos) | Acuse cálido; bajar ansiedad; fijar expectativa de "esto es una admisión, no un formulario" | Confirmación humana y breve. Nombra el programa, dice qué sigue ("nuestro equipo va a revisar tu aplicación") y da un horizonte de tiempo. Tono: cercano, primera persona, sin jerga de sistema. **No** vende ni pide pago. |
| **TP2 — Estamos revisando tu aplicación** | Mismo día si aplicó temprano / mañana temprano si aplicó tarde (ventana `[A DEFINIR]`) | Igual que TP1 | Sostener la narrativa de evaluación; crear anticipación legítima; reforzar que hay criterio detrás | "Muy humano": suena a persona que está mirando su caso. Puede referenciar 1 dato de su aplicación para probar que se leyó (personalización ligera, §8.4). **Honestidad:** el copy debe ser verdadero respecto a si hay o no revisión real (§11, lógica de admisión). Tono: sereno, no urgente todavía. |
| **TP3 — ¡Fuiste admitido!** *(pivote del flujo)* | Unas horas después de TP2 | Igual | **Anunciar la admisión + entregar el link de pago del cupo**; convertir intención en acción | Mensaje **personalizado** según respuestas del formulario y, si hay match, enriquecimiento de LinkedIn (Apify, §8.4 y §9). Celebra, hace sentir seleccionado, explica *por qué* fue admitido (aunque sea a nivel de categoría). Presenta las **dos opciones de pago**: **pago completo con 10% de dto = $1.755 (destacado)** o **reserva de $200**. **Por email** cae en la **landing estilo VSL con video de felicitación**; **por WhatsApp**, **link directo** al checkout. Introduce la fecha límite (viernes de su ventana). Tono: celebratorio pero con criterio; escasez real, no fabricada. |
| **TP4 — Recordatorio 1 (tu cupo te espera)** | ~24 h después de TP3, si no pagó | Igual | Reactivar a quien vio pero no pagó; resolver la primera objeción implícita | Recuerda que el cupo está **apartado hasta el viernes** pero no garantizado; reitera valor + fecha límite. Tono: servicial, no acosador. |
| **TP5 — Recordatorio 2 (media semana)** | Media semana (mié/jue) | Igual | Elevar urgencia con **escasez real (cupos) + prueba social**; reducir fricción de pago | **Escasez real** ("quedan pocos cupos, el grupo se cierra el viernes") + **prueba social** (casos/resultados). Puede ofrecer ayuda / resolver dudas (canal a soporte o humano). Tono: directo, útil. |
| **TP6 — Último llamado (hoy cierra)** | Viernes AM | Igual | Último empujón antes de expirar el cupo | Urgencia máxima pero honesta ("hoy cierra"); deja claro qué pasa después (el cupo se libera / la aplicación se archiva). Tono: firme, respetuoso, sin culpa. |

**Llamatón del viernes (recuperación el día de cierre):** el mismo **viernes (tarde)**, día en que expira el cupo, los **calificados/admitidos que no han pagado** entran a una **fase de recuperación por llamada**. **Su trabajo tiene dos salidas: (1) llevar a pago** en la llamada, o **(2) —si el lead lo necesita— agendar una reunión con el equipo comercial**, que al lead **se le presenta como "equipo de admisiones"** (coherente con la narrativa de admisión, no de venta). A diferencia de Growth Rockstar —que llama la semana siguiente— aquí puede correr **el mismo viernes** porque lo conduce una **IA: el Agente de calls Emma que construye Juan Ortega** (en construcción, §9). En la **etapa inicial** el llamatón lo hace una **persona** y luego pasa al agente. Es el último recurso de conversión dentro del ciclo, coherente con la urgencia "hasta el viernes" de TP4–TP6 y con los cortes por `pagó`/`opt_out`.

**Ramas y estados terminales del flujo:**
- **Pagó** en cualquier punto → se detienen todos los TPs pendientes de inmediato (regla dura: nunca pedir pago a quien ya pagó — ver requisito de idempotencia en §7 y riesgo de "spam" en §9) → entra a onboarding/bienvenida (fuera de alcance de este PRD, ver §5).
- **Opt-out / STOP** en cualquier punto → se detienen todos los TPs y se marca `opt-out` (obligación legal, ver §9).
- **Expiró** (llegó el cierre sin pagar) → se detiene la secuencia; el aplicante queda en estado `expirado` para eventual recuperación/re-oferta (política de re-oferta = pregunta abierta, §11).
- **No admitido** (si la admisión es por score y no todos entran) → **no** recibe TP3+ de admisión; recibe un cierre respetuoso o cae a otra nurture, y **se instrumenta con el evento `no_admitido_notificado`** (§10.4) para poder medir esa rama. Esta rama depende de la decisión de lógica de admisión (§11) y hoy **no está definida**; el evento queda previsto aunque la rama arranque desactivada.

### 8.3 Ejemplos de copy (ILUSTRATIVOS — no definitivos)

> Marca/Ventas ajustan el copy final (§11, #12). Estos ejemplos existen para **validar el tono "muy humano"**, no para aprobar texto. Placeholders `[entre corchetes]` = campos de personalización (§8.4). Nombre de marca ficticio "30X · [Programa]".

**TP1 — Recibimos tu aplicación (inmediato)**
> Hola [Nombre] 👋
> Recibimos tu aplicación al programa [Programa]. Gracias por tomarte el tiempo de contarnos sobre [objetivo declarado].
> Ahora entra a revisión: nuestro equipo la va a leer con calma y te escribimos en las próximas horas con una respuesta. No tienes que hacer nada por ahora.
> — [Nombre del remitente], equipo 30X

**TP2 — Estamos revisando tu aplicación (mismo día / mañana siguiente)**
> [Nombre], una actualización rápida.
> Estamos revisando tu aplicación. Me llamó la atención lo que escribiste sobre [dato real del formulario] — es justo el tipo de reto que trabajamos en [Programa].
> Estamos terminando de revisar los perfiles de esta semana. Te confirmo hoy/mañana. Gracias por la paciencia.
> — [Nombre del remitente]

**TP3 — ¡Fuiste admitido! (pivote — personalizado)**
> [Nombre], tengo buenas noticias 🎉
> Fuiste admitido al programa [Programa].
> Revisamos tu perfil como [cargo — de LinkedIn/Apify si hay, si no del formulario] y tu objetivo de [objetivo declarado], y encajas con el grupo de esta cohorte. No admitimos a todos los que aplican, así que esto es real.
> Para asegurar tu cupo, mira este video corto y completa tu inscripción aquí 👉 [link de pago + VSL]
> Un detalle importante: los cupos de esta cohorte se cierran el **viernes**. Después de esa fecha liberamos el lugar para el siguiente en lista.
> — [Nombre del remitente]

**TP4 — Recordatorio 1 (día siguiente)**
> [Nombre], tu cupo en [Programa] sigue reservado, pero quería avisarte que no queda apartado indefinidamente.
> Si tienes alguna duda antes de inscribirte, respóndeme por aquí y te ayudo. Tu lugar 👉 [link]

**TP5 — Recordatorio 2 (~2 días antes del cierre)**
> [Nombre], se acerca el viernes ⏳
> Ese día cerramos las inscripciones de esta cohorte de [Programa] y liberamos los cupos que queden. Si quieres entrar, este es el momento: [link]
> ¿Algo te está frenando? Escríbeme y lo resolvemos hoy.

**TP6 — Último aviso (viernes, mañana)**
> [Nombre], hoy es el último día.
> Esta noche cerramos las inscripciones de [Programa] y tu cupo se libera. No es una táctica: es que la cohorte arranca y necesitamos cerrar el grupo.
> Si quieres entrar, asegura tu lugar ahora 👉 [link]. Si este no es tu momento, sin problema — gracias por haber aplicado.

### 8.4 Conteo de touchpoints: DEFINIDO en 6 (v0.5)

JJ lo llamó en su momento **"5 touchpoints"**, pero la **cadencia quedó definida en 6** (TP1+TP2 = recibimiento/revisión, TP3 = admisión, TP4+TP5+TP6 = 3 recordatorios) **+ llamatón el viernes**. La ambigüedad "5 vs. 6" venía de contar los recordatorios como 2 o 3; **JJ fijó la estructura en 6 toques** con los momentos de la tabla de §8.2.

La estructura narrativa estable es **4 momentos** — *Recibimiento · Revisión · Admisión + oferta · Cierre con urgencia (3 recordatorios)* — cerrando con el **llamatón** del viernes. El **motor mantiene el número de TPs como parámetro configurable** (RF-26) para permitir **A/B futuro** (§10.3, p. ej. probar 2 vs. 3 recordatorios), pero **la cadencia de arranque está decidida, no abierta**: lo que queda por afinar es el **copy fino** (§11 #12), no cuántos toques ni cuándo.

### 8.5 Personalización (forms + Apify/LinkedIn)

La personalización tiene **grados** y debe **degradar con elegancia** cuando falta información — nunca romperse ni exponer un campo vacío:

| Nivel | Fuente | Se usa en | Fallback si no hay dato |
|---|---|---|---|
| **N0 — Base** | Respuestas del formulario (nombre, programa de interés, rol, objetivo declarado) | Todos los TPs | Siempre disponible (es el mínimo para entrar) |
| **N1 — Contextual** | Derivados del form (industria, tamaño de empresa, urgencia declarada) | TP2, TP3 | Copy genérico pero cálido; nunca un token vacío tipo "Hola {{}}" |
| **N2 — Enriquecido** | LinkedIn vía Apify (cargo, seniority, empresa, señales públicas) — **sujeto a legalidad y consentimiento, ver §9** | TP3 (razón de admisión personalizada) | **Degrada a N1 sin que se note**; si no hay match o el scraping falla, el TP3 igual se envía a tiempo con personalización de formulario. El flujo **nunca** se bloquea esperando a Apify. |

> Regla de diseño: **la personalización es aditiva, no crítica.** Un TP3 sin enriquecimiento de LinkedIn debe verse bien igual. El scraping mejora el mensaje; no es un prerrequisito para enviarlo.

### 8.6 Guion del VSL (checkout)

VSL corto (objetivo `[A DEFINIR]`, sugerido 60–120 s) = el **video de felicitación por ser admitido** que vive en la **landing estilo VSL** enlazada desde el TP3 **por email** (por WhatsApp va el **link directo** al checkout). Guion **ilustrativo** a validar con Ventas/Marca (§11, #12):

**Guion (ejemplo, ~90 s):**
1. **Apertura — la admisión (0–10 s):** *"Hola [Nombre]. Si estás viendo esto, es porque fuiste aceptado al programa [Programa]. Felicitaciones — de verdad."* Reconoce que no todos entran; valida la decisión.
2. **Por qué tú (10–30 s):** *"Cuando revisamos tu aplicación vimos que quieres [objetivo declarado]. Ese es exactamente el punto de partida de las personas que mejor les va en este programa."* Conecta con lo que la persona declaró.
3. **Qué es y qué obtienes (30–75 s):** *"En [Programa] vas a [transformación central] en [formato/duración]. No es teoría: sales con [resultado concreto]."* Promesa central, formato, transformación — concreto, sin humo.
4. **Por qué ahora (75–100 s):** *"Los cupos de esta cohorte se cierran el viernes. No es un truco de marketing: arrancamos como grupo y necesitamos cerrar la lista para empezar bien."* La fecha límite real como consecuencia lógica de una admisión.
5. **Cierre + CTA (100–120 s):** *"Asegura tu cupo en el botón aquí abajo. Nos vemos adentro."* → botón de pago visible bajo el video, con las **dos opciones del checkout**: **pago completo con 10% de dto = $1.755 (destacada)** y **reserva de $200**.

> **Checkout bajo el video (§2.4):** se **destaca el pago completo ($1.755, 10% de dto)** para incentivar que cierren completo y **no vivir persiguiendo reservas** (menos cobranza); la **reserva de $200 (NO reembolsable, comunicado al lead)** queda como alternativa/red de seguridad, y su **saldo se acuerda la semana previa al inicio**. Motivo del incentivo: a diferencia de Growth Rockstar (reserva $95, drop-off reserva→completo ~5%), en **30X el drop-off es más alto históricamente**, por eso empujamos el pago completo. Por **WhatsApp** el TP3 lleva el **link directo** al mismo checkout (sin landing/VSL).

> Placeholders de producción: tomas, edición y variantes por programa = `[PLACEHOLDER]`. El VSL debe tener **una variante por programa** como mínimo; personalización 1:1 del video queda fuera de alcance v1.

### 8.7 Estados clave del aplicante (máquina de estados)

Cada aplicante tiene **un estado de ciclo de vida** y cada TP genera **estados de entrega**. Ambos se instrumentan (ver §10). Diagrama inline (fuente de verdad del embudo aplicación→pago):

```
                          ┌─────────────┐
        [form submit] ──▶ │   aplicó    │  (TP1 inmediato)
                          └──────┬──────┘
                                 ▼
                          ┌─────────────┐
                          │ en_revisión │  (TP2)
                          └──────┬──────┘
                                 ▼
                        ┌────── decisión de admisión (§11) ──────┐
                        ▼                                         ▼
                 ┌─────────────┐                          ┌──────────────┐
                 │  admitido   │  (TP3 + link pago)        │ no_admitido  │──▶ cierre
                 └──────┬──────┘                          └──────────────┘    respetuoso /
                        ▼                                   evento:            nurture
                 ┌───────────────┐                         no_admitido_notificado
                 │ oferta_enviada│  (TP4·TP5·TP6 recordatorios, urgencia → viernes)
                 └───┬───────┬───┬┘
          ┌──────────┘       │   └──────────┐
          ▼                  ▼              ▼
     ┌─────────┐        ┌─────────┐    ┌──────────┐
     │  pagó   │        │ expiró  │    │ opt_out  │
     │(terminal│        │(re-     │    │(terminal │
     │→ onbrd) │        │ oferta?)│    │ legal)   │
     └─────────┘        └─────────┘    └──────────┘

Regla dura: `pagó` u `opt_out` DETIENEN cualquier TP futuro (idempotencia + consentimiento).
```

- **Estado de aplicante (ciclo de vida):** `aplicó` → `en_revisión` → (`admitido` | `no_admitido`) → `oferta_enviada` → (`pagó` | `expiró` | `opt_out`).
- **Estado por touchpoint (entrega):** `programado` → `enviado` → `entregado` → `abierto` → `click` → (`pagó` | `expirado` | `opt_out` | `rebote/fallo`). Cada envío se instrumenta **por canal** (email y WhatsApp).
- **Llamatón del viernes:** actúa sobre los aplicantes en `admitido`/`oferta_enviada` **sin** `pagó` al llegar el cierre; sus resultados alimentan `pagó` (recuperado) o `expiró`/`opt_out`. Lo ejecuta el Agente de calls Emma (o una persona en la etapa inicial). Ver §8.2.

### 8.8 Prototipos (placeholders)

- Copys finales de TP1–TP6 por canal y programa: `[PLACEHOLDER — Figma / doc de copy]` (ejemplos ilustrativos ya en §8.3)
- Página de checkout con VSL: `[PLACEHOLDER — prototipo]`
- Vista de instrumentación / embudo por TP: `[PLACEHOLDER — tablero]`

---

## 9. Dependencias, riesgos y supuestos

### 9.1 Dependencias y riesgos

> **Severidad = probabilidad × impacto**, escala Alta / Media / Baja. Ordenada de mayor a menor severidad para saber qué atacar primero. Cada fila trae un **checkpoint** (fase antes de la cual debe estar mitigado).

> ⚠️ **Paso previo transversal (antes de F0, obligatorio):** **validar con Emmy lo ya montado.** JJ: *"Emmy ya había montado esto."* Existe una versión previa del flow/formulario; este PRD documenta el **delta**, no reinventa. Antes de construir, revisar con **Emmy** (versión previa + bugs de precio + personalización), **Mariana Cerón** (checkout) y **Juan Ortega** (formulario/LinkedIn) qué está montado y qué falta. **La cadencia/copy la define JJ** (ya definida, §8) — no es un build previo que validar. Sin este paso, se corre el riesgo de reconstruir lo existente.
>
> ℹ️ **Recordatorio de responsabilidades (RACI, §0.1):** **JJ es Owner/DRI de todo**; los roles de la columna "Responsable" abajo son **apoyo** sobre su pieza. El paso 0 que destraba el build es **JJ pasando el PRD a Tech (Beto+Emmy)** (§10.0).

| Sev. | Tipo | Descripción | Mitigación | Responsable | Checkpoint |
|---|---|---|---|---|---|
| **ALTA** | **Riesgo — Tono robótico / percepción de spam** *(riesgo #1)* | 6 mensajes automatizados con urgencia pueden leerse como spam de marketing, rompiendo la promesa de admisión y quemando la relación (y el CAC ya gastado). | Copy revisado por Ventas/Marca; personalización real (§8.5) que pruebe que se leyó la aplicación; honestidad en las promesas (no afirmar revisión humana si no la hay); cadencia y nº de TPs por A/B (§10); STOP/opt-out fácil en cada mensaje; **kill-switch con gatillo definido (§10.2)**. | Ventas + Marca (copy) · Producto (controles) | Antes de F1 |
| **ALTA** | **Dependencia — Apify (scraping LinkedIn)** | (a) **legalidad/ToS de LinkedIn y protección de datos** (uso de datos personales sin base legal); (b) rate limits / bloqueos; (c) cobertura parcial. | Tratar N2 como **aditivo, nunca bloqueante** (§8.5): TP3 se envía a tiempo sin LinkedIn. **N2 arranca APAGADO**; se enciende solo con visto bueno legal (base legal, aviso de privacidad, minimización). Cache y colas para rate limits; timeout duro → fallback a N1. Evaluar consentimiento explícito en el formulario. | Legal (base legal) · Producto (integración/fallback) | Antes de F2 (N2) |
| **ALTA** | **Riesgo — Criterio de admisión (el scoring base YA EXISTE; falta el criterio de exclusividad)** | El **scoring salesFlow ya existe** (rol + investment_capacity + urgency → tag Low/Med/High → HubSpot). Lo genuinamente abierto **no es el motor**, sino: (a) si se admite a **todos** o **por score**, y (b) sumar el criterio de **"exclusividad/viralidad"** de JJ para que se sienta selectivo. Si es por score hay una rama "no admitido" hoy inexistente; si entran todos, el copy "fuiste admitido" podría ser engañoso. | **Afinar** el scoring existente (no rehacerlo) + definir criterio de exclusividad/viralidad antes de F1 (§11 #3). Alinear copy con la verdad operativa. Evento `no_admitido_notificado` ya previsto (§10.4). | **Juan Ortega + Emmy** (formulario/scoring) + Ventas + Fundadores | Antes de F1 |
| **MEDIA** | **Dependencia — Checkout de pago (YA EXISTE)** | El pago del cupo **reusa el checkout existente** de LinkedIn Sales (Oracle30x sobre **Stripe**, `30x.com/checkout/linkedin` + `-discount`). **Ya NO es "elegir proveedor"**, sino **integrar** el motor de touchpoints con lo montado. Restricción org: no Vercel/Railway/Supabase. Riesgos residuales: caídas de Stripe, fricción de pago, conciliación tardía que reactive TPs a quien ya pagó, y el **desfase de precio** (RF-25b). | Integrar sobre el **webhook de pago confiable** de Stripe/Oracle30x → evento `pagó` casi en tiempo real para **detener TPs** (idempotencia). Monitoreo de disponibilidad; conciliación con Finanzas; cerrar RF-25b (consistencia de precio). | **Mariana Cerón** (checkout) + Finanzas + Producto | Antes de F0 |
| **ALTA** | **Dependencia — Emma Closer (WhatsApp) — EN DESARROLLO PARALELO** | El closing por **WhatsApp** se opera **por ahora vía el connector (producto de Emmy)**; el **Emma Closer** (rieles tipo Emma/Kapso/Treble) **está en desarrollo simultáneo, NO es un riel ya listo**. Hace **handoff a un closer humano**. Canal = **email Y WhatsApp** (ambos); email depende de deliverability (SPF/DKIM/DMARC, reputación). Riesgo: si el agente no está listo, la conversación de WhatsApp se cubre con el connector de Emmy o cae a manual. | Operar el interino con el **connector de Emmy**; coordinar cronograma del agente; definir el handoff a closer humano; mientras el agente no esté, cubrir WhatsApp con connector + **ruta manual (P4)**. WhatsApp: plantillas aprobadas, número verificado, ventana 24 h. Email: dominio autenticado, calentamiento, monitoreo de rebotes/spam. Instrumentar `entregado` vs `enviado` por canal. **Cadencia definida por JJ** (§8). | **Emmy** (connector/agente) — apoyo; Owner JJ + Growth | Antes de F1 |
| **ALTA** | **Dependencia — Agente de llamadas/voz para el llamatón (Juan Ortega) — EN CONSTRUCCIÓN** | El **llamatón del viernes** (recuperación de admitidos que no pagaron el día de cierre) lo conduce el **Agente de calls Emma que construye Juan Ortega**, hoy **en construcción**. **Su trabajo: llevar a pago** o **—si el lead lo necesita— agendar una reunión con el equipo comercial, presentado al lead como "equipo de admisiones"**. Por ser IA puede correr el mismo viernes. Riesgo: si no está listo, el llamatón no corre automatizado. | En la **etapa inicial** ejecutar el llamatón con una **persona**; migrar al agente cuando esté listo. Coordinar cronograma con Juan Ortega; instrumentar resultados de llamada (contactado/pagó/agendó con "equipo de admisiones"/no contesta/opt-out). | **Juan Ortega** (Agente de calls Emma) — apoyo; Owner JJ + Ventas | Antes de F2 (persona en F1) |
| **ALTA** | **Build/Dependencia — Motor de secuencias NUEVO en el producto** | La orquestación/scheduling de la cadencia es un **build NUEVO dentro del producto**: el **módulo de "campañas" actual NO sirve** para secuencias de admisión y **no** hay plataforma de mailing externa. El motor dispara TPs en tiempos relativos a `aplicó`, respetando ventanas y lógica temprano/tarde de TP2, con cortes pagó/opt-out/STOP. El **auto-checkout con Dapta** sí se reusa/integra. Riesgo: subestimar el build por creer que se "reusa" el módulo actual; envíos a horas inapropiadas (madrugada). | Construir el motor (scheduling con zona horaria del aplicante, ventanas permitidas ancladas a la aplicación (RF-09b), colas idempotentes, reintentos con backoff, pruebas de carga para picos); integrar Dapta y el checkout existente, no reconstruirlos. **Entregable que destraba el build: JJ pasa el PRD a Tech (§10.0).** | **Tech (Beto + Emmy)** — apoyo; Owner JJ | Antes de F0 |
| **MEDIA** | **Dependencia/Build — Landing estilo VSL con video de felicitación** | Por **email**, el TP3 cae en una **landing estilo VSL con video de felicitación por ser admitido** + checkout; hay que **producir el video y la landing** (una variante por programa). Riesgo: sin landing/video, el toque de admisión por email pierde su pieza central. | Producir landing + video de felicitación; una variante por programa; el checkout se reusa (Oracle30x/Stripe) y expone las **dos opciones ($1.755 destacado / $200)**. Fallback: por WhatsApp va el **link directo** mientras se produce. En curso con **Maca Celis + Diseño**; **JJ graba el video el 1-oct** (§0). | **Diseño + Maca Celis** — apoyo; Owner JJ | Antes de F1 |
| **MEDIA** | **Riesgo — Reintentos y costo oculto de operación** | Por la metodología 30X: una instrucción se vuelve decenas de llamadas (Apify, envíos, webhooks). Reintentos y excepciones inflan el costo real por resultado verificado. | Instrumentar costo por resultado verificado (§10); límites de reintento; alertas de anomalías de volumen; QC de excepciones con dueño claro. | Producto + Finanzas | Antes de F2 |
| **MEDIA** | **Riesgo — Carga de revisión humana (excepciones)** | El costo caro no es el modelo sino revisar excepciones (fallos de scraping, rebotes, casos límite). Sin dueño, degrada la calidad. | Definir quién revisa qué y con qué umbral de acierto (pregunta clave de la metodología). Diseñar para minimizar excepciones (fallbacks automáticos). | Ventas (operación) | Antes de F1 |
| **BAJA** | **Riesgo — Cambio de proceso en el equipo** | Ventas pasa de seguimiento manual a supervisar un motor; resistencia o mal uso puede anular el beneficio. | Onboarding del equipo; documentar el nuevo rol (supervisar, no ejecutar); dashboard claro; rollout gradual (§10). | Ventas | Antes de F3 |
| **BAJA** | **Riesgo — Canibalización del pipeline actual de closers** | El flujo automatizado podría percibirse como que "le quita" leads al pipeline humano de cierre sobre agenda calificada (que hoy funciona bien). | **Diseñar aditivo, no sustitutivo (§2.1/§5 B14):** el motor actúa sobre los aplicantes que hoy se pierden en el seguimiento manual; **no reasigna ni desvía** la agenda calificada de los closers. Medir que el pipeline humano **no cae** al activar el feature (métrica de guarda operativa). | JJ + Ventas | Antes de F1 |

### 9.2 Supuestos (a validar — NO son hechos)

- El evento `aplicó` es capturable de forma fiable y en tiempo real desde la app de campañas / formularios. `[SUPUESTO]`
- Existe consentimiento suficiente en el formulario para contactar por el/los canal(es) elegidos. `[SUPUESTO — validar con Legal]`
- El proveedor de pago emite un webhook de confirmación fiable y oportuno para detener TPs. `[SUPUESTO]`
- El volumen de aplicaciones cabe dentro de los rate limits de Apify y de las cuotas de WhatsApp/email. `[SUPUESTO]`
- La fecha límite "viernes" es un cierre real y verificable (no fabricado), coherente con la operación de cada programa. `[SUPUESTO]`
- La personalización de nivel N1 (solo formulario) es suficiente para que el TP3 se sienta "de admisión" aun sin LinkedIn. `[SUPUESTO — a probar en A/B]`
- Los umbrales del gatillo del kill-switch (§10.2) son valores de arranque a calibrar con datos reales de F1. `[SUPUESTO]`
- El **Emma Closer** y el **Agente de calls Emma del llamatón (Juan Ortega)** estarán disponibles según su cronograma de desarrollo paralelo; mientras no lo estén, WhatsApp y el llamatón operan con **persona/manual**. `[SUPUESTO — coordinar cronogramas]`

---

## 10. Plan de lanzamiento y medición

### 10.0 Orden y dependencias / qué destraba qué (flujo PM)

Secuencia de construcción vista como PM: qué es cimiento, qué corre en paralelo y qué depende de qué. **Owner de todo = JJ** (§0.1); los roles nombrados son apoyo.

0. **Destraba todo:** **JJ pasa el PRD a Tech (Beto + Emmy)** → habilita construir el motor. Es el entregable que abre el resto.
1. **Bloqueante / cimiento:** **Motor de secuencias en el producto** (apoyo Tech/Beto+Emmy). Sin esto no corre nada — es el corazón nuevo del feature (scheduling, estados, cortes pagó/opt-out/STOP).
2. **En paralelo (con el motor):** **cadencia + copy** (JJ define — ya definida, queda copy fino) · **landing VSL** (JJ + Diseño + Maca Celis) · **personalización** (Apify + formulario; apoyo Tech/Emmy).
3. **Conectar el checkout** (ya existe, apoyo Mariana Cerón) **al motor**.
4. **Emma Closer** (en desarrollo) → por ahora **por el connector de Emmy** (WhatsApp).
5. **Llamatón de cierre** (apoyo Juan Ortega, Agente de calls Emma) — recuperación del viernes.
6. **Métricas + dashboard** (apoyo Apelis) — medir la conversión aplicación→pago vs. baseline propio, apuntando a la brecha **3% → ~18%** (el **~18% es la conversión real validada de GR**, §2.4).

> Lectura rápida: **0 y 1 son secuenciales y bloqueantes**; **2 corre en paralelo al motor**; **3–6 se enganchan a medida que el motor existe**. El único paso que solo depende de JJ (y destraba a todos) es el **paso 0**.

### 10.1 Fases de lanzamiento

> Cronograma tentativo anclado a hoy (2026-09-30). Fechas objetivo, no compromisos: se confirman al cursar el PRD.

| Fase | Alcance | Criterio de salida | Target |
|---|---|---|---|
| **F0 — Interno / dry-run** | Flujo completo en modo prueba con datos internos; sin envíos a aplicantes reales. Validar scheduler, estados, webhook de pago, fallbacks de Apify, gatillo del kill-switch. | Máquina de estados y detención por `pagó`/`opt_out` funcionan al 100%; instrumentación emite todos los eventos (incl. `no_admitido_notificado`); kill-switch dispara en simulacro. | ~2026-10-08 |
| **F1 — Piloto (1 programa, email + WhatsApp, volumen bajo)** | Un solo programa; **email Y WhatsApp**; % pequeño del tráfico detrás de **feature flag**. Personalización N0/N1 (**Apify/N2 APAGADO**). El **Emma Closer y el llamatón pueden operar con persona** si los agentes aún no están listos. | Costo por resultado verificado calculable; sin incidentes de deliverability/legal; señal de conversión ≥ línea base manual. | ~2026-10-15 |
| **F2 — Expansión controlada** | Más programas y/o segundo canal; activar A/B (§10.3); habilitar N2 (Apify) **tras visto bueno legal**. | Costo por resultado verificado **baja** con el volumen (condición de la metodología para escalar); métricas ancla estables. | ~2026-11 |
| **F3 — General** | Todos los programas y aplicantes; flujo por defecto. | Repago dentro del objetivo; operación con dueño de excepciones definido. | ~2026-12 |

### 10.2 Feature flags, kill-switch y reversión

- **Feature flags:** por **campaña/programa**, por **canal**, por **touchpoint individual** (apagar TP4–TP6 sin tocar TP1–TP3), y por **nivel de personalización** (apagar Apify/N2 al instante).
- **Kill-switch global:** detiene todos los envíos programados de inmediato. **No es solo manual: tiene gatillos automáticos.** Se dispara (auto-pausa + alerta a operación, §9) cuando en una ventana móvil cualquiera de estos supera su umbral — **valores `[SUPUESTO — calibrar en F1]`**:
  - **Tasa de quejas/spam** (marcas "esto es spam" en email o reportes en WhatsApp) **> X%** de los entregados → `X ≈ 0.1%` como punto de partida (referencia de higiene de email).
  - **Tasa de rebote/fallo de entrega > Y%** de los enviados → `Y ≈ 5%`.
  - **Tasa de opt-out/STOP > Z%** de los entregados en la ventana → `Z ≈ 2%`.
  - **Pagos disputados/reversados > W%** de los pagos → `W ≈ 1%`.
  - **Anomalía de volumen** (envíos > N× el baseline por reintentos descontrolados) → freno de seguridad.
  El kill-switch también es accionable **manualmente** por cualquier responsable de §9 ante un incidente cualitativo (p. ej. un copy que suena mal). Reactivar exige revisión humana de la causa.
- **Plan de reversión:** al desactivar el flag, los aplicantes en curso (a) se congelan sin más TPs, o (b) caen al seguimiento manual previo. La política de qué pasa con los "en vuelo" al revertir = decisión operativa (§11, #10). El estado previo (seguimiento manual) sigue disponible como fallback en F1–F2.

### 10.3 Experimentos A/B

Con volumen suficiente (F2+), probar de a una variable:
- **Copy del TP3** (razón de admisión, longitud, grado de personalización).
- **Timing** (T+ de TP3; hora de envío; cadencia de recordatorios).
- **Número de recordatorios** (2 vs 3 → resuelve empíricamente el debate 5 vs 6 TPs, §8.4).
- **Peso por canal** (qué canal —email/WhatsApp— origina el clic/pago; ambos salen siempre por diseño) donde aplique.
- **VSL** (con/sin, longitud, guion).

> Regla: cambiar **una** variable por experimento; métrica de decisión = conversión aplicación→pago del brazo, no aperturas/clicks (métricas intermedias, no ancla).

### 10.4 Instrumentación por touchpoint (eventos)

Cada TP emite eventos con `aplicante_id`, `campaña_id`, `programa`, `touchpoint_id`, `variante_ab`, `canal`, `nivel_personalización`, `timestamp`:

`programado` → `enviado` → `entregado` → `abierto` → `click` → (`pagó` | `expirado` | `opt_out` | `rebote/fallo`).

**Eventos de ciclo de vida / ramas:**
- `no_admitido_notificado` — dispara cuando la lógica por score marca `no_admitido` y se envía el cierre respetuoso; permite medir la rama "no admitido" del embudo (§8.7) aunque hoy arranque desactivada.
- `apify_ok` / `apify_fallback` — mide dependencia y cobertura de LinkedIn (§8.5).
- `webhook_pago_recibido` — latencia de detención tras el pago.
- `tp_detenido_por_pago` — verifica idempotencia (no se pide pago a quien ya pagó).
- `kill_switch_disparado` (con `motivo`/`umbral`) — auditoría de auto-pausas (§10.2).

Estos alimentan el **embudo por touchpoint** (dónde se cae la gente, §2) y el cálculo de las métricas ancla.

### 10.5 Cómo se miden las métricas ancla (metodología de ROI de 30X)

- **Costo por resultado verificado** = costo total de operar el motor (Apify **~$0.31/perfil**, recurrente sobre el **100% de aplicaciones** al ser LinkedIn obligatorio ≈ **$340–$490/mes** a volumen actual de LinkedIn Sales (§3.5.3) — × factor de reintento `[SUPUESTO]` + envíos WhatsApp/email + checkout + scheduling + **reintentos** + **revisión humana de excepciones**) ÷ **cupos pagados válidos que pasaron QC** (cupo asegurado por **reserva $200 o pago completo $1.755/$1.950**, confirmado por webhook, no reversado; ver definición §2.4). Es la única métrica que no mejora bajando la calidad. Se reporta por programa y por cohorte semanal (apoyo: Apelis). `[el precio unitario de Apify y el costo del enriquecimiento de la base ya son reales; el resto de valores = pendientes hasta F1]`
- **Período de repago** = en cuántos meses el ingreso incremental de cupos pagados atribuibles al motor cubre el costo de construcción + operación. `[pendiente hasta tener línea base F1]`
- **Conversión aplicación→pago** = `pagó` ÷ `aplicó` (y su versión por-admitido si hay score), comparada contra la **línea base del seguimiento manual** (medida en F0/F1). Es la métrica de decisión de los A/B.
- **Guarda contra el sesgo de supervivencia:** solo se declara ROI si el costo por resultado verificado **baja con el volumen**; si no es calculable, esto es una **APUESTA** que autorizan los fundadores (no se fabrican números).

---

## 11. Preguntas abiertas

> Cada fila con **responsable + fecha límite real** (relativa a fase, con target de calendario tentativo desde hoy 2026-09-30). Las **bloqueantes** van primero y con fecha más cercana. **Nota v0.3:** varias que estaban abiertas ya se cerraron o degradaron con los hallazgos de §0 — el **proveedor de pago** (checkout ya existe) pasó de "definir" a "reusar". **Nota v0.4:** el **canal quedó decidido = email Y WhatsApp** (ya no es "elegir"); el **motor de secuencias es un build NUEVO en el producto** (no "afinar el módulo actual", que no sirve para admisión); y aparecen **dependencias de cronograma nuevas** (**Emma Closer** y **Agente de calls Emma de Juan Ortega**, ambos en desarrollo paralelo). Lo **genuinamente abierto** sigue siendo: **criterio de exclusividad/viralidad** (Q3), **baseline propio** de aplicación→pago (Q8) y **legalidad del scraping** (Q5). **Nota v0.5:** la **cadencia quedó DEFINIDA por JJ** (6 toques + llamatón, §8) — ya no es pregunta abierta; lo que queda es **pulir el copy fino** (Q12, en revisión). El **RACI** (§0.1) fija que **JJ es owner de todo** y reasigna apoyos (Tech/Beto+Emmy, Diseño+Maca Celis, Apelis); el **checkout** cierra con **dos opciones ($1.755 destacado / $200)**; y el **~18%** es la **conversión real VALIDADA de GR** — referencia/meta direccional hacia la que apuntamos (§2.4), midiendo baseline propio (M1).

| # | Pregunta / Decisión | Responsable | Fecha límite |
|---|---|---|---|
| 2 | **Canal — CERRADO en v0.4: email Y WhatsApp** (ambos, cada touchpoint por los dos). **Cadencia CERRADA en v0.5 (definida por JJ).** Lo que queda abierto es la **disponibilidad/cronograma del Emma Closer** (WhatsApp; interino vía **connector de Emmy**; agente en desarrollo paralelo) y su handoff a closer humano. | **Emmy** (connector/agente) — apoyo; Owner JJ + Producto | Antes de kickoff F1 — **target 2026-10-03** |
| 3 | **Admisión — afinar el scoring existente + criterio de exclusividad:** el **scoring salesFlow (rol+capacidad+urgencia) ya existe**. Lo abierto: ¿se admite a todos o por score?, y **el criterio de "exclusividad/viralidad"** de JJ para que se sienta selectivo. Si es por score, ¿rama "no admitido" y cómo evitar que "fuiste admitido" sea engañoso? *(bloqueante)* | **Juan Ortega + Emmy** (formulario/scoring) + Ventas + Fundadores | Antes de kickoff F1 — **target 2026-10-03** |
| 8 | **Magnitudes del embudo** (aplicaciones/semana, **baseline propio de aplicación→pago** — no el 3% global, ventana de decisión) — línea base para el caso ROI. *(Precios ya fijados: $1.950 lista / $1.755 con 10% de dto / reserva $200, §2.4.)* | JJ + Datos/HubSpot + **Apelis** (métricas/dashboard) | Antes de kickoff F1 — **target 2026-10-03** |
| 13 | **Quién cursa el PRD** (Danilo, Alejandra, Dilan o Andrés) y aprobación del caso como inversión o como **apuesta** | Fundadores | Antes de kickoff F1 — **target 2026-10-03** |
| 6 | **~~Proveedor de pago~~ → CERRADO: se reusa el checkout existente** (Oracle30x sobre Stripe, `30x.com/checkout/linkedin`). Lo que queda abierto es solo: (a) la **integración** con el motor de touchpoints (RF-21, con Mariana Cerón), (b) cerrar el **desfase de precio** (RF-25b) y (c) la **expiración del cupo** (¿viernes fijo o por cohorte?). *(F0)* | **Mariana Cerón** + Finanzas + Producto | Antes de F0 dry-run — **target 2026-10-06** |
| 4 | **Motor de secuencias — es un BUILD NUEVO en el producto** (el módulo de "campañas" actual no sirve; no hay mailing externo). Se **integra** el auto-checkout Dapta y el checkout existente, no se reconstruyen. Lo abierto: zona horaria del aplicante, ventanas permitidas, lógica temprano/tarde de TP2, y el **umbral de "semana suficiente"** para anclar la ventana a la aplicación (E19/RF-09b: cuántos días mínimos antes del viernes para asignar la ventana de esa semana vs. la siguiente). *(F0)* | **Tech (Beto + Emmy)** — apoyo; Owner JJ | Antes de F0 dry-run — **target 2026-10-06** |
| 1 | **Nº y secuencia exactos de touchpoints** (¿5 o 6? ¿2 o 3 recordatorios?) — decisión inicial para F1; final por A/B en F2 (§8.4, §10.3) | Ventas + Producto | Inicial antes de F0 — **target 2026-10-06**; final en F2 |
| 7 | **Profundidad de personalización** y comportamiento exacto sin LinkedIn (¿N1 basta para el TP3?) | Ventas + Producto | Antes de F1 piloto — **target 2026-10-13** |
| 12 | **Pulir copy fino de TP1–TP6** (la cadencia ya está definida, §8; los **copys están en revisión**); **guion y variantes del VSL** por programa; ¿VSL obligatorio o A/B con/sin? | **JJ** + Ventas/Marca (copy) · **Maca Celis + Diseño** (VSL) | En revisión — **target 2026-10-13** |
| 11 | **Dueño de revisión de excepciones** y umbral de acierto aceptable (pregunta clave de la metodología de 30X) | Ventas (operación) | Antes de F1 piloto — **target 2026-10-13** |
| 10 | **Manejo de aplicantes "en vuelo" al revertir/apagar** el flag (congelar vs. pasar a manual) | Producto + Ventas | Antes de F1 piloto — **target 2026-10-13** |
| 5 | **Legalidad del scraping LinkedIn (Apify):** base legal, ToS, consentimiento, minimización, aviso de privacidad — **bloqueante para encender N2**; NO bloquea F1 (N2 apagado) | Legal | Antes de F2 (N2) — **target 2026-10-31** |
| 9 | **Política de re-oferta** para aplicantes en estado `expirado` (¿se recuperan? ¿cómo?) | Ventas | Antes de F2 — **target 2026-10-31** |
| 14 | **Cronograma del Emma Closer** y del **Agente de calls Emma (Juan Ortega)** — ambos en desarrollo paralelo; definir qué corre con agente vs. con persona en F1/F2 | Producto + Juan Ortega + equipo Emma | Antes de F1 — **target 2026-10-13** |
| 15 | **Llamatón del viernes:** su trabajo = **llevar a pago** o **agendar reunión con el equipo comercial (presentado al lead como "equipo de admisiones")**; confirmar que corre el mismo viernes (IA) vs. persona en etapa inicial; guion de llamada; lista de admitidos-no-pagaron y su instrumentación | **Juan Ortega** — apoyo; Owner JJ + Ventas | Antes de F2 — **target 2026-10-31** |
| 16 | **Producción de la landing estilo VSL + video de felicitación** (una variante por programa) para el toque de admisión por email — **en curso**; **JJ graba el video el 1-oct** | **Diseño + Maca Celis** — apoyo; Owner JJ | En curso — **target 2026-10-13** |

---

## 12. Registro de cambios

| Versión | Fecha | Estado | Autor | Cambios |
|---|---|---|---|---|
| **v0.1** | 2026-09-30 | Borrador | Juan José Sarmiento | Versión inicial del PRD (todas las secciones). Cifras de embudo y ROI marcadas como supuestos/pendientes; decisiones clave abiertas en §11. Incluye la auditoría aplicada a §8–§12: (1) fechas límite reales en las 13 preguntas abiertas, priorizadas por fase; (2) gatillo automático del kill-switch con umbrales X/Y/Z/W supuestos; (3) evento `no_admitido_notificado` para la rama no-admitido; (4) columna de severidad + checkpoint en tabla de riesgos; (5) ejemplos reales de copy TP1–TP6 y guion del VSL; (6) diagrama de máquina de estados inline (ASCII). |
| **v0.2** | 2026-09-30 | Borrador | Juan José Sarmiento | **Incorporación de la Sección 0 (hallazgos de Slack): "lo que YA existe vs. el delta a construir".** Cambio mayor de esta versión: documenta que el feature no arranca de cero (checkout Oracle30x/Stripe, flow piloteado, Apify ~$0.31/perfil, scoring salesFlow, WhatsApp/Setter Agent, Dapta ya existen), nombra a los dueños asignados (Mariana Cerón, Cristina, Juan Ortega, Emmy) y fija los datos confirmados (reserva $200, ticket $1,950, baseline ~3%→~18%). |
| **v0.3** | 2026-09-30 | Borrador — **LISTO PARA CURSAR** | Juan José Sarmiento | **Reconciliación de coherencia interna** (6 must-fix de la auditoría FINAL, sin rediseño): (1) proveedor de pago **cerrado** — se reusa el checkout existente (RF-21, §9, §11 Q6); (2) baseline del embudo propagado y **aclarado** — el ~3% es lead→venta global (otro denominador), M1 mide baseline propio con el ~18% de GR como techo (§2.4, §3.2); (3) costo de Apify **~$0.31/perfil** (dato real) en el stack; solo el factor de reintento sigue `[SUPUESTO]` (§3.5.3, §10.5); (4) **ticket $1,950 / reserva $200** fijados y **definición de "cupo pagado válido"** = reserva de $200 confirmada, no reembolsada (§2.4, M2/M3); (5) canal/admisión/scheduler reformulados como **"reusar/afinar lo existente"** (§11 Q2/Q3/Q4); (6) **nuevo RF-25b**: consistencia de precio landing↔checkout ($1,500 vs $1,950) + fallback `_tbd` $1,650 por `start_date_30x` faltante. Menores: fecha unificada a 2026-09-30, responsables reales nombrados en §9/§11, y paso previo "validar con Emmy lo ya montado" antes de F0. |
| **v0.4** | 2026-09-30 | Borrador — **LISTO PARA CURSAR** | Juan José Sarmiento | **Alineamiento con las decisiones recientes de JJ** (ediciones quirúrgicas, sin rediseño): (1) **es un feature NUEVO a construir DENTRO del producto** — ya no hay plataforma de mailing externa y el **módulo de "campañas" actual NO sirve** para secuencias de admisión; el motor vive en el producto (§0, §1, §2.2, nuevo **RF-00**, §9 fila de build nuevo, §11 Q4); (2) **canal = email Y WhatsApp** (cada touchpoint por ambos), no "sobre todo WhatsApp" (§0, §1, §5 A15, **RF-35/RF-36**, §8.2, §11 Q2 cerrada); (3) **Emma Closer** (WhatsApp, rieles Kapso/Treble, handoff a closer humano) en **desarrollo paralelo** — dependencia, no riel listo (§0, §4, §5 B9, **RF-35b**, §9, §11 Q14); (4) **email → landing estilo VSL con video de felicitación** + checkout; **WhatsApp → link directo** (§1, §4, §5 A4, **RF-22**, §8.2/§8.6, §9, §11 Q16); (5) **llamatón el propio viernes** (recuperación de admitidos que no pagaron) conducido por el **Agente de calls Emma de Juan Ortega** (en construcción) o persona en etapa inicial — no la semana siguiente (§0, §3.4, §4, §5 A16/B13, **RF-35d**, §8.2/§8.7, §9, §11 Q15). Se mantiene lo fijado en v0.3 (reserva $200, ticket $1,950, "cupo pagado válido", Apify ~$0.31/perfil, checkout Oracle30x/Stripe ya existe). Genuinamente abierto: exclusividad/viralidad, baseline propio, legalidad del scraping. |
| **v0.5** | 2026-09-30 | Borrador — **LISTO PARA CURSAR** | Juan José Sarmiento | **Alineación 100% con el playbook** (ediciones quirúrgicas, sin rediseño): (1) **RACI explícito** — **JJ es Owner/DRI de TODAS las piezas**; los demás son **apoyo** (Tech/Beto+Emmy = motor; Diseño+Maca Celis = landing VSL; Mariana Cerón = checkout; Juan Ortega = llamatón; Apelis = métricas; Emmy = personalización/connector). El entregable de JJ que destraba el build es **pasar el PRD a Tech** (nuevo **§0.1**, propagado a §9/§11). (2) **Estado y línea de tiempo** (**§0.2**): PRD listo, en espera de revisión con Tech, copys en revisión, landing VSL en curso con Maca Celis, **JJ graba el video el 1-oct**. (3) **Orden y dependencias** del lanzamiento — qué destraba qué (**§10.0**). (4) **Checkout con dos opciones**: **pago completo con 10% de dto = $1.755 (destacado, para no vivir persiguiendo reservas — menos cobranza)** o **reserva $200**; redefinidos "cupo reservado / pagado completo / pagado válido" (§2.4, RF-21, RF-25b, §8.6, A4). (5) **Cadencia DEFINIDA por JJ** = 6 touchpoints (email+WhatsApp) de "aplicó" al viernes + llamatón; copys en revisión (§8.2/§8.4, RF-26, §11 Q2/Q12). (6) **Robustez de la cadencia**: la ventana se ancla a la **aplicación, no a un viernes fijo**; sin semana suficiente → siguiente ventana con cadencia completa (nuevo **E19**, nuevo **RF-09b**). (7) **Llamatón** = llevar a pago o **agendar reunión con el equipo comercial, presentado al lead como "equipo de admisiones"** (§8.2, RF-35d, §9, §11 Q15). (8) **Dato real de Apify** para el ROI: pipeline "Ventas con LinkedIn" (906259304) = 5.871 aplicaciones, **952 con LinkedIn → ≈ $295 una sola vez** (608 que además pueden pagar ≈ $188; 747 dijeron poder pagar); el costo de enriquecimiento deja de ser `[SUPUESTO]` (§3.5.3, §10.5). (9) **Matiz del 18%**: es **referencia interna de Slack (d@30x, 18-sep), NO dato verificado de GR ni target duro**; la meta formal es subir la conversión aplicación→pago con **baseline propio** (§0, §2.4, §3.2 M1). Menores: nota de audiencia (PRD vía Danilo/Alejandra/Dilan/Andrés; playbook para Dylan y Andrés). |
| **v0.6** | 2026-09-30 | Borrador — **LISTO PARA CURSAR** | Juan José Sarmiento | **Marco y decisiones de reserva** (ediciones quirúrgicas, sin cifras inventadas): (1) **Marco:** el feature es una **versión 30X del flujo de admisión de Growth Rockstar** con **nuestras herramientas**; **empezamos por desarrollo de producto** (no hay mailing externo); aprovechamos **mayor contactabilidad vía WhatsApp** e **infra Emma** (encabezado, §0/§1). (2) **Renombre en todo el doc:** el agente de closing = **Emma Closer**; el agente de voz del llamatón = **Agente de calls Emma**. (3) **No canibaliza:** el flujo es **aditivo**, NO lastima el pipeline actual de los closers (agenda calificada, que funciona bien); automatiza admisión + cobro de los aplicantes que hoy se pierden (§2.1, §5 B14, §9 nuevo riesgo). (4) **Comparación GR vs 30X + política de reserva:** reserva GR **$95** / 30X **$200**; GR **no** incentiva el completo (drop-off reserva→completo ~5%), 30X sí (drop-off más alto) → **10% de dto = $1.755**; **reserva $200 NO reembolsable** (comunicado al lead); **pago completo se acuerda la semana previa al inicio** (§2.4, RF-21, §8.6, Apéndice A). (5) **18% de GR VALIDADO:** el ~18% es la **conversión real validada de Growth Rockstar**; deja de ser "por validar" y pasa a ser la **referencia/meta direccional** — la meta es **acercar nuestra conversión aplicación→pago hacia ese ~18%**, midiendo baseline propio (M1) (§0, §2.4, §3.2). Se mantiene todo lo demás de v0.5/v0.6 (RACI, timeline, orden/dependencias, cadencia + robustez, Apify ~$295). |


---


# Apéndice A — Referencia de flujo: Growth Rockstar

# Referencia de flujo comparable — Growth Rockstar (aplicación → admisión → pago)

Flujo real observado en Growth Rockstar (curso principal + Xtreme Growth AI), septiembre 2026. Es esencialmente el modelo que este PRD busca **sistematizar y automatizar con touchpoints personalizados**. Sirve como benchmark de forma.

## El flujo de Growth Rockstar
1. **Aplicar, no comprar:** el CTA es "APLICAR AHORA" / "Aplicar ahora con prioridad" → **formulario Typeform** (no checkout directo). La aplicación es un acto activo, no una compra.
2. **Revisión de perfil con LinkedIn:** el equipo "analiza LinkedIn y referencias". → **Valida directamente nuestra idea de scraping de LinkedIn (Apify)**: ellos ya revisan el LinkedIn del aplicante como parte de la admisión.
3. **Ventana de revisión "humana":** confirmación en **4–10 días hábiles**. → Es el equivalente de nuestro TP2 "estamos revisando tu aplicación" (percepción de revisión real y selectiva).
4. **Escasez explícita y repetida:** "Cupos limitados" (×4), "solo un pequeño porcentaje son seleccionadas", **máx. 100–200 cupos**, "una vez se llena el grupo, cerramos inscripciones". Escasez REAL, no inventada.
5. **Aplicación prioritaria:** quien asiste al webinar entra con prioridad ("tienes más chances de asegurar tu lugar"). Segmento con trato preferente.
6. **Reserva con anticipo:** se **reserva el cupo con un depósito** (observado ~$150 en esta página; **internamente se cita ~$95** para la comparación GR vs. 30X de §2.4 — cifra a confirmar) y el saldo se paga en cuotas antes del inicio. → Exactamente el patrón "aparta tu cupo con anticipo" (coincide con nuestra sección de objeciones/escasez del estudio). **Diferencia clave con 30X:** GR **no** empuja el pago completo (drop-off reserva→completo ~5%); 30X sí lo incentiva con 10% de dto ($1.755) por un drop-off más alto (§2.4).
7. **Urgencia por fecha fija + no reapertura:** fecha de inicio fija; "¿van a reabrir?" → no. Urgencia creíble anclada a una fecha.

## Cómo se mapea a nuestro feature (qué copiar / qué mejorar)
| Growth Rockstar (manual) | Nuestro feature (automatizado) |
|---|---|
| Aplicar por Typeform | TP1 "Recibimos tu aplicación" al enviar el formulario |
| Revisión LinkedIn + referencias (4–10 días) | TP2 "Estamos revisando" + scraping LinkedIn (Apify) para personalizar |
| Confirmación de admisión | TP3 "¡Fuiste admitido!" personalizado (forms + LinkedIn) |
| Reserva con depósito + saldo en cuotas | Link de pago → checkout con VSL; reserva del cupo con anticipo |
| Escasez (cupos) + fecha fija | TP4–TP6 urgencia real "hasta el viernes" |

**Ventaja de nuestro enfoque:** Growth Rockstar tarda 4–10 días y es manual; nosotros comprimimos el ciclo a horas con personalización automática y un flujo de pago con VSL — **más rápido y más personal a escala**, sin perder la sensación humana (ese es el riesgo #1 a cuidar: que no suene robótico).

## Piloto: arrancamos con el programa de VENTAS CON LINKEDIN
La primera implementación de este feature es para el **programa de Ventas con LinkedIn de 30X**. El "programa de …" del flujo, el VSL y el copy se instancian para LinkedIn Sales. Encaja con la auditoría de Growth Rockstar para venta en automático de LinkedIn Sales.

## Auditoría — Argumentos de AUTORIDAD que usa Growth Rockstar (para copiar el patrón)
- **Trayectoria / ediciones:** "edición 16 del Curso", "Luego de 4 años dando este curso".
- **Volumen de alumnos:** "+4.000 alumnos", "+1.100 rockstars se formaron", "+300 Alumnis", "+9 países impactados".
- **Logos de clientes como prueba:** "Casos de éxito reales: Rappi, Mercado Libre, Mural, Auth0, LinkedIn, +50 más"; "Nubank, Bitso, Ualá, Globant, Tiendanube… Google".
- **Red de mentores:** "+120 mentores te apoyan", "+100 mentores top de Latam".
- **Credencial del fundador:** "Dylan Rosemberg impulsó el crecimiento de +400 empresas y formó a +1.100 profesionales en Latam".
- **Testimonios:** carrusel de reseñas de LinkedIn.
- **Selectividad como autoridad:** "Miles de personas aplican cada año, y solo un pequeño porcentaje son seleccionadas".

## Auditoría — Cómo hacen sentir a la persona VISTA POR UN HUMANO (el corazón del "muy humano")
- **Revisión manual explícita del perfil:** *"Luego de que apliques, nuestro equipo analizará tu perfil de LinkedIn y las referencias que proporciones cuidadosamente."* → Es literalmente nuestro TP2 "estamos revisando" + el scraping de LinkedIn (Apify) para personalizar. La clave: DECIR que un humano miró su LinkedIn.
- **Selección deliberada:** "Nos tomamos extremadamente en serio el elegir a los perfiles que más provecho puedan obtener".
- **Voz personal del fundador (primera persona, emoción, firma real):** "Primero, gracias. ¡Me encanta eso!"; "Solo dar clic y enviar este email ya me emociona"; "Me hace sonreír pensar que un nuevo grupo de alumnos…"; "Saludos a todos, Dylan 👋". → Nuestros TP deben ir **firmados por una persona real** (el closer / JJ), en primera persona, con emoción.
- **1:1 y feedback personalizado:** "videollamadas 1:1 para trabajar en sus desafíos", "feedback personalizado".
- **Contacto humano con nombre:** "Contacta vía email a cristina@growthrockstar.com".
- **Tono conversacional en FAQ:** "¡Buena pregunta!", "¿Estás listo para dar el siguiente paso?".

### Traducción a nuestros touchpoints (LinkedIn Sales)
- **TP2 "revisando":** "Estoy revisando tu perfil de LinkedIn y tus respuestas personalmente" — firmado por una persona real; sensación de curaduría, no de bot.
- **TP3 "admitido":** abrir con **un detalle específico de su LinkedIn/forms** (prueba de que un humano lo vio) + stack de autoridad (X profesionales ya formados, logos, mentores) + selectividad ("de las aplicaciones de esta semana, fuiste seleccionado") + link a checkout/VSL.
- **VSL / checkout:** autoridad concentrada (resultados, alumni, logos, mentores) + felicitación personal.
- **Regla anti-robot:** primera persona, firma con nombre, un dato personal real por mensaje; nunca genérico.

**Nota de honestidad:** precios/cupos/credenciales citados son de Growth Rockstar (referencia externa pública), no metas ni claims de 30X.

Fuentes: growthrockstar.com/gr11-aplicacion-prioritaria-webinar · growthrockstar.com/xtreme-growth (revisado sep-2026).
