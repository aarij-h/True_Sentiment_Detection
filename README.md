# True_Sentiment_Detection

The goal of this project is to assess user sentiment toward a product or service based on their review descriptions. While product ratings (out of 5 stars) are commonly used to gauge sentiment, they do not always reflect the true sentiment of the review. This is due to the ambiguity in how users interpret the star rating, especially for ratings that fall in the middle of the scale (e.g., a 3-star rating).

For instance, users who rate a product 3 stars might have vastly different opinions about the product. While many might consider a 3-star rating as indicating a "decent" product with minor issues, others might rate the product 3 stars despite having major complaints, which should arguably be classified as "negative." This discrepancy in sentiment categorization becomes challenging when trying to infer accurate product sentiment from star ratings alone.

# Approach

To address this issue, we propose using a fine-tuned DistilBERT model to analyze the review descriptions directly, while categorizing the star ratings (1-5) into three distinct sentiment classes:

- Negative Class (1-2 stars)
- Neutral Class (3 stars)
- Positive Class (4-5 stars)
  
While the Neutral class may not be consistent across all samples, we can still train the model to understand the distinction between "Negative" and "Positive" sentiment, while recognizing that "Neutral" represents a "decent" product with minor complaints or issues.

# Key Observations with data...

- Positive (4-5 stars) and Negative (1-2 stars) samples are more straightforward for the model to classify, as the sentiment is clearly defined.
- Neutral (3 stars) samples, however, show more variability. Some samples indicate a product with minor issues ("decent"), while others show more significant problems, creating a misalignment with the traditional idea of a "neutral" rating.

**Example of Neutral-rated Samples:**

Set 1 (Neutral-rated samples) - Minor complaints:
  
a] "Not bad, good solid tour of Italy. Ending could have been more exciting...."

- Model Classification: Neutral (minor complaint)
  
b] "I liked the book but I believe it could use more action and details! BOOM SAUCE! ;) ;) ;) :) :) :)"

- Model Classification: Neutral (minor complaint)

c] "Good book, loved it, just dragged on a tiny bit."

- Model Classification: Positive
  
d] "As good as her other book, The Husband's Secret. A good read!"

- Model Classification: Positive
  
Set 2 (Neutral-rated samples) - Major complaints:
a] "Keeps shutting down. Not pleased with this app."

- Model Classification: Negative (major complaint)

b] "Takes too long for energy to recharge."

- Model Classification: Negative (major complaint)

c] "Not what I really wanted, didn't fit my ear! But cost time and money to send back!"

- Model Classification: Negative (major complaint)
  
d] "I cannot really rate the movie. The very poor streaming of it made it unbearable to watch."

- Model Classification: Negative (major complaint)

Observations from the Examples:
Set 1 generally indicates a "decent" product with minor complaints (aligned with our definition of Neutral).
Set 2, on the other hand, is more consistent with a "Bad" or "Negative" product, despite being rated as Neutral.
<br>
Thus, while the Neutral class does not always align with what we expect, the model still performs well in distinguishing Positive and Negative sentiment, especially for Set 2, which can be classified as more critical reviews.

# Model Performance

Now we take a look at a few metrics to evaluate how our model performs.

Class | Precision| Recall | f1-score
---| ---| ---| ---
Negative | 0.73| 0.77| 0.75
Neutral| 0.65| 0.57| 0.61
Positive| 0.78| 0.84| 0.80
Total Accuracy| ---| ---| 0.73
