Actividad SQL Integrada

1. Crea la base de datos 'barberia_db' y úsala.


2. Crea las tablas:

BARBEROS(id INT PK, nombre VARCHAR(80), salario DECIMAL(10,2), id_turno INT)

TURNOS(id_turno INT PK, nombre VARCHAR(80))



3. Inserta datos:
Turnos:
(1,'Mañana'),(2,'Tarde'),(3,'Noche')

Barberos:
(1,'Juan Cortés',1800,1)
(2,'Miguel Rojas',2400,2)
(3,'Pedro Salazar',1600,1)
(4,'Andrés Melo',2600,3)


4. Consulta barberos con salario > 2000 ordenados desc.


5. Muestra nombre del barbero, nombre del turno y salario.


6. Actualiza salario de los barberos del turno Tarde aumentando 12%.


7. Elimina barberos con salario < 1700.



Fin.


---

Código SQL

-- 1. Crear base de datos
CREATE DATABASE barberia_db;

-- (En DBeaver: clic derecho → Set Active)


---

-- 2. Crear tablas

CREATE TABLE TURNOS ( id_turno INT PRIMARY KEY, nombre VARCHAR(80) );

CREATE TABLE BARBEROS ( id INT PRIMARY KEY, nombre VARCHAR(80), salario NUMERIC(10,2), id_turno INT, FOREIGN KEY (id_turno) REFERENCES TURNOS(id_turno) );


---

-- 3. Insertar datos

INSERT INTO TURNOS (id_turno, nombre) VALUES (1, 'Mañana'), (2, 'Tarde'), (3, 'Noche');

INSERT INTO BARBEROS (id, nombre, salario, id_turno) VALUES (1, 'Juan Cortés', 1800, 1), (2, 'Miguel Rojas', 2400, 2), (3, 'Pedro Salazar', 1600, 1), (4, 'Andrés Melo', 2600, 3);


---

-- 4. Barberos con salario > 2000 ordenados desc

SELECT * FROM BARBEROS WHERE salario > 2000 ORDER BY salario DESC;


---

-- 5. Nombre del barbero + turno + salario

SELECT b.nombre AS barbero, t.nombre AS turno, b.salario FROM BARBEROS b JOIN TURNOS t ON b.id_turno = t.id_turno;


---

-- 6. Aumentar 12% salario del turno Tarde

UPDATE BARBEROS SET salario = salario * 1.12 WHERE id_turno = 2;


---

-- 7. Eliminar barberos con salario < 1700

DELETE FROM BARBEROS WHERE salario < 1700;