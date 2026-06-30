# 🧪 QA Manual Testing — JSONPlaceholder API

## Descripción del proyecto

Testing funcional sobre [JSONPlaceholder](https://jsonplaceholder.typicode.com), una API REST pública utilizada para práctica y prototipado. Las pruebas fueron ejecutadas con **Postman**.

## Alcance del testing

| Endpoint | Método | Estado |
|---|---|---|
| /posts | GET | ✅ Completado |
| /posts/{id} | GET | ✅ Completado |
| /posts | POST | ✅ Completado |
| /posts/{id} | PUT | ✅ Completado |
| /posts/{id} | DELETE | ✅ Completado |
| /users | GET | ✅ Completado |
| /posts/{id}/comments | GET | ✅ Completado |

## Artefactos

- [`test-cases.md`](./test-cases.md) — Casos de prueba funcionales de API
- [`bug-report.md`](./bug-report.md) — Bugs y observaciones encontradas durante la ejecución

## Entorno de pruebas

- **API:** JSONPlaceholder v1
- **URL base:** https://jsonplaceholder.typicode.com
- **Herramienta:** Postman
- **Tipo de testing:** Manual — API REST (Funcional)

## Conceptos clave

| Término | Descripción |
|---|---|
| **GET** | Obtener datos del servidor |
| **POST** | Crear un nuevo recurso |
| **PUT** | Actualizar un recurso existente |
| **DELETE** | Eliminar un recurso |
| **Status 200** | OK — respuesta exitosa |
| **Status 201** | Created — recurso creado exitosamente |
| **Status 404** | Not Found — recurso no encontrado |
| **JSON** | Formato de datos usado en las respuestas |

## Resumen de resultados

| Total casos | Pasaron | Fallaron | Observaciones |
|---|---|---|---|
| 15 | 12 | 1 | 2 |

---

*Portfolio de QA Manual — Alexis Avakian*  
*github.com/alavakian*
