# Reto: Agente de Onboarding Dinámico (KYC)

## Contexto

Una entidad financiera está modernizando su proceso de apertura digital de cuentas. Durante el registro, los usuarios deben tomar o cargar una fotografía de su documento de identidad para validar su información.

Una parte importante de los usuarios abandona el proceso cuando la imagen es rechazada por problemas como brillo excesivo, poca iluminación, desenfoque, documento recortado o información ilegible. Actualmente, la aplicación muestra mensajes genéricos que no explican qué ocurrió ni cómo corregirlo.

El equipo necesita construir una experiencia de recuperación asistida: cuando la validación del documento falle, un agente conversacional debe intervenir de manera amable, explicar la causa y orientar al usuario para que pueda tomar una nueva fotografía sin perder el progreso ni cerrar la sesión.

> **Nota:** La aplicación será un prototipo de demostración. No deberá procesar documentos reales ni almacenar información personal.

## Objetivo

Desarrollar una aplicación que simule una experiencia móvil de onboarding KYC (*Know Your Customer*) y permita:

- Cargar o seleccionar una fotografía simulada de un documento de identidad.
- Ejecutar una validación ficticia de la calidad de la imagen.
- Identificar y mostrar el motivo específico del rechazo.
- Activar un agente conversacional que entregue recomendaciones claras y contextuales.
- Permitir que el usuario vuelva a intentar la carga sin reiniciar el proceso.
- Completar exitosamente el onboarding cuando se utilice una imagen válida.

La solución puede desarrollarse con el **stack tecnológico que el equipo prefiera**.

## Alcance técnico

### 1. Experiencia de onboarding

La aplicación debe representar una experiencia optimizada para dispositivos móviles o Aplicación web responsiva e incluir, como mínimo:

- Encabezado o indicador del paso actual del proceso.
- Área para cargar, arrastrar o seleccionar una imagen de prueba.
- Vista previa de la imagen seleccionada.
- Botón para iniciar la validación.
- Estado visible del análisis: pendiente, procesando, aprobado o rechazado.
- Opción para reemplazar la imagen y volver a intentarlo.

### 2. Simulación de validación

No es obligatorio implementar visión artificial ni OCR. La aplicación puede determinar el resultado mediante:

- El nombre del archivo.
- Metadatos o una configuración local asociada a cada imagen.
- Reglas simuladas definidas en el código.
- Una selección manual del escenario, si se identifica claramente como control de demostración.

La validación debe reconocer al menos estos resultados:

| Código | Escenario | Resultado esperado |
|---|---|---|
| `VALID` | Documento legible y completo | Aprobado |
| `GLARE` | Reflejo o brillo excesivo | Rechazado |
| `DARK` | Iluminación insuficiente | Rechazado |
| `CROPPED` | Bordes o datos fuera de la imagen | Rechazado |
| `BLURRY` | Imagen desenfocada | Rechazado |

### 3. Agente de asistencia

Cuando la imagen sea rechazada, la aplicación debe abrir automáticamente un chat o panel de ayuda. El agente debe:

- Saludar de forma breve y empática.
- Explicar el motivo específico del rechazo en lenguaje sencillo.
- Entregar entre dos y tres acciones concretas para corregirlo.
- Invitar al usuario a tomar o cargar una nueva fotografía.
- Mantener el contexto del error durante la conversación.
- Evitar mensajes alarmistas, lenguaje técnico innecesario o atribuir la culpa al usuario.

Ejemplo para el escenario `GLARE`:

> No pudimos leer algunos datos porque hay un reflejo sobre el documento. Intenta colocarlo sobre una superficie plana, evita usar el flash y toma la foto con luz indirecta. Cuando estés listo, puedes intentarlo nuevamente.

En el alcance base, las respuestas pueden estar predefinidas o generarse mediante reglas locales.

### 4. Estados y continuidad

La interfaz debe manejar claramente los estados principales del proceso:

1. Esperando documento.
2. Imagen seleccionada.
3. Validando.
4. Validación rechazada y agente activo.
5. Nuevo intento.
6. Validación aprobada.

El usuario no debe perder su avance al recibir un rechazo. No es necesario implementar autenticación, base de datos ni persistencia permanente.

