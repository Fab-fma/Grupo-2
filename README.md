---

# Diseño de Ciclovía: Análisis de Costos de Pendiente

Este repositorio contiene un análisis para determinar la trayectoria de menor costo para una nueva ciclovía, considerando la pendiente del terreno.

## Contexto

En el diseño de una ciclovía, las pendientes son un factor crucial. Una pendiente excesiva puede aumentar el esfuerzo requerido por los ciclistas y, potencialmente, incrementar los costos de construcción o mantenimiento. Para evaluar esto, hemos utilizado una función de terreno $f(x, y)$ y un modelo de costo para dos trayectorias propuestas.

La función de terreno utilizada es:

$$f(x, y) = 4e^{-0.1(x^2+y^2)} + 2.5e^{-0.1[(x-5)^2+(y-5)^2]}$$

## Trayectorias en Estudio

Se evaluaron dos posibles trayectorias para la ciclovía:

1.  **Trayectoria 1 :**
    $$\mathbf{r}_1(t) = \langle 5t^3, 5t^3 \rangle, \quad t \in [0, 1]$$

2.  **Trayectoria 2 :**
    $$\mathbf{r}_2(t) = \langle 5t, 10t^3 - 15t^2 + 10t \rangle, \quad t \in [0, 1]$$

## Metodología del Costo de Pendiente

Para cada trayectoria, el costo asociado a la pendiente se calcula mediante una integral que considera la relación entre el gradiente de la función del terreno y el vector tangente de la trayectoria. La fórmula general utilizada es:

$$C_P = k_1 \int_{0}^{1} \left( \frac{\nabla f \cdot \mathbf{r}'(t)}{\|\mathbf{r}'(t)\|} \right)^2 \|\mathbf{r}'(t)\| dt$$

Esta fórmula puede simplificarse a:

$$C_P = k_1 \int_{0}^{1} \frac{(\nabla f \cdot \mathbf{r}'(t))^2}{\|\mathbf{r}'(t)\|} dt$$

Donde:
* $C_P$ es el costo de pendiente.
* $k_1$ es una constante de proporcionalidad.
* $\nabla f$ es el vector gradiente de la función de terreno $f(x, y)$.
* $\mathbf{r}'(t)$ es el vector tangente a la trayectoria en el punto $t$.
* $\|\mathbf{r}'(t)\|$ es la magnitud (norma) del vector tangente.

### Gradiente de la Función de Terreno $f(x, y)$

El gradiente de $f(x, y)$ es:

$$\nabla f(x, y) = \left\langle -0.8xe^{-0.1(x^2+y^2)} - 0.5(x-5)e^{-0.1[(x-5)^2+(y-5)^2]}, \quad -0.8ye^{-0.1(x^2+y^2)} - 0.5(y-5)e^{-0.1[(x-5)^2+(y-5)^2]} \right\rangle$$

### Integrales a Evaluar

Las integrales específicas para cada trayectoria son:

**Para la Trayectoria 1 (Curva Cúbica - Nueva):**

$$C_{P,1} = k_1 \int_{0}^{1} 30\sqrt{2}t^2 \left( -4t^3e^{-5t^6} - (2.5t^3-2.5)e^{-0.2(5t^3-5)^2} \right)^2 dt$$

**Para la Trayectoria 2 (Curva Polinomial - Nueva):**

$$C_{P,2} = k_1 \int_{0}^{1} \frac{\left[ 5 \left( -0.8x_2(t)e^{-0.1(x_2(t)^2+y_2(t)^2)} - 0.5(x_2(t)-5)e^{-0.1[(x_2(t)-5)^2+(y_2(t)-5)^2]} \right) + (30t^2 - 30t + 10) \left( -0.8y_2(t)e^{-0.1(x_2(t)^2+y_2(t)^2)} - 0.5(y_2(t)-5)e^{-0.1[(x_2(t)-5)^2+(y_2(t)-5)^2]} \right) \right]^2}{\sqrt{25 + (30t^2 - 30t + 10)^2}} dt$$
donde $x_2(t) = 5t$ y $y_2(t) = 10t^3 - 15t^2 + 10t$.

Estas integrales fueron evaluadas numéricamente utilizando un script de Python.

## Resultados de Costo

Los valores numéricos de las integrales obtenidas son:

* **Para la Trayectoria 1 (Curva Cúbica - Nueva):**
    $$C_{P,1} = k_1 \cdot 1.776496$$

* **Para la Trayectoria 2 (Curva Polinomial - Nueva):**
    $$C_{P,2} = k_1 \cdot 1.746158$$

## Conclusión

Al comparar los costos de pendiente calculados para ambas trayectorias:

* $C_{P,1}$ (Curva Cúbica) es aproximadamente $1.776 \cdot k_1$
* $C_{P,2}$ (Curva Polinomial) es aproximadamente $1.746 \cdot k_1$

Dado que $k_1$ es una constante positiva de proporcionalidad, la trayectoria con el menor valor numérico es la de menor costo.

Por lo tanto, la **Trayectoria 2 (Curva Polinomial - Nueva)** presenta un costo de pendiente ligeramente menor en comparación con la Trayectoria 1. Esto la convierte en la opción preferible desde la perspectiva del costo de pendiente para el diseño de la ciclovía.

---
