# 💬 YouTube Transcript Chatbot (RAG Pipeline)

## Project Summary

This project creates a **Retrieval-Augmented Generation (RAG)** chatbot using **LangChain** and a **Hugging Face LLM** (Llama 3) to answer questions based **only** on the content of a specific YouTube video transcript.

The pipeline ingests the video text, converts it to numerical embeddings, and retrieves the most relevant snippets to generate factual, context-grounded answers, effectively preventing the LLM from hallucinating.

---

## ⚙️ Key Technologies

| Component | Technology | Role |
| :--- | :--- | :--- |
| **Data Source** | `youtube-transcript-api` | Fetches the raw video text. |
| **Embedding Model** | `BAAI/bge-m3` | Converts text into vectors. |
| **Vector Store** | `FAISS` | Indexes and stores vectors for fast **Retrieval**. |
| **LLM (Augmentation)** | `Meta-Llama-3-8B-Instruct` | Generates the final, context-based answer. |
| **Framework** | `LangChain` | Builds the efficient RAG chain. |

---

## 🚀 RAG Pipeline Flow

The chatbot works in three key steps:

1.  **Indexing:** The transcript is split into **chunks** and stored as **embeddings** in the FAISS vector database.
2.  **Retrieval:** When a question is asked, the system quickly retrieves the **top 3 most relevant text chunks** from the database.
3.  **Generation (Augmentation):** These chunks are inserted into a strict prompt ("Answer only from the provided context") and sent to the **Llama 3** model to produce the final answer.

### Final Code Example (RAG Chain)

The complete pipeline is orchestrated using LangChain Runnables:

```python
main_chain = parallel_chain | prompt | chat_model | parser
# Example Invocation:
# main_chain.invoke("Can you summarize the video ?")
