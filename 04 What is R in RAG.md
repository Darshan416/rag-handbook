# 🔍 From Keyword Search to Hybrid Search: A Complete Guide to Retrieval in RAG

## 🧱 1. Keyword Search: Precision Through Matching

Keyword search matches documents based on the overlap of exact words. It transforms text into sparse vectors (word count-based), often scored with algorithms like BM-25.

### ✅ Strengths:

Fast, interpretable, and efficient
Excellent when documents and prompts share domain-specific terms (e.g., product names, medical terms)
Great for debugging and high-precision needs

### ❌ Limitation:

Can’t match documents that mean the same thing but use different words.

## 🧠 2. Semantic Search: Understanding Meaning

Semantic search encodes both documents and prompts into dense vector embeddings using models like BERT or OpenAI Embeddings. Retrieval is based on vector similarity—how close two meanings are in high-dimensional space.

### ✅ Strengths:

Finds conceptually similar content, even when exact words don’t match
Ideal for handling synonyms, paraphrasing, or vague queries

### ❌ Limitation:

Requires more compute
Less interpretable than keyword search
May occasionally retrieve loosely related results

### 🏷️ 3. Metadata Filtering: Precision Cuts

Before or after ranking, many systems use metadata filters—rigid constraints based on structured data (e.g., date ranges, document type, access level).

### ✅ Strengths:

Fast yes/no filtering
Helps narrow the scope to what's contextually or organizationally relevant

### ❌ Limitation:

Not a retrieval technique by itself, but a filter layer

## 🔀 4. Hybrid Search: Best of All Worlds

Real-world systems rarely choose just one of these methods.
🔄 Instead, they use a hybrid search pipeline that combines:

BM25 for exact keyword match
Semantic search for meaning
Metadata filtering for strict criteria

### Here’s how it works:

The retriever receives a prompt
It performs both BM25 and semantic search, producing two ranked lists
Metadata filters remove irrelevant documents from both lists
The remaining results are merged using Reciprocal Rank Fusion (RRF)

### 📊 RRF: Merging Two Worlds

Reciprocal Rank Fusion scores documents based on how high they appear in each list:

A document ranked 1st gets a score of 1 / (K + 1)
Ranked 2nd = 1 / (K + 2), and so on
Total score = sum of scores from keyword and semantic lists

K controls how strongly top-ranked docs dominate.
A smaller K gives more weight to top documents.
A larger K smooths the ranking and balances both sources.

🎚️ You also get another tuning knob: β (beta)
It controls how much weight you give to semantic vs keyword search.
Example: β = 0.8 → 80% semantic + 20% keyword
Use a 70–30 split as a good starting point
