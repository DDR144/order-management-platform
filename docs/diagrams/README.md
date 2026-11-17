# Diagramas del sistema (Archify)

Este directorio contiene el conjunto de diagramas interactivos de la **Order Management Platform (OMP)**. Cada diagrama documenta una vista distinta del sistema congelado en la revisión `c8e3215facdd0e4f0c3ac69919988d5ba83b301a` de `master`.

| Tipo | Qué responde | HTML interactivo | Fuente `.json` |
|---|---|---|---|
| Arquitectura | Vista de runtime: cliente, gateway, microservicios, Keycloak y bases de datos PostgreSQL. | [architecture.html](./architecture.html) | [src/architecture.json](./src/architecture.json) |
| Secuencia | Flujo de creación de un pedido con `POST /api/v1/orders`, validación de stock y posible error `STOCK_INSUFFICIENT`. | [create-order.sequence.html](./create-order.sequence.html) | [src/create-order.sequence.json](./src/create-order.sequence.json) |
| ERD | Modelo de datos de `order_db` (pedidos e historial) e `inventory_db` (productos). | [data-model.erd.html](./data-model.erd.html) | [src/data-model.erd.json](./src/data-model.erd.json) |
| Ciclo de vida | Máquina de estados del pedido: `PENDING`, `CONFIRMED` y `CANCELLED`, más la salida de error por stock insuficiente y las transiciones inválidas. | [order-lifecycle.lifecycle.html](./order-lifecycle.lifecycle.html) | [src/order-lifecycle.lifecycle.json](./src/order-lifecycle.lifecycle.json) |

## Revisión documentada

`c8e3215facdd0e4f0c3ac69919988d5ba83b301a` (rama `master`, origen `https://github.com/DDR144/order-management-platform.git`).

## Cómo regenerar

Para regenerar un diagrama con Archify, usando el perfil `showcase` y la raíz del repositorio actual:

```bash
node .agents/skills/archify/bin/archify.mjs finalize architecture docs/diagrams/src/architecture.json docs/diagrams/architecture.html --repo-root . --quality showcase
```

Sustituye `architecture` y `architecture.json` por el tipo y nombre del diagrama que quieras regenerar (`create-order.sequence`, `data-model.erd`, `order-lifecycle.lifecycle`).

## Nota sobre los recibos de ejecución

Los archivos `*.finalize.json`, `*.finalize-summary.json`, `*.delivery.json` y `*.browser-check.json` son recibos locales generados por la ejecución de `finalize` y **no están versionados**; sirven como evidencia de las comprobaciones realizadas en el entorno de generación.

Una aclaración de lectura: `STOCK_INSUFFICIENT` no es un estado persistido del pedido. En el código es una excepción que responde `409` y deja el pedido en `PENDING`, así que el diagrama de ciclo de vida la representa como salida de error y no como estado.
