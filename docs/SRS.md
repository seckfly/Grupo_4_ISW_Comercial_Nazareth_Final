# Especificación de requisitos de software de Comercial Nazareth

## Propósito y contexto

El sistema organiza las ventas, las existencias y la reposición de Comercial Nazareth, negocio minorista de abarrotes ubicado en Ascope, La Libertad. Humberto Dávalos es el propietario y único trabajador. Registra sus operaciones en cuadernos y estima el stock mediante revisión visual; necesita conocer las cantidades disponibles para decidir qué comprar y cuánto reponer.

Esta especificación reúne el catálogo de quince requisitos funcionales y seis no funcionales del proyecto e incorpora CR-001 en REQ-015. Los identificadores conservan la correspondencia con los documentos anteriores.

## Alcance

Se incluyen ventas, consulta de productos y existencias, mantenimiento de productos e inventario, promociones, solicitudes de separación, consultas del portal de clientes, administración de accesos, resúmenes de ventas, órdenes de compra y recepción de mercadería.

La solución contempla una interfaz React/Vite, un servicio Express y una base MySQL. La venta admite efectivo, Yape y Plin; el registro de una referencia digital identifica el pago indicado por Humberto y no constituye una confirmación bancaria automática.

Quedan fuera del alcance la contabilidad integral, la facturación electrónica, los pagos a proveedores, la apertura y el cierre formal de caja, las notificaciones automáticas y la detección de stock mediante cámaras. El proveedor se comunica con Humberto fuera de la aplicación y no tiene credenciales de acceso.

## Actores y perfiles

| Actor o participante | Relación con el sistema |
|---|---|
| Vendedor | Humberto registra ventas y vincula al cliente cuando se identifica. |
| Administrador | Humberto gestiona promociones y accesos. |
| Responsable de almacén | Humberto consulta existencias y realiza el mantenimiento y los ajustes autorizados. |
| Responsable de compras | Humberto registra órdenes y recepciones. |
| Cliente registrado | Consulta el portal, guarda favoritos y listas y solicita separaciones. |
| Comprador sin registro | Es atendido por el Vendedor y puede comprar sin una cuenta. |
| Proveedor | Entrega mercadería y coordina con Humberto fuera de la aplicación. |

Los cuatro roles internos corresponden al perfil administrativo de Humberto. El cliente registrado utiliza su propio perfil en el portal.

## Requisitos funcionales

| ID | Requisito | Comportamiento requerido | Caso de uso o ámbito |
|---|---|---|---|
| REQ-001 | Registrar venta | El sistema debe registrar los productos, cantidades y método de pago de la venta, calcular el total con los precios del servicio y redondear los importes a dos decimales. La venta, su detalle y la salida de stock deben confirmarse en una misma transacción; ante un error de guardado, deben revertirse sin cambios parciales. | CU-001 |
| REQ-002 | Consultar existencias y alertas | El sistema debe mostrar las existencias y señalar los productos activos cuyo stock sea menor o igual al mínimo configurado. | CU-006 |
| REQ-003 | Identificar proveedor de la orden | El sistema debe guardar razón social, RUC y teléfono del proveedor dentro de la orden, sin exigir un catálogo independiente. | CU-008 |
| REQ-004 | Registrar orden de compra | El sistema debe conservar proveedor, productos, cantidades, costos y estado pendiente, recibida o anulada; calcular el total estimado. | CU-008 |
| REQ-005 | Registrar recepción | El sistema debe registrar cantidades recibidas de una orden pendiente, aumentar el stock y crear movimientos de entrada en una transacción. | CU-009 |
| REQ-006 | Acceder según perfil | El sistema debe permitir inicio y cierre de sesión para el perfil administrativo y el cliente registrado. | Acceso transversal |
| REQ-007 | Consultar catálogo | El sistema debe permitir buscar productos por nombre y categoría, mostrar su precio y disponibilidad, y guardar favoritos y listas en el portal del cliente registrado. | CU-003 |
| REQ-008 | Gestionar promociones | El sistema debe crear, editar, pausar, activar y eliminar campañas por producto, con descuento, vigencia y estado. | CU-004 |
| REQ-009 | Solicitar separación | El sistema debe crear una solicitud con productos, importe estimado y código, conservando el estado de la solicitud. | CU-005 |
| REQ-010 | Vincular cliente a la venta | El sistema debe permitir vincular un cliente registrado a la venta cuando el comprador se identifique y registrar la venta sin cliente asociado cuando no se identifique. | CU-002 |
| REQ-011 | Consultar clientes frecuentes | El sistema debe mostrar nombre, contacto, frecuencia e historial básico de clientes identificados. | Consulta administrativa |
| REQ-012 | Consultar resumen y reportes | El sistema debe mostrar ventas, métodos de pago y productos con movimiento por periodo. | Consulta administrativa |
| REQ-013 | Administrar accesos | El sistema debe registrar, editar y desactivar cuentas con rol autorizado y proteger la cuenta administrativa. | Acceso transversal |
| REQ-014 | Consultar cuenta y beneficios | El sistema debe mostrar al cliente registrado sus datos, historial de compras y puntos asociados a su cuenta. | Portal de clientes |
| REQ-015 | Mantener productos e inventario | El sistema debe permitir registrar y actualizar productos, precios y stock inicial, y realizar ajustes autorizados de existencias conservando su historial. Cada ajuste manual debe incluir un motivo con al menos un carácter distinto de espacios y conservarlo en el historial. Si el motivo está vacío o contiene únicamente espacios, el sistema debe solicitar su corrección sin modificar el stock ni registrar el ajuste. El ajuste, su motivo y la actualización del stock deben guardarse en una misma transacción. Esta condición del motivo no se aplica a las salidas generadas por ventas. | CU-006 |

