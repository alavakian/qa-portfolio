# Test Cases — JSONPlaceholder API

**Proyecto:** JSONPlaceholder API  
**Tester:** Alexis Avakian  
**Fecha:** Junio 2026  
**Herramienta:** Postman  
**URL base:** https://jsonplaceholder.typicode.com

---

## Módulo 1: Posts — GET

---

### TC-001 — Obtener todos los posts

| Campo | Detalle |
|---|---|
| **ID** | TC-001 |
| **Módulo** | Posts |
| **Método** | GET |
| **Endpoint** | `/posts` |
| **Prioridad** | Alta |

**Request:**
```
GET https://jsonplaceholder.typicode.com/posts
```

**Resultado esperado:**
- Status code: `200 OK`
- El cuerpo de la respuesta contiene un array de 100 posts
- Cada post contiene los campos: `id`, `userId`, `title`, `body`

**Resultado obtenido:** ✅ PASS  
Status `200 OK`. Array de 100 objetos con la estructura correcta.

---

### TC-002 — Obtener un post por ID válido

| Campo | Detalle |
|---|---|
| **ID** | TC-002 |
| **Módulo** | Posts |
| **Método** | GET |
| **Endpoint** | `/posts/{id}` |
| **Prioridad** | Alta |

**Request:**
```
GET https://jsonplaceholder.typicode.com/posts/1
```

**Resultado esperado:**
- Status code: `200 OK`
- El cuerpo contiene un objeto con `id: 1`, `userId`, `title` y `body`

**Resultado obtenido:** ✅ PASS  
Status `200 OK`. Objeto con `id: 1` y todos los campos esperados.

---

### TC-003 — Obtener un post con ID inexistente

| Campo | Detalle |
|---|---|
| **ID** | TC-003 |
| **Módulo** | Posts |
| **Método** | GET |
| **Endpoint** | `/posts/{id}` |
| **Prioridad** | Alta |
| **Tipo** | Negativo |

**Request:**
```
GET https://jsonplaceholder.typicode.com/posts/9999
```

**Resultado esperado:**
- Status code: `404 Not Found`
- El cuerpo indica que el recurso no existe

**Resultado obtenido:** ✅ PASS  
Status `404 Not Found`. Cuerpo: `{}`

---

### TC-004 — Obtener comentarios de un post

| Campo | Detalle |
|---|---|
| **ID** | TC-004 |
| **Módulo** | Posts / Comments |
| **Método** | GET |
| **Endpoint** | `/posts/{id}/comments` |
| **Prioridad** | Media |

**Request:**
```
GET https://jsonplaceholder.typicode.com/posts/1/comments
```

**Resultado esperado:**
- Status code: `200 OK`
- Array de comentarios asociados al post 1
- Cada comentario contiene: `id`, `postId`, `name`, `email`, `body`

**Resultado obtenido:** ✅ PASS  
Status `200 OK`. 5 comentarios con estructura correcta.

---

### TC-005 — Obtener comentarios de un post inexistente

| Campo | Detalle |
|---|---|
| **ID** | TC-005 |
| **Módulo** | Posts / Comments |
| **Método** | GET |
| **Endpoint** | `/posts/{id}/comments` |
| **Prioridad** | Media |
| **Tipo** | Negativo |

**Request:**
```
GET https://jsonplaceholder.typicode.com/posts/9999/comments
```

**Resultado esperado:**
- Status code: `404 Not Found` o array vacío con indicación clara

**Resultado obtenido:** ⚠️ OBSERVACIÓN  
Status `200 OK` con array vacío `[]`. El sistema no distingue entre un post sin comentarios y un post inexistente. Ver **OBS-001**.

---

## Módulo 2: Posts — POST

---

### TC-006 — Crear un nuevo post con datos válidos

| Campo | Detalle |
|---|---|
| **ID** | TC-006 |
| **Módulo** | Posts |
| **Método** | POST |
| **Endpoint** | `/posts` |
| **Prioridad** | Alta |

