# Reto: Validador de Contratos de Proveedores

## Contexto

El área Legal y de Procurement de una entidad financiera recibe contratos de proveedores de tecnología que deben revisarse antes de su firma. Actualmente, la revisión se realiza de forma manual y puede tardar varios días o incluso semanas, debido a que cada documento debe compararse con las políticas internas del banco.

La revisión busca confirmar que el contrato incluya cláusulas obligatorias relacionadas, entre otros temas, con protección de datos personales, niveles de servicio (SLA), confidencialidad, seguridad de la información, multas, continuidad del negocio y terminación contractual.

El reto consiste en desarrollar una aplicación web que ayude al equipo legal a identificar rápidamente cláusulas cumplidas, incompletas o ausentes, mostrando los riesgos encontrados y una recomendación clara para cada punto del checklist.

> **Nota:** La aplicación es una herramienta de apoyo para una demostración y no reemplaza la revisión ni el concepto de un profesional legal.

## Objetivo

Construir una aplicación web denominada **Validador de Contratos** que permita:

1. Cargar un contrato propuesto por un proveedor.
2. Cargar un checklist con las cláusulas y condiciones obligatorias.
3. Ejecutar una validación simulada del contrato contra cada punto del checklist.
4. Visualizar un resumen general del nivel de cumplimiento.
5. Consultar la evidencia encontrada, el riesgo detectado y una recomendación por cada validación.
6. Facilitar la revisión humana antes de aprobar o rechazar el contrato.

La experiencia debe comunicar los resultados de forma visual, simple y trazable, utilizando estados tipo semáforo.

## Alcance Técnico

### 1. Carga de archivos

- Permitir cargar mediante un selector o una zona de arrastrar y soltar:
  - Un contrato en formato `.pdf`.
  - Un checklist legal en formato `.md`.
- Mostrar el nombre, tipo y tamaño de cada archivo cargado.
- Validar que ambos archivos estén disponibles antes de habilitar el análisis.
- Mostrar mensajes claros cuando un archivo tenga un formato incorrecto o no pueda procesarse.

### 2. Procesamiento del contrato

- Extraer el texto del PDF en el navegador.
- Interpretar los puntos definidos en el archivo Markdown.
- Relacionar cada punto del checklist con una sección o fragmento del contrato.
- Para efectos del reto, el análisis semántico puede ser **simulado** mediante reglas, términos equivalentes, expresiones regulares y datos mock.
- No debe depender únicamente de coincidencias exactas: debe contemplar sinónimos o expresiones equivalentes. Por ejemplo, “protección de información personal” puede estar relacionada con “tratamiento de datos personales”.
- No se requiere backend, base de datos ni integración con un LLM para completar el alcance principal.

### 3. Estados de validación (sugerido)

Cada punto del checklist debe clasificarse en uno de los siguientes estados:

| Estado | Color sugerido | Descripción |
|---|---|---|
| Cumple | Verde | La cláusula fue identificada y cubre el requerimiento esperado. |
| Revisión requerida | Amarillo | Existe una cláusula relacionada, pero es ambigua, parcial o insuficiente. |
| No cumple | Rojo | La cláusula no fue encontrada o contradice el checklist. |

### 4. Panel de resultados (sugerido)

La pantalla de resultados debe incluir:

- Nombre del contrato y fecha/hora del análisis.
- Porcentaje general de cumplimiento.
- Cantidad de validaciones por estado.
- Barra de progreso o indicador visual del resultado general.
- Listado de todos los puntos del checklist.
- Filtros por estado y una búsqueda por texto.
- Para cada validación:
  - Nombre y descripción del requisito.
  - Estado obtenido.
  - Evidencia o fragmento del contrato relacionado.
  - Explicación breve del hallazgo.
  - Nivel de riesgo: bajo, medio, alto o crítico.
  - Recomendación para corregir el hallazgo.
  - Propuesta de redacción cuando la cláusula esté ausente o incompleta.

### 5. Detalle y revisión humana

- Permitir seleccionar una validación para consultar su detalle.
- Permitir que el usuario marque el punto como revisado.
- Permitir registrar una observación del revisor.
- Permitir cambiar manualmente el estado sugerido por la aplicación.
- Diferenciar visualmente el resultado automático del resultado ajustado por el revisor.

## Stack Tecnológico

- **React** para la construcción de la interfaz.
- **TypeScript** para componentes, modelos de datos y lógica de validación tipada.
- **Tailwind CSS** para estilos y diseño responsivo.
- **Vite** como herramienta recomendada de desarrollo y compilación.
- **Lucide React** para iconografía, opcionalmente.
- **pdfjs-dist** o una alternativa equivalente para extraer texto del PDF en el navegador.
- API nativa `FileReader` para leer el checklist Markdown.
- `localStorage`, opcionalmente, para conservar observaciones y ajustes del revisor.

