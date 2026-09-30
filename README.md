# Phishing Website Detection

A beginner-friendly machine learning project that predicts whether a URL is phishing or legitimate.

## Project Overview

This project builds a binary classification model to detect phishing websites based on URL features. It demonstrates the complete machine learning pipeline from data loading to model evaluation and prediction.

## Problem Statement

Phishing websites are malicious sites that attempt to steal sensitive information by masquerading as legitimate websites. This project aims to automatically identify phishing URLs based on their structural characteristics.

**Goal:** Classify URLs as either:
- **0** = Legitimate
- **1** = Phishing

## Dataset

### Dataset Source
The dataset is a curated collection of legitimate and phishing URLs created for educational purposes.

### Dataset Statistics
- **Total Samples:** 188 URLs
- **Legitimate URLs:** 82 (43.6%)
- **Phishing URLs:** 106 (56.4%)
- **Format:** CSV with columns: `url`, `label`

### Dataset Format
```csv
url,label
https://www.google.com,0
http://secure-login-paypal.com,1
```

## Features

The following features are extracted from each URL:

1. **url_length** - Total length of the URL
2. **num_dots** - Number of dots (.) in the URL
3. **num_hyphens** - Number of hyphens (-) in the URL
4. **num_special_chars** - Number of special characters
5. **num_digits** - Number of digits in the URL
6. **has_https** - Binary indicator (1 if HTTPS, 0 if HTTP)
7. **has_ip_address** - Binary indicator (1 if IP address present)
8. **num_subdomains** - Number of subdomains in the URL
9. **has_suspicious_words** - Binary indicator (1 if suspicious words present)

### Feature Rationale
- **URL length:** Phishing URLs are often longer to hide malicious content
- **Dots and hyphens:** Excessive use can indicate subdomain manipulation
- **Special characters:** Unusual characters may indicate obfuscation
- **Digits:** Numeric patterns can indicate IP addresses or encoded content
- **HTTPS:** Legitimate sites typically use HTTPS
- **IP address:** Direct IP addresses are suspicious
- **Subdomains:** Excessive subdomains can be used for deception
- **Suspicious words:** Words like "login", "verify", "secure" are common in phishing

## Machine Learning Models

### Models Used
1. **Logistic Regression**
   - Linear classification algorithm
   - Interpretable coefficients
   - Good baseline model

2. **Random Forest**
   - Ensemble of decision trees
   - Handles non-linear relationships
   - Provides feature importance

### Why These Models?
- **Logistic Regression:** Simple, interpretable, good for understanding feature relationships
- **Random Forest:** More powerful, handles complex patterns, robust to overfitting

## Evaluation Metrics

The models are evaluated using the following metrics:

- **Accuracy:** Overall correctness of predictions
- **Precision:** How many predicted phishing sites were actually phishing
- **Recall:** How many actual phishing sites were correctly predicted
- **F1-Score:** Harmonic mean of precision and recall
- **Confusion Matrix:** Shows true/false positives and negatives

## Results

### Model Performance Comparison

| Model | Accuracy | Precision | Recall | F1-Score |
|-------|----------|-----------|--------|----------|
| Logistic Regression | 1.0000 | 1.0000 | 1.0000 | 1.0000 |
| Random Forest | 1.0000 | 1.0000 | 1.0000 | 1.0000 |

### Best Model
**Logistic Regression** (selected due to tie-breaker, both models achieved perfect performance)

### Performance Notes
Both models achieved perfect performance on this dataset:
- **Accuracy:** 100% - All predictions were correct
- **Precision:** 100% - All predicted phishing sites were actually phishing
- **Recall:** 100% - All actual phishing sites were correctly identified
- **F1-Score:** 1.0000 - Perfect balance of precision and recall

**Important:** The perfect performance is due to the small, curated educational dataset. In real-world scenarios with larger, more diverse datasets, performance would typically be lower and more realistic.

## How to Run the Project

### Prerequisites
- Python 3.7 or higher
- Jupyter Notebook

### Installation

1. Navigate to the project directory:
```bash
cd phishing-website-detection
```

2. Create a virtual environment (recommended):
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

### Running the Notebook

1. Start Jupyter Notebook:
```bash
jupyter notebook
```

2. Open `phishing_detection.ipynb`

3. Run all cells in order (Cell → Run All)

### Testing the Prediction Function

