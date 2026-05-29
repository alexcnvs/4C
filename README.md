# Salesforce Demo Project Guidelines

Este repositorio está pensado para construir funcionalidades en un entorno demo de Salesforce siguiendo buenas prácticas de arquitectura, configuración, desarrollo, seguridad, documentación y control de versiones.

El objetivo no es únicamente que la funcionalidad funcione, sino que esté construida de forma ordenada, escalable, mantenible y fácil de explicar tanto a nivel funcional como técnico.

---

## 1. Objetivo del proyecto

Construir una funcionalidad en Salesforce utilizando un enfoque profesional basado en:

* Buen diseño funcional.
* Modelo de datos claro.
* Configuración declarativa siempre que sea posible.
* Desarrollo personalizado solo cuando sea necesario.
* Seguridad desde el inicio.
* Control de versiones con GitHub.
* Documentación suficiente para entender, mantener y evolucionar la demo.
* Pruebas funcionales y técnicas.

Aunque el proyecto se construya en una org demo, debe plantearse como si pudiera evolucionar a una implementación real.

---

## 2. Principios generales

Antes de construir cualquier elemento en Salesforce, se debe definir claramente:

* Qué problema resuelve la funcionalidad.
* Qué usuarios intervienen.
* Qué objetos participan.
* Qué datos se crean, leen, modifican o eliminan.
* Qué automatizaciones son necesarias.
* Qué permisos necesita cada tipo de usuario.
* Qué parte debe resolverse con configuración declarativa.
* Qué parte, si existe, requiere desarrollo.
* Qué metadata debe quedar versionada en GitHub.
* Cómo se probará la funcionalidad.

No se deben crear objetos, campos, Flows, Apex o componentes sin haber definido previamente el flujo funcional y el modelo de datos mínimo.

---

## 3. Declarativo antes que código

Siempre se debe priorizar una solución declarativa cuando sea suficiente.

Soluciones declarativas recomendadas:

* Standard Objects.
* Custom Objects.
* Custom Fields.
* Relationships.
* Lightning Record Pages.
* Dynamic Forms.
* Flows.
* Validation Rules.
* Approval Processes.
* Permission Sets.
* Custom Metadata Types.
* Reports.
* Dashboards.

Solo se debe usar código cuando la configuración estándar de Salesforce no sea suficiente o cuando una solución declarativa sea demasiado compleja, frágil o difícil de mantener.

Antes de proponer Apex, Lightning Web Components o integraciones personalizadas, se debe justificar por qué no basta con una solución declarativa.

---

## 4. GitHub como fuente de verdad

El proyecto debe trabajarse con una mentalidad `source-driven`.

GitHub debe actuar como fuente principal de verdad para la configuración y el desarrollo del proyecto.

Buenas prácticas:

* Usar Salesforce DX.
* Mantener la metadata en formato SFDX.
* Versionar objetos, campos, Flows, clases Apex, LWCs, layouts, permission sets y demás metadata relevante.
* Evitar cambios manuales en Salesforce que no se reflejen después en el repositorio.
* Trabajar con ramas para nuevas funcionalidades.
* Hacer commits pequeños, frecuentes y explicativos.
* Documentar los cambios funcionales y técnicos relevantes.

---

## 5. Estructura recomendada del repositorio

```text
force-app/
  main/
    default/
      applications/
      classes/
      customMetadata/
      flows/
      layouts/
      lwc/
      objects/
      permissionsets/
      tabs/
      triggers/

docs/
  functional-requirements.md
  data-model.md
  automation-flow.md
  security-model.md
  testing-plan.md
  deployment-notes.md

scripts/
  apex/
  soql/

README.md
sfdx-project.json
.gitignore
```

---

## 6. Flujo de ramas

La rama `main` debe representar una versión estable del proyecto.

Cada funcionalidad debe trabajarse en una rama separada.

Ejemplo:

```text
main
└── feature/nombre-funcionalidad
```

Nombres recomendados de ramas:

```text
feature/conflict-checking
feature/opportunity-risk-flow
feature/compliance-review
fix/permission-set-access
docs/data-model-update
```

---

## 7. Convención de commits

Los commits deben ser pequeños y claros.

Ejemplos:

```text
feat: add Conflict Check custom object
feat: create precheck request flow
feat: add compliance review permission set
fix: adjust field-level security for compliance users
docs: document conflict checking data model
test: add Apex tests for conflict service
```

