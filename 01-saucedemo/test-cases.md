# Test Cases — Sauce Demo

**Proyecto:** Sauce Demo  
**Tester:** Alexis Avakian  
**Fecha:** Junio 2026  
**Versión:** 1.0

---

## Módulo 1: Login

---

### TC-001 — Login con credenciales válidas

| Campo | Detalle |
|---|---|
| **ID** | TC-001 |
| **Módulo** | Login |
| **Prioridad** | Alta |
| **Tipo** | Funcional |

**Precondiciones:**  
Usuario en la página de login (`https://www.saucedemo.com`)

**Pasos:**
1. Ingresar usuario: `standard_user`
2. Ingresar contraseña: `secret_sauce`
3. Hacer click en "Login"

**Resultado esperado:**  
El sistema redirige al catálogo de productos (`/inventory.html`).

**Resultado obtenido:** ✅ PASS

---

### TC-002 — Login con contraseña incorrecta

| Campo | Detalle |
|---|---|
| **ID** | TC-002 |
| **Módulo** | Login |
| **Prioridad** | Alta |
| **Tipo** | Funcional — Negativo |

**Precondiciones:**  
Usuario en la página de login.

**Pasos:**
1. Ingresar usuario: `standard_user`
2. Ingresar contraseña: `contraseña_incorrecta`
3. Hacer click en "Login"

**Resultado esperado:**  
Se muestra mensaje de error: *"Username and password do not match any user in this service"*. No se permite el acceso.

**Resultado obtenido:** ✅ PASS

---

### TC-003 — Login con campos vacíos

| Campo | Detalle |
|---|---|
| **ID** | TC-003 |
| **Módulo** | Login |
| **Prioridad** | Media |
| **Tipo** | Funcional — Negativo |

**Precondiciones:**  
Usuario en la página de login con ambos campos vacíos.

**Pasos:**
1. No ingresar ningún dato
2. Hacer click en "Login"

**Resultado esperado:**  
Se muestra mensaje de error indicando que el campo usuario es requerido.

**Resultado obtenido:** ✅ PASS

---

### TC-004 — Login con usuario bloqueado

| Campo | Detalle |
|---|---|
| **ID** | TC-004 |
| **Módulo** | Login |
| **Prioridad** | Alta |
| **Tipo** | Funcional |

**Precondiciones:**  
Usuario en la página de login.

**Pasos:**
1. Ingresar usuario: `locked_out_user`
2. Ingresar contraseña: `secret_sauce`
3. Hacer click en "Login"

**Resultado esperado:**  
Se muestra mensaje de error: *"Sorry, this user has been locked out."*

**Resultado obtenido:** ✅ PASS

---

### TC-005 — Login con usuario problemático (performance_glitch_user)

| Campo | Detalle |
|---|---|
| **ID** | TC-005 |
| **Módulo** | Login |
| **Prioridad** | Media |
| **Tipo** | Performance / UX |

**Precondiciones:**  
Usuario en la página de login.

**Pasos:**
1. Ingresar usuario: `performance_glitch_user`
2. Ingresar contraseña: `secret_sauce`
3. Hacer click en "Login"
4. Medir tiempo de carga hasta redirección al catálogo

**Resultado esperado:**  
El sistema redirige al catálogo en menos de 2 segundos.

**Resultado obtenido:** ❌ FAIL — La carga toma aproximadamente 5 segundos. Ver **BUG-001**.

---

## Módulo 2: Catálogo de Productos

---

### TC-006 — Visualización del catálogo tras login exitoso

| Campo | Detalle |
|---|---|
| **ID** | TC-006 |
| **Módulo** | Catálogo |
| **Prioridad** | Alta |
| **Tipo** | Funcional |

**Pasos:**
1. Hacer login con `standard_user`
2. Observar la página de inventario

**Resultado esperado:**  
Se muestran 6 productos con nombre, imagen, descripción y precio.

**Resultado obtenido:** ✅ PASS

---

### TC-007 — Ordenamiento por precio (menor a mayor)

| Campo | Detalle |
|---|---|
| **ID** | TC-007 |
| **Módulo** | Catálogo |
| **Prioridad** | Media |
| **Tipo** | Funcional |

**Pasos:**
1. En el catálogo, seleccionar "Price (low to high)" en el selector de ordenamiento
2. Observar el orden de los productos

