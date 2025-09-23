# CREAR-BASE-DE-DATOS-
INSTRUCCIONES PARA CREAR BASE DE DATOS

1)CREAR BASE DE DATOS:   create database nombre; base

2)LISTAR BASE DE DATOS: show database;

3)TRABAJAR EN LA BASE DE DATOS:  use nombre;

4)CREAR TABLA: 
	CREATE TABLE usuarios (
	IDusuarios INT PRIMARY KEY AUTO_INCREMENT,
	nombre VARCHAR(100),
	correo_Electtronico VARCHAR(100) UNIQUE,
	Fecha_Registro DATE
);

- RELACION ENTRE TABLAS

1) CREATE TABLE pedidos(
	ID INT PRIMARY KEY AUTO_INCREMENT,
	ID_Usuario INT,
	Producto varchar(100),
	fecha_pedido DATE,
	FOREIGN KEY (ID_usuario) REFERENCES usuarios(IDusuarios)
);

- TRAER DATOS DE LA TABLA        
select * from usuarios where id >2;

- PARA EDITAR DATOS DE LA TABLA, ESTE ES EL CÓDIGO EJEMPLO:
ALTER TABLE `tienda`.`usuarios` 
ADD COLUMN `apellido` VARCHAR(100) NULL AFTER `nombre`,
CHANGE COLUMN `id` `idusuario` INT NOT NULL AUTO_INCREMENT ,
CHANGE COLUMN `correo_electronico` `email` VARCHAR(100) NULL DEFAULT NULL ,      (VARCHAR(100), EL 100 ES EL LIMITE DE CARACTERES)
CHANGE COLUMN `fecha_registro` `telefono` VARCHAR(20) NULL DEFAULT NULL ,        (VARCHAR(20), EL 20 ES EL LIMITE DE CARACTERES)
ADD UNIQUE INDEX `correo_electronico_UNIQUE` (`email` ASC) VISIBLE;
;

- O SI UNO QUIERE EDITAR LOS DATOS SIN CODIGO, DA CLIC DERECHO Y LUEGO "ALTER SCHEMA"

- PARA INSERTAR INFORMACION DENTRO DE LOS VALORES DE LA TABLA:
insert into idpedido (fecha,valor,idseguimiento,idusuario) 
values ("2025-09-22","45000",1,3);

- PARA ACTUALIZAR LA INFORMACION DE LOS VALORES DE LA TABLA

update pedidos set idusuario = 5 where idpedido = 3


-PARA ORDENAR LOS DATOS EN ORDEN DESCENDENTE (de mayor a menor), limit 100 es que solamente nos muestra 100 productos

SELECT * FROM classicmodels.products order by buyprice desc limit 100;

- PARA CONTAR CUANTOS CLIENTES HAY DE LA CIUDAD DE NANTES:
select count(*) from customers where city = "Nantes";

- FILTROS CON LIKE E IN (filtrar clientes que su nombre comience por la)

select * from customers where customerName like "la%" 

- FILTROS CON LIKE E IN (filtrar todos clientes que tengan la)
select * from customers where customerName like "%la%"

-PRODUCTOS CON CIERTOS IDS:

select * from customers where customerNumber in (110,111,112,113); (clientes cib
select * from customers where customerNumber not in (110,111,112,113);

- 
select * from orders between "2003-01-10" "2003-02-10";
select * from orders where orderDate between "2003-01-10" and "2003-02-10";
select * from orders where shippedDate between "2003-01-10" and "2003-02-10";
select * from orders where shippedDate > "2003-01-10" and shippedDate < "2003-02-10";
select * from orders where shippedDate >= "2003-01-10" and shippedDate < "2003-02-10";
select count(*) from orders where shippedDate >= "2003-01-10" and shippedDate < "2003-02-10";

- Siempre que queramos buscar info de una tabla, poner por ejemplo "select * from orderdetails;" para que el programa pueda buscar los datos en esa tabla, y luego:
select orderNumber, sum(quantityOrdered) from orderdetails group by orderNumber; (para 
select orderNumber, sum(quantityOrdered * priceEach) from orderdetails group by orderNumber; (para multiplicar cantidad por el precio)

select * from classicmodels.products;
select productLine, count(productCode) from classicmodels.products group by productLine;

-PARA SABER CUÁNTOS PRODUCTOS HAY DE CADA UNO:
select * from products;
select productLine, count(productCode) from classicmodels.products group by productLine;

-PARA CONTAR CUANTOS EMPLEADOS HAY SEGÚN EL CÓDIGO DE LA OFICINA:
select * from employees;
select officeCode, count(employeeNumber) from classicmodels.employees group by officeCode;

-PARA SABER CUANTOS CLIENTES HAY POR CIUDAD, DE MAYOR A MENOR:
select city, count(customerNumber) as clientes from classicmodels.customers group by city order by clientes desc;

-PARA SABER CUANTOS CLIENTES HAY POR CIUDAD, DE MENOR A MAYOR:
select city, count(customerNumber) as clientes from classicmodels.customers group by city order by clientes asc;

-PARA SABER CUANTOS CLIENTES HAY EN CADA CIUDAD QUE COMIENCE POR N O POR CUALQUIER LETRA:
select city, count(customerNumber) as clientes from classicmodels.customers where city like "n%" group by city order by clientes desc;

-BUSCAR PRODUCTOS CON PRECIO MAYOR AL PROMEDIO:
select productName, productLine
from classicmodels.products
 where buyPrice > (select avg(buyPrice) from products); 

-BUSCAR CLIENTES CON AL MENOS UN PEDIDO:
select* from customers where customerNumber in (select customerNumber from orders)

select * from customers 
where customerNumber in (select customerNumber from orders where orderDate between "2003-01-10" and "2003-03-10");
select customerNumber from orders where orderDate between "2003-01-10" and "2003-03-10";

-PARA UNIR COLUMNAS EN UNA SOLAM DE DIFERENTES TABLAS
select customerName from customers
union
select firstName from employees

-PARA UNIR DOS TABLAS EN UNA SOLA
select * from orderdetails od 
inner join orders o 
on od.orderNumber;

-
select od.orderNumber, p.productName, od.quantityOrdered, od.priceEach, p.buyPrice, (od.quantityOrdered * od.priceEach) as total, o.orderDate, o.status
from orderdetails od
inner join orders o
on od.orderNumber = o.orderNumber
inner join products p
on p.productCode = od.productCode
where od.orderNumber = 10100

-
select * from customers c
left join orders o
on c.customerNumber = o.customerNumber;

select c.customerName, o.orderDate from customers c
left join orders o
on c.customerNumber = o.customerNumber;

select c.customerName, o.orderDate from customers c
right join orders o
on c.customerNumber = o.customerNumber;

select * from orderdetails od
inner join orders o
on od.orderNumber = o.orderNumber

select count(*) from customers c
right join orders o
on c.customerNumber = o.customerNumber;

-NOS MUESTRA CUANTOS CLIENTES HAY AUNQUE NO TENGAN ORDENES
select count(*) from customers c
left join orders o
on c.customerNumber = o.customerNumber;

-PARA MOSTRAR LOS CLIENTES CON EL VENDEDOR ASIGNADO:
select c.customerName, c.contactLastName, e.firstName, e.lastName, j.firstName, j.lastName, j.jobTitle from customers c
inner join employees e
on e.employeeNumber = c.salesRepEmployeeNumber
inner join employees j
on j.employeeNumber = e.reportsTo;