## Archivos de Entrada

Los siguientes archivos pueden usarse para facilitar la demostración.

### `contrato_proveedor.pdf`

Contrato ficticio de prestación de servicios tecnológicos.

### `checklist_legal.md`

Archivo que contiene los puntos obligatorios de validación.

## Flujo Sugerido

1. El usuario abre la aplicación y encuentra una explicación breve del propósito de la herramienta.
2. Carga `contrato_proveedor.pdf` y `checklist_legal.md`.
3. La aplicación valida los formatos y habilita el botón **Analizar contrato**.
4. Al iniciar el análisis, se muestra un indicador de progreso con mensajes como “Extrayendo texto”, “Evaluando cláusulas” y “Generando recomendaciones”.
5. La aplicación procesa o simula la comparación del contrato contra el checklist.
6. Se presenta un dashboard con el porcentaje de cumplimiento y la distribución de estados.
7. El usuario filtra los hallazgos y abre el detalle de los puntos con revisión requerida o incumplimiento.
8. El usuario consulta la evidencia, la explicación y la propuesta de cláusula.
9. El revisor añade una observación, cambia el estado si corresponde y marca el punto como revisado.
10. El usuario puede reiniciar el proceso y analizar otro contrato.

## Bonus Adicional: Administración del Checklist

Incorporar una sección que permita administrar los puntos de validación sin modificar manualmente el archivo Markdown.

La funcionalidad bonus debe permitir:

- Crear un nuevo punto del checklist.
- Editar un punto existente.
- Configurar identificador, nombre, descripción, nivel de riesgo, criterios esperados y términos relacionados.
- Validar campos obligatorios y evitar identificadores duplicados.
- Activar o desactivar puntos sin eliminarlos.
- Confirmar los cambios antes de guardarlos.
- Persistir los cambios en `localStorage`.
- Exportar el checklist actualizado en formato Markdown.
- Utilizar los puntos modificados en un nuevo análisis del contrato.

Como mejora opcional dentro del bonus, se puede permitir eliminar puntos con confirmación previa y restaurar el checklist original.

## Criterios de Aceptación

### Carga y validación de archivos

- [ ] La aplicación permite cargar un archivo PDF y un archivo Markdown.
- [ ] Se muestran el nombre, tipo y tamaño de los archivos seleccionados.
- [ ] El botón de análisis solo se habilita cuando ambos archivos son válidos.
- [ ] Los errores de formato o lectura se muestran de forma comprensible.

### Procesamiento

- [ ] El texto del contrato se extrae o se representa mediante una simulación claramente encapsulada.
- [ ] La aplicación interpreta al menos 10 puntos del checklist.
- [ ] Cada punto genera un resultado reproducible con estado, riesgo, evidencia, explicación y recomendación.
- [ ] La validación reconoce al menos algunos términos equivalentes y no solo coincidencias literales.

### Resultados

- [ ] El dashboard presenta el porcentaje general de cumplimiento.
- [ ] Se muestran las cantidades de puntos que cumplen, requieren revisión y no cumplen.
- [ ] Todos los puntos se visualizan con una etiqueta de estado accesible.
- [ ] Es posible filtrar los resultados por estado y buscarlos por texto.
- [ ] Los puntos incompletos o ausentes incluyen una propuesta de redacción.
- [ ] El porcentaje y los contadores coinciden con el detalle de resultados.

### Revisión humana

- [ ] El usuario puede abrir el detalle de cada validación.
- [ ] El usuario puede registrar una observación y marcar el punto como revisado.
- [ ] El usuario puede modificar el estado sugerido.
- [ ] La interfaz diferencia el resultado automático del ajuste manual.

### Experiencia de usuario y calidad técnica

- [ ] La interfaz es clara, responsiva y mantiene una jerarquía visual consistente.
- [ ] Existen estados visibles para carga, procesamiento, éxito, error y reinicio.
- [ ] La aplicación muestra una advertencia indicando que el análisis no constituye asesoría legal.

### Bonus

- [ ] Es posible crear y editar puntos del checklist desde la interfaz.
- [ ] Los formularios validan los datos obligatorios y los identificadores duplicados.
- [ ] Los cambios se conservan en `localStorage` y se usan en análisis posteriores.
- [ ] El checklist actualizado puede exportarse como archivo Markdown.

### Skill recomendado para React

Como sugerencia, se recomienda instalar el skill `vercel-react-best-practices` para orientar la implementación y revisión del código React según las prácticas de rendimiento de Vercel Engineering.

Ejecutar el siguiente comando desde la raíz del proyecto:

```bash
npx skills add vercel-labs/agent-skills
```

En el selector interactivo, marcar `vercel-react-best-practices` con la barra espaciadora y confirmar la instalación con Enter, como se muestra en el siguiente ejemplo:

![Selección del skill vercel-react-best-practices durante la instalación](img/vercel-skill.png)
