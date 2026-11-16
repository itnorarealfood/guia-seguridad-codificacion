# Fuentes, versión y decisiones

## Edición de esta guía

- Versión: **1.0.0**.
- Fecha: **16 de noviembre de 2026**.
- Alcance: construcción de aplicaciones seguras y escalables.
- Naturaleza: adaptación editorial y generalización de documentación existente. No es una copia literal ni una certificación de seguridad.

## Fuente principal indicada por el usuario

[Documentación de norahub, rama dev](https://github.com/itnorarealfood/norahub/tree/dev/docs).

Instantánea consultada: [commit 26af7d31c6d3547aa141265db0e0047ababf066e](https://github.com/itnorarealfood/norahub/commit/26af7d31c6d3547aa141265db0e0047ababf066e), del 16 de julio de 2026. El último cambio que afecta a `docs/` en esa rama es [4306f359d559c26a8c489f44fb1f81f981e9d52c](https://github.com/itnorarealfood/norahub/commit/4306f359d559c26a8c489f44fb1f81f981e9d52c), también del 16 de julio de 2026. Verificación realizada el 16 de noviembre de 2026.

Se revisaron los 18 documentos de esa carpeta y las instrucciones y criterios de calidad relacionados. Las fuentes que aportan los criterios principales son:

| Fuente original | Uso en esta edición |
| --- | --- |
| [AGENTS.md](https://github.com/itnorarealfood/norahub/blob/26af7d31c6d3547aa141265db0e0047ababf066e/AGENTS.md) | Reglas de trabajo, criterios de terminado y documentación |
| [Base de calidad](https://github.com/itnorarealfood/norahub/blob/26af7d31c6d3547aa141265db0e0047ababf066e/openspec/standards/coding-baseline.md) | Prioridades de seguridad, consistencia y mantenibilidad |
| [Base de seguridad](https://github.com/itnorarealfood/norahub/blob/26af7d31c6d3547aa141265db0e0047ababf066e/docs/security/security-baseline.md) | Permisos, validación, aislamiento y dependencias |
| [Autenticación y sesiones](https://github.com/itnorarealfood/norahub/blob/26af7d31c6d3547aa141265db0e0047ababf066e/docs/security/auth-token-management.md) | Sesiones, invitaciones, revocación y doble factor según riesgo |
| [Arquitectura](https://github.com/itnorarealfood/norahub/blob/26af7d31c6d3547aa141265db0e0047ababf066e/docs/architecture/architecture.md) | Separación de responsabilidades, transacciones, rendimiento y reintentos |
| [Aislamiento entre clientes](https://github.com/itnorarealfood/norahub/blob/26af7d31c6d3547aa141265db0e0047ababf066e/docs/architecture/tenancy.md) | Alcance y pruebas de aislamiento cuando aplique |
| [Pruebas](https://github.com/itnorarealfood/norahub/blob/26af7d31c6d3547aa141265db0e0047ababf066e/docs/process/testing-strategy.md) | Pruebas unitarias, integración, recorridos críticos y casos negativos |
| [Observabilidad](https://github.com/itnorarealfood/norahub/blob/26af7d31c6d3547aa141265db0e0047ababf066e/docs/process/observability.md) | Seguimiento, auditoría, métricas y alertas |
| [Integración y entrega](https://github.com/itnorarealfood/norahub/blob/26af7d31c6d3547aa141265db0e0047ababf066e/docs/process/cicd.md) | Comprobaciones bloqueantes y migraciones |
| [Flujo de trabajo](https://github.com/itnorarealfood/norahub/blob/26af7d31c6d3547aa141265db0e0047ababf066e/docs/process/workflow.md) | Requisitos, revisión y evidencias |

## Adaptación solicitada

- Se eliminan marcas, rutas, dominios, credenciales de ejemplo y decisiones exclusivas del producto original.
- No se impone Laravel, Next.js, PostgreSQL, un modelo de repositorio ni una herramienta concreta.
- Se mantienen los criterios de seguridad y consistencia, expresados como resultados y comprobaciones aplicables a diferentes tecnologías.
- Se omiten los capítulos especializados de API, contratos, plugins, modularidad específica y configuración local.
- Los controles de aislamiento y tokens se expresan de forma condicional al diseño real de la aplicación.
- No se ha modificado ningún repositorio fuente.

## Mejoras consultadas individualmente

Decisiones expresas del usuario del 16 de noviembre de 2026:

| Propuesta | Decisión | Aplicación |
| --- | --- | --- |
| Doble factor obligatorio para administradores desde el primer despliegue | Mantenerlo según el riesgo de cada aplicación | No se introduce obligatoriedad universal |
| Detector automático de secretos que bloquee cambios | Aprobado | Requisito obligatorio en la guía y checklist |
| Copias, restauración y procedimiento de incidentes | Dejarlo fuera de esta guía de desarrollo | No se añade ese apartado |

## Referencias de apoyo

La detección automática de secretos y su integración en las verificaciones se apoya en la [guía de seguridad de CI/CD de OWASP](https://cheatsheetseries.owasp.org/cheatsheets/CI_CD_Security_Cheat_Sheet.html) y la [guía de gestión de secretos de OWASP](https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html).

El tratamiento del doble factor según el riesgo se contrastó con la [guía de MFA de OWASP](https://cheatsheetseries.owasp.org/cheatsheets/Multifactor_Authentication_Cheat_Sheet.html). Esta referencia no sustituye la decisión de alcance aprobada para esta edición.

## Conservación y cambios

La versión se conserva en un repositorio privado y archivado. Mientras permanezca archivado, el contenido es de solo lectura. Los administradores que puedan desarchivarlo conservan la capacidad de habilitar cambios.

Las futuras mejoras requieren una decisión explícita y una versión nueva. La referencia al origen permite comparar posteriores ediciones sin sincronizaciones automáticas.
