
# Understanding Machine Performance Through Correlation Analysis

## **Description**
This project analyzes machine performance data to uncover critical insights into the relationships between operational parameters in a manufacturing environment. By leveraging correlation analysis and visualizations, actionable recommendations are provided to optimize system performance and minimize downtime.

---

## **Table of Contents**
1. [Executive Summary](#executive-summary)
2. [Data Overview](#data-overview)
3. [Challenge Questions and Answers](#challenge-questions-and-answers)
4. [Key Findings from the Correlation Analysis](#key-findings-from-the-correlation-analysis)
5. [Actionable Recommendations](#actionable-recommendations)
6. [Code Queries](#code-queries)
7. [Conclusion](#conclusion)
8. [Acknowledgment](#acknowledgment)
9. [How to Use](#how-to-use)
10. [Technologies Used](#technologies-used)

---

## **Executive Summary**
This analysis explores key relationships between operational parameters in machine systems used in high-precision manufacturing. Through a correlation heatmap and scatter plots, we reveal critical insights such as:
- A positive correlation between Spindle Speed (RPM) and Cutting Force (kN).
- A negative correlation between Hydraulic Pressure and Cutting Force.
These findings support recommendations for adaptive control systems, refined hydraulic pressure management, and modular maintenance strategies to improve efficiency and reduce downtime.

---

## **Data Overview**
The dataset (`data/machine_downtime.csv`) contains operational data for machines over time. Key attributes include:
- **Date**: Date of the reading.
- **Machine_ID**: Unique identifier for each machine.
- **Assembly_Line_No**: Identifier for the assembly line.
- **Operational Metrics**: Includes pressures, temperatures, vibrations, torque, cutting force, and spindle speed.
- **Downtime**: Indicator of whether the machine experienced downtime on a given day.

### **Data Range**
- **First Reading**: 31st December 2021  
- **Last Reading**: 1st February 2022  

---

## **Challenge Questions and Answers**
1. **What is the first and last date readings were taken on?**
   - **First Date**: 31st December 2021  
   - **Last Date**: 1st February 2022  

2. **What is the average Torque?**
   - The average Torque recorded is **25.23 Nm**.  

3. **Which assembly line has the highest readings of machine downtime?**
   - **Shopfloor-L1** recorded the highest downtime events with **874 events**, indicating the need for prioritized maintenance.

---

## **Key Findings from the Correlation Analysis**
1. **Spindle Speed and Cutting Force**  
   - **Correlation**: Moderate positive correlation (0.23).  
   - **Insight**: Indicates potential for adaptive control systems to optimize cutting performance.

2. **Hydraulic Pressure and Cutting Force**  
   - **Correlation**: Negative correlation (-0.22).  
   - **Insight**: Fine-tuning hydraulic pressure can improve stability and tool life.

3. **Thermal Management Systems**  
   - **Correlation**: Weak correlations between temperature variables.  
   - **Insight**: Suggests effective thermal isolation, ensuring independent system performance.

4. **Vibration and System Dynamics**  
   - **Correlation**: Weak correlations with other variables.  
   - **Insight**: Indicates robust mechanical design and opportunities for predictive maintenance.

5. **Torque and Cutting Force**  
   - **Correlation**: Weak negative correlation (-0.18).  
   - **Insight**: Adaptive control could improve cutting precision.

6. **Pressure Systems**  
   - **Correlation**: Weak correlations between different pressure metrics.  
   - **Insight**: Subsystems are independent but could benefit from integrated control.

---

## **Actionable Recommendations**
1. **Implement Adaptive Control Systems**  
   Dynamically adjust spindle speed based on cutting force to enhance cutting performance.

2. **Refine Hydraulic Pressure Control**  
   Optimize hydraulic pressure to balance cutting force and reduce wear.

3. **Adopt a Modular Maintenance Approach**  
   Monitor and maintain subsystems (pressure, vibration, temperature) independently for better efficiency.

4. **Long-Term Monitoring with Machine Learning**  
   Use real-time monitoring and machine learning to predict system degradation and prevent failures.

---

## **Code Queries**

### **Load and Explore Data**
```python
import pandas as pd
import numpy as np

# Load the data
downtime = pd.read_csv('data/machine_downtime.csv')

# Explore the dataset
print(downtime.head())
print(downtime.info())
print(downtime.describe())

# Check date range
first_date = downtime['Date'].min()
last_date = downtime['Date'].max()
print(f"First Date: {first_date}")
print(f"Last Date: {last_date}")

# Calculate average torque
avg_torque = np.mean(downtime["Torque(Nm)"])
print(f"Average Torque: {avg_torque} Nm")

# Find the assembly line with the highest downtime
highest_downtime = downtime.groupby("Assembly_Line_No")["Downtime"].count()
print("Downtime by Assembly Line:")
print(highest_downtime)
```

---

### **Correlation Analysis**
```python
import seaborn as sns
import matplotlib.pyplot as plt

# Select only numeric columns for correlation calculation
numeric_downtime = downtime.select_dtypes(include='number')

# Calculate correlations
correlation_matrix = numeric_downtime.corr()

# Plot correlation heatmap
plt.figure(figsize=(10, 8))
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', fmt=".2f")
plt.title('Correlation Heatmap')
plt.show()
```
[Machine Correlation][screenshot/Machine Correlation.png]

![Machine Correlation](https://github.com/user-attachments/assets/9271d5cd-9781-49e7-8602-7d38a99f68ab)

---

### **Scatter Plot for Specific Variables**
```python
# Scatter plot of Cutting Force vs Spindle Speed
plt.figure(figsize=(8, 5))
plt.scatter(
    numeric_downtime['Cutting(KN)'], 
    numeric_downtime['Spindle_Speed(RPM)'], 
    color='blue', s=15
)
plt.xlabel('Cutting Force (kN)')
plt.ylabel('Spindle Speed (RPM)')
plt.title('Scatter Plot: Cutting Force vs Spindle Speed')
plt.show()
```

---

### **Weekly Revenue Analysis**
```python
# Group data by week and sales method to calculate weekly statistics
weekly_stats = downtime.groupby(['Date', 'Assembly_Line_No']).agg({
    'Torque(Nm)': ['mean', 'std', 'min', 'max'],
    'Cutting(KN)': ['mean', 'std', 'min', 'max']
}).reset_index()

print("Weekly Statistics by Method:")
print(weekly_stats)
```

---

## **Conclusion**
This analysis identified key correlations and provided recommendations to optimize manufacturing processes. The implementation of adaptive systems, modular maintenance, and real-time monitoring can significantly reduce downtime and enhance operational efficiency.

---

## **Acknowledgment**
This report was prepared by **Adewole Oyediran** to support innovation in industrial machine management. For inquiries, please contact me at **Bensha2019@outlook.com**.

---

## **How to Use**
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/machine-performance-analysis.git
   ```
2. Place the dataset (`machine_downtime.csv`) in the `data` directory.
3. Run the analysis using the provided Python scripts:
   - `correlation_analysis.py` for correlation heatmaps and key findings.
   - `scatter_plots.py` for visualizing relationships between variables.

---

## **Technologies Used**
- **Python Libraries**:  
  - `pandas` for data manipulation.  
  - `numpy` for numerical computations.  
  - `matplotlib` and `seaborn` for visualizations.
- **Dataset**: `machine_downtime.csv`.




[def]: screenshot/Machine%20Correlation.png
