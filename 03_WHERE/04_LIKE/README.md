# LIKE

## Definición

El operador `LIKE` permite buscar patrones dentro de valores de texto.

Se utiliza principalmente para realizar búsquedas parciales cuando no se conoce el valor exacto que se desea encontrar.

---

## Conceptos clave

`LIKE` responde a la pregunta:

> ¿Qué patrón de texto necesito encontrar?

A diferencia del operador `=`, que busca coincidencias exactas, `LIKE` permite encontrar coincidencias parciales.

Los comodines más utilizados son:

| Comodín | Significado |
|----------|-------------|
| % | Cero o más caracteres |
| _ | Un único carácter |

---

## Sintaxis

```sql
SELECT columna
FROM tabla
WHERE columna LIKE patron;
```

---

## Buscar clientes cuyo nombre comienza con una letra

### Problema

Mostrar los clientes cuyo nombre comienza con la letra A.

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

Buscar registros donde el nombre empiece por A.

### SQL

```sql
SELECT *
FROM Clientes
WHERE Nombre LIKE 'A%';
```

---

## Buscar clientes cuyo nombre termina con una letra

### Problema

Mostrar clientes cuyo nombre termina en o.

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

Buscar registros cuyo nombre finalice con la letra o.

### SQL

```sql
SELECT *
FROM Clientes
WHERE Nombre LIKE '%o';
```

---

## Buscar texto contenido dentro de una cadena

### Problema

Encontrar clientes cuyo nombre contenga la palabra "Mar".

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
Encontrar rápidamente clientes cuyo nombre comienza con J.
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

### Buscar transacciones por referencia

```sql
SELECT *
FROM Transacciones
WHERE TipoTransaccion LIKE '%Transferencia%';
```

Caso:

```text
Localizar movimientos relacionados con transferencias.
```

---

## Uso del comodín %

### Comienza con

```sql
WHERE Nombre LIKE 'A%'
```

Ejemplos válidos:

```text
Ana
Antonio
Andrés
```

---

### Termina con

```sql
WHERE Nombre LIKE '%o'
```

Ejemplos válidos:

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

Ejemplos válidos:

```text
María
Mario
Omar
```

---

## Uso del comodín _

El guion bajo representa exactamente un carácter.

Ejemplo:

```sql
WHERE Nombre LIKE '_uan'
```

Coincidencias:

```text
Juan
```

No coinciden:

```text
Juanito
Manuel
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

Un error común es pensar que `LIKE` busca únicamente coincidencias exactas.

Incorrecto.

Para coincidencias exactas normalmente se utiliza:

```sql
=
```

Ejemplo:

```sql
SELECT *
FROM Clientes
WHERE Nombre = 'Juan';
```

`LIKE` se utiliza para patrones:

```sql
SELECT *
FROM Clientes
WHERE Nombre LIKE 'J%';
```

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar `LIKE`, pregúntate:

1. ¿Conozco el valor exacto?
2. ¿Necesito una coincidencia parcial?
3. ¿El patrón aparece al inicio, medio o final del texto?
4. ¿Qué comodín representa mejor mi necesidad?

### Relación entre cláusulas

`SELECT` responde:

> ¿Qué información necesito obtener?

`FROM` responde:

> ¿De dónde obtendré esa información?

`WHERE` responde:

> ¿Qué registros cumplen la condición?

`LIKE` responde:

> ¿Qué patrón de texto necesito encontrar?

---

## Resumen

El operador `LIKE` permite buscar patrones dentro de cadenas de texto.

Los comodines más utilizados son:

- `%` → cero o más caracteres.
- `_` → exactamente un carácter.

`LIKE` es especialmente útil para:

- Búsquedas parciales.
- Filtrado de nombres.
- Filtrado de correos.
- Filtrado de códigos.
- Búsquedas flexibles en aplicaciones.

Cuando necesitas una coincidencia exacta, generalmente debes utilizar el operador `=`.
