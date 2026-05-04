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
5. **Si existe template** del stack, usá "Use this template". Si no, copiá la estructura base de un proyecto similar.
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

| Template                    | Stack                              | Estado       |
|-----------------------------|------------------------------------|--------------|
| `template-react-vite`       | React + TypeScript + Vite          | _por crear_  |
| `template-nestjs-prisma`    | NestJS + Prisma + PostgreSQL       | _por crear_  |
| `template-flask`            | Python + Flask                     | _por crear cuando aparezca el segundo proyecto Flask_ |
| `template-static-html`      | HTML/CSS estático (con o sin SSG)  | _por crear cuando aparezca el segundo sitio estático_ |

**Política de templates:** crear solo cuando ya tengamos al menos un proyecto del stack en producción y exista intención clara de hacer otro. No creamos templates anticipadamente.

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
| _(primer proyecto va acá)_ |  |  |  |  |  |  |  |

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
