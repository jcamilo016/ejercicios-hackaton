# Reto: Negociador de Alivios Financieros

## Contexto

El reto consiste en construir un portal web que simule un agente a través de un chatbot autónomo de cobranza para clientes en mora. El agente debe iniciar y conducir una conversación empática, recopilar información básica sobre la situación financiera del cliente y ofrecer alternativas de pago o rediferido que cumplan estrictamente las políticas ficticias del banco.

La solución será utilizada en una demostración. Por ello, debe ser visualmente atractiva, responsive, fácil de entender y completamente funcional, sin depender de servicios externos.

> **Aviso:** todos los datos y políticas incluidos en este repositorio son ficticios y se usan únicamente con fines demostrativos. La aplicación no debe presentarse como una herramienta apta para tomar decisiones financieras reales.

## Objetivo

Crear una experiencia de negociación de deuda completamente ejecutada en el navegador, basada en reglas determinísticas y respuestas predefinidas. La aplicación debe mantener en memoria el estado de la conversación, evaluar las reglas de cobranza, calcular propuestas válidas y permitir la intervención simulada de un supervisor cuando el caso no pueda resolverse automáticamente.

## Alcance técnico

La aplicación debe funcionar únicamente en el frontend:

- No crear un backend.
- No utilizar bases de datos ni almacenamiento persistente.
- No consumir APIs externas.
- No integrar modelos de inteligencia artificial.
- Simular al agente mediante una máquina de estados, reglas determinísticas, palabras clave y respuestas predefinidas.
- Mantener el estado de la sesión, la negociación y la auditoría únicamente en memoria.
- Permitir reiniciar la demostración sin recargar la página.

## Stack tecnológico sugerido

- React
- TypeScript
- Vite
- Tailwind CSS
- Lucide React para los iconos

Se pueden agregar dependencias pequeñas para procesar el CSV o manejar fechas, siempre que funcionen localmente en el frontend y no introduzcan servicios externos.

## Archivos de entrada

Antes de implementar, revisa los archivos disponibles en el repositorio:

### `data/clientes_mora.csv`

Contiene información de clientes como:

- ID
- Nombre
- Saldo de la deuda
- Días de mora
- Ingresos mensuales
- Score crediticio
Carga y procesa este archivo desde la aplicación. Si los nombres exactos de las columnas son diferentes, adapta la implementación a la estructura real encontrada.

### `data/politicas_cobranza.txt`

Contiene las reglas utilizadas para determinar las opciones que puede ofrecer el agente, por ejemplo:

- Tasas de interés según el score.
- Cantidad máxima de cuotas.
- Condiciones para períodos de gracia.
- Límites para descuentos.
- Casos que requieren aprobación humana.
Las propuestas generadas nunca deben violar estas políticas. Conserva las políticas procesadas en una estructura TypeScript claramente definida.

## Flujo sugerido

1. Mostrar una pantalla inicial con el nombre del portal, una breve indicación de que se trata de una simulación y un selector de cliente.
2. Al seleccionar un cliente, mostrar únicamente su información: nombre, saldo, días de mora, ingresos mensuales y score crediticio.
3. Iniciar automáticamente el chat con un saludo empático y personalizado.
4. Guiar la conversación para conocer:
   - La situación financiera actual.
   - La capacidad mensual de pago.
   - La fecha en la que podría comenzar a pagar.
   - La preferencia entre cuota baja, plazo corto o período de gracia.
5. Permitir responder tanto mediante botones de respuesta rápida como mediante un campo de texto.
6. Validar cada respuesta, actualizar el estado de la negociación y detectar condiciones de escalamiento.
7. Calcular y mostrar entre dos y tres alternativas válidas según el cliente, sus respuestas y las políticas.
8. Permitir seleccionar una propuesta y mostrar todos sus detalles antes de confirmarla.
9. Solicitar una aceptación explícita y mostrar un resumen final del acuerdo con una confirmación simulada.
10. Permitir reiniciar la demostración, limpiando todo el estado en memoria y regresando al selector de cliente.

## Human-in-the-Loop

El agente debe detener automáticamente la negociación cuando ocurra alguna de estas condiciones:

- El cliente utiliza lenguaje agresivo.
- Solicita un descuento de capital no permitido.
- Solicita condiciones que exceden los límites establecidos.
- Ninguna propuesta válida se ajusta a su capacidad de pago.
- Se detecta una excepción definida en las políticas.

## Criterios de aceptación recomendados

La aplicación estará completa cuando:

- Se pueda seleccionar un cliente cargado desde el CSV.
- El agente inicie una conversación personalizada.
- El cliente pueda responder preguntas mediante botones o texto.
- Se generen propuestas calculadas a partir del cliente y las políticas.
- Ninguna propuesta exceda las reglas establecidas.
- El cliente pueda seleccionar y confirmar una propuesta.
- Una solicitud no permitida active el flujo de supervisor.
- El supervisor pueda aprobar o rechazar la excepción.
- Se pueda reiniciar la demo sin recargar la página.
- La interfaz sea responsive y no presente errores en la consola.

## Consideraciones Adicionales

- Incluir validaciones de seguridad, por ejemplo, no mostrar información de un cliente distinto al seleccionado o no incluir datos bancarios reales.
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
