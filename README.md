# 🍻 Contador de Fiesta

App web gratis para llevar el marcador de chupitos, cervezas y cubatas de: Selva, Fabro, Lima, Alejandro, Carlitos, Juan Edu, Lajara, Illidge y Sergio.

Los contadores se sincronizan en tiempo real entre todos los móviles que tengan la web abierta.

## Paso 1 — Crear la base de datos gratis en Firebase (5 min)

1. Ve a **https://console.firebase.google.com** e inicia sesión con tu cuenta de Google.
2. Clic en **"Crear un proyecto"**. Ponle el nombre que quieras (ej: `contador-fiesta`). Puedes desactivar Google Analytics, no hace falta.
3. Una vez creado, en el menú lateral ve a **Build → Realtime Database**.
4. Clic en **"Crear base de datos"**.
   - Elige la ubicación **Europe (europe-west1)** (más cerca y evita problemas de latencia).
   - En las reglas de seguridad, elige **"Empezar en modo de prueba"** (permite lectura/escritura sin login durante 30 días — para una fiesta puntual es más que suficiente. Si quieres dejarlo indefinidamente, luego te explico cómo hacerlo seguro).
5. En el menú lateral, clic en el icono de engranaje ⚙️ → **"Configuración del proyecto"**.
6. Baja hasta **"Tus apps"** y clic en el icono `</>` (Web).
7. Ponle un apodo (ej: `web`) y clic en **"Registrar app"**. NO hace falta activar Firebase Hosting.
8. Firebase te mostrará un bloque de código con `firebaseConfig = { apiKey: ..., authDomain: ..., ... }`. **Copia ese bloque completo.**

## Paso 2 — Pegar tu configuración en el archivo

1. Abre `index.html` con cualquier editor de texto.
2. Busca esta parte (cerca de la línea 210):

```js
const firebaseConfig = {
  apiKey: "TU_API_KEY",
  authDomain: "TU_PROYECTO.firebaseapp.com",
  databaseURL: "https://TU_PROYECTO-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "TU_PROYECTO",
  storageBucket: "TU_PROYECTO.appspot.com",
  messagingSenderId: "000000000000",
  appId: "TU_APP_ID"
};
```

3. Sustitúyelo entero por el bloque que copiaste de Firebase en el paso anterior. Asegúrate de que `databaseURL` esté incluido (a veces Firebase no lo pone automáticamente si no seleccionaste bien la región — si falta, ve a Realtime Database en la consola y copia la URL que aparece arriba de la página, tipo `https://contador-fiesta-default-rtdb.europe-west1.firebasedatabase.app`).
4. Guarda el archivo.

## Paso 3 — Publicar en GitHub Pages (gratis)

1. Ve a **https://github.com** e inicia sesión.
2. Clic en **"New repository"**. Nómbralo, por ejemplo, `contador-fiesta`. Puede ser público. Clic en **"Create repository"**.
3. En la página del repo recién creado, clic en **"uploading an existing file"** (o arrastra los archivos).
4. Arrastra `index.html` (y este `README.md` si quieres) y haz commit.
5. Ve a la pestaña **Settings** del repositorio → menú lateral **Pages**.
6. En "Branch", selecciona `main` y carpeta `/ (root)` → **Save**.
7. Espera 1-2 minutos y GitHub te dará una URL tipo:
   `https://tu-usuario.github.io/contador-fiesta/`

¡Esa es la URL que compartes con todo el grupo! Cada uno la abre desde su móvil y todos ven los mismos contadores en directo.

## Notas

- **Editar nombres:** si quieres cambiar la lista de personas, edita el array `PERSONAS` dentro de `index.html`.
- **Reiniciar contadores** (ej. para la siguiente fiesta): entra en Firebase Console → Realtime Database → y borra el nodo `contadores` (clic en los tres puntos → Eliminar), o simplemente crea otro proyecto Firebase nuevo para cada evento.
- **Seguridad:** en modo de prueba, cualquiera con el enlace a tu Realtime Database (no la web, la URL de la base de datos) podría leer/escribir. Para una noche de fiesta entre amigos no supone ningún riesgo real, pero las reglas caducan a los 30 días y dejarán de funcionar los contadores hasta que las renueves o las cambies a modo público permanente. Si quieres dejarlo funcionando indefinidamente, dímelo y te paso las reglas.
