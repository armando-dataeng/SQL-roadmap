# Modelo de Datos

## Clientes

| Campo | Tipo |
|---------|---------|
| IdCliente | int |
| Nombre | nvarchar |
| Apellido | nvarchar |
| Cedula | nvarchar |
| Telefono | nvarchar |
| Email | nvarchar |
| FechaRegistro | datetime |
| Activo | bit |

---

## Cuentas

| Campo | Tipo |
|---------|---------|
| IdCuenta | int |
| NumeroCuenta | nvarchar |
| IdCliente | int |
| TipoCuenta | nvarchar |
| Saldo | decimal |
| FechaCreacion | datetime |
| Activa | bit |

---

## Transacciones

| Campo | Tipo |
|---------|---------|
| IdTransaccion | int |
| IdCuenta | int |
| TipoTransaccion | nvarchar |
| Monto | decimal |
| FechaTransaccion | datetime |

---

## Usuarios

| Campo | Tipo |
|---------|---------|
| IdUsuario | int |
| Usuario | nvarchar |
| Contrasena | nvarchar |
| Rol | nvarchar |
| FechaCreacion | datetime |
| Correo | nvarchar |
| Nombre | nvarchar |

---

## Relaciones

Clientes (1) → (N) Cuentas

Cuentas (1) → (N) Transacciones
