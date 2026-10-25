# 🎓 Premios entre amigos — guía paso a paso

Juego de diplomas para el grupo: cada amigo se inscribe con su nombre y una clave, propone categorías, se votan entre todos, tú repartes los diplomas (2 por persona), haces una presentación sorpresa y al final cada quien descarga los suyos como imagen.

- Los amigos usan `index.html`. Tú usas `admin.html` (solo funciona con tu cuenta de Google).
- Sin servidor propio: GitHub Pages (la página) + Firebase (los datos). Son archivos estáticos, no hay que instalar nada.

---

## PARTE 1 · Instalación (una sola vez, ~20 minutos)

### Paso 1. Crear un proyecto de Firebase NUEVO
Usa un proyecto aparte del amigo secreto: las reglas de seguridad son por proyecto y estas pisarían las otras.

1. Entra a https://console.firebase.google.com → **Agregar proyecto** → ponle un nombre (ej. `premios-amigos`). Puedes desactivar Google Analytics.
2. **Compilación → Firestore Database → Crear base de datos** → modo **producción** → escoge una región.
3. **Compilación → Authentication → Comenzar → Método de acceso**: activa **Anónimo** y **Google** (en Google pon tu correo como correo de asistencia).
4. **Configuración del proyecto (⚙) → Tus apps → icono Web `</>`**: registra una app (cualquier nombre). Copia el objeto `firebaseConfig` que te muestra.

### Paso 2. Pegar la configuración en el código
**Ya viene hecho:** `js/config.js` trae los datos del proyecto `diplomas-87bfe`. Si algún día cambias de proyecto, reemplaza ahí el `firebaseConfig`. También puedes cambiar tu firma de los diplomas (`SIGNER_NAME`, `SIGNER_TITLE`).

### Paso 3. Reglas de seguridad (esto es lo que protege los datos)
1. **Ya viene hecho:** `firestore.rules` trae `maicolletrado@gmail.com` como correo del administrador (si cambias de cuenta, edita ese correo).
2. En Firebase: **Firestore Database → pestaña Reglas** → borra lo que haya, pega todo el contenido de `firestore.rules` y pulsa **Publicar**.

Con esto solo tú puedes ver los votos y los resultados. Cada amigo solo puede inscribirse (mientras las inscripciones estén abiertas) y guardar sus propias propuestas y votos, demostrando quién es con su clave.

### Paso 4. Subir a GitHub Pages
1. En GitHub crea un repositorio nuevo (ej. `premios`).
2. Sube todo el contenido de esta carpeta (los archivos, no la carpeta contenedora).
3. **Settings → Pages → Build and deployment → Deploy from a branch → `main` / `(root)` → Save**.
4. Espera 1–2 minutos. Tus enlaces serán:
   - Amigos: `https://TU_USUARIO.github.io/premios/`
   - Tú: `https://TU_USUARIO.github.io/premios/admin.html`

### Paso 5. Autorizar tu dominio en Firebase
**Authentication → Configuración → Dominios autorizados → Agregar dominio** → `TU_USUARIO.github.io` (sin `https://`). Sin esto el botón “Entrar con Google” del panel falla.

### Paso 6. Primer ingreso
1. Abre `.../admin.html` → **Entrar con Google** con el correo que pusiste en las reglas.
2. Pestaña **Resumen**: en **Ajustes** escribe el nombre del evento (sale en el diploma como “Premios …”) y la fecha; guarda.
3. Abre `.../premios/` en otra pestaña o en tu celular y **regístrate tú también** como un amigo más (nombre + clave).

---

## PARTE 2 · Cómo llevar el juego (fase por fase)

Todo se maneja desde **Resumen → Fase actual** con los botones “Siguiente fase” / “Fase anterior”.

### Fase 1 · Inscripción
- Pestaña **Personas → Compartir por WhatsApp**: manda el enlace al grupo.
- Cada amigo escribe su nombre y una clave (mínimo 4 caracteres) y queda registrado. Para volver a entrar usa el mismo nombre y la misma clave.
- Tú ves quién se ha registrado. Si alguien se registra con un nombre equivocado o ajeno, quítalo con 🗑. Si alguien olvida su clave, 🔄 y vuelve a entrar con su nombre para crear otra.
- Si dos amigos se llaman igual, uno debe usar nombre y apellido.

