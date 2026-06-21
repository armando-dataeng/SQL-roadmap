# SELECT

## Definición

La cláusula `SELECT` define qué información será devuelta por una consulta.

Normalmente se utiliza para seleccionar columnas específicas o todas las columnas de una tabla.

---

## Conceptos clave

`SELECT` responde a la pregunta:

> ¿Qué información necesito obtener?

`SELECT` controla las columnas que serán devueltas por la consulta.

No controla:

- De dónde vienen los datos → `FROM`
- Qué filas serán filtradas → `WHERE`
- Cómo serán ordenados los resultados → `ORDER BY`

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

Tabla: `Clientes`  
Columna: `Nombre`

### Lógica

Recuperar únicamente la columna `Nombre`.

### SQL

```sql
SELECT Nombre
FROM Clientes;
```

---

## Seleccionar múltiples columnas

### Problema

Mostrar nombre, apellido y correo electrónico de los clientes.

### Datos

Tabla: `Clientes`  
Columnas: `Nombre`, `Apellido`, `Email`

### Lógica

Recuperar únicamente las columnas necesarias para identificar y contactar clientes.

### SQL

```sql
SELECT
    Nombre,
    Apellido,
    Email
FROM Clientes;
```

---

## Uso del asterisco (*)

El asterisco `*` significa:

> Devuelve todas las columnas disponibles.

### Ejemplo

```sql
SELECT *
FROM Clientes;
```

### Consideración profesional

Aunque `SELECT *` es útil para exploración y aprendizaje, en entornos profesionales suele preferirse seleccionar solo las columnas necesarias.

Esto mejora:

- Legibilidad
- Seguridad
- Rendimiento
- Mantenimiento de consultas

---

## Error común

❌ Incorrecto:

```sql
SELECT
FROM Clientes;
```

✔ Correcto:

```sql
SELECT Nombre
FROM Clientes;
```

---

## Error conceptual frecuente

Un error común es pensar que `SELECT` controla las filas.

Eso es incorrecto.

`SELECT` controla qué columnas o expresiones se devuelven.

Las filas se controlan con `WHERE`.

Ejemplo:

```sql
SELECT Nombre
FROM Clientes
WHERE Activo = 1;
```

Aquí:

- `SELECT Nombre` indica qué columna se devuelve.
- `FROM Clientes` indica la tabla origen.
- `WHERE Activo = 1` indica qué filas cumplen la condición.

---

## Pensamiento de Ingeniería de Datos

Antes de escribir una consulta, piensa:

1. ¿Qué problema necesito resolver?
2. ¿Qué datos existen?
3. ¿Qué información necesito obtener?
4. ¿Qué SQL representa esa lógica?

En una consulta básica:

- `SELECT` responde: ¿Qué información necesito obtener?
- `FROM` responde: ¿De dónde obtendré esa información?
- `WHERE` responde: ¿Qué condiciones deben cumplir los datos?