**Request:**
```
POST https://jsonplaceholder.typicode.com/posts
Content-Type: application/json

{
  "title": "Mi primer post de prueba",
  "body": "Este es el contenido del post creado durante testing manual.",
  "userId": 1
}
```

**Resultado esperado:**
- Status code: `201 Created`
- El cuerpo contiene el objeto creado con un `id` asignado

**Resultado obtenido:** ✅ PASS  
Status `201 Created`. Respuesta incluye `id: 101` y los campos enviados.

---

### TC-007 — Crear un post sin campos obligatorios

| Campo | Detalle |
|---|---|
| **ID** | TC-007 |
| **Módulo** | Posts |
| **Método** | POST |
| **Endpoint** | `/posts` |
| **Prioridad** | Alta |
| **Tipo** | Negativo |

**Request:**
```
POST https://jsonplaceholder.typicode.com/posts
Content-Type: application/json

{}
```

**Resultado esperado:**
- Status code: `400 Bad Request`
- Mensaje de error indicando los campos requeridos

**Resultado obtenido:** ❌ FAIL  
Status `201 Created` con body `{ "id": 101 }`. La API acepta posts vacíos sin validación. Ver **BUG-001**.

---

### TC-008 — Crear un post con userId inválido

| Campo | Detalle |
|---|---|
| **ID** | TC-008 |
| **Módulo** | Posts |
| **Método** | POST |
| **Endpoint** | `/posts` |
| **Prioridad** | Media |
| **Tipo** | Negativo |

**Request:**
```
POST https://jsonplaceholder.typicode.com/posts
Content-Type: application/json

{
  "title": "Test",
  "body": "Contenido",
  "userId": 9999
}
```

**Resultado esperado:**
- Status code: `400 Bad Request` o `404 Not Found`
- La API debería validar que el userId exista

**Resultado obtenido:** ⚠️ OBSERVACIÓN  
Status `201 Created`. La API no valida la existencia del userId. Ver **OBS-002**.

---

## Módulo 3: Posts — PUT

---

### TC-009 — Actualizar un post existente

| Campo | Detalle |
|---|---|
| **ID** | TC-009 |
| **Módulo** | Posts |
| **Método** | PUT |
| **Endpoint** | `/posts/{id}` |
| **Prioridad** | Alta |

**Request:**
```
PUT https://jsonplaceholder.typicode.com/posts/1
Content-Type: application/json

{
  "id": 1,
  "title": "Título actualizado",
  "body": "Contenido actualizado durante testing.",
  "userId": 1
}
```

**Resultado esperado:**
- Status code: `200 OK`
- El cuerpo refleja los datos actualizados

**Resultado obtenido:** ✅ PASS  
Status `200 OK`. Respuesta contiene los datos enviados con `id: 1`.

---

### TC-010 — Actualizar un post inexistente

| Campo | Detalle |
|---|---|
| **ID** | TC-010 |
| **Módulo** | Posts |
| **Método** | PUT |
| **Endpoint** | `/posts/{id}` |
| **Prioridad** | Media |
| **Tipo** | Negativo |

**Request:**
```
PUT https://jsonplaceholder.typicode.com/posts/9999
Content-Type: application/json

{
  "title": "Test",
  "body": "Test",
  "userId": 1
}
```

**Resultado esperado:**
- Status code: `404 Not Found`

**Resultado obtenido:** ✅ PASS  
Status `404 Not Found`.

---

## Módulo 4: Posts — DELETE

---

### TC-011 — Eliminar un post existente

| Campo | Detalle |
|---|---|
| **ID** | TC-011 |
| **Módulo** | Posts |
| **Método** | DELETE |
| **Endpoint** | `/posts/{id}` |
| **Prioridad** | Alta |

**Request:**
```
DELETE https://jsonplaceholder.typicode.com/posts/1
```

**Resultado esperado:**
- Status code: `200 OK`
- Cuerpo vacío o confirmación de eliminación

**Resultado obtenido:** ✅ PASS  
Status `200 OK`. Cuerpo: `{}`

---

