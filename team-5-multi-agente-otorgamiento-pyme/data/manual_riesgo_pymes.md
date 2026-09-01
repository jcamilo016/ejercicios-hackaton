# Manual de Riesgo para Otorgamiento de Crédito Pyme

**Código:** MRP-2026-01  
**Versión:** 1.0  
**Vigencia:** 1 de enero de 2026  
**Moneda de referencia:** Pesos colombianos (COP)  
**Uso:** Documento ficticio para demostraciones y pruebas de software

---

## 1. Propósito

Este manual define las reglas mínimas para analizar solicitudes de crédito de pequeñas y medianas empresas. Su objetivo es orientar la elaboración de una recomendación de crédito consistente, verificable y explicable.

El resultado del análisis automático es únicamente una **recomendación**. Ninguna solicitud puede aprobarse o desembolsarse sin la revisión y decisión explícita del Comité de Crédito.

## 2. Información mínima requerida

Antes de iniciar el análisis deben estar disponibles los siguientes datos:

- Razón social de la empresa.
- Periodo de los estados financieros.
- Activo corriente.
- Pasivo corriente.
- Activos totales.
- Pasivos totales.
- Patrimonio.
- Ingresos operacionales.
- Utilidad operacional.
- Utilidad neta.
- Servicio anual de la deuda.
- Valor del crédito solicitado.
- Plazo y destino del crédito.

Si falta un dato necesario para calcular un indicador obligatorio, el indicador debe marcarse como **No calculable** y la solicitud debe enviarse a **Revisión manual**. Está prohibido estimar o inventar valores ausentes.

## 3. Normalización de cifras

- Todos los cálculos deben realizarse en una misma moneda y unidad.
- En este manual, el punto puede utilizarse como separador de miles y la coma como separador decimal.
- Los valores entre paréntesis representan valores negativos o deducciones.
- Los porcentajes deben calcularse con al menos cuatro decimales y mostrarse redondeados a dos decimales.
- Las razones financieras deben mostrarse redondeadas a dos decimales.
- Cuando un denominador sea cero, el indicador debe marcarse como **No calculable**.
- Los subtotales deben contrastarse con los totales reportados. Una diferencia superior al 1 % debe generar una alerta de inconsistencia.

## 4. Indicadores financieros obligatorios

### 4.1 Liquidez corriente

Mide la capacidad de la empresa para cubrir sus obligaciones de corto plazo.

```text
Liquidez corriente = Activo corriente / Pasivo corriente
```

| Resultado | Evaluación | Puntaje |
|---|---|---:|
| Mayor o igual a 1,30 | Cumple | 25 |
| Entre 1,10 y 1,29 | En observación | 12 |
| Menor a 1,10 | Incumple | 0 |

### 4.2 Nivel de endeudamiento

Mide qué proporción de los activos está financiada con obligaciones frente a terceros.

```text
Endeudamiento (%) = (Pasivos totales / Activos totales) × 100
```

| Resultado | Evaluación | Puntaje |
|---|---|---:|
| Menor o igual al 60 % | Cumple | 25 |
| Mayor al 60 % y menor o igual al 70 % | En observación | 12 |
| Mayor al 70 % | Incumple | 0 |

### 4.3 Margen neto

Mide la utilidad obtenida después de gastos e impuestos por cada unidad monetaria vendida.

```text
Margen neto (%) = (Utilidad neta / Ingresos operacionales) × 100
```

| Resultado | Evaluación | Puntaje |
|---|---|---:|
| Mayor o igual al 5 % | Cumple | 25 |
| Mayor o igual al 2 % y menor al 5 % | En observación | 12 |
| Menor al 2 % | Incumple | 0 |

### 4.4 Cobertura del servicio de la deuda

Mide la capacidad de la utilidad operacional para atender el servicio anual de la deuda.

```text
Cobertura de deuda = Utilidad operacional / Servicio anual de la deuda
```

| Resultado | Evaluación | Puntaje |
|---|---|---:|
| Mayor o igual a 1,20 | Cumple | 25 |
| Mayor o igual a 1,00 y menor a 1,20 | En observación | 12 |
| Menor a 1,00 | Incumple | 0 |

