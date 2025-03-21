# **🔍 Corrective RAG with LangGraph**  
An advanced **Retrieval-Augmented Generation (RAG) pipeline** using **LangGraph** for corrective feedback loops, ensuring accurate and reliable responses.  

## **🚀 Features**  
✅ **Graph-Based Execution** with **LangGraph**  
✅ **Multi-Step Document Retrieval** (FAISS/BM25)  
✅ **Web Search Fallback** (if no relevant documents)  
✅ **Iterative Response Refinement**  
✅ **LLM-Based Correction Mechanism**  

---

## **📌 Project Workflow**  

1. **Retrieve Documents** → Search knowledge base for relevant data.  
2. **Grade Documents** → Evaluate retrieved documents for relevance.  
3. **Decide Next Step**:  
   - If **relevant documents exist** → Generate answer.  
   - If **not relevant** → Trigger **web search**.  
4. **Generate Initial Response** → LLM generates an answer.  
5. **Corrective Feedback Loop** → RAG iterates to improve accuracy.  

---



## **🖥️ Usage**  

### **Run the Corrective RAG System**  
```bash
python main.py
```

### **Example Query Execution**  
```python
from main import predict_custom_agent_local_answer

example = {"input": "What is an airbag in a car?"}
response = predict_custom_agent_local_answer(example)

print(response)
```

---

## **🧩 Key Components**  

### **1️⃣ StateGraph (LangGraph-based Workflow)**  
```python
from langgraph.graph import StateGraph

class GraphState(TypedDict):
    question: str
    generation: str
    search: str
    documents: List[str]
    steps: List[str]

Workflow = StateGraph(GraphState)
```

### **2️⃣ Document Retrieval**  
```python
def retrieve_documents(state):
    question = state["question"]
    documents = search_in_faiss(question)
    return {"documents": documents}
```

### **3️⃣ Decision Logic**  
```python
def decide_next_step(state):
    return "search" if not state["documents"] else "generate"
```

### **4️⃣ Web Search Integration**  
```python
def web_search(state):
    question = state["question"]
    web_results = web_search_tool.invoke({"question": question})
    return {"documents": web_results}
```

### **5️⃣ Corrective Feedback & Refinement**  
```python
def refine_response(state):
    current_answer = state["generation"]
    corrected_answer = refine_with_llm(current_answer, state["documents"])
    return {"generation": corrected_answer}
```

---

## **🛠️ Future Enhancements**  
- **🔁 User Feedback Integration for Refinement**  
- **📊 Confidence Scoring for Responses**  
- **🔍 Hybrid Search with Dense & Sparse Retrieval**  

---

## **📜 License**  
This project is **open-source** under the **MIT License**.  

---

Let me know if you need further refinements! 🚀
