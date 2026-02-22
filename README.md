# Guía breve de programación en C++

*Prof. Jose Francisco Ruiz Muñoz*<br>
*Programación Avanzada 2026-I*<br>
*Universidad Nacional de Colombia - Sede de La Paz*<br>

El lenguaje C++ extiende el lenguaje C incorporando abstracciones de alto nivel como programación orientada a objetos, genéricos (templates) y manejo más seguro de recursos. Es ampliamente utilizado en sistemas de alto rendimiento, videojuegos, simulación científica y software industrial.

---

## 1. El lenguaje C++ y el modelo multiparadigma

C++ es un lenguaje:

* Compilado
* Imperativo
* De tipado estático
* Multiparadigma (procedimental, orientado a objetos y genérico)

A diferencia de C, permite construir **abstracciones de alto nivel** sin perder control sobre la memoria.

---

## 2. Variables y tipos de datos

### 2.1 Definición de variables

```cpp
int x = 10;
double y{3.14};   // inicialización uniforme
```

C++ permite múltiples formas de inicialización:

* Inicialización clásica (`=`)
* Inicialización directa (`()`)
* Inicialización uniforme (`{}`)

---

### 2.2 Tipos básicos

| Tipo          | Descripción          |
| ------------- | -------------------- |
| `int`         | Entero               |
| `double`      | Punto flotante doble |
| `char`        | Carácter             |
| `bool`        | Booleano             |
| `std::string` | Cadena de texto      |

Ejemplo:

```cpp
#include <string>
std::string nombre = "Jose";
```
---

---

### 2.3 Formas de inicialización en C++

C++ permite varias formas de inicializar variables. Aunque todas asignan un valor inicial, **no son completamente equivalentes**.

---

#### 1. Inicialización clásica (`=`)

```cpp
int x = 10;
double y = 3.14;
```

Se llama *copy initialization*.
En tipos simples funciona como una asignación al momento de crear la variable.

Permite conversiones implícitas:

```cpp
int a = 3.7;   // permitido
```

Aquí `3.7` se convierte a `3`.
Se pierde la parte decimal sin que el compilador lo impida.

---

#### 2. Inicialización directa (`()`)

```cpp
int x(10);
double y(3.14);
```

Se llama *direct initialization*.
Invoca directamente el constructor (importante en clases).

También permite conversiones implícitas:

```cpp
int a(3.7);   // permitido
```

De nuevo, se pierde información.

---

#### 3. Inicialización uniforme (`{}`)

Introducida en C++11.

```cpp
int x{10};
double y{3.14};
```

Es la forma recomendada en C++ moderno porque **evita conversiones peligrosas**.

Ejemplo:

```cpp
int a{3.7};   // ERROR de compilación
```

Aquí el compilador detecta que:

* `3.7` es `double`
* `int` no puede representarlo exactamente
* La conversión perdería información

Y bloquea el programa.

---

### ¿Qué es narrowing?

Una conversión *narrowing* es aquella que:

* Reduce el rango o la precisión del valor
* Puede perder información

Ejemplos:

```cpp
double → int      // pierde decimales
long long → int   // puede perder rango
float → int       // pierde precisión
```

La inicialización con `{}` impide este tipo de conversiones.

---

### Recomendación práctica

En C++ moderno se recomienda preferir `{}` porque:

* Es más segura
* Evita errores silenciosos
* Hace explícitas las conversiones que podrían perder información

---

## 3. Estructuras de control

### 3.1 Selección

```cpp
if (x > y) {
    max = x;
} else {
    max = y;
}
```

Similar a C, pero con tipos booleanos explícitos (`bool`).

---

### 3.2 Iteración

```cpp
for (int i = 0; i < 5; ++i) {
    suma += i;
}
```

También existe el **range-based for**:

```cpp
int arr[] = {1,2,3};
for (int v : arr) {
    std::cout << v << std::endl;
}
```

---

## 4. Funciones

```cpp
int suma(int a, int b) {
    return a + b;
}
```

C++ permite:

**Sobrecarga de funciones** — varias funciones con el mismo nombre y distintos parámetros:

```cpp
int suma(int a, int b) { return a + b; }
double suma(double a, double b) { return a + b; }
// suma(1, 2) → 3  ;  suma(1.5, 2.5) → 4.0
```

**Parámetros por referencia** — el parámetro es un alias del argumento (se puede modificar el original):

```cpp
void incrementar(int &x) {
    x++;
}
// int n = 5; incrementar(n);  → n vale 6
```

**Valores por defecto** — los últimos parámetros pueden tener un valor si no se pasan:

```cpp
void saludar(const std::string& nombre, int veces = 1) {
    for (int i = 0; i < veces; i++)
        std::cout << "Hola, " << nombre << "\n";
}
// saludar("Ana");     → imprime una vez
// saludar("Ana", 3); → imprime tres veces
```

## 4.1 Paso por valor vs paso por referencia