After running the notebook, you can test the `predict_url()` function with custom URLs:

```python
# Example usage
url = "http://suspicious-login-site.com"
prediction = predict_url(url)
print(f"Prediction: {prediction}")
```

## Project Pipeline

```
Dataset (CSV)
    ↓
Data Inspection (shape, columns, missing values, duplicates, class distribution)
    ↓
Data Cleaning (remove duplicates, handle missing values)
    ↓
Feature Engineering (extract 9 URL-based features)
    ↓
Train/Test Split (80% train, 20% test)
    ↓
Feature Scaling (StandardScaler)
    ↓
Model Training (Logistic Regression, Random Forest)
    ↓
Model Evaluation (Accuracy, Precision, Recall, F1-Score, Confusion Matrix)
    ↓
Model Comparison
    ↓
Best Model Selection
    ↓
Prediction Function
```

## Limitations

1. **Small Dataset:** The dataset is relatively small (188 URLs) for demonstration purposes
2. **Perfect Performance:** Both models achieved 100% accuracy, which is unrealistic and indicates the dataset is too simple/easy
3. **Simple Features:** Only basic URL features are used; advanced features like page content, SSL certificates, and domain age are not included
2. **Simple Features:** Only basic URL features are used; advanced features like page content, SSL certificates, and domain age are not included
3. **Binary Classification:** Only distinguishes between phishing and legitimate; doesn't identify specific phishing types
4. **No Temporal Analysis:** Doesn't consider time-based patterns or URL lifecycle
5. **Synthetic/Educational Data:** The dataset is curated for learning and may not represent real-world phishing patterns
6. **No Advanced Techniques:** Doesn't use ensemble methods, deep learning, or sophisticated feature engineering

## Future Improvements

1. **Larger Dataset:** Use a larger, real-world phishing dataset (e.g., from PhishTank, Kaggle)
2. **Advanced Features:** Add features like:
   - Domain age and registration details
   - SSL certificate information
   - Page content analysis
   - WHOIS data
   - URL redirection chains
3. **Additional Models:** Experiment with SVM, Gradient Boosting, or Neural Networks
4. **Real-time Integration:** Deploy as a web service or browser extension
5. **Continuous Learning:** Update model with new phishing patterns
6. **Multi-class Classification:** Identify specific types of phishing attacks
7. **Explainability:** Add SHAP values for detailed model explanations

## Technical Details

### Data Splitting
- **Train/Test Split:** 80% training, 20% testing
- **Stratified Split:** Preserves class distribution in both sets
- **Random State:** 42 (for reproducibility)

### Feature Scaling
- **Method:** StandardScaler (z-score normalization)
- **Fit on:** Training data only (prevents data leakage)
- **Transform on:** Both training and test data

### Model Hyperparameters
- **Logistic Regression:** max_iter=1000, random_state=42
- **Random Forest:** n_estimators=100, random_state=42

## File Structure

```
phishing-website-detection/
│
├── data/
│   └── dataset.csv                 # URL dataset with labels
│
├── phishing_detection.ipynb        # Main Jupyter notebook
├── requirements.txt                # Python dependencies
└── README.md                      # This file
```

## Interview Preparation

### 1. What problem does this project solve?
This project solves the problem of automatically detecting phishing websites to protect users from online fraud and identity theft. It analyzes URL characteristics to classify websites as legitimate or phishing.

### 2. Why is this a classification problem?
This is a classification problem because we're predicting a categorical outcome (phishing vs legitimate) based on input features. Specifically, it's binary classification since there are only two possible classes.

### 3. What features were used and why?
We used 9 URL-based features:
- **URL length, dots, hyphens, special characters, digits:** These structural characteristics often differ between legitimate and phishing sites
- **HTTPS indicator:** Legitimate sites typically use HTTPS for security
- **IP address:** Direct IP addresses are uncommon for legitimate sites
- **Subdomains:** Excessive subdomains can indicate deception
- **Suspicious words:** Phishing sites often use words like "login", "verify", "secure" to appear legitimate

These features were chosen because they're simple to extract, computationally efficient, and have been shown to be effective in phishing detection research.

### 4. Why was Logistic Regression used?
Logistic Regression was used because:
- It's a simple, interpretable baseline model
- It provides coefficients that show feature importance
- It's fast to train and doesn't require hyperparameter tuning
- It helps establish a performance baseline before trying more complex models
- It's easy to explain in interviews

