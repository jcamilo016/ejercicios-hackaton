# Reto: Auditor de Privacidad de Datos (Data Masking)

## Contexto

Un banco quiere aprovechar herramientas de Inteligencia Artificial para ayudar a sus asesores a consultar información y redactar solicitudes. Sin embargo, los textos pueden contener información personal, financiera o confidencial —por ejemplo, números de identificación, cuentas bancarias, teléfonos, correos electrónicos o saldos— que no debería enviarse sin protección a servicios externos.

El reto consiste en construir una aplicación que simule un **agente guardián de privacidad**. Antes de que una consulta continúe su camino, la aplicación deberá analizarla, identificar datos sensibles y generar una versión sanitizada mediante técnicas de enmascaramiento de datos (*data masking*).

> **Importante:** la aplicación es una simulación educativa. Todo el análisis debe ejecutarse localmente en el navegador y ningún texto ingresado debe enviarse a una API, backend o servicio externo.

## Objetivo

Desarrollar una aplicación web que permita:

- Escribir o cargar consultas redactadas por asesores bancarios.
- Detectar información potencialmente sensible dentro del texto.
- Diferenciar datos sensibles de números o expresiones que no requieren protección.
- Mostrar en tiempo real el texto original y su versión sanitizada.
- Resaltar los datos detectados e indicar su categoría.
- Presentar un resumen de los hallazgos y permitir copiar el resultado protegido.

Ejemplo:

```text
Entrada:
El cliente Juan Pérez, identificado con cédula 1032456789,
solicita consultar el saldo de $5.250.000 de su cuenta 45781236901.

Salida esperada:
El cliente [NOMBRE], identificado con cédula [DOCUMENTO],
solicita consultar el saldo de [VALOR_MONETARIO] de su cuenta [CUENTA].
```

## Alcance técnico

### Interfaz principal

Construir una interfaz responsiva con las siguientes áreas:

1. **Encabezado:** nombre de la aplicación, breve descripción e indicador de que el procesamiento es local.
2. **Panel de entrada:** área de texto editable, contador de caracteres, selector de una consulta de ejemplo y opción para cargar el archivo de entrada.
3. **Panel de resultado:** versión sanitizada del texto, actualización en tiempo real y resaltado visual de los valores enmascarados.
4. **Resumen de detecciones:** cantidad total de hallazgos y desglose por categoría.
5. **Detalle de hallazgos:** categoría, valor enmascarado, nivel de sensibilidad y acción aplicada. El valor original no debe mostrarse completo en este panel.
6. **Acciones:** limpiar, analizar, copiar texto sanitizado y descargar el resultado como archivo `.txt`.

En pantallas de escritorio, los paneles de entrada y resultado deben mostrarse lado a lado. En dispositivos móviles deben organizarse verticalmente.

### Motor de detección y enmascaramiento

Se pueden usar expresiones regulares, palabras clave cercanas y reglas de contexto.

La solución base debe detectar como mínimo:

| Categoría | Ejemplos | Enmascaramiento sugerido |
|---|---|---|
| Documento de identidad | `1032456789`, `CC 79.456.123` | `[DOCUMENTO]` |
| Cuenta bancaria | `45781236901`, `cuenta 0098-4567-1234` | `******6901` o `[CUENTA]` |
| Tarjeta de crédito | `4111 1111 1111 1111` | `**** **** **** 1111` |
| Correo electrónico | `cliente@correo.com` | `c******@correo.com` |
| Teléfono | `+57 300 456 7890` | `+57 *** *** 7890` |
| Valor monetario o saldo | `$5.250.000`, `COP 850000` | `[VALOR_MONETARIO]` |
| Nombre de persona | `Juan Pérez` cuando aparece después de “cliente” | `[NOMBRE]` |

Para reducir falsos positivos, no se deben ocultar automáticamente todos los números. La decisión debe considerar su formato y el contexto inmediato.

La aplicación debe ser lo suficientemente inteligente para no ocultar números que no son sensibles (ej. "Tengo 2 dudas sobre la sucursal 45").

## Stack tecnológico

- **React**
- **TypeScript**
- **Vite** como herramienta de construcción
- **Tailwind CSS** para estilos y diseño responsivo
- **Lucide React** para iconografía, opcional
- API nativa `FileReader` para cargar el archivo de entrada

No se requiere backend, base de datos, autenticación ni consumo de servicios de Inteligencia Artificial.

## Archivo de entrada con ejemplos

El repositorio incluye el archivo `consultas_asesores.txt` para probar la aplicación.

