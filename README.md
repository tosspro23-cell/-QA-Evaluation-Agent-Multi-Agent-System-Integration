##  QA Agent Self-Learning & Continuous Improvement (Supplementary Section)

This section describes the **self-learning mechanism** of the QA Evaluation Agent, showing how it uses historical case retrieval, embedding, and RAG to continuously improve its evaluation quality and recommendations.

---

### 🖼 Mermaid Diagram: Embedding + RAG Self-Learning Loop

```mermaid
flowchart LR
    A[New Functional Agent Output] --> B[QA Evaluation Agent]
    B --> C[Score & Detect Issues]
    C --> D[Store Case in QA Memory Base]
    D --> E[Generate Embeddings for Output & Recommendations]
    E --> F[Vector Database / Knowledge Store]
    F --> G[Retrieve Similar Past Cases via RAG]
    G --> H[Feed Reference + Updated Prompt to QA Agent]
    H --> I[Functional Agent Re-run or Update]
    I --> B
    style A fill:#E8F0FE,stroke:#1A73E8,stroke-width:2px
    style B fill:#FFF4E5,stroke:#FB8C00,stroke-width:2px
    style C fill:#FFE5E5,stroke:#E53935,stroke-width:2px
    style D fill:#E5FFE5,stroke:#43A047,stroke-width:2px
    style E fill:#FFF4E5,stroke:#FB8C00,stroke-width:2px
    style F fill:#E8F0FE,stroke:#1A73E8,stroke-width:2px
    style G fill:#FFF4E5,stroke:#FB8C00,stroke-width:2px
    style H fill:#FFE5E5,stroke:#E53935,stroke-width:2px
    style I fill:#E8F0FE,stroke:#1A73E8,stroke-width:2px
