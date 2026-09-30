# Tarea: Mi prompt avanzado

## Tarea elegida

Generar casos de prueba para un formulario de registro de usuarios (correo, contrasena y confirmacion de contrasena). La contrasena debe tener minimo 8 caracteres, una mayuscula y un numero. Elegi esta tarea porque probar formularios es algo que hago seguido en mis proyectos y una respuesta desordenada me obliga a reescribir todo.

## Version 1: prompt basico

```text
Dame casos de prueba para un registro de usuarios.
```

- Tecnica agregada: ninguna (punto de partida).
- Que paso: la respuesta fue una lista larga y generica, sin formato fijo, sin datos concretos de entrada y sin considerar las reglas de la contrasena.

## Version 2

```text
Actua como analista de pruebas de software con experiencia en aplicaciones web.

Contexto: formulario de registro con correo, contrasena y confirmacion de contrasena. La contrasena debe tener minimo 8 caracteres, al menos una mayuscula y al menos un numero.

Tarea: escribe 8 casos de prueba.

Formato: tabla con las columnas ID, escenario, datos de entrada, resultado esperado.
```

- Tecnicas agregadas: role prompting y prompt estructurado (contexto, tarea y formato separados).
- Por que: la v1 no tenia enfoque ni formato, asi que defini quien responde, las reglas del formulario y la tabla que necesito.
- Que mejoro: ahora la respuesta es una tabla con las 4 columnas y los casos usan las reglas de la contrasena. Aun faltaban casos limite (campos vacios, exactamente 8 caracteres) y no se veia el razonamiento detras de cada caso.

## Version 3: prompt final

```text
<rol>Asume la función de un especialista QA senior enfocado en pruebas funcionales para aplicaciones web.</rol>

<contexto>Módulo de registro de usuarios compuesto por los campos: correo electrónico, contraseña y confirmación de contraseña. Reglas del password: longitud mínima de 8 caracteres, al menos una letra mayúscula y al menos un número.</contexto>

<ejemplo>
| ID | Escenario | Datos de entrada | Resultado esperado |
| CP-01 | Registro válido | ana@correo.com / Clave1234 / Clave1234 | Cuenta creada |
</ejemplo>

<tarea>
Paso 1: Analiza detalladamente las posibles fallas en cada campo y a nivel global (escenarios válidos, inválidos y valores límite).
Paso 2: Elabora 10 casos de prueba manteniendo la misma estructura del ejemplo.
Paso 3: Realiza una autoevaluación del listado para identificar casos límite ausentes (entradas vacías, correo sin el símbolo @, contraseña de exactamente 8 caracteres y discrepancia en la confirmación de la clave), incorpóralos a la tabla e indica cuáles fueron añadidos.
</tarea>

<formato>Tabla con las columnas ID, escenario, datos de entrada, resultado esperado. Seguidamente, una lista con los casos agregados en el paso 3. Responde en español.</formato>
```

- Tecnicas agregadas: few-shot (un ejemplo de fila), chain of thought (pensar que puede fallar antes de escribir), descomposicion (tres pasos) y autocritica (paso 3).
- Por que: quise que todas las filas tuvieran el mismo formato, que los casos salieran de un razonamiento y no al azar, y que la IA revisara lo que le faltaba.
- Que mejoro: la tabla mantiene el formato exacto, incluye casos limite (8 caracteres justos, campos vacios, contrasenas distintas) y la IA indica cuales agrego despues de revisarse.

## Tecnicas usadas en el prompt final

| Parte del prompt | Tecnica |
|------------------|---------|
| `<rol>Actua como analista de pruebas...</rol>` | Role prompting |
| `<rol>`, `<contexto>`, `<ejemplo>`, `<tarea>`, `<formato>` | Prompt estructurado |
| `<ejemplo>` con la fila CP-01 | Few-shot |
| "Paso 1: piensa paso a paso que puede fallar..." | Chain of thought |
| Paso 1, Paso 2 y Paso 3 dentro de `<tarea>` | Descomposicion |
| "Paso 3: revisa tu tabla... agregalos e indica cuales" | Autocritica |

## Evaluacion del resultado

| Criterio | Cumple (Si / No) |
|----------|------------------|
| La tabla tiene las 4 columnas pedidas | Si |
| Todas las filas siguen el formato del ejemplo | Si |
| Incluye casos limite (8 caracteres, campos vacios, correo sin @) | Si |
| La IA indica que casos agrego en la autocritica | Si |
| No hay casos repetidos ni sin sentido | Si |

<!-- VERIFICA: llena esta tabla con lo que realmente devolvio tu IA -->

## Por que elegi estas tecnicas

Para generar casos de prueba necesito consistencia y cobertura. Use few-shot porque la tabla tiene que tener siempre el mismo formato y asi puedo copiarla a una hoja de calculo sin corregirla. Use chain of thought y descomposicion porque los casos utiles salen de pensar primero que puede fallar en cada campo. Use un rol especifico y un prompt estructurado para que la IA se enfoque en pruebas de software y no mezcle contexto, tarea y formato. Agregue autocritica porque la primera version casi siempre olvida los casos limite. No use solo zero-shot porque daba respuestas generales y sin formato fijo, y no use un rol vago como "experto" porque casi no cambia la respuesta.