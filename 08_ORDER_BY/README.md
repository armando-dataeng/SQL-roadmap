# ORDER BY

## Definición

La cláusula `ORDER BY` permite ordenar los resultados devueltos por una consulta.

Puede ordenar los registros de forma:

- Ascendente (ASC)
- Descendente (DESC)

Si no se especifica un tipo de orden, SQL utiliza `ASC` por defecto.

---

## Conceptos clave

ORDER BY responde a la pregunta:

> ¿Cómo quiero visualizar los resultados?

ORDER BY no modifica los datos almacenados en la base de datos.

Únicamente cambia el orden en que se muestran los resultados de una consulta.

---

## Sintaxis

```sql
SELECT columnas
FROM tabla
ORDER BY columna;
```

Orden ascendente:

```sql
SELECT columnas
FROM tabla
ORDER BY columna ASC;
```

Orden descendente:

```sql
SELECT columnas
FROM tabla
ORDER BY columna DESC;
```

---

## Ordenar clientes por nombre

### Problema

Mostrar los clientes ordenados alfabéticamente.

### Datos

Tabla:

```text
Clientes
```

Columna:

```text
Nombre
```

### Lógica

Ordenar los nombres desde la A hasta la Z.

### SQL

```sql
SELECT *
FROM Clientes
ORDER BY Nombre ASC;
```

---

## Ordenar cuentas por saldo

### Problema

Mostrar las cuentas desde el saldo más alto hasta el más bajo.

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

Ordenar de mayor a menor.

### SQL

```sql
SELECT *
FROM Cuentas
ORDER BY Saldo DESC;
```

---

## Casos de uso reales

### Clientes ordenados alfabéticamente

```sql
SELECT *
FROM Clientes
ORDER BY Nombre ASC;
```

Caso:

```text
Generar listados organizados para atención al cliente.
```

---

### Cuentas con mayor saldo primero

```sql
SELECT *
FROM Cuentas
ORDER BY Saldo DESC;
```

Caso:

```text
Identificar clientes de mayor valor financiero.
```

---

### Transacciones más recientes

```sql
SELECT *
FROM Transacciones
ORDER BY FechaTransaccion DESC;
```

Caso:

```text
Visualizar primero los movimientos más recientes.
```

---

### Usuarios por fecha de creación

```sql
SELECT *
FROM Usuarios
ORDER BY FechaCreacion ASC;
```

Caso:

```text
Analizar el crecimiento histórico del sistema.
```

---

## ASC (Ascendente)

Ordena de menor a mayor.

Ejemplo:

```sql
SELECT *
FROM Cuentas
ORDER BY Saldo ASC;
```

Resultado:

```text
1000
2500
5000
10000
```

---

## DESC (Descendente)

Ordena de mayor a menor.

Ejemplo:

```sql
SELECT *
FROM Cuentas
ORDER BY Saldo DESC;
```

Resultado:

```text
10000
5000
2500
1000
```

---

## Ordenar por múltiples columnas

### Problema

Ordenar clientes por país y luego por nombre.

### SQL

```sql
SELECT *
FROM Clientes
ORDER BY Pais ASC, Nombre ASC;
```

### Lógica

Primero SQL ordena por:

```text
Pais
```

Luego, dentro de cada país, ordena por:

```text
Nombre
```

---

## Error común

❌ Incorrecto

```sql
SELECT *
FROM Clientes
ORDER BY ASC;
```

✔ Correcto

```sql
SELECT *
FROM Clientes
ORDER BY Nombre ASC;
```

---

## Error conceptual frecuente

Muchos principiantes creen que ORDER BY filtra registros.

Incorrecto.

ORDER BY no elimina filas.

Solo cambia el orden de presentación.

Ejemplo:

```sql
SELECT *
FROM Clientes
ORDER BY Nombre ASC;
```

La consulta devuelve los mismos registros.

La única diferencia es el orden.

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar ORDER BY pregúntate:

1. ¿Qué información es más importante visualizar primero?
2. ¿Necesito orden ascendente o descendente?
3. ¿Estoy trabajando con texto, números o fechas?
4. ¿Necesito ordenar por más de una columna?

### Relación entre conceptos

SELECT responde:

> ¿Qué información necesito obtener?

FROM responde:

> ¿De dónde obtendré esa información?

WHERE responde:

> ¿Qué registros necesito?

ORDER BY responde:

> ¿Cómo quiero visualizar esos registros?

---

## Resumen

ORDER BY permite ordenar los resultados de una consulta.

Opciones principales:

- ASC → Ascendente
- DESC → Descendente

Características:

- No modifica los datos almacenados.
- Solo afecta la presentación del resultado.
- Puede ordenar por una o varias columnas.
- Funciona con texto, números y fechas.

Es ampliamente utilizado en:

- Reportes
- Dashboards
- Sistemas bancarios
- Aplicaciones empresariales
- Análisis de datos
