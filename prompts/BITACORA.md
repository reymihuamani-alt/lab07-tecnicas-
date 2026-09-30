# Bitacora de tecnicas avanzadas

Laboratorio 07: Tecnicas Avanzadas de Prompting.
Herramienta de IA usada: [ESCRIBE AQUI CUAL USASTE]

## Ejercicio 2: Zero-shot, one-shot y few-shot

## Ejercicio 3: Chain of Thought

## Ejercicio 4: Role prompting

## Ejercicio 5: Descomposicion

## Ejercicio 6: Prompt estructurado y autocritica



| Tipo | Aciertos (de 5) | Formato de la respuesta | Todas con el mismo formato (Si/No) |
|------|-----------------|-------------------------|------------------------------------|
| Zero-shot | 5 | Formato libre: lista con etiquetas y a veces explicaciones | No |
| One-shot | 5 | DESCRIBIR: suele quedar entre libre y ordenado | Si |
| Few-shot | 5 | Una linea por comentario con el formato "texto -> etiqueta" | Si |

## Ejercicio 3: Chain of Thought

### Prompts usados

#### Directo

```text
Un producto cuesta S/ 120. La tienda aplica un descuento del 25 %
y luego suma el 18 % de IGV sobre el precio con descuento.
Un cliente compra 3 unidades. Cuanto paga en total?
Responde solo con el numero.
```

#### Paso a paso

```text
Un producto cuesta S/ 120. La tienda aplica un descuento del 25 %
y luego suma el 18 % de IGV sobre el precio con descuento.
Un cliente compra 3 unidades. Cuanto paga en total?
Resuelvelo paso a paso: muestra cada calculo y comprueba el resultado
antes de dar la respuesta final.
```

### Verificacion con calculadora

| Paso | Calculo | Resultado |
|------|---------|-----------|
| 1. Precio con descuento | 120 × 0,75 | 90 |
| 2. Precio con IGV | 90 × 1,18 | 106,20 |
| 3. Total por 3 unidades | 106,20 × 3 | 318,60 |


| Pedido | Respuesta de la IA | Muestra los pasos (Si/No) | Correcta (Si/No) |
|--------|--------------------|---------------------------|------------------|
| Directo | S/ 318.60 | No | Si |
| Paso a paso | Paso 1: Descuento del 25 % sobre una unidad Paso 2: IGV del 18 % sobre el precio con descuento Paso 3: Respuesta Final calculada.| Si | Si |

## Ejercicio 4: Role prompting

### Prompts usados

#### A. Sin rol

```text
Explica que es una variable en programacion.
```

#### B. Rol docente

```text
Actua como profesor de programacion que explica a estudiantes que nunca han programado. Explica que es una variable en programacion.
```

#### C. Rol senior

```text
Actua como desarrollador Java senior que explica a un companero de trabajo. Explica que es una variable en programacion.
```

### Resultados

| Version | Vocabulario (sencillo/tecnico) | Usa ejemplos o codigo | A quien le sirve mas |
|---------|--------------------------------|-----------------------|----------------------|
| A. Sin rol | Mixto: explicacion general, algo tecnico | Da un ejemplo corto o un poco de codigo | A cualquier persona, sin un publico definido |
| B. Rol docente | Sencillo, con palabras de la vida diaria | Usa comparaciones, como una caja con etiqueta | A quien nunca ha programado |
| C. Rol senior | Tecnico: tipo de dato, memoria, alcance | Incluye codigo Java | A un companero que ya programa |

## Ejercicio 5: Descomposicion

### Prompts usados

#### Pedido de una sola vez

```text
Crea un sistema de inventario para una tienda.
```

#### Pedido por pasos (mismo chat)

```text
Paso 1: Voy a crear un sistema de inventario para una tienda pequena en Java. Lista los 5 requisitos principales del sistema.
```

```text
Paso 2: Con esos requisitos, disena las clases necesarias. Para cada clase indica sus atributos con su tipo de dato.
```

```text
Paso 3: Escribe el codigo Java de la clase Producto con sus atributos, un constructor y los metodos get y set.
```

```text
Paso 4: Revisa el codigo de la clase Producto y propone 3 mejoras concretas.
```

### Resultados

- Paso 1:Voy a crear un sistema de inventario para una tienda pequena en Java. Lista los 5 requisitos principales del sistema.

- Paso 2: Con esos requisitos, disena las clases necesarias. Para cada clase indica sus atributos con su tipo de dato.

- Paso 3: Escribe el codigo Java de la clase Producto con sus atributos, un constructor y los metodos get y set.

- Paso 4: Revisa el codigo de la clase Producto y propone 3 mejoras concretas.

## Ejercicio 6: Prompt estructurado y autocritica

### Prompts usados

#### Prompt basico

```text
Dame casos de prueba para un login.
```

#### Prompt estructurado y mensaje de autocritica

```text
<rol>Actua como analista de pruebas de software.</rol>
<contexto>Login web con correo y contrasena. La cuenta se bloquea
despues de 3 intentos fallidos.</contexto>
<tarea>Piensa paso a paso que puede fallar y escribe 6 casos de prueba.</tarea>
<formato>Tabla con las columnas: ID, escenario, datos de entrada,
resultado esperado.</formato>

Revisa tu tabla: faltan casos limite como campos vacios, correo sin @
o contrasena con espacios? Agrega los que falten e indica cuales agregaste.
```

### Evaluacion de la tabla final

| Que revisar | Cumple (Si / No) |
|-------------|------------------|
| ¿Tiene las 4 columnas pedidas? |SI|
| ¿Incluye el bloqueo despues de 3 intentos? |Si |
| ¿Incluye casos con campos vacios? |Si |
| ¿Indica que casos agrego en la autocritica? | Si |
| ¿Hay algun caso repetido o que no tenga sentido? | No |
