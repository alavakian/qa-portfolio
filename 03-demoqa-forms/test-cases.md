# Test Cases — DemoQA Forms

**Proyecto:** DemoQA — Practice Form  
**Tester:** Alexis Avakian  
**Fecha:** Junio 2026  
**URL:** https://demoqa.com/automation-practice-form

---

## Módulo 1: Campos de texto

---

### TC-001 — Envío del formulario con todos los campos obligatorios completos

| Campo | Detalle |
|---|---|
| **ID** | TC-001 |
| **Módulo** | Formulario completo |
| **Prioridad** | Alta |
| **Tipo** | Funcional |

**Precondiciones:**  
Usuario en `https://demoqa.com/automation-practice-form`

**Pasos:**
1. Completar First Name: `Alexis`
2. Completar Last Name: `Avakian`
3. Completar Email: `alexis@test.com`
4. Seleccionar Gender: `Male`
5. Completar Mobile: `1234567890`
6. Hacer click en "Submit"

**Resultado esperado:**  
Se muestra modal de confirmación con los datos ingresados.

**Resultado obtenido:** ✅ PASS

---

### TC-002 — Envío del formulario con campos obligatorios vacíos

| Campo | Detalle |
|---|---|
| **ID** | TC-002 |
| **Módulo** | Validación |
| **Prioridad** | Alta |
| **Tipo** | Negativo |

**Pasos:**
1. No completar ningún campo
2. Hacer click en "Submit"

**Resultado esperado:**  
Los campos obligatorios se marcan en rojo. El formulario no se envía.

**Resultado obtenido:** ✅ PASS  
First Name, Last Name, Gender y Mobile se marcan en rojo.

---

### TC-003 — Campo First Name con solo espacios en blanco

| Campo | Detalle |
|---|---|
| **ID** | TC-003 |
| **Módulo** | Validación — First Name |
| **Prioridad** | Media |
| **Tipo** | Negativo |

**Pasos:**
1. Ingresar solo espacios en blanco en First Name: `     `
2. Completar el resto de campos obligatorios correctamente
3. Hacer click en "Submit"

**Resultado esperado:**  
El campo se considera vacío y se marca como inválido.

**Resultado obtenido:** ❌ FAIL  
El formulario se envía con espacios en blanco como nombre. Ver **BUG-001**.

---

### TC-004 — Campo First Name con caracteres especiales

| Campo | Detalle |
|---|---|
| **ID** | TC-004 |
| **Módulo** | Validación — First Name |
| **Prioridad** | Media |
| **Tipo** | Negativo |

**Pasos:**
1. Ingresar en First Name: `@#$%^&*`
2. Completar el resto de campos obligatorios correctamente
3. Hacer click en "Submit"

**Resultado esperado:**  
El campo rechaza caracteres especiales o muestra un mensaje de error.

**Resultado obtenido:** ❌ FAIL  
El formulario acepta caracteres especiales como nombre válido. Ver **BUG-002**.

---

### TC-005 — Campo First Name con número elevado de caracteres

| Campo | Detalle |
|---|---|
| **ID** | TC-005 |
| **Módulo** | Validación — First Name |
| **Prioridad** | Baja |
| **Tipo** | Límite |

**Pasos:**
1. Ingresar en First Name una cadena de 200 caracteres
2. Completar el resto de campos y enviar

**Resultado esperado:**  
El campo limita la entrada o muestra un error por exceso de caracteres.

**Resultado obtenido:** ⚠️ OBSERVACIÓN  
El campo acepta más de 200 caracteres sin ningún límite ni advertencia. Ver **OBS-001**.

---

## Módulo 2: Email

---

### TC-006 — Email con formato válido

| Campo | Detalle |
|---|---|
| **ID** | TC-006 |
| **Módulo** | Validación — Email |
| **Prioridad** | Alta |
| **Tipo** | Funcional |

**Pasos:**
1. Ingresar email: `alexis@test.com`
2. Completar demás campos obligatorios y enviar

**Resultado esperado:**  
El formulario acepta el email y se envía correctamente.

