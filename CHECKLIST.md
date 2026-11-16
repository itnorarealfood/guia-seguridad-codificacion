# Checklist de entrega

Versión 1.0.2 · 16 de noviembre de 2026

Aplicar a la entrega y al comportamiento que modifica. Marcar «no aplica» con una justificación cuando corresponda.

## Requisitos y código

- [ ] El problema, los límites y los criterios de aceptación están claros.
- [ ] Las decisiones relevantes y el cambio de alcance están aprobados.
- [ ] Las reglas de negocio se pueden probar sin depender de la interfaz.
- [ ] Los errores tienen tratamiento explícito.
- [ ] No queda código o esquema obsoleto por el cambio.
- [ ] La documentación afectada está actualizada.

## Seguridad

- [ ] Las sesiones caducan, se pueden revocar y no exponen credenciales.
- [ ] El uso de doble factor está decidido según el riesgo.
- [ ] Cada operación sensible comprueba permisos y pertenencia en el servidor.
- [ ] El acceso entre clientes, empresas o centros queda aislado cuando aplica.
- [ ] Las entradas se validan y los archivos tienen límites y comprobaciones de tipo.
- [ ] Las consultas y la presentación de contenido no ejecutan entradas del usuario.
- [ ] No hay secretos ni datos sensibles en código, ejemplos, errores o registros.
- [ ] La configuración de producción rechaza secretos ausentes o inseguros.
- [ ] **El análisis automático de secretos ha pasado para los archivos y commits de la entrega.**
- [ ] Las exclusiones del detector son concretas, justificadas y revisadas.
- [ ] Las dependencias están fijadas y no tienen vulnerabilidades críticas o altas conocidas pendientes.

## Datos y crecimiento

- [ ] Transacciones y restricciones protegen las invariantes importantes.
- [ ] Reintentos y ejecuciones simultáneas no duplican operaciones.
- [ ] Las operaciones costosas tienen límites; los listados tienen paginación.
- [ ] Las consultas, índices y trabajos en segundo plano soportan el volumen previsto.
- [ ] Los trabajos y eventos conservan contexto y permiten reintentos seguros.
- [ ] Hay registros de seguimiento, auditoría y métricas de las operaciones críticas.

## Pruebas e integración

- [ ] Hay pruebas de reglas, permisos y aislamiento, incluidos los casos negativos.
- [ ] Hay pruebas de validación, consistencia, concurrencia e idempotencia cuando aplica.
- [ ] Se ha comprobado el rendimiento de los recorridos afectados cuando el riesgo lo requiere.
- [ ] Las migraciones se han probado y la transición está documentada.
- [ ] Las comprobaciones automáticas han pasado sin ocultar fallos.
- [ ] La revisión contiene riesgos, evidencias y aprobación de la entrega.