En C++, los parámetros pueden pasarse:

### Por valor (se crea una copia)

```cpp
void incrementar(int x) {
    x++;
}
```

Aquí `x` es una copia.
La variable original no cambia.

---

### Por referencia (se modifica el original)

```cpp
void incrementar(int &x) {
    x++;
}
```

Aquí `x` es un alias del argumento original.

Diferencia conceptual:

* Valor → se copia
* Referencia → se modifica el objeto original

---


---

## 5. Programación orientada a objetos

### 5.1 Definición de clase

```cpp
class Persona {
public:
    std::string nombre;
    int edad;

    void saludar() {
        std::cout << "Hola\n";
    }
};
```

Uso:

```cpp
Persona p;
p.nombre = "Ana";
p.saludar();
```

---

## 6. Manejo de memoria

En C++ clásico:

```cpp
int* p = new int(5);
delete p;
```

En C++ moderno se recomienda usar **RAII** (Resource Acquisition Is Initialization) y punteros inteligentes:

- **RAII**: el recurso (memoria) se adquiere al crear el objeto y se libera automáticamente cuando el objeto sale de alcance. No hace falta llamar a `delete` a mano.
- **Punteros inteligentes**: `std::unique_ptr` es dueño exclusivo del objeto; cuando el puntero se destruye, libera la memoria.

```cpp
#include <memory>
std::unique_ptr<int> p = std::make_unique<int>(5);
// Al salir del bloque, p se destruye y la memoria se libera sola
```

**Salir del bloque** significa que la ejecución abandona el trozo de código entre llaves `{ }`. En ese momento las variables declaradas dentro se destruyen. Un bloque es todo lo que está entre una `{` y su `}` (el cuerpo de una función, un `if`, un `for`, o unas llaves puestas solo para limitar alcance). Ejemplo:

```cpp
{
    std::unique_ptr<int> p = std::make_unique<int>(5);
    // aquí p existe
}   // al llegar aquí, p se destruye y se libera la memoria
```

Así se evitan fugas de memoria (olvidar `delete`) y dobles liberaciones.

---

---

## 6.1 Uso básico de punteros seguros

En C++ moderno se recomienda:

```cpp
int* p = nullptr;
```

Antes de usar un puntero se debe verificar:

```cpp
if (p != nullptr) {
    // usar p
}
```

Un puntero no inicializado puede apuntar a cualquier dirección de memoria.

---


---

## 6.2 Alcance (scope) de variables

Las variables solo existen dentro del bloque donde se declaran.

```cpp
{
    int x = 10;
}
// aquí x ya no existe
```

Intentar usar una variable fuera de su alcance produce error.

---


## 7. Templates (Programación genérica)

```cpp
template <typename T>
T suma(T a, T b) {
    return a + b;
}
```

Uso con distintos tipos (el compilador genera la versión adecuada en cada caso):

```cpp
suma(3, 5);        // int → 8
suma(2.5, 1.5);    // double → 4.0
suma(1.0f, 2.0f); // float → 3.0f
```

Permite escribir código independiente del tipo.

---

## 8. Relación con bajo nivel

C++ mantiene compatibilidad con C:

* Uso de punteros
* Control explícito de memoria
* Traducción eficiente a código máquina

Sin embargo, incorpora abstracciones que el compilador optimiza sin costo adicional cuando se usan correctamente.

---

## 9. Errores comunes

### 1. No inicializar variables

```cpp
int x;
std::cout << x;   // valor indefinido
```

Las variables locales no se inicializan automáticamente.
Siempre deben inicializarse.

Solución: usar inicialización directa o uniforme.

---

### 2. Confundir paso por valor con paso por referencia

```cpp
void f(int x) {
    x = 100;
}
```

El valor original no cambia porque se creó una copia.

Si se desea modificar el argumento original, usar referencia:

```cpp
void f(int &x)
```

---

### 3. Usar punteros sin inicializar

```cpp
int* p;
*p = 10;   // comportamiento indefinido
```

Inicializar siempre:

```cpp
int* p = nullptr;
```

Y verificar antes de usar.

---

### 4. No liberar memoria al usar `new`

```cpp
int* p = new int(5);
// si no se hace delete, hay fuga de memoria
```

Mejor práctica en C++ moderno:

```cpp
std::unique_ptr<int> p = std::make_unique<int>(5);
```

Evita fugas automáticamente.

---

### 5. No usar `{}` cuando hay riesgo de narrowing

```cpp
int x = 3.7;   // pierde información
```

Preferir:

```cpp
int x{3};  // seguro
```

El compilador evita conversiones peligrosas.

---

---

## TAREA

La tarea de este tema se encuentra en el archivo [TAREA.md](TAREA.md).

---

**Este repositorio fue desarrollado con apoyo de inteligencia artificial. El contenido fue revisado, validado y editado cuidadosamente por el docente responsable.*
