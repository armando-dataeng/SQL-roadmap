# CASE

## Definición

La expresión `CASE` permite implementar lógica condicional dentro de una consulta SQL.

Es equivalente a:

```text
IF
ELSE IF
ELSE
```

en lenguajes de programación.

Permite clasificar, transformar y categorizar datos directamente desde SQL.

---

## Conceptos clave

CASE responde a la pregunta:

> ¿Qué valor debo devolver dependiendo de una condición?

Características:

- Evalúa condiciones.
- Devuelve valores diferentes según el resultado.
- Puede utilizarse en SELECT.
- Puede utilizarse en ORDER BY.
- Puede utilizarse en GROUP BY.
- Puede utilizarse en UPDATE.

---

## Sintaxis

```sql
CASE
    WHEN condicion THEN resultado
    WHEN condicion THEN resultado
    ELSE resultado
END
```

---

## Ejemplo básico

### Problema

Clasificar clientes según su saldo.

### Datos

Tabla:

```text
Clientes
```

Columna:

```text
Saldo
```

### SQL

```sql
SELECT
    Nombre,
    Saldo,
    CASE
        WHEN Saldo >= 10000 THEN 'VIP'
        ELSE 'Regular'
    END AS Categoria
FROM Clientes;
```

---

## Resultado

| Nombre | Saldo | Categoria |
|----------|---------|-----------|
| Ana | 15000 | VIP |
| Pedro | 5000 | Regular |

---

## Múltiples condiciones

### Problema

Clasificar clientes en tres niveles.

### SQL

```sql
SELECT
    Nombre,
    Saldo,
    CASE
        WHEN Saldo >= 50000 THEN 'Premium'
        WHEN Saldo >= 10000 THEN 'VIP'
        ELSE 'Regular'
    END AS Categoria
FROM Clientes;
```

---

## ¿Cómo evalúa SQL?

SQL analiza de arriba hacia abajo.

Ejemplo:

```sql
CASE
    WHEN Saldo >= 50000 THEN 'Premium'
    WHEN Saldo >= 10000 THEN 'VIP'
    ELSE 'Regular'
END
```

Si la primera condición es verdadera:

```text
Detiene la evaluación.
```

---

## Caso bancario

### Problema

Determinar el tipo de cuenta.

### SQL

```sql
SELECT
    NumeroCuenta,
    Saldo,
    CASE
        WHEN Saldo < 1000 THEN 'Bajo'
        WHEN Saldo BETWEEN 1000 AND 10000 THEN 'Medio'
        ELSE 'Alto'
    END AS NivelSaldo
FROM Cuentas;
```

---

## CASE con funciones agregadas

### Problema

Contar clientes VIP.

### SQL

```sql
SELECT
    COUNT(
        CASE
            WHEN Saldo >= 10000
                THEN 1
        END
    ) AS ClientesVIP
FROM Cuentas;
```

---

## CASE con SUM

### Problema

Calcular depósitos y retiros.

### SQL

```sql
SELECT
    SUM(
        CASE
            WHEN TipoTransaccion = 'Deposito'
                THEN Monto
            ELSE 0
        END
    ) AS TotalDepositos
FROM Transacciones;
```

---

## CASE en ORDER BY

### Problema

Mostrar primero los clientes VIP.

### SQL

```sql
SELECT
    Nombre,
    Saldo
FROM Clientes
ORDER BY
CASE
    WHEN Saldo >= 10000 THEN 1
    ELSE 2
END;
```

---

## CASE en UPDATE

### Problema

Actualizar categoría de clientes.

### SQL

```sql
UPDATE Clientes
SET Categoria =
CASE
    WHEN Saldo >= 10000 THEN 'VIP'
    ELSE 'Regular'
END;
```

---

## Casos de uso reales

### Clasificación de clientes

```sql
SELECT
    Nombre,
    CASE
        WHEN Saldo >= 10000
            THEN 'VIP'
        ELSE 'Regular'
    END
FROM Clientes;
```

---

### Clasificación de transacciones

```sql
SELECT
    Monto,
    CASE
        WHEN Monto > 5000
            THEN 'Alto Valor'
        ELSE 'Normal'
    END
FROM Transacciones;
```

---

### Riesgo financiero

```sql
SELECT
    ClienteID,
    CASE
        WHEN Saldo < 0
            THEN 'Riesgo'
        ELSE 'Normal'
    END
FROM Cuentas;
```

---

## Error común

❌ Incorrecto

```sql
SELECT
    Nombre,
    CASE
        Saldo > 10000
        THEN 'VIP'
    END
FROM Clientes;
```

✔ Correcto

```sql
SELECT
    Nombre,
    CASE
        WHEN Saldo > 10000
            THEN 'VIP'
    END
FROM Clientes;
```

---

## Error conceptual frecuente

Muchos principiantes creen que:

```sql
CASE
```

filtra registros.

Incorrecto.

CASE transforma valores.

Para filtrar registros se utiliza:

```sql
WHERE
```

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar CASE pregúntate:

1. ¿Necesito clasificar datos?
2. ¿Necesito transformar valores?
3. ¿Necesito crear categorías?
4. ¿Estoy construyendo métricas para BI?
5. ¿La lógica debe estar en SQL o en la aplicación?

---

## Relación con otros conceptos

```text
WHERE        → Filtrar registros
GROUP BY     → Agrupar registros
HAVING       → Filtrar grupos
CASE         → Aplicar lógica condicional
```

---

## Resumen

CASE permite implementar lógica condicional dentro de SQL.

Principales usos:

- Clasificación de clientes.
- Segmentación financiera.
- Dashboards.
- KPIs.
- Business Intelligence.
- Data Analytics.
- Data Engineering.

Es una de las herramientas más utilizadas para transformar datos dentro de una consulta SQL.
