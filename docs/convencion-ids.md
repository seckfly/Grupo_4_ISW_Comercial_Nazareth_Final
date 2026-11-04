# Convención de identificadores

| Elemento | Formato | Ejemplo |
|---|---|---|
| Requisito funcional | REQ-### | REQ-001 |
| Requisito no funcional | RNF-### | RNF-001 |
| Regla del negocio | BR-### | BR-001 |
| Caso de uso | CU-### | CU-001 |
| Clase | CLS-Nombre | CLS-Venta |
| Prueba | PRU-### | PRU-001 |
| Solicitud de cambio | CR-### | CR-001 |

Cada identificador corresponde a un solo elemento. Se conserva cuando se modifica el contenido y no se reutiliza si el elemento se retira.

PRU identifica una prueba documentada. Pull Request identifica la solicitud de integración de GitHub.

## Correspondencia con el proyecto de origen

El número de cada requisito se conserva al normalizar su formato. Los identificadores REQ-001, REQ-002, REQ-007, REQ-010 y REQ-015 mantienen el significado empleado en v2.0.1.

| Elemento | Código de origen | Código de esta entrega |
|---|---|---|
| Registrar venta | RF-01 | REQ-001 |
| Consultar existencias y alertas | RF-02 | REQ-002 |
| Identificar proveedor de la orden | RF-03 | REQ-003 |
| Registrar orden de compra | RF-04 | REQ-004 |
| Registrar recepción | RF-05 | REQ-005 |
| Acceder según perfil | RF-06 | REQ-006 |
| Consultar catálogo | RF-07 | REQ-007 |
| Gestionar promociones | RF-08 | REQ-008 |
| Solicitar separación | RF-09 | REQ-009 |
| Vincular cliente a la venta | RF-10 | REQ-010 |
| Consultar clientes frecuentes | RF-11 | REQ-011 |
| Consultar resumen y reportes | RF-12 | REQ-012 |
| Administrar accesos | RF-13 | REQ-013 |
| Consultar cuenta y beneficios | RF-14 | REQ-014 |
| Mantener productos e inventario | RF-15 | REQ-015 |
| Requisitos no funcionales | RNF-01 a RNF-06 | RNF-001 a RNF-006 |
| Reglas del negocio | BR-01 a BR-08 | BR-001 a BR-008 |
| Casos de uso | CU01, CU02, CU03, CU04, CU05, CU06, CU08, CU09 | CU-001, CU-002, CU-003, CU-004, CU-005, CU-006, CU-008, CU-009 |
