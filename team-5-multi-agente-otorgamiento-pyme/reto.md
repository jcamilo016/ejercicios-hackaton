# Reto: Escuadrón Multiagente para Otorgamiento de Crédito Pyme

## Contexto

El análisis de crédito para pequeñas y medianas empresas suele ser un proceso lento y manual. Un analista debe revisar estados financieros extensos o desordenados, identificar las cifras relevantes, calcular indicadores, contrastar los resultados con las políticas internas de riesgo y redactar un memorando para el comité de crédito.

El reto consiste en representar este proceso mediante un **escuadrón de agentes especializados** que colaboren para evaluar la salud financiera de una empresa y recomendar un cupo de crédito. La aplicación debe permitir observar cómo cada agente recibe información, ejecuta su responsabilidad y entrega sus resultados al siguiente participante del flujo.

La solución se construirá con ayuda de **GitHub Copilot** y podrá usar cualquier stack tecnológico de frontend.

> **Importante:** la recomendación generada por la aplicación no reemplaza la decisión de un analista. La aprobación o el rechazo del desembolso siempre debe quedar en manos de una persona.

## Objetivo

Construir una aplicación web que permita cargar los estados financieros de una Pyme y un manual de políticas de riesgo, simular la colaboración de varios agentes y presentar al usuario un memorando de crédito sugerido.

La aplicación deberá:

- Extraer y organizar los principales datos financieros de la empresa.
- Calcular indicadores financieros relevantes.
- Comparar los resultados con las políticas del banco.
- Formular una recomendación de crédito explicable.
- Mostrar el intercambio de información entre los agentes.
- Solicitar una decisión final humana antes de aprobar o rechazar el desembolso.

## Alcance Técnico

### Aplicación frontend

La solución puede implementarse con cualquier stack de desarrollo frontend. Debe ejecutarse localmente, contar con una interfaz web responsive y ofrecer una experiencia clara para una demostración en vivo.

No es obligatorio desarrollar un backend para la versión base. La lectura y el procesamiento de los archivos pueden realizarse en el navegador, y las respuestas de los agentes pueden provenir de datos predefinidos, reglas determinísticas o funciones simuladas.

### Escuadrón de agentes

La aplicación debe representar, como mínimo, los siguientes roles:

1. **Agente Lector Financiero**
   - Lee el archivo de estados financieros.
   - Identifica y normaliza conceptos como activos, pasivos, patrimonio, ingresos, utilidad, efectivo y deuda.
   - Advierte datos faltantes, inconsistentes o ambiguos.

2. **Agente Analista Financiero**
   - Recibe la información normalizada.
   - Calcula indicadores como liquidez corriente, nivel de endeudamiento, margen neto y cobertura de deuda.
   - Resume fortalezas y señales de alerta.

3. **Agente de Riesgo y Políticas**
   - Consulta el manual de riesgo.
   - Evalúa cada indicador contra los límites definidos.
   - Clasifica el riesgo y determina si la solicitud cumple, incumple o requiere revisión.

4. **Agente Redactor de Crédito**
   - Consolida los hallazgos de los demás agentes.
   - Genera un memorando sugerido con recomendación, cupo propuesto, condiciones, alertas y justificación.

5. **Comité de Crédito Humano**
   - Revisa el memorando y las evidencias.
   - Decide si aprueba o rechaza el desembolso.
   - Puede registrar una observación antes de confirmar la decisión.

### Interfaz mínima sugerida

La interfaz debe incluir:

- Área para cargar o seleccionar los dos archivos de entrada.
- Resumen de la empresa y de las cifras financieras identificadas.
- Visualización de los agentes y su estado: pendiente, procesando, completado, con advertencias o error.
- Línea de tiempo, panel de actividad o conversación que muestre el paso de información entre agentes.
- Panel de indicadores con valor, fórmula, umbral, resultado y nivel de riesgo.
- Memorando de crédito sugerido.
- Acciones humanas para **Aprobar desembolso** o **Rechazar solicitud**.
- Estado final y registro de la decisión tomada.

### Simulación de agentes

En la versión base se permite simular la operación de los agentes. La simulación debe:

- Generar resultados consistentes con los archivos cargados.
- Mostrar una secuencia perceptible de ejecución.
- Incluir mensajes o eventos que evidencien la colaboración.
- Manejar estados de carga, error y datos incompletos.
- Evitar resultados puramente aleatorios que no puedan explicarse a partir de los insumos.

## Archivos de Entrada

Los participantes recibirán o deberán crear los siguientes archivos en el repositorio:

### `estados_financieros_pyme.txt`

Transcripción semiestructurada de los estados financieros de una empresa. Puede contener títulos inconsistentes, separadores distintos, observaciones y cifras expresadas en pesos o millones de pesos.

### `manual_riesgo_pymes.md`

Documento con las políticas del banco, fórmulas, límites y condiciones de otorgamiento.

## Flujo Sugerido

