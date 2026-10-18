# Centro de administración de proyectos

Este directorio contiene el **prototipo informativo** del futuro centro «Modificar».

## Estado de seguridad

- No autentica usuarios.
- No edita ni guarda datos.
- No debe considerarse un panel privado aunque la página incluya `noindex`.
- No incluir contraseñas, tokens, correos privados ni datos operativos en este directorio.
- No conectar formularios de escritura hasta tener un backend que valide identidad, lista de autorización y permisos en cada solicitud.

## Abrir

Abre `index.html` en un navegador para revisar el inventario y la ruta de implementación.

## Próxima fase técnica

1. Confirmar el dominio y la plataforma elegidos para alojar el backend central.
2. Configurar autenticación en servidor y cuentas autorizadas mediante variables de entorno.
3. Implementar auditoría, control de versiones, validación de IDs y rollback.
4. Añadir un adaptador de un solo proyecto piloto y pruebas de seguridad.
5. Activar escrituras solo después de probar el despliegue en un entorno no productivo.

Ver [ADMIN_PANEL_ARCHITECTURE.md](../ADMIN_PANEL_ARCHITECTURE.md) y el [issue de implementación](https://github.com/joanloret/jorgeloreto/issues/1).
