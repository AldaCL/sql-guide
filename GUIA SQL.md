# Guía Práctica de Comandos SQL 

## Introducción

Esta guía cubre los comandos fundamentales de SQL en PostgreSQL, presenta ejemplos claros, buenas prácticas y diagramas visuales utilizando Mermaid para facilitar el aprendizaje de los distintos tipos de JOIN.

***

## Comandos Básicos

### SELECT

Consulta datos de una tabla.

```sql
SELECT columna1, columna2 FROM tabla WHERE condición;
```

**Ejemplo:**

```sql
SELECT nombre, edad FROM empleados WHERE edad >= 30;
```

> Es recomendable especificar solo las columnas necesarias y evitar `SELECT *` por cuestiones de rendimiento y claridad.[^1]

***

### INSERT

Inserta registros en una tabla.

```sql
INSERT INTO tabla (columna1, columna2) VALUES (valor1, valor2);
```

**Ejemplo:**

```sql
INSERT INTO empleados (nombre, edad) VALUES ('Ana', 28);
```

> Es buena práctica indicar siempre los campos en que se insertan los datos.[^2]

***

### UPDATE

Modifica registros existentes.

```sql
UPDATE tabla SET columna1 = valor1 WHERE condición;
```

**Ejemplo:**

```sql
UPDATE empleados SET edad = 29 WHERE nombre = 'Ana';
```

> Siempre utiliza `WHERE` para evitar modificar todos los registros inadvertidamente.[^1]

***

### DELETE

Elimina registros de una tabla.

```sql
DELETE FROM tabla WHERE condición;
```

**Ejemplo:**

```sql
DELETE FROM empleados WHERE nombre = 'Ana';
```

> Verifica la condición del WHERE antes de ejecutar el comando.[^2]

***

### CREATE TABLE

Crea una nueva tabla.

```sql
CREATE TABLE empleados (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100),
    edad INT
);
```

> Usa tipos de datos adecuados y define siempre la clave primaria (PRIMARY KEY).[^2]

***

### ALTER TABLE

Modifica la estructura de una tabla.

```sql
ALTER TABLE empleados ADD COLUMN salario NUMERIC;
```

> Haz respaldos antes de realizar cambios estructurales en tablas en producción.[^2]

***

### DROP TABLE

Elimina una tabla de la base de datos.

```sql
DROP TABLE empleados;
```

> Úsalo con precaución, ya que los datos se pierden permanentemente.[^2]

***

## Joins en SQL: Teoría y Diagramas

Los JOIN permiten combinar registros de dos o más tablas relacionadas.

### INNER JOIN

Devuelve solo los registros que tienen coincidencias en ambas tablas.

```sql
SELECT a.*, b.*
FROM tablaA a
INNER JOIN tablaB b ON a.id = b.id_a;
```


#### Diagrama Mermaid para INNER JOIN

```mermaid
venn
A[Tabla A] B[Tabla B]
A::B
```

> La intersección representa filas coincidentes.[^4][^5]

***

### LEFT JOIN

Devuelve todos los registros de la tabla izquierda y los que coinciden de la derecha; si no hay coincidencia, el resultado de la derecha es NULL.

```sql
SELECT a.*, b.*
FROM tablaA a
LEFT JOIN tablaB b ON a.id = b.id_a;
```


#### Diagrama Mermaid para LEFT JOIN

```mermaid
venn
A[Tabla A] B[Tabla B]
A
A::B
```


***

### RIGHT JOIN

Devuelve todos los registros de la tabla derecha y los que coinciden de la izquierda; si no hay coincidencia, el resultado de la izquierda es NULL.

```sql
SELECT a.*, b.*
FROM tablaA a
RIGHT JOIN tablaB b ON a.id = b.id_a;
```


#### Diagrama Mermaid para RIGHT JOIN

```mermaid
venn
A[Tabla A] B[Tabla B]
B
A::B
```


***

### FULL OUTER JOIN

Devuelve registros cuando hay una coincidencia en una de las tablas.

```sql
SELECT a.*, b.*
FROM tablaA a
FULL OUTER JOIN tablaB b ON a.id = b.id_a;
```


#### Diagrama Mermaid para FULL OUTER JOIN

```mermaid
venn
A[Tabla A] B[Tabla B]
A
B
A::B
```


***

## Buenas Prácticas

