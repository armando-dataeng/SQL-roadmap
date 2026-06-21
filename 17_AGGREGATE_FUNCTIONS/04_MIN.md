# MIN()

## Definición

La función `MIN()` permite obtener el valor más pequeño de una columna.

Es una función agregada ampliamente utilizada para identificar mínimos en datos numéricos, fechas y otros tipos de datos comparables.

---

## Conceptos clave

MIN responde a la pregunta:

> ¿Cuál es el valor más pequeño?

Características:

* Devuelve un único resultado.
* Puede utilizarse con números.
* Puede utilizarse con fechas.
* Ignora valores NULL.
* No modifica datos.

---

## Sintaxis

```sql
SELECT MIN(columna)
FROM tabla;
```

Ejemplo:

```sql
SELECT MIN(Saldo)
FROM Cuentas;
```

---

## Problema

Determinar cuál es el saldo más bajo registrado en el banco.

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

Buscar el menor valor dentro de todos los saldos.

### SQL

```sql
SELECT MIN(Saldo)
FROM Cuentas;
```

---

## Resultado esperado

```text
100
```

Significa:

```text
Existe una cuenta con un saldo mínimo de 100.
```

---

## ¿Cómo funciona MIN?

Supongamos:

| Saldo |
| ----- |
| 5000  |
| 1000  |
| 8000  |
| 300   |

Consulta:

```sql
SELECT MIN(Saldo)
FROM Cuentas;
```

Resultado:

```text
300
```

SQL recorre todos los valores y devuelve el menor.

---

## Casos de uso reales

### Saldo mínimo del banco

```sql
SELECT MIN(Saldo)
FROM Cuentas;
```

Caso:

```text
Identificar la cuenta con menos fondos.
```

---

### Primera transacción registrada

```sql
SELECT MIN(FechaTransaccion)
FROM Transacciones;
```

Caso:

```text
Conocer la fecha más antigua registrada.
```

---

### Monto mínimo de una transacción

```sql
SELECT MIN(Monto)
FROM Transacciones;
```

Caso:

```text
Detectar la operación más pequeña realizada.
```

---

### Cliente más antiguo

```sql
SELECT MIN(FechaRegistro)
FROM Clientes;
```

Caso:

```text
Identificar cuándo comenzó la operación del negocio.
```

---

## MIN con WHERE

Es común combinar MIN con filtros.

```sql
SELECT MIN(Saldo)
FROM Cuentas
WHERE Activa = 1;
```

Proceso:

1. Filtra las cuentas activas.
2. Busca el saldo mínimo entre ellas.

---

## MIN con fechas

MIN funciona perfectamente con fechas.

```sql
SELECT MIN(FechaCreacion)
FROM Cuentas;
```

Resultado:

```text
2023-01-05
```

Significa:

```text
Esa fue la primera cuenta creada.
```

---

## MIN ignora NULL

Supongamos:

| Saldo |
| ----- |
| 1000  |
| 500   |
| NULL  |
| 2000  |

Consulta:

```sql
SELECT MIN(Saldo)
FROM Cuentas;
```

Resultado:

```text
500
```

El valor NULL no participa en la comparación.

---

## Error común

❌ Incorrecto

```sql
SELECT MIN(*)
FROM Cuentas;
```

✔ Correcto

```sql
SELECT MIN(Saldo)
FROM Cuentas;
```

MIN necesita una columna específica.

---

## Error conceptual frecuente

Muchos principiantes creen que:

```sql
MIN()
```

devuelve la primera fila.

Incorrecto.

MIN devuelve:

```text
El valor más pequeño.
```

No necesariamente corresponde a la primera fila almacenada.

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar MIN pregúntate:

1. ¿Qué valor mínimo necesito encontrar?
2. ¿Debo filtrar previamente los datos?
3. ¿La columna contiene valores NULL?
4. ¿Estoy trabajando con números o fechas?
5. ¿Qué decisión de negocio depende de este mínimo?

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
    MIN(Saldo) AS SaldoMinimo,
    MAX(Saldo) AS SaldoMaximo
FROM Cuentas;
```

Resultado:

```text
SaldoMinimo : 100
SaldoMaximo : 95000
```

Esto permite conocer el rango de saldos existente en el banco.

---

## Resumen

MIN() permite obtener el valor más pequeño de una columna.

Principales usos:

* Identificar mínimos financieros.
* Buscar fechas más antiguas.
* Detectar operaciones pequeñas.
* Analizar rangos de datos.
* Business Intelligence.
* Data Analytics.
* Data Engineering.
* Auditorías.

Es una función fundamental para el análisis exploratorio de datos y la generación de métricas.
