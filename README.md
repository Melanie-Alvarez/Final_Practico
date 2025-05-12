# Final_Practico

# Churn Prediction for Interconnect

## 📖 Proyecto

**Objetivo**  
Predecir la probabilidad de que un cliente cancele (“churn”) su suscripción a los servicios de telecomunicaciones de Interconnect, con el fin de lanzar campañas de retención personalizadas.

**Contexto**  
- Interconnect ofrece Internet, telefonía y paquetes convergentes  
- Dispone de cuatro fuentes de datos unidas por `customerID`:  
  - `contract.csv`: información de contrato (fechas, método de pago, cargos)  
  - `personal.csv`: datos demográficos y segmentación  
  - `internet.csv`: detalles de servicios de Internet  
  - `phone.csv`: uso de líneas telefónicas  


---

## 🛠️ Pasos para el análisis

1. **Business Understanding**  
   - Definición del problema, hipótesis y KPIs (Churn Rate, AUC-ROC, Precision/Recall).

2. **Data Understanding**  
   - Exploración inicial:  
     - Histogramas y boxplots.  
     - Conteos de categorías (`Type`, `PaymentMethod`, `PaperlessBilling`).  
     - Correlación entre variables numéricas.  

3. **Data Preparation**  
   - **Funciones de limpieza y encoding** para cada tabla:  
     - `prepare_contract()`:  
       - Conversiones de fechas, cálculo de `tenure` (meses), flag `abandoned` (1/0), year/month, one-hot de `PaymentMethod` y `Type`.  
     - `prepare_personal()`: `gender`, `Partner`, `Dependents` → 0/1.  
     - `prepare_internet()`: servicios ON/OFF → 0/1; one-hot `InternetService`.  
     - `prepare_phone()`: `MultipleLines` → 0/1.  
   - Merge de las cuatro tablas en un solo DataFrame.

4. **Modeling**  
   - Split 70–30% estratificado, manejo de desbalance con SMOTE.  
   - Modelos entrenados y optimizados con **GridSearchCV** (roc_auc):  
     - **LogisticRegression**  
     - **HGBClassifier**  
     - **RandomForest**
   - Métricas en test: AUC-ROC, Precision, Recall, F1-score.  
   - Selección de la mejor configuración global y guardado de modelos en `models/`.

5. **Evaluation & Interpretability**  
   - Permutation Importance top-10 features.  

6. **Deployment / Próximos pasos**  
   - Serializar modelo y exponer un endpoint (FastAPI / SageMaker).  
   - Pipeline ETL diario para scoring y alertas.  
   - Monitoreo de drift y reentrenamiento periódico.  
   - Estrategia de descuentos segmentada por riesgo.

---

## 🚀 Cómo ejecutar

1. Clonar repositorio  
2. Crear entorno e instalar dependencias  
   ```bash
   pip install -r requirements.txt


