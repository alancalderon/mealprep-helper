# Meal Prep Helper - Guia Rapida

## 1) Donde editar comidas

Editar siempre: `mealPrep.json`

- Lista de comidas: `meal_options`
- Porciones a pesar: `weigh_plan`
- Macros estimados por comida: `macros_est`

## 2) Editar una porcion (lo mas comun)

Ruta:

- `meal_options -> [tu comida] -> weigh_plan -> Alan o Michelle`

Ejemplo:

- `"amount": 200, "unit": "g"` = pesa 200g
- `"equiv": { "p": 58 }` = equivale aprox a 58g de proteina

## 3) Agregar una comida nueva

1. Duplica una comida existente en `meal_options`.
2. Cambia `id` por uno nuevo.
3. Actualiza:
   - `name`
   - `description`
   - `macros_est`
   - `weigh_plan`
4. Guarda y recarga la pagina.

## 4) Editar targets diarios (header de Meal Prep)

- `couple.Alan.daily_macros`
- `couple.Michelle.daily_macros`

Campos: `kcal`, `p`, `c`, `f`

## 5) Vista Ejercicio (si no cuadra)

Menu `Ejercicio`:

- Selecciona perfil
- Ajusta `sets`, `reps`, `RIR`, `minutos LISS`, `MET LISS`

## 6) Si no se reflejan cambios

- Recarga navegador.
- Si abriste con doble click, mejor usar servidor:

```bash
python3 -m http.server 8000
```

Abrir: `http://localhost:8000`
