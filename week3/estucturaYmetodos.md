1. Análisis del dominio (StreamHub) y diseño de documentos:
Identifica colecciones necesarias (p. ej., usuarios, películas, series, valoraciones, listas).
Define la estructura JSON de cada documento (campos, arreglos, documentos anidados).

- estructuras

# inserts

users
{
  _id: ObjectId(),
  name: "Ana Torres",
  email: "ana@mail.com",
  age: 26,
  watchedCount: 8,
  watchlist: ["MOV001", "SER002"]
}

---
contents
{
  _id: ObjectId(),
  contentId: "MOV001",
  title: "Inception",
  type: "movie", // movie | series
  genre: ["Sci-Fi", "Action"],
  duration: 148,
  year: 2010
}

---

{
  _id: ObjectId(),
  userEmail: "ana@mail.com",
  contentId: "MOV001",
  rating: 5,
  comment: "Excelente",
  createdAt: new Date()
}

---

# finds

3. Consultas (Lectura) con operadores:
Realiza find() con filtros empleando $gt, $lt, $eq, $in, $and, $or, $regex.
Ejemplos sugeridos:
Películas con duración > 120 min
Usuarios que vieron > 5 contenidos

- Mayor que


Películas con duración > 120 min
```db.contents.find({ duration: { $gt: 120 } })```

Usuarios que vieron más de 5 contenidos
```db.users.find({ watchedCount: { $gt: 5 } })```

- Menor que

Películas de menos de 90 min
```db.contents.find({ duration: { $lt: 90 } })```

Usuarios menores de 30 años
```db.users.find({ age: { $lt: 30 } })```

- Igual a

Contenidos del tipo "movie"
```db.contents.find({ type: { $eq: "movie" } })```

Usuario con email específico
```db.users.find({ email: { $eq: "ana@mail.com" } })```

---

- Dentro de una lista

Contenidos de género Sci-Fi o Action
```db.contents.find({ genre: { $in: ["Sci-Fi", "Action"] } })```

Usuarios con contenidos específicos en su watchlist
```db.users.find({ watchlist: { $in: ["MOV001"] } })```

---

- Varias condiciones (todas deben cumplirse)

Películas largas y antiguas

```db.contents.find({
  $and: [
    { duration: { $gt: 120 } },
    { year: { $lt: 2015 } }
  ]
})

- Usuarios adultos con muchos contenidos vistos

db.users.find({
  $and: [
    { age: { $gt: 18 } },
    { watchedCount: { $gt: 5 } }
  ]
})

---


- Al menos una condición


Contenidos muy largos o muy cortos

db.contents.find({
  $or: [
    { duration: { $gt: 150 } },
    { duration: { $lt: 80 } }
  ]
})

Usuarios jóvenes o con muchos contenidos vistos

db.users.find({
  $or: [
    { age: { $lt: 25 } },
    { watchedCount: { $gt: 10 } }
  ]
})

- Búsqueda por texto
Títulos que contienen la palabra "toy"


db.contents.find({
  title: { $regex: "toy", $options: "i" }
})

Usuarios cuyo nombre empieza por "A"

db.users.find({
  name: { $regex: "^A", $options: "i" }
})


- COMBINADOS 
Películas Sci-Fi largas


db.contents.find({
  $and: [
    { genre: { $in: ["Sci-Fi"] } },
    { duration: { $gt: 120 } }
  ]
})

Usuarios con watchlist y muchos contenidos vistos


db.users.find({
  $and: [
    { watchlist: { $exists: true, $ne: [] } },
    { watchedCount: { $gt: 5 } }
  ]
})




---

# UPDATE Y DELETE 


4. Actualizaciones y eliminaciones:
Modifica información con updateOne()/updateMany() (p. ej., actualizar calificación de un contenido).
Elimina documentos con deleteOne()/deleteMany() cuando aplique.



Actualizar una calificación


db.ratings.updateOne(
  { userEmail: "ana@mail.com", contentId: "MOV001" },
  { $set: { rating: 4 } }
)


Eliminar valoraciones bajas


db.ratings.deleteMany({ rating: { $lt: 2 } })


5. Índices para performance:
Crea índices con createIndex() sobre campos consultados con frecuencia (p. ej., título, género).
Verifica índices existentes con getIndexes() y documenta tus decisiones.

---

- Crear índices


db.users.createIndex({ email: 1 }, { unique: true })
db.contents.createIndex({ title: 1 })
db.contents.createIndex({ genre: 1 })

Verificar índices
db.contents.getIndexes()

- Promedio de rating por contenido


db.ratings.aggregate([
  {
    $group: {
      _id: "$contentId",
      averageRating: { $avg: "$rating" },
      totalRatings: { $sum: 1 }
    }
  },
  { $sort: { averageRating: -1 } }
])

- Cantidad de valoraciones por género ($unwind)


db.ratings.aggregate([
  {
    $lookup: {
      from: "contents",
      localField: "contentId",
      foreignField: "contentId",
      as: "content"
    }
  },
  { $unwind: "$content" },
  { $unwind: "$content.genre" },
  {
    $group: {
      _id: "$content.genre",
      totalRatings: { $sum: 1 }
    }
  },
  { $sort: { totalRatings: -1 } }
])