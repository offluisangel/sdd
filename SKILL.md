---
name: sdd
description: Gestiona el Spec-Driven Development durante todo el ciclo de un cambio. Úsala al explorar, planificar, implementar o revisar cambios no triviales para decidir si corresponde leer una especificación existente, actualizarla, crear una nueva, completarla o deprecarla. También úsala cuando el usuario mencione una especificación, diseño técnico, criterios de aceptación, decisiones de arquitectura o pida trabajar a partir de un SDD.
disable-model-invocation: false
metadata:
  version: 1.0.0
---

# Gestionar Spec-Driven Development (SDD)

Usa los SDD como documentos vivos de decisiones y comportamiento esperado. Mantén alineados problema, alcance, diseño, implementación y validación sin documentar por obligación.

## Principios

- Lee la especificación antes de escribir código o modificarla.
- Busca un SDD relacionado antes de crear uno nuevo.
- Crea un SDD solo cuando ayude a tomar, comunicar o verificar decisiones relevantes.
- Mantén un SDD centrado en un cambio coherente. Divide cambios con objetivos o ciclos de vida independientes.
- Registra decisiones y resultados, no una narración de cada modificación del código.
- No inventes requisitos, decisiones, responsables, fechas históricas ni resultados de validación.
- Trata el SDD como una guía revisable, no como autoridad por encima de evidencia nueva o del pedido actual del usuario.
- Sigue primero las convenciones e instrucciones específicas del proyecto si difieren de esta skill.

## Al comenzar una tarea

Determina si el trabajo puede tener un SDD relacionado antes de proponer un diseño o modificar código.

1. Lee las instrucciones del proyecto y localiza su convención para especificaciones.
2. Busca directorios y archivos como `docs/specs/`, `specs/`, `design/`, `rfcs/`, `adr/` y nombres relacionados con la feature, issue, dominio o componentes afectados.
3. Lee los SDD candidatos y sus referencias relevantes.
4. Clasifica la acción como una de estas:
   - **leer** un SDD existente;
   - **actualizar** un SDD existente;
   - **crear** un SDD nuevo;
   - **deprecar o reemplazar** un SDD;
   - **no usar SDD** para esta tarea.
5. Si encuentras varios documentos plausibles, determina su relación antes de editar cualquiera. Pregunta solo si elegir incorrectamente puede alterar el alcance o decisiones importantes.

No limites la búsqueda al nombre exacto solicitado. Un cambio puede estar documentado bajo el nombre del problema, del flujo, de una iniciativa mayor o de un componente relacionado.

## Cuándo leer un SDD

Lee el SDD relevante antes de:

- diseñar o implementar una feature ya especificada;
- cambiar comportamiento, contratos, datos o arquitectura descritos en él;
- responder preguntas sobre alcance, decisiones, riesgos o criterios de aceptación;
- investigar una regresión relacionada con el cambio;
- revisar si una implementación está terminada;
- estimar o dividir el trabajo descrito;
- modificar o deprecar el propio documento.

Después de leerlo, contrasta sus afirmaciones con el código y la documentación actuales cuando la tarea dependa de ellas. Indica cualquier diferencia material; no asumas que el documento sigue vigente solo porque existe.

## Cuándo crear un SDD nuevo

Crea un SDD cuando el cambio sea suficientemente relevante y no esté cubierto por uno existente. Es una señal fuerte que se cumpla una o más de estas condiciones:

- afecta varios módulos, servicios, capas o equipos;
- cambia una API, esquema, formato, evento, comando o contrato público;
- requiere una migración o modifica persistencia;
- introduce una decisión arquitectónica o un tradeoff difícil de revertir;
- altera un flujo importante, permisos, seguridad, privacidad, disponibilidad o rendimiento;
- tiene varios casos límite o criterios de aceptación que deben acordarse;
- requiere rollout, compatibilidad, observabilidad o estrategia de reversión;
- hay alternativas razonables y conviene registrar por qué se elige una;
- el usuario pide explícitamente una especificación o SDD.

No crees un SDD por defecto para:

- correcciones pequeñas con causa y solución evidentes;
- refactors locales sin cambio de comportamiento ni contratos;
- cambios mecánicos, de formato, texto o dependencias rutinarias;
- tareas cuya decisión ya está documentada y solo requieren ejecución;
- exploraciones sin una propuesta suficientemente definida, salvo que el usuario quiera un borrador.

Si no está claro si aporta valor, explica brevemente el coste o riesgo que el SDD resolvería. Prefiere no crearlo cuando solo repetiría el pedido o el código.

## Cuándo actualizar un SDD existente

Actualiza el SDD existente cuando el trabajo conserva el mismo problema, objetivos y alcance general, pero cambia información material como:

- una decisión de diseño;
- comportamiento esperado o un caso importante;
- contratos, tipos, endpoints, comandos o persistencia;
- restricciones, riesgos o trabajo pendiente;
- criterios de aceptación o estrategia de testing;
- estado de implementación;
- referencias necesarias para entender o verificar el cambio.

No lo actualices por cada detalle menor de implementación. Actualízalo cuando el documento pueda inducir a una decisión o validación incorrecta si queda como está.

Conserva el historial útil:

- actualiza `Última actualización`;
- añade una entrada al changelog para cambios materiales;
- no reescribas decisiones anteriores como si nunca hubieran existido cuando el motivo del cambio sea relevante;
- marca claramente decisiones reemplazadas y enlaza su sustitución.

