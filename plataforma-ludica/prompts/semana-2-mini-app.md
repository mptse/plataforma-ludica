# Prompts

## Mini App A
Haz una app web de control de gastos con FastAPI.

## Mini App B

```
## Rol
Actúa como desarrollador backend con experiencia en FastAPI, Jinja2 y pruebas con pytest.

## Objetivo
Construir la mini-aplicación web registro de gastos con estos requisitos:
- GET / muestra un formulario para registrar un gasto, la lista de gastos y el total por
categoría.
- POST /api/gastos recibe {"descripcion": "Almuerzo", "valor": 15000, "categoria": "comida"}
y responde con el código 201 y el gasto creado con su id.
Las categorías válidas son comida, transporte, estudio y otros. El valor debe ser mayor que
0 y la descripción debe tener entre 1 y 80 caracteres. Si algún dato no es válido, responde
con el código 422.
- GET /api/gastos devuelve la lista de gastos.
- GET /api/gastos/resumen devuelve {"total": número, "por_categoria": {...}} con las cuatro
categorías, aunque alguna tenga 0.

## Contexto
Lee AGENTS.md. El contrato de la API está en tests/test_aceptacion.py: las rutas, los nombres
de los campos y los códigos de estado deben coincidir con esas pruebas.

## Restricciones
- Usa solo las dependencias de requirements.txt.
- Define las rutas en app/main.py y la lógica en app/servicios.py, sin importar FastAPI en servicios.
- Guarda los datos en memoria, sin base de datos ni archivos.
- No modifiques tests/test_aceptacion.py.
- La página usa HTML, CSS y JavaScript sin librerías externas.

## Formato de salida
Antes de escribir código, muestra el plan con las rutas completas de los archivos que vas a
crear y espera mi aprobación. Al terminar, resume en una línea qué hace cada archivo.

## Ejemplo
POST /api/gastos con {"descripcion": "Almuerzo", "valor": 15000, "categoria": "comida"} responde
con el código 201 y devuelve:
{"id": 1, "descripcion": "Almuerzo", "valor": 15000, "categoria": "comida"}
GET /api/gastos/resumen devuelve:
{"total": 15000, "por_categoria": {"comida": 15000, "transporte": 0, "estudio": 0, "otros": 0}}

## Criterio de éxito
python -m pytest -v pasa todas las pruebas y ruff check . no reporta errores.
Si después de 3 intentos las pruebas no pasan, detente y explica el problema.
```

### Prompt de mejoras:

```
## Rol
Actúa como desarrollador backend con experiencia en FastAPI, Jinja2 y pruebas con pytest.

## Objetivo
Agregar a la aplicación de Registro de gastos la funcionalidad de eliminar gastos:
1. Crear el endpoint `DELETE /api/gastos/{id}` que elimine el gasto correspondiente y responda
con el código de estado 204 (sin contenido)[cite: 28]. Si el `id` no existe, debe responder con
código de estado 404.
2. Asegurar que `GET /api/gastos/resumen` y `GET /api/gastos` dejen de incluir y sumar el gasto
eliminado.
3. Actualizar la página principal (`app/templates/index.html`) para mostrar un botón de eliminar
junto a cada gasto que llame al endpoint y actualice tanto la lista como el resumen por categoría.
4. Crear el archivo `tests/test_mejora.py` con pruebas automáticas que verifiquen la eliminación
exitosa (código 204), la actualización del resumen y el error 404 al intentar eliminar un ID inexistente.

## Contexto
Lee `AGENTS.md`, `app/main.py`, `app/servicios.py`, `app/templates/index.html` y `tests/test_aceptacion.py`.

## Restricciones
- Usa solo las dependencias de `requirements.txt`.
- Mantén las rutas en `app/main.py` y la lógica en `app/servicios.py` (sin importar FastAPI en `servicios.py`).
- No modifiques ni borres `tests/test_aceptacion.py`.
- Usa HTML, CSS y JavaScript puro sin librerías externas.

## Formato de salida
Antes de escribir código, muestra el plan con las rutas completas de los archivos que vas a
modificar o crear (`app/main.py`, `app/servicios.py`, `app/templates/index.html` y
`tests/test_mejora.py`) y espera mi aprobación. Al terminar, resume en una línea qué hiciste
en cada archivo.

## Ejemplo
- `DELETE /api/gastos/1` (cuando el gasto 1 existe) responde con código 204 y cuerpo vacío.
- `DELETE /api/gastos/9999` responde con código 404.

## Criterio de éxito
Ejecutar `python -m pytest -v` pasa todas las pruebas (tanto `test_aceptacion.py` como `test_mejora.py`)
y `ruff check .` no reporta errores. Si después de 3 intentos las pruebas no pasan, detente y explica
el problema.
```
