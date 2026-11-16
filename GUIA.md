# Construir una aplicación segura y escalable

Versión 1.0.0 · 16 de noviembre de 2026

## 1. Definir antes de construir

Antes de implementar, deja por escrito:

- Qué problema resuelve la aplicación y qué queda fuera.
- Qué usuarios existen, qué pueden hacer y a qué datos pueden acceder.
- Qué información es sensible y dónde se guarda o transmite.
- Qué operaciones no pueden duplicarse, perderse o quedar a medias.
- Qué volumen inicial y crecimiento se esperan, y qué tiempos de respuesta resultan aceptables.
- Cómo se comprobará que cada requisito funciona.

Elige la solución más sencilla que cumpla esos requisitos. No añadas infraestructura, dependencias ni abstracciones por una necesidad futura sin justificar. Las decisiones relevantes deben quedar documentadas y aprobadas por el responsable del proyecto.

## 2. Escribir código que se pueda mantener

- Usa nombres claros y responsabilidades pequeñas y coherentes.
- Separa las reglas de negocio de la presentación, la persistencia y los servicios externos.
- Mantén los controladores y pantallas ligeros; las reglas importantes deben poder probarse sin abrir la interfaz.
- Aplica SOLID, DRY y Clean Code con criterio. Reutiliza reglas compartidas y evita generalizaciones que compliquen una necesidad sencilla.
- Usa los mecanismos de tipos y validación disponibles en el lenguaje. No desactives comprobaciones para ocultar problemas.
- Trata los errores de forma explícita. El usuario recibe un mensaje útil; el equipo dispone del contexto necesario para diagnosticarlo.
- Al sustituir una implementación, retira el código y esquema obsoletos en el mismo cambio, con una migración segura cuando corresponda.
- Actualiza la documentación afectada junto con el código.

## 3. Identidad, sesiones y permisos

### Autenticación

Utiliza bibliotecas y mecanismos mantenidos. No construyas un sistema criptográfico propio.

- Guarda contraseñas mediante un algoritmo de hash específico para contraseñas y una biblioteca mantenida; nunca en texto plano.
- Limita los intentos de entrada y protege también la recuperación de contraseña y la renovación de sesiones.
- Evita mensajes que permitan averiguar si una cuenta existe.
- Las sesiones deben caducar y poder revocarse. Cerrar sesión debe invalidar la credencial correspondiente en el servidor.
- No guardes tokens sensibles en `localStorage`. Para el navegador, usa el mecanismo seguro previsto por el framework; las cookies de autenticación deben tener las protecciones adecuadas, incluyendo `HttpOnly`, `Secure` en producción y `SameSite` según el flujo.
- Si se usan cookies para autenticar operaciones, aplica defensa contra peticiones falsificadas (CSRF).
- Si el diseño usa access tokens y refresh tokens, los primeros deben durar poco y los segundos rotarse, guardarse como hash y permitir detectar su reutilización.
- Decide y documenta el uso de doble factor según el riesgo de la aplicación y los privilegios de sus usuarios. Esta guía no impone su obligatoriedad universal.

### Autorización

La comprobación real se hace en el servidor para cada operación sensible.

- Autenticarse no equivale a tener permiso para modificar datos.
- Concede solo los permisos necesarios. Un rol desconocido o no configurado debe quedar sin acceso.
- Comprueba tanto la acción permitida como la pertenencia del recurso.
- Si existen varios clientes, empresas o centros, todas las lecturas, escrituras, búsquedas, exportaciones y tareas en segundo plano deben respetar ese alcance.
- El servidor resuelve el contexto autorizado; un identificador enviado desde la pantalla no concede acceso.
- Un administrador solo puede operar dentro de los permisos concedidos. Los accesos globales excepcionales deben ser explícitos y auditados.
- Ocultar botones mejora la experiencia, pero no sustituye ninguna comprobación de permisos.
- Define el flujo de alta según el producto. Cuando se utilicen invitaciones, deben caducar, poder revocarse y respetar los privilegios del actor.

## 4. Tratar toda entrada como no fiable

Valida en el servidor antes de procesar o guardar información, aunque la pantalla ya la haya comprobado.

