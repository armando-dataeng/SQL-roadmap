# Operadores Lógicos

## Definición

Los operadores lógicos permiten combinar múltiples condiciones dentro de una consulta SQL.

Su función es determinar cómo se evaluarán dos o más expresiones lógicas.

Son ampliamente utilizados en:

- WHERE
- HAVING
- JOIN
- CASE

---

## Conceptos clave

Los operadores lógicos responden a la pregunta:

> ¿Cómo relaciono varias condiciones entre sí?

Los operadores lógicos principales son:

| Operador | Significado |
|-----------|------------|
| AND | Todas las condiciones deben cumplirse |
| OR | Al menos una condición debe cumplirse |
| NOT | Invierte el resultado de una condición |

---

## Sintaxis

### AND

```sql
SELECT *
FROM tabla
WHERE condicion1
AND condicion2;
```

### OR

```sql
SELECT *
FROM tabla
WHERE condicion1
OR condicion2;
```

### NOT

```sql
SELECT *
FROM tabla
WHERE NOT condicion;
```

---

## Operador AND

### Problema

Mostrar clientes activos llamados Juan.

### Datos

Tabla:

```text
Clientes
```

Columnas:

```text
Nombre
Activo
```

### Lógica

Ambas condiciones deben cumplirse:

- Nombre = Juan
- Activo = 1

### SQL

```sql
SELECT *
FROM Clientes
WHERE Nombre = 'Juan'
AND Activo = 1;
```

---

## Operador OR

### Problema

Mostrar clientes llamados Juan o Pedro.

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

Puede cumplirse cualquiera de las dos condiciones.

### SQL

```sql
SELECT *
FROM Clientes
WHERE Nombre = 'Juan'
OR Nombre = 'Pedro';
```

---

## Operador NOT

### Problema

Mostrar clientes que no estén activos.

### Datos

Tabla:

```text
Clientes
```

Columna:

```text
Activo
```

### Lógica

Invertir la condición.

### SQL

```sql
SELECT *
FROM Clientes
WHERE NOT Activo = 1;
```

---

## Casos de uso reales

### Clientes activos con saldo alto

```sql
SELECT *
FROM Cuentas
WHERE Activa = 1
AND Saldo > 10000;
```

Caso:

```text
Identificar clientes premium activos.
```

---

### Clientes de varias ciudades

```sql
SELECT *
FROM Clientes
WHERE Ciudad = 'Madrid'
OR Ciudad = 'Barcelona';
```

Caso:

```text
Segmentar clientes por ubicación.
```

---

### Usuarios que no son administradores

```sql
SELECT *
FROM Usuarios
WHERE NOT Rol = 'Administrador';
```

Caso:

```text
Auditoría de permisos.
```

---

## Uso de paréntesis

Los paréntesis permiten controlar el orden lógico de evaluación.

Ejemplo:

```sql
SELECT *
FROM Clientes
WHERE Activo = 1
AND (Nombre LIKE 'G%'
     OR Nombre LIKE 'R%');
```

### Lógica

Primero SQL evalúa:

```sql
Nombre LIKE 'G%'
OR Nombre LIKE 'R%'
```

Luego verifica:

```sql
Activo = 1
```

---

## Error común

❌ Incorrecto

```sql
SELECT *
FROM Clientes
WHERE Nombre = 'Juan'
OR 'Pedro';
```

✔ Correcto

```sql
SELECT *
FROM Clientes
WHERE Nombre = 'Juan'
OR Nombre = 'Pedro';
```

---

## Error conceptual frecuente

Muchos principiantes creen que:

```sql
AND
```

y

```sql
OR
```

funcionan igual.

Incorrecto.

### AND

Todas las condiciones deben cumplirse.

```sql
Nombre = 'Juan'
AND Activo = 1
```

---

### OR

Basta con que una condición sea verdadera.

```sql
Nombre = 'Juan'
OR Nombre = 'Pedro'
```

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar operadores lógicos pregúntate:

1. ¿Necesito una sola condición o varias?
2. ¿Todas deben cumplirse?
3. ¿Basta con que una se cumpla?
4. ¿Necesito controlar el orden lógico mediante paréntesis?

### Relación entre conceptos

SELECT responde:

> ¿Qué información necesito obtener?

FROM responde:

> ¿De dónde obtendré esa información?

WHERE responde:

> ¿Qué registros necesito?

Operadores de comparación responden:

> ¿Cómo comparo los valores?

Operadores lógicos responden:

> ¿Cómo combino múltiples condiciones?

---

## Resumen

Los operadores lógicos permiten combinar condiciones dentro de una consulta SQL.

Principales operadores:

- AND
- OR
- NOT

Conceptos fundamentales:

- AND exige que todas las condiciones sean verdaderas.
- OR exige que al menos una condición sea verdadera.
- NOT invierte una condición.
- Los paréntesis permiten controlar el orden de evaluación.

Los operadores lógicos son esenciales para construir filtros complejos y consultas utilizadas en entornos reales.
