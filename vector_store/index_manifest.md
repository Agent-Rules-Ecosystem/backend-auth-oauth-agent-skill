# MANIFIESTO Y REGLAS DE INDEXACIÓN VECTORIAL

## 1. Concepto y Objetivo
El directorio `vector_store/` registra los fragmentos (chunks) indexados del proyecto para permitir búsquedas semánticas profundas sin necesidad de leer archivos completos en cada interacción.

## 2. Registro de Documentos Indexados

| ID Fragmento | Documento Origen | Módulo / Sección | Última Sincronización |
|---|---|---|---|
| `chunk_001` | `.agents/core/brain.md` | Core Protocol | 2026-08-03 |
| `chunk_002` | `.agents/knowledge/code_style.md` | Rules & Style | 2026-08-03 |
| `chunk_003` | `overview/tracker.md` | Route Tracker | Dynamic |

## 3. Regla de Sincronización
- Al agregar una nueva regla global en `.agents/knowledge/` o un cambio significativo de arquitectura, registrar el fragmento en este manifiesto.
- El motor del agente usará `vector_store/config.json` para definir tamaño de ventana de fragmentos (512 tokens) y traslape (50 tokens).
