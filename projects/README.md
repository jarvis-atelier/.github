# Catálogo de Proyectos — Jarvis Atelier

Registro vivo del portfolio del estudio. **Acá no vive código** — solo metadata. El código de cada proyecto vive en su propio repo dentro de la org `jarvis-atelier`.

Este archivo es la fuente única de verdad sobre **qué proyectos tenemos, quién los maneja, en qué stack están y en qué estado se encuentran**. Mantenerlo actualizado es responsabilidad de todo el equipo.

---

## Antes de empezar — cómo funciona esto

> **TL;DR**: en GitHub no existen carpetas a nivel org. Cada proyecto es un **repo independiente**. La org `jarvis-atelier` es una lista plana de repos.

Si nunca trabajaste en una organización de GitHub, **leé esta sección antes de avanzar**. Es el concepto fundacional que evita confusiones a futuro.

### En GitHub no existen "carpetas" a nivel organización

La org `jarvis-atelier` no es una carpeta — es un **namespace** que agrupa repos. **Cada proyecto es un repo independiente.** No podés meter un repo dentro de otro, ni dentro de una "carpeta projects/".

Cuando entrás a `github.com/jarvis-atelier`, esa lista de repos que ves **es** el portfolio del estudio. No hay un nivel más abajo.

### Cómo se ve en la práctica

❌ **Esto NO se puede hacer en GitHub** (esta estructura no existe):

```
jarvis-atelier/
└── projects/
    ├── client-acme/
    │   ├── web/
    │   └── api/
    └── client-globant/
```

✅ **Esto sí — cada proyecto es un repo independiente:**

```
jarvis-atelier/   (lista plana de repos en la org)
├── client-acme-portal-web        ← repo independiente
├── client-acme-portal-api        ← repo independiente
├── client-globant-dashboard      ← repo independiente
└── product-jarvis-cli            ← repo independiente
```

Los guiones en el nombre **no crean carpetas**. Son solo una convención de naming para que la lista quede ordenada alfabéticamente y los proyectos del mismo cliente aparezcan agrupados visualmente.

### Ejemplo: arrancás el proyecto del cliente Acme

Te asignan el portal del cliente Acme, con frontend y backend separados. Conceptualmente, lo que hacés es:

1. Pedís aprobación al lead.
2. Creás **dos repos independientes** en la org:
   - `client-acme-portal-web` ← frontend
   - `client-acme-portal-api` ← backend
