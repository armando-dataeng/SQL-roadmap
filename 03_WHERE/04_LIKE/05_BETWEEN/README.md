# BETWEEN

## Definición

El operador `BETWEEN` permite filtrar valores que se encuentran dentro de un rango determinado.

Es equivalente a utilizar:

```sql
>= valor_inicial
AND
<= valor_final
```

`BETWEEN` incluye ambos extremos del rango.

---

## Conceptos clave

`BETWEEN` responde a la pregunta:

> ¿Qué registros se encuentran dentro de este rango?

Puede utilizarse con:

- Números
- Fechas
- Horas
- Valores alfanuméricos

El rango siempre se evalúa:

```text
Valor mínimo → Valor máximo
```

---

## Sintaxis

```sql
SELECT columnas
FROM tabla
WHERE columna BETWEEN valor_inicial AND valor_final;
```

---

## Filtrar cuentas por saldo

### Problema

Mostrar cuentas con saldo entre 1,000 y 10,000.

### Datos

Tabla:

```text
Cuentas
```

Columna:

```text
Saldo
```

### Lógica

Recuperar únicamente las cuentas cuyo saldo se encuentre dentro del rango especificado.

### SQL

```sql
SELECT *
FROM Cuentas
WHERE Saldo BETWEEN 1000 AND 10000;
```

---

## Filtrar clientes por rango de fechas

### Problema

Mostrar clientes registrados durante el año 2024.

### Datos

Tabla:

```text
Clientes
```

Columna:

```text
FechaRegistro
```

### Lógica

Recuperar únicamente clientes registrados dentro del período indicado.

### SQL

```sql
SELECT *
FROM Clientes
WHERE FechaRegistro BETWEEN '2024-01-01' AND '2024-12-31';
```

---

## Casos de uso reales

### Clientes registrados durante un período

```sql
SELECT *
FROM Clientes
WHERE FechaRegistro BETWEEN '2025-01-01' AND '2025-06-30';
```

Caso:

```text
Analizar captación de clientes durante el primer semestre.
```

---

### Cuentas con saldo medio

```sql
SELECT *
FROM Cuentas
WHERE Saldo BETWEEN 5000 AND 50000;
```

Caso:

```text
Segmentar clientes según nivel de saldo.
```

---

### Transacciones dentro de un rango monetario

```sql
SELECT *
FROM Transacciones
WHERE Monto BETWEEN 1000 AND 10000;
```

Caso:

```text
Analizar movimientos financieros de monto medio.
```

---

### Transacciones por período

```sql
SELECT *
FROM Transacciones
WHERE FechaTransaccion
BETWEEN '2025-01-01'
AND '2025-01-31';
```

Caso:

```text
Generar reportes mensuales.
```

---

## BETWEEN con números

```sql
SELECT *
FROM Cuentas
WHERE Saldo BETWEEN 1000 AND 5000;
```

Equivale a:

```sql
SELECT *
FROM Cuentas
WHERE Saldo >= 1000
AND Saldo <= 5000;
```

---

## BETWEEN con fechas

```sql
SELECT *
FROM Clientes
WHERE FechaRegistro
BETWEEN '2025-01-01'
AND '2025-12-31';
```

Muy utilizado en reportes y análisis históricos.

---

## Error común

❌ Incorrecto

```sql
SELECT *
FROM Cuentas
WHERE Saldo BETWEEN 10000 AND 1000;
```

✔ Correcto

```sql
SELECT *
FROM Cuentas
WHERE Saldo BETWEEN 1000 AND 10000;
```

---

## ¿Por qué ocurre este error?

Muchos principiantes creen que SQL reorganiza automáticamente los límites.

No es así.

SQL interpreta:

```sql
BETWEEN valor_inicial AND valor_final
```

como:

```sql
>= valor_inicial
AND
<= valor_final
```

Por lo tanto:

```sql
BETWEEN 10000 AND 1000
```

equivale a:

```sql
Saldo >= 10000
AND
Saldo <= 1000
```

Lo cual es imposible.

---

## Error conceptual frecuente

Un error común es pensar que `BETWEEN` excluye los extremos.

Incorrecto.

`BETWEEN` incluye ambos valores.

Ejemplo:

```sql
SELECT *
FROM Cuentas
WHERE Saldo BETWEEN 1000 AND 5000;
```

Incluye:

```text
1000
2000
3000
4000
5000
```

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar `BETWEEN`, pregúntate:

1. ¿Estoy trabajando con un rango?
2. ¿Cuál es el valor mínimo?
3. ¿Cuál es el valor máximo?
4. ¿Necesito incluir ambos extremos?

### Relación entre cláusulas

`SELECT` responde:

> ¿Qué información necesito obtener?

`FROM` responde:

> ¿De dónde obtendré esa información?

`WHERE` responde:

> ¿Qué registros cumplen la condición?

`BETWEEN` responde:

> ¿Qué registros se encuentran dentro de un rango?

---

## Resumen

El operador `BETWEEN` permite filtrar registros dentro de un rango determinado.

Características principales:

- Incluye ambos extremos.
- Funciona con números.
- Funciona con fechas.
- Funciona con valores alfanuméricos.
- Equivale a utilizar `>=` y `<=`.

Es ampliamente utilizado para:

- Reportes financieros.
- Segmentación de clientes.
- Consultas históricas.
- Análisis temporales.
- Rangos monetarios.
