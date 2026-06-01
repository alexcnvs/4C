# Resumen de la reunión

## Resumen rápido

La reunión se centró en la discusión del gestor de contactos y sus funcionalidades, donde ZR explicó los problemas identificados durante la implementación del sistema. 

Se discutieron dos casos principales de uso:
- la gestión de contactos externos que llegan a través de formularios web en blanco
- la moderación de contactos existentes que han realizado modificaciones a través de formularios de edición

ZR explicó que el gestor de contactos actúa como una "barrera de seguridad" para los datos externos que llegan al sistema CRM, permitiendo controlar la entrada de datos y mantener la trazabilidad. 

Se identificaron dos puntos complejos que no se consiguieron implementar correctamente:
- la gestión de contactos que se inscriben a eventos y luego reciben comunicaciones de recordatorio
- la detección y gestión de duplicados entre contactos existentes y nuevos

La discusión incluyó también:
- la funcionalidad de carga masiva de contactos
- la integración con herramientas existentes como el sistema de eventos y la gestión de miembros

---

## Siguientes pasos

### Alejandro
- Validar con el equipo de África los dos puntos más complejos del gestor de contactos:
  1. que los datos introducidos por el contacto en el formulario prevalezcan en las comunicaciones del primer evento aunque no hayan sido moderados
  2. que el primer evento de captación quede registrado correctamente en la ficha del contacto

- Trabajar con África para validar si es viable no moderar los contactos inscritos a un evento hasta que pase la fecha del mismo, como posible solución técnica al problema de prevalencia de datos.

### ZR
- Compartir el documento de casos de uso del gestor de contactos con el equipo para su revisión.
- Enviar el email identificado del proyecto de avales (con los puntos relevantes marcados por Laura) al equipo para su referencia.
- Grabar un vídeo demostrativo del funcionamiento de la herramienta de carga masiva (Business Card) para compartirlo con el equipo.
- Validar con África y Laura Hernández los procedimientos correctos de uso del gestor de eventos para evitar malas prácticas como cargar contactos existentes en blanco repetidamente.
- Verificar con África el requisito de la carga masiva en el gestor de contactos para confirmar si fue solicitado formalmente o si puede desvincularse del mismo.

---

## Colaboración

- Alejandro y ZR: Reunirse con África para revisar y depurar el requisito de la carga masiva dentro del gestor de contactos y determinar si debe integrarse o mantenerse separada.
- Alejandro y ZR: Revisar y validar con África los casos de uso relacionados con errores de validación en formularios y cómo deben quedar registrados en el gestor de contactos.

---

## Resumen

### Problemas del Gestor de Contactos

ZR y Alejandro discutieron problemas con el gestor de contactos en un documento de Africa que habían revisado con el equipo. 

ZR explicó que el primer problema identificado fue la confusión sobre manejar dos datos distintos: uno en CRM y otro temporal en el gestor de contactos. 

ZR señaló que los casos de uso no estaban completamente entendidos, especialmente en lo que respecta a cómo se manejan los datos cuando pasan por la "barrera" del gestor de contactos.

---

### Gestor de Contratos del CRM

ZR explicó la funcionalidad del gestor de contratos, que sirve como herramienta de entrada del CRM para canalizar datos de contactos de relaciones externas provenientes de diferentes fuentes como:
- formularios de campañas
- inscripciones web
- eventos
- modificaciones de perfiles

Describió los casos de uso específicos, incluyendo:
- formularios de newsletter
- inscripciones a eventos
- creación de contactos alumni

Destacando que:
- las modificaciones desde CRM son transparentes
- los datos externos pasan por controles adicionales

---

### Gestión de Contactos en Newsletter

ZR explicó el proceso de entrada de contactos a través del formulario de Newsletter y el gestor de eventos, destacando dos puntos complejos:
- la detección de duplicados
- la gestión de contactos pendientes de moderación

Se discutió que los datos introducidos desde web o eventos se moderan, pero los datos originales del contacto se mantienen para el primer evento.

ZR identificó estos dos puntos como los más difíciles de implementar en el sistema actual.

---

### Gestión de Contactos en CRM

Alejandro y ZR discutieron un problema de comunicación con eventos donde los participantes se inscriben pero no reciben invitaciones, generando emails de recordatorio y agradecimiento.

ZR mencionó que este punto fue identificado por Laura como relevante en el proyecto de avales y que necesitan validar con el equipo si realmente quieren implementar esta funcionalidad.