## 5. Puntaje y clasificación financiera

El puntaje financiero corresponde a la suma de los cuatro indicadores obligatorios. El máximo posible es 100 puntos.

| Puntaje | Clasificación | Interpretación inicial |
|---:|---|---|
| 85 a 100 | Riesgo bajo | Puede recomendarse, sujeto a revisión cualitativa |
| 60 a 84 | Riesgo medio | Requiere condiciones adicionales y revisión del comité |
| 0 a 59 | Riesgo alto | No debe recomendarse en condiciones estándar |

Reglas adicionales:

- Si un indicador **Incumple**, la clasificación final no puede ser Riesgo bajo.
- Si dos o más indicadores **Incumplen**, la recomendación automática debe ser **No favorable**.
- Si dos o más indicadores quedan **En observación**, la clasificación final debe ser, como mínimo, Riesgo medio.
- Un indicador **No calculable** obliga a enviar la solicitud a Revisión manual, independientemente del puntaje disponible.

## 6. Determinación del cupo sugerido

El cupo base será el menor valor entre los siguientes límites:

```text
Límite por ingresos = Ingresos operacionales anuales × 25 %
Límite por EBITDA   = EBITDA anual × 1,50
Cupo base           = menor(Límite por ingresos, Límite por EBITDA)
```

Si el EBITDA no está disponible, el cupo no debe calcularse automáticamente y la solicitud debe enviarse a Revisión manual.

El cupo sugerido se obtiene aplicando el factor correspondiente a la clasificación:

| Clasificación | Factor sobre el cupo base |
|---|---:|
| Riesgo bajo | 100 % |
| Riesgo medio | 70 % |
| Riesgo alto | 0 % |

Reglas para el valor final:

- El cupo recomendado nunca puede superar el valor solicitado por la empresa.
- El cupo recomendado nunca puede superar el cupo base ajustado por riesgo.
- El valor final debe redondearse hacia abajo al múltiplo de COP 5 millones más cercano.
- Las garantías no aumentan el cupo calculado; únicamente pueden respaldar la recomendación.
- Un cupo de cero corresponde a una recomendación **No favorable**.

```text
Cupo sugerido = menor(Valor solicitado, Cupo base × Factor de riesgo)
```

## 7. Evaluación cualitativa y alertas

Las siguientes situaciones deben registrarse como alertas, aunque los indicadores financieros cumplan:

| Código | Situación | Severidad | Acción requerida |
|---|---|---|---|
| ALT-01 | Un cliente representa más del 20 % de las ventas | Media | Evaluar concentración de ingresos |
| ALT-02 | Pérdida reciente de un cliente que represente 10 % o más de las ventas | Alta | Solicitar plan de sustitución de ingresos |
| ALT-03 | Cartera con más de 90 días superior al 5 % de las cuentas por cobrar | Alta | Solicitar detalle y gestión de recuperación |
| ALT-04 | Crecimiento de inventarios superior al 20 % | Media | Validar rotación y obsolescencia |
| ALT-05 | Estados financieros sin auditoría externa | Media | Solicitar certificación del contador y representante legal |
| ALT-06 | Proyecciones futuras sin soporte verificable | Baja | No utilizar la proyección para aumentar el cupo |
| ALT-07 | Obligaciones financieras vencidas | Crítica | Detener recomendación y escalar al comité |
| ALT-08 | Diferencia contable superior al 1 % | Crítica | Detener análisis hasta aclarar la inconsistencia |

Una alerta no debe eliminarse ni ocultarse porque exista una garantía. El memorando debe citar la evidencia del archivo que originó cada alerta.

## 8. Reglas de decisión

La aplicación puede generar uno de los siguientes resultados:

### Recomendación favorable

Se utiliza cuando:

- El riesgo financiero es bajo.
- Ningún indicador incumple.
- No existen alertas críticas.
- La información mínima está completa.

### Recomendación favorable con condiciones

Se utiliza cuando:

- El riesgo financiero es medio; o
- Existe al menos una alerta de severidad alta; y
- No existen alertas críticas ni dos indicadores incumplidos.

