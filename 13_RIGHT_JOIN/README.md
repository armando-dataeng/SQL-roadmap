# RIGHT JOIN

## Definición

La cláusula `RIGHT JOIN` permite combinar registros de dos tablas relacionadas.

A diferencia de `INNER JOIN`, `RIGHT JOIN` conserva todas las filas de la tabla derecha, incluso cuando no existe una coincidencia en la tabla izquierda.

Cuando no existe coincidencia, SQL devuelve NULL en las columnas de la tabla izquierda.

---

## Conceptos clave

RIGHT JOIN responde a la pregunta:

> ¿Cómo puedo conservar todos los registros de la tabla derecha aunque no tengan relación en la tabla izquierda?

Características:

- Conserva todas las filas de la tabla derecha.
- Devuelve las coincidencias encontradas en la tabla izquierda.
- Si no existe coincidencia, devuelve NULL.
- No modifica ninguna tabla.

---

## Sintaxis

```sql
SELECT columnas
FROM TablaA
RIGHT JOIN TablaB
    ON TablaA.Columna = TablaB.Columna;
```

Ejemplo:

```sql
SELECT
    c.Nombre,
    cu.NumeroCuenta
FROM Clientes c
RIGHT JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

---

## Relación utilizada

### Tabla Clientes

| IdCliente | Nombre |
|------------|---------|
| 1 | Juan |
| 2 | Ana |

### Tabla Cuentas

| IdCuenta | NumeroCuenta | IdCliente |
|-----------|-------------|------------|
| 101 | 0001 | 1 |
| 102 | 0002 | 2 |
| 103 | 0003 | 5 |

---

## Resultado

| Nombre | NumeroCuenta |
|----------|-------------|
| Juan | 0001 |
| Ana | 0002 |
| NULL | 0003 |

La cuenta 0003 aparece porque RIGHT JOIN conserva todas las filas de la tabla derecha.

---

## Problema

Mostrar todas las cuentas bancarias, incluso si no tienen un cliente asociado.

### Datos

Tablas:

```text
Clientes
Cuentas
```

Relación:

```text
Clientes.IdCliente
=
Cuentas.IdCliente
```

### Lógica

Mostrar todas las cuentas.

Si existe cliente:

```text
Mostrar el cliente.
```

Si no existe cliente:

```text
Mostrar NULL.
```

### SQL

```sql
SELECT
    c.Nombre,
    cu.NumeroCuenta
FROM Clientes c
RIGHT JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

---

## Tabla izquierda y tabla derecha

En:

```sql
FROM Clientes c
RIGHT JOIN Cuentas cu
```

Tabla izquierda:

```text
Clientes
```

Tabla derecha:

```text
Cuentas
```

RIGHT JOIN siempre conserva las filas de la tabla derecha.

---

## La cláusula ON

```sql
ON c.IdCliente = cu.IdCliente
```

SQL compara:

```text
Clientes.IdCliente
```

con

```text
Cuentas.IdCliente
```

Cuando encuentra coincidencia:

```text
Une temporalmente las filas.
```

Cuando no encuentra coincidencia:

```text
Conserva la fila derecha y rellena con NULL la izquierda.
```

---

## Casos de uso reales

### Todas las cuentas registradas

```sql
SELECT
    c.Nombre,
    cu.NumeroCuenta
FROM Clientes c
RIGHT JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

Caso:

```text
Auditar cuentas sin propietario asociado.
```

---

### Todas las transacciones

```sql
SELECT
    cu.NumeroCuenta,
    t.Monto
FROM Cuentas cu
RIGHT JOIN Transacciones t
    ON cu.IdCuenta = t.IdCuenta;
```

Caso:

```text
Detectar movimientos huérfanos.
```

---

## Diferencia entre INNER JOIN y RIGHT JOIN

### INNER JOIN

```sql
SELECT
    c.Nombre,
    cu.NumeroCuenta
FROM Clientes c
INNER JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

Resultado:

```text
Juan
Ana
```

---

### RIGHT JOIN

```sql
SELECT
    c.Nombre,
    cu.NumeroCuenta
FROM Clientes c
RIGHT JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

Resultado:

```text
Juan
Ana
NULL
```

---

## Diferencia entre LEFT JOIN y RIGHT JOIN

### LEFT JOIN

Conserva:

```text
Tabla izquierda
```

---

### RIGHT JOIN

Conserva:

```text
Tabla derecha
```

---

## Equivalencia importante

Estas dos consultas producen el mismo resultado:

### RIGHT JOIN

```sql
SELECT
    c.Nombre,
    cu.NumeroCuenta
FROM Clientes c
RIGHT JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

### LEFT JOIN invertido

```sql
SELECT
    c.Nombre,
    cu.NumeroCuenta
FROM Cuentas cu
LEFT JOIN Clientes c
    ON cu.IdCliente = c.IdCliente;
```

Por esta razón, muchos desarrolladores prefieren utilizar LEFT JOIN en lugar de RIGHT JOIN.

---

## Error común

❌ Incorrecto

```sql
SELECT *
FROM Clientes c
RIGHT JOIN Cuentas cu;
```

✔ Correcto

```sql
SELECT *
FROM Clientes c
RIGHT JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

---

## Error conceptual frecuente

Muchos principiantes creen que:

```sql
RIGHT JOIN
```

es diferente a invertir las tablas y usar:

```sql
LEFT JOIN
```

En muchos casos prácticos ambos producen exactamente el mismo resultado.

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar RIGHT JOIN pregúntate:

1. ¿Qué tabla necesito conservar completamente?
2. ¿Puedo invertir las tablas y utilizar LEFT JOIN?
3. ¿Existen registros huérfanos que necesito detectar?
4. ¿Cómo interpretaré los valores NULL?

### Relación entre conceptos

INNER JOIN responde:

> ¿Qué registros coinciden?

LEFT JOIN responde:

> ¿Qué registros existen en la tabla izquierda aunque no tengan coincidencia?

RIGHT JOIN responde:

> ¿Qué registros existen en la tabla derecha aunque no tengan coincidencia?

---

## Resumen

RIGHT JOIN combina registros de dos tablas relacionadas.

Características principales:

- Conserva todas las filas de la tabla derecha.
- Devuelve coincidencias de la tabla izquierda.
- Utiliza NULL cuando no existe coincidencia.
- No modifica datos.
- Puede reemplazarse por LEFT JOIN invirtiendo las tablas.

Se utiliza para:

- Auditorías.
- Detección de registros huérfanos.
- Validación de integridad.
- Ingeniería de Datos.
- Análisis de calidad de datos.