**Resultado obtenido:** ✅ PASS

---

### TC-007 — Email sin símbolo @

| Campo | Detalle |
|---|---|
| **ID** | TC-007 |
| **Módulo** | Validación — Email |
| **Prioridad** | Alta |
| **Tipo** | Negativo |

**Pasos:**
1. Ingresar email: `alexistest.com`
2. Completar demás campos y enviar

**Resultado esperado:**  
El campo se marca como inválido con mensaje de error.

**Resultado obtenido:** ✅ PASS  
El campo se resalta en rojo y el formulario no se envía.

---

### TC-008 — Email sin dominio

| Campo | Detalle |
|---|---|
| **ID** | TC-008 |
| **Módulo** | Validación — Email |
| **Prioridad** | Media |
| **Tipo** | Negativo |

**Pasos:**
1. Ingresar email: `alexis@`
2. Completar demás campos y enviar

**Resultado esperado:**  
El campo se marca como inválido.

**Resultado obtenido:** ✅ PASS  
Campo marcado como inválido. Formulario no se envía.

---

## Módulo 3: Teléfono móvil

---

### TC-009 — Teléfono con 10 dígitos válidos

| Campo | Detalle |
|---|---|
| **ID** | TC-009 |
| **Módulo** | Validación — Mobile |
| **Prioridad** | Alta |
| **Tipo** | Funcional |

**Pasos:**
1. Ingresar mobile: `1234567890`
2. Completar demás campos y enviar

**Resultado esperado:**  
El formulario acepta el número y se envía correctamente.

**Resultado obtenido:** ✅ PASS

---

### TC-010 — Teléfono con menos de 10 dígitos

| Campo | Detalle |
|---|---|
| **ID** | TC-010 |
| **Módulo** | Validación — Mobile |
| **Prioridad** | Alta |
| **Tipo** | Negativo |

**Pasos:**
1. Ingresar mobile: `12345`
2. Completar demás campos y enviar

**Resultado esperado:**  
El campo se marca como inválido indicando que se requieren 10 dígitos.

**Resultado obtenido:** ✅ PASS  
Campo marcado en rojo. Formulario no se envía.

---

### TC-011 — Teléfono con letras

| Campo | Detalle |
|---|---|
| **ID** | TC-011 |
| **Módulo** | Validación — Mobile |
| **Prioridad** | Media |
| **Tipo** | Negativo |

**Pasos:**
1. Ingresar mobile: `abcdefghij`
2. Completar demás campos y enviar

**Resultado esperado:**  
El campo rechaza letras o muestra error de validación.

**Resultado obtenido:** ❌ FAIL  
El campo acepta letras y el formulario intenta enviarse. Ver **BUG-003**.

---

## Módulo 4: Selector de género

---

### TC-012 — Selección de género obligatoria

| Campo | Detalle |
|---|---|
| **ID** | TC-012 |
| **Módulo** | Validación — Gender |
| **Prioridad** | Alta |
| **Tipo** | Funcional |

**Pasos:**
1. Completar todos los campos obligatorios excepto Gender
2. Hacer click en "Submit"

**Resultado esperado:**  
El formulario no se envía y el campo Gender se resalta como obligatorio.

**Resultado obtenido:** ✅ PASS

---

### TC-013 — Selección de cada opción de género

| Campo | Detalle |
|---|---|
| **ID** | TC-013 |
| **Módulo** | Gender |
| **Prioridad** | Media |
| **Tipo** | Funcional |

**Pasos:**
1. Seleccionar "Male", completar formulario y enviar — verificar modal
2. Repetir con "Female"
3. Repetir con "Other"

**Resultado esperado:**  
Las tres opciones son seleccionables y se reflejan correctamente en el modal de confirmación.

**Resultado obtenido:** ✅ PASS

---

## Módulo 5: Fecha de nacimiento

---

### TC-014 — Selección de fecha válida

| Campo | Detalle |
|---|---|
| **ID** | TC-014 |
| **Módulo** | Date of Birth |
| **Prioridad** | Media |
| **Tipo** | Funcional |

