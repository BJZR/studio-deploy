# Studio

Chat multi-IA con herramientas de texto y documentos. Esta carpeta es la versión compilada y publicada
con GitHub Pages: **no la edites**, se genera sola desde el repositorio privado `studio-src`.

Studio no usa servidor. Todo corre en tu navegador y, si quieres, guarda tus datos **cifrados** en repositorios
privados de tu cuenta (`studio-db`, `studio-db-1`, …).

## Paso a paso: conectar tus datos de GitHub

### 1. Crea el token de acceso

1. En GitHub: foto de perfil → **Settings** → **Developer settings** → **Personal access tokens** → **Fine-grained tokens**.
2. Pulsa **Generate new token** y ponle de nombre `studio`.
3. **Expiration**: elige una fecha (por ejemplo, 90 días).
4. **Repository access** → **Only select repositories** → elige `studio-db` (y `studio-db-1`, `studio-db-2`… si ya existen).
5. **Permissions** → **Repository permissions** → **Contents: Read and write**.
6. *(Opcional)* **Administration: Read and write**, solo si quieres que Studio cree solo los repos `studio-db-1`, `studio-db-2`…
   cuando uno se llene. Con «Only select repositories» GitHub no permite crear repos nuevos: si falla, Studio te avisará y
   puedes crearlos con `scripts/new-shard.sh` y añadirlos al token.
7. **Generate token** y copia el valor (empieza por `github_pat_`). GitHub solo lo muestra una vez.

### 2. Conéctalo en Studio

1. Abre la web, pulsa **⚙ Proveedores** y baja hasta **GitHub (datos cifrados)**.
2. Escribe tu usuario, el token y una **contraseña de cifrado** de al menos 10 caracteres.
3. Pulsa **Conectar**. Studio crea `studio-db` (privado) si no existe y empieza a guardar tus datos cifrados.

En otro dispositivo repite el paso 2 con **la misma contraseña de cifrado**.

### Importante

- El token se guarda en tu navegador **cifrado con tu contraseña de cifrado**; cada vez que abras Studio te la pedirá.
- **Si pierdes la contraseña de cifrado, tus datos no se pueden recuperar.** Guárdala en un gestor de contraseñas.
- Si crees que el token se filtró, revócalo en GitHub y crea otro.
- Los textos que envías a un proveedor de IA se rigen por la política de ese proveedor. Las llamadas salen directo del
  navegador, así que la API debe permitir CORS (con Ollama: `OLLAMA_ORIGINS=*`).

## Proveedores de IA

En **⚙ Proveedores** eliges uno de la lista y pegas tu API key. Hay tres tipos de API; casi todo el mercado usa el primero:

| Tipo | Proveedores incluidos |
|---|---|
| Compatible con OpenAI | OpenAI (ChatGPT), xAI (Grok), Mistral, DeepSeek, Groq, OpenRouter, Together AI, Fireworks AI, Perplexity y modelos locales (Ollama, LM Studio, llama.cpp) |
| Anthropic | Claude |
| Google Gemini | Gemini |

- **Personalizado:** hay una opción por cada tipo; escribe la URL base de cualquier otra API. Si necesita una autenticación propia, usa **Cabeceras extra** (JSON, por ejemplo `{"api-key": "…"}`).
- **Cargar modelos:** pide al proveedor la lista de modelos disponibles para tu clave, así no dependes de nombres que cambian.
- **Probar conexión:** envía un mensaje corto antes de guardar.
- **CORS:** sin servidor, las llamadas salen directo del navegador, y la API debe permitirlo. Claude se llama con la cabecera que Anthropic exige para uso en navegador. No he podido confirmar el CORS de todos los proveedores (por ejemplo Grok): si uno lo bloquea, Studio lo indica con un mensaje claro y tendrás que usar otro proveedor. Con Ollama: `OLLAMA_ORIGINS=*`.

## Licencia

Todos los derechos reservados (ver `LICENSE`).
