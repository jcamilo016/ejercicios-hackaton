# Instrucciones para el sistema de diseño

Este repositorio utiliza los archivos `DESIGN.md` y `.github/copilot-instructions.md` para mantener una apariencia consistente en las aplicaciones desarrolladas durante el hackatón. Ambos archivos cumplen funciones diferentes, pero trabajan en conjunto para orientar a GitHub Copilot y a los equipos.

## ¿Qué es `DESIGN.md`?

`DESIGN.md` es la fuente de verdad para las decisiones visuales del repositorio. Define el formato y las reglas que deben seguir las interfaces de las aplicaciones, de modo que los equipos no tengan que inventar estilos diferentes para cada reto.

El archivo comienza con un bloque de configuración en formato YAML que contiene los elementos principales del sistema de diseño:

- **Colores:** tonos para acciones principales y secundarias, superficies, fondos, textos y errores.
- **Tipografía:** familias tipográficas, tamaños permitidos y alturas de línea.
- **Espaciado:** unidad base y escala de separaciones autorizadas.
- **Bordes:** radios permitidos para componentes y elementos de interfaz.

Después del bloque de configuración, el archivo documenta:

- La filosofía visual de las aplicaciones.
- Los patrones para componentes como botones y tarjetas.
- Los estados de interacción, por ejemplo `hover`, `focus` y `disabled`.
- Las restricciones que no deben incumplirse, como evitar degradados, limitar los pesos tipográficos y utilizar iconos de trazo.

Cuando se requiera modificar o ampliar `DESIGN.md`, se puede consultar la biblioteca de ejemplos disponible en [DesignMD Library](https://designmd.app/library). Esta biblioteca sirve como referencia para explorar sistemas de diseño y adaptar una propuesta al formato del archivo.

## ¿Qué es `.github/copilot-instructions.md`?

El archivo `.github/copilot-instructions.md` contiene instrucciones permanentes para GitHub Copilot dentro de este repositorio. Su objetivo es proporcionar reglas de contexto que el agente debe considerar al ayudar a escribir o modificar código.

En este proyecto, el archivo indica que `DESIGN.md` es la fuente de verdad para las decisiones visuales y establece que, antes de crear una página, formulario, componente o estilo, el agente debe:

1. Leer `DESIGN.md` desde la raíz del repositorio.
2. Usar exclusivamente los colores, la tipografía y el espaciado definidos allí.
3. Seguir los patrones documentados para los componentes.
4. Respetar todas las reglas incluidas en la sección **Constraints**.

## ¿Cómo lee este agente el archivo `DESIGN.md`?

Cuando se trabaja con GitHub Copilot desde este repositorio, el agente recibe automáticamente las instrucciones definidas en `.github/copilot-instructions.md`. Estas instrucciones le indican que debe consultar `DESIGN.md` antes de realizar cualquier tarea relacionada con una interfaz de usuario.

El flujo esperado es el siguiente:

1. El usuario solicita crear o modificar una interfaz, componente, formulario, página o estilo.
2. El agente identifica que la tarea tiene impacto visual.
3. Antes de generar código, el agente abre y lee el archivo `DESIGN.md` ubicado en la raíz del repositorio.
4. El agente extrae los tokens, patrones de componentes y restricciones aplicables.
5. El código se genera utilizando esas definiciones, sin introducir colores, tamaños o espaciados no autorizados.
6. Si falta una definición necesaria, el agente consulta al usuario antes de inventar un nuevo patrón.

Por ejemplo, si se solicita crear un botón principal, el agente debe tomar de `DESIGN.md` el color `primary`, el texto blanco, el radio `medium` y el espaciado definido para el componente. De esta manera, las instrucciones de Copilot controlan el proceso y `DESIGN.md` aporta las decisiones visuales concretas.
