# raku-cron

Disparador de cron para el pipeline de cTrader del proyecto RAKU. **Este repo
es público a propósito y no contiene ninguna lógica de la estrategia** — ni
parámetros, ni código del mecanismo, ni datos de operaciones.

GitHub degrada la prioridad de los workflows programados en repos privados
(corría cada 2-5h en vez de cada 15 min); un repo público no tiene ese límite.
La solución: separar dónde vive el *workflow* (aquí, público, vacío) de dónde
vive el *código real* (repo privado `raku-shadow-resolver`).

Cada corrida:
1. Clona `raku-shadow-resolver` (privado) usando un token con permiso de repo,
   guardado como secreto de este repo — nunca queda expuesto.
2. Corre todos los scripts desde ahí adentro.
3. Empuja los resultados de vuelta al repo privado y al panel.

Todo lo demás — mecanismo, parámetros, historial de señales — sigue viviendo
exclusivamente en el repo privado.
