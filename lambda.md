# Expresiones Lambda en C++

Las **expresiones lambda** en C++ permiten definir funciones anónimas de manera compacta y eficiente. Son útiles para operaciones simples y se pueden usar en algoritmos estándar, funciones de orden superior y más.

## Sintaxis básica

```cpp
[ captura ] ( parámetros ) -> tipo_de_retorno { cuerpo };
```

- `captura`: Variables externas que la lambda puede utilizar.
- `parámetros`: Argumentos de la función (opcional).
- `tipo_de_retorno`: Tipo de retorno explícito (opcional, generalmente inferido).
- `cuerpo`: Código que ejecuta la lambda.

## Ejemplos

### 1. **Lambda básica**

```cpp
#include <iostream>

int main() {
    auto saludo = []() { std::cout << "Hola, mundo!" << std::endl; };
    saludo(); // Llama a la lambda
    return 0;
}
```

### 2. **Lambda con parámetros**

```cpp
#include <iostream>

int main() {
    auto suma = [](int a, int b) { return a + b; };
    std::cout << "Suma: " << suma(3, 5) << std::endl;
    return 0;
}
```

### 3. **Captura de variables por valor**

```cpp
#include <iostream>

int main() {
    int x = 10, y = 20;
    auto sumaCaptura = [x, y]() { return x + y; };
    std::cout << "Suma con captura: " << sumaCaptura() << std::endl;
    return 0;
}
```

### 4. **Captura de variables por referencia**

```cpp
#include <iostream>

int main() {
    int contador = 0;
    auto incrementar = [&contador]() { contador++; };
    incrementar();
    incrementar();
    std::cout << "Contador: " << contador << std::endl; // Imprime 2
    return 0;
}
```

### 5. **Lambda con tipo de retorno explícito**

```cpp
#include <iostream>

int main() {
    auto dividir = [](double a, double b) -> double {
        if (b == 0) return 0.0;
        return a / b;
    };
    std::cout << "División: " << dividir(10, 2) << std::endl;
    return 0;
}
```

### 6. **Uso en `std::sort`**

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> numeros = {5, 2, 8, 1, 3};
    
    std::sort(numeros.begin(), numeros.end(), [](int a, int b) {
        return a > b; // Orden descendente
    });
    
    for (int n : numeros) {
        std::cout << n << " ";
    }
    return 0;
}
```

### 7. **Lambda almacenada en `std::function`**

```cpp
#include <iostream>
#include <functional>

int main() {
    std::function<int(int, int)> multiplicar = [](int a, int b) { return a * b; };
    std::cout << "Multiplicación: " << multiplicar(4, 3) << std::endl;
    return 0;
}
```

## Tipos de captura en lambdas

| Sintaxis       | Tipo de Captura | Modifica la variable original |
|---------------|---------------|-----------------------------|
| `[x]`        | Por valor     | ❌ No |
| `[&x]`       | Por referencia | ✅ Sí |
| `[=]`        | Todas por valor | ❌ No |
| `[&]`        | Todas por referencia | ✅ Sí |
| `[x, &y]`    | Mixta | ❌ No (`x`), ✅ Sí (`y`) |

## Conclusión

Las lambdas en C++ son herramientas poderosas para definir funciones en línea de manera concisa. Son especialmente útiles en algoritmos estándar, programación funcional y concurrencia. 

