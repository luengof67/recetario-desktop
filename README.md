# Recetario de Cocina · App de escritorio (Tauri)

Versión de escritorio para Windows del recetario (platos, alérgenos y menús), empaquetada con **Tauri 2**. El HTML original está intacto en `src/index.html`: cualquier cambio que hagas ahí se refleja en la app al recompilar.

## Cómo compilar (GitHub Actions, sin instalar nada en tu PC)

1. Crea un repositorio nuevo en GitHub (por ejemplo `recetario-desktop`).
2. Sube todo el contenido de esta carpeta:
   ```
   git init
   git add .
   git commit -m "Proyecto Tauri inicial"
   git branch -M main
   git remote add origin https://github.com/luengof67/recetario-desktop.git
   git push -u origin main
   ```
3. En GitHub → pestaña **Actions** → workflow **"Compilar app de escritorio (Windows)"** → botón **Run workflow**.
4. Espera ~10-15 minutos la primera vez (las siguientes son más rápidas gracias a la caché de Rust).
5. Al terminar, descarga el artefacto **recetario-windows**: contiene el instalador `.msi` y el `.exe` (NSIS). Cualquiera de los dos sirve; el NSIS instala sin pedir permisos de administrador.

También se compila automáticamente si haces push de una etiqueta que empiece por `v` (ej. `git tag v1.0.0 && git push --tags`).

## Actualizar la app

1. Edita `src/index.html` (es el mismo archivo de siempre).
2. Sube el número de versión en `src-tauri/tauri.conf.json`, `src-tauri/Cargo.toml` y `package.json` (opcional pero recomendable).
3. Push y vuelve a lanzar el workflow.

## Notas

- **No hay firma de código**: Windows SmartScreen puede mostrar un aviso la primera vez ("Más información → Ejecutar de todas formas"). Es normal en apps sin certificado, igual que un APK fuera de Play Store.
- **Requisitos del PC destino**: Windows 10/11 con WebView2 (viene preinstalado en Windows 11 y en la mayoría de Windows 10 actualizados; el instalador lo descarga si falta).
- La app necesita **conexión a internet** para Firestore, Gemini y las fuentes de Google, igual que la versión web.
- El icono se generó a partir de la paleta de la app (verde `#2F5233` / azafrán `#DDA321`). Si quieres cambiarlo, sustituye los archivos de `src-tauri/icons/` o genera un juego nuevo con `npx tauri icon ruta/a/tu-icono.png` (necesita un PNG de 1024×1024).
- Tamaño de ventana inicial: 1200×820, redimensionable, mínimo 900×620. Se ajusta en `src-tauri/tauri.conf.json`.