### TC-012 — Eliminar un post inexistente

| Campo | Detalle |
|---|---|
| **ID** | TC-012 |
| **Módulo** | Posts |
| **Método** | DELETE |
| **Endpoint** | `/posts/{id}` |
| **Prioridad** | Media |
| **Tipo** | Negativo |

**Request:**
```
DELETE https://jsonplaceholder.typicode.com/posts/9999
```

**Resultado esperado:**
- Status code: `404 Not Found`

**Resultado obtenido:** ✅ PASS  
Status `404 Not Found`.

---

## Módulo 5: Users — GET

---

### TC-013 — Obtener todos los usuarios

| Campo | Detalle |
|---|---|
| **ID** | TC-013 |
| **Módulo** | Users |
| **Método** | GET |
| **Endpoint** | `/users` |
| **Prioridad** | Media |

**Request:**
```
GET https://jsonplaceholder.typicode.com/users
```

**Resultado esperado:**
- Status code: `200 OK`
- Array de 10 usuarios con campos: `id`, `name`, `username`, `email`, `address`, `phone`, `website`, `company`

**Resultado obtenido:** ✅ PASS  
Status `200 OK`. 10 usuarios con estructura completa.

---

### TC-014 — Obtener un usuario por ID válido

| Campo | Detalle |
|---|---|
| **ID** | TC-014 |
| **Módulo** | Users |
| **Método** | GET |
| **Endpoint** | `/users/{id}` |
| **Prioridad** | Media |

**Request:**
```
GET https://jsonplaceholder.typicode.com/users/1
```

**Resultado esperado:**
- Status code: `200 OK`
- Objeto con datos completos del usuario 1

**Resultado obtenido:** ✅ PASS  
Status `200 OK`. Datos completos del usuario con `id: 1`.

---

### TC-015 — Obtener un usuario con ID inexistente

| Campo | Detalle |
|---|---|
| **ID** | TC-015 |
| **Módulo** | Users |
| **Método** | GET |
| **Endpoint** | `/users/{id}` |
| **Prioridad** | Media |
| **Tipo** | Negativo |

**Request:**
```
GET https://jsonplaceholder.typicode.com/users/9999
```

**Resultado esperado:**
- Status code: `404 Not Found`

**Resultado obtenido:** ✅ PASS  
Status `404 Not Found`. Cuerpo: `{}`

---

## Resumen de Ejecución

| ID | Endpoint | Método | Descripción | Estado |
|---|---|---|---|---|
| TC-001 | /posts | GET | Obtener todos los posts | ✅ PASS |
| TC-002 | /posts/1 | GET | Obtener post por ID válido | ✅ PASS |
| TC-003 | /posts/9999 | GET | Post con ID inexistente | ✅ PASS |
| TC-004 | /posts/1/comments | GET | Comentarios de un post | ✅ PASS |
| TC-005 | /posts/9999/comments | GET | Comentarios de post inexistente | ⚠️ OBS |
| TC-006 | /posts | POST | Crear post con datos válidos | ✅ PASS |
| TC-007 | /posts | POST | Crear post sin campos obligatorios | ❌ FAIL |
| TC-008 | /posts | POST | Crear post con userId inválido | ⚠️ OBS |
| TC-009 | /posts/1 | PUT | Actualizar post existente | ✅ PASS |
| TC-010 | /posts/9999 | PUT | Actualizar post inexistente | ✅ PASS |
| TC-011 | /posts/1 | DELETE | Eliminar post existente | ✅ PASS |
| TC-012 | /posts/9999 | DELETE | Eliminar post inexistente | ✅ PASS |
| TC-013 | /users | GET | Obtener todos los usuarios | ✅ PASS |
| TC-014 | /users/1 | GET | Obtener usuario por ID válido | ✅ PASS |
| TC-015 | /users/9999 | GET | Usuario con ID inexistente | ✅ PASS |

**Total: 15 casos | ✅ 12 PASS | ❌ 1 FAIL | ⚠️ 2 OBSERVACIONES**
