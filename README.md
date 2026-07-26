Página web del flujo de perfilamiento de vivienda: captura los datos del
lead paso a paso (la casa se va "construyendo" en pantalla a medida que
avanza) y muestra el resultado — proyectos sugeridos si el perfil es
viable, o caminos alternativos (arrendamiento, ahorro programado, mentoría
PerteneSER) si aún no lo es.

## Constitución del Proyecto

- **Propósito:** ayudar a un afiliado (o futuro afiliado) de Colsubsidio a
  entender, en minutos y sin jerga, si está listo para comprar vivienda hoy
  y qué camino concreto seguir si todavía no.
- **Piezas del sistema (repos separados):**
  1. **Esta página web** — el formulario y la pantalla de resultado.
  2. Un **simulador de WhatsApp** que replica el mismo flujo de forma
     conversacional.
  3. **SimCRM** — un dashboard para asesores comerciales que recibe cada
     lead perfilado vía webhook.
  4. El **motor de perfilamiento** (FastAPI, repo aparte) — centraliza
     todas las reglas financieras, de elegibilidad y de scoring. Esta
     página web solo **consume** su API (`/afiliados/{id}`, `/perfilar`);
     no implementa ninguna regla de negocio por su cuenta.
- **Reglas de comportamiento del agente** (tono, prohibición de
  alucinaciones, ruta de escape humana, transparencia ante el rechazo):
  ver [`CONSTITUCION.md`](./CONSTITUCION.md).
- **Documentación viva:** las reglas de negocio y el contrato de datos
  están documentados en [`AUTH.md`](./AUTH.md),
  [`FINANCIERO.md`](./FINANCIERO.md) e [`INVENTARIO.md`](./INVENTARIO.md).
  Cualquier cambio en el contrato del motor (`/perfilar`, `/afiliados`)
  debe reflejarse ahí antes que en el código.

## Specs

| Archivo | Contenido |
|---|---|
| [`AUTH.md`](./AUTH.md) | Cómo se identifica a un afiliado (sin login tradicional) |
| [`FINANCIERO.md`](./FINANCIERO.md) | Reglas del motor financiero (SMMLV, VIS/VIP, subsidios, scoring) |
| [`INVENTARIO.md`](./INVENTARIO.md) | Catálogo de macroproyectos y contrato real de `POST /perfilar`, incluyendo brechas conocidas frente al frontend actual |
| [`CONSTITUCION.md`](./CONSTITUCION.md) | Reglas de comportamiento para todo texto generado por el proyecto |

## Desarrollo local

Necesitas Node.js — [instálalo con nvm](https://github.com/nvm-sh/nvm#installing-and-updating).

```sh
git clone <this-repository-url>
cd <repository-name>
bun install   # o: npm i
bun dev       # o: npm run dev
```

## Construido con

- TanStack Start
- TypeScript
- React
- Tailwind CSS

---

Este proyecto se originó en [Lovable](https://lovable.dev); sigue
sincronizado con el editor si el repositorio está conectado.
