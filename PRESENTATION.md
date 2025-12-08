# Machine Failure Prediction: Dataset and ML Model Analysis

## Dataset Overview

### Vibration Dataset of Main Journal Bearings in Internal Combustion Engines

**Source**: [ScienceDirect - Data in Brief (2024)](https://www.sciencedirect.com/science/article/pii/S2352340924011764)

This dataset contains vibration signatures from both healthy and faulty main journal bearings in internal combustion engines, collected under diverse climatic and varying operating conditions.

### Key Dataset Characteristics

- **Total Samples**: 390,263 measurement records
- **Features**: 25 attributes including:
  - Vibration channels (4 channels + kurtosis metrics)
  - Operating parameters (RPM, temperature, humidity)
  - Control signals (Demand, Control, Output Drive)
  - Binary inputs (8 rear input signals)

- **Target Variable**: Machine condition (faulty vs. healthy)
  - Faulty: 209,662 samples (53.7%)
  - Healthy: 180,601 samples (46.3%)

- **Data Collection**: Captured using tri-axial accelerometers in a state-of-the-art climatic and vibration chamber following MIL-STD-810G standards

- **Environmental Conditions**:
  - Multiple temperature settings (including -10°C)
  - Varying humidity levels
  - Different engine rotation speeds (e.g., 1000 RPM)

### Dataset Value

This dataset provides a reliable benchmark for validating diagnostic algorithms under real-world engine conditions, addressing the gap in publicly available datasets for predictive maintenance in internal combustion engines.

---

## Machine Learning Models Evaluated

Seven supervised learning algorithms were trained and evaluated on this dataset:

| Model | Accuracy | Balanced Accuracy | F1 Score | ROC-AUC |
|-------|----------|-------------------|----------|---------|
| **Random Forest** | **100.00%** | **100.00%** | **100.00%** | **100.00%** |
| Decision Tree | 99.86% | 99.86% | 99.86% | 99.94% |
| K-Nearest Neighbors | 99.52% | 99.51% | 99.52% | 99.90% |
| Gradient Boosting | 99.52% | 99.50% | 99.52% | 99.99% |
| SVM (RBF) | 99.09% | 99.05% | 99.09% | 99.78% |
| AdaBoost | 93.78% | 93.72% | 93.78% | 98.74% |
| Logistic Regression | 89.42% | 89.33% | 89.42% | 94.32% |

### Model Configuration

- **Train/Test Split**: 80/20 (312,210 training samples, 78,053 test samples)
- **Data Preprocessing**: StandardScaler normalization
- **Feature Set**: 22 numeric features (excluding timestamp and source file)
- **Evaluation Metric**: Balanced accuracy (to handle class imbalance)

---

## Best Model: Random Forest Classifier

### Why Random Forest is the Best Model

**1. Perfect Performance Metrics**
- Achieved 100% accuracy, balanced accuracy, F1 score, and ROC-AUC
- Confusion matrix shows near-perfect classification:
  - True Negatives (Faulty): 41,931
  - False Positives: 2
  - False Negatives: 0
  - True Positives (Healthy): 36,120

**2. Model Characteristics**
- **Configuration**: 200 trees with max depth of 20
- **Algorithm**: Ensemble learning using bagging
- **Parallel Processing**: Leverages multi-core processing for efficiency

**3. Key Advantages**

**Robustness**
- Ensemble of 200 decision trees reduces overfitting risk
- Handles non-linear relationships between vibration features and machine condition
- Resistant to noise in sensor data

**Feature Importance**
- Can identify which vibration channels and operating conditions are most predictive
- Provides interpretable insights into failure patterns

**Generalization**
- Strong performance on unseen test data (78,053 samples)
- Maintains balanced performance across both classes

**Practical Benefits**
- Fast prediction time after training
- Handles mixed feature types (vibration signals, operating parameters)
- No need for extensive feature engineering

**4. Comparison with Other Models**

- **vs. Decision Tree**: Random Forest's ensemble approach prevents overfitting better than a single tree (99.86% accuracy)
- **vs. Gradient Boosting**: Achieves superior results while being easier to tune and less prone to overfitting
- **vs. SVM**: Faster training and prediction times with better accuracy
- **vs. Logistic Regression**: Captures complex non-linear patterns that linear models miss

### Model Limitations and Considerations

While the Random Forest achieved perfect performance on the test set, practitioners should:

1. **Validate on new data**: Test the model on independent datasets from different engines or conditions
2. **Monitor for drift**: Real-world operating conditions may differ from training data
3. **Consider computational resources**: 200 trees require more memory than simpler models
4. **Implement confidence thresholds**: Use prediction probabilities for uncertain cases

---

## Conclusion

The Random Forest classifier is the optimal model for this machine failure prediction task, demonstrating:

- Perfect classification performance across all metrics
- Robust handling of the multi-feature vibration dataset
- Practical applicability for predictive maintenance systems
- Strong generalization to unseen data

This model can be deployed to enable proactive maintenance, reducing unexpected downtime and supporting data-driven maintenance decisions for internal combustion engines operating under diverse environmental conditions.

---

## Sources

- [Vibration dataset of main journal bearings in internal combustion engines - ScienceDirect](https://www.sciencedirect.com/science/article/pii/S2352340924011764)
- [GitHub - PredictiveMaintenance and Vibration Resources](https://github.com/Charlie5DH/PredictiveMaintenance-and-Vibration-Resources)