Las condiciones deben estar vinculadas a las alertas encontradas. Algunos ejemplos son solicitar información adicional, obtener una garantía válida, reducir el cupo o efectuar seguimiento periódico.

### Revisión manual

Se utiliza cuando:

- Falta información obligatoria.
- Existe un indicador No calculable.
- Se detectan cifras ambiguas o inconsistentes.
- El análisis automático no puede asociar una política con una conclusión.

### Recomendación no favorable

Se utiliza cuando:

- Dos o más indicadores incumplen.
- La clasificación financiera es Riesgo alto.
- Existe una alerta crítica sin resolver.
- El cupo ajustado por riesgo es igual a cero.

## 9. Condiciones mínimas del memorando de crédito

El memorando sugerido debe contener:

1. Identificación de la empresa y características de la solicitud.
2. Resumen ejecutivo.
3. Tabla de cifras financieras utilizadas.
4. Indicadores, fórmulas, resultados, umbrales y evaluación.
5. Puntaje y clasificación de riesgo.
6. Alertas cualitativas con su evidencia.
7. Cálculo detallado del cupo sugerido.
8. Recomendación: favorable, favorable con condiciones, revisión manual o no favorable.
9. Condiciones propuestas y documentos pendientes.
10. Advertencia de que la decisión final corresponde al Comité de Crédito.

Cada conclusión debe diferenciar claramente:

- **Dato:** información extraída del estado financiero.
- **Cálculo:** resultado obtenido mediante una fórmula.
- **Política:** regla de este manual aplicada.
- **Conclusión:** interpretación o recomendación resultante.

## 10. Human-in-the-Loop

- La aplicación no puede aprobar ni desembolsar automáticamente un crédito.
- Los botones **Aprobar desembolso** y **Rechazar solicitud** solo deben habilitarse cuando el análisis y el memorando hayan finalizado.
- El usuario debe revisar las evidencias y confirmar explícitamente su decisión.
- Toda decisión humana debe registrar resultado, comentario, fecha y hora.
- Si el comité modifica el cupo sugerido, debe ingresar una justificación.
- Una decisión humana no debe alterar ni eliminar los resultados originales de los agentes.

## 11. Manejo de errores y trazabilidad

- No se deben inventar datos para completar un análisis.
- Los errores de lectura deben identificar el archivo y el campo afectado.
- Cada indicador debe conservar los valores de entrada usados en su cálculo.
- Cada regla aplicada debe referenciar la sección correspondiente de este manual.
- Los resultados del análisis deben distinguir entre información extraída, calculada y generada por un modelo.
- Si se utiliza un LLM, sus respuestas deben validarse antes de usarse en cálculos o decisiones.

## 12. Datos esperados para el caso de demostración

Esta sección permite validar el funcionamiento usando el archivo de ejemplo `estados_financieros_pyme.txt`.

| Concepto | Resultado esperado |
|---|---:|
| Liquidez corriente | 1,43 |
| Endeudamiento | 54,55 % |
| Margen neto | 7,00 % |
| Cobertura de deuda | 1,26 |
| Puntaje financiero | 100 puntos |
| Clasificación financiera inicial | Riesgo bajo |
| Límite por ingresos | COP 850 millones |
| Límite por EBITDA | COP 720 millones |
| Cupo base | COP 720 millones |
| Valor solicitado | COP 650 millones |
| Cupo sugerido antes de la revisión cualitativa | COP 650 millones |

Aunque los cuatro indicadores cumplen, el caso contiene alertas cualitativas de severidad alta. Por tanto, el resultado esperado es **Recomendación favorable con condiciones**, pendiente de revisión y decisión del Comité de Crédito.

Condiciones sugeridas para el caso de prueba:

- Presentar un plan para sustituir los ingresos del cliente perdido.
- Entregar el detalle de la cartera con vencimiento superior a 90 días.
- Presentar certificación de los estados financieros firmada por el contador y el representante legal.
- Validar el avalúo y la situación jurídica de la garantía ofrecida.

---

> Este manual es ficticio. Fue creado exclusivamente para ejercicios, demostraciones y pruebas de aplicaciones. No constituye asesoría financiera ni una política real de otorgamiento de crédito.
