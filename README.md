## QA Agent Self-Learning Loop

The QA Evaluation Agent within our Multi-Agent Architecture has a **self-learning mechanism** that allows it to improve its evaluation and suggestion quality over time by referencing historical evaluation cases. This mechanism can work at two levels:

1. **MVP Level** (Excel / Dataverse + Few-Shot)
2. **RAG Level** (Embeddings + Vector Database Retrieval)

---

### 1️⃣ Self-Learning Logic (Text Overview)

1. **Output Evaluation**
   - QA Agent evaluates the output of a Functional Agent.
   - Produces:
     - **Natural Language Summary** (human-readable)
     - **Structured JSON Output** (stored in case repository)

2. **Case Storage**
   - **MVP**: JSON stored in Excel / Dataverse table.
   - **RAG**: JSON stored in vector database as embeddings.

3. **Case Retrieval**
   - **MVP**: Read historical cases manually or via Power Automate flow; feed into prompt as Few-Shot examples.
   - **RAG**: Automatically retrieve top-N most relevant historical cases using vector similarity search.

4. **Prompt Injection**
   - Retrieved cases are injected into QA Agent prompt to improve evaluation quality.
   - Provides context: what correct outputs look like, previous deviations, recommendations.

5. **Continuous Improvement**
   - QA Agent evaluates new outputs **in context of historical cases**, improving consistency and accuracy.
   - Each new evaluation can itself be stored as a new case to enrich the repository.

---

### 2️⃣ Comparison: MVP vs RAG Self-Learning

| Feature | MVP (Excel / Dataverse) | RAG + Vector DB |
|---------|------------------------|----------------|
| Case Storage | Excel / Dataverse table | Embeddings in vector database |
| Retrieval | Manual / Flow-based | Automatic, similarity-based |
| Few-Shot Context | Limited by token length | Can handle large historical dataset |
| Automation | Low | High |
| Scalability | Low | High |
| Performance | Slow with large datasets | Fast retrieval and contextualization |

---

### 3️⃣ Mermaid Diagram (Self-Learning Loop)

```mermaid
flowchart TD
    A[Functional Agent Output] --> B[QA Agent Evaluation]
    B --> C{Output Components}
    C --> C1[Natural Language Summary]
    C --> C2[Structured JSON Case]
    C2 --> D[Case Storage]
    D --> D1[MVP: Excel / Dataverse]
    D --> D2[RAG: Vector DB + Embeddings]
    B --> E[Evaluation Summary Feed]
    E --> F[Prompt Injection for Next Evaluation]
    D1 --> F
    D2 --> F
    F --> B
    style B fill:#f9f,stroke:#333,stroke-width:2px
    style D1 fill:#bbf,stroke:#333,stroke-width:1px
    style D2 fill:#bbf,stroke:#333,stroke-width:1px
    style F fill:#bfb,stroke:#333,stroke-width:1px
