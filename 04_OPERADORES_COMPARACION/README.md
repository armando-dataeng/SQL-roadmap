# Operadores de Comparación

## Definición

Los operadores de comparación permiten comparar valores dentro de una condición SQL.

Son utilizados principalmente en la cláusula `WHERE` para determinar qué registros cumplen una condición específica.

El resultado de una comparación siempre será:

- Verdadero (TRUE)
- Falso (FALSE)

---

## Conceptos clave

Los operadores de comparación responden a la pregunta:

> ¿Cómo comparo un valor con otro?

Son la base de:

- WHERE
- HAVING
- JOIN
- CASE
- Subconsultas

Sin operadores de comparación no sería posible filtrar datos.

---

## Sintaxis

```sql
SELECT columnas
FROM tabla
WHERE columna operador valor;
```

Ejemplo:

```sql
SELECT *
FROM Clientes
WHERE Nombre = 'Juan';
```

---

## Operadores disponibles

| Operador | Significado |
|-----------|------------|
| = | Igual |
| <> | Distinto |
| > | Mayor que |
| < | Menor que |
| >= | Mayor o igual que |
| <= | Menor o igual que |

---

## Igual (=)

### Problema

Encontrar clientes llamados Juan.

### Datos

Tabla:

```text
Clientes
```

Columna:

```text
Nombre
```

### Lógica

Buscar registros cuyo nombre sea exactamente Juan.

### SQL

```sql
SELECT *
FROM Clientes
WHERE Nombre = 'Juan';
```

---

## Distinto (<>)

### Problema

Mostrar clientes que no sean Juan.

### SQL

```sql
SELECT *
FROM Clientes
WHERE Nombre <> 'Juan';
```

---

## Mayor que (>)

### Problema

Mostrar cuentas con saldo superior a 10,000.

### SQL

```sql
SELECT *
FROM Cuentas
WHERE Saldo > 10000;
```

---

## Menor que (<)

### Problema

Mostrar cuentas con saldo inferior a 10,000.

### SQL

```sql
SELECT *
FROM Cuentas
WHERE Saldo < 10000;
```

---

## Mayor o igual que (>=)

### Problema

Mostrar cuentas con saldo de 10,000 o más.

### SQL

```sql
SELECT *
FROM Cuentas
WHERE Saldo >= 10000;
```

---

## Menor o igual que (<=)

### Problema

Mostrar cuentas con saldo de 10,000 o menos.

### SQL

```sql
SELECT *
FROM Cuentas
WHERE Saldo <= 10000;
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

### Clientes inactivos

```sql
SELECT *
FROM Clientes
WHERE Activo <> 1;
```

Caso:

```text
Detectar clientes que requieren reactivación.
```

---

### Cuentas de alto valor

```sql
SELECT *
FROM Cuentas
WHERE Saldo > 50000;
```

Caso:

```text
Segmentar clientes premium.
```

---

### Transacciones pequeñas

```sql
SELECT *
FROM Transacciones
WHERE Monto < 1000;
```

Caso:

```text
Analizar operaciones de bajo importe.
```

---

## Error común

❌ Incorrecto

```sql
SELECT *
FROM Cuentas
WHERE Saldo => 10000;
```

✔ Correcto

```sql
SELECT *
FROM Cuentas
WHERE Saldo >= 10000;
```

---

## Error conceptual frecuente

Muchos principiantes confunden:

```sql
>=
```

con

```sql
=>
```

En SQL solamente existe:

```sql
>=
```

y

```sql
<=
```

El orden de los símbolos importa.

---

## Pensamiento de Ingeniería de Datos

Antes de escribir una condición pregúntate:

1. ¿Qué valor necesito comparar?
2. ¿La comparación debe ser exacta o parcial?
3. ¿Necesito un rango?
4. ¿Qué operador representa mejor la lógica del negocio?

### Relación entre conceptos

`SELECT` responde:

> ¿Qué información necesito obtener?

`FROM` responde:

> ¿De dónde obtendré esa información?

`WHERE` responde:

> ¿Qué registros cumplen la condición?

Los operadores de comparación responden:

> ¿Cómo se evaluará esa condición?

---

## Resumen

Los operadores de comparación permiten evaluar condiciones dentro de una consulta SQL.

Operadores principales:

- =
- <>
- >
- <
- >=
- <=

Son la base de:

- WHERE
- HAVING
- JOIN
- CASE
- Subconsultas

Todo filtrado en SQL comienza con una comparación.
