# Práctica 2 (S33): Despliegue y Optimización de Modelo de Detección de Fraudes en AWS EC2

## Resultados Obtenidos
* **Mejores Hiperparámetros (`GridSearchCV`):** `{'criterion': 'entropy', 'max_depth': 8, 'n_estimators': 100}`
* **Recall — Clase Fraude (1):** **0.80 (80%)**
* **Métrica ROC-AUC Score:** **0.8925**

## Análisis e Interpretación de Resultados
* **Efectividad en la detección de fraudes:** El modelo demuestra una alta capacidad operativa para identificar transacciones ilícitas en un entorno desbalanceado (90% legítimas vs. 10% fraude). Al alcanzar un **Recall del 80%** en la clase `Fraude (1)`, el sistema logra interceptar 8 de cada 10 fraudes reales, minimizando el riesgo financiero por falsos negativos. Asimismo, el **ROC-AUC Score de ~0.89** confirma que el clasificador distingue con gran solvencia entre el comportamiento normal y el fraudulento a través de distintos umbrales de decisión.
* **Utilidad de serializar ambos archivos (`.pkl`):** Guardar tanto el modelo (`modelo_fraude_opt.pkl`) como el escalador (`scaler_fraude.pkl`) es indispensable para llevar el pipeline a producción (ya sea almacenándolos en un bucket de **AWS S3** o consumiéndolos desde una **API REST**). Cuando lleguen nuevas transacciones en tiempo real, los datos crudos deben transformarse exactamente con la misma media y desviación estándar aprendidas durante el entrenamiento (`scaler_fraude.pkl`) antes de pasar al modelo (`modelo_fraude_opt.pkl`); de lo contrario, las predicciones perderían precisión por inconsistencia de escala.
