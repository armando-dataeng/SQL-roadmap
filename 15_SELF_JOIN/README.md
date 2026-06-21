# SELF JOIN

## Definición

Un SELF JOIN ocurre cuando una tabla se relaciona consigo misma.

No existe una cláusula específica llamada SELF JOIN.

Se realiza utilizando un JOIN tradicional (INNER, LEFT, etc.) pero utilizando la misma tabla dos veces mediante alias diferentes.

---

## Conceptos clave

SELF JOIN responde a la pregunta:

> ¿Cómo puedo comparar o relacionar registros dentro de la misma tabla?

Características:

- Utiliza una única tabla.
- Requiere alias obligatoriamente.
- Permite representar jerarquías.
- Permite comparar registros de la misma entidad.

---

## Sintaxis

```sql
SELECT columnas
FROM Tabla A
INNER JOIN Tabla B
    ON A.Columna = B.Columna;
```

Observa que:

```text
Tabla A
```

y

```text
Tabla B
```

son realmente la misma tabla.

---

## Ejemplo clásico: Empleados y Supervisores

### Tabla Empleados

| IdEmpleado | Nombre | IdSupervisor |
|------------|---------|--------------|
| 1 | Carlos | NULL |
| 2 | Ana | 1 |
| 3 | Pedro | 1 |
| 4 | Laura | 2 |

---

## Problema

Mostrar cada empleado junto con el nombre de su supervisor.

### Datos

Tabla:

```text
Empleados
```

Relación:

```text
Empleados.IdSupervisor
=
Empleados.IdEmpleado
```

### Lógica

La misma tabla contiene:

- Empleados
- Supervisores

Por lo tanto:

```text
La tabla debe relacionarse consigo misma.
```

### SQL

```sql
SELECT
    e.Nombre AS Empleado,
    s.Nombre AS Supervisor
FROM Empleados e
INNER JOIN Empleados s
    ON e.IdSupervisor = s.IdEmpleado;
```

---

## Resultado

| Empleado | Supervisor |
|-----------|------------|
| Ana | Carlos |
| Pedro | Carlos |
| Laura | Ana |

---

## ¿Qué representan los alias?

### Alias e

```sql
FROM Empleados e
```

Representa:

```text
Empleado
```

---

### Alias s

```sql
INNER JOIN Empleados s
```

Representa:

```text
Supervisor
```

---

Aunque es la misma tabla:

```text
Empleados
```

SQL la interpreta como dos conjuntos de datos distintos.

---

## Casos de uso reales

### Organigramas

```sql
SELECT
    e.Nombre,
    s.Nombre
FROM Empleados e
INNER JOIN Empleados s
    ON e.IdSupervisor = s.IdEmpleado;
```

Caso:

```text
Construir estructuras organizacionales.
```

---

### Relaciones padre-hijo

Tabla:

```text
Categorias
```

Ejemplo:

```text
Tecnología
 └─ Computadoras
```

Consulta:

```sql
SELECT
    h.Nombre AS Hija,
    p.Nombre AS Padre
FROM Categorias h
INNER JOIN Categorias p
    ON h.IdPadre = p.IdCategoria;
```

---

### Referidos de clientes

Tabla:

```text
Clientes
```

Ejemplo:

```text
Cliente A recomendó Cliente B.
```

Consulta:

```sql
SELECT
    c.Nombre,
    r.Nombre
FROM Clientes c
INNER JOIN Clientes r
    ON c.IdReferidor = r.IdCliente;
```

---

## Base de datos bancaria

Supongamos:

### Tabla Clientes

| IdCliente | Nombre | IdReferidor |
|------------|---------|-------------|
| 1 | Juan | NULL |
| 2 | Ana | 1 |
| 3 | Pedro | 1 |

---

### Consulta

```sql
SELECT
    c.Nombre AS Cliente,
    r.Nombre AS Referidor
FROM Clientes c
INNER JOIN Clientes r
    ON c.IdReferidor = r.IdCliente;
```

---

### Resultado

| Cliente | Referidor |
|----------|-----------|
| Ana | Juan |
| Pedro | Juan |

---

## Error común

❌ Incorrecto

```sql
SELECT *
FROM Empleados
INNER JOIN Empleados;
```

✔ Correcto

```sql
SELECT *
FROM Empleados e
INNER JOIN Empleados s
    ON e.IdSupervisor = s.IdEmpleado;
```

---

## Error conceptual frecuente

Muchos principiantes creen que SELF JOIN es un tipo especial de JOIN.

Incorrecto.

SELF JOIN no es una cláusula SQL.

Es simplemente:

```text
Una tabla unida consigo misma.
```

Utilizando:

- INNER JOIN
- LEFT JOIN
- RIGHT JOIN
- FULL JOIN

según sea necesario.

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar SELF JOIN pregúntate:

1. ¿La relación existe dentro de la misma tabla?
2. ¿Estoy modelando una jerarquía?
3. ¿Necesito comparar registros de la misma entidad?
4. ¿Qué alias harán más legible la consulta?

### Relación entre conceptos

INNER JOIN responde:

> ¿Qué registros coinciden entre dos tablas?

SELF JOIN responde:

> ¿Qué registros coinciden dentro de la misma tabla?

---

## Resumen

SELF JOIN permite relacionar una tabla consigo misma.

Características principales:

- Utiliza alias obligatoriamente.
- No es una cláusula SQL independiente.
- Se construye usando JOINs tradicionales.
- Permite modelar jerarquías.
- Facilita comparaciones internas.

Es ampliamente utilizado para:

- Organigramas.
- Relaciones padre-hijo.
- Categorías jerárquicas.
- Sistemas de referidos.
- Estructuras empresariales.
- Ingeniería de Datos.