- Define esquemas estrictos: tipos, formatos, rangos, longitudes y valores permitidos. Rechaza campos desconocidos cuando el esquema no los admita.
- Valida los identificadores y comprueba los permisos antes de operar con el recurso.
- Usa consultas parametrizadas o mecanismos seguros de persistencia; no construyas consultas concatenando entradas.
- Escapa o sanitiza el contenido al mostrarlo según su contexto para evitar que se ejecute como código.
- Aplica límites de tamaño y consumo a entradas y operaciones costosas.
- Para archivos, comprueba extensión, tipo real y firma cuando corresponda, además de límites de bytes, hojas, filas y columnas.
- Una importación debe validarse antes de confirmar sus cambios. Usa preparación previa y confirmación transaccional para evitar estados parciales.

La aplicación debe contemplar fallos de control de acceso, inyección, contenido malicioso, configuración insegura, dependencias vulnerables y peticiones del servidor hacia destinos no autorizados.

## 5. Proteger secretos y datos sensibles

- Contraseñas, claves privadas y tokens se obtienen del entorno o de un sistema de gestión de secretos. Nunca se incluyen en código, documentación, archivos de ejemplo ni historial del repositorio.
- Los ejemplos usan marcadores inequívocos y datos ficticios.
- La aplicación debe rechazar el arranque en producción si faltan secretos obligatorios o contienen valores inseguros de ejemplo.
- Los secretos no deben llegar a la pantalla, al código distribuido al navegador, a errores ni a registros.
- Protege el transporte en producción, restringe los orígenes permitidos y configura las cabeceras de seguridad correspondientes.
- Evita exponer detalles internos y herramientas de desarrollo fuera de los entornos autorizados.

### Comprobación automática obligatoria de secretos

Antes de aceptar cambios, una herramienta de detección de secretos debe revisar los archivos y los nuevos commits incluidos en la entrega, también configuración, documentación y datos de prueba.

- El resultado debe ser bloqueante: una detección pendiente de resolver impide integrar o publicar.
- La revisión manual complementa la herramienta; no la sustituye.
- Un falso positivo requiere una exclusión concreta, justificada y revisada. No se desactiva el control global para superar el bloqueo.
- Los informes no deben imprimir el valor completo del secreto.
- El proyecto documenta la herramienta y el punto del flujo donde aplica el bloqueo.

