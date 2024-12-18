# Amazon USA Data Financial Insights  Across All  States log-normalization
# Amazon Financial Dataset: R&D, Marketing, Campaigns, and Profit

# This file is invalid because it uses nbformat v5.8.0 and nbconvert v7.3.1. It works on my laptop, but I’m not sure why it isn’t working when uploaded to GitHub.

# You can try running the following command:

# Copy code
pip install --upgrade nbformat

```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import re
import datetime

import json
import os
import copy

import seaborn as sns
import os
print(os.getcwd())




file_path = r'........your path\Amazon_Company_Data_All_States.xlsx'
data = pd.read_excel(file_path)

```

```python
# Display the first few rows of the dataset
data.head()

# Applying Log Normalization
# Adding 1 to avoid log(0)

data['R&D Log'] = np.log(data['R&D Amount (in $)'] + 1)
data['Marketing Log'] = np.log(data['Marketing Amount (in $)'] + 1)
data['Profit Log'] = np.log(data['Profit (in $)'] + 1)


# Visualization: Original vs Log Normalized Data (R&D Amount)



plt.figure(figsize=(10, 5))
plt.plot(data['State'], data['R&D Amount (in $)'], label='R&D Amount (Original)', marker='o')
plt.plot(data['State'], data['R&D Log'], label='R&D Amount (Log Normalized)', marker='x')
plt.xticks(rotation=90)
plt.title('Original vs Log-Normalized R&D Amount')
plt.xlabel('State')
plt.ylabel('R&D Amount')
plt.legend()
plt.tight_layout()
plt.show()
```

![Screenshot 2024-12-18 214310](https://github.com/user-attachments/assets/5d80e1c9-11eb-4c1d-93c1-1e15603223e2)


#  Gaussian Distribution
# Plot Gaussian distribution for log-normalized R&D Amount
```python

plt.figure(figsize=(8, 5))
sns.histplot(data['R&D Log'], kde=True, bins=20, color='blue')
plt.title('Gaussian Distribution of Log-Normalized R&D Amount')
plt.xlabel('Log-Normalized R&D Amount')
plt.ylabel('Density')
plt.show()
```
![4593e505-3d99-4fc6-8c5a-15ad388915e1](https://github.com/user-attachments/assets/632e2060-c81d-4923-92dd-82a7853fcc7c)




#  Standard Normal Distribution (SND)
# Standardizing the log-normalized data for R&D Amount
```python

mean = data['R&D Log'].mean()
std = data['R&D Log'].std()
data['R&D Z-Score'] = (data['R&D Log'] - mean) / std


# Visualization: Standard Normal Distribution (Z-Scores)


plt.figure(figsize=(12, 6))
sns.histplot(data['R&D Z-Score'], kde=True, bins=30, color='purple', stat="density")
x = np.linspace(data['R&D Z-Score'].min(), data['R&D Z-Score'].max(), 1000)
y = 1 / (np.sqrt(2 * np.pi) * std) * np.exp(-0.5 * ((x - mean) ** 2))
plt.plot(x, y, color='red', label='Theoretical Normal Curve')
plt.title('Standard Normal Distribution of R&D Amount (Z-Scores)')
plt.xlabel('Z-Score')
plt.ylabel('Density')
plt.legend()
plt.show()
```

![97c8f004-cdf4-4c7a-a4ae-ca05dc10c462](https://github.com/user-attachments/assets/6d69be76-1a41-47e3-b33c-ab776e2a2f85)

```python
# Output processed data for verification
data[['State', 'R&D Amount (in $)', 'R&D Log', 'R&D Z-Score']].head()
```

![Screenshot 2024-12-18 215456](https://github.com/user-attachments/assets/490868ce-9186-4542-b31c-65360a0797f8)



## Description:
This dataset provides fictional yet insightful financial data of Amazon's business activities across all 50 states of the USA. It is specifically designed to help students, researchers, and practitioners perform various data analysis tasks such as log normalization, Gaussian distribution visualization, and financial performance comparisons.

Each row represents a state and contains the following columns:

- **R&D Amount (in $):** The investment made in research and development.
- **Marketing Amount (in $):** The expenditure on marketing activities.
- **Campaign Amount (in $):** The costs associated with promotional campaigns.
- **State:** The state in which the data is recorded.
- **Profit (in $):** The net profit generated from the state.

Additional features include log-normalized and Z-score transformations for advanced analysis.

---

## Use Cases:
This dataset is ideal for practicing:

1. **Log Transformation:** Normalize skewed data for better modeling and analysis.
2. **Statistical Analysis:** Explore relationships between financial investments and profit.
3. **Visualization:** Create compelling graphs such as Gaussian distributions and standard normal distributions.
4. **Machine Learning Projects:** Build regression models to predict profits based on R&D and marketing spend.

---

## File Information:
- **File Format:** Excel (.xlsx)
- **Number of Records:** 50 (one for each state of the USA)
- **Columns:** 5 primary financial columns and additional preprocessed columns for normalization and Z-scores.

---

## Important Note:
This dataset is **synthetically generated** and is not based on actual Amazon financial records. It is created solely for educational and practice purposes.

---

## Tags:
- Financial Analysis
- Data Visualization
- Machine Learning
- Statistical Analysis
- Educational Dataset

