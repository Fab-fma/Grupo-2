## 2. Desarrollo y aplicación de la solución 

---

# Análisis de Costos por Pendiente para Ciclovía

Este documento detalla el cálculo y la comparación de los costos de construcción asociados a la pendiente para dos trayectorias de ciclovía propuestas. El objetivo es encontrar la ruta que minimice los costos manteniendo una pendiente moderada, como se especifica en el proyecto.

## Conceptos Fundamentales

Para evaluar las trayectorias, nos basamos en tres componentes matemáticos clave: la función de elevación del terreno, el cálculo de la pendiente a lo largo de un camino y la función de costo asociada.

### 1. Superficie del Terreno

La elevación del parque está modelada por la siguiente función, donde `(x, y)` son las coordenadas en metros:

$$f(x,y)=4e^{-0.1(x^{2}+y^{2})}+2.5e^{-0.1[(x-5)^{2}+(y-5)^{2}]}$$

### 2. Cálculo de la Pendiente

La pendiente de la ciclovía en cualquier punto no es constante, ya que sigue la topografía del terreno. Se calcula usando la **derivada direccional**, que mide la tasa de cambio de la elevación en la dirección en que avanza el camino.

$$\text{Pendiente} = \frac{\nabla f \cdot \mathbf{r}'(t)}{\|\mathbf{r}'(t)\|}$$

Donde:
-   `$\nabla f$` es el **vector gradiente** de la superficie. Apunta en la dirección de la máxima inclinación en cualquier punto del terreno.
-   `$\mathbf{r}(t)$` es la **función vectorial** que describe la trayectoria de la ciclovía en el plano `(x, y)`.
-   `$\mathbf{r}'(t)$` es el **vector tangente** a la trayectoria. Indica la dirección del camino en el plano.
-   `$\|\mathbf{r}'(t)\|` es la **magnitud del vector tangente**, que representa la rapidez con la que se recorre la trayectoria.

### 3. Función de Costo por Pendiente

El costo de construcción no es lineal. Para penalizar tramos excesivamente inclinados, el costo es proporcional al **cuadrado de la pendiente**. Para obtener el costo total, integramos esta cantidad a lo largo de toda la trayectoria:

$$\text{Costo}_{\text{pendiente}} = k_{1} \int_{\text{trayectoria}} (\text{Pendiente})^2 ds = k_{1}\int_{0}^{1} \left( \frac{\nabla f \cdot \mathbf{r}'(t)}{\|\mathbf{r}'(t)\|} \right)^{2} \|\mathbf{r}'(t)\| dt$$

-   `$k_1$` es una **constante de proporcionalidad**. No representa un valor físico, sino que traduce el resultado numérico de la integral a unidades monetarias o de esfuerzo constructivo. Un valor de `$k_1$` más alto significa que el presupuesto es más sensible a las pendientes fuertes. En este análisis, mantendremos `$k_1$` como una constante para comparar las trayectorias de forma relativa.

> **Sugerencia de Gráfico:** En este punto, sería muy útil insertar una visualización 3D de la superficie `$f(x,y)$` junto con las dos trayectorias propuestas (`$\mathbf{r}_1(t)$` y `$\mathbf{r}_2(t)$`) para ofrecer un contexto visual claro del problema.

---

## Paso 1: Cálculo del Gradiente del Terreno

El primer paso para resolver las integrales de costo es obtener el gradiente de `$f(x,y)$`.

-   **Derivada parcial respecto a x:**
    $$
    \frac{\partial f}{\partial x} = -0.8x e^{-0.1(x^2+y^2)} - 0.5(x-5) e^{-0.1((x-5)^2+(y-5)^2)}
    $$

-   **Derivada parcial respecto a y:**
    $$
    \frac{\partial f}{\partial y} = -0.8y e^{-0.1(x^2+y^2)} - 0.5(y-5) e^{-0.1((x-5)^2+(y-5)^2)}
    $$

El vector gradiente $\nabla f(x,y) = \left\langle \frac{\partial f}{\partial x}, \frac{\partial f}{\partial y} \right\rangle$ se usará para evaluar la pendiente en ambas trayectorias.

---

## Análisis de Trayectorias

### Trayectoria 1: Línea Recta

