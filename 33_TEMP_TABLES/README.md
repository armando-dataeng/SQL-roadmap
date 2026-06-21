# TEMP TABLES

## Definición

Una Temporary Table (Tabla Temporal) es una tabla creada temporalmente dentro de SQL Server para almacenar datos durante una sesión o proceso específico.

Su propósito es almacenar resultados intermedios que posteriormente serán utilizados por otras consultas.

Al finalizar la sesión o proceso:

```text
La tabla desaparece automáticamente.
```

---

## Conceptos clave

Una tabla temporal responde a la pregunta:

> ¿Dónde puedo almacenar resultados temporales mientras ejecuto un proceso complejo?

Características:

- Almacena datos temporalmente.
- Puede tener índices.
- Puede utilizarse en JOINs.
- Puede utilizarse en Stored Procedures.
- Se elimina automáticamente.

---

# Tipos de tablas temporales

## Local Temporary Table

Visible únicamente para la sesión actual.

Prefijo:

```sql
#
```

Ejemplo:

```sql
#ClientesVIP
```

---

## Global Temporary Table

Visible para todas las sesiones.

Prefijo:

```sql
##
```

Ejemplo:

```sql
##ClientesVIP
```

---

# Crear una tabla temporal

## Sintaxis

```sql
CREATE TABLE #NombreTabla
(
    Columna TipoDato
);
```

---

## Ejemplo

```sql
CREATE TABLE #ClientesVIP
(
    IdCliente INT,
    Nombre VARCHAR(100),
    Saldo DECIMAL(10,2)
);
```

---

# Insertar datos

```sql
INSERT INTO #ClientesVIP
SELECT
    IdCliente,
    Nombre,
    Saldo
FROM Clientes
WHERE Saldo > 10000;
```

---

# Consultar datos

```sql
SELECT *
FROM #ClientesVIP;
```

---

# Caso bancario

## Problema

Identificar clientes VIP.

### SQL

```sql
CREATE TABLE #ClientesVIP
(
    IdCliente INT,
    Nombre VARCHAR(100),
    Saldo DECIMAL(10,2)
);

INSERT INTO #ClientesVIP
SELECT
    IdCliente,
    Nombre,
    Saldo
FROM Clientes
WHERE Saldo >= 10000;

SELECT *
FROM #ClientesVIP;
```

---

# SELECT INTO

Otra forma común.

## SQL

```sql
SELECT
    IdCliente,
    Nombre,
    Saldo
INTO #ClientesVIP
FROM Clientes
WHERE Saldo >= 10000;
```

---

## ¿Qué hace?

1. Crea la tabla.
2. Inserta los datos.

Todo en una sola instrucción.

---

# Uso con JOIN

## SQL

```sql
SELECT
    c.Nombre,
    cu.NumeroCuenta
INTO #ClientesCuentas
FROM Clientes c
INNER JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

---

## Consulta posterior

```sql
SELECT *
FROM #ClientesCuentas;
```

---

# Uso dentro de Stored Procedures

## SQL

```sql
CREATE PROCEDURE sp_ClientesVIP
AS
BEGIN

    SELECT
        IdCliente,
        Nombre,
        Saldo
    INTO #ClientesVIP
    FROM Clientes
    WHERE Saldo >= 10000;

    SELECT *
    FROM #ClientesVIP;

END;
```

---

# Crear índices en tablas temporales

## SQL

```sql
CREATE TABLE #Clientes
(
    IdCliente INT,
    Nombre VARCHAR(100)
);

CREATE INDEX IX_TempCliente
ON #Clientes(IdCliente);
```

---

## Beneficio

Consultas más rápidas sobre grandes volúmenes de datos.

---

# Tabla temporal global

## SQL

```sql
CREATE TABLE ##ClientesGlobal
(
    IdCliente INT,
    Nombre VARCHAR(100)
);
```

---

## Diferencia

```text
#Tabla     → Sesión actual

##Tabla    → Todas las sesiones
```

---

# Eliminar tabla temporal

Aunque SQL la elimina automáticamente, es buena práctica hacerlo manualmente.

```sql
DROP TABLE #ClientesVIP;
```

---

# Casos de uso reales

## ETL

Guardar resultados intermedios.

```sql
#DatosLimpios
```

---

## Reporting

Preparar información para reportes.

```sql
#VentasMensuales
```

---

## Data Engineering

Transformaciones por etapas.

```sql
#ClientesTransformados
```

---

## Stored Procedures

Dividir procesos complejos.

```sql
#ResultadosParciales
```

---

# Temp Tables vs CTE

## CTE

```sql
WITH ClientesVIP AS
(
    SELECT *
    FROM Clientes
)
SELECT *
FROM ClientesVIP;
```

Existe únicamente durante una consulta.

---

## Temp Table

```sql
CREATE TABLE #ClientesVIP
```

Puede reutilizarse varias veces durante la sesión.

---

# Temp Tables vs Views

## View

```sql
CREATE VIEW vw_ClientesVIP
```

Persistente.

---

## Temp Table

```sql
CREATE TABLE #ClientesVIP
```

Temporal.

---

# Error común

❌ Incorrecto

```sql
SELECT *
FROM ClientesVIP;
```

Si la tabla temporal fue creada como:

```sql
#ClientesVIP
```

---

✔ Correcto

```sql
SELECT *
FROM #ClientesVIP;
```

---

# Error conceptual frecuente

Muchos principiantes creen que:

```text
CTE y Temp Table son iguales.
```

Incorrecto.

CTE:

```text
Existe durante una consulta.
```

Temp Table:

```text
Existe durante la sesión.
```

---

# Rendimiento

Para conjuntos pequeños:

```text
CTE suele ser suficiente.
```

---

Para procesos complejos:

```text
Temp Tables suelen ser mejores.
```

---

# Pensamiento de Data Engineering

Antes de crear una Temp Table pregúntate:

1. ¿Necesito reutilizar resultados?
2. ¿La consulta es muy compleja?
3. ¿Necesito índices temporales?
4. ¿Debo dividir el proceso en etapas?
5. ¿Un CTE sería suficiente?

---

# Relación con otros conceptos

```text
CTE               → Resultado temporal lógico
VIEW              → Consulta persistente
TEMP TABLE        → Tabla temporal física
STORED PROCEDURE  → Puede utilizar Temp Tables
```

---

# Resumen

Las Temp Tables permiten almacenar resultados temporales durante una sesión.

Tipos:

```sql
#TablaLocal
##TablaGlobal
```

Son ampliamente utilizadas en:

- SQL Server
- ETL
- Data Engineering
- Reporting
- Stored Procedures
- Procesos complejos

Son una herramienta fundamental para trabajar con grandes volúmenes de datos y transformaciones por etapas.