### 5. Experiencia visual y accesibilidad

- Diseño responsivo con prioridad para una pantalla móvil.
- Mensajes de estado que no dependan exclusivamente del color.
- Controles con etiquetas comprensibles y navegación básica mediante teclado.
- Indicadores visibles durante la validación simulada.
- Diferenciación clara entre mensajes del usuario y del agente.

## Imágenes de prueba

El repositorio incluye `data/` con imágenes ficticias o intervenidas. No se deben utilizar documentos ni datos personales reales.

Las imágenes pueden ser creadas por el equipo o sustituirse por recursos gráficos equivalentes.

## Flujo sugerido

1. El usuario abre la aplicación y visualiza el paso de verificación de identidad.
2. La aplicación explica brevemente cómo tomar una fotografía adecuada.
3. El usuario carga o selecciona una imagen de `carpeta_imagenes/`.
4. La aplicación muestra la vista previa y habilita la acción **Validar documento**.
5. Se simula el análisis durante un periodo corto y se presenta el resultado.
6. Si la imagen falla:
   - Se muestra el motivo del rechazo.
   - El agente abre el chat automáticamente.
   - El agente entrega instrucciones asociadas al tipo de error.
   - El usuario puede hacer preguntas o iniciar un nuevo intento.
7. Si la imagen es válida:
   - Se muestra un estado de aprobación.
   - Se habilita la acción **Continuar**.
8. El usuario completa el flujo sin recargar la página ni perder su estado.

## Reglas

- La experiencia debe estar diseñada principalmente para dispositivos móviles, aunque también debe funcionar en escritorio.
- La validación de imágenes puede ser simulada; no se requiere integrar servicios reales de identidad, biometría, OCR o visión artificial.
- Cada imagen de prueba debe producir un resultado determinista y reproducible.
- El mensaje del agente debe variar según el motivo del rechazo.
- El chat no puede bloquear la posibilidad de cargar una nueva imagen.
- No se deben utilizar, solicitar, transmitir ni almacenar documentos de identidad reales.

## Criterios de aceptación

La solución se considerará completa cuando cumpla todos los siguientes puntos:

- [ ] La aplicación presenta una interfaz responsiva que simula un onboarding móvil.
- [ ] El usuario puede cargar o seleccionar una imagen y visualizarla antes de validarla.
- [ ] Existe un estado visible de procesamiento durante la validación.
- [ ] La aplicación reconoce al menos una imagen válida y cuatro tipos diferentes de fallo.
- [ ] Cada archivo de prueba activa consistentemente el resultado esperado.
- [ ] Ante un rechazo, el chat del agente se abre automáticamente sin cerrar ni reiniciar la sesión.
- [ ] El agente explica la causa del fallo y ofrece recomendaciones específicas para solucionarlo.
- [ ] El usuario puede reemplazar la imagen y realizar varios intentos dentro del mismo flujo.
- [ ] Una imagen válida permite finalizar la verificación y avanzar al siguiente paso.
- [ ] Los estados aprobado y rechazado se comunican con texto o iconografía, además del color.

## Bonus adicional: respuestas con un LLM mediante GitHub Copilot SDK

Como extensión opcional, reemplazar las respuestas predefinidas del agente por respuestas generadas mediante un modelo de lenguaje real utilizando **GitHub Copilot SDK**.

El bonus debe:

- Crear una sesión del agente y enviarle el diagnóstico simulado de la imagen.
- Utilizar un mensaje de sistema que defina al agente como asistente de onboarding KYC, con tono empático, breve y orientado a la acción.
- Mantener el contexto de la conversación durante los mensajes de seguimiento.
- Restringir las respuestas al proceso de captura y calidad del documento.
- Indicar explícitamente cuando una solicitud se encuentre fuera del alcance del agente.
- Manejar estados de carga, errores de conexión y respuestas vacías.
- Ofrecer una respuesta local de respaldo si el modelo o el SDK no están disponibles.

El modelo debe convertir ese contexto en una orientación natural y útil, pero **no debe modificar el resultado de la validación** ni afirmar que realizó una verificación de identidad real.

