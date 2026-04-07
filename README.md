# Meal Prep Helper

SPA minimalista (React + Tailwind por CDN) para preparar comidas de Alan y Michelle rapido desde el telefono.

## Archivos importantes

- `mealPrep.json`: fuente de verdad para comidas, porciones y macros estimados.
- `index.html`: interfaz completa (SPA), calculadora de ejercicio y render de tarjetas.

## Como abrir la app

Opciones:

1. Abrir `index.html` directamente en el navegador (usa fallback embebido).
2. Recomendado: levantar un servidor local para que lea `mealPrep.json` en vivo.

Ejemplo rapido:

```bash
python3 -m http.server 8000
```

Luego abrir: `http://localhost:8000`

## Donde editar comidas

Todo se edita en `mealPrep.json`, dentro de `meal_options`.

Cada comida soporta:

- `id`: numero unico.
- `name`: nombre del platillo.
- `description`: descripcion corta.
- `ingredients`: lista de ingredientes (opcional, pero recomendado).
- `biohacking_note`: nota opcional (se muestra en un toggle colapsable).
- `macros_est`: macros estimados por perfil.
- `weigh_plan`: porciones reales para pesar por perfil.
- `alan_portion` / `michelle_portion`: texto libre opcional de referencia.
- `note`: nota adicional opcional.

## Estructura de una comida (ejemplo)

```json
{
  "id": 1,
  "name": "Carne de Res con Pasta o Papa",
  "description": "Carne molida 90/10 o Ribeye magro con pasta bien cocida o papas",
  "ingredients": ["Carne magra", "Pasta/Papa", "Salsa de tomate"],
  "biohacking_note": "Caminata de 10 min post-ingesta para control glucemico.",
  "macros_est": {
    "Alan": { "kcal": 740, "p": 58, "c": 80, "f": 22 },
    "Michelle": { "kcal": 580, "p": 56, "c": 52, "f": 20 }
  },
  "weigh_plan": {
    "Alan": [
      { "label": "Carne (cocida)", "amount": 200, "unit": "g", "equiv": { "p": 58 } },
      { "label": "Pasta/Papa (cocida)", "amount": 350, "unit": "g", "equiv": { "c": 80 } }
    ],
    "Michelle": [
      { "label": "Carne (cocida)", "amount": 193, "unit": "g", "equiv": { "p": 56 } },
      { "label": "Pasta/Papa (cocida)", "amount": 230, "unit": "g", "equiv": { "c": 52 } }
    ]
  }
}
```

## Como agregar una comida nueva

1. Abrir `mealPrep.json`.
2. Ir a `meal_options`.
3. Duplicar un bloque existente.
4. Cambiar `id` por uno nuevo (unico).
5. Completar `name`, `description`, `macros_est` y `weigh_plan`.
6. Guardar y recargar la app.

Notas:

- Si una comida solo aplica a un perfil, puedes incluir solo ese perfil en `macros_est` y `weigh_plan`.
- En `equiv` puedes poner uno o varios campos: `p`, `c`, `f`, `kcal`.

## Como editar targets diarios (arriba en Meal Prep)

En `mealPrep.json`:

- `couple.Alan.daily_macros`
- `couple.Michelle.daily_macros`

Campos:

- `kcal`
- `p`
- `c`
- `f`

## Calculadora de ejercicio (menu "Ejercicio")

Usa:

- Perfil (Alan o Michelle)
- Sets
- Reps por set
- RIR promedio
- Minutos de LISS
- MET promedio LISS
- Objetivo kcal/dia

La estimacion usa:

- Peso, estatura y SMM del perfil activo (`trainingProfiles` en `index.html`).
- Ajuste de intensidad en pesas por RIR y reps.
- Ajuste por composicion corporal para pesas y LISS.

## Donde editar parametros de calculo de ejercicio

En `index.html`:

- `trainingProfiles`: datos corporales base.
- `estimateStrengthKcal(...)`: formula de pesas.
- `estimateLissKcal(...)`: formula LISS basada en MET.
- `estimateLissMinutesForTarget(...)`: minutos estimados para objetivo kcal.

## Convenciones para editar sin romper la UI

- Mantener nombres de perfil consistentes: `"Alan"` y `"Michelle"`.
- No repetir `id` de comidas.
- Mantener `amount` numerico y `unit` como texto corto (`g`, `pza`, etc.).
- Si faltan datos de un perfil en una comida, la tarjeta de ese perfil puede no mostrarse.

## Troubleshooting

- Si no ves cambios en comidas, recarga el navegador.
- Si abriste con doble click y no carga JSON, usa servidor local.
- Si hay error de formato, validar `mealPrep.json` como JSON valido (comas, llaves, comillas).
