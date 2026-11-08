# baterias-tokens (privado)

La batería de tokens: el cableado que alimenta de tokens al stack de
agente a costo cero. No genera tokens: los tokens vienen de los
proveedores gratuitos. Lo que guarda este repo es todo lo necesario para
conectar cualquier máquina a esas fuentes y rotar entre ellas cuando una
se agota.

## Las fuentes (verificado 2026-11-07/08)

| Fuente | Modelo | Costo | Límite medido |
|---|---|---|---|
| Groq (API gratuita) | openai/gpt-oss-120b, openai/gpt-oss-20b | $0 | 8.000 TPM; el prompt de dsh pesa ~4.600 por llamado, el segundo llamado da 429 |
| Gemini (AI Studio, gratis) | gemini-3-flash-preview | $0 | nivel gratuito |
| OpenAI | gpt-4o-mini y otros | clave válida, sin créditos | 429 insufficient_quota |
| Grok (xAI) | — | — | clave rechazada dos veces (400) |

## Rotación

Cuando una fuente se agota, se cambia a la siguiente sin parar el trabajo.
Es el patrón que Marco quiere replicar: rotación entre modelos gratuitos,
igual que Codex con varias sesiones paralelas del mismo modelo.

Orden: Groq (gpt-oss-120b) → Groq (gpt-oss-20b) → Gemini → esperar al
reinicio del límite.

## Qué hay aquí

- `puente-groq/` — el puente local: dsh apunta al puente sin clave y el
  puente reenvía a Groq con el mecanismo del conector.
- `dsh/` — configuración del proveedor de dsh (por el puente y directo).
- `proveedores.md` — registro de proveedores con sus límites medidos.

## Regla de seguridad

Nunca van claves en este repo, ni en privado. Las claves viven en la
bóveda y se usan por el conector. Aquí solo van referencias (nombres de
variables como `GROQ_API_KEY`), nunca valores.
