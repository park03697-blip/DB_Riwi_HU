# Historia de Usuario — Semana 1  
## Diseño Conceptual y Lógico de Base de Datos  
### (DER → Modelo Relacional)

---

## Objetivo de la Historia de Usuario

**Como** analista del Hospital *“Vida Sana”*,  
**quiero** diseñar una base de datos relacional normalizada  
**para** gestionar pacientes, médicos, citas y diagnósticos de forma consistente y sin duplicidades.

Se deben aplicar principios de modelado conceptual y lógico, incluyendo:

- Diagrama Entidad–Relación (DER)
- Modelo relacional
- Normalización hasta **Tercera Forma Normal (3FN)**

**No incluye:**

- Scripts SQL de creación
- Carga de datos
- Interfaz gráfica

---

## Descripción de las Tareas

### TASK 1 — Análisis y planificación del problema

- Comprender los requisitos del sistema a modelar.
- Definir las entidades principales, sus atributos y relaciones.
- Considerar desde el inicio las reglas de normalización para evitar retrabajo.

---

### TASK 2 — Diseño del modelo conceptual (DER)

- Diseñar el **Diagrama Entidad–Relación (DER)** aplicando normalización implícita.
- Identificar:
  - Claves primarias (PK)
  - Claves foráneas (FK)
  - Tipos de relaciones entre entidades

**Sugerencia:**  
Se puede utilizar *draw.io* y exportar el diagrama como imagen o PDF.

---

### TASK 3 — Conversión al modelo relacional

- Transformar el DER en un modelo relacional.
- Garantizar correspondencia directa con el diagrama conceptual.
- Especificar tipos de datos para cada campo de las tablas.
- Exportar el modelo en imagen o PDF.

---

### TASK 4 — Revisión de integridad y coherencia

- Verificar equivalencia entre el DER y el modelo relacional.
- Confirmar que la normalización se mantiene hasta **3FN** en ambos modelos.

---

### TASK 5 — Preparación y envío de la entrega

Preparar **dos archivos**:

1. DER (imagen o PDF)
2. Modelo relacional (imagen o PDF)

Condiciones:

- Ambos deben reflejar exactamente las mismas estructuras y relaciones.
- Nombrar los archivos claramente, por ejemplo:
  - `DER.pdf`
  - `ModeloRelacional.pdf`

---

## Criterios de Aceptación

- Se evidencia normalización hasta **3FN**.
- El DER define claramente:
  - Entidades
  - Relaciones
  - PK y FK
- El modelo relacional corresponde **1:1** con el DER.
- Se especifican tipos de datos en el modelo relacional.
- La equivalencia entre ambos modelos está verificada.

---
