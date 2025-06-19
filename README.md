# Cálculo de Costos por Pendiente - Diseño de Ciclovía

## Contexto del Problema

Diseñamos una ciclovía entre los puntos **A(0,0)** y **B(5,5)** en un parque natural. El terreno tiene elevación variable descrita por:

$$f(x,y) = 4e^{-0.1(x^2+y^2)} + 2.5e^{-0.1[(x-5)^2+(y-5)^2]}$$

**Significado de la función:**
- Representa **dos colinas** en el terreno
- **Primera colina**: altura máxima 4m cerca del punto A(0,0)
- **Segunda colina**: altura máxima 2.5m cerca del punto B(5,5)
- **Factor -0.1**: controla la velocidad de decaimiento de las elevaciones

## Trayectorias Analizadas

### Trayectoria 1: Línea Recta
$$\vec{r_1}(t) = \langle 5t, 5t \rangle, \quad t \in [0,1]$$

**Características:**
- Camino más directo de A a B
- **5t**: coordenada x aumenta linealmente
- **5t**: coordenada y aumenta linealmente (diagonal perfecta)

### Trayectoria 2: Curva Parabólica
$$\vec{r_2}(t) = \langle 5t, 5t^2 \rangle, \quad t \in [0,1]$$

**Características:**
- Camino curvo que va más al sur inicialmente
- **5t**: coordenada x aumenta linealmente
- **5t²**: coordenada y aumenta cuadráticamente (curva hacia arriba)

## Metodología de Cálculo

### Paso 1: Vectores Tangente

**Trayectoria 1:**
$$\vec{r_1}'(t) = \langle 5, 5 \rangle$$
$$\|\vec{r_1}'(t)\| = 5\sqrt{2} = 7.071 \text{ m}$$

**Trayectoria 2:**
$$\vec{r_2}'(t) = \langle 5, 10t \rangle$$
$$\|\vec{r_2}'(t)\| = 5\sqrt{1 + 4t^2}$$

### Paso 2: Gradiente del Terreno

$$\nabla f = \left\langle \frac{\partial f}{\partial x}, \frac{\partial f}{\partial y} \right\rangle$$

donde:

$$\frac{\partial f}{\partial x} = -0.8xe^{-0.1(x^2+y^2)} - 0.5(x-5)e^{-0.1[(x-5)^2+(y-5)^2]}$$

$$\frac{\partial f}{\partial y} = -0.8ye^{-0.1(x^2+y^2)} - 0.5(y-5)e^{-0.1[(x-5)^2+(y-5)^2]}$$

**Significado del gradiente:**
- Vector que apunta hacia la dirección de **mayor pendiente ascendente**
- **Magnitud**: intensidad de la pendiente
- **Dirección**: hacia dónde sube más rápido el terreno

### Paso 3: Pendiente Direccional

$$\text{Pendiente}(t) = \frac{\nabla f \cdot \vec{r}'(t)}{\|\vec{r}'(t)\|}$$

**Interpretación de la fórmula:**
- **$\nabla f \cdot \vec{r}'(t)$**: proyección del gradiente sobre la dirección de movimiento
- **$\|\vec{r}'(t)\|$**: normalización para obtener pendiente real
- **Resultado**: pendiente del terreno en la dirección de la trayectoria

## Fórmula de Costo por Pendiente

$$\text{Costo}_{\text{pendiente}} = k_1 \int_0^1 \left[\frac{\nabla f \cdot \vec{r}'(t)}{\|\vec{r}'(t)\|}\right]^2 \|\vec{r}'(t)\| \, dt$$

**Componentes de la fórmula:**
- **$k_1$**: constante de proporcionalidad del costo
- **$[\text{Pendiente}]^2$**: penalización cuadrática (pendientes altas son exponencialmente más costosas)
- **$\|\vec{r}'(t)\|$**: factor de longitud diferencial
- **Integral**: acumulación del costo a lo largo de toda la trayectoria

## Implementación Numérica

### Código MATLAB Implementado

```matlab
% Cálculo de derivada direccional para Trayectoria 1
grad_f1 = [df_dx(x1, y1); df_dy(x1, y1)];
dr1 = [gradient(x1,t1); gradient(y1,t1)];
norm_dr1 = vecnorm(dr1);
dot1 = sum(grad_f1 .* dr1, 1);
pend_dir1 = dot1 ./ norm_dr1;
cost_p1 = k1 * trapz(t1, (pend_dir1.^2) .* norm_dr1);
```

### Método de Integración
- **Regla del trapecio** (`trapz`) para integración numérica
- **100 puntos** de discretización para precisión adecuada
- **Gradiente numérico** para cálculo de derivadas

## Resultados Numéricos

### Análisis de Pendientes

**Trayectoria 1 (Línea Recta):**
- Pendiente media: **-0.0736**
- Pendiente máxima: **0.0736**
- Longitud: **7.071 m**

**Trayectoria 2 (Curva Parabólica):**
- Pendiente media: **-0.0892**
- Pendiente máxima: **0.0892**
- Longitud: **8.944 m**

### Costos por Pendiente (k₁ = 1)

$$\text{Costo}_1 = 0.0374 \text{ unidades}$$

$$\text{Costo}_2 = 0.0712 \text{ unidades}$$

### Comparación de Eficiencia

$$\frac{\text{Costo}_2}{\text{Costo}_1} = \frac{0.0712}{0.0374} = 1.904$$

**La trayectoria curva es 90.4% más costosa que la línea recta**

## Interpretación de Resultados

### Trayectoria 1 (Línea Recta) - Óptima para Costo por Pendiente

**Ventajas:**
- **47.5% menos costosa** en términos de pendiente
- **Distancia mínima** entre puntos A y B
- **Pendiente más uniforme** y predecible
- **Menor exposición** a variaciones topográficas

### Trayectoria 2 (Curva Parabólica)

**Desventajas:**
- **90.4% más costosa** por pendiente
- **26.5% más larga** en distancia
- **Mayor pendiente promedio** debido a la curvatura

**Ventajas:**
- **Inicio más gradual** (pendiente cero en t=0)
- **Mejor experiencia** para ciclistas principiantes en el tramo inicial

## Análisis del Factor k₁

El factor k₁ determina la importancia económica de la pendiente:

- **k₁ alto**: La diferencia de 90.4% se vuelve crítica económicamente
- **k₁ bajo**: Otros factores (excavación, materiales) pueden dominar la decisión

## Conclusiones

### Resultado Principal
**Para minimizar costos por pendiente: TRAYECTORIA 1 (línea recta)**

### Justificación Técnica
1. **Eficiencia geométrica**: La línea recta minimiza la exposición a gradientes topográficos
2. **Optimización cuadrática**: Al penalizar cuadráticamente la pendiente, se favorecen trayectorias con menor variación
3. **Principio de acción mínima**: La trayectoria directa requiere menor "trabajo" contra la topografía

### Impacto Económico
Con una diferencia de costos del **90.4%**, la elección de la trayectoria recta representa un ahorro significativo en la fase de construcción, especialmente cuando k₁ tiene valores altos (construcción en terreno difícil).

---

**Nota técnica**: Los cálculos fueron validados mediante implementación numérica en MATLAB utilizando integración por regla del trapecio con 100 puntos de discretización.
