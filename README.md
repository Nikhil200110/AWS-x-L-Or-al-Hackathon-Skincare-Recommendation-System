# Skin Condition Classification Hackathon - Team 3

## Overview
This project was developed as part of the L'Oréal Skin Condition Classification Hackathon. The goal was to create a sustainable and efficient machine learning model capable of classifying skin conditions (e.g., oily, dry, acne-prone) based on beauty product descriptions. The project leverages Large Language Models (LLMs) for data labeling and trains a classification model while optimizing for both accuracy and environmental sustainability (measured via carbon emissions).

---

## Team Members
- **Nikhil Gaikwad**  
- **Abdul Hadi**  
- **Adetutu Adebayo**  
- **Amit Joshi**  

---

## Project Pipeline
The project followed a structured pipeline to achieve its objectives:

1. **AWS for Prompting**: Utilized AWS services for managing prompts and data storage.  
2. **Label Data Using LLM & Prompts**: Employed LLMs (Claude 3.5 Sonnet, Llamo 3.1 70B Instruct, etc.) to label unlabelled product descriptions.  
3. **Train Classification Model**: Trained multiple machine learning models on the labeled dataset.  
4. **Evaluate Carbon Emissions**: Measured the environmental impact of model training using the `codecarbon` library.  

---

## Data Labeling Process
### Steps:
1. **Ingest & Extract**:  
   - Data was stored in an AWS S3 bucket and processed using AWS SageMaker.  
   - Binary classification was applied to product descriptions to identify skin conditions.  

2. **Enrich**:  
   - Cross-verification and validation were performed to ensure label accuracy.  
   - Automated validation was used due to the impracticality of manually verifying 6,000+ descriptions.  

### Prompt Template:
The LLM was guided to:  
- Extract attributes (e.g., skin concerns, age groups, skin types) using synonyms and contextual mapping.  
- Perform binary classification (`1` for present, `0` for absent).  
- Output a comma-separated list of binary values without additional explanations.  

Example attributes included:  
- **Skin Concerns**: Dark pigmentation, acne, wrinkles.  
- **Age Groups**: 18-34, 35-54, 55-99.  
- **Skin Types**: Dry, oily, combination.  

---

## Model Training
### Steps:
1. **Data Preprocessing**:  
   - Text cleaning (removing special characters, stopwords, lemmatization).  
   - Vectorization using `TfidfVectorizer` with character n-grams.  

2. **Model Training**:  
   - Multiple models were trained, including LightGBM, SVM, XGBoost, and RoBERTa.  
   - Hyperparameter tuning was performed to optimize performance.  

3. **Evaluation Metrics**:  
   - Accuracy, F1-score, recall, and precision were used to assess model performance.  
   - Carbon emissions were tracked using `codecarbon`.  

---

## Results
### Performance Comparison
| Model               | Accuracy | F1-score | Carbon Emission (kg CO2) |
|---------------------|----------|----------|---------------------------|
| RoBERTa + LightGBM  | 0.90     | 0.84     | 0.0069                    |
| LightGBM            | 0.88     | 0.84     | 0.0005                    |
| SVM                 | 0.87     | 0.82     | 0.0151                    |
| XGBoost             | 0.89     | 0.82     | 0.0020                    |
| Gradient Boosting   | 0.88     | 0.82     | 0.0128                    |
| Random Forest       | 0.79     | 0.76     | 0.0001                    |
| RoBERTa + XGBoost   | 0.90     | 0.83     | 0.0069                    |

### Key Findings:
- **Highest Accuracy**: RoBERTa + LightGBM (0.90 accuracy, 0.84 F1-score).  
- **Lowest Carbon Emissions**: Logistic Regression (0.0001 kg CO2).  
- **Recommended Model**: Logistic Regression + LightGBM (balanced accuracy and emissions).  

---

## Recommendations
1. **Prioritize Sustainability**:  
   - Use Logistic Regression + LightGBM for low emissions without significant accuracy trade-offs.  
2. **Hybrid Approach**:  
   - Combine high-accuracy models (e.g., RoBERTa) for critical tasks with sustainable models for less critical tasks.  
3. **Optimization Strategies**:  
   - Hyperparameter tuning, data augmentation, and transfer learning to further improve performance and efficiency.  

---

## Conclusion
This project demonstrates the feasibility of building accurate and sustainable machine learning models for skin condition classification. By leveraging LLMs for data labeling and optimizing model training, we achieved a balance between performance and environmental responsibility.  

For long-term success, L'Oréal can adopt a hybrid approach, integrating high-accuracy models where needed while gradually transitioning to more sustainable solutions.  

---

## Acknowledgments
- **L'Oréal** for organizing the hackathon.  
- **KEDGE Business School** for their support.  
- **AWS** for providing the infrastructure and tools.  

---

## Repository Structure
- `data/`: Contains labeled and unlabelled datasets.  
- `notebooks/`: Jupyter notebooks for data labeling, model training, and evaluation.  
- `models/`: Saved model files.  
- `results/`: Performance metrics and carbon emission reports.  

For detailed code and implementation, explore the repository!  
