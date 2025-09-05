
# Guía Práctica SQL: Dataset CO (Customer Orders)

## Tablas y Significado

| Tabla | Descripción breve |
| :-- | :-- |
| CUSTOMERS | Información de los clientes: id, email y nombre completo. |
| INVENTORY | Almacena cantidades de productos en las tiendas: inventario, tienda, producto, cantidad disponible. |
| ORDERS | Órdenes realizadas por clientes: id, fecha, referencia a cliente y tienda, estado. |
| ORDER_ITEMS | Detalle de productos en cada orden: cada ítem de orden, producto, cantidad, precio unitario, envío. |
| PRODUCTS | Lista de productos: id, nombre, precio, detalles y metadatos de imágenes. |
| SHIPMENTS | Envíos realizados: id, tienda, cliente, dirección y estado del envío. |
| STORES | Información sobre las tiendas: id, nombre, dirección, lat/long, imagen y detalles. |


***

## Consultas Básicas para Explorar los Datos

1. **Ver todos los clientes**

```sql
SELECT * FROM co.customers;
```

2. **Ver productos con su precio**

```sql
SELECT product_id, product_name, unit_price FROM co.products;
```

3. **Ver los pedidos realizados con fechas**

```sql
SELECT order_id, customer_id, order_tms FROM co.orders;
```

4. **Ver la cantidad de productos en inventario por tienda**

```sql
SELECT store_id, product_id, product_inventory FROM co.inventory;
```

5. **Ver los detalles de los envíos**

```sql
SELECT shipment_id, store_id, customer_id, delivery_address, shipment_status FROM co.shipments;
```


***

## Preguntas y Ejercicios para Estudiantes

### 1. ¿Cuántos clientes hay registrados?

**Respuesta:**

```sql
SELECT ... 
```


### 2. Lista el nombre y correo de todos los clientes que existen.

**Respuesta:**

```sql
SELECT ...
```


### 3. ¿Cuántos productos diferentes están dados de alta?

**Respuesta:**

```sql
SELECT ...
```


### 4. ¿Cuántos pedidos ha realizado cada cliente?

**Respuesta:**

```sql
SELECT ...
```


### 5. Nombre y dirección de las tiendas que tienen más de un producto distinto en inventario.

**Respuesta:**

```sql
SELECT ... 
```


### 6. Detalles de todos los productos incluidos en la orden con id = 1.

**Respuesta:**

```sql
SELECT ...

```


### 7. ¿Cuántos envíos tienen estado 'DELIVERED'?

**Respuesta:**

```sql
SELECT  ....
```


### 8. Para cada orden, muestra el nombre del cliente, la fecha y el total gastado en productos.

**Respuesta:**

```sql
SELECT  ...
```


### 9. Lista los productos que están agotados (inventario = 0) en cualquier tienda.

**Respuesta:**

```sql
SELECT  ...
```


***


<div style="text-align: center">⁂</div>

[^1]: https://www.youtube.com/watch?v=TXVLofytIgw

[^2]: https://www.youtube.com/watch?v=41hkAqJ82d8

[^3]: https://docs.oracle.com/es-ww/iaas/nosql-database/doc/table-design.html

[^4]: https://www.mywebstudies.com/post/oracle-dba/tablas-y-vistas-del-diccionario-de-datos-en-oracle

[^5]: https://interpolados.wordpress.com/2017/11/24/estructura-de-la-base-de-datos-oracle/

[^6]: https://www.youtube.com/watch?v=Gx3_Ri428cw

[^7]: https://experienceleague.adobe.com/es/docs/commerce-business-intelligence/mbi/analyze/warehouse-manager/table-relationships

[^8]: https://www.youtube.com/watch?v=PtYJgupJ7uE

[^9]: https://translate.google.com/translate?u=https%3A%2F%2Fdocs.oracle.com%2Fcd%2FE19078-01%2Fmysql%2Fmysql-refman-5.0%2Finformation-schema.html\&hl=es\&sl=en\&tl=es\&client=srp

[^10]: https://support.microsoft.com/es-es/office/relaciones-entre-tablas-en-un-modelo-de-datos-533dc2b6-9288-4363-9538-8ea6e469112b

[^11]: https://www.scribd.com/document/351184660/Manual-Oracle-Crear-Tablas

[^12]: https://www.campusmvp.es/recursos/post/Fundamentos-de-SQL-Consultas-SELECT-multi-tabla-Tipos-de-JOIN.aspx

[^13]: https://translate.google.com/translate?u=https%3A%2F%2Fwww.oracle.com%2Fdatabase%2F\&hl=es\&sl=en\&tl=es\&client=srp

[^14]: https://blog.comparasoftware.com/que-es-tabla-en-base-de-datos/

[^15]: https://docs.oracle.com/cloud/help/es/analytics-cloud/ACUBI/ACUBI.pdf

[^16]: https://translate.google.com/translate?u=https%3A%2F%2Fwww.databasestar.com%2Foracle-live-sql%2F\&hl=es\&sl=en\&tl=es\&client=srp

[^17]: https://cursos.virtual.uniandes.edu.co/isis2304/wp-content/uploads/sites/137/2017/08/tutorial_general_sqlloader.pdf

[^18]: https://docs.oracle.com/es/applications/jd-edwards/cross-product/9.2/eoaag/forms-used-to-review-sales-order-information.html

[^19]: https://docs.oracle.com/es/learn/db23ai-sql-features/index.html

[^20]: https://www.youtube.com/watch?v=tawZmX6KM4c

