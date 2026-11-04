# SRS de Comercial Nazareth (v1.1)

Humberto Dávalos es el propietario y único trabajador del negocio y desempeña los roles internos del sistema. El cliente registrado utiliza el portal.

| ID | Requisito |
|---|---|
| REQ-001 | El sistema debe registrar los productos, cantidades y método de pago de la venta, calcular el total con los precios del servicio y redondear los importes a dos decimales. La venta, su detalle y la salida de stock deben confirmarse en una misma transacción; ante un error de guardado, deben revertirse sin cambios parciales. |
| REQ-002 | El sistema debe mostrar las existencias y señalar los productos activos cuyo stock sea menor o igual al mínimo configurado. |
| REQ-007 | El sistema debe permitir buscar productos por nombre y categoría, mostrar su precio y disponibilidad, y guardar favoritos y listas en el portal del cliente registrado. |
| REQ-010 | El sistema debe permitir vincular un cliente registrado a la venta cuando el comprador se identifique y registrar la venta sin cliente asociado cuando no se identifique. |
| REQ-015 | El sistema debe permitir registrar y actualizar productos, precios y stock inicial, y realizar ajustes autorizados de existencias conservando su historial. Cada ajuste manual debe incluir un motivo con al menos un carácter distinto de espacios y conservarlo en el historial. Si el motivo está vacío o contiene únicamente espacios, el sistema debe solicitar su corrección sin modificar el stock ni registrar el ajuste. El ajuste, su motivo y la actualización del stock deben guardarse en una misma transacción. Esta condición del motivo no se aplica a las salidas generadas por ventas. |

## Reglas aplicables

- Los métodos de pago son efectivo, Yape y Plin. La referencia de Yape o Plin no constituye una confirmación bancaria automática.
- El cálculo de descuentos debe coincidir entre la interfaz y el servicio.
