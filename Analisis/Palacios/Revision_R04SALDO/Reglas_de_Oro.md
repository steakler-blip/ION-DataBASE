# Reglas de Oro

Supuestos y decisiones **confirmados por el cliente** que aplican de forma transversal a todos los layouts. Su propósito es **no volver a preguntar**: cuando una pregunta de un concentrado (`Preguntas_Cliente`) cae bajo una regla de oro, queda **respondida** y la corrección se aplica directamente.

Cada regla tiene: identificador, la regla, su origen, qué resuelve y cómo se aplica. Este archivo es **vivo**: conforme el cliente confirme más supuestos, se agregan aquí y se propagan a los layouts.

---

## RO-01 · Moneda única: Peso Mexicano (MXN)

**Regla.** La compañía **solo opera en pesos mexicanos**. No hay operaciones en otras monedas.

**Origen.** Confirmado por el cliente.

**Qué resuelve.** Cualquier pregunta sobre el tipo de moneda queda respondida. El campo de moneda de cualquier layout se fija al **valor de moneda nacional** del catálogo que corresponda, **sin mapear ni contemplar otras monedas**. Ya no se pregunta al cliente por moneda.

**Cómo se aplica por layout:**

| Layout                        | Campo          | Valor                    | Nota                                                                |
| ----------------------------- | -------------- | ------------------------ | ------------------------------------------------------------------- |
| CLIENTES POR PRODUCTO (R2450) | MONEDA         | `'MXN'`                  | clave alfa de MONEDA_ISO; reemplaza el `'2'` del catálogo deprecado |
| R04A_SALDOS                   | MONEDA         | `0` (MXN en Moneda_R04A) | el `ELSE 0` del CASE queda correcto al ser MXN la única             |
| HIPOTECARIO                   | MONEDA_CREDITO | `14`                     | código de moneda nacional del catálogo Monedas                      |

**Efecto en preguntas abiertas:** quedan **resueltas** las preguntas de moneda de R2450 (CRIT-01), R04A y HIPOTECARIO. No requieren confirmación adicional.

---

## Cómo agregar una nueva regla de oro

1. Asignar el siguiente identificador (`RO-02`, `RO-03`, …).
2. Escribir la regla, su origen (quién/cuándo la confirmó) y qué resuelve.
3. Indicar cómo se aplica por layout (campo y valor/criterio).
4. Marcar como **resueltas** las preguntas correspondientes en los concentrados afectados.

_Candidatas a futuras reglas (aún sin confirmar, hoy siguen como pregunta): mapeo único de localidad SAF → cve_municipio_siti; valor por defecto cuando IND_PERSONA no es F ni J; criterio de las 10 categorías de TIPO_CLIENTE._

---

_Reglas de Oro del proyecto. Aplican a todos los layouts y a los concentrados/SP que se generen._

## Consideraciones adicionales

El Excel resultados_BW.xlsx contiene nombres de campos que no pasan la validación de datos y una breve descripción de la plataforma BW que se encarga de realizar esta tarea, se debe validar si cumplen con las consideraciones del layout y emitir posibles soluciones o validaciones adicionales
Existe una versión en crudo del Layout y una versión con comentarios, hay que comparar posibles diferencias en la configuración y cantidad de campos especificados en ambos layouts.
El archivo V1.01_Credito_IFRS9_R04A_Comentarios, contiene observaciones de los involucrados de la columna "p" hasta la "AF"