- **Usa sentencias preparadas** para prevenir inyección SQL y mejorar rendimiento.[^1]
- **Normaliza** tus tablas pero no sobre-normalices, busca un balance entre rendimiento y mantenibilidad.[^3]
- Utiliza **índices** en columnas que se consultan frecuentemente para mejorar la rapidez de búsquedas.
- Usa `VACUUM` y `ANALYZE` regularmente para el mantenimiento y optimización de la base de datos.[^6]
- Siempre realiza **respaldos** antes de modificaciones estructurales.
- Define nombres de columnas y tablas que sean claros y concisos.
- Limita el privilegio de las cuentas: El principio de menor privilegio refuerza la seguridad.[^7]

***

## Ejercicios Propuestos

1. Crear una tabla llamada `clientes` con campos id (PK), nombre y email.
2. Insertar tres registros a la tabla.
3. Consultar sólo los correos electrónicos de los clientes.
4. Realizar un JOIN sencillo entre clientes y una tabla de pedidos.

***

## Recursos para Diagramación

- Los diagramas Mermaid se pueden visualizar en editores compatibles, como VSCode o en https://mermaid.live.
- Usa bloques de código ```mermaid para integrarlos en Markdown fácilmente[^9][^12].

---

Esta guía puede ser utilizada como referencia rápida y práctica para estudiantes y profesionales que recién comienzan con PostgreSQL y SQL.
<span style="display:none">[^10][^11][^13][^14][^15][^16][^17][^18][^19][^20][^8]</span>

<div style="text-align: center">⁂</div>

[^1]: https://learnsql.es/blog/los-comandos-mas-comunes-de-postgresql-una-guia-para-principiantes/

[^2]: https://es.slideshare.net/slideshow/comandos-y-funciones-sql-postgres/36657726

[^3]: https://www.reddit.com/r/PostgreSQL/comments/1h0zt4u/postgresql_best_practices_guidelines/

[^4]: https://translate.google.com/translate?u=https%3A%2F%2Fwww.cybertec-postgresql.com%2Fen%2Fer-diagrams-with-sql-and-mermaid%2F\&hl=es\&sl=en\&tl=es\&client=srp

[^5]: http://mermaid.js.org/syntax/entityRelationshipDiagram.html

[^6]: https://www.enterprisedb.com/blog/vacuum-y-analyze-en-postgresql-consejos-basados-en-las-mejores-practicas

[^7]: https://www.datasunrise.com/es/centro-de-conocimiento/seguridad-en-postgresql/

[^8]: https://www.librebyte.net/base-de-datos/comandos-para-administrar-postgres/

[^9]: https://cloud.google.com/spanner/docs/psql-commands?hl=es-419

[^10]: https://www.todopostgresql.com/meta-commands-de-psql-mas-utilizados-en-postgresql/

[^11]: https://docs.aws.amazon.com/es_es/prescriptive-guidance/latest/postgresql-query-tuning/postgresql-query-tuning.pdf

[^12]: https://www.todopostgresql.com/comandos-de-transacciones-en-postgresql/

[^13]: https://dev.to/infrony/creando-diagramas-con-chatgpt-y-mermaid-js-4h6m

[^14]: https://kinsta.com/es/blog/postgres-listar-bases-de-datos/

[^15]: https://learnsql.es/blog/19-ejercicios-practicos-de-postgresql-con-soluciones-detalladas/

[^16]: https://www.um.es/geograf/sigmur/sigpdf/postgresql.pdf

[^17]: https://translate.google.com/translate?u=https%3A%2F%2Fdocs.mermaidchart.com%2Fmermaid-oss%2Fsyntax%2FentityRelationshipDiagram.html\&hl=es\&sl=en\&tl=es\&client=srp

[^18]: https://translate.google.com/translate?u=https%3A%2F%2Fmermaid.js.org%2Fintro%2Fsyntax-reference.html\&hl=es\&sl=en\&tl=es\&client=srp

[^19]: https://translate.google.com/translate?u=https%3A%2F%2Fstackoverflow.com%2Fquestions%2F65212332%2Fhow-to-render-a-mermaid-flowchart-dynamically\&hl=es\&sl=en\&tl=es\&client=srp

[^20]: https://es.linkedin.com/advice/0/what-best-practices-optimizing-postgresql-database-t90vc?lang=es\&lang=es

