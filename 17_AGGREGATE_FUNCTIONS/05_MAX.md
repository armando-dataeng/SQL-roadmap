# MAX()

## Definición

La función `MAX()` permite obtener el valor más grande de una columna.

Es una función agregada utilizada para identificar máximos en datos numéricos, fechas y otros tipos de datos comparables.

---

## Conceptos clave

MAX responde a la pregunta:

> ¿Cuál es el valor más grande?

Características:

* Devuelve un único resultado.
* Puede utilizarse con números.
* Puede utilizarse con fechas.
* Ignora valores NULL.
* No modifica datos.

---

## Sintaxis

```sql
SELECT MAX(columna)
FROM tabla;
```

Ejemplo:

```sql
SELECT MAX(Saldo)
FROM Cuentas;
```

---

## Problema

Determinar cuál es el saldo más alto registrado en el banco.

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

Buscar el mayor valor dentro de todos los saldos.

### SQL

```sql
SELECT MAX(Saldo)
FROM Cuentas;
```

---

## Resultado esperado

```text
95000
```

Significa:

```text
Existe una cuenta con un saldo máximo de 95,000.
```

---

## ¿Cómo funciona MAX?

Supongamos:

| Saldo |
| ----- |
| 5000  |
| 1000  |
| 8000  |
| 300   |

Consulta:

```sql
SELECT MAX(Saldo)
FROM Cuentas;
```

Resultado:

```text
8000
```

SQL recorre todos los valores y devuelve el mayor.

---

## Casos de uso reales

### Saldo máximo del banco

```sql
SELECT MAX(Saldo)
FROM Cuentas;
```

Caso:

```text
Identificar la cuenta con más fondos.
```

---

### Última transacción registrada

```sql
SELECT MAX(FechaTransaccion)
FROM Transacciones;
```

Caso:

```text
Conocer la transacción más reciente.
```

---

### Mayor monto transaccionado

```sql
SELECT MAX(Monto)
FROM Transacciones;
```

Caso:

```text
Detectar operaciones de alto valor.
```

---

### Cliente más reciente

```sql
SELECT MAX(FechaRegistro)
FROM Clientes;
```

Caso:

```text
Identificar el cliente registrado más recientemente.
```

---

## MAX con WHERE

Es común combinar MAX con filtros.

```sql
SELECT MAX(Saldo)
FROM Cuentas
WHERE Activa = 1;
```

Proceso:

1. Filtra cuentas activas.
2. Busca el saldo máximo entre ellas.

---

## MAX con fechas

MAX funciona perfectamente con fechas.

```sql
SELECT MAX(FechaCreacion)
FROM Cuentas;
```

Resultado:

```text
2025-06-01
```

Significa:

```text
Esa fue la cuenta creada más recientemente.
```

---

## MAX ignora NULL

Supongamos:

| Saldo |
| ----- |
| 1000  |
| 500   |
| NULL  |
| 2000  |

Consulta:

```sql
SELECT MAX(Saldo)
FROM Cuentas;
```

Resultado:

```text
2000
```

El valor NULL no participa en la comparación.

---

## Error común

❌ Incorrecto

```sql
SELECT MAX(*)
FROM Cuentas;
```

✔ Correcto

```sql
SELECT MAX(Saldo)
FROM Cuentas;
```

MAX necesita una columna específica.

---

## Error conceptual frecuente

Muchos principiantes creen que:

```sql
MAX()
```

devuelve la última fila.

Incorrecto.

MAX devuelve:

```text
El valor más grande.
```

No necesariamente corresponde a la última fila almacenada.

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar MAX pregúntate:

1. ¿Qué valor máximo necesito encontrar?
2. ¿Debo filtrar previamente los datos?
3. ¿La columna contiene valores NULL?
4. ¿Estoy trabajando con números o fechas?
5. ¿Qué decisión de negocio depende de este máximo?

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
    AVG(Saldo) AS SaldoPromedio,
    MAX(Saldo) AS SaldoMaximo
FROM Cuentas;
```

Resultado:

```text
SaldoMinimo    : 100
SaldoPromedio  : 8,500
SaldoMaximo    : 95,000
```

Esto permite comprender rápidamente la distribución de los saldos del banco.

---

## Comparación MIN vs MAX

```sql
SELECT
    MIN(Monto) AS MontoMinimo,
    MAX(Monto) AS MontoMaximo
FROM Transacciones;
```

Caso:

```text
Identificar el rango de valores de las transacciones.
```

---

## Resumen

MAX() permite obtener el valor más grande de una columna.

Principales usos:

* Identificar máximos financieros.
* Buscar fechas recientes.
* Detectar operaciones de alto valor.
* Analizar rangos de datos.
* Business Intelligence.
* Data Analytics.
* Data Engineering.
* Auditorías.

Es una función fundamental para el análisis exploratorio y la generación de métricas empresariales.
