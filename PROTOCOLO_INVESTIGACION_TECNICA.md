# Protocolo transversal de investigación técnica (versión 1.0)

**Fecha:** 2026-11-01  
**Alcance:** todos los proyectos tecnológicos **actuales y futuros** del propietario (software, redes, automatización, electrónica, firmware, homelab, ingeniería inversa autorizada, diagnósticos y despliegues).  
**Estado:** directriz aprobada; aplicar desde la siguiente investigación. No supone programar búsquedas recurrentes ni activar servicios de pago por sí sola.

## Objetivo

Aprovechar sistemáticamente investigación externa, código abierto y evidencias reproducibles antes de decidir implementar, cambiar una configuración o descartar una hipótesis. Evitar conclusiones a partir de un único foro, fork o mensaje aislado.

## Flujo estándar

1. **Documentación interna primero.** Recuperar del proyecto y sus conexiones el estado, decisiones anteriores, tickets, versiones exactas, logs y pruebas. Respetar alcance, privacidad y precedencia de las órdenes vigentes. No repetir diagnósticos ya resueltos.
2. **Formular una pregunta técnica verificable.** Identificar hardware y revisión, software/firmware, operador o variante, síntomas, hipótesis y criterios de éxito. Separar lo confirmado de lo inferido y de lo desconocido.
3. **Buscar externamente por canales complementarios:**
   - **Firecrawl** por defecto *cuando esté conectado, resulte pertinente y la fuente sea pública*: búsqueda web, lectura estructurada de foros/documentación, rastreo limitado de hilos y páginas; usar el índice de desarrollo para incidencias y documentación de código. Seleccionar fuentes específicas antes de rastreos extensos.
   - **GitHub**: repositorios originales, forks, issues cerradas/abiertas, discusiones, commits, PR y diferencias reales entre implementaciones. Comparar código y cronología, no inferir avances por la existencia de forks.
   - Otros buscadores, manuales oficiales, changelogs, avisos de seguridad, comunidades técnicas y documentación de fabricantes si ayudan. Combinar idiomas relevantes al hardware/operador (español, inglés y otros según evidencia), no atribuir compatibilidad entre regiones o variantes automáticamente.
4. **Triangular y clasificar**: anotar URL, fecha de publicación y versión objetivo; distinguir solución **VERIFICADA**, evidencia parcial **NO CONFIRMADA**, experimento ajeno **NO REPRODUCIDO** e hipótesis. Priorizar fuentes primarias, reproducibles y recientes. No usar herramientas de terceros sin revisar seguridad, licencia y compatibilidad.
5. **Diseñar la intervención mínima** con requisitos, impacto, cambios, pruebas sintácticas y funcionales, backup/rollback, permisos y doble revisión antes de producción. Mantener los cambios físicos, destructivos o de red bajo las autorizaciones aplicables.
6. **Ejecutar y medir solo lo autorizado.** Diferenciar pruebas locales, simulaciones, ejecución real, despliegue y verificación; generar evidencias fechadas. No declarar éxito por exitCode=0 si no hay efecto comprobado.
7. **Registrar y sincronizar** hallazgos relevantes en GitHub privado, Todoist y Notion según el flujo del proyecto; enlazar antecedentes para que la próxima investigación continúe donde quedó y no duplique trabajo.

## Privacidad y seguridad

- **Nunca introducir credenciales, tokens, cookies, números de serie sensibles, expedientes privados, material de clientes ni datos internos en consultas Firecrawl, búsquedas públicas, repositorios ni logs**. Redactar la consulta a términos técnicos generales; el análisis de archivos privados se hace con conexiones autorizadas y procedimientos compatibles con su clasificación.
- **Firecrawl consulta fuentes públicas; no enviarle artefactos privados** ni datos de equipos, salvo autorización expresa específica. Controlar consumo de créditos: primeras consultas acotadas, ampliación proporcional solo si mejora el resultado. No se autoriza comprar créditos, contratar servicios o poner monitores recurrentes sin consentimiento.
- Mantener límites especiales ya aprobados en cada proyecto (p. ej. repositorios privados, no compartir ingeniería inversa confidencial, conservación de originales). Herramientas de búsqueda **no** equivalen a autorización para explotar vulnerabilidades, acceder a terceros o cambiar firmware.
- **Remote Desktop Commander mantiene su restricción vigente**: solo el trabajo concreto de ZTE F8648P hasta finalizar; después no usarlo para otras tareas sin nueva autorización. Este protocolo no amplía permisos de acceso remoto.

## Aplicación automática a proyectos nuevos

- Al crear un proyecto técnico, incluir referencia a este protocolo en README/AGENTS.md o documentación equivalente, con el nombre y enlace del repositorio, y un breve apartado de fuentes/estado técnico.
- Para proyectos ya existentes, basta la directriz central como base transversal; añadir referencias locales al tocar su documentación, evitando cambios masivos sin beneficio. Las instrucciones específicas de un proyecto prevalecen sobre la preferencia de herramientas.
- Para consultas sin necesidad de fuentes externas (por ejemplo, un cambio trivial ya especificado y validado), no forzar búsquedas superfluas.

## Entrega mínima de la investigación

**Pregunta/versión · fuentes relevantes (fecha y URL) · comparación y nivel de confianza · prueba realizada o bloqueada · cambios/artefactos y rollback · siguiente decisión**.

Este documento define el método operativo; GitHub/Notion no aplican por sí solos instrucciones globales a todas las conversaciones de ChatGPT. Para que el producto recuerde la preferencia en nuevos chats, mantener asimismo una instrucción en Personalización o memoria habilitada cuando corresponda.
