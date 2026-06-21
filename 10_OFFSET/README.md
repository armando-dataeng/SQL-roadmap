# OFFSET

## Definición

La cláusula `OFFSET` permite omitir una cantidad determinada de filas antes de comenzar a devolver resultados.

Se utiliza principalmente para:

- Paginación
- Navegación de resultados
- Dashboards
- APIs
- Consultas sobre grandes volúmenes de datos

En SQL Server, OFFSET debe utilizarse junto con ORDER BY.

---

## Conceptos clave

OFFSET responde a la pregunta:

> ¿Cuántos registros debo saltar antes de mostrar resultados?

OFFSET no limita registros.

OFFSET únicamente omite filas.

Para limitar filas normalmente se combina con:

```sql
FETCH NEXT
```

o conceptualmente con:

```sql
TOP
```

---

## Sintaxis

```sql
SELECT columnas
FROM tabla
ORDER BY columna
OFFSET cantidad ROWS;
```

Ejemplo:

```sql
SELECT *
FROM Clientes
ORDER BY IdCliente
OFFSET 5 ROWS;
```

---

## Saltar los primeros 5 clientes

### Problema

Mostrar los clientes después de los primeros cinco registros.

### Datos

Tabla:

```text
Clientes
```

Columna:

```text
IdCliente
```

### Lógica

Ignorar los primeros cinco registros.

### SQL

```sql
SELECT *
FROM Clientes
ORDER BY IdCliente
OFFSET 5 ROWS;
```

---

## Mostrar la segunda página de resultados

### Problema

Mostrar los siguientes cinco clientes después de los primeros cinco.

### Datos

Tabla:

```text
Clientes
```

### Lógica

1. Saltar los primeros cinco registros.
2. Mostrar los siguientes cinco.

### SQL

```sql
SELECT *
FROM Clientes
ORDER BY IdCliente
OFFSET 5 ROWS
FETCH NEXT 5 ROWS ONLY;
```

---

## Casos de uso reales

### Segunda página de clientes

```sql
SELECT *
FROM Clientes
ORDER BY IdCliente
OFFSET 10 ROWS
FETCH NEXT 10 ROWS ONLY;
```

Caso:

```text
Mostrar la página 2 de un listado de clientes.
```

---

### Tercera página de cuentas

```sql
SELECT *
FROM Cuentas
ORDER BY IdCuenta
OFFSET 20 ROWS
FETCH NEXT 10 ROWS ONLY;
```

Caso:

```text
Navegación paginada de cuentas bancarias.
```

---

### Transacciones recientes por bloques

```sql
SELECT *
FROM Transacciones
ORDER BY FechaTransaccion DESC
OFFSET 50 ROWS
FETCH NEXT 25 ROWS ONLY;
```

Caso:

```text
Consultar bloques de movimientos financieros.
```

---

### Usuarios del sistema

```sql
SELECT *
FROM Usuarios
ORDER BY IdUsuario
OFFSET 100 ROWS
FETCH NEXT 20 ROWS ONLY;
```

Caso:

```text
Paginación en aplicaciones empresariales.
```

---

## OFFSET sin FETCH

También es válido:

```sql
SELECT *
FROM Clientes
ORDER BY IdCliente
OFFSET 5 ROWS;
```

### Resultado

SQL ignora los primeros cinco registros y devuelve todos los demás.

---

## OFFSET con FETCH

```sql
SELECT *
FROM Clientes
ORDER BY IdCliente
OFFSET 5 ROWS
FETCH NEXT 5 ROWS ONLY;
```

### Resultado

SQL:

1. Omite cinco filas.
2. Devuelve cinco filas.

---

## Error común

❌ Incorrecto

```sql
SELECT *
FROM Clientes
OFFSET 5 ROWS;
```

✔ Correcto

```sql
SELECT *
FROM Clientes
ORDER BY IdCliente
OFFSET 5 ROWS;
```

---

## ¿Por qué ocurre este error?

En SQL Server:

```sql
OFFSET
```

requiere obligatoriamente:

```sql
ORDER BY
```

Porque SQL necesita saber en qué orden contar las filas que serán omitidas.

---

## Error conceptual frecuente

Muchos principiantes creen que:

```sql
OFFSET 5 ROWS
```

devuelve cinco registros.

Incorrecto.

OFFSET solamente omite filas.

Ejemplo:

```sql
SELECT *
FROM Clientes
ORDER BY IdCliente
OFFSET 5 ROWS;
```

Resultado:

```text
Se ignoran los primeros cinco registros.
Se muestran todos los demás.
```

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar OFFSET pregúntate:

1. ¿Necesito paginar resultados?
2. ¿Cuántas filas debo omitir?
3. ¿Cuántas filas debo mostrar?
4. ¿Tengo una columna adecuada para ORDER BY?

### Relación entre conceptos

SELECT responde:

> ¿Qué información necesito obtener?

FROM responde:

> ¿De dónde obtendré esa información?

WHERE responde:

> ¿Qué registros necesito?

ORDER BY responde:

> ¿Cómo quiero visualizar esos registros?

TOP responde:

> ¿Cuántos registros necesito devolver?

OFFSET responde:

> ¿Cuántos registros debo omitir antes de devolver resultados?

---

## Resumen

OFFSET permite omitir filas antes de devolver resultados.

Características principales:

- Requiere ORDER BY en SQL Server.
- No limita resultados.
- Omite filas.
- Se utiliza para paginación.
- Funciona frecuentemente junto con FETCH NEXT.

Es ampliamente utilizado en:

- Aplicaciones web
- Dashboards
- APIs
- Reportes
- Sistemas bancarios
- Grandes volúmenes de datos