Tipos recomendados:

```text
feat: nueva funcionalidad
fix: corrección
docs: documentación
test: pruebas
refactor: mejora interna sin cambiar comportamiento
chore: tareas menores o configuración
```

---

## 8. Diseño del modelo de datos

Antes de crear campos u objetos, se debe definir el modelo de datos.

Para cada objeto hay que documentar:

* Nombre del objeto.
* Propósito.
* Relación con otros objetos.
* Campos clave.
* Usuarios que pueden ver, crear o modificar registros.
* Automatizaciones relacionadas.
* Informes o vistas esperadas.

Criterios:

* No crear objetos personalizados si un objeto estándar resuelve bien el caso.
* No crear campos duplicados o ambiguos.
* Usar nombres claros y consistentes.
* Evitar campos que mezclen varios significados.
* Usar relaciones `Lookup` o `Master-Detail` solo cuando tenga sentido funcional.
* Usar `Record Types` solo si cambian procesos, layouts, picklists o comportamientos.
* Usar picklists controladas cuando se necesite consistencia.
* Evitar texto libre para datos que luego deban filtrarse, reportarse o automatizarse.

---

## 9. Convenciones de nombres

Los nombres deben ser claros, consistentes y fáciles de entender.

### Objetos

```text
Conflict_Check__c
Compliance_Review__c
Risk_Assessment__c
```

### Campos

```text
Status__c
Risk_Level__c
Related_Opportunity__c
Precheck_Result__c
Review_Comments__c
Submitted_By__c
Submitted_Date__c
Reviewed_By__c
Reviewed_Date__c
Decision__c
Decision_Reason__c
```

### Flows

```text
Opportunity - Launch Precheck
Conflict Check - Update Status
Compliance Review - Submit for Approval
```

### Apex

```text
ConflictCheckService
ConflictCheckController
ConflictCheckTriggerHandler
ConflictCheckTest
```

### Permission Sets

```text
Conflict_Check_User
Conflict_Check_Compliance
Conflict_Check_Admin
```

El nombre debe explicar la función del elemento sin necesidad de abrirlo.

---

## 10. Seguridad y permisos

La seguridad debe diseñarse desde el principio.

Se debe definir:

* Qué usuarios pueden acceder a la funcionalidad.
* Qué usuarios pueden crear registros.
* Qué usuarios pueden editarlos.
* Qué usuarios solo pueden leer.
* Qué campos deben estar ocultos o protegidos.
* Qué acciones deben estar restringidas.

Buenas prácticas:

* Usar `Permission Sets` en lugar de depender exclusivamente de perfiles.
* Aplicar principio de mínimo privilegio.
* Revisar `Field-Level Security`.
* Revisar permisos de objeto.
* Revisar acceso a nivel de registro.
* Usar `Organization-Wide Defaults`, sharing rules o manual sharing cuando aplique.
* En Apex, respetar CRUD, FLS y sharing.
* Evitar que un usuario pueda acceder a datos que no debería ver.
* No usar `without sharing` salvo que exista una justificación clara.

---

## 11. Apex y seguridad

Si se usa Apex, se debe considerar explícitamente:

* `with sharing`
* `inherited sharing`
* User Mode
* Validación de permisos de objeto.
* Validación de permisos de campo.
* Sanitización de entradas.
* Evitar exposición innecesaria de datos en métodos `@AuraEnabled`.

Buenas prácticas:

* No poner lógica compleja directamente en triggers.
* Usar `Trigger Handler Pattern`.
* Separar lógica en clases de servicio.
* Evitar SOQL dentro de bucles.
* Evitar DML dentro de bucles.
* Preparar el código para operaciones bulk.
* No hardcodear IDs.
* Usar Custom Metadata para reglas configurables.
* Escribir tests unitarios reales.
* Cubrir escenarios positivos, negativos y casos límite.

Estructura recomendada:

```text
classes/
  ConflictCheckService.cls
  ConflictCheckServiceTest.cls
  ConflictCheckTriggerHandler.cls
  ConflictCheckController.cls
```

---

## 12. Automatizaciones

Las automatizaciones deben ser simples, trazables y fáciles de mantener.

Orden recomendado:

1. Flow.
2. Validation Rules.
3. Approval Processes.
4. Apex solo si Flow no es suficiente.

Buenas prácticas para Flows:

