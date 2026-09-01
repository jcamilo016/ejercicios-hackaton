# Reto: Triage Inteligente de Phishing

## Contexto

Una entidad bancaria recibe diariamente cientos de reportes de empleados sobre correos electrónicos sospechosos. El equipo del Centro de Operaciones de Seguridad (SOC) debe revisar cada reporte, identificar posibles indicadores de compromiso y decidir qué casos requieren atención inmediata.

El volumen de solicitudes supera la capacidad de análisis manual del equipo. Esta demora puede permitir que una campaña de phishing, el robo de credenciales o la distribución de ransomware afecte la red corporativa en cuestión de minutos.

El reto consiste en construir una aplicación que funcione como primera línea de defensa y ayude al SOC a clasificar, priorizar y explicar automáticamente los correos reportados.

> **Importante:** todos los datos utilizados en el reto son ficticios. La aplicación no debe ejecutar enlaces, abrir archivos adjuntos ni conectarse a dominios incluidos en los correos.

## Objetivo

Desarrollar una aplicación de **triage de phishing** que permita:

- Cargar una colección de correos electrónicos simulados desde un archivo JSON.
- Analizar las señales de riesgo presentes en cada correo.
- Extraer y visualizar indicadores de compromiso, como URLs, dominios, direcciones de correo y nombres de archivos adjuntos.
- Clasificar cada reporte según su nivel de amenaza.
- Explicar de forma clara por qué un correo fue clasificado como legítimo o peligroso.
- Priorizar los casos críticos en un panel con apariencia de Centro de Operaciones de Seguridad.
- Incorporar intervención humana antes de ejecutar una acción de contención sobre los casos severos.

La solución puede implementarse con un **stack tecnológico de libre elección**. El análisis puede estar basado en reglas, datos simulados o lógica local; no es obligatorio utilizar servicios externos ni un backend.

## Alcance Técnico

### 1. Carga de datos

La aplicación debe permitir seleccionar o cargar el archivo `reportes_phishing.json` y validar que su estructura sea correcta.

Debe manejar, como mínimo, los siguientes estados:

- Archivo pendiente de carga.
- Archivo procesándose.
- Archivo cargado correctamente.
- Archivo vacío, inválido o con registros incompletos.

### 2. Panel SOC

La vista principal debe simular un panel de un SOC y mostrar, como mínimo:

- Total de correos analizados.
- Cantidad de casos por nivel de amenaza.
- Cantidad de casos pendientes de revisión humana.
- Listado de reportes ordenado por prioridad o nivel de riesgo.
- Filtros por nivel de amenaza, estado y texto de búsqueda.

### 3. Análisis de los correos

Para cada correo, la aplicación debe analizar al menos:

- Remitente y dominio del remitente.
- Diferencias entre el nombre visible y la dirección real del remitente.
- Asunto y contenido del mensaje.
- Lenguaje de urgencia, amenaza, premio o solicitud de credenciales.
- URLs y dominios presentes en el contenido.
- Uso de direcciones IP, acortadores, dominios similares o enlaces cuyo texto visible no coincide con su destino.
- Archivos adjuntos y extensiones potencialmente peligrosas.
- Cualquier indicador de suplantación incluido en los datos de prueba.

El análisis puede realizarse mediante reglas locales. No se requiere visitar las URLs ni inspeccionar archivos reales.

### 4. Clasificación y puntuación

Cada correo debe recibir:

- Un puntaje de riesgo entre `0` y `100`.
- Una clasificación: `Legítimo`, `Sospechoso`, `Alto` o `Severo`.
- Una lista de evidencias o razones que expliquen el resultado.
- Un estado operativo: `Pendiente`, `Analizado`, `Requiere revisión`, `Confirmado` o `Descartado`.

La interfaz debe diferenciar visualmente los niveles de amenaza mediante etiquetas, colores o iconos accesibles. El color no debe ser el único medio para comunicar la severidad.

### 5. Detalle del reporte

Al seleccionar un correo, la aplicación debe mostrar:

- Datos completos del reporte.
- Remitente, destinatario, asunto, fecha y cuerpo del correo.
- Puntaje y nivel de amenaza.
- Indicadores de compromiso extraídos.
- Reglas o señales activadas.
- Explicación legible del resultado.
- Estado y acciones disponibles.

### 6. Human-in-the-Loop

Los correos clasificados como `Severo` deben requerir confirmación humana. La vista de detalle debe incluir la acción **“Aislar IP del empleado”**.

Al utilizarla, la aplicación debe:

1. Mostrar una confirmación con el usuario o equipo afectado y el motivo de la acción.
2. Permitir cancelar o confirmar la operación.
3. Simular la contención sin ejecutar acciones reales de red.
4. Actualizar el estado del reporte y registrar visualmente la decisión.

También debe ser posible marcar un reporte como falso positivo o descartarlo, conservando evidencia de la decisión tomada.

### 7. Persistencia y comportamiento

