# Bug Reports & Observaciones — DemoQA Forms

**Proyecto:** DemoQA — Practice Form  
**Tester:** Alexis Avakian  
**Fecha:** Junio 2026

---

## BUG-001 — El campo First Name acepta espacios en blanco como valor válido

| Campo | Detalle |
|---|---|
| **ID** | BUG-001 |
| **Severidad** | Media |
| **Prioridad** | Alta |
| **Módulo** | Validación — First Name |
| **Estado** | Abierto |
| **Caso relacionado** | TC-003 |

### Descripción

Al ingresar únicamente espacios en blanco en el campo First Name y enviar el formulario, el sistema lo acepta como valor válido. El modal de confirmación muestra el nombre como un espacio vacío, lo que indica ausencia de validación de contenido real en el campo.

### Pasos para reproducir

1. Ir a `https://demoqa.com/automation-practice-form`
2. En el campo First Name ingresar: `     ` (5 espacios)
3. Completar Last Name, Gender y Mobile con datos válidos
4. Hacer click en "Submit"

### Resultado esperado

El campo debería detectar que el contenido es solo espacios y marcarse como inválido, requiriendo un nombre real.

### Resultado obtenido

El formulario se envía exitosamente. El modal de confirmación muestra el campo Student Name con espacios en blanco.

### Impacto

- Permite el registro de usuarios con nombres inválidos
- Genera datos inconsistentes en el sistema
- En producción podría afectar funcionalidades que dependan del nombre del usuario (saludo personalizado, facturación, etc.)

---

## BUG-002 — El campo First Name acepta caracteres especiales

| Campo | Detalle |
|---|---|
| **ID** | BUG-002 |
| **Severidad** | Media |
| **Prioridad** | Media |
| **Módulo** | Validación — First Name |
| **Estado** | Abierto |
| **Caso relacionado** | TC-004 |

### Descripción

El campo First Name acepta caracteres especiales (`@#$%^&*`) como entrada válida. No existe ninguna restricción que limite el campo a letras y caracteres propios de nombres reales.

### Pasos para reproducir

1. Ir a `https://demoqa.com/automation-practice-form`
2. En First Name ingresar: `@#$%^&*`
3. Completar demás campos obligatorios con datos válidos
4. Hacer click en "Submit"

### Resultado esperado

El campo debería rechazar caracteres especiales y mostrar un mensaje como: *"El nombre solo puede contener letras."*

### Resultado obtenido

El formulario se envía correctamente y el modal muestra `@#$%^&*` como nombre del estudiante.

### Impacto

- Datos de usuario inválidos almacenados en el sistema
- Posible conflicto con sistemas que procesan o parsean nombres (ej: generación de PDFs, emails automáticos)
- Riesgo de inyección de caracteres en otros contextos

---

## BUG-003 — El campo Mobile acepta letras como entrada

| Campo | Detalle |
|---|---|
| **ID** | BUG-003 |
| **Severidad** | Alta |
| **Prioridad** | Alta |
| **Módulo** | Validación — Mobile |
| **Estado** | Abierto |
| **Caso relacionado** | TC-011 |

### Descripción

El campo Mobile Number acepta letras como entrada válida. Al ingresar `abcdefghij` (10 caracteres alfabéticos), el formulario no lo rechaza en el momento de la escritura ni al enviar.

### Pasos para reproducir

1. Ir a `https://demoqa.com/automation-practice-form`
2. En el campo Mobile ingresar: `abcdefghij`
3. Completar demás campos obligatorios con datos válidos
4. Hacer click en "Submit"

### Resultado esperado

El campo debería:
- Aceptar únicamente dígitos numéricos
- Mostrar error si se ingresan letras: *"El número de teléfono solo puede contener dígitos."*

### Resultado obtenido

El campo acepta las letras sin mostrar ningún error. El formulario intenta enviarse aunque el número de teléfono no sea válido.

### Impacto

- Datos de contacto inválidos almacenados en el sistema
- Imposibilidad de contactar al usuario por teléfono
- En producción, podría generar errores en sistemas de SMS, verificación por teléfono, o CRMs

---

## OBS-001 — Sin límite máximo de caracteres en campos de texto

| Campo | Detalle |
|---|---|
| **ID** | OBS-001 |
| **Tipo** | Observación de comportamiento |
| **Severidad** | Baja |
| **Módulo** | Validación — Campos de texto |
| **Estado** | Abierto |
| **Caso relacionado** | TC-005 |

### Descripción

Los campos de texto del formulario (First Name, Last Name) no tienen definido un límite máximo de caracteres. Es posible ingresar cadenas de 200 o más caracteres sin ningún tipo de restricción o advertencia.

### Comportamiento esperado

Los campos deberían tener un límite razonable (ej: 50 caracteres para nombres) con un mensaje de advertencia al alcanzarlo.

### Impacto

- Sin límite definido, podrían generarse entradas excesivamente largas que afecten el almacenamiento o la visualización
- Inconsistencia en la experiencia de usuario — no hay feedback sobre límites permitidos

---

## OBS-002 — El formulario acepta fechas futuras como fecha de nacimiento

| Campo | Detalle |
|---|---|
| **ID** | OBS-002 |
| **Tipo** | Observación de comportamiento |
| **Severidad** | Media |
| **Módulo** | Date of Birth |
| **Estado** | Abierto |
| **Caso relacionado** | TC-015 |

### Descripción

El campo Date of Birth no valida que la fecha seleccionada sea anterior a la fecha actual. Es posible registrar una fecha de nacimiento en el futuro sin que el sistema muestre ningún error.

### Comportamiento esperado

El sistema debería validar que la fecha de nacimiento sea:
- Anterior a la fecha actual
- Razonablemente válida (ej: no más de 120 años en el pasado)

### Impacto

- Permite el registro de fechas de nacimiento imposibles (ej: año 2090)
- En producción podría afectar cálculos de edad, elegibilidad de servicios o verificaciones de identidad

---

## Resumen

| ID | Tipo | Descripción | Severidad | Estado |
|---|---|---|---|---|
| BUG-001 | Bug | First Name acepta espacios en blanco | Media | Abierto |
| BUG-002 | Bug | First Name acepta caracteres especiales | Media | Abierto |
| BUG-003 | Bug | Mobile acepta letras | Alta | Abierto |
| OBS-001 | Observación | Sin límite de caracteres en campos de texto | Baja | Abierto |
| OBS-002 | Observación | Fechas futuras aceptadas como nacimiento | Media | Abierto |
