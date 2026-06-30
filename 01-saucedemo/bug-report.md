# Bug Reports — Sauce Demo

**Proyecto:** Sauce Demo  
**Tester:** Alexis Avakian  
**Fecha:** Junio 2026

---

## BUG-001 — Tiempo de carga excesivo para `performance_glitch_user`

| Campo | Detalle |
|---|---|
| **ID** | BUG-001 |
| **Severidad** | Media |
| **Prioridad** | Media |
| **Módulo** | Login |
| **Estado** | Abierto |
| **Caso relacionado** | TC-005 |

### Descripción

El usuario `performance_glitch_user` experimenta una demora de aproximadamente 5 segundos al hacer login antes de ser redirigido al catálogo. El tiempo de respuesta supera ampliamente el umbral aceptable de 2 segundos para una operación de autenticación estándar.

### Pasos para reproducir

1. Ir a `https://www.saucedemo.com`
2. Ingresar usuario: `performance_glitch_user`
3. Ingresar contraseña: `secret_sauce`
4. Hacer click en "Login"
5. Medir el tiempo hasta la carga completa de `/inventory.html`

### Resultado esperado

Redirección al catálogo en menos de 2 segundos.

### Resultado obtenido

La página tarda ~5 segundos en cargar. Durante ese tiempo no hay indicador de carga visible, lo que puede llevar al usuario a creer que el sistema no está respondiendo y hacer click múltiples veces.

### Impacto en el usuario

- Experiencia de usuario degradada
- Posible frustración y abandono
- Riesgo de múltiples envíos del formulario de login

### Evidencia

- Entorno: Chrome 125, Windows 11
- Hora de prueba: reproducible de forma consistente

---

## BUG-002 — Acceso directo a inventario sin autenticación activa

| Campo | Detalle |
|---|---|
| **ID** | BUG-002 |
| **Severidad** | Alta |
| **Prioridad** | Alta |
| **Módulo** | Seguridad / Autenticación |
| **Estado** | Abierto |
| **Caso relacionado** | TC-020 |

### Descripción

Al acceder directamente a la URL `/inventory.html` sin tener una sesión activa, el sistema muestra la página de inventario en lugar de redirigir al login. Esto representa una vulnerabilidad de control de acceso donde rutas protegidas son accesibles sin autenticación.

### Pasos para reproducir

1. Asegurarse de no tener sesión activa (o abrir ventana de incógnito)
2. Ingresar directamente en la barra de direcciones: `https://www.saucedemo.com/inventory.html`
3. Observar qué página carga

### Resultado esperado

El sistema detecta la ausencia de sesión y redirige a `https://www.saucedemo.com` (login).

### Resultado obtenido

La página `/inventory.html` carga parcialmente — se muestra la estructura de la página pero sin productos, y sin redirección al login.

### Impacto en el usuario

- Brecha de seguridad: rutas protegidas expuestas sin autenticación
- Comportamiento inconsistente que puede generar confusión
- En un entorno real, podría exponer datos sensibles o funcionalidad restringida

### Evidencia

- Entorno: Chrome 125, Windows 11
- Reproducible en modo incógnito

---

## BUG-003 — El carrito persiste tras cerrar sesión y volver a loguearse

| Campo | Detalle |
|---|---|
| **ID** | BUG-003 |
| **Severidad** | Baja |
| **Prioridad** | Baja |
| **Módulo** | Carrito / Sesión |
| **Estado** | Abierto |

### Descripción

Al agregar productos al carrito, cerrar sesión y volver a ingresar con el mismo usuario, los productos permanecen en el carrito. Dependiendo del caso de uso, este comportamiento puede o no ser intencional — pero no está documentado ni comunicado al usuario.

### Pasos para reproducir

1. Hacer login con `standard_user`
2. Agregar 2 productos al carrito
3. Hacer logout desde el menú
4. Volver a hacer login con `standard_user`
5. Ir al carrito

### Resultado esperado

El carrito debería estar vacío al iniciar una nueva sesión, o el sistema debería informar al usuario que los productos fueron guardados.

### Resultado obtenido

Los productos siguen en el carrito sin ninguna notificación al usuario.

### Impacto en el usuario

- Comportamiento inesperado que puede generar confusión
- Ausencia de comunicación hacia el usuario sobre el estado del carrito

---

## BUG-004 — Ausencia de indicador de carga durante el proceso de login

| Campo | Detalle |
|---|---|
| **ID** | BUG-004 |
| **Severidad** | Baja |
| **Prioridad** | Baja |
| **Módulo** | Login / UX |
| **Estado** | Abierto |

### Descripción

Al hacer click en "Login", el botón no muestra ningún indicador de que la solicitud está siendo procesada. Combinado con el bug BUG-001 (demora de 5 segundos para ciertos usuarios), esto genera una experiencia de usuario deficiente donde el sistema aparenta estar "congelado".

### Pasos para reproducir

1. Ir a `https://www.saucedemo.com`
2. Ingresar cualquier credencial válida
3. Hacer click en "Login"
4. Observar el botón y la interfaz durante el proceso de carga

### Resultado esperado

El botón debería deshabilitarse o mostrar un spinner/mensaje de "Cargando..." mientras se procesa el login.

### Resultado obtenido

El botón permanece igual y no hay ningún feedback visual durante la espera.

### Impacto en el usuario

- Experiencia de usuario degradada, especialmente notable con `performance_glitch_user`
- Riesgo de clicks múltiples por parte del usuario al no recibir feedback

---

## Resumen de Bugs

| ID | Descripción | Severidad | Estado |
|---|---|---|---|
| BUG-001 | Tiempo de carga excesivo en login | Media | Abierto |
| BUG-002 | Acceso a inventario sin autenticación | Alta | Abierto |
| BUG-003 | Carrito persiste entre sesiones | Baja | Abierto |
| BUG-004 | Sin indicador de carga en login | Baja | Abierto |
