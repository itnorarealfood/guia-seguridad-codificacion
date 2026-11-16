# Procedencia y decisiones

Versión **1.0.2** · 16 de noviembre de 2026

Este repositorio es la **fuente de verdad** de la guía. Las normas vigentes son las redactadas y versionadas aquí; la guía y la checklist están completas en archivos locales.

La referencia de origen registra la procedencia histórica de la adaptación. Su contenido no se sincroniza automáticamente ni determina las futuras ediciones de esta guía.

## Procedencia

La base indicada por el usuario fue la [documentación de desarrollo, rama dev](https://github.com/itnorarealfood/norahub/tree/26af7d31c6d3547aa141265db0e0047ababf066e/docs), consultada el 16 de noviembre de 2026.

- Revisión del repositorio de origen: `26af7d31c6d3547aa141265db0e0047ababf066e`, del 16 de julio de 2026.
- Último cambio de la carpeta de documentación en esa rama: `4306f359d559c26a8c489f44fb1f81f981e9d52c`, del 16 de julio de 2026.
- Se revisaron 18 documentos, las instrucciones para asistentes y la base de calidad.
- Se generalizaron sus criterios de seguridad, consistencia, rendimiento, pruebas y entrega. Se retiraron marcas, entornos, tecnologías obligatorias y capítulos específicos de API y plugins.
- Los repositorios de origen permanecen sin cambios.

## Decisiones aprobadas por el usuario

- Doble factor según el riesgo de cada aplicación.
- Detección automática de secretos obligatoria y bloqueante antes de aceptar cambios.
- Copias de seguridad, restauración y gestión de incidentes fuera del alcance de esta guía de desarrollo.

La detección automática se contrastó con las guías públicas de OWASP sobre [seguridad de CI/CD](https://cheatsheetseries.owasp.org/cheatsheets/CI_CD_Security_Cheat_Sheet.html) y [gestión de secretos](https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html).

## Revisión 1.0.2

La guía pasa a lectura pública y la escritura queda reservada al propietario mediante reglas de protección para todas las ramas y etiquetas. Se mantiene el contenido de las decisiones de seguridad aprobadas.
