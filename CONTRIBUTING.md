# Cómo contribuir

Gracias por querer aportar a un proyecto de Jarvis Atelier. Esta guía cubre el flujo de trabajo que usamos en **todos** nuestros repos, sin importar el stack (Node, Python, sitios estáticos, lo que sea). Si algún proyecto tiene reglas adicionales, van a estar en su propio `CONTRIBUTING.md` y mandan sobre lo que dice acá.

## Antes de empezar

1. **Buscá si ya existe.** Revisá issues abiertos y cerrados antes de crear uno nuevo o ponerte a codear.
2. **Discutí cambios grandes primero.** Si vas a tocar arquitectura, agregar una dependencia pesada o reescribir un módulo entero, abrí un issue de discusión antes del PR. Nadie quiere ver 2000 líneas de diff que rechazar.
3. **Leé el README y la doc del proyecto.** Cada repo tiene su contexto: stack específico, convenciones, decisiones tomadas. No las pises sin entender por qué están.

## Setup local

**Cada proyecto documenta su setup en su propio `README.md`.** Como mínimo, todo repo de la org debe tener una sección **Quickstart** con:

- Cómo clonar e instalar dependencias
- Cómo configurar variables de entorno (referencia a `.env.example`)
- Cómo correr migraciones / seed (si aplica)
- Cómo levantar el proyecto en modo desarrollo

Comandos base orientativos según los stacks que usamos en el estudio:

**Node (React/Vite, NestJS):**

```bash
git clone https://github.com/jarvis-atelier/<repo>.git
cd <repo>
pnpm install
cp .env.example .env
pnpm dev
```

**Python (Flask):**

```bash
git clone https://github.com/jarvis-atelier/<repo>.git
cd <repo>
python -m venv .venv
source .venv/bin/activate     # en Windows: .venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env
flask --app app run --debug
```

**Sitio estático HTML:**

```bash
git clone https://github.com/jarvis-atelier/<repo>.git
cd <repo>
# Si tiene build step (Astro, Eleventy, Vite static):
pnpm install
pnpm dev
# Si es HTML puro: abrí index.html con Live Server o un http-server local
```

Si algún paso falla siguiendo el README del proyecto, **abrí un issue** en vez de hackear el setup. Si te falla a vos, le falla al próximo.

## Workflow de branches

Trabajamos con trunk-based + branches cortas. Nada de branches que vivan dos semanas.

- `main` — siempre desplegable
- `feat/<scope>-<descripcion-corta>` — nuevas features
- `fix/<scope>-<descripcion-corta>` — bugfixes
- `refactor/<scope>-<descripcion-corta>` — refactors sin cambio de comportamiento
- `chore/<descripcion>` — config, deps, tooling
- `docs/<descripcion>` — solo documentación

Ejemplos:
- `feat/auth-magic-link-login`
- `fix/checkout-mp-webhook-retry`
- `refactor/users-service-extract-query-builder`

## Convenciones de commits

Conventional Commits. Sin atribuciones automáticas de IA.

```
<tipo>(<scope opcional>): <descripcion en imperativo>

<cuerpo opcional con mas contexto>

<footer opcional con refs a issues>
```

Tipos: `feat`, `fix`, `refactor`, `docs`, `test`, `chore`, `perf`, `ci`, `build`, `style`.

Ejemplos:

```
feat(auth): agregar login con magic link
fix(checkout): reintentar webhook de Mercado Pago en caso de timeout
refactor(users): extraer query builder a un servicio dedicado
docs: actualizar README con instrucciones de Railway
```

Reglas:
- Imperativo: "agregar", no "agregado" ni "agrega".
- Una idea por commit. Si te cuesta resumirlo, probablemente son dos commits.
- El cuerpo explica el **por qué**, no el **qué** (el qué se ve en el diff).

## Tests

Antes de mandar PR:

- **Unit tests** para lógica nueva (servicios, utilidades, hooks, funciones puras).
- **Integration tests** para endpoints, flujos que tocan DB o servicios externos.
- **E2E** para flujos críticos (login, checkout, etc.) — solo si el proyecto los tiene configurados.
- **Coverage mínimo: 80%** sobre el código nuevo o modificado. No sobre el repo entero.

Comandos según stack (ejecutá los que correspondan al proyecto):

```bash
# Node / TypeScript
pnpm test
pnpm test:coverage

# Python
pytest
pytest --cov

# Sitio estático
# Validá que buildea correctamente y revisá manualmente los flujos.
# Si tiene tests configurados (Playwright, Cypress), corrélos.
```

Si el cambio es solo docs, config o assets estáticos, está bien decirlo en el PR y saltearse tests.

## Lint, format y typecheck

Cada stack tiene su toolchain. **Todo PR tiene que pasar el lint y el format del repo en el que está.**

```bash
# Node / TypeScript
pnpm lint
pnpm format:check
pnpm typecheck   # o tsc --noEmit

# Python
ruff check .
ruff format --check .
mypy .           # si está configurado

# HTML / CSS estático
pnpm prettier --check .
# htmlhint, stylelint según corresponda al proyecto
```

Si tu editor no formatea automáticamente, configurá las extensiones correspondientes (Prettier, ESLint, Ruff, etc.) antes de seguir. No vamos a aceptar PRs solo por formato.

## Pull Requests

1. **Una cosa por PR.** Si tu PR mezcla feature + refactor + bugfix, separalo.
2. **Llenar el template** que está en `.github/PULL_REQUEST_TEMPLATE.md`. No lo borres.
3. **Linkear issues.** Usá `Closes #123` o `Related to #456` en la descripción.
4. **Screenshots** si tocás UI (antes/después). Para flujos, GIF corto.
5. **Self-review** antes de pedir review humana. Leé tu propio diff línea por línea.
6. **PRs chicos.** Idealmente <400 líneas de diff. PRs gigantes se aprueban tarde y mal.
7. **Resolver conflictos** vos, no el reviewer. `git rebase main` antes de pedir review.

### Proceso de review

- Mínimo **un approve** de un maintainer antes de mergear.
- CI tiene que estar en verde (lint, typecheck, tests, build — los que aplique al stack).
- Comentarios marcados como `nit:` son opcionales; el resto, no.
- El autor mergea su propio PR (squash & merge por default, salvo que se acuerde otra cosa).

## Reportar bugs y proponer features

- **Bugs:** usá el template de bug report. Incluí pasos para reproducir, entorno y logs.
- **Features:** usá el template de feature request. Empezá por **el problema**, no por la solución.

## Decisiones de arquitectura

Para cambios grandes (nueva dependencia core, cambio de patrón, migración de servicio), abrí una **ADR** (Architectural Decision Record) en `docs/adr/` del proyecto correspondiente. Formato corto: contexto, decisión, consecuencias.

## Crear un proyecto nuevo en la org

Si vas a arrancar un repo nuevo en Jarvis Atelier, **leé primero** [`projects/README.md`](./projects/README.md). Ahí están las reglas de naming, topics, ownership y registro en el catálogo.

## Seguridad

¿Encontraste una vulnerabilidad? **No abras un issue público.** Seguí el proceso de [SECURITY.md](./SECURITY.md).

## Código de conducta

Todo aporte cae bajo nuestro [Código de Conducta](./CODE_OF_CONDUCT.md). Léelo antes de participar.

## Preguntas

Si algo no quedó claro, abrí un issue con label `question` o escribí al canal interno del equipo. Mejor preguntar dos veces que asumir mal.
