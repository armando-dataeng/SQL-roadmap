# VIEWS

## Definición

Una View (Vista) es una consulta SQL almacenada que puede ser utilizada como si fuera una tabla.

Las vistas no almacenan datos físicamente.

Al consultar una vista, SQL ejecuta la consulta definida en ella y devuelve los resultados.

---

## Conceptos clave

Una vista responde a la pregunta:

> ¿Cómo puedo reutilizar consultas complejas sin escribirlas repetidamente?

Características:

- Simplifican consultas complejas.
- Mejoran la reutilización.
- Facilitan la seguridad.
- No almacenan datos.
- Se actualizan automáticamente cuando cambian los datos base.

---

## Sintaxis

### Crear una vista

```sql
CREATE VIEW NombreVista
AS
SELECT columnas
FROM tabla;
```

### Consultar una vista

```sql
SELECT *
FROM NombreVista;
```

### Eliminar una vista

```sql
DROP VIEW NombreVista;
```

---

## Primer ejemplo

### Problema

Mostrar únicamente los clientes activos.

### Datos

Tabla:

```text
Clientes
```

### Lógica

Guardar la consulta para reutilizarla.

### SQL

```sql
CREATE VIEW vw_ClientesActivos
AS
SELECT *
FROM Clientes
WHERE Activo = 1;
```

---

## Consultar la vista

```sql
SELECT *
FROM vw_ClientesActivos;
```

---

## Caso bancario

### Problema

Mostrar el saldo total por cliente.

### SQL

```sql
CREATE VIEW vw_SaldoClientes
AS
SELECT
    IdCliente,
    SUM(Saldo) AS SaldoTotal
FROM Cuentas
GROUP BY IdCliente;
```

---

## Consultar la vista

```sql
SELECT *
FROM vw_SaldoClientes;
```

---

## ¿Qué ventaja tiene?

Sin vista:

```sql
SELECT
    IdCliente,
    SUM(Saldo) AS SaldoTotal
FROM Cuentas
GROUP BY IdCliente;
```

Cada vez debes escribir toda la consulta.

Con vista:

```sql
SELECT *
FROM vw_SaldoClientes;
```

Más simple y reutilizable.

---

## Vistas con JOIN

### Problema

Mostrar clientes y sus cuentas.

### SQL

```sql
CREATE VIEW vw_ClientesCuentas
AS
SELECT
    c.IdCliente,
    c.Nombre,
    cu.NumeroCuenta,
    cu.Saldo
FROM Clientes c
INNER JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

---

## Consultar la vista

```sql
SELECT *
FROM vw_ClientesCuentas;
```

---

## Casos de uso reales

### Business Intelligence

```sql
CREATE VIEW vw_VentasMensuales
AS
SELECT
    Mes,
    SUM(Ventas) AS TotalVentas
FROM Ventas
GROUP BY Mes;
```

---

### Data Engineering

```sql
CREATE VIEW vw_TransaccionesDiarias
AS
SELECT
    FechaTransaccion,
    SUM(Monto) AS TotalDia
FROM Transacciones
GROUP BY FechaTransaccion;
```

---

### Reporting

```sql
CREATE VIEW vw_ClientesVIP
AS
SELECT *
FROM Clientes
WHERE NivelCliente = 'VIP';
```

---

## Seguridad mediante vistas

Una vista puede ocultar información sensible.

### Tabla original

```sql
SELECT *
FROM Clientes;
```

Columnas:

```text
IdCliente
Nombre
Correo
Telefono
Salario
```

---

### Vista

```sql
CREATE VIEW vw_ClientesPublicos
AS
SELECT
    IdCliente,
    Nombre
FROM Clientes;
```

---

### Resultado

Los usuarios solo verán:

```text
IdCliente
Nombre
```

---

## Modificar una vista

### SQL Server

```sql
ALTER VIEW vw_ClientesActivos
AS
SELECT *
FROM Clientes
WHERE Activo = 1;
```

---

## Eliminar una vista

```sql
DROP VIEW vw_ClientesActivos;
```

---

## Error común

❌ Incorrecto

```sql
CREATE VIEW vw_Clientes
SELECT *
FROM Clientes;
```

✔ Correcto

```sql
CREATE VIEW vw_Clientes
AS
SELECT *
FROM Clientes;
```

---

## Error conceptual frecuente

Muchos principiantes creen que:

```text
Una vista almacena datos.
```

Incorrecto.

Una vista almacena:

```text
La consulta.
```

No los datos.

Cada vez que consultas la vista:

```text
SQL ejecuta nuevamente la consulta.
```

---

## Pensamiento de Ingeniería de Datos

Antes de crear una vista pregúntate:

1. ¿Esta consulta será reutilizada?
2. ¿Es una consulta compleja?
3. ¿Necesito simplificar reportes?
4. ¿Debo ocultar información sensible?
5. ¿Esta lógica pertenece a la capa de datos?

---

## Relación con otros conceptos

```text
SELECT             → Obtener datos
JOIN               → Relacionar tablas
GROUP BY           → Agrupar datos
CTE                → Consulta temporal
VIEW               → Consulta persistente reutilizable
```

---

## Diferencia entre CTE y VIEW

### CTE

```sql
WITH ClientesCTE AS
(
    SELECT *
    FROM Clientes
)
SELECT *
FROM ClientesCTE;
```

Existe únicamente durante la ejecución.

---

### VIEW

```sql
CREATE VIEW vw_Clientes
AS
SELECT *
FROM Clientes;
```

Permanece almacenada en la base de datos.

---

## Resumen

Las Views permiten encapsular consultas SQL y reutilizarlas como si fueran tablas.

Ventajas:

- Reutilización.
- Legibilidad.
- Seguridad.
- Simplificación de consultas.
- Integración con BI y Reporting.

Son ampliamente utilizadas en:

- SQL Server
- PostgreSQL
- Oracle
- MySQL
- Data Engineering
- Business Intelligence
- Sistemas empresariales
