# 🚀 Telecom X - Parte 2: Predicción de Churn de Clientes

![GitHub](https://img.shields.io/badge/Python-3.8%2B-blue)
![GitHub](https://img.shields.io/badge/Licencia-MIT-green)

---

## 📌 Objetivo del Proyecto
**Predecir la cancelación de clientes (Churn)** mediante análisis de variables clave como:
🔹 Antigüedad (`tenure`)
🔹 Tipo de contrato
🔹 Métodos de pago
🔹 Servicios contratados

**KPI Principal**: Reducir la tasa de churn del 26.5% al 15% mediante estrategias basadas en datos.

---

## 📂 Estructura del Proyecto
````
├── data/
│ ├── raw/ # Datos originales (clientes_raw.csv)
│ └── processed/ # Datos procesados (clientes_clean.csv)
├── notebooks/
│ ├── 1_EDA_Churn.ipynb # Análisis exploratorio
│ └── 2_Modelado_Churn.ipynb # Modelos predictivos
├── outputs/
│ ├── figures/ # Gráficos guardados (.png)
│ └── reports/ # Informes en PDF
└── README.md # Este archivo
````
---

## 🔍 Proceso de Preparación de Datos

### 1. Clasificación de Variables
| Tipo          | Ejemplos                          | Tratamiento                 |
|---------------|-----------------------------------|-----------------------------|
| **Numéricas** | tenure, MonthlyCharges            | Estandarización (StandardScaler) |
| **Categóricas** | Contract, PaymentMethod         | One-Hot Encoding            |
| **Binarias**  | Churn, PaperlessBilling          | Mapeo (Yes=1, No=0)         |

### 2. Transformaciones Clave
```python
# Codificación de variables categóricas
df_encoded = pd.get_dummies(df, columns=['Contract', 'PaymentMethod'])

# Estandarización de numéricas
scaler = StandardScaler()
df[['tenure', 'MonthlyCharges']] = scaler.fit_transform(df[['tenure', 'MonthlyCharges']])
````
### 3. División Train-Test
````
X_train, X_test, y_train, y_test = train_test_split(
    X, y, 
    test_size=0.3, 
    stratify=y,
    random_state=42
)
````
Justificación: 30% para test permite evaluación robusta manteniendo datos suficientes para entrenamiento.

---

🤖 Modelización
Modelos Implementados
| Modelo          | Precisión                          | Recall (Churn)                 | Requiere Escalado
|---------------|-----------------------------------|-----------------------------|-----------------------------|
| **Regresión Logística** | 72%            | 74% |Sí|
| **Random Forest** | 79%	         | 65%           |No|

Elección Final: Random Forest por mejor balance accuracy-recall.

---
📌 Conclusiones

Factores críticos:

🔹 Contratos mensuales (45% impacto)

🔹 Antigüedad <12 meses (38%)

Recomendaciones:

🔹 Convertir 30% contratos mensuales a anuales

🔹 Programa de retención para clientes nuevos

---

## 🛠️ Cómo Ejecutar el Proyecto

### 📌 Requisitos Previos

🔹 Python 3.8+

🔹 Jupyter Notebook

🔹 Librerías listadas en `requirements.txt`

### Instalación

```bash
git clone https://github.com/tu_usuario/telecom-churn-analysis.git
cd telecom-churn-analysis
pip install -r requirements.txt
````
---

## 📬 Contacto

Cualquier duda o sugerencia, puedes escribirme a pedro.tamani@gmail.com
