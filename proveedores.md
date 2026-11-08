# Registro de proveedores de tokens

Fecha: 2026-11-08. Todo verificado contra las APIs, no de memoria.

## Groq (API gratuita) — la fuente principal

- Clave creada en console.groq.com, nivel gratuito, conectada y verificada
  2026-11-07. Conector `custom.groq`.
- Modelos que lista la clave (11): gpt-oss-20b/120b, qwen/qwen3.8-27b,
  whisper y guardias. Sin modelos Llama de chat en esta clave.
- Base URL OpenAI-compatible: `https://api.groq.com/openai/v1`.
- **Límite medido 2026-11-08: 8.000 TPM.** El prompt de dsh pesa ~4.600
  tokens por llamado; el segundo llamado (4.605 usados + 4.461 pedidos)
  da 429 y dsh lo trata como fatal. El plan Developer (250.000 TPM) es
  de pago.
- La API está detrás de Cloudflare y bloquea el User-Agent por defecto
  de Python (403 error 1010); el helper ya manda User-Agent de navegador.

## Gemini (AI Studio, nivel gratuito)

- Clave conectada y verificada 2026-11-07. Conector `custom.gemini`.
- Modelo que funciona: `gemini-3-flash-preview`. Ojo: gemini-2.5-flash ya
  no está disponible para usuarios nuevos (404).
- Solo texto: no genera video, no tiene navegador ni GitHub.

## OpenAI

- Clave conectada y válida, pero la cuenta NO tiene créditos
  (429 insufficient_quota). Sin recargar saldo no sirve para generar.

## Grok (xAI)

- Dos claves rechazadas (400 Incorrect API key). La clave se crea en
  console.x.ai, empieza con "xai-", y la API cobra por uso y necesita
  saldo aparte de la suscripción del chat.

## Regla

Las claves guardadas en la bóveda NO se pueden leer de vuelta. Pecas las
usa por el conector, nunca las pega en ningún lado. Aquí solo van nombres
de variables y límites, nunca valores.