Esta ruta es el camino más directo que conecta los puntos A(0,0) y B(5,5).

-   **Función Vectorial**: $\mathbf{r}_1(t) = \langle 5t, 5t \rangle$, con $t \in [0, 1]$.
-   **Vector Tangente**: $\mathbf{r}_1'(t) = \langle 5, 5 \rangle$.
-   **Magnitud**: $\|\mathbf{r}_1'(t)\| = \sqrt{5^2 + 5^2} = 5\sqrt{2}$.

#### Integral de Costo

Tras sustituir $x=5t$ y $y=5t$ en el gradiente y realizar el producto punto `$\nabla f \cdot \mathbf{r}_1'(t)$`, la integral de costo queda:

$$\text{Costo}_1 = k_1 \int_{0}^{1} \frac{(-40te^{-5t^2} - 25(t-1)e^{-5(t-1)^2})^2}{(5\sqrt{2})^2} (5\sqrt{2}) dt$$

Simplificando la expresión, obtenemos:

$$\text{Costo}_1 = \frac{k_1}{5\sqrt{2}} \int_{0}^{1} \left(-40te^{-5t^2} - 25(t-1)e^{-5(t-1)^2}\right)^2 dt$$

### Trayectoria 2: Curva Polinomial

Esta ruta sigue una trayectoria parabólica entre los puntos A y B.

-   **Función Vectorial**: $\mathbf{r}_2(t) = \langle 5t, 5t^2 \rangle$, con $t \in [0, 1]$.
-   **Vector Tangente**: $\mathbf{r}_2'(t) = \langle 5, 10t \rangle$.
-   **Magnitud**: $\|\mathbf{r}_2'(t)\| = \sqrt{5^2 + (10t)^2} = 5\sqrt{1 + 4t^2}$.

#### Integral de Costo

Sustituyendo $x=5t$ y $y=5t^2$ en las componentes del gradiente y realizando el producto punto `$\nabla f \cdot \mathbf{r}_2'(t)$`, la integral de costo es:

$$\text{Costo}_2 = k_1 \int_{0}^{1} \frac{\left( 5 \frac{\partial f}{\partial x}(5t, 5t^2) + 10t \frac{\partial f}{\partial y}(5t, 5t^2) \right)^2}{(5\sqrt{1+4t^2})^2} (5\sqrt{1+4t^2}) dt$$

Simplificando la expresión:

$$\text{Costo}_2 = \frac{k_1}{5} \int_{0}^{1} \frac{\left( 5 \frac{\partial f}{\partial x} + 10t \frac{\partial f}{\partial y} \right)^2}{\sqrt{1+4t^2}} dt$$

---

## Resultados y Conclusión

Las integrales resultantes no tienen una solución analítica sencilla y deben resolverse por métodos numéricos. El valor numérico de cada integral representa la "penalización total por pendiente" de cada ruta.

> **Sugerencia de Gráfico:** Para complementar la comparación, se podría insertar un gráfico 2D que muestre la `Pendiente` en función del parámetro `t` para ambas trayectorias. Este gráfico mostraría visualmente qué tramos de cada ruta son más empinados y por qué el costo de una es mayor que la otra.

Al evaluar numéricamente las integrales, obtenemos los siguientes costos:

### **Costo Trayectoria 1 (Recta):**

$$\text{Costo}_1 \approx k_1 \cdot (1.0538)$$

### **Costo Trayectoria 2 (Curva):**

$$\text{Costo}_2 \approx k_1 \cdot (13.9056)$$

### Conclusión Final

La comparación de los resultados numéricos es clara:

**La trayectoria de la línea recta (`Costo₁`) es significativamente más eficiente en términos de costo por pendiente que la trayectoria curva (`Costo₂`).**

El costo asociado a la pendiente para la ruta parabólica es más de 13 veces superior al de la ruta recta. Esto indica que, a pesar de que ambas rutas conectan los mismos puntos, la trayectoria curva atraviesa regiones del terreno con pendientes mucho más pronunciadas, lo que dispararía los costos de construcción bajo el modelo propuesto. Por lo tanto, desde la perspectiva de minimizar la penalización por pendiente, la trayectoria recta es la opción óptima.