* Usar nombres descriptivos.
* Documentar qué dispara el Flow.
* Evitar Flows enormes con demasiadas responsabilidades.
* Separar procesos cuando tenga sentido.
* Evitar bucles innecesarios.
* Evitar consultas o actualizaciones excesivas dentro de bucles.
* Controlar errores con rutas de fault.
* Usar variables y recursos con nombres claros.
* No hardcodear IDs.
* Usar Custom Metadata cuando haya reglas configurables.
* Añadir descripciones en elementos importantes del Flow.

Para cada Flow se debe documentar:

```text
Nombre:
Tipo:
Objeto:
Cuándo se ejecuta:
Objetivo:
Entradas:
Salidas:
Reglas principales:
Errores controlados:
```

---

## 13. Lightning Web Components

Solo se deben crear LWCs cuando la interfaz estándar de Salesforce no sea suficiente.

Antes de crear un LWC, revisar si se puede resolver con:

* Lightning Record Page.
* Dynamic Forms.
* Quick Actions.
* Screen Flow.
* Related Lists.
* Standard Components.

Buenas prácticas para LWC:

* Crear componentes pequeños y reutilizables.
* Separar lógica de presentación.
* No cargar datos innecesarios.
* Respetar permisos y seguridad.
* Usar Apex solo cuando Lightning Data Service no sea suficiente.
* Mostrar errores claros al usuario.
* Evitar lógica de negocio crítica solo en frontend.
* Documentar propiedades públicas y eventos.

---

## 14. Custom Metadata y configuración

Toda regla que pueda cambiar en el futuro debería estar en configuración, no hardcodeada.

Ejemplos:

* Estados permitidos.
* Niveles de riesgo.
* Umbrales.
* Criterios de validación.
* Parámetros de integración.
* Reglas de asignación.
* Mensajes configurables.

Preferir:

```text
Custom Metadata Types
Custom Labels
Custom Settings, solo si tiene sentido específico
```

Evitar:

```text
IDs hardcodeados
Nombres de usuarios hardcodeados
Nombres de perfiles hardcodeados
Valores de picklist escritos directamente en Apex sin control
```

---

## 15. Validaciones y calidad de datos

La funcionalidad debe proteger la calidad de los datos.

Usar validaciones para evitar:

* Registros incompletos.
* Estados incoherentes.
* Cambios no permitidos según fase.
* Campos obligatorios solo en ciertos momentos.
* Avances de fase sin información mínima.
* Duplicidades cuando sean relevantes.

Los mensajes de error deben ser claros para el usuario.

Buen ejemplo:

```text
No puedes enviar la revisión a Compliance hasta completar el nivel de riesgo y añadir al menos un interlocutor relacionado.
```

Mal ejemplo:

```text
Error en validación.
```

---

## 16. Experiencia de usuario

La demo debe ser fácil de entender para una persona funcional.

Priorizar:

* Páginas limpias.
* Campos agrupados por secciones.
* Acciones visibles en el momento adecuado.
* Estados fáciles de interpretar.
* Mensajes claros.
* Menos campos cuando no sean necesarios.
* Componentes estándar siempre que sea posible.
* Vistas de lista útiles.
* Informes básicos para demostrar valor.

Cada pantalla debe responder a una pregunta funcional clara:

* Qué tengo que hacer.
* Qué estado tiene este registro.
* Qué información falta.
* Qué decisión se ha tomado.
* Quién tiene que actuar ahora.

---

## 17. Trazabilidad y auditoría

Cuando la funcionalidad implique decisiones, aprobaciones o revisión de información, se debe mantener trazabilidad.

Valorar:

* Historial de campos.
* Objeto específico para revisiones.
* Campos de fecha.
* Campos de usuario responsable.
* Estados del proceso.
* Comentarios de revisión.
* Registro del resultado.
* Relación con la oportunidad, cuenta, contacto u objeto principal.

Campos útiles:

```text
Submitted_By__c
Submitted_Date__c
Reviewed_By__c
Reviewed_Date__c
Decision__c
Decision_Reason__c
Risk_Level__c
Status__c
```

---

## 18. Testing

Toda funcionalidad debe tener una estrategia de pruebas.

### Pruebas funcionales

* Probar usuarios con distintos permisos.
* Probar escenarios positivos.
* Probar escenarios negativos.
* Probar campos obligatorios.
* Probar cambios de estado.
* Probar errores esperados.
* Probar visibilidad de campos.
* Probar experiencia en Lightning.

