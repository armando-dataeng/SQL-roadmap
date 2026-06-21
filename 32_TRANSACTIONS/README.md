# TRANSACTIONS

## Definición

Una Transaction (Transacción) es una unidad lógica de trabajo que agrupa una o varias operaciones SQL.

Su objetivo es garantizar que todas las operaciones se ejecuten correctamente o que ninguna se aplique.

Principio fundamental:

```text
Todo o nada.
```

---

## Conceptos clave

Una transacción responde a la pregunta:

> ¿Cómo garantizo que mis datos permanezcan consistentes?

Ejemplo bancario:

Transferir:

```text
100 USD
```

desde:

```text
Cuenta A
```

hacia:

```text
Cuenta B
```

Si una operación falla:

```text
La transferencia completa debe cancelarse.
```

---

# Sintaxis básica

```sql
BEGIN TRANSACTION;

-- Operaciones

COMMIT;
```

---

## Ejemplo simple

```sql
BEGIN TRANSACTION;

UPDATE Cuentas
SET Saldo = Saldo - 100
WHERE IdCuenta = 1;

UPDATE Cuentas
SET Saldo = Saldo + 100
WHERE IdCuenta = 2;

COMMIT;
```

---

## ¿Qué hace?

Paso 1:

```text
Resta 100 a la Cuenta A
```

Paso 2:

```text
Suma 100 a la Cuenta B
```

Paso 3:

```text
Confirma los cambios
```

---

# COMMIT

## Definición

Confirma permanentemente los cambios realizados.

---

## Ejemplo

```sql
BEGIN TRANSACTION;

UPDATE Clientes
SET Nombre = 'Pedro'

COMMIT;
```

Después del COMMIT:

```text
Los cambios son permanentes.
```

---

# ROLLBACK

## Definición

Cancela la transacción.

Revierte todos los cambios realizados.

---

## Ejemplo

```sql
BEGIN TRANSACTION;

UPDATE Cuentas
SET Saldo = Saldo - 1000
WHERE IdCuenta = 1;

ROLLBACK;
```

Resultado:

```text
La actualización desaparece.
```

---

# Caso bancario real

## Problema

Transferir dinero entre cuentas.

### SQL

```sql
BEGIN TRANSACTION;

UPDATE Cuentas
SET Saldo = Saldo - 500
WHERE IdCuenta = 1;

UPDATE Cuentas
SET Saldo = Saldo + 500
WHERE IdCuenta = 2;

COMMIT;
```

---

## ¿Qué pasa si falla?

Supongamos:

```sql
UPDATE Cuentas
SET Saldo = Saldo + 500
WHERE IdCuenta = 999;
```

La cuenta no existe.

Entonces:

```sql
ROLLBACK;
```

Resultado:

```text
La cuenta origen recupera su dinero.
```

---

# TRY / CATCH

En SQL Server suele utilizarse:

```sql
BEGIN TRY
```

y

```sql
BEGIN CATCH
```

---

## Ejemplo profesional

```sql
BEGIN TRY

    BEGIN TRANSACTION;

    UPDATE Cuentas
    SET Saldo = Saldo - 500
    WHERE IdCuenta = 1;

    UPDATE Cuentas
    SET Saldo = Saldo + 500
    WHERE IdCuenta = 2;

    COMMIT;

END TRY

BEGIN CATCH

    ROLLBACK;

END CATCH;
```

---

# Propiedades ACID

Toda transacción debe cumplir:

```text
ACID
```

---

## Atomicity

```text
Todo o nada.
```

La transacción completa se ejecuta o se cancela.

---

## Consistency

```text
Los datos permanecen válidos.
```

---

## Isolation

```text
Las transacciones no interfieren entre sí.
```

---

## Durability

```text
Los cambios confirmados sobreviven a fallos.
```

---

# SAVEPOINT

## Definición

Permite crear puntos de restauración dentro de una transacción.

---

## Ejemplo

```sql
BEGIN TRANSACTION;

UPDATE Cuentas
SET Saldo = Saldo - 100;

SAVE TRANSACTION PuntoSeguro;

UPDATE Cuentas
SET Saldo = Saldo + 100;

ROLLBACK TRANSACTION PuntoSeguro;
```

---

## Resultado

SQL revierte únicamente hasta el punto guardado.

---

# Transacciones implícitas

Algunos motores pueden iniciar transacciones automáticamente.

Ejemplo:

```sql
UPDATE Clientes
SET Nombre = 'Ana';
```

SQL puede tratarlo como una transacción individual.

---

# Casos de uso reales

## Sistemas bancarios

Transferencias.

---

## Comercio electrónico

Pago de pedidos.

---

## ERP

Registro de facturas.

---

## Recursos Humanos

Pago de nómina.

---

## ETL

Carga de datos masiva.

---

# Bloqueos (Locks)

Las transacciones pueden generar:

```text
LOCKS
```

---

## ¿Por qué?

Para evitar:

```text
Lecturas incorrectas.
Actualizaciones simultáneas.
Pérdida de datos.
```

---

# Error común

❌ Incorrecto

```sql
UPDATE CuentaA;

UPDATE CuentaB;
```

Sin transacción.

---

✔ Correcto

```sql
BEGIN TRANSACTION;

UPDATE CuentaA;

UPDATE CuentaB;

COMMIT;
```

---

# Error conceptual frecuente

Muchos principiantes creen que:

```text
COMMIT guarda datos.
```

Realmente:

```text
COMMIT confirma una transacción.
```

No son exactamente lo mismo.

---

# Pensamiento de DBA

Antes de crear una transacción pregúntate:

1. ¿Qué ocurre si falla una operación?
2. ¿Puedo dejar datos inconsistentes?
3. ¿Necesito ROLLBACK?
4. ¿Qué tablas participan?
5. ¿La transacción será corta o larga?

---

# Relación con otros conceptos

```text
INDEXES         → Mejoran rendimiento
TRANSACTIONS    → Garantizan consistencia
TRIGGERS        → Automatizan acciones
PROCEDURES      → Ejecutan procesos
```

---

# Ejemplo completo

```sql
BEGIN TRY

    BEGIN TRANSACTION;

    UPDATE Cuentas
    SET Saldo = Saldo - 1000
    WHERE IdCuenta = 1;

    UPDATE Cuentas
    SET Saldo = Saldo + 1000
    WHERE IdCuenta = 2;

    COMMIT;

END TRY

BEGIN CATCH

    ROLLBACK;

END CATCH;
```

Este es uno de los ejemplos más representativos de una transacción bancaria.

---

# Resumen

Las transacciones permiten ejecutar múltiples operaciones como una única unidad lógica.

Comandos principales:

```sql
BEGIN TRANSACTION
COMMIT
ROLLBACK
SAVE TRANSACTION
```

Propiedades fundamentales:

```text
ACID
```

Son esenciales para:

- Bancos
- Fintech
- ERP
- CRM
- E-commerce
- Data Engineering
- DBA
- Sistemas críticos