**Resultado esperado:**  
Los productos se muestran ordenados de menor a mayor precio.

**Resultado obtenido:** ✅ PASS

---

### TC-008 — Ordenamiento por precio (mayor a menor)

| Campo | Detalle |
|---|---|
| **ID** | TC-008 |
| **Módulo** | Catálogo |
| **Prioridad** | Media |
| **Tipo** | Funcional |

**Pasos:**
1. Seleccionar "Price (high to low)" en el selector de ordenamiento
2. Observar el orden de los productos

**Resultado esperado:**  
Los productos se muestran ordenados de mayor a menor precio.

**Resultado obtenido:** ✅ PASS

---

### TC-009 — Acceso al detalle de producto

| Campo | Detalle |
|---|---|
| **ID** | TC-009 |
| **Módulo** | Catálogo |
| **Prioridad** | Alta |
| **Tipo** | Funcional |

**Pasos:**
1. Hacer click en el nombre de cualquier producto
2. Observar la página de detalle

**Resultado esperado:**  
Se muestra la página de detalle con nombre, imagen, descripción, precio y botón "Add to cart".

**Resultado obtenido:** ✅ PASS

---

## Módulo 3: Carrito de Compras

---

### TC-010 — Agregar producto al carrito desde el catálogo

| Campo | Detalle |
|---|---|
| **ID** | TC-010 |
| **Módulo** | Carrito |
| **Prioridad** | Alta |
| **Tipo** | Funcional |

**Pasos:**
1. En el catálogo, hacer click en "Add to cart" de cualquier producto
2. Observar el ícono del carrito en el header

**Resultado esperado:**  
El botón cambia a "Remove" y el contador del carrito muestra "1".

**Resultado obtenido:** ✅ PASS

---

### TC-011 — Agregar múltiples productos al carrito

| Campo | Detalle |
|---|---|
| **ID** | TC-011 |
| **Módulo** | Carrito |
| **Prioridad** | Media |
| **Tipo** | Funcional |

**Pasos:**
1. Agregar 3 productos distintos al carrito
2. Hacer click en el ícono del carrito

**Resultado esperado:**  
El carrito muestra los 3 productos con nombre, cantidad y precio individual.

**Resultado obtenido:** ✅ PASS

---

### TC-012 — Eliminar producto del carrito

| Campo | Detalle |
|---|---|
| **ID** | TC-012 |
| **Módulo** | Carrito |
| **Prioridad** | Alta |
| **Tipo** | Funcional |

**Pasos:**
1. Con al menos 1 producto en el carrito, ir al carrito
2. Hacer click en "Remove" sobre un producto

**Resultado esperado:**  
El producto desaparece del carrito y el contador se actualiza.

**Resultado obtenido:** ✅ PASS

---

### TC-013 — Continuar comprando desde el carrito

| Campo | Detalle |
|---|---|
| **ID** | TC-013 |
| **Módulo** | Carrito |
| **Prioridad** | Media |
| **Tipo** | Funcional |

**Pasos:**
1. Ir al carrito con al menos 1 producto
2. Hacer click en "Continue Shopping"

**Resultado esperado:**  
El sistema regresa al catálogo manteniendo los productos ya agregados al carrito.

**Resultado obtenido:** ✅ PASS

---

## Módulo 4: Checkout

---

### TC-014 — Iniciar proceso de checkout

| Campo | Detalle |
|---|---|
| **ID** | TC-014 |
| **Módulo** | Checkout |
| **Prioridad** | Alta |
| **Tipo** | Funcional |

**Pasos:**
1. Con productos en el carrito, hacer click en "Checkout"
2. Observar el formulario

**Resultado esperado:**  
Se muestra el formulario con campos: First Name, Last Name, Zip/Postal Code.

**Resultado obtenido:** ✅ PASS

---

### TC-015 — Checkout con campos vacíos

| Campo | Detalle |
|---|---|
| **ID** | TC-015 |
| **Módulo** | Checkout |
| **Prioridad** | Alta |
| **Tipo** | Funcional — Negativo |

**Pasos:**
1. En el formulario de checkout, dejar todos los campos vacíos
2. Hacer click en "Continue"

**Resultado esperado:**  
Se muestra error indicando que el campo "First Name" es requerido.

