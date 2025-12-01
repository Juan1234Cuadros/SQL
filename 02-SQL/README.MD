CREATE DATABASE base_data_empleados;

//2

\c base_data_empleados;
SELECT current_database();
\conninfo

//3

CREATE TABLE empleados (
id SERIAL PRIMARY KEY,
nombre VARCHAR(120) NOT NULL,
cargo VARCHAR(80),
salario NUMERIC(10,2),
fecha_ingreso DATE DEFAULT CURRENT_DATE,
activo BOOLEAN DEFAULT TRUE
);

CREATE TABLE departamentos (
id SERIAL PRIMARY KEY,
nombre VARCHAR(100) UNIQUE NOT NULL
);

CREATE TABLE asignaciones (
id SERIAL PRIMARY KEY,
empleado_id INT REFERENCES empleados(id),
departamento_id INT REFERENCES departamentos(id),
fecha_asignacion DATE DEFAULT CURRENT_DATE
);

//4

INSERT INTO empleados (nombre, cargo, salario, fecha_ingreso, activo) VALUES
('Pedro Mendoza', 'Gerente', 3500000, '2024-02-01', TRUE);

INSERT INTO empleados (nombre, cargo, salario) VALUES
('Laura Medina', 'Asistente', 1800000),
('Jorge Ruiz', 'Tecnico', 2200000),
('Sandra Torres', 'Analista', 2500000);

INSERT INTO departamentos (nombre) VALUES
('Contabilidad'),
('Sistemas'),
('Recursos Humanos');

INSERT INTO asignaciones (empleado_id, departamento_id) VALUES
(1, 1),
(2, 2),
(3, 2),
(4, 3);

//5

SELECT * FROM empleados;
SELECT nombre, cargo FROM empleados;
SELECT nombre, salario FROM empleados WHERE activo = TRUE;
SELECT COUNT(*) FROM empleados;
SELECT nombre, salario FROM empleados ORDER BY salario DESC;
SELECT * FROM empleados LIMIT 2;

//6

SELECT * FROM empleados WHERE nombre = 'Pedro Mendoza';
SELECT * FROM empleados WHERE cargo LIKE '%Analista%';
SELECT * FROM empleados WHERE fecha_ingreso > '2024-01-01';
SELECT * FROM empleados WHERE salario > 2000000;
SELECT * FROM empleados WHERE activo = TRUE AND salario > 2000000;
SELECT * FROM empleados WHERE nombre LIKE '%a%' OR nombre LIKE '%o%';
SELECT * FROM empleados WHERE nombre IN ('Laura Medina', 'Jorge Ruiz');
SELECT * FROM empleados WHERE nombre NOT LIKE '%Torres%';