La aplicación debe permitir cargar el archivo completo, presentar la lista de consultas encontradas y seleccionar una de ellas para analizarla. Si el formato es inválido o el archivo está vacío, deberá mostrar un mensaje comprensible sin interrumpir la aplicación.

## Reglas

- Todo el procesamiento debe realizarse localmente en el navegador.
- No se deben enviar, almacenar ni registrar los textos ingresados fuera de la sesión actual.
- La aplicación no debe requerir backend, base de datos ni API externa.
- El texto original debe conservarse sin modificaciones en el panel de entrada.
- El resultado debe mantener la redacción y el orden del texto, reemplazando únicamente los datos detectados.
- No se debe enmascarar un número solo por ser numérico; se debe evaluar su formato y contexto.
- Las reglas deben ser determinísticas: la misma entrada y configuración deben producir siempre la misma salida.
- Cuando dos reglas coincidan sobre el mismo fragmento, debe aplicarse la regla más específica o de mayor prioridad, evitando reemplazos duplicados.
- Los valores originales no deben aparecer completos en el listado de hallazgos ni en mensajes de consola.
- Los ejemplos proporcionados son el mínimo requerido; la solución puede incluir más casos.
- El diseño debe ser claro, profesional, accesible y responsivo.

## Bonus adicional: configuración de reglas de privacidad

Incorporar una sección llamada **Configuración de reglas** que permita al usuario decidir cómo se identifica y protege la información sensible sin modificar el código fuente.

Cada regla configurable debe incluir:

- Nombre de la regla.
- Categoría del dato.
- Descripción.
- Patrón de detección mediante expresión regular.
- Palabras clave de contexto opcionales, por ejemplo: `cédula`, `cuenta`, `saldo` o `teléfono`.
- Estrategia de protección: reemplazo total, conservación de los últimos cuatro caracteres o reemplazo personalizado.
- Texto de reemplazo personalizado.
- Prioridad de aplicación.
- Control para activar o desactivar la regla.

La sección debe permitir:

- Crear, editar y eliminar reglas personalizadas.
- Probar una regla con un texto antes de guardarla.
- Validar expresiones regulares inválidas y mostrar un mensaje útil.
- Restablecer la configuración predeterminada.
- Persistir las reglas en `localStorage`.
- Mostrar una advertencia cuando una regla sea demasiado amplia y pueda generar falsos positivos.

## Criterios de aceptación

### Funcionales

- [ ] El usuario puede escribir una consulta manualmente.
- [ ] El usuario puede cargar `consultas_asesores.txt` y seleccionar cualquiera de sus consultas.
- [ ] La aplicación genera una versión sanitizada sin consumir APIs externas.
- [ ] Se detectan, como mínimo, documentos, cuentas, tarjetas, correos, teléfonos, valores monetarios y nombres en contexto.
- [ ] Cada dato detectado se reemplaza según la estrategia definida para su categoría.
- [ ] El resultado se actualiza en tiempo real o mediante una acción explícita de análisis.
- [ ] Se muestra el total de hallazgos y su desglose por categoría.
- [ ] El usuario puede copiar y descargar el texto sanitizado.
- [ ] Una consulta sin datos sensibles produce un estado de “sin hallazgos” y no altera el texto.
- [ ] Los números de los ejemplos no sensibles, como `2`, `45`, `8:00` y `3`, se conservan.
- [ ] Los solapamientos entre reglas no generan reemplazos corruptos o duplicados.

### Bonus

- [ ] El usuario puede crear, editar, activar, desactivar y eliminar reglas.
- [ ] Las expresiones regulares se validan antes de guardar una regla.
- [ ] Es posible probar una regla y visualizar qué fragmentos detecta.
- [ ] Las reglas personalizadas se conservan en `localStorage`.
- [ ] Existe una opción para restaurar las reglas predeterminadas.
- [ ] La prioridad resuelve correctamente las coincidencias entre reglas.

## Consideraciones Adicionales

- Utilizar fuentes, colores, imágenes alusivas a Banco Popular.

### Skill recomendado para React

Como sugerencia, se recomienda instalar el skill `vercel-react-best-practices` para orientar la implementación y revisión del código React según las prácticas de rendimiento de Vercel Engineering.

Ejecutar el siguiente comando desde la raíz del proyecto:

```bash
npx skills add vercel-labs/agent-skills
```

En el selector interactivo, marcar `vercel-react-best-practices` con la barra espaciadora y confirmar la instalación con Enter, como se muestra en el siguiente ejemplo:

![Selección del skill vercel-react-best-practices durante la instalación](img/vercel-skill.png)