# SELECT

## Definición

La cláusula SELECT define qué información será devuelta por una consulta. 


Normalmente se utiliza para seleccionar columnas específicas o todas las columnas de una tabla.
---

## Sintaxis

```sql
SELECT columna
FROM tabla;
```

---

## Problema

Mostrar el nombre de todos los clientes.

### Datos

Tabla:

Clientes

Columna:

Nombre

### Lógica

Recuperar únicamente la columna Nombre.

### SQL

```sql
SELECT Nombre
FROM Clientes;
```
SELECT
    Nombre,
    Apellido,
    Email
FROM Clientes;
Explicacion: SELECT puede devolver una o múltiples columnas.
---

## Error común

❌

```sql
SELECT
FROM Clientes;
```

✔

```sql
SELECT Nombre
FROM Clientes;
```

---

## Pensamiento de Ingeniería de Datos

SELECT responde a la pregunta:

¿Qué información necesito obtener?

FROM responde:

¿De dónde obtendré esa información?

WHERE responde:

¿Qué condiciones deben cumplir los datos?
