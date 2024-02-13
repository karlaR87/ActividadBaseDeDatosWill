-- Base en PHPMyAdmin
CREATE DATABASE ejemplo;
USE ejemplo;

-- Crear la tabla de empleados
CREATE TABLE empleados (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50),
    apellido VARCHAR(50),
    fecha_nacimiento DATE,
    sueldo DECIMAL(10, 2)
);
 
-- Crear la tabla de productos
CREATE TABLE productos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    precio DECIMAL(10, 2)
);

INSERT INTO `empleados` (`nombre`, `apellido`, `fecha_nacimiento`, `sueldo`) VALUES 
('Juan', 'Pérez', '1990-05-15', '2500.00'),
('María', 'García', '1985-09-20', '2800.00'),
('Pedro', 'López', '1993-02-10', '2200.00'),
('Ana', 'Martínez', '1988-11-30', '3000.00'),
('Luis', 'Rodríguez', '1995-07-25', '2600.00'),
('Laura', 'Fernández', '1983-04-12', '3200.00'),
('Carlos', 'Gómez', '1991-08-05', '2700.00'),
('Sara', 'Díaz', '1998-01-18', '2400.00'),
('Javier', 'Ruiz', '1980-12-07', '3500.00'),
('Elena', 'Sánchez', '1994-06-22', '2900.00'),
('Daniel', 'Gutiérrez', '1987-03-28', '2300.00'),
('Carmen', 'López', '1990-10-11', '3100.00'),
('Raúl', 'Martín', '1986-09-03', '2700.00'),
('Marta', 'Hernández', '1992-05-08', '2600.00'),
('Alejandro', 'Pérez', '1989-07-14', '3300.00'),
('Eva', 'González', '1997-04-01', '2700.00'),
('Alberto', 'Dominguez', '1984-11-19', '2800.00'),
('Nuria', 'Jiménez', '1993-08-26', '3100.00'),
('Roberto', 'Serrano', '1982-02-09', '2900.00'),
('Patricia', 'Ramírez', '1996-10-04', '3200.00');

INSERT INTO `productos` (`nombre`, `precio`) VALUES 
('Camisa', '25.99'),
('Pantalón', '39.99'),
('Zapatos', '49.99'),
('Bufanda', '12.50'),
('Gorra', '9.99'),
('Sudadera', '34.99'),
('Falda', '29.99'),
('Chaqueta', '59.99'),
('Sombrero', '14.99'),
('Calcetines', '6.99'),
('Pulsera', '8.50'),
('Collar', '18.99'),
('Anillo', '22.99'),
('Bolso', '45.99'),
('Cinturón', '19.99'),
('Gafas de sol', '27.50'),
('Reloj', '89.99'),
('Corbata', '15.99'),
('Vestido', '54.99'),
('lapiz', '25.99'),
('computadora', '25.99'),
('Lentes', '25.99'),
('Pendientes', '11.50');


-- Consultas para COUNT()
SELECT COUNT(*) 
FROM empleados

SELECT COUNT(*) 
FROM empleados WHERE sueldo= '2800.00'

SELECT precio, COUNT(*) 
FROM productos GROUP BY precio

SELECT precio, COUNT(*) 
FROM productos GROUP BY precio
HAVING precio = '25.99'

-- Consulta para SUM()
SELECT SUM(precio)
FROM productos

-- Consulta para AVG()

SELECT AVG(precio) AS promedio FROM productos;

-- Consulta para MIN()

SELECT MIN(precio)
FROM productos

-- Consulta para MAX()
SELECT MAX (sueldo) FROM empleados

-- Consultas de las Subconsultas

SELECT nombre 
FROM productos 
WHERE precio > (SELECT AVG(precio) FROM productos);

SELECT nombre, apellido 
FROM empleados 
WHERE sueldo IN (2000, 2500, 3000);

SELECT nombre 
FROM productos AS p WHERE EXISTS (SELECT 1 FROM empleados WHERE nombre IS NOT NULL);



BASE EN HEIDI
-- BASE DE DATOS PARA LOS JOIN


CREATE DATABASE ejemplo_join;
USE ejemplo_join;


CREATE TABLE clientes (
    id_cliente INT PRIMARY KEY,
    nombre VARCHAR(100)
);

CREATE TABLE pedidos (
    id_pedido INT PRIMARY KEY,
    id_cliente INT,
    producto VARCHAR(100),
    cantidad INT
);

INSERT INTO clientes (id_cliente, nombre) VALUES
(1, 'Juan'),
(2, 'María'),
(3, 'Pedro');

INSERT INTO pedidos (id_pedido, id_cliente, producto, cantidad) VALUES
(1, 1, 'Camiseta', 2),
(2, 2, 'Pantalón', 1),
(3, 1, 'Zapatos', 1);

INSERT INTO pedidos (id_pedido, producto, cantidad) VALUES
(4,'Camiseta', 2),

SELECT * FROM clientes;

SELECT clientes.nombre, pedidos.producto
FROM clientes
INNER JOIN pedidos ON clientes.id_cliente = pedidos.id_cliente;


--- LEFT JOIN 
SELECT clientes.nombre, pedidos.producto
FROM clientes
LEFT JOIN pedidos ON clientes.id_cliente = pedidos.id_cliente;


--- RIGHT JOIN
SELECT clientes.nombre, pedidos.producto
FROM clientes
RIGHT JOIN pedidos ON clientes.id_cliente = pedidos.id_cliente;


--- FULL JOIN
SELECT clientes.nombre, pedidos.producto
FROM clientes
LEFT JOIN pedidos ON clientes.id_cliente = pedidos.id_cliente
UNION
SELECT clientes.nombre, pedidos.producto
FROM clientes
RIGHT JOIN pedidos ON clientes.id_cliente = pedidos.id_cliente;
