# CTF_STU160: AI Detective Challenge

## Project Overview
This repository contains the solution for the "Capture the Flag" AI Detective challenge. The objective was to identify a manipulated book within a large dataset of books and reviews, locate hidden clues, and train a Machine Learning model to distinguish between suspicious and genuine reviews.

## Approach Summary
My solution automates the forensic process using the following workflow:

1.  **Hash Generation:** Computed the SHA256 target hash derived from my Student ID.
2.  **Metadata Filtering (Flag 1):** Filtered `books.csv` to identify "suspect" books matching specific criteria (1234 ratings, 5.0 average rating) and extracted their `parent_asin` identifiers.
3.  **Content Search (Flag 2):** Scanned `reviews.csv` for the target hash to locate the specific manipulated review and confirm the target book.
4.  **Authenticity Analysis (Flag 3):**
    * Trained a Logistic Regression model (TF-IDF vectorization) on the dataset to classify reviews as "Suspicious" (short) or "Genuine" (detailed).
    * Utilized SHAP (SHapley Additive exPlanations) to interpret the model and identify the top 3 words that contribute to a review being classified as genuine.

## Repository Structure
* `solver.py`: The single Python script that automates the retrieval of Flag 1, Flag 2, and Flag 3.
* `flags.txt`: The final output file containing the three required flags.
* `reflection.md`: A detailed report (150–250 words) explaining the methodology, analysis, and challenges faced.
* `README.md`: This project summary.

## Setup & Execution
### Prerequisites
The solution requires Python and the following libraries:
* `pandas`
* `numpy`
* `scikit-learn`
* `shap`
* `nltk`

### How to Run
1.  Ensure `books.csv` and `reviews.csv` are in the root directory.
2.  Run the solver script:
    ```bash
    python solver.py
    ```
3.  The script will output the flags to the console and the process flow.
