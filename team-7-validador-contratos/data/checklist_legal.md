# Checklist legal para contratos de proveedores tecnológicos

**Código:** CHK-LEGAL-TEC-001  
**Versión:** 1.0  
**Fecha de actualización:** 1 de septiembre de 2026  
**Propietario:** Dirección Jurídica y de Procurement  
**Clasificación:** Uso interno - Documento ficticio para demostración  

## Propósito

Este checklist contiene los controles mínimos que deben evaluarse antes de aprobar un contrato con un proveedor de tecnología. Cada control debe contrastarse con el contenido completo del contrato y clasificarse de acuerdo con la evidencia encontrada.

> Este documento es ficticio y se proporciona únicamente para probar una aplicación. No constituye asesoría legal ni reemplaza la revisión de un profesional.

## Estados de evaluación

| Estado | Definición |
|---|---|
| Cumple | El contrato contiene evidencia suficiente y satisface todos los criterios obligatorios del control. |
| Revisión requerida | Se encontró una cláusula relacionada, pero uno o más criterios obligatorios están incompletos, son ambiguos o quedaron sujetos a un acuerdo futuro. |
| No cumple | No existe evidencia suficiente o la disposición contractual contradice el requerimiento. |

## Reglas generales de análisis

- Evaluar el significado de la cláusula y no solamente coincidencias exactas de palabras.
- Considerar sinónimos, abreviaturas y expresiones jurídicas equivalentes.
- Citar como evidencia el fragmento más relevante del contrato.
- No inferir obligaciones que no estén expresamente descritas.
- Si una condición queda pendiente de una negociación futura, clasificar el control como **Revisión requerida**.
- Ante criterios contradictorios dentro del contrato, conservar el resultado de mayor riesgo.
- La decisión definitiva debe ser confirmada por un revisor humano.

---

## LEG-001 - Protección y tratamiento de datos personales

- **Categoría:** Privacidad
- **Riesgo:** Crítico
- **Peso:** 15
- **Obligatorio:** Sí
- **Descripción:** El contrato debe definir las responsabilidades del proveedor cuando tenga acceso a datos personales y establecer controles suficientes para protegerlos durante todo su ciclo de vida.
- **Criterios obligatorios:**
  - [ ] Identificar el rol del proveedor como encargado o responsable del tratamiento, según corresponda.
  - [ ] Limitar el tratamiento a las instrucciones documentadas del banco.
  - [ ] Exigir medidas técnicas y organizativas para proteger los datos.
  - [ ] Establecer un plazo máximo para notificar incidentes de privacidad.
  - [ ] Exigir autorización previa o reglas expresas para utilizar subencargados.
  - [ ] Regular la devolución o eliminación de los datos al terminar el servicio.
- **Términos relacionados:** datos personales, privacidad, tratamiento de datos, habeas data, encargado del tratamiento, responsable del tratamiento, titular, incidente de privacidad, subencargado
- **Redacción de referencia:** El proveedor tratará los datos personales únicamente conforme a instrucciones documentadas del banco, aplicará medidas técnicas y organizativas apropiadas, notificará cualquier incidente de privacidad dentro de las veinticuatro horas siguientes a su detección, no utilizará subencargados sin autorización previa y devolverá o eliminará los datos al finalizar el servicio.

---

## LEG-002 - Confidencialidad y manejo de información

- **Categoría:** Confidencialidad
- **Riesgo:** Alto
- **Peso:** 10
- **Obligatorio:** Sí
- **Descripción:** El contrato debe proteger la información confidencial del banco y restringir su uso al cumplimiento del objeto contractual.
- **Criterios obligatorios:**
  - [ ] Definir de manera amplia qué se considera información confidencial.
  - [ ] Limitar el uso de la información al objeto del contrato.
  - [ ] Restringir el acceso a las personas que necesiten conocerla.
  - [ ] Exigir medidas razonables de protección y custodia.
  - [ ] Regular la devolución o destrucción de la información.
  - [ ] Mantener la obligación después de la terminación del contrato.
