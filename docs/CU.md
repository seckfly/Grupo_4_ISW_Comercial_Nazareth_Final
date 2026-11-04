# Casos de uso de Comercial Nazareth (v1.1)

| ID | Caso de uso | Actor | Requisitos relacionados |
|---|---|---|---|
| CU-001 | Registrar venta | Vendedor | REQ-001; utiliza REQ-007 y, cuando el comprador se identifica, REQ-010 |
| CU-002 | Vincular cliente a la venta | Vendedor | REQ-010 |
| CU-003 | Consultar catálogo | Cliente registrado, Vendedor y Responsable de compras | REQ-007 |
| CU-006 | Gestionar inventario | Responsable de almacén | REQ-002, REQ-015 |

## CU-001: Registrar venta

Actor: Vendedor, rol desempeñado por Humberto Dávalos.

Precondiciones: Humberto tiene una sesión administrativa activa. Los productos están activos y cuentan con precio y stock registrados.

### Flujo principal

1. Humberto consulta el catálogo mediante CU-003 y selecciona los productos y cantidades de la venta.
2. El sistema comprueba que la venta tenga productos, que las cantidades sean positivas y que exista stock suficiente.
3. Si el comprador se identifica como cliente registrado, Humberto lo vincula mediante CU-002. En caso contrario, continúa sin cliente asociado.
4. Humberto elige efectivo, Yape o Plin. El sistema calcula el total con los precios del servicio y muestra los campos del método elegido.
5. Humberto registra el monto recibido en efectivo o la referencia de la operación digital.
6. El sistema valida el monto recibido en efectivo o la referencia de la operación digital, según el método elegido, y calcula el vuelto cuando corresponde.
7. El sistema guarda la cabecera y el detalle de la venta, registra la salida de inventario y descuenta el stock en una misma transacción.
8. El sistema confirma el guardado y muestra el identificador de la venta.

### Alternativas y excepciones

| Situación | Respuesta |
|---|---|
| El comprador no se identifica como cliente registrado | Continuar sin vincular una cuenta. |
| El monto recibido en efectivo supera el total | Calcular y mostrar el vuelto. |
| Se selecciona Yape o Plin | Registrar la referencia digital sin atribuirle una confirmación bancaria automática. |
| La venta está vacía o contiene cantidades no válidas | Solicitar la corrección antes de continuar. |
| Un producto no tiene stock suficiente | Identificar el producto y rechazar el intento actual. Humberto puede iniciar una nueva selección. |
| El monto recibido o la referencia digital no son válidos para el método elegido | Solicitar la corrección antes de guardar. |
| Falla el guardado | Revertir la transacción y mostrar que la venta no fue confirmada. |

Postcondición de éxito: quedan guardados la venta, su detalle y el movimiento de salida, con el stock actualizado.

Postcondición ante fallo de guardado: no quedan una venta parcial ni descuentos de stock correspondientes a una venta sin confirmar.

CU-001 incluye CU-003. CU-002 extiende CU-001 cuando el comprador se identifica como cliente registrado.

## CU-002: Vincular cliente a la venta

Actor: Vendedor, rol desempeñado por Humberto Dávalos.

Requisito relacionado: REQ-010.

Relación: extiende CU-001 cuando el comprador se identifica como cliente registrado. La vinculación es opcional y no impide guardar la venta.

Precondiciones: Humberto tiene una sesión administrativa activa y una venta en curso en CU-001. El comprador se identifica como cliente registrado.

### Flujo principal
1. Humberto busca al cliente registrado con los datos que proporciona el comprador.
2. El sistema muestra el cliente que coincide.
3. Humberto confirma que es el cliente indicado por el comprador.
4. El sistema asocia el cliente a la venta en curso.
5. El sistema devuelve el control a CU-001, que continúa con la elección del método de pago.

### Alternativas y excepciones

| Situación | Respuesta |
|---|---|
| El comprador no se identifica | CU-002 no se ejecuta. La venta continúa sin cliente asociado. |
| El sistema no encuentra un cliente registrado con los datos indicados | Humberto repite la búsqueda o continúa la venta sin cliente asociado. |

Postcondición de éxito: la venta en curso queda asociada a un cliente registrado. La vinculación no modifica los productos, el total ni el método de pago.

Postcondición sin vinculación: la venta continúa sin cliente asociado y puede confirmarse.

## CU-003: Consultar catálogo

Actores: Cliente registrado, Vendedor y Responsable de compras.

Requisito relacionado: REQ-007.

Relación: CU-001 incluye CU-003.

Precondiciones: hay productos registrados. Para guardar favoritos y listas, el cliente registrado tiene una sesión iniciada en el portal.

### Flujo principal
1. El actor ingresa el nombre del producto, elige una categoría, o ambos.
2. El sistema busca los productos que coinciden.
3. El sistema muestra cada coincidencia con su nombre, precio y disponibilidad.
4. El cliente registrado guarda un producto en favoritos o en una lista.
5. El sistema conserva la selección en el portal del cliente.

### Alternativas y excepciones

| Situación | Respuesta |
|---|---|
| La búsqueda no tiene coincidencias | El sistema indica que no se encontraron productos. |
| El actor es el Vendedor o el Responsable de compras | Consulta precio y disponibilidad. Los favoritos y las listas pertenecen al portal del cliente registrado. |
| El actor no es un cliente registrado | Puede consultar el catálogo, pero no guardar favoritos ni listas. |
| CU-001 invoca la consulta | Humberto elige los productos y cantidades de la venta desde los resultados. |

Postcondición de éxito: el actor ve los resultados con precio y disponibilidad. Si el cliente registrado guardó favoritos o listas, quedan conservados.

## CU-006: Gestionar inventario

Actor: Responsable de almacén, rol desempeñado por Humberto Dávalos.

Requisitos relacionados: REQ-002 y REQ-015.

Precondiciones: Humberto tiene una sesión administrativa activa con acceso autorizado para el mantenimiento de productos y los ajustes de existencias.

### Flujo principal
1. Humberto consulta las existencias.
2. El sistema muestra las existencias y señala los productos activos cuyo stock es menor o igual al mínimo configurado.
3. Humberto registra un producto con su precio y stock inicial, o actualiza el precio de un producto existente.
4. Humberto indica el ajuste manual de existencias y su motivo.
5. El sistema comprueba que el motivo contenga al menos un carácter distinto de espacios.
6. El sistema guarda el ajuste y su motivo en el historial y actualiza el stock en una misma transacción.
7. Humberto consulta el historial, que muestra el motivo de cada ajuste y conserva los registros anteriores.

### Alternativas y excepciones

| Situación | Respuesta |
|---|---|
| El stock de un producto activo es igual al mínimo configurado | El sistema lo señala en la alerta. |
| Un producto inactivo tiene stock menor o igual al mínimo | El sistema no lo incluye en la alerta. |
| El usuario no tiene acceso autorizado | El sistema rechaza el mantenimiento de productos y los ajustes, y no guarda cambios. |
| El motivo está vacío o contiene únicamente espacios | El sistema solicita corregir el motivo. El stock permanece sin cambios y no se registra el ajuste. |
| Falla el guardado del ajuste, su motivo o el stock | El sistema revierte la transacción. El stock y el historial conservan el estado anterior al intento. |

Postcondición de éxito: los productos, precios y existencias quedan actualizados. Cada ajuste manual conserva su motivo en el historial, junto con los ajustes anteriores.

La exigencia del motivo corresponde a los ajustes manuales de CU-006. Las salidas de inventario por ventas siguen el flujo de CU-001.
