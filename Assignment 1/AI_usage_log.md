## I used Chat for creating my visualizations by prompting it with the titles and labels I wanted as well as the type of visualization. I wanted to make sure that there was consistency across visuals. I also used chat to help make my output print cleaner so I had it help me with formatting.

##I asked Chat to help me figure out how to make the data used in the analysis accessible to anyone on any computer. It suggested I upload the data to my GitHub so I did that.

##I asked chat to write me a function that checks the speeds of each of the models and I also had it write me the code to output this information as an organized table.

##I uploaded an example of the model table to chat as well as my classification report and asked for it to be organized in a neat markdown way with my justifications so that I could more easily format the information in a table.
------------------------------------------------------------------------

## Task: Apply sentiment models to sample text + create labels

**What I was trying to do:**\
Run sentiment models on a sample of airline reviews and generate
predicted labels for comparison. Chat provided example code to run models on `ReviewBody`, store scores, and
map scores to `positive/neutral/negative`.

------------------------------------------------------------------------

## Task: Extract only the VADER compound score efficiently


**What I was trying to do:**\
I wanted to store only the VADER compound score (not the full polarity dict) as a
numeric column.
I created a separate `vader_compound` column for the sampled dataset.\
- Ensured consistent naming between compound scores and prediction
labels.

**What I Learned:**\
- VADER returns multiple metrics (pos, neu, neg, compound).\
- The compound score is the normalized overall sentiment value ranging
from -1 to 1.

**AI Errors Found:**\
- AI did not warn about potential column mismatches (e.g., `compound` vs
`vader_compound`) which could lead to incorrect printed results.

------------------------------------------------------------------------

## Task: Create custom text cleaning function for airline reviews

**What I was trying to do:**\
Clean airline review text by removing HTML, URLs, numbers, and extra
whitespace before running sentiment models.

**AI Prompt:**\
"What kind of cleaning should I be doing for NLP? Give an example of a Python function to clean text by removing HTML, URLs,
lowercasing, and normalizing whitespace for NLP preprocessing."

**What I Modified:**\
- Added contraction expansion (e.g., "don't" → "do not").\
- Removed numbers to reduce noise in long narrative reviews.\
- Applied the function specifically to the `ReviewBody` column.\
- Validated cleaning using before and after examples from the dataset.

**What I Learned:**\
- Over-cleaning can remove meaningful sentiment  if not carefully
controlled.

------------------------------------------------------------------------

## Task: Design model-specific preprocessing for VADER, TextBlob, and Transformer


**What I was trying to do:**\
Decide whether all sentiment models should use the same cleaned text or
separate preprocessing pipelines.


**AI Response:**\
Explained that VADER should not be aggressively cleaned or lowercased,
while TextBlob benefits from normalized text and transformers perform
better with more natural language input.

**What I Learned:**\
- Different NLP models require different preprocessing strategies.\
- Model-aware preprocessing leads to more valid and fair model
comparison.
-Using identical preprocessing would bias the comparison and reduce VADER
performance since it relies on punctuation and capitalization intensity
signals.

------------------------------------------------------------------------

## Task: Create domain-specific stopword list for airline sentiment analysis



**What I was trying to do:**\
Develop a custom stopword list tailored to airline review text to reduce
noise in sentiment analysis.

**AI Prompt:**\
"How do I create custom stopwords for sentiment analysis on airline
reviews using NLTK?"

**AI Response:**\
Suggested loading NLTK English stopwords and adding custom stopwords like airline or british airways

**What I Modified:**\
- I initially removed custom words but then spoke to Professor Vo and ended up removing these from the stopwords list since it can provide context. for instance if someone says something negative about another airline we might misinterpret the review