- **Términos relacionados:** información confidencial, reserva, secreto, información sensible, no divulgación, NDA, custodia, destrucción de información
- **Redacción de referencia:** El proveedor utilizará la información confidencial exclusivamente para ejecutar el contrato, limitará su acceso al personal autorizado, aplicará medidas adecuadas de custodia y, cuando el banco lo solicite, devolverá o destruirá la información. La obligación permanecerá vigente durante cinco años después de la terminación.

---

## LEG-003 - Niveles de servicio y compensaciones

- **Categoría:** Servicio
- **Riesgo:** Alto
- **Peso:** 12
- **Obligatorio:** Sí
- **Descripción:** El contrato debe establecer indicadores de servicio medibles y consecuencias claras cuando el proveedor no alcance los niveles acordados.
- **Criterios obligatorios:**
  - [ ] Definir un porcentaje mínimo de disponibilidad mensual.
  - [ ] Establecer tiempos de respuesta para incidentes según su severidad.
  - [ ] Establecer tiempos máximos de solución o restauración.
  - [ ] Describir el método de medición y las exclusiones permitidas.
  - [ ] Exigir reportes periódicos de desempeño.
  - [ ] Incluir créditos de servicio, descuentos u otra consecuencia por incumplimiento.
- **Términos relacionados:** SLA, nivel de servicio, disponibilidad, tiempo de respuesta, tiempo de solución, restauración, severidad, indicador de servicio, crédito de servicio, descuento
- **Redacción de referencia:** El proveedor garantizará una disponibilidad mensual mínima del 99,9 %, atenderá y resolverá los incidentes dentro de los tiempos definidos por severidad y reconocerá créditos de servicio cuando incumpla los niveles pactados, sin perjuicio de las demás acciones contractuales.

---

## LEG-004 - Seguridad de la información y gestión de incidentes

- **Categoría:** Ciberseguridad
- **Riesgo:** Crítico
- **Peso:** 15
- **Obligatorio:** Sí
- **Descripción:** El proveedor debe implementar controles de seguridad proporcionales al riesgo y responder oportunamente ante incidentes que afecten al banco.
- **Criterios obligatorios:**
  - [ ] Exigir cifrado de información en tránsito y en reposo.
  - [ ] Aplicar autenticación multifactor y mínimo privilegio a los accesos sensibles.
  - [ ] Mantener registros de eventos y revisar periódicamente los accesos.
  - [ ] Ejecutar un proceso documentado de gestión de vulnerabilidades.
  - [ ] Definir plazos para corregir vulnerabilidades críticas y altas.
  - [ ] Notificar incidentes de seguridad dentro de un plazo máximo definido.
  - [ ] Entregar un informe de causa raíz después de un incidente relevante.
- **Términos relacionados:** seguridad de la información, ciberseguridad, cifrado, encriptación, TLS, autenticación multifactor, MFA, mínimo privilegio, vulnerabilidad, incidente de seguridad, causa raíz
- **Redacción de referencia:** El proveedor mantendrá controles de cifrado, autenticación multifactor, mínimo privilegio, registro de eventos y gestión de vulnerabilidades. Todo incidente que afecte el servicio o la información será notificado dentro de las veinticuatro horas siguientes a su detección y contará con un informe de causa raíz.

---

## LEG-005 - Continuidad del negocio y recuperación ante desastres

- **Categoría:** Resiliencia operativa
- **Riesgo:** Crítico
- **Peso:** 12
- **Obligatorio:** Sí
- **Descripción:** El proveedor debe asegurar la recuperación del servicio y la información frente a fallas graves, desastres o interrupciones prolongadas.
- **Criterios obligatorios:**
  - [ ] Mantener un plan documentado de continuidad del negocio.
  - [ ] Mantener un plan de recuperación ante desastres.
  - [ ] Definir objetivos de tiempo y punto de recuperación, RTO y RPO.
  - [ ] Ejecutar pruebas periódicas de los planes y entregar sus resultados al banco.
  - [ ] Mantener respaldos protegidos y verificar su restauración.
  - [ ] Informar oportunamente la activación de los planes de recuperación.
