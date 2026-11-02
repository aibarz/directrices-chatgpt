# Protocolo global obligatorio: versionado y trazabilidad de despliegues

Vigencia: 2026-11-02. Aplicable a todos los repositorios de `aibarz`, máquinas T520, ASUS y futuro HP 6200; también a nuevas máquinas, servicios, firmware y módulos. Este documento es la fuente normativa, no una certificación de que ya esté instalado su ejecutor.

## Principio de identidad

**Una versión instalada no es el texto del README ni únicamente el número que muestra una ventana.** La identidad verificable de una instalación es la tupla:

`(project, semver, build_id, source_commit, release_manifest_sha256, host, installed_file_sha256, verified_utc)`.

- `semver` cambia cuando cambia el comportamiento/contrato distribuido; utilizar versión MAJOR.MINOR.PATCH. Un hotfix se identifica con nuevo PATCH o prerelease explícita.
- `build_id` es único por empaquetado (por ejemplo `0.4.8+gabcdef1.run1234`); **nunca** reutilizar el mismo identificador si cambia un solo byte.
- Un commit Git identifica fuentes y es distinto de un SHA-256 binario. No comparar Git blob SHA-1 con SHA-256; calcular hashes de artefactos en la compilación y de ficheros realmente instalados.
- README documenta la rama por defecto, no demuestra producción. Ramas de prueba y PR draft jamás se reportan como instaladas por sí solas.
- Incluir `--version` / diálogo Acerca de / endpoint de inventario mostrando versión + build + commit + digest, sin mostrar secretos. Cambiar tanto los valores mostrados como metadatos y manifiesto en el mismo paquete.
- Reemplazar automáticamente etiquetas visibles solo **después de verificar** que el binario instalado coincide con el manifiesto aprobado. Si no hay firma/manifest válido: `VERSION_NO_VERIFICADA`, no inventar subversión.

## Contrato de manifiesto (ejemplo sin datos reales)

```json
{
  "schema": "internos/release-manifest-v1",
  "project": "nexo",
  "version": "0.4.8",
  "build_id": "0.4.8+gabcdef0.ci123",
  "source_repo": "aibarz/nexo-desktop",
  "source_commit": "abcdef0123456789abcdef0123456789abcdef01",
  "built_utc": "2026-11-02T22:00:00Z",
  "artifacts": [
    {"path": "nexo.pyw", "sha256": "0000000000000000000000000000000000000000000000000000000000000000", "bytes": 0}
  ]
}
```

**Los datos son FICTICIOS**. Manifiesto siempre fuera del código que se esté validando, y no puede autorreferenciar su propio SHA. Producir `SHA256(manifest.json)` a partir del JSON final de bytes exactos; opcionalmente firmar los bytes con clave custodiada fuera de Git.

## Ciclo obligatorio

1. **DOCUMENTAR**: inspeccionar repositorios, versión realmente instalada, inventario y hashes anteriores; registrar timestamp y host.
2. **VALIDAR**: comparar archivos de fuente y catálogo de artefactos; generar número de versión y build ID nuevos si cambia el contenido ejecutable.
3. **PREPARAR**: compilar/empacar una vez; generar manifiesto de hashes; publicar artefactos inmutables de la release y un changelog; preservar backup y rollback de la versión anterior.
4. **PROBAR**: tests sintácticos, contractuales, seguridad y CI; primera y segunda revisión; no reutilizar tests de otra build.
5. **APLICAR**: instalador controlado en host elegido, sin comandos arbitrarios, sólo artefactos aprobados; archivo de versión y manifiesto se instalan en una única operación transaccional junto a la build.
6. **VERIFICAR**: desde el host calcular SHA-256 de cada artefacto y del manifiesto; comparar con la release; probar función real, procesos/sesión y rollback. El recibo incluye `runId`, host, ruta, UTC, commit, versión, digest, hashes observados, backup y estado.
7. **REGISTRAR**: actualizar registro central de versiones y el propio repositorio/README/Todoist/Notion/NEXO con el nuevo estado **sólo tras recibo válido**. Nunca modificar histórico para aparentar éxito.
8. **ACEPTAR**: `DEPLOYED_VERIFIED` si hashes coinciden y pruebas funcionales pasan. `DEPLOYED_DRIFT` si el host presenta modificaciones locales. `UNKNOWN` si no hay recibo reciente. `PLANNED` o `STAGED` no son despliegues.
9. **RECUPERAR**: rollback atómico, volver a medir hashes y actualizar registro con versión restaurada; una restauración también genera evento verificable.

## Reglas de coherencia

- Si el README dice 0.4.6, un recibo del host dice 0.4.7 y la PR 0.4.7 está abierta: **el host es la evidencia de instalación**, el README y la PR son fuente de inconsistencia documental. No reescribir la historia: corregir README y crear incidencia de reconciliación.
- Si `git status` indica modificaciones locales, calcular hashes y registrarlas; no ejecutar `git reset --hard`, actualizar ni sobrescribir hasta preservar originals.
- Una versión se asigna **a los bytes desplegados**. Dos ejecutables diferentes con el mismo número deben tener builds diferentes; no afirmar "mismo 0.4.7" sin el build ID.
- Escanear automáticamente SOLO archivos allowlisted, sin valores de credenciales, ficheros de configuración reales, claves, rutas sensibles ni historiales privados.
- NEXO debe mostrar versión de cada agente y último checkUTC, con indicador `DRIFT`/ `NO_VERIFICADO`; no usar la barra de progreso como sustituto de la verificación.
- Despliegues en T520, ASUS y HP6200 deben registrar host independiente: que T520 use 0.4.7 no implica que ASUS lo use.
- No utilizar Remote Desktop Commander hasta nueva autorización. Usar SSH/NEXO-Pull funciones fijas y allowlisted; nunca ampliar permisos por conveniencia.

## Estado inicial

El registro `INVENTARIO_VERSIONES.md` conserva evidencias previas, pero no es inventario remoto de hoy. La generación del manifiesto + verificador y su integración en pipelines/deployments son trabajo técnico separado con pruebas. Mientras tanto, un recibo histórico sigue siendo evidencia de su fecha, no de un estado presente no consultado.