### Pruebas Apex

* Crear clases de test.
* No depender de datos existentes en la org.
* Crear datos de prueba dentro del test.
* Cubrir escenarios bulk.
* Cubrir errores.
* Cubrir casos sin datos.
* Validar permisos cuando aplique.
* No limitarse a buscar cobertura; probar comportamiento real.

---

## 19. Documentación mínima

Toda funcionalidad debe documentarse con al menos:

```text
docs/functional-requirements.md
docs/data-model.md
docs/automation-flow.md
docs/security-model.md
docs/testing-plan.md
docs/deployment-notes.md
```

---

## 20. Contenido recomendado de la documentación

### `docs/functional-requirements.md`

Debe incluir:

* Objetivo.
* Usuarios implicados.
* Flujo funcional.
* Reglas de negocio.
* Casos especiales.
* Criterios de aceptación.

### `docs/data-model.md`

Debe incluir:

* Objetos.
* Campos.
* Relaciones.
* Picklists.
* Reglas de obligatoriedad.
* Consideraciones de reporting.

### `docs/automation-flow.md`

Debe incluir:

* Flows.
* Triggers.
* Acciones.
* Condiciones.
* Errores.
* Dependencias.

### `docs/security-model.md`

Debe incluir:

* Perfiles.
* Permission Sets.
* Acceso a objetos.
* Acceso a campos.
* Acceso a registros.
* Consideraciones de Apex.

### `docs/testing-plan.md`

Debe incluir:

* Escenarios a probar.
* Usuarios de prueba.
* Datos necesarios.
* Resultado esperado.

### `docs/deployment-notes.md`

Debe incluir:

* Metadata incluida.
* Dependencias.
* Pasos manuales si existen.
* Orden de despliegue.
* Validaciones posteriores.

---

## 21. Criterios de aceptación

Cada funcionalidad debe tener criterios de aceptación claros.

Ejemplo:

```text
Dado que soy un usuario comercial,
cuando estoy en una oportunidad,
entonces puedo lanzar un precheck si la oportunidad tiene los datos mínimos completos.

Dado que lanzo un precheck,
cuando existen posibles conflictos,
entonces se crea un registro de Conflict Check relacionado con la oportunidad.

Dado que soy usuario de Compliance,
cuando reviso un Conflict Check,
entonces puedo aprobarlo, rechazarlo o pedir más información.

Dado que una revisión está aprobada,
cuando vuelvo a la oportunidad,
entonces veo el estado actualizado y puedo continuar el proceso.
```

---

## 22. Qué evitar

Evitar:

* Crear campos sin documentar su propósito.
* Crear automatizaciones duplicadas.
* Usar Flows demasiado grandes.
* Usar Apex cuando Flow sería suficiente.
* Usar Flow cuando Apex sería más claro y mantenible.
* Hardcodear IDs.
* Depender de perfiles concretos.
* Hacer cambios manuales que no se versionan.
* Construir sin modelo de seguridad.
* Crear interfaces demasiado complejas.
* Mezclar lógica de negocio con lógica visual.
* No contemplar errores.
* No probar con distintos tipos de usuario.
* No documentar decisiones técnicas.

---

## 23. Forma de trabajo esperada

Cuando se construya una funcionalidad en este proyecto, se debe seguir esta estructura:

1. Resumen funcional de lo que se va a construir.
2. Modelo de datos recomendado.
3. Objetos y campos necesarios.
4. Automatizaciones necesarias.
5. Seguridad y permisos.
6. Experiencia de usuario.
7. Qué debe ir a GitHub.
8. Estructura de archivos recomendada.
9. Pasos de implementación en Salesforce.
10. Pruebas necesarias.
11. Riesgos o decisiones a confirmar.
12. Siguiente acción concreta.

No se deben dar respuestas genéricas. Cada recomendación debe aterrizarse al caso concreto.

Cuando haya varias opciones, se debe explicar:

* Opción recomendada.
* Alternativa posible.
* Ventajas.
* Inconvenientes.
* Cuándo elegir cada una.

---

## 24. Criterio final

La solución ideal debe ser:

* Sencilla.
* Escalable.
* Segura.
* Versionada.
* Documentada.
* Fácil de demostrar.
* Fácil de mantener.
* Coherente con buenas prácticas de Salesforce.

La prioridad es construir una demo sólida que pueda servir como base para una futura implementación real.
