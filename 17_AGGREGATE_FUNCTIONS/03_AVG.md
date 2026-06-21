# AVG()

## Definición

La función `AVG()` permite calcular el promedio de los valores de una columna numérica.

Es ampliamente utilizada en análisis de datos, métricas financieras, Business Intelligence y Data Engineering.

---

## Conceptos clave

AVG responde a la pregunta:

> ¿Cuál es el valor promedio?

Características:

* Opera sobre columnas numéricas.
* Devuelve un único resultado.
* Ignora valores NULL.
* No modifica datos.

---

## Sintaxis

```sql
SELECT AVG(columna)
FROM tabla;
```

Ejemplo:

```sql
SELECT AVG(Saldo)
FROM Cuentas;
```

---

## Problema

Determinar el saldo promedio de las cuentas bancarias.

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

Sumar todos los saldos y dividirlos entre la cantidad de registros válidos.

### SQL

```sql
SELECT AVG(Saldo)
FROM Cuentas;
```

---

## Resultado esperado

```text
8500
```

Significa:

```text
El saldo promedio de las cuentas es 8500.
```

---

## ¿Cómo funciona AVG?

Supongamos los siguientes saldos:

| Saldo |
| ----- |
| 1000  |
| 3000  |
| 5000  |

Consulta:

```sql
SELECT AVG(Saldo)
FROM Cuentas;
```

SQL realiza:

```text
(1000 + 3000 + 5000) / 3
```

Resultado:

```text
3000
```

---

## Casos de uso reales

### Saldo promedio de cuentas

```sql
SELECT AVG(Saldo)
FROM Cuentas;
```

Caso:

```text
Conocer el comportamiento financiero promedio de los clientes.
```

---

### Monto promedio por transacción

```sql
SELECT AVG(Monto)
FROM Transacciones;
```

Caso:

```text
Analizar el tamaño promedio de las operaciones.
```

---

### Promedio de depósitos

```sql
SELECT AVG(Monto)
FROM Transacciones
WHERE TipoTransaccion = 'Deposito';
```

Caso:

```text
Determinar cuánto depositan en promedio los clientes.
```

---

### Promedio de retiros

```sql
SELECT AVG(Monto)
FROM Transacciones
WHERE TipoTransaccion = 'Retiro';
```

Caso:

```text
Analizar hábitos de retiro.
```

---

## AVG con WHERE

Es común combinar AVG con filtros.

```sql
SELECT AVG(Saldo)
FROM Cuentas
WHERE Activa = 1;
```

Proceso:

1. Filtra cuentas activas.
2. Calcula el promedio únicamente de esas cuentas.

---

## AVG ignora NULL

Supongamos:

| Saldo |
| ----- |
| 1000  |
| 2000  |
| NULL  |
| 3000  |

Consulta:

```sql
SELECT AVG(Saldo)
FROM Cuentas;
```

Resultado:

```text
2000
```

SQL ignora el valor NULL.

---

## Error común

❌ Incorrecto

```sql
SELECT AVG(Nombre)
FROM Clientes;
```

✔ Correcto

```sql
SELECT AVG(Saldo)
FROM Cuentas;
```

AVG solo debe utilizarse sobre columnas numéricas.

---

## Error conceptual frecuente

Muchos principiantes creen que:

```sql
AVG()
```

devuelve el valor más frecuente.

Incorrecto.

AVG devuelve:

```text
La media aritmética.
```

Es decir:

```text
Suma de valores
÷
Cantidad de registros
```

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar AVG pregúntate:

1. ¿La columna es numérica?
2. ¿Debo excluir ciertos registros?
3. ¿Existen valores NULL?
4. ¿Necesito el promedio general o segmentado?
5. ¿Qué decisión de negocio soportará esta métrica?

---

## Relación con otras funciones agregadas

```text
COUNT() → Cantidad de registros
SUM()   → Total acumulado
AVG()   → Promedio
MIN()   → Valor mínimo
MAX()   → Valor máximo
```

---

## Caso bancario completo

```sql
SELECT
    COUNT(*) AS TotalCuentas,
    SUM(Saldo) AS SaldoTotal,
    AVG(Saldo) AS SaldoPromedio
FROM Cuentas;
```

Resultado:

```text
TotalCuentas : 150
SaldoTotal   : 1,250,000
SaldoPromedio: 8,333.33
```

---

## Resumen

AVG() permite calcular el promedio de una columna numérica.

Principales usos:

* Análisis financiero
* Business Intelligence
* KPIs
* Dashboards
* Data Analytics
* Data Engineering
* Reportes ejecutivos

Es una de las funciones más utilizadas para comprender tendencias y comportamientos de los datos.
