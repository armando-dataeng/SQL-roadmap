# FULL JOIN

## Definición

La cláusula `FULL JOIN` permite combinar registros de dos tablas relacionadas.

Devuelve:

- Las filas que coinciden entre ambas tablas.
- Las filas que existen únicamente en la tabla izquierda.
- Las filas que existen únicamente en la tabla derecha.

Cuando no existe coincidencia, SQL rellena las columnas faltantes con NULL.

---

## Conceptos clave

FULL JOIN responde a la pregunta:

> ¿Cómo puedo visualizar todos los registros de ambas tablas, independientemente de que tengan coincidencia?

Características:

- Conserva todas las filas de ambas tablas.
- Devuelve coincidencias cuando existen.
- Utiliza NULL cuando no existe coincidencia.
- No modifica ninguna tabla.

---

## Sintaxis

```sql
SELECT columnas
FROM TablaA
FULL JOIN TablaB
    ON TablaA.Columna = TablaB.Columna;
```

Ejemplo:

```sql
SELECT
    c.Nombre,
    cu.NumeroCuenta
FROM Clientes c
FULL JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

---

## Relación utilizada

### Tabla Clientes

| IdCliente | Nombre |
|------------|---------|
| 1 | Juan |
| 2 | Ana |
| 3 | Pedro |

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
| Pedro | NULL |
| NULL | 0003 |

Observa que:

- Pedro aparece aunque no tenga cuenta.
- La cuenta 0003 aparece aunque no tenga cliente.

FULL JOIN conserva ambas tablas completas.

---

## Problema

Mostrar todos los clientes y todas las cuentas, independientemente de que exista una relación entre ellos.

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

Mostrar:

```text
Coincidencias
+
Clientes sin cuenta
+
Cuentas sin cliente
```

### SQL

```sql
SELECT
    c.Nombre,
    cu.NumeroCuenta
FROM Clientes c
FULL JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

---

## ¿Qué hace SQL?

La condición:

```sql
ON c.IdCliente = cu.IdCliente
```

busca coincidencias.

Después:

- Conserva las coincidencias.
- Conserva los registros exclusivos de Clientes.
- Conserva los registros exclusivos de Cuentas.

---

## Casos de uso reales

### Auditoría de clientes y cuentas

```sql
SELECT
    c.Nombre,
    cu.NumeroCuenta
FROM Clientes c
FULL JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

Caso:

```text
Detectar clientes sin cuentas y cuentas sin cliente.
```

---

### Auditoría de cuentas y transacciones

```sql
SELECT
    cu.NumeroCuenta,
    t.IdTransaccion
FROM Cuentas cu
FULL JOIN Transacciones t
    ON cu.IdCuenta = t.IdCuenta;
```

Caso:

```text
Detectar movimientos sin cuenta asociada.
```

---

### Calidad de datos

```sql
SELECT *
FROM Clientes c
FULL JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

Caso:

```text
Validar integridad referencial.
```

---

## Comparación de JOINs

### INNER JOIN

Devuelve:

```text
Solo coincidencias.
```

---

### LEFT JOIN

Devuelve:

```text
Coincidencias
+
Tabla izquierda completa.
```

---

### RIGHT JOIN

Devuelve:

```text
Coincidencias
+
Tabla derecha completa.
```

---

### FULL JOIN

Devuelve:

```text
Coincidencias
+
Tabla izquierda completa
+
Tabla derecha completa.
```

---

## Visualización conceptual

```text
Clientes
    ∩
Cuentas
```

INNER JOIN:

```text
Solo la intersección.
```

---

```text
Clientes
```

LEFT JOIN:

```text
Todo Clientes + intersección.
```

---

```text
Cuentas
```

RIGHT JOIN:

```text
Todo Cuentas + intersección.
```

---

```text
Clientes ∪ Cuentas
```

FULL JOIN:

```text
Todo.
```

---

## Error común

❌ Incorrecto

```sql
SELECT *
FROM Clientes
FULL JOIN Cuentas;
```

✔ Correcto

```sql
SELECT *
FROM Clientes c
FULL JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

---

## Error conceptual frecuente

Muchos principiantes creen que:

```sql
FULL JOIN
```

devuelve únicamente coincidencias.

Incorrecto.

Eso es exactamente lo que hace:

```sql
INNER JOIN
```

FULL JOIN devuelve:

- Coincidencias.
- Registros exclusivos de la izquierda.
- Registros exclusivos de la derecha.

---

## Compatibilidad importante

SQL Server soporta:

```sql
FULL JOIN
```

y

```sql
FULL OUTER JOIN
```

Ambos son equivalentes:

```sql
FULL JOIN
```

=

```sql
FULL OUTER JOIN
```

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar FULL JOIN pregúntate:

1. ¿Necesito visualizar ambas tablas completas?
2. ¿Estoy realizando una auditoría?
3. ¿Busco registros huérfanos?
4. ¿Necesito detectar problemas de integridad referencial?

### Relación entre conceptos

INNER JOIN responde:

> ¿Qué registros coinciden?

LEFT JOIN responde:

> ¿Qué registros existen en la izquierda?

RIGHT JOIN responde:

> ¿Qué registros existen en la derecha?

FULL JOIN responde:

> ¿Qué registros existen en cualquiera de las dos tablas?

---

## Resumen

FULL JOIN combina registros de dos tablas relacionadas.

Características principales:

- Conserva ambas tablas completas.
- Devuelve coincidencias.
- Devuelve registros exclusivos.
- Utiliza NULL cuando no existe coincidencia.
- Es muy utilizado para auditorías y calidad de datos.

Es especialmente útil para:

- Ingeniería de Datos.
- Gobierno de datos.
- Calidad de datos.
- Auditorías.
- Integridad referencial.
