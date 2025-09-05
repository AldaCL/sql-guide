## Teoría: ¿Cómo funcionan las subconsultas?

- Se utiliza una subconsulta cuando se necesita un valor (o conjunto de valores) que depende de otra tabla, o de un cálculo previo, usualmente para filtrar registros, generar condiciones, crear agregados o realizar comparaciones.
- Las subconsultas pueden ubicarse en distintas partes de una sentencia SQL, como en la cláusula `WHERE`, `HAVING`, `FROM` o incluso en la lista de selecciones (`SELECT`).[^2][^1]

**Tipos principales de subconsultas:**

- **Escalar:** Devuelve un único valor y puede usarse como un campo o en una condición.
- **De conjunto o tabla:** Devuelve varias filas y una o varias columnas, habitualmente utilizada con IN, EXISTS, ALL o ANY.
- **Correlacionada:** Se refiere a valores de la consulta exterior y se evalúa para cada fila del resultado exterior.[^3][^2]

***

## Ejemplos prácticos con Customer Orders (CO)

### 1. Subconsulta escalar en WHERE

**Ejemplo:** Obtener los productos cuyo precio sea igual al precio máximo registrado.

```sql
SELECT product_name, unit_price
FROM co.products
WHERE unit_price = (SELECT MAX(unit_price) FROM co.products);
```

- La subconsulta `(SELECT MAX(unit_price) FROM co.products)` obtiene el precio más alto, y el WHERE filtra los productos con ese precio.[^4][^1]

***

### 2. Subconsulta de conjunto en WHERE usando IN

**Ejemplo:** Listar clientes que han realizado al menos una orden.

```sql
SELECT full_name, email_address
FROM co.customers
WHERE customer_id IN (SELECT DISTINCT customer_id FROM co.orders);
```

- Aquí, la subconsulta retorna un conjunto de IDs de clientes que tienen pedidos en la tabla de órdenes.

***

### 3. Subconsulta correlacionada

**Ejemplo:** Listar productos que han sido pedidos más de una vez.

```sql
SELECT p.product_id, p.product_name
FROM co.products p
WHERE 1 < (SELECT COUNT(*) FROM co.order_items oi WHERE oi.product_id = p.product_id);
```

- La subconsulta cuenta cuántas veces aparece cada producto en los ítems de órdenes, y el resultado sólo incluye los productos pedidos más de una vez.

***

### 4. Subconsulta en SELECT

**Ejemplo:** Mostrar cada producto junto con el total de veces que ha sido incluido en órdenes.

```sql
SELECT 
  p.product_name,
  (SELECT COUNT(*) FROM co.order_items oi WHERE oi.product_id = p.product_id) AS total_ordenes
FROM co.products p;
```

- La subconsulta devuelve un conteo para cada fila de la tabla exterior.[^4][^2]

***

### 5. Subconsulta en FROM

**Ejemplo:** Listar clientes junto con el total gastado en todas sus órdenes.

```sql
SELECT c.full_name, t.total_gastado
FROM co.customers c
JOIN (
  SELECT o.customer_id, SUM(oi.quantity * oi.unit_price) AS total_gastado
  FROM co.orders o
  JOIN co.order_items oi ON o.order_id = oi.order_id
  GROUP BY o.customer_id
) t ON c.customer_id = t.customer_id;
```

- Aquí la subconsulta se trata como una tabla temporal que agrupa los gastos por cliente, y se usa en el JOIN exterior.[^1][^4]

***

## Recomendaciones para alumnos

- Usa subconsultas cuando no se puede realizar la consulta con un simple JOIN o cuando necesitas cálculos previos.
- Prefiere subconsultas escalares para condiciones, y de conjunto para listar varios elementos relacionados.
- Considera que las subconsultas correlacionadas pueden impactar el rendimiento porque se ejecutan por cada fila exterior.[^4][^1]

***

Estos ejemplos y explicaciones muestran cómo las subconsultas pueden facilitar la resolución de problemas complejos y análisis avanzados en SQL, usando de referencia el dataset CO (Customer Orders).[^2][^3][^4]
<span style="display:none">[^10][^11][^12][^13][^14][^15][^16][^17][^18][^19][^20][^5][^6][^7][^8][^9]</span>

<div style="text-align: center">⁂</div>

[^1]: https://josejuansanchez.org/bd/unidad-09-teoria/index.html

[^2]: https://www.geeksforgeeks.org/sql/sql-subquery/

[^3]: https://www.mywebstudies.com/post/oracle-sql/uso-subconsultas-sql

[^4]: https://learnsql.es/blog/practica-de-subconsultas-sql-15-ejercicios-con-soluciones/

[^5]: https://learnsql.es/blog/5-ejemplos-de-subconsultas-sql/

[^6]: https://learn.microsoft.com/es-es/sql/relational-databases/performance/subqueries?view=sql-server-ver17

[^7]: https://docs.aws.amazon.com/es_es/redshift/latest/dg/r_Subquery_examples.html

[^8]: https://www.srcodigofuente.es/subconsultas-en-sql

[^9]: https://dev.to/yugabyte/order-by-in-subquery-3hop

[^10]: https://translate.google.com/translate?u=https%3A%2F%2Fwww.devart.com%2Fdbforge%2Fsql%2Fstudio%2Fsql-subqueries-with-examples.html\&hl=es\&sl=en\&tl=es\&client=srp

[^11]: https://translate.google.com/translate?u=https%3A%2F%2Fwww.dataquest.io%2Fblog%2Fsql-subqueries-for-beginners%2F\&hl=es\&sl=en\&tl=es\&client=srp

[^12]: https://docs.vertica.com/11.1.x/en/data-analysis/queries/subqueries/subquery-examples/

[^13]: https://translate.google.com/translate?u=https%3A%2F%2Fwww.dbvis.com%2Fthetable%2Fthe-complete-guide-to-sql-subqueries%2F\&hl=es\&sl=en\&tl=es\&client=srp

[^14]: https://learn.microsoft.com/es-es/office/client-developer/access/desktop-database-reference/sql-subqueries-microsoft-access-sql

[^15]: https://mode.com/sql-tutorial/sql-sub-queries/

[^16]: https://translate.google.com/translate?u=https%3A%2F%2Fstackoverflow.com%2Fquestions%2F19897584%2Fwhich-customer-has-placed-most-orders-sql-query\&hl=es\&sl=en\&tl=es\&client=srp

[^17]: https://translate.google.com/translate?u=https%3A%2F%2Fmode.com%2Fsql-tutorial%2Fsql-sub-queries%2F\&hl=es\&sl=en\&tl=es\&client=srp

[^18]: https://stackoverflow.com/questions/6766481/order-by-inside-a-subquery

[^19]: https://translate.google.com/translate?u=https%3A%2F%2Fwww.w3resource.com%2Fsql-exercises%2Fsubqueries%2Findex.php\&hl=es\&sl=en\&tl=es\&client=srp

[^20]: https://www.ibm.com/docs/en/qmf/13.1.0?topic=ddfmtuss-creating-subquery-retrieve-data-from-more-than-one-table

