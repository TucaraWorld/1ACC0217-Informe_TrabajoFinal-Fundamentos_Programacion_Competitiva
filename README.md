<p align="center">
  <img src="./assets/logo-upc.png" alt="Logo UPC" width="750"/>
</p>

<h2 align="center">INFORME DEL TRABAJO FINAL</h2>
<h2 align="center">(ABET)</h2>

<h3 align="center">CURSO DE FUNDAMENTOS DE PROGRAMACIÓN COMPETITIVA – CC217</h3>
<h4 align="center">Carrera de Ciencias de la Computación</h4>

<p align="center"><strong>Sección:</strong> 271</p>


<h4 align="center">Alumno:</h4>

<p align="center">
  • Felices Vallejos, Aaron Alvaro <br/>
  • Ibarra Cabrera, Camila Adriana <br/>
  • Rojas Sánchez, Patricia Lucía del Rosario
</p>

<br/>

<p align="center"><strong>Julio 2025</strong></p>
<p style="page-break-after: always;"></p>

---

<h2 align="center"> CONTENIDO</h2>

## 1. Introducción

### 1.1 Contexto, objetivo, métodos, conclusiones

---

## 2. Objetivo del estudiante

### 2.1 Cómo se logró el objetivo según el *student outcome*

---

## 3. Plan de actividades

### 3.1 Actividades para construir los algoritmos

---

## 4. Desarrollo

### 4.1 Ejercicios con estructura `map`

#### 4.1.1 Primer ejercicio  

- **Tipo de algoritmo:** Para la resolución de este ejercicio se utiliza la estructura `map`.  
- **Herramienta web:** El problema pertenece a la plataforma LeetCode
- **Enlace:**  
  https://leetcode.com/problems/maximum-sum-queries/submissions/1683370047/  
- **Enunciado:**  
  Se te dan dos arreglos de enteros indexados desde 0, `nums1` y `nums2`, cada uno de longitud `n`, y un arreglo 2D indexado desde 1 llamado `queries`, donde `queries[i] = [xi, yi]`.

  Para la *i-ésima* consulta, debes encontrar el valor máximo de `nums1[j] + nums2[j]` entre todos los índices `j` (donde `0 ≤ j < n`) que cumplan `nums1[j] ≥ xi` y `nums2[j] ≥ yi`, o devolver `-1` si no existe ningún `j` que cumpla esas condiciones.

  Debes retornar un arreglo `answer`, donde `answer[i]` es la respuesta a la *i-ésima* consulta.

- **Código:**

```cpp
#include <iostream>
#include <vector>
#include <array>
#include <map>
#include <algorithm>
using namespace std;

class Solution {
public:
    vector<int> maximumSumQueries(vector<int>& nums1, vector<int>& nums2, vector<vector<int>>& queries) {
        int n = nums1.size(), m = queries.size();

        vector<array<int, 3>> puntos;
        for (int i = 0; i < n; ++i) {
            puntos.push_back({ nums1[i], nums2[i], nums1[i] + nums2[i] });
        }

        vector<array<int, 3>> consultas;
        for (int i = 0; i < m; ++i) {
            consultas.push_back({ queries[i][0], queries[i][1], i });
        }

        sort(puntos.begin(), puntos.end(), greater<>());
        sort(consultas.begin(), consultas.end(), greater<>());

        map<int, int> mejores;
        vector<int> respuestas(m, -1);
        int pos = 0;

        for (auto& [qx, qy, idx] : consultas) {
            while (pos < n && puntos[pos][0] >= qx) {
                int y = puntos[pos][1];
                int suma = puntos[pos][2];

                auto it = mejores.lower_bound(y);
                if (it != mejores.end() && it->second >= suma) {
                    ++pos;
                    continue;
                }

                mejores[y] = suma;
                ++pos;
            }

            int mejor = -1;
            auto it = mejores.lower_bound(qy);
            while (it != mejores.end()) {
                mejor = max(mejor, it->second);
                ++it;
            }

            respuestas[idx] = mejor;
        }

        return respuestas;
    }
};
```
- **Ingreso y salida de los datos:**
  
  ![Ingreso y salida](./assets/input-output-map.png)
  - Para `[4, 1]`: el único punto válido es `(4,2)` → `4+2 = 6`  
  - Para `[1, 3]`: el mejor punto es `(1,9)` → `1+9 = 10`  
  - Para `[2, 5]`: el mejor punto es `(2,5)` → `2+5 = 7`  

  Cada resultado representa el mayor `x + y` que cumple las condiciones de la consulta.

- **Verificación del algoritmo y explicación:**

  ![Captura de ejecución](./assets/submission-map.png)
  
  El algoritmo recibe dos vectores (`nums1` y `nums2`) y una lista de consultas. Cada consulta busca el valor máximo de `nums1[j] + nums2[j]`, cumpliendo que `nums1[j] ≥ xi` y `nums2[j] ≥ yi`.

  Primero, se combinan los valores de entrada `(x, y, x+y)` en un solo vector de puntos y se ordenan de forma descendente. Las consultas también se ordenan por `x` para facilitar el procesamiento.

  Se utiliza un `map` ordenado para almacenar los mejores puntos (según `y`) que podrían responder futuras consultas. Por cada consulta, se insertan al mapa los puntos válidos y luego se busca, con `lower_bound`, el mejor `x + y` que cumpla con `y ≥ yi`.

  Finalmente, se guarda la mejor suma posible o `-1` si no hay ninguna válida, y se devuelve la lista de respuestas en el orden original de las consultas.

#### 4.1.2 Segundo ejercicio  

### 4.2 Ejercicios con algoritmo KMP

#### 4.2.1 Primer ejercicio  
#### 4.2.2 Segundo ejercicio  

### 4.3 Ejercicios con algoritmo Z

#### 4.3.1 Primer ejercicio  
#### 4.3.2 Segundo ejercicio  

### 4.4 Ejercicios con Segment Tree

#### 4.4.1 Primer ejercicio  
#### 4.4.2 Segundo ejercicio  

### 4.5 Ejercicios con Árbol Fenwick

#### 4.5.1 Primer ejercicio  
#### 4.5.2 Segundo ejercicio  

### 4.6 Ejercicios con Árboles Ternarios

#### 4.6.1 Primer ejercicio  
#### 4.6.2 Segundo ejercicio  

### 4.7 Ejercicios con Trie

#### 4.7.1 Primer ejercicio  
#### 4.7.2 Segundo ejercicio  

### 4.8 Ejercicios con Programación Dinámica

#### 4.8.1 Primer ejercicio  
#### 4.8.2 Segundo ejercicio  

---

## 5. Conclusiones

### 5.1 Enumere las conclusiones del trabajo final enfatizando su punto de vista en base al objetivo

---

## 6. Anexos

---

## 7. Bibliografía

