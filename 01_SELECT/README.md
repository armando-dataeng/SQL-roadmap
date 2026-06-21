# SELECT

## Definición

La cláusula `SELECT` define qué información será devuelta por una consulta.

Normalmente se utiliza para seleccionar columnas específicas o todas las columnas de una tabla.

---

## Conceptos clave

`SELECT` responde a la pregunta:

> ¿Qué información necesito obtener?

`SELECT` controla qué información será devuelta por una consulta.

Puede devolver:

- Una columna
- Varias columnas
- Todas las columnas mediante (*)
- Expresiones
- Resultados de funciones

Ejemplos:

```sql
SELECT Nombre
FROM Clientes;
```

```sql
SELECT Nombre, Apellido
FROM Clientes;
```

```sql
SELECT *
FROM Clientes;
```

---

## Sintaxis

```sql
SELECT columna
FROM tabla;
```

---

## Seleccionar una columna

### Problema

Mostrar el nombre de todos los clientes.

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

Recuperar únicamente la columna Nombre.

### SQL

```sql
SELECT Nombre
FROM Clientes;
```

---

## Seleccionar múltiples columnas

### Problema

Mostrar nombre, apellido y correo electrónico de todos los clientes.

### Datos

Tabla:

```text
Clientes
```

Columnas:

```text
Nombre
Apellido
Email
```

### Lógica

Recuperar únicamente las columnas necesarias para identificar y contactar a los clientes.

### SQL

```sql
SELECT
    Nombre,
    Apellido,
    Email
FROM Clientes;
```

### Explicación

`SELECT` puede devolver una o múltiples columnas dependiendo de la necesidad del problema.

---

## Uso del asterisco (*)

El símbolo `*` significa:

> Devuelve todas las columnas disponibles.

### Ejemplo

```sql
SELECT *
FROM Clientes;
```

### Ventajas

- Exploración rápida de datos.
- Aprendizaje.
- Pruebas rápidas.

### Desventajas

- Menor rendimiento.
- Menor claridad.
- Dependencia de cambios en el esquema.

### Consideración profesional

En entornos profesionales suele preferirse especificar únicamente las columnas necesarias.

Ejemplo:

```sql
SELECT
    Nombre,
    Apellido,
    Email
FROM Clientes;
```

---

## Error común

❌ Incorrecto

```sql
SELECT
FROM Clientes;
```

✔ Correcto

```sql
SELECT Nombre
FROM Clientes;
```

---

## Error conceptual frecuente

Un error común es pensar que `SELECT` controla las filas.

Incorrecto.

`SELECT` controla las columnas o expresiones que serán devueltas.

Las filas son controladas mediante la cláusula `WHERE`.

Ejemplo:

```sql
SELECT Nombre
FROM Clientes
WHERE Activo = 1;
```

### Explicación

- `SELECT` define qué información mostrar.
- `FROM` define de dónde provienen los datos.
- `WHERE` define qué registros cumplen la condición.

---

## Pensamiento de Ingeniería de Datos

Antes de escribir una consulta, piensa:

1. ¿Qué problema necesito resolver?
2. ¿Qué datos existen?
3. ¿Qué información necesito obtener?
4. ¿Cómo represento esa lógica en SQL?

### Relación entre cláusulas

`SELECT` responde:

> ¿Qué información necesito obtener?

`FROM` responde:

> ¿De dónde obtendré esa información?

`WHERE` responde:

> ¿Qué condiciones deben cumplir los datos?

## Resumen

SELECT es la cláusula encargada de definir qué información será devuelta por una consulta.

Puede devolver:

- Una columna
- Varias columnas
- Todas las columnas mediante (*)
- Expresiones
- Funciones

SELECT no controla:

- El origen de los datos (FROM)
- El filtrado de filas (WHERE)
- El ordenamiento (ORDER BY)
