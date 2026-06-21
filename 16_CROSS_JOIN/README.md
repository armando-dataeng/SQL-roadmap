# CROSS JOIN

## Definición

La cláusula `CROSS JOIN` combina cada fila de una tabla con cada fila de otra tabla.

No requiere una condición `ON`.

El resultado es conocido como:

```text
Producto Cartesiano
```

---

## Conceptos clave

CROSS JOIN responde a la pregunta:

> ¿Qué ocurre si combino todos los registros de una tabla con todos los registros de otra?

Características:

- No utiliza ON.
- No busca coincidencias.
- Combina todo con todo.
- Puede generar grandes cantidades de registros.

---

## Sintaxis

```sql
SELECT columnas
FROM TablaA
CROSS JOIN TablaB;
```

Ejemplo:

```sql
SELECT *
FROM Clientes
CROSS JOIN Productos;
```

---

## Producto Cartesiano

Supongamos:

### Tabla Clientes

| IdCliente | Nombre |
|------------|---------|
| 1 | Juan |
| 2 | Ana |

---

### Tabla Productos

| IdProducto | Producto |
|------------|----------|
| 10 | Laptop |
| 20 | Mouse |

---

## Consulta

```sql
SELECT
    c.Nombre,
    p.Producto
FROM Clientes c
CROSS JOIN Productos p;
```

---

## Resultado

| Nombre | Producto |
|----------|----------|
| Juan | Laptop |
| Juan | Mouse |
| Ana | Laptop |
| Ana | Mouse |

Observa que:

```text
2 Clientes
×
2 Productos

=
4 filas
```

---

## Fórmula general

Si una tabla contiene:

```text
A filas
```

y la otra contiene:

```text
B filas
```

Entonces:

```text
Resultado = A × B
```

Ejemplo:

```text
100 clientes
×
50 productos

=
5000 filas
```

---

## Problema

Generar todas las combinaciones posibles entre clientes y productos.

### Datos

Tablas:

```text
Clientes
Productos
```

### Lógica

Cada cliente debe combinarse con cada producto.

### SQL

```sql
SELECT
    c.Nombre,
    p.Producto
FROM Clientes c
CROSS JOIN Productos p;
```

---

## Casos de uso reales

### Catálogo de promociones

```sql
SELECT
    c.IdCliente,
    p.IdProducto
FROM Clientes c
CROSS JOIN Productos p;
```

Caso:

```text
Generar ofertas potenciales para todos los clientes.
```

---

### Calendarios

Tabla:

```text
Fechas
```

Tabla:

```text
Sucursales
```

Consulta:

```sql
SELECT *
FROM Fechas
CROSS JOIN Sucursales;
```

Caso:

```text
Generar calendario completo por sucursal.
```

---

### Simulaciones financieras

```sql
SELECT *
FROM TasasInteres
CROSS JOIN EscenariosEconomicos;
```

Caso:

```text
Evaluar todas las combinaciones posibles.
```

---

### Data Warehousing

```sql
SELECT *
FROM DimFecha
CROSS JOIN DimProducto;
```

Caso:

```text
Construcción de matrices analíticas.
```

---

## Diferencia con INNER JOIN

### INNER JOIN

```sql
SELECT *
FROM Clientes c
INNER JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

Busca:

```text
Coincidencias.
```

---

### CROSS JOIN

```sql
SELECT *
FROM Clientes c
CROSS JOIN Cuentas cu;
```

Genera:

```text
Todas las combinaciones posibles.
```

---

## Diferencia visual

### INNER JOIN

```text
Juan → Cuenta 1
Ana  → Cuenta 2
```

Solo relaciones válidas.

---

### CROSS JOIN

```text
Juan → Cuenta 1
Juan → Cuenta 2
Juan → Cuenta 3

Ana → Cuenta 1
Ana → Cuenta 2
Ana → Cuenta 3
```

Todo con todo.

---

## Error común

❌ Incorrecto

```sql
SELECT *
FROM Clientes c
CROSS JOIN Cuentas cu
ON c.IdCliente = cu.IdCliente;
```

✔ Correcto

```sql
SELECT *
FROM Clientes c
CROSS JOIN Cuentas cu;
```

---

## ¿Por qué ocurre este error?

CROSS JOIN no utiliza:

```sql
ON
```

Porque no busca coincidencias.

Simplemente combina todos los registros.

---

## Error conceptual frecuente

Muchos principiantes creen que:

```sql
CROSS JOIN
```

es una forma alternativa de:

```sql
INNER JOIN
```

Incorrecto.

INNER JOIN:

```text
Busca coincidencias.
```

CROSS JOIN:

```text
Genera todas las combinaciones posibles.
```

---

## Riesgo importante

CROSS JOIN puede generar millones de filas accidentalmente.

Ejemplo:

```text
1000 clientes
×
1000 productos

=
1,000,000 filas
```

Por esta razón debe utilizarse cuidadosamente.

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar CROSS JOIN pregúntate:

1. ¿Realmente necesito todas las combinaciones?
2. ¿Cuántas filas tiene cada tabla?
3. ¿Cuántos registros generará el producto cartesiano?
4. ¿Existe una alternativa más eficiente?

### Relación entre conceptos

INNER JOIN responde:

> ¿Qué registros coinciden?

LEFT JOIN responde:

> ¿Qué registros existen en la izquierda?

RIGHT JOIN responde:

> ¿Qué registros existen en la derecha?

FULL JOIN responde:

> ¿Qué registros existen en cualquiera de las tablas?

SELF JOIN responde:

> ¿Qué registros se relacionan dentro de la misma tabla?

CROSS JOIN responde:

> ¿Qué ocurre si combino absolutamente todo con todo?

---

## Resumen

CROSS JOIN genera el producto cartesiano entre dos tablas.

Características principales:

- No utiliza ON.
- No busca coincidencias.
- Combina todas las filas posibles.
- Puede generar grandes volúmenes de datos.

Se utiliza para:

- Simulaciones.
- Calendarios.
- Matrices analíticas.
- Data Warehousing.
- Generación de escenarios.
- Ingeniería de Datos.

Debe utilizarse con precaución debido al crecimiento exponencial de registros.
