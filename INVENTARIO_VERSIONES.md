# Inventario de versiones y evidencias — 2026-11-02

**Nunca equiparar versión de README, Git HEAD o CI con binario instalado.** Este registro diferencia evidencia histórica e información reciente, sin acceder a secretos.

| Host | Componente | Identificación evidenciada | Evidencia | Estado |
|---|---|---|---|---|
| T520 | NEXO Desktop | `0.4.7` declarada en fichero `nexo.pyw`, SHA-256 `FFE0DBFC64A0ED29DB11B01F4B7B2D31C08B0B3FB422DE87667F8FDD271AB38B` | [Inventario 9024, 30/10](https://github.com/aibarz/proyectos-internos/blob/main/nexo-pull/control/ssh-receipts/20261030081500000000000000009024.json) | **OBSERVADO 30/10**, no manifest de release, dirty=1; subversión/build desconocida y verificación actual pendiente |
| T520 | Pugi | `0.4.18` en `pugi.pyw`, SHA-256 `FADBAC776A1572C08CFD2CB2518596BC58D2BBF6697B1C4E009757B4BDD6B95D` | [Inventario 9021, 30/10](https://github.com/aibarz/proyectos-internos/blob/main/nexo-pull/control/ssh-receipts/20261030085500000000000000009021.json) | **OBSERVADO 30/10**, build exacta sin manifiesto |
| T520 | GNP | `0.9.5` agente, SHA-256 `291297203EA77373B73EF8714CC34B9D5B37C4E497C048759DE51715D52A13F4` documentado 27/10 | [Entrega y hash](https://github.com/aibarz/proyectos-internos/blob/main/nexo-pull/deploy/gnp095/README.md) y [latido 02/11](https://github.com/aibarz/proyectos-internos/blob/main/nexo-pull/control/STATUS.md) | **LATIDO 02/11** dice 0.9.5, SHA actual no recalculado |
| ASUS | Cualquier componente | NA | No recibo accesible en esta auditoría | **UNKNOWN** |
| HP6200 | Cualquier componente | NA | Equipo sin despliegue auditado | **UNKNOWN** |

**Discrepancia activa:** `aibarz/nexo-desktop/main/README.md` declara 0.4.6 y su PR #4 para 0.4.7 está en borrador, mientras el T520 ya ejecutaba un fichero con etiqueta 0.4.7 el 30/10. Además, `trackedChanges:true` impide considerar que el árbol local coincide con el commit Git. **No suponer cuál de las diferencias es la buena ni sobrescribir.** El objetivo próximo indicado por el propietario es 0.4.8, todavía no desplegado/verificado.

**Estado de implantación de la norma:** Documentada para los repositorios; la implantación automática en todos los instaladores está PENDIENTE. La existencia de un nuevo README no equivale a corregir binarios ni completar inventarios remotos.
