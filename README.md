# Meal Recommender – AI-Powered Personalized Nutrition


## 📌 Problem Statement

In recent years, the connection between **gut microbiome composition**, **dietary habits**, and **overall health** has gained significant attention. Personalized nutrition—especially meal planning based on gut health indicators and lifestyle factors—offers a promising path toward improving **metabolic**, **digestive**, and **inflammatory conditions**.

The goal of this project is to develop a **scalable machine learning model** that can predict **personalized meal plans** based on:
- Gut microbiome profile (e.g., Bacteroides, Firmicutes)
- Dietary intake (protein, fiber, carbohydrate, fat)
- Demographic features (age, gender, BMI)
- Food allergy data

The system is built using **PySpark and Spark MLlib**, optimized for **big data environments**, with interpretable visualizations and clinically relevant outcomes.


## 📂 Data Selection

**Source**: American Gut Project and lifestyle survey data

**Data Features**:
- **Microbiome Indicators**: Bacteroides, Firmicutes, Lactobacillus, etc.
- **Demographics**: Age, Gender, BMI
- **Nutrient Intake**: Protein, Fiber, Carbohydrates, Fat
- **Allergies**: Dairy, Gluten, Nuts
 
![image](https://github.com/user-attachments/assets/4d5e8469-7a10-4ccb-afb5-0b96bb4dd458)

![image](https://github.com/user-attachments/assets/edf7ba60-a764-4192-8f90-7c6ab51d5f8b)


## 📊 Exploratory Data Analysis (EDA)

- Most users consume **moderate levels** of protein and fiber.
- **Meal plan labels are imbalanced**, heavily skewed toward a few diets.
- Age and BMI trends vary across plans, suggesting feature relevance.

**Challenges Identified**:
- Significant **class imbalance** in target labels.
  
![image](https://github.com/user-attachments/assets/c8b78876-1a55-4137-9626-edcf5d0f5ac4)

![image](https://github.com/user-attachments/assets/b81fb764-2c04-4453-8384-c11eefd36e2b)

![image](https://github.com/user-attachments/assets/ff4b55a3-f7d1-409b-8408-ba589379d78b)


## 🧠 Model Selection

I considered several models that would generate approproate results. 
### 1. Logistic Regression
- Interpretable and fast
- Limited in handling non-linear relationships

### 2. Decision Tree
- Easy to interpret
- Prone to overfitting with class imbalance

### 4. Gradient Boosted Trees (GBT) + One-vs-Rest
- High potential for accuracy
- More resource intensive and complex to tune

Our dataset presented several real-world challenges:
Non-linear relationships between microbiome features and meal plan categories
Mixed data types (nutrient levels, demographics, categorical allergies)
Significant class imbalance across diet labels
Interactions that simpler models (like logistic regression) cannot capture
To address these issues, I chose Gradient Boosted Trees, a model that builds an ensemble of trees sequentially, with each new tree correcting the errors of the previous ones. This makes GBT particularly effective when:
Patterns are complex
Features interact
Data is messy or noisy
High accuracy is essential
These conditions aligned perfectly with our dataset.

## 🛠️ Data Preparation

- **Categorical Encoding**: Converted text labels like “High Protein” into numeric indices
- **Allergy Normalization**: Cleaned inconsistent allergy formats
- **Class Balancing**:
  - Method 1: Upsample minority classes
  - Method 2: Merge similar rare classes and resample


## 📌 Feature Selection

### Method 1: Correlation Matrix
- Assessed relationships between numeric variables

![image](https://github.com/user-attachments/assets/c5077e1a-6997-4b9c-8fd7-e244316d1545)

### Method 2
- Chi Square test to select the categorical features
- Correlation matrix to assess the independence of each numerical variable
  
![image](https://github.com/user-attachments/assets/b9bc7258-dab0-4acb-ab28-45ec127cb5f9)

## Gradient Boosted Trees (GBT) – Model Results
###Performance Overview
Delivered competitive accuracy, showing strong learning of complex interactions
Performed especially well on non-linear microbiome–nutrition relationships
Showed improved sensitivity to underrepresented diet categories compared to baseline models
Demonstrated strong F1 performance, indicating balanced prediction quality even in the presence of class imbalance
Reduced error on categories that were previously misclassified by Decision Trees
Highlighted feature interactions (e.g., fiber × Lactobacillus, BMI × fat intake) that simpler models could not capture
### Business Insights
GBT modeling reveals high-value predictive features, helping nutrition platforms understand why certain meal plans are recommended
Enables more fine-grained personalization, especially for users whose microbiome or diet patterns don’t fit common categories
Helps improve precision in recommendations, reducing misleading or overly generic diet suggestions
Can enhance premium wellness product offerings by supporting advanced personalization tiers
Provides model interpretability through feature importance for dietitians and nutrition scientists
### Real-Life Impact
Supports evidence-based nutritional planning, especially when microbiome data contains complex patterns
Improves recommendations for users with nuanced health profiles (e.g., borderline BMI, mixed allergy data, mild dysbiosis)
Helps reduce misaligned diet suggestions through more accurate classification
Strengthens proactive, preventive health interventions, such as fiber-rich diets for low-diversity microbiomes
Builds trust with end users by powering more accurate and clinically aligned diet recommendations
