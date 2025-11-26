#CTF Challenge Reflection

##Methodology
To solve the "AI Detective" challenge, I employed a data forensic approach linking metadata analysis with content scanning.

Target Identification (Flag 1 & 2): I generated my unique search signature (87ED580B) by hashing my Student ID STU007. I filtered the books.csv metadata to isolate "suspect" books matching the anomaly criteria: exactly 1234 ratings with a perfect 5.0 average. Instead of relying on potentially inconsistent titles, I extracted the parent_asin identifiers to link these suspects to the reviews.csv dataset. Scanning the text of these linked reviews revealed the hidden hash within a review for Borrowed Time, allowing me to calculate Flag 1 from the book's title and Flag 2 directly from the hash.

Analysis & Machine Learning (Flag 3)
For the final phase, I developed a Machine Learning pipeline to explain review authenticity.

Model Training: I utilized TF-IDF vectorization and a Logistic Regression classifier to distinguish between "Suspicious" (short/bot-like) and "Genuine" (detailed) reviews.

Explainability: Using SHAP (SHapley Additive exPlanations), I analyzed the model's decision-making process for the "Genuine" class. The analysis revealed that the tokens "br" (likely representing line breaks in formatted text), "world", and "34" were the strongest indicators of authenticity.

Challenges & Resolution
A critical challenge arose when isolating the target book for analysis: it contained insufficient data (only 2 reviews) to train a viable local model. I resolved this by expanding the training scope to the global dataset, enabling the model to learn universal linguistic patterns of genuine reviews, which were then successfully applied to generate Flag 3.