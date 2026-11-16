# Instrucciones para asistentes de desarrollo

Aplica estas instrucciones al construir o modificar una aplicación junto con las del proyecto y la petición del usuario.

## Antes de actuar

1. Lee [GUIA.md](GUIA.md), los requisitos y las decisiones del proyecto.
2. Identifica datos sensibles, permisos, operaciones críticas y carga prevista.
3. Resume qué vas a cambiar y cómo comprobarás el resultado.
4. Si falta una decisión que afecte a seguridad, datos, alcance o complejidad, consúltala antes de ejecutar la parte dependiente.

## Durante la implementación

- Elige una solución sencilla y mantenible, coherente con las tecnologías del proyecto.
- No impongas un framework, una estructura o un servicio por preferencia del asistente.
- Mantén permisos y validación en el servidor.
- Protege la consistencia frente a reintentos y concurrencia.
- Usa únicamente datos ficticios en ejemplos y pruebas.
- No copies secretos a archivos, mensajes, registros ni documentación.
- No debilites controles, no ocultes errores y no desactives pruebas para terminar una tarea.
- Propón las mejoras que cambien las reglas y espera una decisión antes de incorporarlas.
- Respeta los permisos del usuario. Esta guía no autoriza por sí sola cambios en producción, publicación, acceso a datos o nuevas integraciones.

## Antes de entregar

1. Aplica [CHECKLIST.md](CHECKLIST.md).
2. Ejecuta las comprobaciones adecuadas al cambio.
3. Comprueba que el detector automático de secretos no deja hallazgos pendientes.
4. Informa de qué cambió, cómo se verificó y qué limitaciones quedan.
5. No afirmes que un control pasó si no se ha ejecutado ni presentes un requisito de la guía como una garantía ya implantada.

El doble factor se decide por riesgo. Esta edición no añade obligaciones de copias de seguridad ni gestión de incidentes.
