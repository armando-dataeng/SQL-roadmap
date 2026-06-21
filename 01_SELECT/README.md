# SELECT

## Definición

La cláusula SELECT define qué columnas serán devueltas por una consulta.

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

SELECT responde:

¿Qué información necesito obtener?
