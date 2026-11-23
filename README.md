# Préstamo de equipo en Odoo

Práctica de Programación de Negocios · UNICAH · Odoo 20.0

**Estudiante:** José Nieto  
**Número de cuenta:** 0801 2005 17968

Módulo: `prestamo_unicah` — control de equipos, préstamos y devoluciones de la universidad.

## Respuestas

### Paso 1. Catálogo de equipos

1. Al desmarcar **Activo**, Odoo oculta el equipo de las listas y búsquedas (`active=False`), pero el registro sigue en la base de datos y los préstamos históricos siguen referenciándolo. Es mejor que borrarlo porque conserva el historial y no rompe las llaves foráneas de las líneas de préstamo.
2. `copy=False` evita que al duplicar un equipo se copie también el código de inventario. Así cada copia queda sin código y hay que asignarle uno propio y único.

### Paso 2. Registro de préstamos

1. `_name = "prestamo.prestamo"` define el modelo nuevo (su nombre técnico y su tabla en la base de datos). `_inherit = ["mail.thread"]` no crea otro modelo: le agrega a este las funciones del chatter (mensajes, seguidores y seguimiento de cambios).
2. `tracking=True` en `state` hace que Odoo registre en el chatter cada cambio de valor de ese campo (por ejemplo "Borrador → Prestado"), con fecha y usuario. Se verá funcionar en el paso 4, cuando los botones cambien el estado.
