# Reto: Cazador de Fugas de Capital

## Contexto

Los clientes de alto valor están trasladando parte de su dinero hacia neobancos, fintechs y plataformas de inversión externas en busca de mejores tasas, mayor rentabilidad o productos más flexibles. Cuando una transferencia saliente de gran volumen es solicitada, el banco dispone de pocos segundos para identificar el riesgo de fuga, entender el perfil del cliente y presentar una alternativa relevante.

El desafío consiste en construir una aplicación web que funcione como un centro de monitoreo para el equipo de retención de liquidez. La solución deberá detectar transferencias potencialmente dirigidas a competidores, calcular su nivel de riesgo y recomendar una contraoferta personalizada antes de que el dinero abandone el banco.

> **Nota:** La aplicación será una simulación front-end. No necesita conectarse a sistemas bancarios reales, ejecutar transferencias ni enviar mensajes reales.

## Objetivo

Desarrollar una aplicación web denominada **Cazador de Fugas de Capital** que permita:

- Monitorear solicitudes de transferencias salientes mediante una simulación en tiempo real.
- Detectar operaciones de alto valor dirigidas a entidades competidoras.
- Enriquecer cada alerta con la información financiera y el segmento del cliente.
- Calcular un nivel de riesgo de fuga de capital.
- Seleccionar una oferta de retención personalizada desde el catálogo del banco.
- Redactar una propuesta de mensaje para el cliente.
- Incorporar un flujo **Human-in-the-Loop** en el que un ejecutivo revise y apruebe la contraoferta antes de simular su envío.
- Visualizar indicadores y tendencias que ayuden al equipo a priorizar su gestión.

## Alcance Técnico

La aplicación deberá ejecutarse completamente en el navegador y no requerirá API, backend ni base de datos. Los datos podrán cargarse desde archivos estáticos incluidos en el repositorio o mediante controles de carga de archivos.

### Panel de monitoreo

Construir un dashboard que incluya, como mínimo:

- Total de capital en riesgo.
- Número de alertas activas.
- Clientes de alto valor afectados.
- Valor potencialmente retenido.
- Tasa de retención simulada.
- Distribución del capital en riesgo por entidad destino.
- Evolución de las transferencias detectadas.

Las visualizaciones deberán implementarse con **Recharts** y responder correctamente al cambio de tamaño de la pantalla.

### Simulación en tiempo real

Las transferencias deberán incorporarse progresivamente al monitor, por ejemplo, utilizando `setInterval` o una cola simulada. Cada operación debe mostrar:

- Fecha y hora.
- Cliente.
- Segmento.
- Monto y moneda.
- Entidad destino.
- Estado de la operación.
- Nivel o puntaje de riesgo.
- Tiempo transcurrido desde la detección.

El usuario debe poder pausar, reanudar y reiniciar la simulación.

### Motor de detección (sugerido)

Para cada transferencia, la aplicación deberá:

1. Comparar el identificador de la entidad destino con el listado de competidores.
2. Consultar la información del cliente en el maestro de clientes.
3. Evaluar el monto de la transferencia respecto a su saldo disponible.
4. Asignar un puntaje de riesgo entre 0 y 100.
5. Clasificar el caso como riesgo **bajo**, **medio**, **alto** o **crítico**.
6. Generar una alerta cuando se cumplan las reglas configuradas.

### Detalle de alerta (sugerida)

Al seleccionar una alerta, deberá mostrarse una vista detallada con:

- Datos básicos y segmento del cliente.
- Saldo actual y monto que desea transferir.
- Porcentaje del saldo comprometido.
- Entidad destino y motivo de la detección.
- Puntaje, nivel y factores que explican el riesgo.
- Producto de retención recomendado.
- Rentabilidad estimada de la oferta.
- Mensaje de retención propuesto.

### Recomendación personalizada (sugerida)

El motor de recomendaciones deberá seleccionar un producto del catálogo considerando, al menos:

- Monto de la transferencia.
- Segmento y perfil de riesgo del cliente.
- Plazo preferido.
- Liquidez requerida.
- Tasa o rentabilidad de los productos disponibles.

La interfaz deberá explicar de forma breve por qué fue seleccionado el producto. La misma oferta no debe asignarse indiscriminadamente a todos los clientes.

### Human-in-the-Loop

Antes de simular cualquier contacto con el cliente, un ejecutivo deberá poder:

- Revisar la alerta y la recomendación.
- Editar el mensaje sugerido.
- Aprobar y simular el envío del SMS.
- Rechazar o descartar la propuesta.
- Registrar el resultado como **pendiente**, **oferta enviada**, **retenido** o **no retenido**.

Las acciones deben producir retroalimentación visual mediante estados, confirmaciones o notificaciones. No debe realizarse ningún envío real.

## Stack Tecnológico

- **React** para la construcción de componentes y la interfaz.
- **TypeScript** con tipado estricto para datos, reglas, alertas y ofertas.
- **Tailwind CSS** para estilos, layout y diseño responsive.
- **Recharts** para indicadores y visualizaciones.
- **Vite** como herramienta recomendada de desarrollo y compilación.
- API nativa `FileReader` y/o una librería ligera para interpretar CSV y JSON.
- `localStorage` opcional para conservar el estado de la demo.

No se requiere backend, autenticación ni integración con servicios bancarios reales.

## Archivos de Entrada

Todos los datos serán ficticios y deberán evitar información personal o financiera real.

### `Master_Clientes.csv`

Contiene los datos necesarios para enriquecer las transferencias y personalizar las ofertas.

### `competidores.csv`

Contiene las entidades que deben ser identificadas como posibles destinos de fuga de capital.

### `catalogo_inversiones.json`

Contiene los productos que el banco puede ofrecer para retener los recursos.

