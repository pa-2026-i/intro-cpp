# Tarea

---

## Instrucciones de entrega

La solución de los ejercicios debe presentarse en formato de diapositivas.

Las diapositivas deben:

* Incluir explicaciones claras y concisas de cada ejercicio.

* Incorporar recursos gráficos adecuados (diagramas, esquemas, fragmentos de código comentados) que faciliten la comprensión de los conceptos desarrollados.

* Presentar el código fuente de manera legible, destacando las partes relevantes para la explicación.

* Mantener una estructura ordenada y coherente entre las diferentes secciones.

---

## Ejercicio 1 — Inicialización y narrowing

Escriba un programa que:

1. Declare una variable `double` con valor `5.7`.
2. Intente asignarla a un `int` usando:

   * Inicialización clásica
   * Inicialización uniforme
3. Observe y explique qué ocurre en cada caso.

Explique:

* ¿Qué es una conversión *narrowing*?
* ¿Por qué `{}` es más segura?

---

## Ejercicio 2 — Variables no inicializadas

Escriba un programa que:

1. Declare una variable `int` sin inicializar.
2. Imprima su valor.
3. Luego corrija el programa inicializando correctamente la variable.

Explique:

* ¿Por qué el valor inicial es indefinido?
* ¿Cómo evitar este error sistemáticamente?

---

## Ejercicio 3 — Paso por valor

Implemente una función:

```cpp
void duplicar(int x);
```

La función debe multiplicar `x` por 2.

En `main`:

1. Declare una variable `int`.
2. Llame a la función.
3. Muestre que el valor original no cambia.

Explique por qué ocurre esto.

---

## Ejercicio 4 — Paso por referencia

Modifique el ejercicio anterior usando:

```cpp
void duplicar(int &x);
```

Ahora el valor original debe cambiar.

Explique la diferencia conceptual entre:

* Copia
* Referencia

---

## Ejercicio 5 — Alcance de variables

Escriba un programa que:

1. Declare una variable dentro de un bloque `{}`.
2. Intente usarla fuera del bloque.
3. Observe el error del compilador.

Explique:

* ¿Qué es el alcance (*scope*)?
* ¿Por qué es importante para la seguridad del programa?

---

## Ejercicio 6 — Uso incorrecto de punteros

Escriba un programa que:

1. Declare un puntero sin inicializar.
2. Intente usarlo.

Luego:

1. Corrija el programa inicializando el puntero con `nullptr`.
2. Agregue una verificación antes de usarlo.

Explique:

* ¿Qué significa comportamiento indefinido?
* ¿Por qué `nullptr` es importante?

---

## Ejercicio 7 — Memoria dinámica con `new` y `delete`

Escriba un programa que:

1. Reserve memoria dinámica para un entero.
2. Asigne un valor.
3. Libere correctamente la memoria.

Explique:

* ¿Qué ocurre si no se llama a `delete`?
* ¿Qué es una fuga de memoria?

---

## Ejercicio 8 — Uso de `std::unique_ptr`

Reescriba el ejercicio anterior usando:

```cpp
std::unique_ptr<int>
```

Explique:

* ¿Qué problema resuelve `unique_ptr`?
* ¿Por qué es preferible en C++ moderno?

---

## Ejercicio 9 — Clase simple

Defina una clase `Rectangulo` con:

* Atributos: `base`, `altura`
* Método: `area()`

En `main`:

1. Cree un objeto.
2. Calcule el área.
3. Muestre el resultado.

Use inicialización uniforme para los atributos.

---

## Ejercicio 10 — Función template

Implemente una función template:

```cpp
template <typename T>
T mayor(T a, T b);
```

Debe retornar el mayor de los dos valores.

Pruebe la función con:

* `int`
* `double`

Explique:

* ¿Qué ventaja tiene un template frente a escribir dos funciones distintas?

---
