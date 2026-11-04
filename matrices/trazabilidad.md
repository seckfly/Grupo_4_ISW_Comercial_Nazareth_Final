# Matriz de trazabilidad de Comercial Nazareth (adaptación ágil V2)

La columna «¿Cubierto?» indica si el requisito está vinculado a un caso de uso, una clase y una prueba.

| Requisito | Descripción | Caso de uso | Clase | Prueba | ¿Cubierto? | Último CR |
|---|---|---|---|---|---|---|
| REQ-001 | Registrar venta | CU-001 | CLS-Venta, CLS-DetalleVenta, CLS-Producto, CLS-MovimientoInventario | PRU-001, PRU-003 | Sí | No aplica |
| REQ-002 | Consultar existencias y alertas | CU-006 | CLS-Producto | PRU-002 | Sí | No aplica |
| REQ-007 | Consultar catálogo, favoritos y listas | CU-003, incluido por CU-001 | CLS-Producto, CLS-ListaProductos, CLS-Cliente | PRU-007 | Sí | No aplica |
| REQ-010 | Vincular cliente a la venta | CU-002; extiende CU-001 | CLS-Cliente, CLS-Venta | PRU-004 | Sí | No aplica |
| REQ-015 | Mantener productos e inventario con motivo en ajustes manuales | CU-006 | CLS-Producto, CLS-MovimientoInventario | PRU-016, PRU-017, PRU-018, PRU-019 | Sí | CR-001 |

**Cobertura:** 5 de 5 requisitos con prueba = (5 ÷ 5) × 100 = 100 %
