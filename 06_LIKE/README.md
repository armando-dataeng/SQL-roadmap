# LIKE

## Definición

El operador `LIKE` permite buscar patrones dentro de valores de texto.

Se utiliza cuando no se conoce exactamente el valor que se desea encontrar o cuando se necesita realizar búsquedas parciales.

A diferencia del operador `=`, que busca coincidencias exactas, `LIKE` permite encontrar coincidencias basadas en patrones.

---

## Conceptos clave

LIKE responde a la pregunta:

> ¿Qué patrón de texto necesito encontrar?

LIKE trabaja principalmente junto con:

- WHERE
- Operadores lógicos
- Operadores de comparación

Los comodines más utilizados son:

| Comodín | Significado |
|----------|------------|
| % | Cero o más caracteres |
| _ | Un único carácter |

---

## Sintaxis

```sql
SELECT columnas
FROM tabla
WHERE columna LIKE patron;
```

Ejemplo:

```sql
SELECT *
FROM Clientes
WHERE Nombre LIKE 'A%';
```

---

## Buscar nombres que comienzan con una letra

### Problema

Mostrar clientes cuyo nombre comienza con la letra A.

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

Buscar registros cuyo nombre empiece por A.

### SQL

```sql
SELECT *
FROM Clientes
WHERE Nombre LIKE 'A%';
```

---

## Buscar nombres que terminan con una letra

### Problema

Mostrar clientes cuyo nombre termina con la letra O.

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

Buscar registros cuyo nombre finalice con O.

### SQL

```sql
SELECT *
FROM Clientes
WHERE Nombre LIKE '%O';
```

---

## Buscar texto contenido dentro de una cadena

### Problema

Encontrar clientes cuyo nombre contiene "Mar".

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

Buscar registros que contengan la secuencia de caracteres "Mar" en cualquier posición.

### SQL

```sql
SELECT *
FROM Clientes
WHERE Nombre LIKE '%Mar%';
```

---

## Casos de uso reales

### Buscar clientes por nombre parcial

```sql
SELECT *
FROM Clientes
WHERE Nombre LIKE 'J%';
```

Caso:

```text
Encontrar clientes cuyo nombre comienza con J.
```

---

### Buscar cuentas por prefijo

```sql
SELECT *
FROM Cuentas
WHERE NumeroCuenta LIKE '001%';
```

Caso:

```text
Identificar cuentas pertenecientes a una sucursal específica.
```

---

### Buscar correos corporativos

```sql
SELECT *
FROM Usuarios
WHERE Correo LIKE '%@empresa.com';
```

Caso:

```text
Identificar usuarios con correo corporativo.
```

---

### Buscar transferencias

```sql
SELECT *
FROM Transacciones
WHERE TipoTransaccion LIKE '%Transferencia%';
```

Caso:

```text
Encontrar movimientos relacionados con transferencias.
```

---

## Uso del comodín %

### Comienza con

```sql
WHERE Nombre LIKE 'A%'
```

Ejemplos:

```text
Ana
Andrés
Antonio
```

---

### Termina con

```sql
WHERE Nombre LIKE '%o'
```

Ejemplos:

```text
Pedro
Mario
Bruno
```

---

### Contiene

```sql
WHERE Nombre LIKE '%Mar%'
```

Ejemplos:

```text
María
Mario
Omar
```

---

## Uso del comodín _

El símbolo `_` representa exactamente un carácter.

Ejemplo:

```sql
SELECT *
FROM Clientes
WHERE Nombre LIKE '_uan';
```

Coincide con:

```text
Juan
```

No coincide con:

```text
Juanito
Manuel
```

---

## Uso combinado con operadores lógicos

### Ejemplo

```sql
SELECT *
FROM Clientes
WHERE Nombre LIKE 'G%'
OR Nombre LIKE 'R%';
```

---

### Utilizando paréntesis

```sql
SELECT *
FROM Clientes
WHERE Activo = 1
AND (
    Nombre LIKE 'G%'
    OR Nombre LIKE 'R%'
);
```

### Lógica

Primero SQL evalúa:

```sql
Nombre LIKE 'G%'
OR Nombre LIKE 'R%'
```

Después evalúa:

```sql
Activo = 1
```

---

## Error común

❌ Incorrecto

```sql
SELECT *
FROM Clientes
WHERE Nombre LIKE A%;
```

✔ Correcto

```sql
SELECT *
FROM Clientes
WHERE Nombre LIKE 'A%';
```

---

## Error conceptual frecuente

Muchos principiantes creen que:

```sql
LIKE
```

es equivalente a:

```sql
=
```

Incorrecto.

### Coincidencia exacta

```sql
SELECT *
FROM Clientes
WHERE Nombre = 'Juan';
```

---

### Coincidencia por patrón

```sql
SELECT *
FROM Clientes
WHERE Nombre LIKE 'J%';
```

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar LIKE pregúntate:

1. ¿Conozco el valor exacto?
2. ¿Necesito una coincidencia parcial?
3. ¿El patrón aparece al inicio, medio o final?
4. ¿Qué comodín representa mejor mi necesidad?

### Relación entre conceptos

SELECT responde:

> ¿Qué información necesito obtener?

FROM responde:

> ¿De dónde obtendré esa información?

WHERE responde:

> ¿Qué registros necesito?

Operadores de comparación responden:

> ¿Cómo comparo valores?

Operadores lógicos responden:

> ¿Cómo combino condiciones?

LIKE responde:

> ¿Qué patrón de texto necesito encontrar?

---

## Resumen

LIKE permite buscar patrones dentro de cadenas de texto.

Comodines principales:

- `%` → cero o más caracteres.
- `_` → exactamente un carácter.

Es ampliamente utilizado para:

- Búsquedas parciales.
- Filtros por nombre.
- Correos electrónicos.
- Códigos.
- Referencias.
- Sistemas de búsqueda.

Cuando se necesita una coincidencia exacta, generalmente debe utilizarse el operador `=`.
