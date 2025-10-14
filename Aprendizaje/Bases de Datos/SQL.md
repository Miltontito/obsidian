# DDL (Data Definition Language)
define y modifica la estructura de la BD:
- CREATE
- ALTER
- DROP
- TRUNCATE
# DML (Data Manipulation Language)
gestiona los datos dentro de la tabla:
- SELECT
- INSERT
- UPDATE
- DELETE
## JOIN
### INNER-JOIN
%% JOIN = INNER JOIN %%
```
SELECT tableA.column1,tableA.column2,tableB.column1,.... 
FROM tableA INNER JOIN tableB 
ON tableA.matching_column = tableB.matching_column;
```
![[SQL-Join.webp]]
Selecciona todas las FILAS de ambas tablas siempre que cumplan la condición, esto dará como resultado la combinación de toda las FILAS de ambas tablas donde la condición se cumpla.
### LEFT-JOIN
### RIGHT-JOIN
### FULL-JOIN


# DCL (Data Control Language)
controla permisos y accesos:
- GRANT
- REVOKE
# TCL (Transaccion Control Language)
controla transacciones
- COMMIT
- ROLLBACK
- SAVEPOINT