9UHJIOKPLEJERCICIO INTEGRAL MYSQL – BARBERÍA

-- Crear BD
CREATE DATABASE barberia_db;
USE barberia_db;

-- Tablas
CREATE TABLE clientes(
id INT PRIMARY KEY AUTO_INCREMENT,
nombre VARCHAR(50),
telefono VARCHAR(20)
);

CREATE TABLE servicios(
id INT PRIMARY KEY AUTO_INCREMENT,
nombre VARCHAR(50),
precio DECIMAL(10,2)
);

CREATE TABLE barberos(
id INT PRIMARY KEY AUTO_INCREMENT,
nombre VARCHAR(50)
);

CREATE TABLE citas(
id INT PRIMARY KEY AUTO_INCREMENT,
cliente_id INT,
barbero_id INT,
servicio_id INT,
fecha DATE,
hora TIME,
FOREIGN KEY (cliente_id) REFERENCES clientes(id),
FOREIGN KEY (barbero_id) REFERENCES barberos(id),
FOREIGN KEY (servicio_id) REFERENCES servicios(id)
);

-- Inserts
INSERT INTO clientes(nombre,telefono) VALUES
('Juan Gómez','3001234567'),
('Carlos Ruiz','3019876543'),
('Miguel Torres','3025558899');

INSERT INTO servicios(nombre,precio) VALUES
('Corte de cabello',25000.00),
('Barba',18000.00),
('Corte + Barba',40000.00);

INSERT INTO barberos(nombre) VALUES
('Andrés'),
('Felipe'),
('Santiago');

INSERT INTO citas(cliente_id,barbero_id,servicio_id,fecha,hora) VALUES
(1,1,1,'2024-03-01','10:00:00'),
(1,2,2,'2024-03-01','10:30:00'),
(2,3,3,'2024-03-05','14:00:00'),
(3,1,1,'2024-03-06','09:00:00');

-- Consultas
SELECT * FROM citas;

SELECT c.nombre AS cliente, b.nombre AS barbero, s.nombre AS servicio, s.precio, fecha, hora
FROM citas ct
JOIN clientes c ON ct.cliente_id=c.id
JOIN barberos b ON ct.barbero_id=b.id
JOIN servicios s ON ct.servicio_id=s.id;

SELECT c.nombre, SUM(s.precio) AS total_gastado
FROM citas ct
JOIN clientes c ON ct.cliente_id=c.id
JOIN servicios s ON ct.servicio_id=s.id
GROUP BY c.id
ORDER BY total_gastado DESC;

UPDATE servicios SET precio=30000.00 WHERE id=1;

DELETE FROM citas WHERE id=2;