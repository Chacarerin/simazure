# simazure · Guía de despliegue

> El despliegue lo realiza el usuario de forma manual.

## 1. Características

| | |
|---|---|
| Tipo de sitio | Estático, un solo archivo (`index.html`) |
| Compilación | No requiere |
| Variables de entorno | Ninguna |
| Base de datos | Ninguna |
| Repositorio | `github.com/Chacarerin/simazure` · público · rama `main` |

## 2. Primer despliegue en Vercel

1. En vercel.com, **Add New › Project** e importar el repositorio `Chacarerin/simazure`.
2. **Framework Preset:** `Other`. Dejar vacíos el comando de compilación y el directorio de salida.
3. **Deploy.** Vercel sirve `index.html` en la raíz del dominio asignado.

Cada `push` a `main` publica una versión nueva de forma automática.

## 3. Alternativa sin Vercel

El archivo funciona abierto directamente en el navegador. Para el aula virtual basta subir
`index.html`, renombrado como `GSI-TI3V62-Simulador-Azure.html`.

## 4. Verificación después de publicar

- La página carga sin errores en la consola del navegador.
- `az account show -o table` responde con la suscripción «Azure for Students».
- Recargar la página conserva la sesión anterior; «Reiniciar» la borra.
