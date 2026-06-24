# SQL INJECTION

## Definición

SQL Injection (SQLi) es una vulnerabilidad de seguridad que ocurre cuando una aplicación construye consultas SQL utilizando datos proporcionados por el usuario sin validarlos o parametrizarlos correctamente.

Esto puede permitir que un atacante modifique el comportamiento esperado de una consulta y acceda o manipule información de forma no autorizada.

SQL Injection es una de las vulnerabilidades más conocidas en aplicaciones que interactúan con bases de datos.

---

# ¿Por qué ocurre?

Supongamos una aplicación con un formulario de inicio de sesión.

El usuario ingresa:

```text
Username

Password
```

---

La aplicación construye una consulta SQL.

Si los datos del usuario se concatenan directamente en la consulta, existe el riesgo de modificar su comportamiento.

---

La causa principal es:

```text
Construcción insegura
de consultas SQL.
```

---

# Concepto Fundamental

Nunca debemos construir consultas SQL concatenando texto proporcionado por el usuario.

La forma correcta consiste en utilizar:

```text
Prepared Statements

o

Parameterized Queries
```

---

# Arquitectura

```text
Usuario

↓

Aplicación

↓

Consulta SQL

↓

Base de Datos
```

---

La validación debe realizarse antes de que los datos lleguen al motor de base de datos.

---

# Código Vulnerable

Ejemplo (NO recomendado):

```sql
SELECT *
FROM Users
WHERE Username = '<valor ingresado por el usuario>';
```

---

Problema:

```text
La consulta depende
directamente
de la entrada del usuario.
```

---

# Código Seguro

Utilizar consultas parametrizadas.

Ejemplo conceptual:

```sql
SELECT *
FROM Users
WHERE Username = ?;
```

---

El valor del parámetro se envía por separado, evitando que altere la estructura de la consulta.

---

# Prepared Statements

Los Prepared Statements separan:

```text
Consulta SQL

↓

Datos del usuario
```

---

Beneficios:

- Mayor seguridad.
- Mejor rendimiento en consultas repetitivas.
- Código más mantenible.

---

# ORMs

Los Object-Relational Mappers (ORMs) suelen utilizar consultas parametrizadas por defecto.

Ejemplos:

```text
Entity Framework

Hibernate

SQLAlchemy

Django ORM
```

---

Aunque reducen el riesgo, es importante utilizarlos correctamente y evitar construir SQL dinámico de forma insegura.

---

# Medidas de Prevención

## Utilizar consultas parametrizadas

Siempre que sea posible.

---

## Validar entradas

Comprobar:

```text
Formato

Longitud

Tipo de dato

Valores permitidos
```

---

## Aplicar Least Privilege

La aplicación no debe conectarse utilizando un usuario administrador.

---

## Utilizar Roles

Asignar únicamente los permisos necesarios.

---

## Evitar SQL dinámico innecesario

Construir consultas dinámicas solo cuando sea imprescindible y de forma segura.

---

## Mantener el DBMS actualizado

Las actualizaciones incluyen mejoras de seguridad.

---

# Defensa en Capas

Una estrategia efectiva combina:

```text
Validación

↓

Prepared Statements

↓

Roles

↓

Least Privilege

↓

Auditoría

↓

Monitoreo
```

---

# Caso Real

Una aplicación web consulta la base de datos mediante un usuario con permisos de solo lectura.

Además:

- Utiliza Prepared Statements.
- Valida todas las entradas.
- Registra eventos mediante auditoría.
- Monitorea intentos sospechosos.

Resultado:

```text
Menor superficie
de ataque.
```

---

# Buenas Prácticas

## Utilizar consultas parametrizadas

Evitar concatenar datos del usuario.

---

## Validar entradas

Nunca confiar en la información recibida.

---

## Limitar permisos

Aplicar el principio de menor privilegio.

---

## Utilizar autenticación segura

Reducir el riesgo de acceso indebido.

---

## Registrar eventos

Facilitar investigaciones.

---

## Mantener dependencias actualizadas

Actualizar librerías y el DBMS.

---

# Error Común

Construir consultas mediante:

```text
Concatenación
de cadenas.
```

---

Resultado:

```text
Mayor riesgo

de SQL Injection.
```

---

# Error Conceptual Frecuente

Muchos creen:

```text
Escapar caracteres

↓

Es suficiente.
```

---

Incorrecto.

La mejor práctica consiste en utilizar:

```text
Prepared Statements

o

Parameterized Queries.
```

---

# Caso de Entrevista

Pregunta:

```text
¿Cómo prevenirías
una vulnerabilidad
de SQL Injection?
```

---

Respuesta:

```text
Utilizando consultas parametrizadas o Prepared Statements, validando las entradas del usuario, aplicando el principio de menor privilegio, evitando la construcción insegura de SQL dinámico y manteniendo el sistema actualizado.
```

---

# Pregunta de Entrevista Avanzada

Pregunta:

```text
¿Un ORM elimina
por completo
el riesgo
de SQL Injection?
```

---

Respuesta:

```text
No.

Los ORMs suelen utilizar consultas parametrizadas, pero si el desarrollador construye SQL dinámico de forma insegura o utiliza funciones que concatenan entradas del usuario, la vulnerabilidad puede seguir existiendo.
```

---

# Pensamiento de Seguridad

Antes de ejecutar una consulta pregúntate:

1. ¿Estoy utilizando consultas parametrizadas?
2. ¿Validé la entrada del usuario?
3. ¿La aplicación utiliza el principio de menor privilegio?
4. ¿Estoy evitando SQL dinámico innecesario?
5. ¿La consulta puede registrarse mediante auditoría?
6. ¿Cómo detectaré intentos sospechosos?
7. ¿El DBMS y las librerías están actualizados?

---

# Relación con los siguientes módulos

```text
DATABASE SECURITY
        ↓
SQL INJECTION
        ↓
HIGH AVAILABILITY
        ↓
REPLICATION
        ↓
DISASTER RECOVERY
```

---

# Resumen

SQL Injection es una vulnerabilidad que aparece cuando una aplicación construye consultas SQL utilizando entradas del usuario de forma insegura.

Conceptos principales:

- Consultas parametrizadas.
- Prepared Statements.
- Validación de entradas.
- Principio de menor privilegio.
- Roles y permisos.
- Auditoría.
- Monitoreo.

Buenas prácticas:

- Nunca concatenar entradas del usuario en consultas SQL.
- Utilizar siempre consultas parametrizadas.
- Validar los datos recibidos.
- Limitar los permisos de la aplicación.
- Mantener actualizado el software.

La mejor defensa contra SQL Injection consiste en combinar desarrollo seguro, control de accesos y una estrategia de seguridad en múltiples capas.
