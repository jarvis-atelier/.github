# Política de Seguridad

En Jarvis Atelier nos tomamos la seguridad en serio. Si encontraste una vulnerabilidad en cualquiera de nuestros repos, leé esta política antes de actuar.

## Reporte de vulnerabilidades

**No abras un issue público ni un PR para reportar vulnerabilidades.** Hacerlo expone el problema antes de que podamos arreglarlo.

### Cómo reportar

Mandá un correo a **security@jarvis-atelier.dev** con la siguiente información:

- **Descripción** clara del problema.
- **Tipo de vulnerabilidad** (XSS, SQLi, IDOR, RCE, exposición de credenciales, etc.).
- **Impacto potencial** (qué se podría hacer si se explota).
- **Pasos para reproducir** detallados, idealmente con un PoC mínimo.
- **Versión / commit afectado.**
- **Tu nombre o handle** para acreditarte (opcional — podemos tratar el reporte de forma anónima si preferís).

Si el reporte involucra datos sensibles, podés cifrarlo con nuestra clave PGP pública (disponible bajo pedido al mismo correo).

### Alternativa: GitHub Security Advisories

Si preferís el canal de GitHub, usá la pestaña **Security → Report a vulnerability** del repo afectado. Eso abre un advisory privado donde podemos coordinar la solución sin exposición pública.

## Qué esperar de nosotros

| Etapa | Tiempo objetivo |
|---|---|
| Acuse de recibo | **48 horas hábiles** |
| Triage inicial y validación | **5 días hábiles** |
| Plan de remediación comunicado | **10 días hábiles** |
| Parche disponible (según severidad) | **30-90 días** |

Si la vulnerabilidad es crítica y está siendo explotada activamente, aceleramos todos los plazos.

Te vamos a mantener al tanto durante todo el proceso. Si en algún momento dejamos de comunicar, recordánoslo — no es desinterés, es que algo se nos pasó.

## Severidad

Usamos una clasificación adaptada de CVSS:

- **Crítica** — RCE, escalación de privilegios completa, exposición masiva de datos sensibles. Parche en horas/días.
- **Alta** — IDOR con acceso a datos de otros tenants, bypass de autenticación, SQLi explotable. Parche en días/semanas.
- **Media** — XSS reflejado, CSRF en endpoints sensibles, leaks parciales. Parche en el siguiente release planificado.
- **Baja** — config subóptima, headers faltantes, hardening recomendado. Se incorpora a backlog.

## Disclosure responsable

Pedimos que:

- Nos des **tiempo razonable** para parchear antes de hacer público el hallazgo (mínimo 90 días, o lo que acordemos).
- **No accedas a datos** de otros usuarios más allá de lo necesario para demostrar el problema.
- **No alteres ni borres datos** durante la prueba.
- **No hagas DoS** intencional ni pruebas de carga sin coordinarlas previamente.
- **No uses la vulnerabilidad** para nada que no sea reportarla.

A cambio:

- No vamos a tomar acciones legales contra reportes hechos de buena fe siguiendo esta política.
- Te vamos a acreditar públicamente (si querés) en el changelog, advisory o sección de agradecimientos.
- Cuando tengamos un programa formal de bug bounty, los reportes previos se considerarán para reconocimiento.

## Alcance

Esta política cubre todos los repos públicos de la organización **jarvis-atelier** en GitHub y los servicios desplegados que sean propiedad de Jarvis Atelier (dominios `*.jarvis-atelier.dev` y los que se publiquen oficialmente).

**Fuera de alcance:**

- Ataques de ingeniería social a empleados o usuarios.
- Vulnerabilidades en dependencias de terceros que ya tengan un CVE público sin impacto demostrable en nuestros sistemas (reportalas upstream).
- Reportes generados automáticamente por scanners sin validación manual ni PoC.
- Clickjacking en páginas sin acciones sensibles.
- Falta de headers de seguridad en endpoints estáticos sin riesgo concreto.
- Prácticas recomendadas sin impacto explotable demostrable.

## Versiones soportadas

Por defecto solo damos soporte de seguridad a la **última versión mayor publicada** de cada producto. Si tu reporte aplica a versiones más viejas, lo evaluamos pero la prioridad va a la rama activa.

## Contacto

- **Email:** security@jarvis-atelier.dev
- **PGP:** disponible bajo pedido
- **GitHub Security Advisories:** habilitado en todos nuestros repos

Gracias por ayudarnos a mantener seguros nuestros productos y a nuestros usuarios.