- **Términos relacionados:** continuidad del negocio, recuperación ante desastres, disaster recovery, BCP, DRP, RTO, RPO, respaldo, restauración, contingencia operativa
- **Redacción de referencia:** El proveedor mantendrá planes de continuidad y recuperación ante desastres, con RTO y RPO definidos, respaldos protegidos y pruebas al menos anuales cuyos resultados estarán disponibles para el banco.

---

## LEG-006 - Derecho de auditoría y conservación de evidencias

- **Categoría:** Cumplimiento
- **Riesgo:** Alto
- **Peso:** 8
- **Obligatorio:** Sí
- **Descripción:** El banco debe poder verificar el cumplimiento del proveedor y acceder a evidencias suficientes durante la vigencia del contrato.
- **Criterios obligatorios:**
  - [ ] Reconocer el derecho de auditoría del banco y de sus auditores autorizados.
  - [ ] Permitir verificaciones de autoridades competentes cuando corresponda.
  - [ ] Definir un periodo mínimo de conservación de evidencias.
  - [ ] Incluir evidencias de accesos, cambios, respaldos y vulnerabilidades.
  - [ ] Exigir planes de acción para corregir los hallazgos.
  - [ ] Permitir auditorías sin aviso previo cuando exista un incidente material.
- **Términos relacionados:** auditoría, inspección, verificación, evidencia, registro, log, trazabilidad, plan de acción, hallazgo, autoridad competente
- **Redacción de referencia:** El banco, sus auditores y las autoridades competentes podrán verificar el cumplimiento del contrato. El proveedor conservará evidencias de accesos, cambios, respaldos y vulnerabilidades por al menos doce meses y presentará planes de acción para los hallazgos identificados.

---

## LEG-007 - Multas, penalidades y remedios por incumplimiento

- **Categoría:** Riesgo contractual
- **Riesgo:** Alto
- **Peso:** 10
- **Obligatorio:** Sí
- **Descripción:** El contrato debe establecer consecuencias económicas objetivas ante incumplimientos relevantes o reiterados del proveedor.
- **Criterios obligatorios:**
  - [ ] Definir los eventos que generan una multa o penalidad.
  - [ ] Establecer el método de cálculo o el valor aplicable.
  - [ ] Definir un límite acumulado cuando corresponda.
  - [ ] Permitir descontar los valores de facturas pendientes.
  - [ ] Aclarar que la aplicación de la penalidad no impide exigir el cumplimiento.
  - [ ] Diferenciar las penalidades de los créditos de servicio del SLA.
- **Términos relacionados:** multa, penalidad, cláusula penal, sanción, descuento, incumplimiento, compensación económica, apremio, crédito de servicio
- **Redacción de referencia:** Ante un incumplimiento atribuible al proveedor, el banco podrá aplicar una penalidad equivalente al porcentaje definido para el evento y descontarla de las facturas pendientes, sin que ello impida exigir el cumplimiento o ejercer otras acciones contractuales.

---

## LEG-008 - Terminación anticipada y transición de salida

- **Categoría:** Terminación
- **Riesgo:** Alto
- **Peso:** 8
- **Obligatorio:** Sí
- **Descripción:** El banco debe poder terminar el contrato ante eventos relevantes y recibir apoyo suficiente para transferir el servicio sin afectar la operación.
- **Criterios obligatorios:**
  - [ ] Permitir la terminación por incumplimiento material no subsanado.
  - [ ] Permitir la terminación por incidentes graves de seguridad o confidencialidad.
  - [ ] Permitir la terminación por conveniencia del banco con aviso previo.
  - [ ] Exigir la entrega de documentación, configuraciones e inventarios.
  - [ ] Exigir la revocación de accesos y la eliminación o devolución de información.
  - [ ] Definir un periodo mínimo de asistencia para la transición.
