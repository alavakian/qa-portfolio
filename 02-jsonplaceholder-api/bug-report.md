# Bug Reports & Observaciones — JSONPlaceholder API

**Proyecto:** JSONPlaceholder API  
**Tester:** Alexis Avakian  
**Fecha:** Junio 2026  
**Herramienta:** Postman

---

## BUG-001 — La API acepta la creación de posts sin campos obligatorios

| Campo | Detalle |
|---|---|
| **ID** | BUG-001 |
| **Severidad** | Alta |
| **Prioridad** | Alta |
| **Módulo** | Posts — POST |
| **Estado** | Abierto |
| **Caso relacionado** | TC-007 |

### Descripción

Al realizar una request POST a `/posts` con un body vacío `{}`, la API responde con status `201 Created` en lugar de rechazar la solicitud. Esto indica ausencia de validación de campos obligatorios (`title`, `body`, `userId`).

### Request reproducible

```
POST https://jsonplaceholder.typicode.com/posts
Content-Type: application/json

{}
```

### Respuesta obtenida

```json
HTTP/1.1 201 Created

{
  "id": 101
}
```

### Resultado esperado

```
HTTP/1.1 400 Bad Request

{
  "error": "Los campos title, body y userId son obligatorios."
}
```

### Impacto

- Permite la creación de recursos inválidos o incompletos en el sistema
- En un entorno productivo, esto podría generar registros corruptos en la base de datos
- Ausencia de feedback claro para el cliente que consume la API

---

## OBS-001 — Respuesta ambigua al consultar comentarios de un post inexistente

| Campo | Detalle |
|---|---|
| **ID** | OBS-001 |
| **Tipo** | Observación de comportamiento |
| **Severidad** | Baja |
| **Módulo** | Posts / Comments — GET |
| **Estado** | Abierto |
| **Caso relacionado** | TC-005 |

### Descripción

Al consultar `/posts/9999/comments` (post inexistente), la API devuelve `200 OK` con un array vacío `[]`. Este comportamiento es ambiguo: el cliente no puede distinguir si el post no tiene comentarios o si el post directamente no existe.

### Request reproducible

```
GET https://jsonplaceholder.typicode.com/posts/9999/comments
```

### Respuesta obtenida

```json
HTTP/1.1 200 OK

[]
```

### Comportamiento esperado

```
HTTP/1.1 404 Not Found

{
  "error": "El post con id 9999 no existe."
}
```

### Impacto

- Comportamiento inconsistente: `GET /posts/9999` devuelve `404`, pero `GET /posts/9999/comments` devuelve `200`
- Dificulta el manejo de errores en aplicaciones que consumen esta API
- Puede generar confusión en el equipo de desarrollo al depurar

---

## OBS-002 — La API no valida la existencia del userId al crear un post

| Campo | Detalle |
|---|---|
| **ID** | OBS-002 |
| **Tipo** | Observación de comportamiento |
| **Severidad** | Media |
| **Módulo** | Posts — POST |
| **Estado** | Abierto |
| **Caso relacionado** | TC-008 |

### Descripción

Al crear un post con un `userId` que no existe en el sistema (ej: `9999`), la API acepta la solicitud y devuelve `201 Created`. No se valida la integridad referencial entre el post y el usuario.

### Request reproducible

```
POST https://jsonplaceholder.typicode.com/posts
Content-Type: application/json

{
  "title": "Test",
  "body": "Contenido de prueba",
  "userId": 9999
}
```

### Respuesta obtenida

```json
HTTP/1.1 201 Created

{
  "title": "Test",
  "body": "Contenido de prueba",
  "userId": 9999,
  "id": 101
}
```

### Comportamiento esperado

```
HTTP/1.1 400 Bad Request

{
  "error": "El usuario con id 9999 no existe."
}
```

### Impacto

- Permite crear posts huérfanos, sin usuario válido asociado
- En producción, esto puede generar inconsistencias de datos y problemas al mostrar información del autor
- Indica ausencia de validación de integridad referencial

---

## Resumen

| ID | Tipo | Descripción | Severidad | Estado |
|---|---|---|---|---|
| BUG-001 | Bug | POST acepta body vacío sin validación | Alta | Abierto |
| OBS-001 | Observación | Respuesta ambigua en comentarios de post inexistente | Baja | Abierto |
| OBS-002 | Observación | No se valida existencia de userId en POST | Media | Abierto |
