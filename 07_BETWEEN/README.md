# BETWEEN

## Definición

El operador `BETWEEN` permite filtrar registros cuyos valores se encuentran dentro de un rango determinado.

Es una forma simplificada de expresar:

```sql
>= valor_inicial
AND
<= valor_final
```

Una característica importante es que `BETWEEN` incluye ambos extremos del rango.

---

## Conceptos clave

BETWEEN responde a la pregunta:

> ¿Qué registros se encuentran dentro de este rango?

Puede utilizarse con:

- Números
- Fechas
- Horas
- Valores alfanuméricos

BETWEEN trabaja junto con:

- WHERE
- Operadores de comparación
- Operadores lógicos

---

## Sintaxis

```sql
SELECT columnas
FROM tabla
WHERE columna BETWEEN valor_inicial AND valor_final;
```

Ejemplo:

```sql
SELECT *
FROM Cuentas
WHERE Saldo BETWEEN 1000 AND 10000;
```

---

## Filtrar cuentas por saldo

### Problema

Mostrar las cuentas cuyo saldo se encuentra entre 1,000 y 10,000.

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

Mostrar únicamente las cuentas cuyo saldo esté dentro del rango especificado.

### SQL

```sql
SELECT *
FROM Cuentas
WHERE Saldo BETWEEN 1000 AND 10000;
```

---

## Filtrar clientes por fecha de registro

### Problema

Mostrar los clientes registrados durante el año 2025.

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

Buscar registros cuya fecha esté dentro del período especificado.

### SQL

```sql
SELECT *
FROM Clientes
WHERE FechaRegistro
BETWEEN '2025-01-01'
AND '2025-12-31';
```

---

## Casos de uso reales

### Clientes registrados durante un período

```sql
SELECT *
FROM Clientes
WHERE FechaRegistro
BETWEEN '2025-01-01'
AND '2025-06-30';
```

Caso:

```text
Analizar la captación de clientes durante el primer semestre.
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
Analizar operaciones financieras de importe medio.
```

---

### Transacciones de un mes específico

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

Muy utilizado para reportes y análisis históricos.

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
Saldo >= valor_inicial
AND
Saldo <= valor_final
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

Lo cual genera cero resultados.

---

## Error conceptual frecuente

Muchos principiantes creen que BETWEEN excluye los extremos.

Incorrecto.

BETWEEN incluye ambos extremos.

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

Antes de utilizar BETWEEN pregúntate:

1. ¿Estoy trabajando con un rango?
2. ¿Cuál es el valor mínimo?
3. ¿Cuál es el valor máximo?
4. ¿Necesito incluir ambos extremos?

### Relación entre conceptos

SELECT responde:

> ¿Qué información necesito obtener?

FROM responde:

> ¿De dónde obtendré esa información?

WHERE responde:

> ¿Qué registros necesito?

Operadores de comparación responden:

> ¿Cómo comparo valores?

Operadores lógicos responden:

> ¿Cómo combino condiciones?

BETWEEN responde:

> ¿Qué registros se encuentran dentro de un rango?

---

## Resumen

BETWEEN permite filtrar registros dentro de un rango determinado.

Características principales:

- Incluye ambos extremos.
- Funciona con números.
- Funciona con fechas.
- Equivale a utilizar `>=` y `<=`.

Es ampliamente utilizado para:

- Reportes financieros.
- Segmentación de clientes.
- Análisis temporales.
- Consultas históricas.
- Rangos monetarios.