Este control se comprueba como parte de la entrega; no basta con declararlo en la documentación. Es la ampliación aprobada para esta edición. Véase la [referencia de OWASP sobre seguridad del desarrollo y secretos](https://cheatsheetseries.owasp.org/cheatsheets/CI_CD_Security_Cheat_Sheet.html).

## 6. Mantener datos correctos con reintentos y concurrencia

Los fallos de red, dobles pulsaciones y procesos simultáneos no deben producir duplicados ni estados inconsistentes.

- Usa persistencia transaccional adecuada para los datos operativos. Los archivos temporales y las cachés reconstruibles no sustituyen a la base de datos.
- Refuerza las invariantes críticas con restricciones de integridad y unicidad en la base de datos.
- Agrupa en una transacción los cambios que deben completarse juntos.
- Evita comprobar si algo existe y crearlo después como dos pasos desprotegidos. Usa inserciones o actualizaciones atómicas y controla los conflictos.
- Las operaciones críticas reintentables deben ser idempotentes: repetir la misma solicitud produce el mismo efecto, sin duplicarlo.
- Cuando se use una clave de idempotencia, guarda la identidad de la operación y su resultado; la misma clave con datos distintos debe rechazarse. Define su plazo de conservación.
- Prefiere establecer un estado explícito a alternarlo. Por ejemplo, «marcar como completado» se puede repetir con seguridad; «invertir el estado» puede deshacer la primera operación.
- Usa bloqueos cuando exista una carrera que las restricciones y transacciones no resuelvan por sí solas.
- Las migraciones deben ser pequeñas, revisables y compatibles con una transición segura. No retires datos o columnas críticas sin un plan de cambio.

## 7. Preparar el crecimiento con medidas concretas

Escalar empieza por evitar trabajo innecesario y conocer los límites reales.

- Define objetivos de carga y respuesta para las operaciones importantes.
- Mide latencia, errores, consultas lentas y trabajos pendientes antes de introducir complejidad.
- Añade índices a búsquedas y relaciones frecuentes. Revisa las consultas que se repiten por cada elemento de un listado.
- Pagina los listados y limita las búsquedas, exportaciones e importaciones costosas.
- Usa una estrategia coherente para obtener y almacenar temporalmente los datos. No conviertas la caché en la única copia de información operativa.
- Lleva a segundo plano los trabajos lentos cuando lo necesite la experiencia de usuario. Define reintentos seguros y estado visible de los trabajos.
- Los trabajos y eventos también deben ser idempotentes y conservar el contexto del usuario o cliente que corresponda.
- Si un cambio de datos debe producir un evento fiable, guarda ambos de forma coordinada antes de entregar el evento.
- Comprueba con pruebas de carga o rendimiento los recorridos donde el volumen pueda afectar a la corrección o al servicio.
- Añade colas, servicios o infraestructura distribuida cuando una necesidad medida lo justifique.

## 8. Poder entender lo que ocurre

Cada operación crítica debe dejar información suficiente para seguir su ejecución.

- Usa registros estructurados con fecha, nivel, operación, resultado e identificador de seguimiento.
- Conserva ese identificador al pasar por trabajos en segundo plano y eventos.
- Audita acceso, cambios de credenciales y permisos, operaciones administrativas y modificaciones de datos críticos.
- Identifica al actor y el contexto cuando sea necesario, evitando datos sensibles innecesarios.
- Mide errores, latencia, accesos fallidos, consultas lentas y trabajos atascados.
- Define alertas para fallos relevantes y comportamientos anómalos.

## 9. Probar lo que puede romperse

Las pruebas deben demostrar comportamiento, límites y permisos.

- Pruebas unitarias para reglas de negocio, cálculos, validaciones y decisiones de acceso.
- Pruebas de integración para persistencia, sesiones, permisos, transacciones y procesos en segundo plano.
- Pruebas de extremo a extremo para los recorridos esenciales del usuario.
- Casos negativos: usuario sin sesión, permiso insuficiente, datos de otro cliente, entradas inválidas y archivos malformados.
- Reintentos y operaciones simultáneas: mismo resultado sin duplicados y restricciones respetadas.
- Expiración y revocación de sesiones; rotación y reutilización de tokens cuando ese mecanismo exista.
- Rendimiento de los recorridos críticos con el volumen previsto.

Si cambias una regla y no añades o ajustas pruebas, explica por qué la cobertura existente es suficiente.

## 10. Integrar y entregar con evidencia

- Trabaja en cambios pequeños, vinculados a requisitos verificables y revisados antes de integrarse.
- Protege las ramas compartidas y define cómo se aprueban y publican las entregas.
- Ejecuta formato, análisis de código, comprobación de tipos cuando exista, pruebas y revisión de dependencias.
- Mantén versiones reproducibles de dependencias y revisa las vulnerabilidades antes de publicar.
- Una dependencia nueva debe estar mantenida y justificar su necesidad. No se entrega con vulnerabilidades críticas o altas conocidas pendientes.
- Ejecuta la detección automática de secretos del apartado 5.
- Prueba las migraciones sobre una base de datos temporal y documenta cómo volver a una versión compatible cuando corresponda.
- No ignores controles fallidos, no desactives verificaciones ni cambies pruebas solo para ocultar un fallo.
- La revisión incluye comportamiento, seguridad, impacto en datos y rendimiento, riesgos y evidencias de las comprobaciones.
- Usa la [checklist de entrega](CHECKLIST.md) antes de considerar terminado el cambio.

## Regla de aplicación

Las tecnologías y los parámetros concretos se documentan por proyecto. «No aplica» debe tener una explicación verificable; no debe usarse para omitir un control necesario.

Si una mejora cambia el alcance, las reglas de seguridad o la complejidad acordada, propón el cambio y solicita una decisión antes de incorporarlo.
