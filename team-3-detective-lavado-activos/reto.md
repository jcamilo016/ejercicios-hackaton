# Reto: Agente Detective de Lavado de Activos (AML)

## Contexto

Los analistas de cumplimiento de una entidad financiera deben revisar un alto volumen de alertas asociadas a transferencias internacionales. Este proceso puede convertirse en un cuello de botella: retrasar una operación legítima afecta la experiencia del cliente, mientras que permitir una operación ilícita puede exponer a la entidad a riesgos financieros, legales y reputacionales.

El equipo necesita una herramienta visual que apoye el análisis inicial de las transacciones, contraste los participantes contra una lista restrictiva y determine si el monto transferido se desvía del comportamiento histórico del cliente.

> **Importante:** esta aplicación es una simulación educativa. No reemplaza un sistema AML real ni la decisión de un analista de cumplimiento.

## Objetivo

Construir con GitHub Copilot una aplicación web denominada **Agente Detective AML**, capaz de:

- Cargar y procesar un flujo simulado de transferencias internacionales.
- Validar los nombres de origen y destino contra una lista restrictiva.
- Comparar el monto de cada operación con el comportamiento histórico del cliente.
- Asignar un nivel de riesgo mediante un semáforo: **verde, amarillo o rojo**.
- Mostrar de forma clara los pasos ejecutados, las evidencias encontradas y la justificación del resultado.
- Permitir que un analista tome la decisión final sobre las operaciones que requieren revisión humana.

## Alcance técnico

La solución debe ser una aplicación **exclusivamente frontend**, ejecutada en el navegador y sin API, backend, base de datos ni servicios externos.

Debe incluir como mínimo:

1. **Carga de archivos**
   - Permitir seleccionar o arrastrar los tres archivos de entrada.
   - Validar el tipo de archivo y las columnas o propiedades obligatorias.
   - Mostrar mensajes comprensibles cuando los datos no sean válidos.

2. **Procesamiento de transacciones**
   - Leer archivos CSV y JSON desde el navegador.
   - Procesar las operaciones una a una o mediante una simulación automática con pausas breves.
   - Normalizar nombres para hacer comparaciones sin depender de mayúsculas, espacios adicionales o tildes.

3. **Motor de evaluación de riesgo**
   - Comparar ordenante y beneficiario con la lista restrictiva.
   - Relacionar cada transferencia con el historial del cliente.
   - Calcular la desviación entre el monto de la operación y el promedio histórico.
   - Aplicar reglas determinísticas, visibles y fáciles de modificar.

4. **Interfaz de investigación**
   - Resumen con totales de operaciones verdes, amarillas, rojas y pendientes.
   - Listado o tabla de transacciones con filtros por nivel de riesgo y estado.
   - Panel de detalle con datos de la operación, resultado de cada validación y evidencias.
   - Línea de tiempo o lista de pasos que represente el proceso de análisis.
   - Diseño responsivo, accesible y coherente con un entorno financiero.

5. **Human-in-the-loop**
   - Enviar las operaciones amarillas a una bandeja de revisión.
   - Permitir al analista elegir **Liberar fondos** o **Congelar fondos**.
   - Solicitar un comentario o justificación antes de confirmar la decisión.
   - Registrar visualmente la decisión, la fecha y el estado final durante la sesión.

## Stack tecnológico

- **React**
- **TypeScript** con tipado estricto
- **Tailwind CSS**
- **Vite** como herramienta de construcción y desarrollo
- **Papa Parse** o una alternativa equivalente para leer archivos CSV
- **Lucide React** para iconografía, opcional
- Estado local de React; no se requiere una librería global de estado
- `localStorage`, opcionalmente, para conservar las decisiones al recargar la página

## Archivos de entrada

Los archivos deberán estar disponibles en el repositorio como datos de demostración. Se pueden ajustar los nombres de los campos, siempre que se documenten y se mantenga la información mínima indicada.

### `transferencias_internacionales.json`

Representa el flujo de operaciones entrantes.

Campos mínimos sugeridos:

| Campo | Tipo | Descripción |
|---|---|---|
| `id` | string | Identificador único de la transferencia |
| `fecha` | string | Fecha y hora en formato ISO 8601 |
| `clienteId` | string | Identificador del cliente |
| `nombreOrigen` | string | Nombre de la persona o empresa que envía |
| `nombreDestino` | string | Nombre de la persona o empresa que recibe |
| `paisOrigen` | string | País de origen |
| `paisDestino` | string | País de destino |
| `monto` | number | Valor de la transferencia |
| `moneda` | string | Código de moneda, por ejemplo `USD` |

### `lista_restrictiva_mock.csv`

Contiene personas y empresas sancionadas o restringidas para efectos de la simulación.

Columnas mínimas sugeridas:

| Columna | Descripción |
|---|---|
| `id` | Identificador del registro |
| `nombre` | Nombre de la persona o empresa |
| `tipo` | Persona o empresa |
| `pais` | País asociado |
| `motivo` | Motivo simulado de inclusión |

### `historial_clientes.csv`

Resume el comportamiento habitual de cada cliente.

Columnas mínimas sugeridas:

| Columna | Descripción |
|---|---|
| `cliente_id` | Identificador del cliente |
| `nombre_cliente` | Nombre del cliente |
| `monto_promedio` | Monto promedio histórico |
| `monto_maximo_habitual` | Máximo considerado habitual |
| `numero_operaciones` | Cantidad histórica de operaciones |
| `moneda` | Moneda utilizada para los valores históricos |

