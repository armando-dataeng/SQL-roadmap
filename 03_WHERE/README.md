# WHERE

## Definición

La cláusula `WHERE` permite filtrar filas según una o varias condiciones lógicas.

Su propósito es limitar el conjunto de resultados a aquellos registros que cumplen los criterios especificados.

---

## Conceptos clave

`WHERE` responde a la pregunta:

> ¿Qué registros necesito obtener?

La cláusula `WHERE` controla las filas que serán devueltas por una consulta.

No controla:

- Qué información será devuelta → `SELECT`
- De dónde provienen los datos → `FROM`
- Cómo serán ordenados los resultados → `ORDER BY`

---

## Sintaxis

```sql
SELECT columna
FROM tabla
WHERE condicion;
```

---

## Filtrar clientes activos

### Problema

Mostrar únicamente los clientes activos.

### Datos

Tabla:

```text
Clientes
```

Columnas:

```text
Nombre
Activo
```

### Lógica

Solo deben mostrarse los registros cuyo estado sea activo.

### SQL

```sql
SELECT *
FROM Clientes
WHERE Activo = 1;
```

---

## Filtrar cuentas con saldo superior a un valor

### Problema

Mostrar las cuentas con saldo mayor a 10,000.

### Datos

Tabla:

```text
Cuentas
```

Columnas:

```text
NumeroCuenta
Saldo
```

### Lógica

Solo deben mostrarse las cuentas cuyo saldo sea superior a 10,000.

### SQL

```sql
SELECT *
FROM Cuentas
WHERE Saldo > 10000;
```

---

## Filtrar clientes por nombre

### Problema

Buscar clientes llamados Juan.

### Datos

Tabla:

```text
Clientes
```

Columnas:

```text
Nombre
```

### Lógica

Mostrar únicamente los registros cuyo nombre sea Juan.

### SQL

```sql
SELECT *
FROM Clientes
WHERE Nombre = 'Juan';
```

---

## Casos de uso reales

### Clientes activos

```sql
SELECT *
FROM Clientes
WHERE Activo = 1;
```

Caso:

```text
Identificar clientes habilitados para operar.
```

---

### Cuentas con saldo elevado

```sql
SELECT *
FROM Cuentas
WHERE Saldo > 50000;
```

Caso:

```text
Identificar clientes de alto valor.
```

---

### Transacciones sospechosas

```sql
SELECT *
FROM Transacciones
WHERE Monto > 100000;
```

Caso:

```text
Detectar movimientos financieros que requieren revisión.
```

---

### Usuarios administradores

```sql
SELECT *
FROM Usuarios
WHERE Rol = 'Administrador';
```

Caso:

```text
Identificar usuarios con privilegios elevados.
```

---

## Operadores comunes

### Igual

```sql
WHERE Nombre = 'Juan'
```

---

### Distinto

```sql
WHERE Nombre <> 'Juan'
```

---

### Mayor que

```sql
WHERE Saldo > 1000
```

---

### Menor que

```sql
WHERE Saldo < 1000
```

---

### Mayor o igual que

```sql
WHERE Saldo >= 1000
```

---

### Menor o igual que

```sql
WHERE Saldo <= 1000
```

---

## Error común

❌ Incorrecto

```sql
SELECT *
FROM Clientes
WHERE Nombre = Juan;
```

✔ Correcto

```sql
SELECT *
FROM Clientes
WHERE Nombre = 'Juan';
```

---

## Error conceptual frecuente

Un error común es pensar que `WHERE` selecciona columnas.

Incorrecto.

`WHERE` selecciona filas.

Ejemplo:

```sql
SELECT Nombre
FROM Clientes
WHERE Activo = 1;
```

Aquí:

- `SELECT Nombre` define la columna.
- `FROM Clientes` define la tabla.
- `WHERE Activo = 1` define las filas.

---

## Pensamiento de Ingeniería de Datos

Antes de escribir una condición, pregúntate:

1. ¿Qué registros necesito encontrar?
2. ¿Qué columna contiene la información necesaria?
3. ¿Qué operador representa la lógica del problema?
4. ¿Cómo traduzco esa lógica a SQL?

### Relación entre cláusulas

`SELECT` responde:

> ¿Qué información necesito obtener?

`FROM` responde:

> ¿De dónde obtendré esa información?

`WHERE` responde:

> ¿Qué registros cumplen la condición?

---

## Resumen

La cláusula `WHERE` permite filtrar registros mediante condiciones lógicas.

Puede utilizar:

- Operadores de comparación
- Operadores lógicos
- Funciones
- Expresiones

`WHERE` controla las filas del resultado.

No controla:

- Las columnas (`SELECT`)
- El origen de los datos (`FROM`)
- El ordenamiento (`ORDER BY`)

Una consulta sin `WHERE` devuelve todos los registros disponibles.

Una consulta con `WHERE` devuelve únicamente los registros que cumplen la condición especificada.