No es obligatorio utilizar una base de datos. El estado puede mantenerse en memoria o en el almacenamiento local del navegador. Si la página se recarga y no existe persistencia, la aplicación debe volver a un estado inicial coherente.

## Archivos de Prueba

### `reportes_phishing.json`

Archivo principal con una colección de correos simulados. Debe incluir casos legítimos y maliciosos con diferentes niveles de dificultad.

## Flujo Sugerido

1. El analista abre la aplicación y visualiza el estado inicial del panel SOC.
2. Carga el archivo `reportes_phishing.json`.
3. La aplicación valida el archivo y analiza cada correo.
4. Se calculan el puntaje, la severidad y las evidencias de cada reporte.
5. El panel actualiza sus indicadores y ordena primero los casos de mayor riesgo.
6. El analista utiliza filtros o el buscador para explorar los resultados.
7. Selecciona un reporte y revisa el correo, los indicadores extraídos y la explicación.
8. Si el caso es severo, confirma o cancela la acción simulada **“Aislar IP del empleado”**.
9. El analista también puede confirmar la amenaza o marcar el caso como falso positivo.
10. El panel refleja el nuevo estado y mantiene un registro visual de la decisión.

## Reglas

1. La aplicación debe funcionar con un stack de libre elección y documentar cómo ejecutarla localmente.
2. El análisis debe producir siempre un puntaje, una clasificación y al menos una explicación por correo válido.
3. La clasificación no puede depender únicamente de una palabra; debe considerar una o más señales del mensaje.
4. Una señal individual puede aumentar el riesgo, pero las combinaciones de señales deben tener mayor peso.
5. Los casos severos no pueden ejecutar la acción de contención sin confirmación humana explícita.
6. La acción **“Aislar IP del empleado”** es exclusivamente una simulación y no debe realizar llamadas reales a infraestructura.
7. La aplicación no debe navegar hacia las URLs, descargar adjuntos ni ejecutar contenido de los datos de prueba.
8. Los valores esperados del archivo no deben mostrarse como si fueran el resultado del análisis ni utilizarse para calcularlo.
9. Los registros inválidos deben reportarse de forma clara sin impedir el procesamiento de los demás registros válidos.
10. Los filtros, contadores y estados deben mantenerse sincronizados después de cada decisión del analista.
11. La interfaz debe ser responsiva y permitir una demostración adecuada en una pantalla de escritorio.

### Referencia sugerida para la severidad

| Puntaje | Clasificación | Comportamiento esperado |
| ---: | --- | --- |
| 0–24 | Legítimo | Mostrar como riesgo bajo |
| 25–49 | Sospechoso | Recomendar revisión |
| 50–74 | Alto | Priorizar en la cola del SOC |
| 75–100 | Severo | Requerir revisión humana y habilitar contención simulada |

Los rangos pueden ajustarse, siempre que la decisión esté documentada y sea consistente.

## Criterios de Aceptación

- [ ] La solución incluye instrucciones claras para instalarla y ejecutarla localmente.
- [ ] La aplicación permite cargar `reportes_phishing.json` desde la interfaz.
- [ ] Un archivo válido se procesa sin necesidad de modificar manualmente sus datos.
- [ ] Los registros inválidos se identifican sin bloquear los registros válidos.
- [ ] El panel muestra el total de reportes y el conteo por nivel de amenaza.
- [ ] Los correos aparecen ordenados o pueden ordenarse según su prioridad.
- [ ] El usuario puede filtrar por severidad y estado, y buscar reportes.
- [ ] Cada correo válido recibe un puntaje entre 0 y 100 y una clasificación visible.
- [ ] El detalle muestra el contenido del correo y los indicadores extraídos.
- [ ] La aplicación explica con razones concretas por qué considera peligroso o legítimo cada correo.
- [ ] Los casos legítimos y maliciosos del archivo de prueba producen resultados coherentes.
- [ ] Los casos severos quedan marcados como pendientes de revisión humana.
- [ ] La acción **“Aislar IP del empleado”** solo aparece o se habilita para casos severos.
- [ ] La acción de aislamiento solicita confirmación y simula correctamente el resultado.
- [ ] El analista puede confirmar una amenaza o marcarla como falso positivo.
- [ ] Los indicadores y estados del panel se actualizan después de una decisión humana.
- [ ] Ningún enlace o archivo adjunto de prueba se abre o ejecuta automáticamente.
- [ ] La interfaz es clara, responsiva y utiliza más de un recurso visual para comunicar la severidad.

## Bonus Adicional

- Permitir editar desde la interfaz las reglas, los pesos y los umbrales de clasificación.
- Incorporar gráficos sobre la distribución de amenazas y los indicadores más frecuentes.
- Exportar los resultados del análisis y el historial de decisiones a JSON o CSV.
- Integrar un modelo LLM para generar explicaciones o apoyar la clasificación, manteniendo reglas de seguridad y salidas estructuradas.
- Utilizar el **GitHub Copilot SDK** para implementar un agente especializado en análisis de phishing.
- Incluir trazabilidad de decisiones con fecha, acción y analista simulado.
