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

RELACION ENTRE TABLAS

1) CREATE TABLE pedidos(
	ID INT PRIMARY KEY AUTO_INCREMENT,
	ID_Usuario INT,
	Producto varchar(100),
	fecha_pedido DATE,
	FOREIGN KEY (ID_usuario) REFERENCES usuarios(IDusuarios)
);

TRAER DATOS DE LA TABLA        
select * from usuarios where id >2;

PARA EDITAR DATOS DE LA TABLA, ESTE ES EL CÓDIGO EJEMPLO:
ALTER TABLE `tienda`.`usuarios` 
ADD COLUMN `apellido` VARCHAR(100) NULL AFTER `nombre`,
CHANGE COLUMN `id` `idusuario` INT NOT NULL AUTO_INCREMENT ,
CHANGE COLUMN `correo_electronico` `email` VARCHAR(100) NULL DEFAULT NULL ,      (VARCHAR(100), EL 100 ES EL LIMITE DE CARACTERES)
CHANGE COLUMN `fecha_registro` `telefono` VARCHAR(20) NULL DEFAULT NULL ,        (VARCHAR(20), EL 20 ES EL LIMITE DE CARACTERES)
ADD UNIQUE INDEX `correo_electronico_UNIQUE` (`email` ASC) VISIBLE;
;

O SI UNO QUIERE EDITAR LOS DATOS SIN CODIGO, DA CLIC DERECHO Y LUEGO "ALTER SCHEMA"

PARA INSERTAR INFORMACION DENTRO DE LOS VALORES DE LA TABLA:
insert into idpedido (fecha,valor,idseguimiento,idusuario) 
values ("2025-09-22","45000",1,3);

PARA ACTUALIZAR LA INFORMACION DE LOS VALORES DE LA TABLA

update pedidos set idusuario = 5 where idpedido = 3


PARA ORDENAR LOS DATOS EN ORDEN DESCENDENTE (de mayor a menor), limit 100 es que solamente nos muestra 100 productos

SELECT * FROM classicmodels.products order by buyprice desc limit 100;
