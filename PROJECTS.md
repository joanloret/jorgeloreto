# Portafolio maestro de proyectos

Inventario central de proyectos de Jorge Loreto. Los repositorios siguen independientes para conservar historial, permisos, configuración, despliegues y responsables. Este documento distingue entre **página informativa**, **aplicación publicada** y **servicio backend**: no son equivalentes.

## Publicación del portafolio

- **Sitio central:** https://jorgeloreto-portfolio.onrender.com/
- **Repositorio:** [jorgeloreto](https://github.com/joanloret/jorgeloreto)
- **Hosting:** Render Static Site, conectado a `main` con despliegue automático.
- **Costo previsto:** $0 para el servicio estático dentro de los límites del plan gratuito; revisar el uso de ancho de banda en Render.
- **Páginas por proyecto:** la carpeta `proyectos/` contiene una ficha independiente para cada proyecto identificado.
- **SEO básico:** metadatos por página, URL canónica, Open Graph, `robots.txt`, `sitemap.xml` y favicon.

## Inventario

| Grupo | Proyecto | Repositorio | Estado conocido | Página / siguiente paso |
|---|---|---|---|---|
| DRIVECOPP · 847 | Bot_847 | [BOTDRIVE](https://github.com/joanloret/BOTDRIVE) | Backend Flask en Render; despliegues recientes reportados como exitosos. El servicio gratuito puede dormir por inactividad. | [Ficha](https://jorgeloreto-portfolio.onrender.com/proyectos/bot-847.html) · [Servicio](https://botdrive-r4si.onrender.com) |
| DRIVECOPP · 847 | Horarios_847 | [Horarios-847](https://github.com/joanloret/Horarios-847) | Aplicación privada de horarios. README indica que no debe considerarse producción hasta configurar OAuth, usuarios permitidos y fuente real. | [Ficha](https://jorgeloreto-portfolio.onrender.com/proyectos/horarios-847.html) · publicar solo tras validación |
| DRIVECOPP · 847 | Incumplimieto_Usf | Repositorio por identificar | No se ha identificado un repositorio correcto; no se vincula con otra aplicación por suposición. | [Ficha provisional](https://jorgeloreto-portfolio.onrender.com/proyectos/incumplimieto-usf.html) · confirmar repositorio y propósito |
| Portafolio | TECH | [TECH](https://github.com/joanloret/TECH) | Repositorio público; la URL de producto no está verificada. | [Ficha](https://jorgeloreto-portfolio.onrender.com/proyectos/tech.html) · revisar README y contenido |
| Música | 9 Loretos | [9](https://github.com/joanloret/9) | Sitio estático en Render: [loretos.onrender.com](https://loretos.onrender.com). La ficha del repositorio documenta reproductores oficiales y una API de reacciones que requiere configurar Cloudflare D1. | [Sitio musical](https://loretos.onrender.com) · [Ficha](https://jorgeloreto-portfolio.onrender.com/proyectos/proyecto-musical.html) |
| Portafolio | FIMSS | [FIMSS](https://github.com/joanloret/FIMSS) | Repositorio Flutter. Existe un proyecto Supabase llamado FIMSS; la base de datos estuvo inactiva y la conexión aún debe verificarse. No asumir que el repositorio y la base ya están conectados. | [Ficha](https://jorgeloreto-portfolio.onrender.com/proyectos/fimss.html) · revisar compilación y Supabase |
| Portafolio | Ringtones | [Ringtones-master](https://github.com/joanloret/Ringtones-master) | Código disponible; tecnología y estado de publicación por auditar. | [Ficha](https://jorgeloreto-portfolio.onrender.com/proyectos/ringtones.html) · revisar archivos y requisitos |
| Portafolio | Identificador dactilar | [Identificador_Dactilar-master](https://github.com/joanloret/Identificador_Dactilar-master) | Código disponible; aplicación y entorno de ejecución por auditar. No publicar datos biométricos reales. | [Ficha](https://jorgeloreto-portfolio.onrender.com/proyectos/identificador-dactilar.html) · revisar privacidad y tecnología |
| Portafolio | D-Notch / DynamicNotch | [D-Notch](https://github.com/joanloret/D-Notch) | Aplicación nativa macOS. Una página web informativa no sustituye ni convierte la app en una aplicación web. | [Ficha](https://jorgeloreto-portfolio.onrender.com/proyectos/d-notch.html) · revisar licencia, autoría y proceso de distribución |
| Portafolio | turn-on | [turn-on](https://github.com/joanloret/turn-on) | Proyecto Next.js; no hay URL de producción verificada. | [Ficha](https://jorgeloreto-portfolio.onrender.com/proyectos/turn-on.html) · revisar rutas, variables y build antes de publicar |
| Portafolio | jorgeloreto | [jorgeloreto](https://github.com/joanloret/jorgeloreto) | Portafolio y fichas de proyectos publicados como sitio estático. | [Abrir portafolio](https://jorgeloreto-portfolio.onrender.com/) |

## Estrategia de alojamiento sin costo

1. **Páginas estáticas y fichas informativas:** mantener HTML/CSS/JS sin dependencias y desplegar en un hosting estático gratuito. Para sitios de bajo tráfico ya conectados a Render, revisar el límite de ancho de banda; Cloudflare Pages es la alternativa a evaluar si se necesita más margen estático.
2. **Aplicaciones web dinámicas:** elegir plataforma después de verificar framework, persistencia, autenticación y límites. El plan gratuito de Render puede dormir por inactividad; no se debe presentar como alta disponibilidad.
3. **Datos compartidos:** no usar almacenamiento local del navegador como fuente oficial. Para datos operativos, evaluar persistencia, permisos por rol, copias de seguridad, exportación y recuperación antes de pasar a producción.
4. **Supabase Free:** útil para prototipos y pilotos; sus proyectos pueden pausarse por inactividad y el plan gratuito no equivale a un SLA de producción. Verificar el estado del proyecto FIMSS antes de aplicar migraciones.
5. **Dominio:** usar primero el subdominio gratuito del proveedor. Un dominio propio normalmente implica un costo anual, así que no se presupone como requisito.
6. **Seguridad:** ningún secreto, token, clave privada, teléfono de administrador ni dato biométrico debe publicarse en el repositorio o en el frontend.
7. **Despliegues:** probar en una rama o entorno de prueba; publicar cambios de producción solo después de revisar los flujos esenciales y confirmar que no se alteran datos reales.

## Prioridades de auditoría

- **P0 — integridad y acceso:** verificar Supabase FIMSS, autenticación y permisos; confirmar fuente de datos y autorización de Horarios_847.
- **P1 — operación:** probar el flujo de administración de BOTDRIVE, persistencia, recuperación de errores y cold start del plan gratuito.
- **P1 — producto web:** revisar las funciones reales de TECH, turn-on, Ringtones e Identificador dactilar antes de prometer características en sus páginas.
- **P2 — publicación:** validar 9 Loretos y la API de reacciones, incluido el binding D1.
- **P2 — privacidad y distribución:** revisar el tratamiento de datos del Identificador dactilar y la licencia/autoría de D-Notch.
- **P3 — orden:** decidir nombres definitivos de repositorios y servicios solo después de revisar integraciones, workflows, URLs y enlaces entrantes.

## Reglas de mantenimiento

- No eliminar ni fusionar repositorios solo por nombres parecidos; comparar código, historial, dependencias y despliegues.
- Marcar una aplicación como **producción** solo cuando la URL, autenticación, datos y flujos principales hayan sido probados.
- Cada nuevo proyecto debe registrar propósito, repositorio, URL, hosting, variables requeridas (nunca sus valores secretos), responsable y procedimiento de recuperación.
- Revisar mensualmente límites de uso, despliegues fallidos, dependencias y enlaces rotos.

