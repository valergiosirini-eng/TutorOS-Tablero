[README.md](https://github.com/user-attachments/files/29635272/README.md)
# Tablero TuroOS

Tablero de gestión de tareas (mismo artifact que `Tareas_Val_1`, adaptado a este proyecto): vista de tablero por fase, avance por fase, pirámide de prioridades y archivo. Guarda en Supabase, no en localStorage -- se ve igual desde cualquier dispositivo.

## Desplegar (una vez)
Repo ya creado: `valergiosirini-eng/TutorOS-Tablero` (vacío, Pages aún no activado -- verificado 2026-07-03).
1. Sube `index.html` (el de esta carpeta) a la raíz de ese repo.
2. GitHub → repo → Settings → Pages → Source: "Deploy from a branch" → branch `main`, carpeta `/ (root)` → Save.
3. Abre `https://valergiosirini-eng.github.io/TutorOS-Tablero/`.

## Botón "Trabajar con Claude"
Cada tarjeta tiene un botón que abre Claude Desktop directamente en este proyecto (Cowork), con el contexto de esa tarea ya escrito en el mensaje. Usa el esquema oficial `claude://cowork/new?q=...&folder=...` (ver "Open Claude Desktop with a link" en support.claude.com). También hay un botón general en la cabecera para retomar el proyecto sin partir de una tarea concreta.

Cómo funciona en la práctica:
- No es literalmente "la misma conversación" reabierta -- cada clic abre una sesión de Cowork **nueva**, pero anclada a la misma carpeta del proyecto. Como esa carpeta ya tiene `_planning/PROJECT_MEMORY.md` y memoria persistente, Claude recupera el contexto igualmente, sin que tengas que repetir nada.
- Claude Desktop te pedirá confirmar la carpeta cada vez (medida de seguridad normal, no un fallo).
- Requiere: Claude Desktop instalado en el mismo ordenador donde haces clic, con Cowork disponible (plan de pago), y la app abierta o lista para abrirse.
- Deliberadamente **no** hay un chatbot embebido con una API key de Anthropic en este HTML público. Poner una key secreta en una página de GitHub Pages sería el mismo error que encontramos y corregimos en `NoteSummariserClean.py` -- cualquiera que vea el código fuente podría usarla a tu costa. El deep link usa tu sesión ya autenticada en Claude Desktop, sin exponer ninguna credencial.

## Notas
- La key incluida en el archivo es la Supabase *publishable* key del proyecto TuroOS (`bnidngytvlffhrtcafok`) -- pensada para ser pública. La service_role key nunca debe estar aquí.
- Datos: tabla `turoos_tasks` en el mismo proyecto Supabase que usa `RS TutorOS` (tablas `rsos_attempts`/`rsos_term_status`). Un solo proyecto Supabase para todo TuroOS.
- Las fases (columna "Fase") están precargadas con las tareas reales del roadmap MVP acordado en `_planning/PROJECT_MEMORY.md`. Edítalas, archívalas o añade las tuyas desde la propia interfaz -- todo se sincroniza solo.
- Sin autenticación (RLS `anon` abierto), igual que `Tareas_Val_1` -- pensado para uso personal, no para compartir la URL públicamente si no quieres que se edite.
