# Reto: Agente Asesor de Inversiones (Robo-Advisor)

## Contexto

Ante cambios bruscos del mercado, revisar y ajustar manualmente los portafolios de inversión puede ser un proceso lento, costoso y reservado para clientes con patrimonios elevados. Una institución financiera quiere explorar una experiencia digital que democratice este tipo de orientación mediante un agente capaz de relacionar noticias del mercado con la composición actual del portafolio de cada cliente.

El reto consiste en construir una aplicación demostrativa que simule un **agente asesor de inversiones (robo-advisor)**. La solución deberá leer titulares financieros ficticios, estimar su posible impacto y proponer una redistribución del portafolio, explicándola de manera clara y visual.

> **Importante:** la aplicación es únicamente una simulación con fines educativos. No debe presentarse como asesoría financiera real ni ejecutar transacciones.

## Objetivo

Desarrollar una aplicación web que permita:

1. Cargar información ficticia de clientes y sus portafolios actuales.
2. Cargar noticias financieras simuladas.
3. Seleccionar un cliente y analizar las noticias disponibles.
4. Clasificar el posible impacto de las noticias como positivo, negativo o neutral.
5. Generar una propuesta de redistribución del portafolio.
6. Comparar visualmente la distribución actual con la sugerida.
7. Mostrar un mensaje corto y persuasivo que explique la recomendación.

El stack tecnológico es de **libre elección**. Se valorará una solución simple, mantenible, visualmente atractiva y fácil de ejecutar localmente.

## Alcance Técnico

### Carga y validación de datos

- Permitir cargar o leer desde el repositorio los archivos `Master_Clientes.csv` y `noticias_mercado.txt`.
- Validar la estructura, los campos obligatorios y los valores numéricos.
- Informar claramente si un archivo no tiene el formato esperado.
- No enviar archivos ni datos a servicios externos, salvo cuando se implemente explícitamente el bonus con un LLM.

### Gestión de clientes

- Mostrar un listado o selector de clientes.
- Presentar datos básicos del cliente seleccionado: identificador, nombre, perfil de riesgo y valor total del portafolio.
- Mostrar la distribución actual por clase de activo.

### Análisis de noticias

- Mostrar los titulares cargados y su fecha.
- Analizar cada noticia mediante reglas simuladas o palabras clave.
- Asignar a cada titular:
  - impacto: `positivo`, `negativo` o `neutral`;
  - nivel: `alto`, `medio` o `bajo`;
  - activos potencialmente afectados;
  - explicación breve.
- Permitir ejecutar el análisis mediante una acción visible, por ejemplo, **Analizar mercado**.

### Motor de recomendación

- Generar una nueva distribución del portafolio a partir del perfil de riesgo del cliente y del impacto agregado de las noticias.
- Mantener el porcentaje de cada activo entre `0` y `100`.
- Garantizar que la suma de la distribución sugerida sea exactamente `100 %`.
- Evitar recomendaciones extremas: ningún activo podrá cambiar más de **20 puntos porcentuales** respecto de su asignación actual.
- Respetar límites mínimos de liquidez:
  - perfil conservador: al menos `10 %`;
  - perfil moderado: al menos `5 %`;
  - perfil agresivo: sin mínimo obligatorio.
- Permitir que la lógica sea determinística para que el mismo conjunto de datos produzca el mismo resultado.

### Explicación del agente

El agente deberá generar un mensaje breve que incluya:

- conclusión general sobre el contexto del mercado;
- principales cambios propuestos;
- motivo de la recomendación;
- referencia al perfil de riesgo del cliente;
- aclaración de que la decisión final corresponde al usuario.

## Archivos de Prueba

Los siguientes archivos deberán estar disponibles en el repositorio, preferiblemente dentro de una carpeta `data/`.

### `Master_Clientes.csv`

Contiene la información de los clientes y la distribución actual de sus portafolios.

### `noticias_mercado.txt`

Contiene titulares ficticios, uno por línea, con campos separados por `|`.

## Flujo Sugerido