La conversación se centró en la gestión de nuevos contactos en el sistema CRM, incluyendo:
- la detección de duplicados
- la capacidad de modificar datos

ZR explicó que el sistema debe permitir:
- buscar causas específicas
- vincular nuevos contactos con información existente

---

### Implementación Sistema Gestión Contactos Orbis

ZR explicó que África quiere implementar un sistema de gestión de contactos donde se use Orbis como herramienta de referencia y se evite la duplicación de datos.

Discutieron el proceso de resolución de identidad, donde el sistema parpadea solo en cuatro casos específicos:
- nombre
- apellidos
- email
- empresa del contacto

POL preguntó sobre las reglas de purificación en fuentes de entrada, y ZR aclaró que la herramienta debe permitir consultar las entradas automáticas que se bajan y moderarlas según los cambios realizados en el formulario CRM.

---

### Gestión de Formularios y Duplicados

Alejandro y ZR discutieron el manejo de formularios en blanco y la gestión de duplicados en el sistema de contactos.

ZR explicó que cuando un usuario selecciona un contacto duplicado, se mostraría la misma pantalla de modificación que para contactos existentes, permitiendo:
- actualizar la relación
- sustituir
- añadir la información

ZR también mencionó que actualmente existen dos herramientas separadas:
- una para contactos CRN pendientes de modificación
- otra para formularios web en blanco y cargas masivas

---

### Gestión de Contactos en CRM

ZR explicó los problemas de gestión de contactos en el sistema CRM cuando los participantes modifican sus datos después de la inscripción, lo que causa entradas duplicadas en el gestor de eventos.

ZR aclaró que la información mostrada debe prevalecer sobre los datos históricos de CRM, priorizando siempre lo que el contacto ha introducido personalmente.

Alejandro preguntó sobre los diferentes puntos de acceso al sistema donde los contactos verían información diferente según si el evento ha terminado, y ZR confirmó que se mostraría la información más reciente introducida por el contacto.

---

### Gestión de Datos de Contactos

ZR y Alejandro discutieron la gestión de datos de contactos en el sistema de eventos, enfocándose en cómo se manejan los contactos inscritos manualmente y la trazabilidad de eventos.

ZR expresó preocupación sobre la moderación de grandes listas de contactos y sugirió consultar con África sobre posibles soluciones técnicas.

La conversación se centró en asegurar que el primer evento de cada contacto se registre correctamente en la ficha de contacto para análisis posterior.

---

### Carga Masiva de Contactos Técnicos

ZR explicó los problemas técnicos con la carga masiva de contactos, incluyendo:
- errores de validación
- posibles duplicados

Señaló que los formularios deben tener las mismas variaciones restrictivas que el CRM para evitar errores de entrada de datos.

ZR también describió una funcionalidad separada que utiliza un CSV con datos funcionales para crear contactos e intereses, donde el sistema identifica errores y potenciales duplicados para su gestión posterior.

---

### Proceso de Carga Masiva de Contactos

ZR explicó un proceso histórico para cargar datos de contactos de manera masiva utilizando una herramienta llamada Business Card que se implementó en 2009 para simular el funcionamiento de una tarjeta de visita digital.

La herramienta permitía crear contactos con información como:
- nombres
- empresas
- industrias
- relaciones

Guardando los datos como archivos CSV con un límite de caracteres específico.

ZR demostró el proceso funcional mostrando la interfaz donde se podían introducir datos de contacto y relaciones, incluyendo campos como:
- email
- teléfonos
- direcciones

Aunque reconoció que la herramienta ya no se utiliza actualmente.

---

### Sistema Q.R.M y Detección Duplicada

ZR discutió el funcionamiento del sistema Q.R.M y su capacidad para detectar contactos duplicados durante la carga masiva.

Explicó que el sistema ya identifica cuando un contacto existe y no permite altas duplicadas, pero cuestionó si este requisito es necesario para el gestor de contactos.

ZR mencionó que el objetivo principal es mostrar los resultados de la gestión de contactos y permitir que el usuario procese la información posteriormente.

---

### Gestor de Contactos Funcionalidad

ZR explicó la funcionalidad del gestor de contactos, incluyendo:
- la gestión de duplicados
- la carga masiva
- la moderación de datos

Se discutieron los diferentes casos de uso, como:
- la moderación de contactos existentes
- la gestión de nuevos contactos desde formularios

ZR también mostró cómo se mantiene la trazabilidad de las modificaciones de datos y las acciones realizadas en el sistema.

Alejandro confirmó que entendió la explicación y acordaron dejar la reunión aquí.
