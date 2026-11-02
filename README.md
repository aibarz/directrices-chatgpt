# directrices-chatgpt

## Investigación técnica transversal

Para todos los proyectos tecnológicos presentes y futuros, aplicar [Protocolo de investigación técnica](PROTOCOLO_INVESTIGACION_TECNICA.md): documentación interna → Firecrawl y búsqueda multilingüe de fuentes públicas → GitHub (código, forks, issues, PR) → contraste por versión → pruebas, registro y verificación. Sin publicar secretos, datos privados ni exceder permisos; consultas externas acotadas y sin seguimiento automático no autorizado.


## Control de versiones y despliegues

**Norma transversal:** [Protocolo de versionado por commit, build ID, manifiesto SHA-256 y recibo de verificación](https://github.com/aibarz/directrices-chatgpt/blob/main/PROTOCOLO_VERSIONADO_DESPLIEGUES.md). Una versión mencionada en el README o una PR no prueba la versión instalada en T520/ASUS/HP6200. Consultar [inventario histórico verificable](https://github.com/aibarz/directrices-chatgpt/blob/main/INVENTARIO_VERSIONES.md). Despliegues futuros deben asignar nueva identidad de build si cambia cualquier artefacto y verificar hashes en destino. **Aplicación automática pendiente**: este enlace no certifica instalaciones ni modifica ejecutables.
