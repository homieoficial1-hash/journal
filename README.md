# Journal

Journal personal de trading. Entras con tu cuenta de Google y los datos se guardan en Firestore, así que ves lo mismo en la computadora y en el celular.

**Archivos**

| Archivo | Para qué |
|---|---|
| `index.html` | La app completa |
| `firebase-config.js` | La configuración de tu proyecto de Firebase y tu correo |
| `firestore.rules` | Las reglas que hacen que solo tú puedas leer y escribir |

---

## Configuración paso a paso

No necesitas instalar nada: todo se hace desde el navegador. Son unos 20 minutos.

### 1. Crear el proyecto de Firebase

1. Entra a <https://console.firebase.google.com> con tu cuenta de Google.
2. **Crear un proyecto** → nombre, por ejemplo `trading-journal`.
3. Google Analytics: **desactívalo** (no hace falta) → **Crear proyecto**.

El plan gratuito (Spark) alcanza de sobra para uso personal.

### 2. Activar el inicio de sesión con Google

1. Menú izquierdo → **Compilación → Authentication** → **Comenzar**.
2. Pestaña **Método de acceso** → **Google** → **Habilitar**.
3. Elige tu correo como "correo de asistencia" → **Guardar**.

### 3. Crear la base de datos Firestore

1. Menú izquierdo → **Compilación → Firestore Database** → **Crear base de datos**.
2. Ubicación: la más cercana a ti (por ejemplo `nam5 (United States)`). No se puede cambiar después.
3. Elige **Iniciar en modo de producción** → **Crear**.
4. Abre la pestaña **Reglas**, borra lo que haya y pega el contenido de `firestore.rules`.
5. Cambia `TU_CORREO@gmail.com` por **tu correo de Google exacto** → **Publicar**.

Estas reglas son el candado real: aunque alguien encuentre la página y entre con su Google, Firestore no le deja ver ni tocar nada.

### 4. Registrar la app web y copiar la configuración

1. Arriba a la izquierda, ⚙️ → **Configuración del proyecto**.
2. Abajo, en **Tus apps**, haz clic en el ícono **`</>`** (Web).
3. Ponle un nombre (`journal`). **No** marques Firebase Hosting → **Registrar app**.
4. Te muestra un bloque `const firebaseConfig = { apiKey: "...", ... }`. Cópialo.
5. Abre `firebase-config.js` y reemplaza los valores con los tuyos.
6. Cambia también `ALLOWED_EMAIL` por tu correo (el mismo del paso 3).

> Estos valores no son secretos: cualquier app web de Firebase los muestra. Lo que protege tus datos son las reglas del paso 3.

### 5. Subir los archivos a GitHub (repositorio público)

1. Entra a <https://github.com/new>.
2. Nombre: `trading-journal`. Marca **Public** → **Create repository**.
3. En la página del repositorio vacío, haz clic en **uploading an existing file**.
4. Arrastra estos 4 archivos: `index.html`, `firebase-config.js`, `firestore.rules` y `README.md`.
5. **Commit changes**.

> Al ser público, cualquiera puede ver el código y el correo permitido, pero **no tus datos**: esos viven en Firestore y las reglas solo dejan entrar a tu cuenta. Si más adelante quieres que nadie vea el código, pasa el repositorio a privado con GitHub Pro (GitHub Pages en repos privados requiere Pro).

### 6. Publicar con GitHub Pages (gratis)

1. En el repositorio: **Settings → Pages**.
2. **Source: Deploy from a branch** → rama **main**, carpeta **/ (root)** → **Save**.
3. En 1–2 minutos aparece arriba la dirección: `https://TU_USUARIO.github.io/trading-journal/`.

Cada vez que cambies un archivo en GitHub, Pages publica la nueva versión solo (tarda uno o dos minutos).

### 7. Autorizar tu dominio en Firebase

Sin este paso, el botón de Google da error `auth/unauthorized-domain`.

1. Firebase → **Authentication → Configuración → Dominios autorizados**.
2. **Agregar dominio** → `TU_USUARIO.github.io` (sin `https://` y sin `/trading-journal`).

### 8. Entrar

1. Abre `https://TU_USUARIO.github.io/trading-journal/` → **Continuar con Google**.
2. Si tenías datos en la versión anterior (en el navegador), ábrela, usa **Exportar copia** y luego, en la nueva, **menú ☰ → Importar copia**.
3. En el celular: abre la misma dirección y, en el menú del navegador, **Agregar a pantalla de inicio**. Queda como una app.

---

## Problemas comunes

| Mensaje | Solución |
|---|---|
| "Falta configurar Firebase en firebase-config.js" | No se pegó la configuración del paso 4, o el archivo no se subió a GitHub. |
| `auth/unauthorized-domain` | Falta el paso 7. |
| "… no tiene acceso a este journal" | El correo en `firebase-config.js` no coincide con la cuenta con la que entraste. |
| "Esta cuenta no tiene acceso a los datos" o "No se pudo guardar (permission-denied)" | El correo en las reglas de Firestore no coincide, o no se publicaron las reglas (paso 3). |
| El botón de Google no hace nada en el celular | El navegador bloqueó la ventana emergente; permite ventanas emergentes para tu sitio. |

## Respaldo

Los datos viven en Firestore. Aun así, de vez en cuando usa **menú ☰ → Exportar copia** para guardar un archivo `.json` de respaldo.
