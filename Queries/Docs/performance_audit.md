📌 Índices en MongoDB: ¿Por qué mis consultas son lentas y cómo usar .explain("executionStats")?

Introducción

En MongoDB, los índices son fundamentales para mejorar el rendimiento de las consultas.
Sin índices, MongoDB debe recorrer toda la colección para encontrar documentos, lo que genera consultas lentas y alto consumo de recursos.

Tomando como base el siguiente esquema:

USERS
POSTS
LIKES

analizaremos:

Qué son los índices
Por qué las consultas son lentas
Qué índices necesita este modelo
Cómo usar .explain("executionStats")
Cómo interpretar resultados reales

✔︎ 1. ¿Qué es un índice en MongoDB?

Un índice es una estructura de datos que permite localizar documentos rápidamente sin escanear toda la colección.

Consulta sin índice
db.posts.find({
  author_id: ObjectId("123")
})

Sin índice, MongoDB hace:

COLLSCAN (Collection Scan)

Es decir:

Lee todos los documentos
Evalúa uno por uno
Filtra los que coinciden

Esto es muy costoso en colecciones grandes.

Consulta con índice
db.posts.createIndex({
  author_id: 1
})

Ahora MongoDB usa un B-Tree:

author_id -> referencias a documentos

La búsqueda se vuelve directa y mucho más rápida.

✔︎ 2. ¿Por qué las consultas son lentas?

Las consultas lentas generalmente ocurren por:

COLLSCAN
Falta de índices
Índices incorrectos
Ordenamientos en memoria
Demasiados documentos examinados
Índices compuestos mal diseñados
3. Análisis del esquema
USERS
_id
username
email
password_hash
avatar_url
bio
created_at
Consultas comunes

Buscar usuario por username:

db.users.findOne({
  username: "juan"
})

Buscar por email:

db.users.findOne({
  email: "juan@gmail.com"
})
Índices recomendados
db.users.createIndex(
  { username: 1 },
  { unique: true }
)

db.users.createIndex(
  { email: 1 },
  { unique: true }
)
POSTS

Campos importantes:

author_id
author_username
author_avatar_url
content
media_url
tags
editors
likes_count
created_at
Caso 1 — Obtener posts de un usuario

Consulta:

db.posts.find({
  author_id: userId
})

Sin índice:

MongoDB revisa todos los posts

Índice recomendado:

db.posts.createIndex({
  author_id: 1
})
Caso 2 — Timeline ordenado por fecha

Consulta:

db.posts.find({
  author_id: userId
})
.sort({
  created_at: -1
})
.limit(20)

Si solo existe:

{ author_id: 1 }

MongoDB:

Filtra documentos
Los guarda temporalmente
Ordena en memoria

Esto es costoso.

Índice correcto
db.posts.createIndex({
  author_id: 1,
  created_at: -1
})

Este índice permite:

Filtrar
Ordenar
Aplicar limit

sin operaciones extra.

Caso 3 — Feed global

Consulta:

db.posts.find()
.sort({
  created_at: -1
})
.limit(20)

Índice:

db.posts.createIndex({
  created_at: -1
})
Caso 4 — Búsqueda por tags

Consulta:

db.posts.find({
  tags: "mongodb"
})

Como tags es un array, MongoDB crea un:

Multikey Index

Índice:

db.posts.createIndex({
  tags: 1
})
LIKES

Campos:

post_id
user_id
created_at
Caso 5 — Likes de un post

Consulta:

db.likes.find({
  post_id
})

Índice:

db.likes.createIndex({
  post_id: 1
})
Caso 6 — Verificar si un usuario ya dio like

Consulta:

db.likes.findOne({
  post_id,
  user_id
})

Índice recomendado:

db.likes.createIndex(
  {
    post_id: 1,
    user_id: 1
  },
  {
    unique: true
  }
)
Beneficios
Evita likes duplicados

No permite:

mismo usuario + mismo post
Acelera búsquedas

MongoDB encuentra el documento directamente.

4. Cómo usar .explain("executionStats")

.explain() permite analizar cómo MongoDB ejecuta una consulta.

