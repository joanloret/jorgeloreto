# Dash Loreto — arquitectura propuesta y despliegue seguro

## Objetivo y decisiones del propietario
Dash Loreto es una idea en etapa de diseño: un centro de control para administrar proyectos desde el Mac del propietario y, cuando sea necesario, acceder mediante internet.

Decisiones confirmadas:
- Nombre del proyecto: **Dash Loreto**.
- Uso previsto: Mac + acceso web privado.
- Prioridad: seguridad y acceso exclusivo para el propietario.
- Estado actual: prototipo informativo; no autentica usuarios ni guarda cambios.
- Restricción de esta fase: no fusionar la rama, no desplegar en producción y no habilitar escrituras productivas.

El panel deberá ofrecer una entrada central con autenticación de servidor, permisos por proyecto/sucursal/módulo y confirmación de identificadores antes de guardar.

## Arquitectura recomendada
1. **Mac del propietario:** entorno principal de desarrollo, revisión y pruebas. Mantener una copia local del código y utilizar Git para cambios versionados.
2. **GitHub:** repositorio central del código, ramas de funciones, revisiones y registro de cambios; el repositorio por sí solo no constituye el control de acceso del panel.
3. **Cloudflare (candidato para el acceso web):** Pages para la interfaz y Workers para una API administrativa aislada, sujeto a revisar requisitos y límites antes de seleccionarlo definitivamente.
4. **Identidad y autorización en servidor:** proveedor de identidad con verificación del lado servidor y lista permitida de una única cuenta del propietario. No confiar en botones ocultos, rutas secretas ni validaciones solo del navegador.
5. **Almacenamiento persistente:** elegir una base de datos tras mapear los datos y permisos de cada proyecto. No usar almacenamiento local del navegador como fuente de verdad ni asumir que una instancia temporal conserva los datos.
6. **Integraciones por adaptador:** conectar cada proyecto mediante endpoints explícitos y mínimos permisos. No conceder acceso genérico a todos los repositorios ni exponer secretos en el frontend.

La arquitectura debe permitir que el panel web siga disponible sin que el Mac permanezca encendido; el Mac continúa siendo el espacio principal de trabajo, no necesariamente el servidor de producción.

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
