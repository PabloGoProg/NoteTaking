## Variables del Modelo
La selección del variables utilizadas para este modelo sigue los siguientes criterios:

* Relevancia conceptual y relación con la teoría económica
* Pertinencia para el diseño e impacto de la ZELE
* Disponibilidad, calidad y consistencia de datos
* Comportamiento estadístico adecuado para estimación
### Variables Dependientes

1. **PIB real de Risaralda (proxy para PIB municipal)**: Se usa el PIB de Risaralda como una variable aproximada, pues el DANE no publica el PIB municipal de Pereira.
2. **Empleo formal / Tasa de desempleo (TD)**: El empleo formal y la TD reflejan los efectos del crecimiento económico sobre el mercado laboral. Con un aumento económico en el territorio, se debería espera un cambio inversamente proporcional en estás variables.
3. **Tejido empresarial (total de empresas registradas en Pereira)**: El número de empresas activas es un indicador clave para evaluar el dinamismo económico territorial.

### Variables Explicativas Principales (Independientes)

1. **Exportaciones totales (departamentales o municipales según disponibilidad)**
2. **Importaciones totales**
3. **Balanza comercial (export – import)**
4. **Inversión empresarial (capital constituido + reformas)**
5. **Tejido empresarial sectorial**
6. **Remesas recibidas en Risaralda**
7. **Indicadores de competitividad (IDC o similares)**
8. **Población total**

### Variables de Control del Modelo (Constantes)

1. **Población total (Risaralda o Pereira)**
2. **Índice de pobreza multidimensional (IPM)**
3. **Inflación o variación del IPC**
4. **Tasa de participación laboral**

---
## Diseño del Modelo

## 1. Ecuaciones Formales

**Metodología**: Regresión Lineal Multiple estimada por Mínimos Cuadrados Ordinarios (MCO).

El diseño del modelo contempla dos ecuaciones principales y una ecuación secundaria opcional, dependiendo del comportamiento de las series y de la correlación entre variables.

### Ecuación 1: Determinantes del Crecimiento Económico (PIB)

El primer modelo busca explicar cómo los factores lísticos, empresariales y de competitividad han influido históricamente en el desempeño económico de Risaralda y, por ende, de Pereira.

$$
\Delta \ln(PIB_t) = \alpha_0 
+ \beta_1 \Delta \ln(EXP_t) 
+ \beta_2 \Delta \ln(INV_t) 
+ \beta_3 \Delta \ln(EMP_t) 
+ \beta_4 \Delta \ln(REM_t) 
+ \beta_5 IDC_t 
+ \beta_6 \Delta \ln(POB_t) 
+ \varepsilon_t
$$
Donde:

- $\Delta \ln(PIB_t)$ Es la taza del crecimiento real del PIB de Risaralda.
- $\Delta \ln(EXP_t)$ Es la taza de crecimiento de las exportaciones.
- $\Delta \ln(INV_t)$ Es la taza de crecimiento de la inversión empresarial.
- $\Delta \ln(EMP_t)$ Es la taza de crecimiento del tejido empresarial.
- $IDC_t$ Es el indicador de competitividad territorial.
- $\Delta \ln(POB_t)$ Es la taza de crecimiento poblacional.
- $\varepsilon_t$ Es el termino de error aleatorio.

### Ecuación 2: Determinantes del Empleo Formal / Tasa de Desempleo

El segundo modelo se orienta a evaluar cómo el crecimiento económico y la dinámica empresarial repercuten en el mercado laboral local.

$$
TD_t = \gamma_0 
+ \gamma_1 \Delta \ln(PIB_t) 
+ \gamma_2 \Delta \ln(EMP_t) 
+ \gamma_3 \Delta \ln(INV_t) 
+ \gamma_4 IPM_t 
+ \gamma_5 IDC_t 
+ \mu_t
$$

Donde:

* $TD_t$ Es la taza de Desempleo de Pereira.
* $\Delta \ln(PIB_t)$ Es la taza del crecimiento económico (PIB).
* $\Delta \ln(EMP_t)$ Es la taza del crecimiento del tejido empresarial.
* $\Delta \ln(INV_t)$ Es la taza de crecimiento de la inversión empresarial.
* $IPM_t$ Es el índice de pobreza multidimensional.
* $IDC_t$ Es el indicador de competitividad territorial.
* $\mu_t$ Es el error aleatorio.

### Ecuación 3: Determinantes del Crecimiento Empresarial

Este modelo busca explicar como el crecimiento económico y las variables económico logísticas afectan el crecimiento empresarial (Nuevas Empresas).

$$
\Delta \ln(EMP_t) = \delta_0 
+ \delta_1 \Delta \ln(INV_t) 
+ \delta_2 \Delta \ln(EXP_t) 
+ \delta_3 IDC_t 
+ \delta_4 \Delta \ln(PIB_t) 
+ \eta_t
$$