## Flujo sugerido

1. El usuario abre la aplicación y visualiza una pantalla de bienvenida con instrucciones breves.
2. Carga los tres archivos requeridos o utiliza los archivos de demostración incluidos.
3. La aplicación valida la estructura y muestra un resumen de los registros cargados.
4. El usuario inicia el análisis de las transferencias.
5. Para cada operación, el sistema muestra una secuencia auditable:
   - **Paso 1:** lectura y validación de la transacción.
   - **Paso 2:** búsqueda del origen y destino en la lista restrictiva.
   - **Paso 3:** consulta del comportamiento histórico del cliente.
   - **Paso 4:** cálculo de indicadores y asignación del nivel de riesgo.
   - **Paso 5:** recomendación y siguiente acción.
6. Las operaciones verdes se marcan como de riesgo bajo; las rojas se marcan para bloqueo o investigación prioritaria; las amarillas pasan a revisión humana.
7. El analista revisa la evidencia de una operación amarilla, registra su justificación y decide liberar o congelar los fondos.
8. El tablero actualiza los contadores y conserva un historial visible de las decisiones tomadas durante la sesión.

## Reglas y expectativas

### Reglas funcionales mínimas

El equipo debe implementar y documentar una política de riesgo determinística. Como punto de partida puede utilizar las siguientes reglas:

- **Rojo — riesgo alto:** el nombre de origen o destino coincide con un registro de la lista restrictiva.
- **Amarillo — revisión requerida:** no existe coincidencia restrictiva, pero el monto supera el `monto_maximo_habitual` o es igual o superior al doble del `monto_promedio` del cliente.
- **Amarillo — información insuficiente:** el cliente no tiene historial disponible o faltan datos relevantes para completar el análisis.
- **Verde — riesgo bajo:** no existe coincidencia restrictiva, el cliente tiene historial y el monto se encuentra dentro de su comportamiento esperado.

Si una operación cumple más de una regla, debe prevalecer siempre el nivel de mayor riesgo: **rojo > amarillo > verde**.

### Expectativas de implementación

- El resultado debe ser reproducible: la misma entrada debe producir la misma clasificación.
- Cada clasificación debe mostrar qué regla se activó y qué datos la sustentan.
- La interfaz puede mostrar el **proceso de análisis**, pero no debe afirmar que revela razonamiento privado o pensamiento interno de un modelo de IA.
- Toda la información debe procesarse localmente en el navegador.
- No se deben realizar llamadas a APIs, servicios de IA ni fuentes externas.
- No se requiere autenticación, persistencia en servidor, pruebas automatizadas ni pipeline de CI/CD para completar el reto.
- Los datos utilizados deben ser ficticios y no deben contener información personal o financiera real.
- Los componentes deben estar separados por responsabilidad y los modelos de datos deben definirse mediante interfaces o tipos de TypeScript.
- Los estados de riesgo no deben depender únicamente del color; deben incluir texto, iconos o etiquetas accesibles.
- GitHub Copilot debe utilizarse como asistente de desarrollo, pero el equipo es responsable de revisar, comprender y validar el código generado.

## Criterios de aceptación

El reto se considerará completado cuando se cumplan todos los siguientes criterios:

- [ ] Permite cargar y validar los tres archivos definidos en el reto.
- [ ] Informa claramente los archivos, campos o registros inválidos sin bloquear toda la interfaz.
- [ ] Analiza todas las transferencias válidas y muestra el avance o estado del procesamiento.
- [ ] Compara tanto el nombre de origen como el de destino contra la lista restrictiva.
- [ ] Compara el monto con el historial del cliente y muestra los valores usados en el cálculo.
- [ ] Clasifica cada operación como verde, amarilla o roja aplicando reglas documentadas.
- [ ] Una coincidencia con la lista restrictiva siempre produce una clasificación roja.
- [ ] Una operación sin coincidencias y dentro del comportamiento esperado se clasifica como verde.
- [ ] Una operación dudosa, atípica o con información insuficiente se clasifica como amarilla.
- [ ] El detalle de cada operación presenta los pasos, reglas activadas y evidencias del análisis.
- [ ] Las operaciones amarillas pueden ser revisadas por una persona.
- [ ] El analista puede liberar o congelar una operación amarilla y debe registrar una justificación.
- [ ] El tablero refleja la decisión humana y actualiza el estado y los indicadores correspondientes.
- [ ] La interfaz es responsiva y comunica los niveles de riesgo con texto o iconos además del color.

## Consideraciones Adicionales

- Incluir validaciones de seguridad.
- Incluir manejo de errores.
- Utilizar fuentes, colores, imágenes alusivas a Banco Popular.

### Skill recomendado para React

Como sugerencia, se recomienda instalar el skill `vercel-react-best-practices` para orientar la implementación y revisión del código React según las prácticas de rendimiento de Vercel Engineering.

Ejecutar el siguiente comando desde la raíz del proyecto:

```bash
npx skills add vercel-labs/agent-skills
```

En el selector interactivo, marcar `vercel-react-best-practices` con la barra espaciadora y confirmar la instalación con Enter, como se muestra en el siguiente ejemplo:

![Selección del skill vercel-react-best-practices durante la instalación](img/vercel-skill.png)