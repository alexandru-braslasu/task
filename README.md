# Company Classifier

## Short description
This notebook performs **automatic business classification** for insurance-related companies using **cosine similarity** and **Sentence Transformers**. It assigns taxonomy labels to businesses based on their descriptions, industry sector, and other relevant attributes. The final output is a CSV file containing classified companies.

---

## Implementation
The classification is based on **text similarity** between company descriptions and predefined taxonomy labels. The core model used for text embedding is **all-MiniLM-L6-v2**. The classification follows these steps:

### Key steps in the process:
1. **Loading the Data** – The system reads company details from `ml_insurance_challenge.csv` and taxonomy labels from `insurance_taxonomy.xlsx`.
2. **Text Preparation** – Standardizes text by lowercasing, trimming spaces, and merging relevant columns (`description`, `business_tags`, `sector`, `category`, `niche`).
3. **Generating Embeddings** – Uses **Sentence Transformers** to convert text into numerical vectors.
4. **Computing Similarity Scores** – Applies **cosine similarity** between company embeddings and taxonomy embeddings.
5. **Assigning Labels** – Matches each company with the taxonomy labels that exceed a similarity threshold.
6. **Saving the Results** – The classified data is stored in `classified_companies.csv`.

---

## Dynamic Threshold Reduction Strategy
To ensure the best classification, the threshold is **gradually lowered from 0.99**. This strategy helps to avoid companies being left unclassified while maintaining accuracy.

### **Advantages of This Approach:**
- **Increases classification rate** – If no label initially meets 0.99, lowering the threshold allows reasonable matches, reducing "Unclassified" cases.
- **Balances precision and coverage** – A high threshold ensures accurate labels, while gradual relaxation prevents forced misclassifications.
- **Acts as an intelligent fallback system** – If a perfect match isn’t found, the model slowly adjusts, finding the next best alternative.

---

## Data Challenges
- The dataset requires **column name standardization** before processing.
- Some company descriptions may be incomplete, affecting classification accuracy.
- If no label reaches the similarity threshold, the company is marked as **Unclassified**.

---

## Results
The classification assigns each company to the **most similar taxonomy labels**. If no strong match is found, a lower similarity threshold is tested afterward until classification occurs. The results are saved in `classified_companies.csv`.

---

## Code Structure
The notebook is structured as follows:
1. **Importing Libraries** – Uses Pandas, NumPy, Sklearn, and Sentence Transformers.
2. **Loading and Preparing Data** – Reads the input files, standardizes text, and prepares the dataset.
3. **Generating Embeddings** – Converts text descriptions into vector representations.
4. **Computing Similarity and Assigning Labels** – Compares company embeddings with taxonomy labels and assigns classifications.
5. **Saving the Results** – Exports the classified companies to `classified_companies.csv`.

---

## Observations
This notebook provides an **efficient way to classify companies** without supervised training. Potential improvements include:
- **Fine-tuning the threshold selection** to improve label accuracy.
- **Evaluating performance metrics** to validate classification quality.
- **Exploring alternative similarity measures** (e.g., Euclidean distance, Pearson correlation).

---

## 8. Execution Environment  
The notebook was executed in **Google Colab** to leverage cloud-based resources for faster processing.