## Cuándo crear otro SDD en vez de modificar

Crea uno separado cuando:

- aparece un objetivo independiente;
- el nuevo trabajo puede aprobarse, implementarse o revertirse por separado;
- amplía sustancialmente el alcance original;
- reemplaza una solución completada con otra iniciativa;
- mezclar ambos cambios volvería ambiguos los criterios de aceptación o el estado.

Relaciona ambos documentos en `Referencias`. Si el nuevo SDD reemplaza al anterior, marca el anterior como `deprecado` solo cuando esa relación esté decidida, e indica cuál lo sustituye.

## Crear el documento

1. Usa [`sdd-template.md`](./sdd-template.md), ubicado junto a esta skill, como estructura base. Debes leerlo antes de crear una especificación. No modifiques el template al crear una especificación.
2. Respeta una plantilla o convención local si el proyecto ya tiene una.
3. Guarda el archivo en la ubicación definida por el proyecto. Si no existe una convención, usa `docs/specs/<nombre-del-cambio>.md`.
4. Usa un nombre corto, descriptivo y estable en `kebab-case`. Evita nombres genéricos como `feature.md` o `changes.md`.
5. Empieza en estado `borrador`.
6. Completa primero:
   - Contexto;
   - Objetivos y límites;
   - Decisiones conocidas;
   - Criterios de aceptación.
7. Añade diseño, contratos, datos, testing, riesgos y diagramas solo si aportan información necesaria.
8. Elimina secciones opcionales que no correspondan. No uses `N/A` para rellenar la plantilla.
9. Usa la fecha actual para creación y actualización. Si no conoces el autor, no inventes uno: conserva un marcador explícito o pregunta si ese dato es obligatorio.
10. Registra incertidumbres reales en `Preguntas, riesgos y pendientes`; no presentes suposiciones como decisiones.

Antes de terminar el borrador, comprueba que:

- el contexto describe el problema y no solo la solución;
- los objetivos pueden distinguirse de lo que queda fuera de alcance;
- cada decisión importante incluye motivo y coste o alternativa cuando sean relevantes;
- el diseño tiene detalle suficiente para implementar, pero no prescribe detalles accidentales;
- los criterios de aceptación son observables y verificables;
- los riesgos incluyen mitigación cuando se conoce;
- las referencias usan rutas o enlaces concretos.

## Trabajar desde un SDD

Cuando implementes un cambio descrito por un SDD:

1. Resume internamente objetivos, límites, decisiones y criterios de aceptación antes de editar código.
2. Inspecciona el código afectado y verifica que las premisas del SDD sean actuales.
3. Implementa dentro del alcance acordado.
4. Si aparece una contradicción material, no la ocultes ni fuerces el código para obedecer un diseño inválido:
   - reúne evidencia;
   - corrige el SDD si la decisión nueva es clara y está dentro del pedido;
   - pregunta al usuario si cambia producto, alcance o un tradeoff importante.
5. Actualiza el SDD cuando cambie una decisión importante, no después de cada edición.
6. Usa los criterios de aceptación para orientar la validación y el reporte final.

No marques casillas ni afirmes que algo está implementado o verificado sin evidencia. Diferencia con claridad entre diseño acordado, código escrito y validación ejecutada.

## Estados y ciclo de vida

Usa los estados de esta manera:

- `borrador`: hay decisiones abiertas o todavía no se ha aprobado la ejecución;
- `aprobado`: el alcance y las decisiones necesarias están acordados;
- `implementando`: existe trabajo de implementación activo;
- `completado`: la implementación terminó y los criterios aplicables fueron verificados;
- `deprecado`: el documento ya no representa la solución vigente y señala su reemplazo o motivo.

No cambies automáticamente `borrador` a `aprobado`; la aprobación requiere una señal explícita del usuario o del proceso del proyecto. Puedes cambiar a `implementando` cuando la implementación solicitada comienza y el documento ya está aprobado, salvo que la convención local indique otra cosa.

Marca `completado` únicamente cuando:

- el alcance acordado está implementado;
- los criterios de aceptación aplicables están satisfechos;
- la validación relevante se ejecutó o el documento registra con claridad qué no pudo verificarse;
- no quedan pendientes que bloqueen considerar terminado el cambio.

## Revisar un SDD

Cuando el usuario pida revisar una especificación:

1. Compara el SDD con el pedido, código, contratos y documentos relacionados.
2. Detecta contradicciones, alcance ambiguo, decisiones sin motivo, supuestos no confirmados y criterios no verificables.
3. Prioriza observaciones que puedan causar una implementación incorrecta o una falsa señal de finalización.
4. Propón cambios concretos. Edita el documento si el usuario pidió corregirlo y existe evidencia suficiente.
5. No conviertas preferencias menores de redacción en problemas de diseño.

## Idioma y redacción

- Sigue el idioma del usuario y de la documentación del proyecto. Si el usuario escribe en español o el template está en español, redacta el SDD en español.
- Conserva los nombres de código, APIs, tipos, comandos y términos técnicos en su forma habitual.

## Resultado esperado

Al terminar una acción con SDD, comunica de forma breve:

- qué documento se leyó, creó o actualizó;
- qué decisión o cambio material quedó registrado;
- el estado actual del SDD;
- preguntas o discrepancias que sigan abiertas;
- qué validación se realizó, si corresponde.
