# COUNT()

## Definición

La función COUNT() permite contar registros en una tabla.

Es una de las funciones agregadas más utilizadas en SQL.

---

## Conceptos clave

COUNT responde a la pregunta:

> ¿Cuántos registros existen?

COUNT devuelve un único valor numérico.

No modifica datos.

---

## Sintaxis

```sql
SELECT COUNT(*)
FROM Clientes;
```

---

## Problema

Determinar cuántos clientes existen registrados.

### Datos

Tabla:

```text
Clientes
```

### Lógica

Contar todas las filas de la tabla.

### SQL

```sql
SELECT COUNT(*)
FROM Clientes;
```

---

## COUNT(*)

Cuenta todas las filas.

```sql
SELECT COUNT(*)
FROM Clientes;
```

Ejemplo:

```text
150
```

Significa:

```text
Existen 150 clientes.
```

---

## COUNT(columna)

Cuenta únicamente los valores NO NULL.

```sql
SELECT COUNT(Email)
FROM Clientes;
```

Si existen:

```text
150 clientes
120 correos registrados
```

Resultado:

```text
120
```

---

## Casos de uso reales

### Cantidad de clientes

```sql
SELECT COUNT(*)
FROM Clientes;
```

Caso:

```text
Conocer el número total de clientes.
```

---

### Cantidad de cuentas

```sql
SELECT COUNT(*)
FROM Cuentas;
```

Caso:

```text
Conocer cuántas cuentas existen.
```

---

### Cantidad de transacciones

```sql
SELECT COUNT(*)
FROM Transacciones;
```

Caso:

```text
Conocer el volumen de operaciones.
```

---

### Clientes activos

```sql
SELECT COUNT(*)
FROM Clientes
WHERE Activo = 1;
```

Caso:

```text
Conocer cuántos clientes están activos.
```

---

## Error común

❌ Incorrecto

```sql
SELECT Nombre, COUNT(*)
FROM Clientes;
```

✔ Correcto

```sql
SELECT COUNT(*)
FROM Clientes;
```

---

## Error conceptual frecuente

Muchos principiantes creen que:

```sql
COUNT(*)
```

cuenta columnas.

Incorrecto.

COUNT(*) cuenta filas.

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar COUNT pregúntate:

1. ¿Necesito contar filas?
2. ¿Necesito contar valores no nulos?
3. ¿Necesito contar registros filtrados?
4. ¿Necesito agrupar resultados?

---

## Resumen

COUNT() permite contar registros.

Principales variantes:

```sql
COUNT(*)
COUNT(columna)
```

Se utiliza para:

- Reportes
- KPIs
- Dashboards
- Auditorías
- Data Engineering
- Business Intelligence
