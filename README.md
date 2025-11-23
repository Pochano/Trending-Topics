### Alumno: Jose Miguel Valdivia Castillo
### Profesor: Erick Mauricio Gomez Nieto


## Descripción
Se busca implementar un **Segment Tree optimizado y persistente** para almacenar y consultar los $k$-*trending topics* (tópicos de tendencia) más relevantes en un rango de tiempo variable a partir de un conjunto de noticias.

---

### Características Principales

* **Pre-procesado de Texto Avanzado:** Incluye normalización, tokenización, eliminación de *stop words* (utilizando `Stop_Words_Ingles.txt`) y aplicación del **Porter Stemming** (implementado en `Porter_Stemming.h`/`.cpp`) para la identificación precisa de la raíz de las palabras clave.
* **Estructuras de Datos Personalizadas:** Uso de un **Hash Map Custom (`Gestor_Topicos`)** para la gestión eficiente de IDs y frecuencias globales de los tópicos, y un **Vector Dinámico Custom (`Vector`)** para manejar las raíces del Segment Tree.
* **Segment Tree Persistente:** La implementación del Segment Tree (`Segment_Tree.h`/`.cpp`) permite realizar consultas de rango de tiempo (`[RI_Consulta, RD_Consulta]`) con complejidad $O(k \log^2 N)$, donde cada inserción genera una nueva versión del árbol.

---

## Arquitectura

### Explicación de Clases y Archivos

| Clase/Estructura | Archivo(s) | Rol en el Proyecto |
| :--- | :--- | :--- |
| `Topico_Data` | `Segment_Tree.h` | Estructura base que almacena el `ID_Topico`, `Frecuencia_Global` y `Frecuencia_Local` en los nodos del Segment Tree. |
| `Entrada` | `HashMap.h` | Estructura interna del Hash Map, representando un slot para un tópico y su ID. |
| `Gestor_Topicos` | `HashMap.h`, `HashMap.cpp` | Implementación de la **Tabla Hash custom** para asignar IDs únicos a las raíces y controlar sus frecuencias globales. |
| `Vector` | `Vector.h`, `Vector.cpp` | Implementación de un **Vector Dinámico custom** que almacena las raíces (`Nodo_ST*`) del Segment Tree Persistente. |
| `Nodo_ST` | `Segment_Tree.h` | Estructura que representa un **nodo del Segment Tree**, conteniendo punteros a sus hijos y el *array* de los $k$-tópicos principales (`Top_k`). |
| `Segment_Tree` | `Segment_Tree.h`, `Segment_Tree.cpp` | Implementa el **Segment Tree Persistente** para la inserción de noticias (tiempos) y la consulta de los $k$-tópicos en un rango. |
| `Porter_Stemming` | `Porter_Stemming.h`, `Porter_Stemming.cpp` | Implementa el algoritmo de **Porter Stemming** (cinco pasos) para reducir las palabras a su raíz. |
| Funciones de Preprocesado | `Prepocesado.h` | Contiene funciones auxiliares para la lectura, normalización, tokenización, y filtrado de *stop words* del texto de las noticias. |
| Funciones de Menú | `Menus_Configuracion.h` | Gestión de la interfaz de consola, carga de la carpeta de noticias y control del flujo principal del programa. |

---

### Imagen Referencial Arquitectura

![](https://media.geeksforgeeks.org/wp-content/uploads/20250620181811171029/right_left_rotation_31.webp  )   


### Diagrama Conceptual del Flujo de Datos
El Segment Tree opera de forma persistente. Cada nueva noticia procesada se considera un "punto en el tiempo" y genera una nueva raíz del Segment Tree, reutilizando los nodos no afectados de la versión anterior.

**Árbol antes de insertar (Tiempo $t$):**
Una raíz ($R_t$) apunta a una estructura de árbol que resume los tópicos desde el inicio hasta el tiempo $t$.
[Conceptual representation of the tree's state at time 't']

**Árbol después de insertar (Tiempo $t+1$):**
Una nueva raíz ($R_{t+1}$) se crea, compartiendo la mayoría de los nodos del árbol antiguo ($R_t$) y creando una nueva ruta de nodos modificados que reflejan la inserción del nuevo tópico principal de la noticia.
[Conceptual representation of the tree's state at time 't+1' showing shared and new nodes]


## Dependencias

### Aclaraciones
El proyecto está configurado para:
* **GCC** (Compilador de C++) en la versión **15.2.0**

### C++
No requiere librerías adicionales aparte de la **Standard Template Library (STL)**. Necesita un compilador que soporte al menos **C++17**.
Se compila con: g++ -std=c++17 -o Archivo *.cpp


