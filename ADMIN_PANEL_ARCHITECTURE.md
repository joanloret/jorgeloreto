# Panel central «Modificar» — arquitectura y despliegue seguro

## Objetivo
Ofrecer desde cada sitio una entrada al panel central con autenticación de servidor, permisos por proyecto/sucursal/módulo y confirmación de identificadores antes de guardar.

## Inventario auditado (rama predeterminada: main)

| Repositorio | Arquitectura observada | Área que requerirá integración |
|---|---|---|
| BOTDRIVE | Flask/Python en Render; Google Sheets/Drive y webhook de WhatsApp | Contenido, registros y sucursales; respetar controles de administrador existentes |
| 9 | Sitio estático HTML/CSS/JS en Render; Pages Functions para reacciones | Contenido y metadatos de demos; no exponer secretos ni editar datos de reacciones como contenido |
| jorgeloreto | Portafolio HTML/CSS estático | Página de entrada al panel y enlaces por proyecto |
| Horarios-847 | Cloudflare Pages Functions; token de Google validado en servidor; API de consulta | Edición de horarios solo con endpoint administrativo nuevo, lista permitida y almacenamiento configurado |
| TECH | Sitio HTML/CSS estático | Contenido público; requiere API para guardar |
| turn-on | Next.js | Integración según rutas, servidor y despliegue reales; no asumir hosting |
| FIMSS | Proyecto Flutter | Administración web separada o panel web compatible; no modificar app móvil como si fuera sitio estático |
| Identificador_Dactilar-master | README de título; no se encontró index.html en la raíz | Descubrir punto de entrada real antes de insertar UI |
| Ringtones-master | README de título; no se encontró index.html en la raíz | Descubrir punto de entrada real antes de insertar UI |
| D-Notch | Aplicación nativa macOS (Swift) | Sitio informativo separado; la app nativa no es una página web editable |

## Contrato de seguridad para guardar cambios
Cada operación debe incluir y mostrar en una pantalla de revisión:
- `project_id`: repositorio/proyecto de destino.
- `branch_id`: sucursal o `global` cuando no aplique.
- `module_id`: sección o módulo funcional.
- `record_id`: identificador estable del registro; nunca seleccionar solo por texto visible.
- `action`, versión actual del registro y resumen del cambio.

El servidor debe autenticar la sesión, comprobar la lista de usuarios autorizados y los permisos del proyecto, validar los identificadores contra el servidor y rechazar cambios obsoletos. El cliente no puede decidir por sí mismo que una persona es administradora.

## Bloqueos que impiden habilitar guardado en producción
1. No existe todavía un backend administrativo común confirmado para todos los repositorios.
2. El servicio Render disponible para BOTDRIVE es la aplicación productiva del bot; no se debe reutilizar para paneles de otros proyectos sin aislar rutas, permisos y datos.
3. El sitio estático de música tiene una API de reacciones, pero no es un sistema de administración general.
4. Horarios-847 ya valida tokens de Google para consulta, pero su README indica que la configuración de OAuth y la fuente de datos deben completarse y que no se debe publicar como producción todavía.
5. No se deben guardar credenciales, tokens ni claves en el frontend o en GitHub.

## Estrategia segura
- Crear un servicio administrativo separado y protegido.
- Usar Google Identity (o un proveedor acordado) con validación del token en servidor y allowlist de correos.
- Guardar los secretos solo en variables de entorno del backend.
- Añadir adaptadores específicos por proyecto; no ofrecer acciones genéricas de escritura para un módulo sin almacenamiento y autorización verificados.
- Activar las operaciones de escritura una por una tras probar autenticación, autorización, confirmación de identificadores, auditoría y rollback.
- Mantener los despliegues existentes y no borrar ni fusionar repositorios duplicados durante la integración inicial.