1. El usuario abre la aplicación y consulta una breve explicación del proceso.
2. Carga `estados_financieros_pyme.txt` y `manual_riesgo_pymes.md`.
3. La aplicación valida los archivos y habilita la acción **Iniciar análisis**.
4. El Agente Lector extrae y normaliza las cifras, dejando visibles sus hallazgos y advertencias.
5. El Agente Analista calcula los indicadores y entrega sus resultados al Agente de Riesgo.
6. El Agente de Riesgo consulta las políticas, evalúa los umbrales y genera una clasificación fundamentada.
7. El Agente Redactor consolida la información y produce el memorando sugerido.
8. El usuario revisa el memorando, las fórmulas, las fuentes y las alertas.
9. El comité humano aprueba o rechaza la solicitud y, opcionalmente, agrega un comentario.
10. La aplicación presenta el estado final y conserva un registro visible de la decisión durante la sesión.

## Reglas

- Deben intervenir al menos cuatro agentes especializados y un responsable humano.
- Cada agente debe tener un propósito, una entrada y una salida claramente identificables.
- La interfaz debe evidenciar el intercambio de información entre los agentes; no basta con mostrar únicamente el resultado final.
- Los cálculos financieros deben ser determinísticos, verificables y mostrar la fórmula utilizada.
- La aplicación debe indicar qué regla del manual respalda cada evaluación.
- La recomendación debe diferenciar claramente hechos, cálculos, alertas y conclusiones.
- No se deben inventar cifras ausentes. Los datos faltantes deben señalarse y, si afectan una decisión, solicitar revisión humana.
- Ningún agente puede ejecutar o marcar automáticamente la aprobación del desembolso.
- Los botones de decisión solo deben habilitarse cuando el análisis haya finalizado.
- Antes de confirmar la decisión humana, la aplicación debe solicitar una confirmación explícita.
- No deben incluirse datos personales reales ni información bancaria confidencial en los archivos de demostración.
- Los secretos, tokens o credenciales nunca deben almacenarse en el repositorio ni exponerse en el código que se ejecuta en el navegador.
- La solución debe incluir un `README.md` con instrucciones de instalación, ejecución, uso y una explicación breve de la arquitectura.

## Criterios de Aceptación

El reto se considera completado cuando:

- [ ] La aplicación permite cargar los dos archivos requeridos y valida su presencia y formato.
- [ ] Se muestran al menos cuatro agentes con responsabilidades diferenciadas.
- [ ] El usuario puede observar el orden de ejecución y los mensajes intercambiados entre los agentes.
- [ ] Las principales cifras financieras se extraen y presentan de forma estructurada.
- [ ] Se calculan, como mínimo, liquidez corriente, endeudamiento, margen neto y cobertura de deuda.
- [ ] Cada indicador muestra su fórmula, resultado, umbral aplicable y estado de cumplimiento.
- [ ] Las políticas utilizadas pueden rastrearse hasta el archivo `manual_riesgo_pymes.md`.
- [ ] La aplicación muestra alertas ante datos faltantes, inconsistencias o incumplimientos.
- [ ] Se genera un memorando con resumen ejecutivo, análisis, riesgos, cupo recomendado, condiciones y justificación.
- [ ] El cupo recomendado respeta las restricciones definidas en el manual.
- [ ] El resultado de los agentes se presenta como una recomendación y no como una aprobación definitiva.
- [ ] Solo una acción humana permite aprobar o rechazar la solicitud.
- [ ] La decisión requiere confirmación y queda visible en el registro de la sesión.
- [ ] La interfaz funciona correctamente en resoluciones de escritorio y móvil.
- [ ] El repositorio contiene instrucciones suficientes para ejecutar la aplicación localmente.

## Bonus Adicional: agentes reales con GitHub Copilot SDK

Como extensión opcional, reemplazar total o parcialmente las respuestas simuladas por agentes reales implementados mediante **GitHub Copilot SDK**.

El bonus puede incluir:

- Una sesión o agente independiente por cada rol del escuadrón, con instrucciones específicas.
- Un orquestador que controle el orden de ejecución y el contexto que recibe cada agente.
- Salidas estructuradas y validadas antes de compartirlas con otro agente.
- Trazabilidad de solicitudes, respuestas, duración, errores y reintentos.
- Referencias a los fragmentos de los archivos que fundamentan cada conclusión.
- Controles para cancelar el análisis o reintentar únicamente el agente que falló.
- Un modo seleccionable entre **Simulación** y **Agentes reales**.

### Criterios para obtener el bonus

- [ ] Al menos dos agentes utilizan un LLM real y colaboran mediante información estructurada.
- [ ] La aplicación identifica visualmente qué pasos fueron simulados y cuáles fueron generados por un modelo.
- [ ] Los fallos del modelo se controlan sin perder el análisis completo ni bloquear la interfaz.
- [ ] Las respuestas generadas incluyen evidencia o referencia al insumo utilizado.
- [ ] Las credenciales se administran de forma segura y no se publican en el repositorio.
- [ ] La intervención humana permanece obligatoria para la decisión final.
