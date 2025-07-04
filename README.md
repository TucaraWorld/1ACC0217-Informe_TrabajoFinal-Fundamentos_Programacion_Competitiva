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

---





## 📚 Contenido

- [Introducción](#introducción)
- [Objetivo del estudiante](#objetivo-del-estudiante)
- [Plan de actividades](#plan-de-actividades)
- [Desarrollo](#desarrollo)
  - [Ejercicio con Map](#ejercicio-con-map)
  - [Ejercicio con KMP](#ejercicio-con-kmp)
  - [Ejercicio con Segment Tree](#ejercicio-con-segment-tree)
  - [Ejercicio con Trie](#ejercicio-con-trie)
  - [Ejercicio con Programación Dinámica](#ejercicio-con-programación-dinámica)
- [Conclusiones](#conclusiones)
- [Bibliografía](#bibliografía)

---

## 🧩 Introducción

_Contexto, objetivo, métodos y conclusiones generales..._

---

## 🎯 Objetivo del estudiante

_Describa cómo ha logrado el objetivo de acuerdo con el student outcome de su carrera._

---

## 🛠️ Plan de actividades

_Descripción detallada de las actividades realizadas para la construcción de los algoritmos._

---

## 🧠 Desarrollo

### 🗺️ Ejercicio con Map

- **Tipo de algoritmo:** Estructura `map`
- **Plataforma:** LeetCode  
- **Enlace:** [maximum-sum-queries](https://leetcode.com/problems/maximum-sum-queries/submissions/1683370047/)

#### 🧾 Enunciado

Se te dan dos arreglos `nums1` y `nums2` y una lista de consultas `queries[i] = [xi, yi]`. Para cada consulta, encuentra el máximo `nums1[j] + nums2[j]` tal que `nums1[j] ≥ xi` y `nums2[j] ≥ yi`, o devuelve `-1` si no existe.

#### 💻 Código

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
        for (int i = 0; i < n; ++i)
            puntos.push_back({ nums1[i], nums2[i], nums1[i] + nums2[i] });

        vector<array<int, 3>> consultas;
        for (int i = 0; i < m; ++i)
            consultas.push_back({ queries[i][0], queries[i][1], i });

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