**Resultado obtenido:** ✅ PASS

---

### TC-016 — Checkout con datos válidos

| Campo | Detalle |
|---|---|
| **ID** | TC-016 |
| **Módulo** | Checkout |
| **Prioridad** | Alta |
| **Tipo** | Funcional |

**Pasos:**
1. Completar: First Name: `Alexis`, Last Name: `Avakian`, Zip: `1234`
2. Hacer click en "Continue"

**Resultado esperado:**  
Se muestra el resumen de la orden con los productos, subtotal, impuestos y total.

**Resultado obtenido:** ✅ PASS

---

### TC-017 — Verificación del cálculo de total

| Campo | Detalle |
|---|---|
| **ID** | TC-017 |
| **Módulo** | Checkout |
| **Prioridad** | Alta |
| **Tipo** | Funcional |

**Pasos:**
1. Agregar 2 productos al carrito (ej: $9.99 + $15.99)
2. Completar checkout hasta el resumen
3. Verificar que el subtotal = suma de productos y que el total = subtotal + tax

**Resultado esperado:**  
Subtotal: $25.98 / Tax: $2.08 / Total: $28.06

**Resultado obtenido:** ✅ PASS

---

### TC-018 — Confirmación de orden

| Campo | Detalle |
|---|---|
| **ID** | TC-018 |
| **Módulo** | Checkout |
| **Prioridad** | Alta |
| **Tipo** | Funcional |

**Pasos:**
1. En el resumen de orden, hacer click en "Finish"

**Resultado esperado:**  
Se muestra pantalla de confirmación con el mensaje: *"Thank you for your order!"*

**Resultado obtenido:** ✅ PASS

---

### TC-019 — Logout del sistema

| Campo | Detalle |
|---|---|
| **ID** | TC-019 |
| **Módulo** | Navegación |
| **Prioridad** | Media |
| **Tipo** | Funcional |

**Pasos:**
1. Hacer click en el menú hamburguesa (≡) en el header
2. Hacer click en "Logout"

**Resultado esperado:**  
El sistema redirige a la página de login y la sesión queda cerrada.

**Resultado obtenido:** ✅ PASS

---

### TC-020 — Acceso directo a inventario sin sesión activa

| Campo | Detalle |
|---|---|
| **ID** | TC-020 |
| **Módulo** | Seguridad |
| **Prioridad** | Alta |
| **Tipo** | Funcional — Seguridad |

**Pasos:**
1. Sin estar logueado, intentar acceder directamente a `https://www.saucedemo.com/inventory.html`

**Resultado esperado:**  
El sistema redirige al login y no permite el acceso al inventario.

**Resultado obtenido:** ❌ FAIL — Ver **BUG-002**.

---

## Resumen de Ejecución

| ID | Descripción | Estado |
|---|---|---|
| TC-001 | Login con credenciales válidas | ✅ PASS |
| TC-002 | Login con contraseña incorrecta | ✅ PASS |
| TC-003 | Login con campos vacíos | ✅ PASS |
| TC-004 | Login con usuario bloqueado | ✅ PASS |
| TC-005 | Login con performance_glitch_user | ❌ FAIL |
| TC-006 | Visualización del catálogo | ✅ PASS |
| TC-007 | Ordenamiento precio menor a mayor | ✅ PASS |
| TC-008 | Ordenamiento precio mayor a menor | ✅ PASS |
| TC-009 | Acceso al detalle de producto | ✅ PASS |
| TC-010 | Agregar producto al carrito | ✅ PASS |
| TC-011 | Múltiples productos en carrito | ✅ PASS |
| TC-012 | Eliminar producto del carrito | ✅ PASS |
| TC-013 | Continuar comprando | ✅ PASS |
| TC-014 | Iniciar checkout | ✅ PASS |
| TC-015 | Checkout con campos vacíos | ✅ PASS |
| TC-016 | Checkout con datos válidos | ✅ PASS |
| TC-017 | Verificación de cálculo de total | ✅ PASS |
| TC-018 | Confirmación de orden | ✅ PASS |
| TC-019 | Logout del sistema | ✅ PASS |
| TC-020 | Acceso sin sesión activa | ❌ FAIL |

**Total: 20 casos | ✅ 18 PASS | ❌ 2 FAIL**
