# DATABASE SECURITY

## Definición

Database Security es el conjunto de políticas, tecnologías y buenas prácticas utilizadas para proteger una base de datos contra accesos no autorizados, pérdida de información, modificaciones indebidas y ataques informáticos.

Su objetivo es garantizar la:

```text
Confidencialidad

Integridad

Disponibilidad
```

de los datos.

---

# ¿Por qué existe?

Las bases de datos almacenan información crítica como:

```text
Clientes

Pagos

Contraseñas

Información médica

Datos financieros

Propiedad intelectual
```

---

Pregunta:

```text
¿Qué ocurre
si un atacante
accede a la base
de datos?
```

---

Consecuencias:

```text
Robo de información

Fraude

Pérdidas económicas

Sanciones legales

Daño reputacional
```

---

La solución es:

```text
Database Security.
```

---

# Principios Fundamentales

Toda estrategia de seguridad debe proteger:

```text
Confidencialidad

↓

Solo usuarios autorizados.

----------------------------

Integridad

↓

Los datos no deben alterarse
sin autorización.

----------------------------

Disponibilidad

↓

La información debe estar
disponible cuando se necesite.
```

---

Estos tres principios forman la:

```text
CIA Triad
```

---

# Capas de Seguridad

```text
Usuarios

↓

Roles

↓

Permisos

↓

Autenticación

↓

Base de Datos

↓

Backups

↓

Auditoría

↓

Monitoreo
```

---

La seguridad nunca depende de una sola medida.

---

# Autenticación

Permite verificar:

```text
¿Quién eres?
```

---

Ejemplos:

- Usuario y contraseña.
- Active Directory.
- LDAP.
- OAuth.
- Certificados.
- Autenticación Multifactor (MFA).

---

# Autorización

Después de autenticarse se responde:

```text
¿Qué puedes hacer?
```

---

Ejemplos:

```text
SELECT

INSERT

UPDATE

DELETE

EXECUTE
```

---

La autorización normalmente se implementa mediante:

```text
Roles

Permisos

GRANT

REVOKE
```

---

# Cifrado (Encryption)

Los datos pueden cifrarse:

## En tránsito

Cuando viajan por la red.

Ejemplo:

```text
TLS / SSL
```

---

## En reposo

Cuando están almacenados.

Ejemplo:

```text
Transparent Data Encryption (TDE)
```

---

## En Backups

Las copias también deben cifrarse.

---

# Protección contra SQL Injection

Nunca construir consultas concatenando texto.

Incorrecto:

```sql
SELECT *
FROM Users
WHERE Username = '" + username + "';
```

---

Correcto:

```sql
SELECT *
FROM Users
WHERE Username = ?;
```

---

Utilizar:

```text
Consultas Parametrizadas
```

o

```text
Prepared Statements
```

---

# Principio de Menor Privilegio

Cada usuario debe tener:

```text
Solo

los permisos

necesarios.
```

---

Nunca utilizar:

```text
Administrador

para aplicaciones.
```

---

# Segmentación

Separar usuarios según su función.

Ejemplo:

```text
DBA

Developer

Analyst

Application

ETL
```

---

Cada uno con permisos específicos.

---

# Seguridad Física

La seguridad también incluye:

```text
Centros de datos

Acceso físico

Servidores

Alimentación eléctrica

Red
```

---

# Auditoría

Registrar eventos como:

```text
Logins

Cambios

Permisos

Consultas críticas

DDL

DML
```

---

Permite detectar:

```text
Actividad sospechosa.
```

---

# Gestión de Contraseñas

Buenas prácticas:

- Contraseñas fuertes.
- Rotación periódica.
- MFA cuando sea posible.
- Nunca compartir credenciales.

---

# Actualizaciones

Mantener el DBMS actualizado.

Las actualizaciones corrigen:

```text
Vulnerabilidades

Errores

Problemas de seguridad
```

---

# Caso Real

Empresa Financiera.

Medidas implementadas:

```text
MFA

TLS

TDE

Roles

Auditoría

Backups cifrados

Monitoreo
```

---

Resultado:

```text
Arquitectura segura.
```

---

# Amenazas Comunes

## SQL Injection

---

## Robo de credenciales

---

## Privilegios excesivos

---

## Malware

---

## Ransomware

---

## Acceso interno no autorizado

---

## Exposición de Backups

---

# Buenas Prácticas

## Aplicar Least Privilege

Siempre.

---

## Utilizar Roles

Evitar permisos individuales.

---

## Cifrar conexiones

TLS / SSL.

---

## Cifrar Backups

Nunca almacenarlos sin protección.

---

## Habilitar Auditoría

Registrar eventos críticos.

---

## Actualizar el DBMS

Aplicar parches de seguridad.

---

## Revisar permisos periódicamente

Eliminar accesos innecesarios.

---

## Proteger cuentas administrativas

Preferiblemente con MFA.

---

# Error Común

Utilizar:

```text
Usuario administrador

↓

Para todas las aplicaciones.
```

---

Resultado:

```text
Mayor riesgo

↓

Mayor impacto
ante un incidente.
```

---

# Error Conceptual Frecuente

Muchos creen:

```text
Seguridad

=

Contraseña fuerte.
```

---

Incorrecto.

La seguridad incluye:

```text
Usuarios

Roles

Permisos

Backups

Auditoría

Cifrado

Monitoreo

Actualizaciones
```

---

# Caso de Entrevista

Pregunta:

```text
¿Cuáles son
los principios básicos
de la seguridad
en bases de datos?
```

---

Respuesta:

```text
La seguridad en bases de datos se basa en proteger la confidencialidad, integridad y disponibilidad de la información mediante autenticación, autorización, cifrado, auditoría, control de accesos, copias de seguridad y monitoreo continuo.
```

---

# Pregunta de Entrevista Avanzada

Pregunta:

```text
¿Cómo protegerías
una base de datos
en producción?
```

---

Respuesta:

```text
Aplicaría el principio de menor privilegio, utilizaría roles, habilitaría auditoría, cifraría las conexiones y los datos almacenados, implementaría autenticación multifactor para cuentas administrativas, automatizaría los Backups, mantendría el DBMS actualizado y monitorearía continuamente la actividad del sistema.
```

---

# Pensamiento de un DBA

Antes de poner una base de datos en producción pregúntate:

1. ¿Quién tendrá acceso?
2. ¿Los permisos son mínimos?
3. ¿Las conexiones están cifradas?
4. ¿Los Backups están protegidos?
5. ¿La auditoría está habilitada?
6. ¿Existe monitoreo?
7. ¿Cómo responderé ante un incidente de seguridad?

---

# Relación con los siguientes módulos

```text
AUDITING
        ↓
DATABASE SECURITY
        ↓
HIGH AVAILABILITY
        ↓
REPLICATION
        ↓
DISASTER RECOVERY
```

---

# Resumen

Database Security reúne las prácticas necesarias para proteger una base de datos frente a amenazas internas y externas.

Conceptos principales:

- CIA Triad.
- Autenticación.
- Autorización.
- Roles y permisos.
- Cifrado.
- SQL Injection.
- Auditoría.
- Backups.
- Monitoreo.
- Actualizaciones.

Una estrategia de seguridad efectiva combina múltiples capas de protección para garantizar que los datos permanezcan confidenciales, íntegros y disponibles incluso frente a incidentes o ataques.
