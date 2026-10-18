# Dash Loreto — concepto de centro de control

Este directorio contiene el **prototipo informativo de Dash Loreto**, una idea para reunir en un solo lugar la administración de los proyectos de Jorge Loreto. Todavía no es una aplicación funcional ni un servicio privado.

## Estado de seguridad

- No autentica usuarios ni restringe el acceso a una sola persona.
- No edita ni guarda datos.
- La meta del proyecto es que solo el propietario pueda acceder y modificar, pero esa regla aún no está implementada. `noindex` no es seguridad.
- No incluir contraseñas, tokens, correos privados ni datos operativos en este directorio.
- No conectar formularios de escritura hasta tener un backend que valide identidad, lista de autorización y permisos en cada solicitud.

## Abrir

Abre `index.html` en un navegador para revisar el inventario y la ruta de implementación.

## Arquitectura propuesta

- **Mac:** entorno principal para desarrollar, revisar y probar cambios.
- **GitHub:** código versionado y cambios mediante ramas y revisiones.
- **Cloudflare (candidato):** interfaz web y API administrativa aislada, sujeto a validar requisitos.
- **Autenticación:** proveedor de identidad con verificación en servidor y allowlist de una sola cuenta propietaria.
- **Datos:** almacenamiento persistente, auditoría y recuperación; se elegirá después de revisar las necesidades de cada integración.
- **Integraciones:** adaptadores por proyecto, con permisos mínimos y sin compartir secretos con el navegador.

El panel web no dependerá de que el Mac esté encendido. El Mac será el espacio principal de trabajo, no necesariamente el servidor.

## Próxima fase técnica

1. Revisar el inventario de proyectos y confirmar qué datos requiere administrar cada uno.
2. Elegir proveedor de identidad y definir cómo registrar de forma segura la única cuenta propietaria.
3. Diseñar API, modelo de datos, auditoría, versionado y recuperación.
4. Crear un entorno de pruebas aislado y un adaptador piloto sin escrituras productivas.
5. Ejecutar pruebas de autenticación, autorización, acceso no autorizado, recuperación y concurrencia.
6. Considerar cualquier despliegue solo tras una revisión explícita; esta fase no autoriza despliegues ni cambios productivos.

Ver [ADMIN_PANEL_ARCHITECTURE.md](../ADMIN_PANEL_ARCHITECTURE.md) y el [issue de implementación](https://github.com/joanloret/jorgeloreto/issues/1).
