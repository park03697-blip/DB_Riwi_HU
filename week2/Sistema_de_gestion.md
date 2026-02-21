# Sistema Académico en SQL
Base de Datos: gestion_academica_universidad

---

## TASK 1. Crear la base de datos y tablas

### 1. Crear la base de datos

```sql
CREATE DATABASE gestion_academica_universidad;
USE gestion_academica_universidad;


2. Tabla estudiantes
CREATE TABLE estudiantes (
    id_estudiante INT AUTO_INCREMENT PRIMARY KEY,
    nombre_completo VARCHAR(100) NOT NULL,
    correo_electronico VARCHAR(100) UNIQUE NOT NULL,
    genero VARCHAR(10),
    identificacion VARCHAR(20) UNIQUE NOT NULL,
    carrera VARCHAR(100) NOT NULL,
    fecha_nacimiento DATE NOT NULL,
    fecha_ingreso DATE NOT NULL
);

3. Tabla docentes
CREATE TABLE docentes (
    id_docente INT AUTO_INCREMENT PRIMARY KEY,
    nombre_completo VARCHAR(100) NOT NULL,
    correo_institucional VARCHAR(100) UNIQUE NOT NULL,
    departamento_academico VARCHAR(100) NOT NULL,
    anios_experiencia INT
);

4. Tabla cursos
CREATE TABLE cursos (
    id_curso INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    codigo VARCHAR(20) UNIQUE NOT NULL,
    creditos INT,
    semestre INT,
    id_docente INT,
    FOREIGN KEY (id_docente) REFERENCES docentes(id_docente)
);


5. Tabla inscripciones
CREATE TABLE inscripciones (
    id_inscripcion INT AUTO_INCREMENT PRIMARY KEY,
    id_estudiante INT,
    id_curso INT,
    fecha_inscripcion DATE NOT NULL,
    calificacion_final DECIMAL(4,2),
    
    FOREIGN KEY (id_estudiante) REFERENCES estudiantes(id_estudiante),
    FOREIGN KEY (id_curso) REFERENCES cursos(id_curso)
);



TASK 2. Insertar datos


Insertar estudiantes
INSERT INTO estudiantes 
(nombre_completo, correo_electronico, genero, identificacion, carrera, fecha_nacimiento, fecha_ingreso)
VALUES
('Ana Perez','ana@mail.com','F','1001','Ingenieria','2000-05-10','2023-01-15'),
('Luis Gomez','luis@mail.com','M','1002','Derecho','1999-02-20','2022-08-10'),
('Maria Ruiz','maria@mail.com','F','1003','Medicina','2001-03-12','2023-01-20'),
('Carlos Lopez','carlos@mail.com','M','1004','Ingenieria','1998-11-25','2021-02-01'),
('Sofia Torres','sofia@mail.com','F','1005','Arquitectura','2000-09-05','2023-02-10');



Insertar docentes
INSERT INTO docentes 
(nombre_completo, correo_institucional, departamento_academico, anios_experiencia)
VALUES
('Dr. Ramirez','ramirez@uni.edu','Ingenieria',10),
('Dra. Morales','morales@uni.edu','Salud',7),
('Prof. Castillo','castillo@uni.edu','Derecho',4);



Insertar cursos
INSERT INTO cursos (nombre, codigo, creditos, semestre, id_docente)
VALUES
('Base de Datos','BD101',4,3,1),
('Programacion','PR201',5,2,1),
('Anatomia','AN301',4,4,2),
('Derecho Civil','DC401',3,1,3);



Insertar inscripciones
INSERT INTO inscripciones 
(id_estudiante, id_curso, fecha_inscripcion, calificacion_final)
VALUES
(1,1,'2024-01-10',4.5),
(1,2,'2024-01-10',3.8),
(2,4,'2024-01-12',4.2),
(3,3,'2024-01-15',4.7),
(4,1,'2024-01-16',3.9),
(5,2,'2024-01-18',4.0),
(2,1,'2024-01-20',3.5),
(3,1,'2024-01-22',4.8);




TASK 3. Consultas


Listar estudiantes con cursos
SELECT e.nombre_completo, c.nombre AS curso, i.calificacion_final
FROM inscripciones i
JOIN estudiantes e ON i.id_estudiante = e.id_estudiante
JOIN cursos c ON i.id_curso = c.id_curso;


Cursos con docentes con más de 5 años de experiencia
SELECT c.nombre, d.nombre_completo
FROM cursos c
JOIN docentes d ON c.id_docente = d.id_docente
WHERE d.anios_experiencia > 5;
Promedio de notas por curso
SELECT c.nombre, AVG(i.calificacion_final) AS promedio
FROM inscripciones i
JOIN cursos c ON i.id_curso = c.id_curso
GROUP BY c.nombre;
Estudiantes inscritos en más de un curso
SELECT e.nombre_completo, COUNT(*) AS total_cursos
FROM inscripciones i
JOIN estudiantes e ON i.id_estudiante = e.id_estudiante
GROUP BY e.nombre_completo
HAVING COUNT(*) > 1;


Agregar columna a estudiantes
ALTER TABLE estudiantes
ADD estado_academico VARCHAR(20);



Eliminar un docente
DELETE FROM docentes WHERE id_docente = 3;


Cursos con más de 2 estudiantes
SELECT c.nombre, COUNT(*) AS inscritos
FROM inscripciones i
JOIN cursos c ON i.id_curso = c.id_curso
GROUP BY c.nombre
HAVING COUNT(*) > 2;


TASK 4. Subconsultas y funciones


Estudiantes con promedio mayor al general
SELECT e.nombre_completo
FROM estudiantes e
JOIN inscripciones i ON e.id_estudiante = i.id_estudiante
GROUP BY e.id_estudiante
HAVING AVG(i.calificacion_final) >
(
  SELECT AVG(calificacion_final) FROM inscripciones
);


Carreras con estudiantes en cursos semestre mayor o igual a 2
SELECT DISTINCT carrera
FROM estudiantes
WHERE id_estudiante IN (
  SELECT id_estudiante
  FROM inscripciones i
  JOIN cursos c ON i.id_curso = c.id_curso
  WHERE c.semestre >= 2
);


Indicadores generales
SELECT 
ROUND(AVG(calificacion_final),2) AS promedio,
SUM(calificacion_final) AS total,
MAX(calificacion_final) AS maximo,
MIN(calificacion_final) AS minimo,
COUNT(*) AS total_notas
FROM inscripciones;