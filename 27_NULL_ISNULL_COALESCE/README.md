# NULL, IS NULL, ISNULL y COALESCE

## Definición

NULL representa la ausencia de un valor.

No significa:

- 0
- Cadena vacía ('')
- FALSE

Significa:

```text
Valor desconocido o inexistente.
```

---

## Conceptos clave

Muchos errores ocurren porque los desarrolladores creen que:

```sql
NULL = NULL
```

es verdadero.

Incorrecto.

En SQL:

```sql
NULL = NULL
```

Resultado:

```text
UNKNOWN
```

---

# ¿Qué es NULL?

Supongamos:

| IdCliente | Telefono |
|------------|----------|
| 1 | 555-1234 |
| 2 | NULL |
| 3 | 555-9876 |

El cliente 2:

```text
No tiene teléfono registrado.
```

---

## Error clásico

❌ Incorrecto

```sql
SELECT *
FROM Clientes
WHERE Telefono = NULL;
```

Resultado:

```text
No devuelve filas.
```

---

✔ Correcto

```sql
SELECT *
FROM Clientes
WHERE Telefono IS NULL;
```

---

# IS NULL

## Definición

Permite identificar valores NULL.

---

## Sintaxis

```sql
SELECT *
FROM Clientes
WHERE Telefono IS NULL;
```

---

## Problema

Mostrar clientes sin teléfono.

### SQL

```sql
SELECT *
FROM Clientes
WHERE Telefono IS NULL;
```

---

## Resultado

| IdCliente | Telefono |
|------------|----------|
| 2 | NULL |

---

# IS NOT NULL

## Definición

Permite encontrar registros con valores existentes.

---

## SQL

```sql
SELECT *
FROM Clientes
WHERE Telefono IS NOT NULL;
```

---

## Resultado

| IdCliente | Telefono |
|------------|----------|
| 1 | 555-1234 |
| 3 | 555-9876 |

---

# ISNULL()

## Definición

Función específica de SQL Server.

Permite reemplazar NULL por otro valor.

---

## Sintaxis

```sql
ISNULL(columna, valor_reemplazo)
```

---

## Ejemplo

```sql
SELECT
    Nombre,
    ISNULL(Telefono,'No registrado') AS Telefono
FROM Clientes;
```

---

## Resultado

| Nombre | Telefono |
|----------|-----------|
| Ana | 555-1234 |
| Pedro | No registrado |

---

## Caso bancario

Mostrar saldo.

```sql
SELECT
    NumeroCuenta,
    ISNULL(Saldo,0) AS Saldo
FROM Cuentas;
```

---

# COALESCE()

## Definición

Devuelve el primer valor que NO sea NULL.

Es estándar ANSI SQL.

Funciona en:

- SQL Server
- PostgreSQL
- MySQL
- Oracle

---

## Sintaxis

```sql
COALESCE(valor1, valor2, valor3...)
```

---

## Ejemplo

```sql
SELECT
    COALESCE(TelefonoMovil,
             TelefonoCasa,
             TelefonoTrabajo,
             'Sin teléfono')
FROM Clientes;
```

---

## ¿Qué hace?

Busca:

1. TelefonoMovil
2. Si es NULL → TelefonoCasa
3. Si es NULL → TelefonoTrabajo
4. Si todos son NULL → 'Sin teléfono'

---

## Resultado

| Telefono |
|------------|
| 555-1111 |
| 555-2222 |
| Sin teléfono |

---

# ISNULL vs COALESCE

## ISNULL

SQL Server.

```sql
ISNULL(Telefono,'N/A')
```

---

## COALESCE

ANSI SQL.

```sql
COALESCE(Telefono,'N/A')
```

---

## ¿Cuál usar?

En proyectos profesionales:

```text
COALESCE
```

Porque es portable entre motores.

---

# NULL en funciones agregadas

Supongamos:

| Saldo |
|--------|
| 1000 |
| 2000 |
| NULL |
| 3000 |

---

## SUM()

```sql
SELECT SUM(Saldo)
FROM Cuentas;
```

Resultado:

```text
6000
```

---

## AVG()

```sql
SELECT AVG(Saldo)
FROM Cuentas;
```

Resultado:

```text
2000
```

---

## COUNT(columna)

```sql
SELECT COUNT(Saldo)
FROM Cuentas;
```

Resultado:

```text
3
```

---

## COUNT(*)

```sql
SELECT COUNT(*)
FROM Cuentas;
```

Resultado:

```text
4
```

---

# NOT IN y NULL

Este es uno de los temas favoritos en entrevistas.

Supongamos:

```sql
SELECT IdCliente
FROM Cuentas;
```

Resultado:

```text
1
2
NULL
```

---

Consulta:

```sql
SELECT *
FROM Clientes
WHERE IdCliente NOT IN
(
    SELECT IdCliente
    FROM Cuentas
);
```

Puede producir resultados inesperados.

---

## Solución profesional

Utilizar:

```sql
NOT EXISTS
```

Ejemplo:

```sql
SELECT *
FROM Clientes c
WHERE NOT EXISTS
(
    SELECT 1
    FROM Cuentas cu
    WHERE cu.IdCliente = c.IdCliente
);
```

---

# Casos de uso reales

## Data Engineering

Reemplazo de valores faltantes.

```sql
SELECT
    COALESCE(Ciudad,'Desconocida')
FROM Clientes;
```

---

## Business Intelligence

Evitar valores vacíos en dashboards.

```sql
SELECT
    COALESCE(Ventas,0)
FROM ReporteVentas;
```

---

## Auditoría

Encontrar registros incompletos.

```sql
SELECT *
FROM Clientes
WHERE Email IS NULL;
```

---

# Error común

❌ Incorrecto

```sql
WHERE Email = NULL
```

✔ Correcto

```sql
WHERE Email IS NULL
```

---

# Error conceptual frecuente

Muchos principiantes creen que:

```sql
NULL = NULL
```

es verdadero.

Incorrecto.

Resultado:

```text
UNKNOWN
```

---

# Pensamiento de Ingeniería de Datos

Antes de trabajar con datos pregúntate:

1. ¿Existen valores NULL?
2. ¿Debo reemplazarlos?
3. ¿Debo excluirlos?
4. ¿Afectan mis métricas?
5. ¿COALESCE sería útil?

---

# Relación con otros conceptos

```text
WHERE        → Filtrar datos
CASE         → Clasificar datos
IN           → Verificar pertenencia
EXISTS       → Verificar existencia
NULL         → Ausencia de valor
COALESCE     → Reemplazar NULL
IS NULL      → Detectar NULL
```

---

# Resumen

NULL representa ausencia de valor.

Herramientas fundamentales:

```sql
IS NULL
IS NOT NULL
ISNULL()
COALESCE()
```

Son esenciales para:

- SQL Server
- PostgreSQL
- MySQL
- Oracle
- Data Engineering
- BI
- Data Quality
- ETL
- Auditoría
