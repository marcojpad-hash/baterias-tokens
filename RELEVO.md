# Relevo — cuando Pecas se queda sin tokens

Fecha: 2026-11-08.

## La idea

Si Pecas (Muse) se queda sin tokens, el trabajo no se para: queda a cargo
un modelo abierto gratuito, `openai/gpt-oss-120b` por Groq, corriendo en
GitHub Actions. Puede ser un modelo de lenguaje normal y regular: para
coordinar (leer el tablero, decir qué está atorado, abrir avisos) alcanza
y sobra. Si además hay un bot (dsh) disponible, también puede actuar,
pero el modelo de lenguaje es suficiente para el relevo.

## Cómo se activa

Pecas crea el archivo `RELEVO_ACTIVO` en el repo `agente-cero-costo`
cuando se le acaban los tokens. El workflow `relevo.yml` lo ve cada hora
y corre el orquestador. Cuando Pecas vuelve (reinicio de tokens), borra
el archivo y retoma el tablero.

## Qué hace el relevo

- Lee el tablero de CAPCOT (`ajustes_entre_modelos/DELEGACIONES.md`) y
  el protocolo.
- Escribe el reporte de qué está atorado, quién debe qué a quién y el
  siguiente paso de cada pendiente.
- Abre un aviso (issue con etiqueta `relevo`) si no hay uno abierto.

## Qué NO puede hacer

- Navegador ni YouTube Studio: no puede corregir Shorts ni revisar
  Analytics.
- Iniciar sesión como Marco ni crear cuentas.
- Crear repositorios (ni la app de Muse ni Actions pueden crearlos).
- Correr lo que solo vive en el box (el montaje oficial de Imaginantes,
  edge-tts).

## Cómo vuelve Pecas

Borra `RELEVO_ACTIVO`, lee el último reporte del relevo y retoma. El
relevo no borra nada ni reasigna trabajo: solo informa.
