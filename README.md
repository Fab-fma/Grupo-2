¡Claro, entiendo! El problema con el texto dentro de los bloques de ecuaciones LaTeX en Markdown de GitHub es que no siempre se renderiza bien o puede causar errores si no se usa el comando correcto de LaTeX para texto (`\text{...}`). Para mantenerlo simple y compatible, y dado que pediste evitar cosas "fancy", la mejor estrategia es sacar el texto de las ecuaciones y dejar solo la parte matemática pura, o usar una notación más simple.

Vamos a ajustar el `README.md` para representar el "Costo Pendiente" de una forma más concisa, sin texto dentro de las ecuaciones, para asegurar la máxima compatibilidad y evitar fallos.

Aquí tienes la versión revisada:

---

# Diseño de Ciclovía: Análisis de Costos de Pendiente

Este repositorio contiene un análisis para determinar la trayectoria de menor costo para una nueva ciclovía, considerando la pendiente del terreno.

## Contexto

En el diseño de una ciclovía, las pendientes son un factor crucial. Una pendiente excesiva puede aumentar el esfuerzo requerido por los ciclistas y, potencialmente, incrementar los costos de construcción o mantenimiento. Para evaluar esto, hemos utilizado una función de terreno $f(x, y)$ y un modelo de costo para dos trayectorias propuestas.

La función de terreno utilizada es:

$$f(x, y) = 4e^{-0.1(x^2+y^2)} + 2.5e^{-0.1[(x-5)^2+(y-5)^2]}$$

## Trayectorias en Estudio

Se evaluaron dos posibles trayectorias para la ciclovía:

1.  **Trayectoria 1 (Línea Recta):**
    $$\mathbf{r}_1(t) = \langle 5t, 5t \rangle, \quad t \in [0, 1]$$

2.  **Trayectoria 2 (Curva Polinomial):**
    $$\mathbf{r}_2(t) = \langle 5t, 5t^2 \rangle, \quad t \in [0, 1]$$

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

**Para la Trayectoria 1 (Línea Recta):**

$$C_{P,1} = k_1 \cdot 10\sqrt{2} \int_{0}^{1} \left( -4te^{-5t^2} - (2.5t-2.5)e^{-0.2(5t-5)^2} \right)^2 dt$$

**Para la Trayectoria 2 (Curva Polinomial):**

$$C_{P,2} = k_1 \int_{0}^{1} \frac{\left[ (-20t - 40t^3)e^{-2.5(t^2+t^4)} + (12.5t+12.5 - 25t^3)e^{-0.1[(5t-5)^2+(5t^2-5)^2]} \right]^2}{5\sqrt{1 + 4t^2}} dt$$

Estas integrales fueron evaluadas numéricamente.

## Resultados de Costo

Los valores numéricos de las integrales obtenidas (calculadas usando un script de Python con `scipy.integrate`) son:

* **Para la Trayectoria 1 (Línea Recta):**
    $$C_{P,1} = k_1 \cdot 1.776496$$

* **Para la Trayectoria 2 (Curva Polinomial):**
    $$C_{P,2} = k_1 \cdot 1.902757$$

## Conclusión

Al comparar los costos de pendiente calculados para ambas trayectorias:

* $C_{P,1}$ (Línea Recta) es aproximadamente $1.776 \cdot k_1$
* $C_{P,2}$ (Curva Polinomial) es aproximadamente $1.903 \cdot k_1$

Dado que $k_1$ es una constante positiva de proporcionalidad, la trayectoria con el menor valor numérico es la de menor costo.

Por lo tanto, la **Trayectoria 1 (Línea Recta)** presenta un costo de pendiente menor en comparación con la Trayectoria 2, lo que la convierte en la opción preferible desde la perspectiva del costo de pendiente para el diseño de la ciclovía.

---

### Cambios realizados:

* **Notación de Costo:** He reemplazado `\text{Costo}_{\text{pendiente}}` por $C_P$ para la notación general y $C_{P,1}$, $C_{P,2}$ para las trayectorias específicas dentro de las ecuaciones. Esto es más conciso y evita problemas con `\text` en algunos renderizadores.
* **Gradiente como vector:** Usé `\left\langle ... \right\rangle` para el gradiente para que se vea más claramente como un vector, aunque `(...)` también es común.
* **Espaciado:** Mantuve el buen espaciado entre las ecuaciones para asegurar una correcta visualización.

Con estos cambios, el `README.md` debería ser muy compatible con GitHub y presentarse de forma clara y profesional.
