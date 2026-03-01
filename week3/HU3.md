# Historia de Usuario – Semana 3
## Gestión de Contenido y Usuarios en MongoDB

---

## 🎯 Objetivo de la Historia de Usuario

Como usuario:

- Modelar e implementar en MongoDB colecciones para usuarios, contenido audiovisual y valoraciones, realizando operaciones CRUD, creando índices y ejecutando agregaciones para gestionar datos semiestructurados de forma eficiente y obtener reportes y métricas de uso.
- Aplicar conceptos de NoSQL y MongoDB CRUD:
  - `insertOne()` / `insertMany()`
  - `find()`
  - `updateOne()` / `updateMany()`
  - `deleteOne()` / `deleteMany()`
- Utilizar índices:
  - `createIndex()`
  - `getIndexes()`
- Ejecutar agregaciones con:
  - `aggregate()`
  - `$match`, `$group`, `$sort`, `$project`, `$unwind`
- Emplear operadores de consulta:
  - `$gt`, `$lt`, `$eq`, `$in`
  - `$and`, `$or`, `$regex`
  - Operadores lógicos y comparadores avanzados

---

## 📝 Descripción de las Tareas

### TASK 1 – Análisis del dominio y diseño de documentos

1. Análisis del dominio **StreamHub** y diseño de documentos:
   - Identificar las colecciones necesarias (por ejemplo: usuarios, películas, series, valoraciones, listas).
   - Definir la estructura JSON de cada documento (campos, arreglos y documentos anidados).

---

### TASK 2 – Inserción de datos

2. Inserción de datos:
   - Realizar la población inicial utilizando `insertOne()` y/o `insertMany()` en las colecciones definidas.
   - Incluir variedad de casos, como:
     - Películas con reseñas
     - Usuarios con historial de visualización

---

### TASK 3 – Consultas (Lectura) con operadores

3. Consultas con operadores:
   - Realizar consultas `find()` empleando los operadores:
     - `$gt`, `$lt`, `$eq`, `$in`, `$and`, `$or`, `$regex`

   **Ejemplos sugeridos:**
   - Películas con duración mayor a 120 minutos
   - Usuarios que hayan visto más de 5 contenidos

---

### TASK 4 – Actualizaciones y eliminaciones

4. Actualizaciones y eliminaciones:
   - Modificar información usando `updateOne()` y `updateMany()`  
     (por ejemplo, actualizar la calificación de un contenido).
   - Eliminar documentos utilizando `deleteOne()` y `deleteMany()` cuando aplique.

---

### TASK 5 – Índices para performance

5. Índices para rendimiento:
   - Crear índices con `createIndex()` sobre campos consultados con frecuencia  
     (por ejemplo: título, género).
   - Verificar los índices existentes con `getIndexes()`.
   - Documentar y justificar las decisiones tomadas en relación con los índices creados.

---

## ✅ Criterios de Aceptación

- Se definieron y documentaron correctamente las colecciones y los documentos para el dominio.
- Se poblaron datos utilizando `insertOne()` y `insertMany()` cubriendo casos variados.
- Existen consultas `find()` utilizando los operadores:
  - `$gt`, `$lt`, `$eq`, `$in`, `$and`, `$or`, `$regex`
  con resultados coherentes.
- Se ejecutaron correctamente operaciones `updateOne()`, `updateMany()`, `deleteOne()` y `deleteMany()`.
- Se crearon y verificaron índices usando `createIndex()` y `getIndexes()`, justificando su uso para mejorar el rendimiento.
- Se entregaron al menos **dos pipelines de agregación** utilizando:
  - `$match`, `$group`, `$sort`, `$project`, `$unwind`
  para la obtención de métricas solicitadas.

---

## 📦 Entrega

- Archivo comprimido en formato `.zip` que contenga:
  - Un archivo `.js` o `.txt` con **todos los comandos de MongoDB utilizados**:
    - Inserciones
    - Consultas
    - Actualizaciones
    - Eliminaciones
    - Índices
    - Agregaciones
  - Mínimo **dos consultas `aggregate()`** incluidas.
  - (Opcional) Capturas o exportaciones desde MongoDB Compass.
- Subir el archivo `.zip` a Moodle antes de la fecha de entrega.