- **Términos relacionados:** terminación anticipada, resolución, incumplimiento material, terminación por conveniencia, transición de salida, reversibilidad, transferencia, revocación de accesos
- **Redacción de referencia:** El banco podrá terminar el contrato por incumplimiento, incidentes graves o conveniencia. Al finalizar, el proveedor prestará asistencia de transición, entregará la documentación y configuraciones, revocará accesos y certificará la devolución o eliminación de la información.

---

## LEG-009 - Propiedad intelectual y derechos de uso

- **Categoría:** Propiedad intelectual
- **Riesgo:** Medio
- **Peso:** 5
- **Obligatorio:** Sí
- **Descripción:** El contrato debe diferenciar los activos preexistentes de los entregables desarrollados para el banco y otorgar derechos de uso suficientes.
- **Criterios obligatorios:**
  - [ ] Reconocer la titularidad de los activos preexistentes de cada parte.
  - [ ] Definir la licencia aplicable al software o plataforma del proveedor.
  - [ ] Permitir al banco utilizar los entregables creados específicamente para él.
  - [ ] Definir el tratamiento de configuraciones, informes y documentación.
  - [ ] Prohibir el uso no autorizado de marcas y contenidos del banco.
- **Términos relacionados:** propiedad intelectual, derechos de autor, licencia, software, entregable, desarrollo, código fuente, configuración, marca, documentación
- **Redacción de referencia:** Cada parte conservará sus activos preexistentes. El banco recibirá los derechos necesarios para usar la plataforma durante la vigencia y podrá utilizar y modificar sin restricción temporal los informes, configuraciones y entregables creados específicamente para él.

---

## LEG-010 - Subcontratación y gestión de terceros

- **Categoría:** Terceros
- **Riesgo:** Alto
- **Peso:** 5
- **Obligatorio:** Sí
- **Descripción:** El banco debe conocer y controlar la participación de terceros que puedan acceder a sus sistemas, servicios o información.
- **Criterios obligatorios:**
  - [ ] Exigir autorización previa y escrita del banco para subcontratistas relevantes.
  - [ ] Mantener un listado actualizado de los terceros utilizados.
  - [ ] Imponer a los terceros obligaciones equivalentes de confidencialidad, privacidad y seguridad.
  - [ ] Mantener al proveedor principal como responsable de las actuaciones de sus terceros.
  - [ ] Exigir notificación previa cuando se incorpore o reemplace un tercero.
  - [ ] Permitir que el banco se oponga por motivos razonables de riesgo o cumplimiento.
- **Términos relacionados:** subcontratación, subcontratista, tercero, proveedor secundario, subencargado, autorización previa, cadena de suministro, responsabilidad solidaria
- **Redacción de referencia:** El proveedor no incorporará subcontratistas con acceso a sistemas o información del banco sin autorización previa y escrita. Mantendrá un listado actualizado, notificará cualquier cambio, impondrá obligaciones equivalentes y continuará siendo responsable por las actuaciones de los terceros.

---

## Cálculo sugerido del resultado

Para calcular el porcentaje general, la aplicación puede asignar el siguiente factor al estado de cada control:

| Estado | Factor |
|---|---:|
| Cumple | 1,0 |
| Revisión requerida | 0,5 |
| No cumple | 0,0 |

La fórmula sugerida es:

```text
porcentaje = suma(peso del control × factor del estado) / suma total de pesos × 100
```

El porcentaje debe redondearse a un decimal. La aplicación debe mostrar también la cantidad de controles por estado, ya que el porcentaje por sí solo no sustituye la revisión de riesgos críticos.