**Pasos:**
1. Hacer click en el campo Date of Birth
2. Seleccionar una fecha válida usando el datepicker
3. Completar demás campos y enviar

**Resultado esperado:**  
La fecha se registra correctamente y aparece en el modal de confirmación.

**Resultado obtenido:** ✅ PASS

---

### TC-015 — Fecha futura como fecha de nacimiento

| Campo | Detalle |
|---|---|
| **ID** | TC-015 |
| **Módulo** | Date of Birth |
| **Prioridad** | Media |
| **Tipo** | Negativo |

**Pasos:**
1. Seleccionar una fecha futura en el datepicker
2. Completar demás campos y enviar

**Resultado esperado:**  
El formulario rechaza fechas futuras como fecha de nacimiento válida.

**Resultado obtenido:** ⚠️ OBSERVACIÓN  
El formulario acepta fechas futuras sin validación. Ver **OBS-002**.

---

## Módulo 6: Envío y confirmación

---

### TC-016 — Modal de confirmación muestra datos correctos

| Campo | Detalle |
|---|---|
| **ID** | TC-016 |
| **Módulo** | Confirmación |
| **Prioridad** | Alta |
| **Tipo** | Funcional |

**Pasos:**
1. Completar el formulario con datos conocidos
2. Enviar y verificar el modal

**Resultado esperado:**  
El modal muestra exactamente los datos ingresados, sin modificaciones.

**Resultado obtenido:** ✅ PASS

---

### TC-017 — Cierre del modal de confirmación

| Campo | Detalle |
|---|---|
| **ID** | TC-017 |
| **Módulo** | Confirmación |
| **Prioridad** | Media |
| **Tipo** | Funcional |

**Pasos:**
1. Enviar formulario correctamente
2. En el modal, hacer click en "Close"

**Resultado esperado:**  
El modal se cierra y el formulario vuelve a su estado inicial (vacío).

**Resultado obtenido:** ✅ PASS

---

### TC-018 — Upload de imagen de perfil

| Campo | Detalle |
|---|---|
| **ID** | TC-018 |
| **Módulo** | Upload |
| **Prioridad** | Baja |
| **Tipo** | Funcional |

**Pasos:**
1. Hacer click en "Choose File" en el campo Picture
2. Seleccionar una imagen .jpg del equipo
3. Verificar que el nombre del archivo aparece junto al botón

**Resultado esperado:**  
El nombre del archivo se muestra correctamente junto al botón de upload.

**Resultado obtenido:** ✅ PASS

---

## Resumen de Ejecución

| ID | Descripción | Estado |
|---|---|---|
| TC-001 | Formulario completo con datos válidos | ✅ PASS |
| TC-002 | Envío con campos obligatorios vacíos | ✅ PASS |
| TC-003 | First Name con espacios en blanco | ❌ FAIL |
| TC-004 | First Name con caracteres especiales | ❌ FAIL |
| TC-005 | First Name con más de 200 caracteres | ⚠️ OBS |
| TC-006 | Email con formato válido | ✅ PASS |
| TC-007 | Email sin símbolo @ | ✅ PASS |
| TC-008 | Email sin dominio | ✅ PASS |
| TC-009 | Teléfono con 10 dígitos válidos | ✅ PASS |
| TC-010 | Teléfono con menos de 10 dígitos | ✅ PASS |
| TC-011 | Teléfono con letras | ❌ FAIL |
| TC-012 | Género obligatorio | ✅ PASS |
| TC-013 | Selección de cada opción de género | ✅ PASS |
| TC-014 | Fecha de nacimiento válida | ✅ PASS |
| TC-015 | Fecha futura como nacimiento | ⚠️ OBS |
| TC-016 | Modal muestra datos correctos | ✅ PASS |
| TC-017 | Cierre del modal | ✅ PASS |
| TC-018 | Upload de imagen | ✅ PASS |

**Total: 18 casos | ✅ 13 PASS | ❌ 3 FAIL | ⚠️ 2 OBSERVACIONES**
