# TRIGGERS

## Definición

Un Trigger (Disparador) es un objeto de base de datos que se ejecuta automáticamente cuando ocurre un evento específico.

Los eventos más comunes son:

- INSERT
- UPDATE
- DELETE

A diferencia de un Stored Procedure:

```text
Stored Procedure → Se ejecuta manualmente.

Trigger → Se ejecuta automáticamente.
```

---

## Conceptos clave

Un Trigger responde a la pregunta:

> ¿Qué acción debe ejecutarse automáticamente cuando cambian los datos?

Características:

- Se ejecuta automáticamente.
- Está asociado a una tabla o vista.
- No requiere ejecución manual.
- Puede utilizarse para auditoría.
- Puede utilizarse para validaciones.
- Puede utilizarse para registrar cambios.

---

# Sintaxis

```sql
CREATE TRIGGER NombreTrigger
ON Tabla
AFTER INSERT
AS
BEGIN

    -- Código SQL

END;
```

---

# Eventos principales

## INSERT

Se ejecuta después de insertar registros.

```sql
AFTER INSERT
```

---

## UPDATE

Se ejecuta después de actualizar registros.

```sql
AFTER UPDATE
```

---

## DELETE

Se ejecuta después de eliminar registros.

```sql
AFTER DELETE
```

---

# Primer ejemplo

## Problema

Registrar cuando se crea un cliente.

### SQL

```sql
CREATE TRIGGER trg_NuevoCliente
ON Clientes
AFTER INSERT
AS
BEGIN

    PRINT 'Nuevo cliente registrado';

END;
```

---

## ¿Qué ocurre?

Si ejecutamos:

```sql
INSERT INTO Clientes
VALUES
(
    1,
    'Pedro',
    'Lopez'
);
```

SQL ejecutará automáticamente:

```text
Nuevo cliente registrado
```

---

# Trigger de Auditoría

## Problema

Guardar historial de clientes creados.

### Tabla de auditoría

```sql
CREATE TABLE AuditoriaClientes
(
    IdAuditoria INT IDENTITY(1,1),
    Fecha DATETIME,
    Accion VARCHAR(50)
);
```

---

### Trigger

```sql
CREATE TRIGGER trg_AuditoriaClientes
ON Clientes
AFTER INSERT
AS
BEGIN

    INSERT INTO AuditoriaClientes
    (
        Fecha,
        Accion
    )
    VALUES
    (
        GETDATE(),
        'INSERT'
    );

END;
```

---

## Resultado

Cada nuevo cliente generará un registro de auditoría.

---

# INSERTED y DELETED

SQL Server proporciona dos tablas virtuales.

```text
INSERTED
DELETED
```

---

## INSERTED

Contiene filas nuevas.

```sql
SELECT *
FROM INSERTED;
```

---

## DELETED

Contiene filas eliminadas.

```sql
SELECT *
FROM DELETED;
```

---

# Trigger de UPDATE

## Problema

Auditar cambios de saldo.

### SQL

```sql
CREATE TRIGGER trg_CambioSaldo
ON Cuentas
AFTER UPDATE
AS
BEGIN

    INSERT INTO AuditoriaCambios
    (
        FechaCambio
    )
    VALUES
    (
        GETDATE()
    );

END;
```

---

# Trigger de DELETE

## Problema

Registrar cuentas eliminadas.

### SQL

```sql
CREATE TRIGGER trg_EliminarCuenta
ON Cuentas
AFTER DELETE
AS
BEGIN

    PRINT 'Cuenta eliminada';

END;
```

---

# Caso bancario real

## Problema

Registrar todas las transacciones.

### SQL

```sql
CREATE TRIGGER trg_AuditoriaTransacciones
ON Transacciones
AFTER INSERT
AS
BEGIN

    INSERT INTO AuditoriaTransacciones
    (
        FechaEvento
    )
    VALUES
    (
        GETDATE()
    );

END;
```

---

# Trigger usando INSERTED

## SQL

```sql
CREATE TRIGGER trg_LogClientes
ON Clientes
AFTER INSERT
AS
BEGIN

    INSERT INTO LogClientes
    (
        IdCliente,
        FechaRegistro
    )
    SELECT
        IdCliente,
        GETDATE()
    FROM INSERTED;

END;
```

---

## ¿Qué ocurre?

Cada fila insertada se copia automáticamente al log.

---

# Casos de uso reales

## Auditoría

```sql
INSERT
UPDATE
DELETE
```

registrados automáticamente.

---

## Seguridad

Detectar modificaciones críticas.

---

## Cumplimiento normativo

Historial de cambios.

---

## Sistemas bancarios

Seguimiento de movimientos financieros.

---

## ETL

Control de calidad de datos.

---

# Modificar Trigger

```sql
ALTER TRIGGER trg_NuevoCliente
ON Clientes
AFTER INSERT
AS
BEGIN

    PRINT 'Cliente creado';

END;
```

---

# Eliminar Trigger

```sql
DROP TRIGGER trg_NuevoCliente;
```

---

# Error común

❌ Incorrecto

```sql
CREATE TRIGGER trg_Test
AFTER INSERT
AS
BEGIN

END;
```

---

✔ Correcto

```sql
CREATE TRIGGER trg_Test
ON Clientes
AFTER INSERT
AS
BEGIN

END;
```

---

# Error conceptual frecuente

Muchos principiantes creen que:

```text
Trigger = Stored Procedure
```

Incorrecto.

Stored Procedure:

```text
Se ejecuta manualmente.
```

Trigger:

```text
Se ejecuta automáticamente.
```

---

# Rendimiento

Los Triggers pueden afectar el rendimiento.

Cada:

```text
INSERT
UPDATE
DELETE
```

puede ejecutar lógica adicional.

Por esta razón:

```text
Deben utilizarse con moderación.
```

---

# Pensamiento de Ingeniería de Datos

Antes de crear un Trigger pregúntate:

1. ¿La acción debe ser automática?
2. ¿Puedo resolverlo mediante ETL?
3. ¿Existe impacto en rendimiento?
4. ¿Necesito auditoría?
5. ¿Necesito trazabilidad?

---

# Relación con otros conceptos

```text
VIEW               → Consulta reutilizable
FUNCTION           → Devuelve valores
STORED PROCEDURE   → Ejecuta lógica manualmente
TRIGGER            → Ejecuta lógica automáticamente
```

---

# Resumen

Los Triggers permiten ejecutar acciones automáticas cuando ocurren cambios en los datos.

Eventos principales:

```sql
INSERT
UPDATE
DELETE
```

Son ampliamente utilizados para:

- Auditoría
- Seguridad
- Trazabilidad
- Sistemas bancarios
- ERP
- CRM
- SQL Server
- Data Governance

Deben utilizarse cuidadosamente debido a su impacto potencial en el rendimiento.