### 5. Why was Random Forest used?
Random Forest was used because:
- It's an ensemble method that combines multiple decision trees
- It can capture non-linear relationships between features
- It's robust to overfitting compared to single decision trees
- It provides feature importance scores
- It typically performs well on classification tasks
- It handles different feature scales well

### 6. Logistic Regression vs Random Forest
- **Logistic Regression:** Linear model, assumes linear relationship between features and target, faster training, more interpretable, can struggle with complex patterns
- **Random Forest:** Non-linear model, can capture complex interactions, slower training, less interpretable (but provides feature importance), typically better performance on complex tasks

### 7. What does train/test split mean?
Train/test split means dividing the dataset into two parts:
- **Training set (80%):** Used to train the model
- **Test set (20%):** Used to evaluate the model on unseen data

This is crucial to test how well the model generalizes to new data and prevents overfitting. The test set must never be used during training.

### 8. What does overfitting mean?
Overfitting occurs when a model learns the training data too well, including noise and patterns that don't generalize to new data. An overfitted model performs well on training data but poorly on test data. Random Forest helps reduce overfitting through ensemble averaging.

### 9. What does the confusion matrix mean?
The confusion matrix shows the model's prediction performance:
- **True Negative (TN):** Correctly predicted legitimate sites
- **False Positive (FP):** Legitimate sites incorrectly flagged as phishing
- **False Negative (FN):** Phishing sites missed (legitimate prediction)
- **True Positive (TP):** Correctly predicted phishing sites

For phishing detection, false negatives are more costly than false positives.

### 10. Accuracy vs Precision vs Recall vs F1
- **Accuracy:** Overall correctness (TP + TN) / Total
- **Precision:** How many predicted phishing sites were actually phishing (TP / (TP + FP))
- **Recall:** How many actual phishing sites were caught (TP / (TP + FN))
- **F1-Score:** Harmonic mean of precision and recall (2 × (Precision × Recall) / (Precision + Recall))

F1-Score provides a single metric that balances precision and recall.

### 11. Why does recall matter for phishing detection?
Recall matters because missing a phishing site (false negative) can lead to:
- Users entering sensitive information on malicious sites
- Financial loss and identity theft
- Security breaches

False positives (flagging legitimate sites as phishing) are less costly but still inconvenient. Therefore, we want to maximize recall while maintaining reasonable precision.

### 12. What are the project's limitations?
- Small dataset size (188 URLs)
- Perfect performance (100% accuracy) is unrealistic and indicates the dataset is too simple
- Simple feature engineering (only URL-based features)
- No analysis of page content or domain reputation
- Binary classification only
- Educational dataset that may not reflect real-world patterns
- No advanced ML techniques used
- The perfect scores suggest the dataset patterns are too obvious and wouldn't generalize to real-world phishing detection

### 13. How does the model predict a new URL?
The prediction process:
1. Extract the same 9 features from the new URL
2. Scale the features using the same scaler fitted on training data
3. Pass the scaled features to the trained model
4. The model outputs a prediction (0 or 1)
5. Convert 0 to "Legitimate" and 1 to "Phishing"

### Complete Project Flow in Simple Language
1. **Load Data:** Read URLs and labels from a CSV file
2. **Inspect Data:** Check data quality, missing values, and class balance
3. **Clean Data:** Remove duplicates and handle missing values
4. **Extract Features:** Convert each URL into 9 numerical features
5. **Split Data:** Divide into training (80%) and testing (20%) sets
6. **Scale Features:** Normalize features to similar ranges
7. **Train Models:** Teach Logistic Regression and Random Forest to recognize patterns
8. **Evaluate Models:** Test both models on unseen data using metrics
9. **Compare Models:** Choose the better performing model
10. **Make Predictions:** Use the best model to classify new URLs

**Note on Performance:** Both models achieved 100% accuracy on this educational dataset. In real interviews, you should acknowledge that this is unusual and due to the small, curated nature of the dataset. Real-world phishing detection typically achieves 85-95% accuracy depending on the complexity of the features and dataset size.

## Conclusion

This project demonstrates a complete machine learning pipeline for phishing detection using simple, interpretable models. It's designed to be educational and easy to understand for beginners learning machine learning concepts.

## License

This is a portfolio project for educational purposes.