## ¿Qué hace este PR?

Explicá en 2-3 líneas qué cambia y por qué. Nada de "varios fixes" — sé concreto.

## Tipo de cambio

- [ ] Bug fix (cambio que arregla un problema existente)
- [ ] Feature (nueva funcionalidad)
- [ ] Refactor (cambio interno sin afectar comportamiento)
- [ ] Docs (documentación, comentarios, README)
- [ ] Chore / Config (build, deps, CI, tooling)
- [ ] Performance (mejora de rendimiento)
- [ ] Breaking change (rompe compatibilidad — explicá impacto abajo)

## Checklist

- [ ] Probé el cambio en local y funciona
- [ ] Agregué/actualicé tests (unit, integration o e2e según corresponda)
- [ ] Pasa el lint (`npm run lint` / `pnpm lint`)
- [ ] Pasa el typecheck (`tsc --noEmit`)
- [ ] Actualicé documentación si era necesario (README, comentarios, Notion, etc.)
- [ ] No dejé `console.log`, `TODO` huérfanos ni código comentado
- [ ] Variables de entorno nuevas están documentadas en `.env.example`
- [ ] Migraciones de Prisma generadas y revisadas (si aplica)
- [ ] Sin secrets hardcodeados

## Issues relacionados

- Closes #
- Related to #

## Screenshots / Videos

Si el cambio toca UI, adjuntá antes/después. Para flujos completos, un GIF o video corto vale más que mil palabras.

## Notas para el reviewer

¿Hay algo específico donde querés ojos? ¿Una decisión de arquitectura que dudás? ¿Un trade-off que conviene discutir? Acá es el lugar.

## Plan de deploy / rollback

Si requiere pasos especiales (correr seed, ejecutar migración, invalidar cache, configurar variable nueva en Railway/Render), listalos.

- [ ] No requiere pasos especiales
- [ ] Requiere migración de DB
- [ ] Requiere variable de entorno nueva
- [ ] Requiere coordinación con otro servicio
