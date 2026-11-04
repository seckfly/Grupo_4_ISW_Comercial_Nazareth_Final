# Comercial Nazareth: entrega final

Grupo 4 · Ingeniería de Software

Sistema de gestión comercial y portal de clientes de Comercial Nazareth. Esta entrega parte de v2.0.1 e integra el SRS completo, los ocho casos de uso y el flujo del proceso crítico CU-006: Gestionar inventario.

## Integrantes

| Integrante | Código |
|---|---|
| Marco Antonio Martell Alvarez | N00471929 |
| Alejandro Horna Quezada | N00475530 |
| Isaí Samuel Bejarano Benites | N00490010 |
| Cesar Jeremin Alonso Chuquimango Reyes | N00480808 |
| Alonso Castillo Davalos | N00491764 |


## Documentos

| Documento | Contenido |
|---|---|
| [SRS completo](docs/SRS.md) | Quince requisitos funcionales, seis no funcionales y ocho reglas del negocio. |
| [Casos de uso](docs/CU.md) | Ocho casos de uso, sus actores, flujos y excepciones. |
| [Proceso crítico](docs/proceso-critico.md) | Justificación y flujo de CU-006, con los controles del ajuste manual. |
| [Convención de identificadores](docs/convencion-ids.md) | Identificadores y correspondencia con el proyecto de origen. |
| [Matriz de trazabilidad](matrices/trazabilidad.md) | Relaciones de los cinco requisitos seleccionados para el laboratorio. |
| [Pruebas](pruebas/pruebas.md) | Nueve casos de prueba del alcance seleccionado. |
| [Agilidad y concurrencia](docs/agilidad.md) | Kanban, límites de dos tarjetas por etapa y evidencias del flujo de V2. |
| [Reporte v1.1](reportes/reporte-v1.1.md) | Comparación histórica entre v1.0 y v1.1. |

## Modelos

| Modelo | Visualización | Fuente editable |
|---|---|---|
| Casos de uso del sistema | [PNG](modelos/casos-de-uso.png) | Diagrama conservado del proyecto de origen. |
| Clases del alcance seleccionado | [PNG](modelos/clases.png) | [draw.io](modelos/clases.drawio) |
| Flujo de CU-006: Gestionar inventario | [PNG](modelos/actividad-gestionar-inventario.png) | [draw.io](modelos/actividad-gestionar-inventario.drawio) · [XML](modelos/actividad-gestionar-inventario.xml) |

## Alcance de la trazabilidad

El SRS reúne el catálogo completo del proyecto. La matriz, el modelo de clases y las nueve pruebas conservan el alcance de REQ-001, REQ-002, REQ-007, REQ-010 y REQ-015. La cobertura del 100 % corresponde a esos cinco requisitos seleccionados.

CU-006 incorpora CR-001: cada ajuste manual requiere un motivo válido y conserva el ajuste, el motivo y el stock en una misma transacción. El flujo de esta entrega desarrolla ese proceso y su relación con la reposición.

## Kanban

[Tablero de Comercial Nazareth](https://trello.com/b/9LEaT3KG/comercial-nazareth-kanban-v2). En curso y En revisión admiten un máximo de dos tarjetas cada una. Las reglas contemplan capacidad, bloqueos, correcciones y criterios de cierre.

## Antecedentes

- [Base v2.0.1](https://github.com/seckfly/Grupo_4_ISW_Comercial_Nazareth_Lab7_V2/tree/v2.0.1).
- [Repositorio del proyecto de origen](https://github.com/seckfly/Grupo_4_ISW_Comercial_Nazareth).
- [Repositorio del laboratorio 7](https://github.com/seckfly/Grupo_4_ISW_Comercial_Nazareth_Lab7).
- [CR-001](https://github.com/seckfly/Grupo_4_ISW_Comercial_Nazareth_Lab7/issues/5).
