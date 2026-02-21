# Historia de Usuario  
## Diseño y Consulta de un Sistema Académico en SQL

---

## Objetivo de la Historia de Usuario

**Como** usuario de una institución académica,  
**quiero** diseñar e implementar una base de datos académica  
**para** gestionar estudiantes, docentes, cursos e inscripciones y analizar el rendimiento de forma confiable.

### Alcance

Se debe:

- Crear la base de datos **gestion_academica_universidad**.
- Definir tablas con restricciones:
  - NOT NULL
  - UNIQUE
  - FOREIGN KEY
  - CHECK
- Insertar datos de ejemplo.
- Ejecutar consultas con:
  - JOIN
  - GROUP BY
  - AVG
  - HAVING
- Aplicar:
  - ALTER TABLE
  - ON DELETE
- Construir una vista.
- Gestionar permisos y transacciones:
  - GRANT / REVOKE
  - BEGIN / SAVEPOINT / ROLLBACK / COMMIT

---

## Descripción de las Tareas

---

### TASK 1 — Diseño inicial y creación de la base de datos

1. Crear la base de datos:

2. Diseñar las tablas con campos mínimos:

#### Tabla: estudiantes

- id_estudiante (PK, autoincremental)
- nombre_completo
- correo_electronico
- genero
- identificacion (UNIQUE)
- carrera
- fecha_nacimiento
- fecha_ingreso

---

#### Tabla: docentes

- id_docente (PK, autoincremental)
- nombre_completo
- correo_institucional
- departamento_academico
- anios_experiencia

---

#### Tabla: cursos

- id_curso (PK, autoincremental)
- nombre
- codigo (UNIQUE)
- creditos
- semestre
- id_docente (FK)

---

#### Tabla: inscripciones

- id_inscripcion (PK, autoincremental)
- id_estudiante (FK)
- id_curso (FK)
- fecha_inscripcion
- calificacion_final

---

Aplicar restricciones:

- NOT NULL
- UNIQUE
- FOREIGN KEY
- CHECK

---

### TASK 2 — Inserción de datos

- Insertar al menos:
- 5 estudiantes
- 3 docentes
- 4 cursos
- Crear:
- 8 inscripciones distribuidas entre estudiantes y cursos.

---

### TASK 3 — Consultas básicas y manipulación

Realizar consultas que permitan:

- Listar estudiantes con sus cursos e inscripciones (JOIN).
- Mostrar cursos dictados por docentes con más de 5 años de experiencia.
- Obtener promedio de calificaciones por curso (GROUP BY + AVG).
- Mostrar estudiantes inscritos en más de un curso (HAVING COUNT > 1).
- Usar ALTER TABLE para agregar la columna:


- Eliminar un docente y analizar el efecto en cursos (ON DELETE).
- Consultar cursos con más de 2 estudiantes inscritos.

---

### TASK 4 — Subconsultas y funciones

Realizar consultas con:

- Estudiantes cuyo promedio sea mayor al promedio general.
- Carreras con estudiantes en cursos de semestre ≥ 2.
- Uso de funciones:
- ROUND
- SUM
- MAX
- MIN
- COUNT

---

### TASK 5 — Creación de una vista

Crear la vista:


Debe mostrar:

- Nombre del estudiante
- Nombre del curso
- Nombre del docente
- Semestre
- Calificación final

---

### TASK 6 — Control de acceso y transacciones

Configurar:

#### Permisos

- Otorgar permisos de solo lectura a:
sobre la vista.

- Revocar permisos de modificación en inscripciones.

---

#### Transacciones

Simular actualización de calificaciones usando:

- BEGIN
- SAVEPOINT
- ROLLBACK
- COMMIT

---

## Criterios de Aceptación

- Base de datos creada correctamente.
- Tablas definidas con PK, FK y restricciones.
- Datos mínimos insertados:
- 5 estudiantes
- 3 docentes
- 4 cursos
- 8 inscripciones
- Consultas evidencian uso de:
- JOIN
- GROUP BY
- AVG
- HAVING
- ALTER TABLE
- ON DELETE
- Subconsultas y funciones entregan resultados correctos.
- Vista creada con los campos requeridos.
- Permisos y transacciones configurados correctamente.

---