### Fase 2 · Propuestas de categorías
- Cada persona debe escribir **exactamente 5 categorías distintas** (la app no deja guardar con menos; las reglas también lo exigen).
- Pestaña **Propuestas → Checklist**: ves quién ya completó ✅ 5/5, quién va a medias ⚠️ y quién no ha empezado ⏳. El botón **Recordar por WhatsApp** arma un mensaje con los nombres pendientes.
- Cuando todos estén en ✅, pasa a la siguiente fase. Si falta alguien, la app te avisa quién antes de cerrar.

### Fase 3 · Armando las categorías (solo tú)
- Al entrar aquí **se cierran las inscripciones** y nadie puede enviar más propuestas.
- Pestaña **Propuestas → Ideas recibidas**: toca ＋ en las mejores (las repetidas aparecen juntas con ×N).
- Pestaña **Categorías**: edita los nombres, ordénalas con ↑↓, agrega un **premio** opcional a cada una (sale en el diploma) y quita las que sobren. Necesitas **personas × 2**: con 12 personas, 24 categorías.

### Fase 4 · Categorías consolidadas
- Todos ven la lista oficial antes de votar. Es el momento para que vayan pensando a quién nominar en cuál.

### Fase 5 · Votación
- Cada persona ve a las demás. Para cada una elige **en qué categoría la nomina**. Esa categoría ya no puede volver a usarla y a esa persona ya no puede darle otro voto.
- Con 12 personas son 11 votos por persona (132 en total) y todos reciben votos. Los votos son secretos.
- Pestaña **Votos**: ves quién ya terminó (11/11) y el conteo en vivo. Los votos parciales también cuentan.

### Fase 6 · Reparto (solo tú)
- Pestaña **Resultados → Calcular reparto**: la app asigna cada categoría maximizando los votos, con exactamente 2 diplomas por persona. Los empates se sortean (🎲 Re-sortear).
- Puedes cambiar el ganador de cualquier categoría con el selector, ver cualquier diploma con 🎓 y mezclar el orden con 🔀.
- Revisa que cada persona tenga 2 y pulsa **Ir a la presentación**. Tus amigos solo ven “¡Los resultados son sorpresa!”.

### Fase 7 · Presentación (solo tú)
- Pestaña **Presentación → Iniciar presentación**: modo pantalla completa. Comparte tu pantalla o proyéctala.
- Teclas: → o espacio = avanzar · ← = retroceder · Esc = salir (en el celular, los botones).
- Cada categoría tiene dos pasos: primero el nombre de la categoría con tambores y luego el ganador con confeti y su diploma. Al final hay un resumen con todos.

### Fase 8 · Diplomas publicados
- Cuando termines, **Presentación → Publicar diplomas a los amigos**. Cada quien entra con su nombre y su clave, ve todos los resultados y descarga o comparte sus diplomas como imagen.
- Si te arrepientes, “Volver a ocultar”.

---

## Preguntas frecuentes

- **El botón de Google no abre nada o da error:** revisa el Paso 5 (dominio autorizado) y que Google esté activado en Authentication.
- **Dice “Sin permiso” en el panel:** el correo en `firestore.rules` no es el de la cuenta con la que entraste, o no publicaste las reglas (Paso 3).
- **Un amigo no puede registrarse:** puede que las inscripciones estén cerradas (pestaña Personas → Abrir inscripciones) o que ya exista ese nombre.
- **Alguien se equivocó de nombre al registrarse:** quítalo en Personas (🗑) y que se registre de nuevo.
- **Cambié las reglas o el código:** vuelve a pegar las reglas en Firebase y re-sube los archivos a GitHub; los cambios aparecen en 1–2 minutos.
- **Probar en tu computador:** abre una terminal en la carpeta y corre `python3 -m http.server`; entra a `http://localhost:8000` (agrega `localhost` a los dominios autorizados si usas Google ahí).
- **Pruebas del algoritmo de reparto:** `npm test` (requiere Node).