1. El usuario abre la aplicación y visualiza la advertencia de simulación.
2. La aplicación carga los archivos de prueba incluidos o permite seleccionarlos manualmente.
3. El sistema valida los archivos y presenta mensajes claros si encuentra errores.
4. El usuario selecciona un cliente.
5. La aplicación muestra su perfil y portafolio actual.
6. El usuario revisa los titulares y pulsa **Analizar mercado**.
7. El sistema clasifica el impacto de las noticias y muestra un resumen del mercado.
8. El usuario pulsa **Generar recomendación**.
9. La aplicación calcula el portafolio sugerido, valida sus restricciones y muestra la comparación gráfica.
10. El agente presenta una explicación breve de la propuesta.
11. El usuario puede reiniciar el análisis, cambiar de cliente o cargar nuevos archivos.

## Criterios de Aceptación

La solución se considerará completa cuando:

- [ ] Permita cargar o utilizar `Master_Clientes.csv` y `noticias_mercado.txt`.
- [ ] Valide correctamente la estructura y el contenido de ambos archivos.
- [ ] Permita seleccionar cualquiera de los clientes válidos.
- [ ] Muestre la distribución actual del portafolio y el perfil de riesgo.
- [ ] Clasifique todas las noticias por impacto y nivel.
- [ ] Relacione cada noticia con uno o más tipos de activo.
- [ ] Genere una distribución sugerida cuya suma sea exactamente `100 %`.
- [ ] Respete el límite de cambio de 20 puntos porcentuales por activo.
- [ ] Respete el mínimo de liquidez correspondiente al perfil del cliente.
- [ ] Muestre al menos un gráfico comparativo entre el portafolio actual y el sugerido.
- [ ] Destaque visualmente los activos que aumentan, disminuyen o permanecen iguales.
- [ ] Genere una explicación breve, comprensible y relacionada con las noticias analizadas.
- [ ] Incluya estados de carga, errores y ausencia de datos.
- [ ] Muestre permanentemente que la recomendación es una simulación y no constituye asesoría financiera.
- [ ] Sea responsiva y utilizable en escritorio y dispositivos móviles.
- [ ] Incluya un `README.md` con el stack elegido y las instrucciones de ejecución.

## Bonus: agente con un LLM real mediante GitHub Copilot SDK

Como mejora adicional, reemplazar o complementar la explicación simulada con un agente respaldado por un modelo de lenguaje a través de **GitHub Copilot SDK**.

El agente deberá recibir únicamente información estructurada y ficticia:

- perfil de riesgo;
- portafolio actual;
- análisis de las noticias;
- portafolio sugerido;
- reglas y límites aplicados.

El LLM podrá:

- resumir el contexto del mercado;
- explicar en lenguaje natural los cambios propuestos;
- adaptar el tono al nivel de conocimiento del usuario;
- responder preguntas sobre la recomendación sin modificar los cálculos aprobados por el motor de reglas.

Condiciones del bonus:

- Los porcentajes deben ser calculados y validados por código; el LLM no será la fuente de verdad para cálculos financieros.
- La respuesta debe basarse exclusivamente en los datos entregados al modelo.
- El prompt del sistema debe impedir promesas de rentabilidad, recomendaciones absolutas o presentación de la respuesta como asesoría profesional.
- Debe existir manejo de errores, timeout y una respuesta simulada de respaldo si el modelo no está disponible.
- Las credenciales o tokens nunca deben quedar incluidos en el código fuente ni exponerse en el navegador.
- La integración y sus requisitos de configuración deben documentarse en el `README.md`.
- La interfaz debe indicar si el mensaje fue generado por el LLM o por el modo simulado.

### Criterios de aceptación del bonus

- [ ] La aplicación inicia una sesión o invocación válida mediante GitHub Copilot SDK.
- [ ] El agente recibe contexto estructurado y no archivos completos innecesarios.
- [ ] La respuesta hace referencia al cliente, su perfil y los cambios calculados.
- [ ] El LLM no altera los porcentajes definidos por el motor de recomendación.
- [ ] La aplicación continúa funcionando mediante un fallback local cuando el servicio no está disponible.
- [ ] No se exponen secretos en el repositorio, los logs ni la interfaz.
