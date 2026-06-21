# UNION y UNION ALL

## Definición

Las cláusulas `UNION` y `UNION ALL` permiten combinar los resultados de dos o más consultas SELECT en un único conjunto de resultados.

---

## Conceptos clave

UNION responde a la pregunta:

> ¿Cómo puedo combinar resultados provenientes de distintas consultas?

Características:

- Une múltiples consultas.
- Las consultas deben tener el mismo número de columnas.
- Las columnas deben ser compatibles en tipo de dato.
- Devuelve un único resultado.

---

# Diferencia entre UNION y UNION ALL

## UNION

Combina resultados y elimina duplicados.

```sql
SELECT Nombre
FROM Clientes

UNION

SELECT Nombre
FROM Prospectos;
```

---

## UNION ALL

Combina resultados y conserva duplicados.

```sql
SELECT Nombre
FROM Clientes

UNION ALL

SELECT Nombre
FROM Prospectos;
```

---

## Ejemplo práctico

### Tabla Clientes

| Nombre |
|----------|
| Ana |
| Pedro |
| Juan |

### Tabla Prospectos

| Nombre |
|----------|
| Juan |
| Luis |

---

## UNION

```sql
SELECT Nombre
FROM Clientes

UNION

SELECT Nombre
FROM Prospectos;
```

Resultado:

| Nombre |
|----------|
| Ana |
| Pedro |
| Juan |
| Luis |

Observa:

```text
Juan aparece una sola vez.
```

---

## UNION ALL

```sql
SELECT Nombre
FROM Clientes

UNION ALL

SELECT Nombre
FROM Prospectos;
```

Resultado:

| Nombre |
|----------|
| Ana |
| Pedro |
| Juan |
| Juan |
| Luis |

Observa:

```text
Juan aparece dos veces.
```

---

## Reglas importantes

### Número de columnas

❌ Incorrecto

```sql
SELECT Nombre
FROM Clientes

UNION

SELECT Nombre, Telefono
FROM Prospectos;
```

---

✔ Correcto

```sql
SELECT Nombre
FROM Clientes

UNION

SELECT Nombre
FROM Prospectos;
```

---

### Tipos compatibles

❌ Incorrecto

```sql
SELECT Nombre
FROM Clientes

UNION

SELECT FechaNacimiento
FROM Clientes;
```

---

✔ Correcto

```sql
SELECT Nombre
FROM Clientes

UNION

SELECT Nombre
FROM Prospectos;
```

---

## Caso bancario

### Problema

Combinar movimientos de depósitos y retiros.

### SQL

```sql
SELECT
    FechaTransaccion,
    Monto,
    'Deposito' AS Tipo
FROM Depositos

UNION ALL

SELECT
    FechaTransaccion,
    Monto,
    'Retiro' AS Tipo
FROM Retiros;
```

---

## Resultado esperado

| Fecha | Monto | Tipo |
|---------|---------|---------|
| 01/01 | 500 | Deposito |
| 02/01 | 200 | Retiro |
| 03/01 | 1000 | Deposito |

---

## UNION con ORDER BY

```sql
SELECT Nombre
FROM Clientes

UNION

SELECT Nombre
FROM Prospectos

ORDER BY Nombre;
```

---

## Casos de uso reales

### Consolidar clientes

```sql
SELECT Nombre
FROM ClientesActivos

UNION

SELECT Nombre
FROM ClientesHistoricos;
```

---

### Consolidar ventas

```sql
SELECT *
FROM Ventas2024

UNION ALL

SELECT *
FROM Ventas2025;
```

---

### ETL

```sql
SELECT *
FROM SistemaA

UNION ALL

SELECT *
FROM SistemaB;
```

---

### Data Warehouse

```sql
SELECT *
FROM FactVentas2024

UNION ALL

SELECT *
FROM FactVentas2025;
```

---

## Rendimiento

### UNION

```sql
UNION
```

SQL elimina duplicados.

Por lo tanto:

```text
Más costoso.
```

---

### UNION ALL

```sql
UNION ALL
```

No elimina duplicados.

Por lo tanto:

```text
Más rápido.
```

---

## ¿Cuál utilizar?

Si necesitas eliminar duplicados:

```sql
UNION
```

---

Si necesitas máximo rendimiento:

```sql
UNION ALL
```

---

## Error común

❌ Incorrecto

```sql
SELECT Nombre
FROM Clientes

UNION

SELECT Nombre,
       Telefono
FROM Prospectos;
```

---

✔ Correcto

```sql
SELECT Nombre
FROM Clientes

UNION

SELECT Nombre
FROM Prospectos;
```

---

## Error conceptual frecuente

Muchos principiantes creen que:

```sql
UNION
```

y

```sql
UNION ALL
```

son iguales.

Incorrecto.

UNION:

```text
Elimina duplicados.
```

UNION ALL:

```text
Conserva duplicados.
```

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar UNION pregúntate:

1. ¿Necesito combinar conjuntos de datos?
2. ¿Los esquemas son compatibles?
3. ¿Debo eliminar duplicados?
4. ¿Es más importante la precisión o el rendimiento?
5. ¿UNION ALL sería suficiente?

---

## Relación con otros conceptos

```text
JOIN          → Relacionar tablas horizontalmente
UNION         → Combinar resultados verticalmente
CTE           → Organizar consultas complejas
VIEW          → Reutilizar consultas
```

---

## Resumen

UNION y UNION ALL permiten combinar resultados de múltiples consultas.

Principales diferencias:

| Característica | UNION | UNION ALL |
|----------------|--------|------------|
| Combina resultados | Sí | Sí |
| Elimina duplicados | Sí | No |
| Más rápido | No | Sí |
| Más utilizado en ETL | No | Sí |

Son ampliamente utilizados en:

- ETL
- Data Engineering
- Data Warehousing
- Reporting
- Business Intelligence
- Integración de datos
