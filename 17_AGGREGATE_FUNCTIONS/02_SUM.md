# SUM()

## Definición

La función `SUM()` permite sumar todos los valores de una columna numérica.

Es una de las funciones agregadas más utilizadas en SQL para análisis financieros, reportes y métricas de negocio.

---

## Conceptos clave

SUM responde a la pregunta:

> ¿Cuál es el total acumulado?

Características:

* Opera sobre columnas numéricas.
* Devuelve un único resultado.
* Ignora valores NULL.
* No modifica datos.

---

## Sintaxis

```sql
SELECT SUM(columna)
FROM tabla;
```

Ejemplo:

```sql
SELECT SUM(Saldo)
FROM Cuentas;
```

---

## Problema

Determinar cuánto dinero administra el banco en todas las cuentas.

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

Sumar todos los saldos existentes.

### SQL

```sql
SELECT SUM(Saldo)
FROM Cuentas;
```

---

## Resultado esperado

```text
1,250,000
```

Significa:

```text
El banco administra 1,250,000 unidades monetarias.
```

---

## SUM sobre Transacciones

### Problema

Calcular el monto total movido por todas las transacciones.

### SQL

```sql
SELECT SUM(Monto)
FROM Transacciones;
```

---

## Casos de uso reales

### Saldo total del banco

```sql
SELECT SUM(Saldo)
FROM Cuentas;
```

Caso:

```text
Conocer el dinero total administrado.
```

---

### Total de depósitos

```sql
SELECT SUM(Monto)
FROM Transacciones
WHERE TipoTransaccion = 'Deposito';
```

Caso:

```text
Calcular el total depositado por los clientes.
```

---

### Total de retiros

```sql
SELECT SUM(Monto)
FROM Transacciones
WHERE TipoTransaccion = 'Retiro';
```

Caso:

```text
Calcular el total retirado.
```

---

### Movimientos de una cuenta específica

```sql
SELECT SUM(Monto)
FROM Transacciones
WHERE IdCuenta = 1;
```

Caso:

```text
Conocer el volumen de movimientos de una cuenta.
```

---

## SUM con WHERE

SUM puede combinarse con filtros.

```sql
SELECT SUM(Saldo)
FROM Cuentas
WHERE Activa = 1;
```

Aquí SQL:

1. Filtra las cuentas activas.
2. Suma únicamente esos saldos.

---

## SUM ignora NULL

Supongamos:

| Saldo |
| ----- |
| 1000  |
| 2000  |
| NULL  |
| 3000  |

Consulta:

```sql
SELECT SUM(Saldo)
FROM Cuentas;
```

Resultado:

```text
6000
```

El valor NULL no participa en la suma.

---

## Error común

❌ Incorrecto

```sql
SELECT SUM(Nombre)
FROM Clientes;
```

✔ Correcto

```sql
SELECT SUM(Saldo)
FROM Cuentas;
```

SUM solo debe utilizarse sobre columnas numéricas.

---

## Error conceptual frecuente

Muchos principiantes creen que:

```sql
SUM()
```

cuenta registros.

Incorrecto.

SUM suma valores.

Para contar registros se utiliza:

```sql
COUNT(*)
```

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar SUM pregúntate:

1. ¿La columna es numérica?
2. ¿Necesito sumar todos los registros o solo algunos?
3. ¿Debo aplicar filtros con WHERE?
4. ¿Existen valores NULL?
5. ¿Estoy calculando una métrica de negocio?

---

## Relación con otros conceptos

```text
COUNT() → Cuenta registros
SUM()   → Suma valores
AVG()   → Calcula promedios
MIN()   → Obtiene el menor valor
MAX()   → Obtiene el mayor valor
```

---

## Resumen

SUM() permite obtener el total acumulado de una columna numérica.

Principales usos:

* Saldos bancarios
* Ventas
* Ingresos
* Costos
* Transacciones
* KPIs
* Dashboards
* Business Intelligence
* Data Engineering

Es una de las funciones más utilizadas en sistemas financieros y analíticos.