La solicitud de separación de CU-005 contempla hasta tres productos distintos y un vencimiento de 24 horas, conforme a la especificación del proyecto. La solicitud no confirma una venta ni bloquea existencias.

## Requisitos no funcionales

| ID | Requisito | Condición de aceptación |
|---|---|---|
| RNF-001 | Rapidez de registro | Una venta de hasta tres líneas, con precios cargados y un administrador, se confirma en menos de 15 segundos, sin contar la espera de un pago externo. |
| RNF-002 | Separación de perfiles | Las opciones administrativas quedan fuera de la navegación del cliente y las operaciones protegidas rechazan roles no autorizados. |
| RNF-003 | Tiempo de consulta | Productos, stock y resumen responden en tres segundos o menos, con un usuario concurrente y el catálogo de demostración en entorno local. |
| RNF-004 | Integridad de venta | Venta, detalle y movimiento se confirman juntos; ante un error no quedan modificaciones parciales. |
| RNF-005 | Consistencia monetaria | Totales y subtotales usan dos decimales, con diferencia admitida de S/ 0,00 respecto del cálculo redondeado. |
| RNF-006 | Respaldo recuperable | Conservar una copia de la base de datos al cierre de cada jornada y comprobar su restauración con las ventas incluidas. |

Para RNF-001 se consideran diez operaciones equivalentes, todas bajo el umbral. Para RNF-003 se miden diez consultas por operación en el entorno indicado. RNF-002 se contrasta con las opciones de navegación y el rechazo de operaciones no autorizadas; RNF-004, con ventas válidas, stock insuficiente y fallos de guardado; RNF-005, con cantidades y precios conocidos; RNF-006, mediante restauración y comparación de los registros conservados.

## Reglas del negocio

| ID | Regla |
|---|---|
| BR-001 | Yape y Plin se registran como método de pago. El código de operación no confirma el pago bancario. |
| BR-002 | La venta usa el precio consultado por el servicio y redondea a dos decimales. El cálculo de descuentos debe coincidir entre interfaz y backend. |
| BR-003 | Una venta puede registrarse sin cliente asociado. |
| BR-004 | Una orden de compra no aumenta el stock. El incremento ocurre al confirmar la recepción. |
| BR-005 | Una solicitud de separación no confirma una venta ni garantiza el bloqueo de existencias. |
| BR-006 | La alerta muestra stock menor o igual al mínimo. CU-008 puede extender CU-006 cuando el stock está por debajo del mínimo y Humberto decide reponer. Si el stock equivale al mínimo, se muestra la alerta, pero esa condición por sí sola no activa CU-008. |
| BR-007 | Los datos del proveedor se guardan en la orden. El proveedor no tiene credenciales ni un caso de uso independiente. |
| BR-008 | Una recepción parcial mantiene pendiente la orden y acumula cantidades recibidas. Se rechazan referencias duplicadas y cantidades superiores al saldo por recibir. |

El cálculo de descuentos debe coincidir entre la interfaz y el servicio. En los ajustes manuales de CU-006 se aplica REQ-015: motivo válido, conservación del historial y guardado conjunto del ajuste, el motivo y el stock. Ante un fallo se conserva el estado anterior al intento.

## Trazabilidad del alcance seleccionado

La [matriz](../matrices/trazabilidad.md) relaciona REQ-001, REQ-002, REQ-007, REQ-010 y REQ-015 con sus casos de uso, clases y nueve [casos de prueba](../pruebas/pruebas.md). Su cobertura del 100 % se calcula sobre esos cinco requisitos seleccionados.

El [diagrama general](../modelos/casos-de-uso.png) representa los ocho casos de uso. El [modelo de clases](../modelos/clases.png) corresponde al alcance seleccionado de ventas, catálogo, clientes e inventario. El [proceso crítico](proceso-critico.md) desarrolla CU-006.

## Fuentes del catálogo

- [SRS del proyecto de origen](https://github.com/seckfly/Grupo_4_ISW_Comercial_Nazareth/blob/64f9148301299ef28ec6f473e48544c3ad85b673/docs/iter1-inicio/srs-breve.md).
- Informe de la Evaluación Parcial de Comercial Nazareth, apartados 3 y 5: requisitos y especificaciones de los casos de uso.
- [SRS de la base v2.0.1](https://github.com/seckfly/Grupo_4_ISW_Comercial_Nazareth_Lab7_V2/blob/v2.0.1/docs/SRS.md), que incorpora [CR-001](https://github.com/seckfly/Grupo_4_ISW_Comercial_Nazareth_Lab7/issues/5).
