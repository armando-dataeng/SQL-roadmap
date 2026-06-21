# FROM

## Definición

La cláusula `FROM` especifica la tabla o conjunto de tablas desde donde serán obtenidos los datos.

Toda consulta que recupere información desde una tabla necesita indicar el origen de los datos mediante `FROM`.

---

## Conceptos clave

`FROM` responde a la pregunta:

> ¿De dónde obtendré la información?

La cláusula `FROM` controla el origen de los datos.

No controla:

- Qué información será devuelta → `SELECT`
- Qué filas serán filtradas → `WHERE`
- Cómo serán ordenados los resultados → `ORDER BY`

---

## Sintaxis

```sql
SELECT columna
FROM tabla;
```

---

## Seleccionar datos desde una tabla

### Problema

Mostrar el nombre de todos los clientes registrados.

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

Los datos se encuentran almacenados en la tabla `Clientes`.

Por lo tanto, debemos indicar a SQL que obtenga la información desde esa tabla.

### SQL

```sql
SELECT Nombre
FROM Clientes;
```

---

## Obtener todas las columnas de una tabla

### Problema

Visualizar toda la información disponible de los clientes.

### Datos

Tabla:

```text
Clientes
```

### Lógica

Recuperar todas las columnas existentes en la tabla.

### SQL

```sql
SELECT *
FROM Clientes;
```

---

## Casos de uso reales

### Consultar clientes

```sql
SELECT Nombre
FROM Clientes;
```

Caso:

```text
Obtener el listado de clientes registrados.
```

---

### Consultar cuentas

```sql
SELECT NumeroCuenta
FROM Cuentas;
```

Caso:

```text
Obtener todas las cuentas bancarias existentes.
```

---

### Consultar transacciones

```sql
SELECT *
FROM Transacciones;
```

Caso:

```text
Visualizar movimientos financieros registrados.
```

---

### Consultar usuarios

```sql
SELECT Usuario
FROM Usuarios;
```

Caso:

```text
Obtener el listado de usuarios del sistema.
```

---

## Error común

❌ Incorrecto

```sql
SELECT Nombre;
```

✔ Correcto

```sql
SELECT Nombre
FROM Clientes;
```

---

## Error conceptual frecuente

Un error común es pensar que `FROM` obtiene únicamente tablas.

Incorrecto.

`FROM` define el origen de los datos que utilizará la consulta.

Ese origen puede ser:

- Una tabla
- Varias tablas
- Una vista
- Una subconsulta
- Una expresión derivada

Ejemplo:

```sql
SELECT Nombre
FROM Clientes;
```

Aquí:

- `SELECT` define qué información mostrar.
- `FROM` define de dónde proviene la información.

---

## Pensamiento de Ingeniería de Datos

Antes de escribir una consulta, pregúntate:

1. ¿Qué problema necesito resolver?
2. ¿Qué datos existen?
3. ¿En qué tabla se encuentran esos datos?
4. ¿Cómo represento esa lógica en SQL?

### Relación entre cláusulas

`SELECT` responde:

> ¿Qué información necesito obtener?

`FROM` responde:

> ¿De dónde obtendré esa información?

`WHERE` responde:

> ¿Qué condiciones deben cumplir los datos?

---

## Resumen

La cláusula `FROM` define el origen de los datos utilizados por una consulta.

Puede trabajar con:

- Tablas
- Vistas
- Subconsultas
- Múltiples tablas mediante JOIN

`FROM` no controla:

- Qué información será devuelta (`SELECT`)
- Qué filas serán filtradas (`WHERE`)
- Cómo serán ordenados los resultados (`ORDER BY`)

Toda consulta debe conocer primero el origen de los datos antes de poder recuperarlos, filtrarlos o relacionarlos.