### `transferencias_salientes.csv`

Archivo adicional necesario para alimentar la simulación del monitor.

## Flujo Sugerido

1. El usuario abre la aplicación y visualiza el dashboard sin datos o con datos de demostración.
2. Carga los cuatro archivos de entrada o selecciona la opción **Usar datos de ejemplo**.
3. La aplicación valida los archivos y presenta un resumen de los registros cargados.
4. El usuario inicia la simulación.
5. Las transferencias aparecen progresivamente en el monitor.
6. Cada transferencia se cruza con el maestro de clientes y el listado de competidores.
7. El motor calcula el puntaje de riesgo y genera las alertas correspondientes.
8. Los indicadores y gráficos se actualizan en tiempo real.
9. El ejecutivo abre una alerta prioritaria y consulta su explicación.
10. La aplicación selecciona una oferta del catálogo y redacta un mensaje personalizado.
11. El ejecutivo edita, aprueba o rechaza la contraoferta.
12. Si la aprueba, la aplicación simula el envío y permite registrar el resultado de retención.
13. El dashboard refleja el resultado y actualiza el capital retenido.

## Reglas

### Reglas de detección

- Una transferencia se considera dirigida a la competencia cuando `entidad_destino_id` coincide con un registro de `competidores.csv`.
- Solo se genera una alerta cuando el monto sea igual o superior a **COP 50.000.000**. El umbral puede estar definido como una constante editable.
- Si la transferencia representa al menos el **30 %** del saldo disponible, el riesgo debe incrementarse.
- Los clientes de los segmentos **Preferente** o **Banca Privada** deben recibir una prioridad adicional.
- Las entidades con `nivel_amenaza` alto deben aumentar el puntaje de riesgo.
- Una operación no debe generar alertas duplicadas.

### Puntaje de riesgo (sugerido)

El equipo puede ajustar los pesos, pero deberá mantener una lógica comprensible y trazable:

| Factor | Puntaje sugerido |
|---|---:|
| Destino identificado como competidor | +30 |
| Monto igual o superior a COP 200.000.000 | +20 |
| Transferencia igual o superior al 30 % del saldo | +20 |
| Cliente Preferente o Banca Privada | +15 |
| Entidad destino con amenaza alta | +15 |

Clasificación sugerida:

| Puntaje | Nivel |
|---:|---|
| 0–29 | Bajo |
| 30–59 | Medio |
| 60–79 | Alto |
| 80–100 | Crítico |

### Reglas de recomendación

- El cliente debe pertenecer a uno de los segmentos elegibles del producto.
- El monto debe estar dentro del rango permitido.
- El producto debe ser compatible con el perfil de riesgo.
- Debe priorizarse la coincidencia con el plazo y la necesidad de liquidez del cliente.
- Entre alternativas equivalentes, deberá recomendarse la de mayor tasa.
- Si no existe un producto compatible, la aplicación deberá indicarlo y permitir la revisión manual.

### Reglas operativas y de privacidad

- No utilizar datos personales ni financieros reales.
- Enmascarar identificadores sensibles y números de teléfono en la interfaz.
- No enviar SMS reales ni ejecutar transacciones.
- Toda oferta debe requerir aprobación humana explícita.
- Una alerta descartada o resuelta debe conservar su estado durante la sesión.
- Los cálculos y recomendaciones deben ser determinísticos para los mismos datos de entrada.

## Criterios de Aceptación

Se considerará completado el reto cuando:

- [ ] Es posible cargar y validar los cuatro archivos de entrada.
- [ ] La aplicación ofrece datos de ejemplo para iniciar la demo rápidamente.
- [ ] Las transferencias aparecen progresivamente y la simulación se puede pausar, reanudar y reiniciar.
- [ ] Las operaciones hacia competidores se detectan correctamente.
- [ ] El puntaje de riesgo se calcula y se acompaña de una explicación de sus factores.
- [ ] El dashboard presenta indicadores actualizados y al menos dos gráficos construidos con Recharts.
- [ ] Las alertas pueden filtrarse, buscarse y ordenarse.
- [ ] El detalle de cada alerta muestra cliente, transferencia, riesgo y entidad destino.
- [ ] La oferta recomendada cambia de acuerdo con el perfil, monto y necesidades del cliente.
- [ ] Cuando no existe una oferta compatible, la interfaz informa la situación sin fallar.
- [ ] El ejecutivo puede editar, aprobar, rechazar y simular el envío del mensaje.
- [ ] Ninguna oferta se envía o se marca como enviada sin una acción humana explícita.
- [ ] El resultado de la gestión actualiza el estado de la alerta y los indicadores de retención.
- [ ] La interfaz es responsive, consistente y distingue visualmente los niveles de riesgo.
- [ ] Los errores de formato o datos faltantes se muestran de manera clara.
- [ ] No se utilizan datos reales ni se realizan operaciones financieras o comunicaciones reales.

## Bonus Opcional

- Permitir que el usuario configure umbrales y pesos del puntaje desde la interfaz.
- Exportar las alertas y sus resultados a CSV.
- Utilizar fuentes, colores, imágenes alusivas a Banco Popular.

### Skill recomendado para React

Como sugerencia, se recomienda instalar el skill `vercel-react-best-practices` para orientar la implementación y revisión del código React según las prácticas de rendimiento de Vercel Engineering.

Ejecutar el siguiente comando desde la raíz del proyecto:

```bash
npx skills add vercel-labs/agent-skills
```

En el selector interactivo, marcar `vercel-react-best-practices` con la barra espaciadora y confirmar la instalación con Enter, como se muestra en el siguiente ejemplo:

![Selección del skill vercel-react-best-practices durante la instalación](img/vercel-skill.png)
