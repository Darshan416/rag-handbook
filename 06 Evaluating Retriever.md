# **🧪 How to evaluate RAG systems?**

In Retrieval-Augmented Generation (RAG) systems, the retriever is the gatekeeper of relevance. It decides what information your LLM will see. So before you tune the generator, you must ask:

## 👉 Is my retriever surfacing the right documents?

Let’s explore how to measure retrieval quality beyond just latency or throughput. We’re talking about precision, recall, MAP, and MRR—the true north metrics that tell you whether your retriever is doing its job.

## 🎯 Start with Ground Truth

To evaluate a retriever properly, you need three ingredients:

1) A prompt (the user query)
2) The retriever’s ranked results
3) A ground truth list of relevant documents for that prompt
   This ground truth is critical—it’s your "answer key." Without it, you're guessing.

## 📏 Precision vs. Recall

These are the core building blocks of retrieval evaluation:
Precision = Relevant / Retrieved
→ Measures trustworthiness. Are the results useful?
Recall = Relevant / Relevant in corpus
→ Measures coverage. Are you missing anything important?
💡 Trade-off: Increase recall → risk more irrelevant docs → precision drops. The reverse is also true.

## 📦 Precision@K and Recall@K

Since you rarely show users 100 results, we often measure these within the top K results:
Precision@10: % of top 10 that are relevant
Recall@10: % of all relevant docs captured in top 10
📊 Changing K helps simulate strict vs. lenient evaluation environments.

## ⭐ Mean Average Precision (MAP@K)

MAP looks beyond just how many relevant docs were retrieved—it cares about where they were ranked.
Penalizes relevant documents ranked low
Rewards for putting relevant docs higher
Useful when you want to rank well, not just retrieve

## 🔁 Mean Reciprocal Rank (MRR)

Sometimes, getting just one relevant doc fast is more important than getting all of them.
Reciprocal Rank = 1 / (rank of first relevant doc)
MRR = average across multiple prompts
Great when you want to optimize for the first relevant hit—e.g., in FAQs, support bots, or QA systems.

## ⚙️ Why It Matters in RAG

Every time your retriever surfaces irrelevant docs:

1) Your LLM may hallucinate
2) You waste tokens and context space
3) User trust drops

## By tracking precision, recall, MAP, and MRR:

✅ You catch issues early
✅ You validate hybrid retrieval setups (e.g., BM25 + dense embeddings)
✅ You optimize for relevance before worrying about generation quality

## 🚨 Caveat:

All these metrics need labeled data—a list of what should be retrieved. That can be manual and time-consuming. But once you have it, you can:
Compare retriever configs
A/B test hybrid strategies
Monitor quality drift in production
In RAG systems, retrieval is the foundation. If your retriever fails, your generator never had a chance.

📌 TL;DR: Evaluate it. Measure it. Tune it. Your LLM will thank you later.