Ejemplo
db.posts.find({
  author_id: ObjectId("abc")
}).explain("executionStats")
Resultado típico SIN índice
{
  "queryPlanner": {
    "winningPlan": {
      "stage": "COLLSCAN"
    }
  },
  "executionStats": {
    "executionSuccess": true,
    "nReturned": 12,
    "executionTimeMillis": 1830,
    "totalKeysExamined": 0,
    "totalDocsExamined": 1500000
  }
}
Interpretación
COLLSCAN

MongoDB recorrió toda la colección.

Malo para performance.

totalDocsExamined
1500000

MongoDB revisó 1.5 millones de documentos.

totalKeysExamined
0

No utilizó índices.

executionTimeMillis
1830 ms

Consulta lenta.

Resultado CON índice

Creamos índice:

db.posts.createIndex({
  author_id: 1
})

Consulta nuevamente:

db.posts.find({
  author_id: ObjectId("abc")
}).explain("executionStats")
Resultado optimizado
{
  "queryPlanner": {
    "winningPlan": {
      "stage": "IXSCAN"
    }
  },
  "executionStats": {
    "executionSuccess": true,
    "nReturned": 12,
    "executionTimeMillis": 4,
    "totalKeysExamined": 12,
    "totalDocsExamined": 12
  }
}
5. Campos importantes en .explain()
A. winningPlan.stage
Malo
COLLSCAN
Bueno
IXSCAN

Significa:

Index Scan

MongoDB utilizó un índice.

B. totalDocsExamined

Debe ser cercano a:

nReturned

‼️ Ejemplo ideal:

nReturned: 20
totalDocsExamined: 20
C. SORT

Si aparece:

{
  "stage": "SORT"
}

MongoDB está ordenando en memoria.

Eso consume:

RAM
CPU
Tiempo
Ejemplo problemático
db.posts.find({
  author_id: userId
})
.sort({
  created_at: -1
})

Con índice:

{ author_id: 1 }

MongoDB no puede ordenar eficientemente.

Solución
db.posts.createIndex({
  author_id: 1,
  created_at: -1
})
D. totalKeysExamined

Cantidad de entradas del índice revisadas.

Idealmente debe ser pequeña.

6. El orden de los índices importa

Índice:

{
  author_id: 1,
  created_at: -1
}

Optimiza:

find({ author_id })
sort({ created_at: -1 })

Pero NO optimiza correctamente:

find({
  created_at: ...
})

Porque el índice comienza por:

author_id
Regla de oro

En índices compuestos:

los campos filtrados primero

Luego:

campos usados en sort

7. Índices finales recomendados
USERS
db.users.createIndex(
  { username: 1 },
  { unique: true }
)

db.users.createIndex(
  { email: 1 },
  { unique: true }
)
POSTS
db.posts.createIndex({
  author_id: 1,
  created_at: -1
})

db.posts.createIndex({
  created_at: -1
})

db.posts.createIndex({
  tags: 1
})
LIKES
db.likes.createIndex({
  post_id: 1
})

db.likes.createIndex(
  {
    post_id: 1,
    user_id: 1
  },
  {
    unique: true
  }
)
8. Flujo profesional de depuración

Cuando una consulta sea lenta:

Paso 1

Ejecutar:

.explain("executionStats")
Paso 2

Buscar:

COLLSCAN
SORT
docs examined muy altos
Paso 3

Diseñar índices basados en:

filtros (find)
ordenamientos (sort)
límites (limit)
Paso 4

Volver a ejecutar .explain()

Paso 5

Comparar métricas

Métrica	Antes	Después
executionTimeMillis	1800 ms	4 ms
totalDocsExamined	1.5M	12
stage	COLLSCAN	IXSCAN
Conclusión

Los índices son esenciales para escalar aplicaciones en MongoDB.

En este esquema:

POSTS es la colección crítica
LIKES necesita índices compuestos
Los sort() deben apoyarse en índices
.explain("executionStats") es la herramienta principal de diagnóstico

La diferencia entre:

COLLSCAN

y:

IXSCAN

puede significar pasar de:

2 segundos

a:

3 ms

en producción.
