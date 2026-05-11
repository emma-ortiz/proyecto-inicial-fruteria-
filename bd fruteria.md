Actua como un administrador de base de datos; proyecto fruteria , que entidades se necesitan para su gestion

<img width="1026" height="691" alt="image" src="https://github.com/user-attachments/assets/43182432-aeca-4cd1-b230-a81eb3aac6bf" />
## Entidades para la Gestión de una Frutería

Para un sistema de gestión de frutería, estas son las entidades principales:

---

### 🛒 Núcleo comercial

**Producto**
Nombre, tipo (fruta/verdura), unidad de medida, precio de venta, precio de compra, stock actual, stock mínimo, imagen

**Categoría**
Nombre (cítricos, tropicales, verduras de hoja, etc.), descripción

**Proveedor**
Nombre, RFC/NIT, contacto, teléfono, email, dirección, condiciones de pago

---

### 👥 Clientes y ventas

**Cliente**
Nombre, teléfono, email, dirección, tipo (mayoreo/menudeo), RFC (opcional para factura)

**Venta**
Fecha, folio, cliente, empleado, total, descuento, forma de pago, estado

**DetalleVenta**
Producto, cantidad, precio unitario, subtotal (tabla pivote Venta–Producto)

---

### 📦 Inventario y compras

**Compra**
Fecha, proveedor, empleado, total, estado (pendiente/recibida)

**DetalleCompra**
Producto, cantidad, precio unitario, subtotal

**MovimientoInventario**
Tipo (entrada/salida/merma/ajuste), producto, cantidad, fecha, motivo, empleado

---

### 👨‍💼 Operación interna

**Empleado**
Nombre, puesto, teléfono, fecha de ingreso, usuario del sistema

**Caja / Turno**
Empleado, fecha apertura/cierre, fondo inicial, total ventas, total gastos, diferencia

**Gasto**
Concepto, monto, fecha, categoría, empleado que registra

---

### 🔧 Catálogos de soporte

**UnidadMedida** — kg, pieza, manojo, caja, etc.
**FormaPago** — efectivo, tarjeta, transferencia
**TipoMovimiento** — para el inventario

---

## Relaciones clave

```
Categoría       1──N  Producto
Proveedor       1──N  Compra
Compra          1──N  DetalleCompra ──N──1  Producto
Cliente         1──N  Venta
Venta           1──N  DetalleVenta  ──N──1  Producto
Empleado        1──N  Venta / Compra / MovimientoInventario
Producto        1──N  MovimientoInventario
```

---

¿Quieres que genere el **diagrama ER**, el **script SQL** de creación de tablas, o profundizamos en alguna entidad en particular?


proporciona las entidades con sus atributos y tipo en forma de trabla para cada una de las entidades

##tablas
<img width="753" height="662" alt="image" src="https://github.com/user-attachments/assets/bd0a4042-aee2-4bb7-9ed9-5168f47dcf3f" />
<img width="749" height="638" alt="image" src="https://github.com/user-attachments/assets/dfcd2d19-db38-4a47-87cc-7ed3b5b72b40" />
<img width="758" height="716" alt="image" src="https://github.com/user-attachments/assets/f2683b5f-d821-454b-adf8-326ab0063216" />
<img width="745" height="744" alt="image" src="https://github.com/user-attachments/assets/d72a9d3c-f771-458a-b18b-44f175a93290" />
<img width="745" height="646" alt="image" src="https://github.com/user-attachments/assets/f462784c-4fac-446d-8575-c609b9a87572" />
<img width="760" height="273" alt="image" src="https://github.com/user-attachments/assets/1581e4cd-eebe-4757-ac49-ce32728cb860" />

## de acuerdo a tu respuesta anterior puedes generar un script de sql 