3. Configurás cada uno (topics, CODEOWNERS, branch protection en `main`).
4. Cloneás cada repo en tu máquina, donde te quede cómodo.
5. Codeás, abrís PRs, mergeás.
6. Sumás ambos repos al [Portfolio activo](#portfolio-activo) de este catálogo abriendo un PR.

Los pasos exactos están en [Cómo registrar un proyecto nuevo](#cómo-registrar-un-proyecto-nuevo) más abajo.

### Tu workspace local NO tiene relación con la estructura de la org

En tu máquina, organizás los clones como prefieras. Cada dev puede tener su propio orden:

```
C:\dev\jarvis\                   ← un dev
├── client-acme-portal-web\
├── client-acme-portal-api\
└── product-jarvis-cli\

~/Code/jarvis-atelier/           ← otro dev, totalmente válido
├── client-acme-portal-web/
└── docs/
```

Lo único que existe **oficialmente** son los repos individuales en GitHub. Tu carpeta local es tu organización personal y nadie te la audita.

### Errores frecuentes que vas a evitar leyendo esto

- ❌ "Voy a subir mi carpeta `client-acme/` al repo `.github`" → **No.** Cada proyecto es un repo separado en la org.
- ❌ "Voy a hacer un repo `projects` y meter todos los clientes ahí dentro" → **No.** Es exactamente lo que GitHub no te deja escalar bien (permisos, CI, history mezclado).
- ❌ "Voy a clonar todo el estudio en mi máquina" → **No hace falta.** Cloneás solo los repos donde laburás.
- ✅ "Voy a crear un repo `client-acme-portal-web` siguiendo la convención de nombres" → **Sí, así es.**

---

## Cómo registrar un proyecto nuevo

Cuando arranques un proyecto nuevo en la org, seguí estos pasos **en orden**:

1. **Pedí aprobación a un lead** antes de crear el repo. Necesitamos saber quién es el cliente o producto, owner principal y stack tentativo.
2. **Creá el repo** siguiendo la [convención de nombres](#convención-de-nombres-de-repos).
3. **Marcá visibilidad** (privado por default, salvo que sea OSS o producto público).
4. **Aplicá los topics** correspondientes (lenguaje, stack, tipo, cliente, estado). Ver [topics oficiales](#topics-oficiales).
5. **Elegí el template** correcto según el [árbol de decisión](#cómo-elegir-cuál-usar). Como mínimo siempre arrancás con `template-jarvis-base` (cimiento universal del atelier); si tu stack tiene template específico, ese ya viene con la base adentro. Hacelo con "Use this template" desde GitHub.
6. **Configurá CODEOWNERS** en `.github/CODEOWNERS` con los owners del repo.
7. **Configurá branch protection** en `main`: requerir PR + 1 approve + CI verde.
8. **Escribí el README** con sección Quickstart (ver [`CONTRIBUTING.md`](../CONTRIBUTING.md#setup-local)).
9. **Abrí un PR contra este archivo** sumando la fila correspondiente en [Portfolio activo](#portfolio-activo).

Sin paso 9, el proyecto no existe oficialmente. Si no está en este catálogo, no lo conocemos.

---

## Convención de nombres de repos

Formato:

```
<tipo>-<cliente|producto>-<rol>
```

**Tipos válidos:**

| Tipo        | Uso                                            | Ejemplo                       |
|-------------|------------------------------------------------|-------------------------------|
| `client-`   | Trabajo para un cliente externo                | `client-acme-portal-web`      |
| `product-`  | Producto propio del estudio                    | `product-jarvis-cli`          |
| `internal-` | Herramienta interna del equipo                 | `internal-billing-tools`      |
| `template-` | Template para arrancar nuevos proyectos        | `template-react-vite`         |
| `lib-`      | Librería reutilizable entre proyectos          | `lib-mp-sdk-wrapper`          |
| `config-`   | Configs compartidas (ESLint, Prettier, etc.)   | `config-js-base`              |

**Reglas:**

- Todo en minúsculas, separado por guiones.
- Si el proyecto tiene frontend + backend en repos separados, usá sufijo `-web` y `-api`.
- Si es fullstack en un solo repo (monorepo del proyecto), no agregues sufijo.
- El nombre del cliente lo definís con el lead — usalo consistente en topics, repo names y catálogo.

---

## Topics oficiales

Todo repo de la org **debe** llevar topics aplicables. Sin topics, no aparece en los filtros y nadie lo encuentra.

**Por lenguaje (`lang-*`):**

`lang-typescript`, `lang-javascript`, `lang-python`, `lang-html`, `lang-css`

**Por stack / framework (`stack-*`):**

`stack-react`, `stack-vite`, `stack-nestjs`, `stack-nextjs`, `stack-flask`, `stack-fastapi`, `stack-django`, `stack-astro`, `stack-eleventy`, `stack-static-html`, `stack-prisma`, `stack-postgres`

**Por tipo (`type-*`):**

`type-frontend`, `type-backend`, `type-fullstack`, `type-static-site`, `type-cli`, `type-bot`, `type-script`, `type-library`, `type-template`

**Por cliente / producto (`client-*` / `product-*`):**

`client-<nombre>`, `product-<nombre>` — uno por proyecto.

**Por estado (`status-*`):**

`status-active`, `status-maintenance`, `status-archived`

> Si necesitás un topic que no está en la lista, abrí un PR contra este archivo proponiéndolo. No inventes topics sueltos por repo, se nos desordena el filtro.

---

## Templates disponibles

Repos marcados como **Template repository**. Usalos con "Use this template" desde GitHub.

| Template                | Rol en el atelier                              | Stack que trae                                | Estado |
|-------------------------|------------------------------------------------|-----------------------------------------------|--------|
| `template-jarvis-base`  | Esqueleto universal stack-agnóstico            | Solo lo común: README skeleton, LICENSE (MIT), `.gitignore`, `.gitattributes`, `.editorconfig`, CI placeholder, dependabot, CODEOWNERS, pointers a SECURITY/CONTRIBUTING org-level | ✅ disponible |
| `template-jarvis-web`   | Default web/frontend del atelier               | React 18 + TypeScript + Vite 5 + Vitest 2 + ESLint 9 + Prettier 3, extiende `base` | ✅ disponible |
| `template-jarvis-api`   | Default backend del atelier                    | NestJS 10 + Prisma 5 + Postgres 16 + Jest + Supertest + Docker compose, extiende `base` | ✅ disponible |
| `template-flask`        | Default Python web del atelier                 | Python + Flask                                | _por crear cuando aparezca el segundo proyecto Flask_ |
| `template-static-html`  | Default sitio estático del atelier             | HTML/CSS estático (con o sin SSG)             | _por crear cuando aparezca el segundo sitio estático_ |

### Cómo elegir cuál usar

Antes de hacer "Use this template", respondé estas preguntas **en orden**:

**1. ¿Tu proyecto necesita interfaz web?**
- **No** (CLI, bot, script, integración B2B sin UI) → ir a la pregunta 2.
- **Sí** → ir a la pregunta 3.

**2. ¿Necesita backend HTTP en TypeScript/Node?**
- **Sí, NestJS + Prisma + Postgres** (default del atelier) → `template-jarvis-api`.
- **No, otro stack** (Python, Go, Flask, etc.) → arrancá con `template-jarvis-base` y armá tu setup encima. Cuando aparezca el segundo proyecto del mismo stack, extraemos un template específico.

**3. ¿Tu proyecto es solo frontend o también tiene backend propio?**
- **Solo frontend** (estático, SPA contra una API ajena, panel administrativo de un servicio externo) → `template-jarvis-web`.
- **Frontend + backend** → ir a la pregunta 4.

**4. ¿Repos separados (default) o monorepo (excepción)?**
- **Separados** (lo normal según [polyrepo](#convención-de-nombres-de-repos)) → creá **dos repos**: uno con `template-jarvis-web` (sufijo `-web`) y otro con `template-jarvis-api` (sufijo `-api`).
- **Monorepo** (caso justificado: producto propio chico, MVP unificado, deploy de un solo binario) → arrancá con `template-jarvis-base` y combiná las estructuras dentro de `apps/web/` y `apps/api/`. Ver [guía detallada](https://github.com/jarvis-atelier/docs/blob/main/starter-templates.md).

### Cuándo NO usar template

- **Experimento descartable** (< 1 semana, no va a producción) — `git init` y listo, sin ceremonia.
- **Spike técnico** que sabés que vas a tirar — ídem.
- **Fork de un proyecto open-source** — heredás la estructura del fuente. No fuerces la del atelier encima.
- **Stack que no calza con ningún template** y que sabés que es proyecto único — base + manual; no inventes un template para un stack que vas a usar UNA vez.

### Política de templates

Crear template para un stack solo cuando **ya haya al menos un proyecto del stack en producción** Y exista intención clara de hacer otro. No creamos templates anticipadamente — el primer proyecto de un stack se hace a mano, el segundo se templateiza.

**Excepción**: `template-jarvis-base` no es stack-template, es el **cimiento universal**. Existe desde día 1 porque cualquier repo del atelier lo necesita (README, LICENSE, .gitignore, line endings, CI scaffolding).

> **Más profundidad**: para entender la filosofía detrás de los templates, qué incluye cada uno, cómo extender la base, y cuándo hacer monorepo vs polyrepo, ver la guía completa en [`docs/starter-templates.md`](https://github.com/jarvis-atelier/docs/blob/main/starter-templates.md).

---

## Ciclo de vida de un proyecto

Todo proyecto pasa por estos estados. Cambiar de estado requiere actualizar:
1. El topic `status-*` del repo
2. La fila en este catálogo (mover de sección)

**`active`** → Desarrollo activo. Owner asignado, PRs frecuentes, deploy regular.

**`maintenance`** → No hay desarrollo nuevo. Solo se aplican bugfixes críticos y parches de seguridad. Owner sigue siendo responsable de responder en plazo razonable.

**`archived`** → Cerrado. El repo se marca como **archived** en GitHub (read-only). Nadie va a tocarlo más. Puede reactivarse si el cliente vuelve, pero hay que sacarlo de archive y revisar deps obsoletas.

---

## Quién aprueba qué

| Acción                            | Quién aprueba                  |
|-----------------------------------|--------------------------------|
| Crear repo nuevo                  | Lead                           |
| Cambiar a `maintenance`           | Lead + owner del proyecto      |
| Archivar proyecto                 | Lead                           |
| Reasignar owner                   | Lead + owner saliente y entrante |
| Agregar topic nuevo a la taxonomía | Lead (vía PR a este archivo)   |
| Cambiar convención de nombres     | Decisión de equipo             |

---

## Portfolio activo

Proyectos en desarrollo activo. Ordenado por fecha de inicio descendente.

| Proyecto | Repo | Cliente / Producto | Stack | Lenguaje | Owner | Inicio | Notas |
|----------|------|--------------------|-------|----------|-------|--------|-------|
| **CASA SALCO ERP** | [`client-casa-salco`](https://github.com/jarvis-atelier/client-casa-salco) | Casa Salco | Flask + SocketIO + Celery + Pydantic / React + Vite + TS + Tailwind + shadcn/ui / Tauri (Fase 2 POS) / PostgreSQL + SQLite + Redis | Python + TypeScript | @oarivas | 2026-05-04 | ERP multi-sucursal. Reingeniería del legacy Harbour. Hardware AFIP/Kretz/Systel. Deploy Railway/Fly. Default branch renombrado de `master` a `main` el 2026-05-09. |
| **AutoBit** | [`client-giuliano`](https://github.com/jarvis-atelier/client-giuliano) | Giuliano | Flask 3 + htmx + Jinja2 + SQLAlchemy 2 + Alembic + SQLite (con FTS5) + structlog + pytest | Python | @oarivas | 2026-05-05 | PMV Marketplace Automotriz (Perú) — conecta dueños de vehículos con talleres y tiendas de repuestos. PMV completo (10 lotes, 17 phases, ~150 tests). Default branch renombrado de `master` a `main` el 2026-05-09. |

---

## En mantenimiento

Proyectos sin desarrollo activo, pero soportados ante bugs críticos.

| Proyecto | Repo | Cliente | Owner | Última actividad | Notas |
|----------|------|---------|-------|------------------|-------|
| _(vacío)_ |  |  |  |  |  |

---

## Archivados

Proyectos cerrados. El repo está en estado **archived** en GitHub.

| Proyecto | Repo | Razón de archivo | Fecha de archivo |
|----------|------|------------------|------------------|
| _(vacío)_ |  |  |  |

---

## Mantenimiento de este archivo

Este catálogo se mantiene **a mano** por ahora. Cuando tengamos más de ~15 proyectos activos, vale la pena automatizar la generación de las tablas leyendo topics de los repos vía un GitHub Action programado. Por ahora, manual + disciplina alcanza.

Si encontrás inconsistencias (un repo que no está acá, un estado mal puesto, un owner desactualizado), **abrí un PR**. No esperes a que lo arregle otro.
