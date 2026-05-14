
# General Health Query Chatbot

This repository is focusing on building a safe and informative general health query chatbot.

## Task Objective

The primary objective of this task was to develop a general health information chatbot, named `HealthBot`, capable of providing accurate and safe health advice. The chatbot incorporates prompt engineering and a robust safety filtering system to prevent harmful or inappropriate responses, such as medical diagnoses, prescriptions, or emergency advice.

## Data/Knowledge Source

This chatbot does not rely on a specific training dataset in the traditional sense. Instead, it leverages the vast knowledge base of a large language model (LLM) and is guided by a carefully crafted system prompt to provide general health information. Its responses are based on the LLM's pre-trained knowledge, filtered and constrained by the safety mechanisms implemented.

## Models Applied

-   **Primary LLM**: The chatbot utilizes the **OpenRouter API** to access various large language models. For this implementation, the `openai/gpt-3.5-turbo` model was specifically configured (`MODEL = "openai/gpt-3.5-turbo"`).
-   **Technique**: The core technique applied is **Prompt Engineering** to guide the LLM's behavior, coupled with a multi-layered **Safety Filtering** system (regex-based pre-filter and a post-filter) to ensure responsible AI interactions.

## Key Results and Findings

### Multi-Layered Safety

The chatbot successfully implements a three-layer safety mechanism:
1.  **Pre-filter**: Uses regular expressions to intercept dangerous queries (e.g., emergency, diagnosis, prescription requests, harmful substance queries) *before* they reach the LLM, returning a pre-written safe response.
2.  **System Prompt (Prompt Engineering)**: Explicitly defines `HealthBot`'s persona, purpose, and strict rules (e.g., never diagnose, never prescribe, always recommend a doctor).
3.  **Post-filter**: Scans the LLM's output for any risky phrases that might have slipped through and appends a safety disclaimer if found.

### Performance Highlights

-   **Average Evaluation Score**: The chatbot achieved an average score of **81.2%** across a set of diverse test cases, indicating good adherence to expected keywords and safety protocols.
-   **Effective Emergency Handling**: Queries related to medical emergencies, diagnosis, and prescription requests were successfully blocked by the pre-filter, demonstrating 100% effectiveness in these critical safety scenarios.
-   **Contextual Conversations**: With `remember_history=True`, the chatbot maintains conversation context, allowing for natural multi-turn interactions.

### Strengths

-   Robust three-layer safety (pre-filter, prompt engineering, post-filter).
-   Emergency queries are intercepted immediately, without LLM interaction.
-   Supports multi-turn conversations with memory.
-   Flexibility to swap LLM models via OpenRouter without modifying safety logic.
-   Consistent professional tone enforced by the system prompt.

### Limitations

-   No persistent memory across different Colab sessions.
-   Reliance on regex filters means cleverly rephrased dangerous queries might bypass the pre-filter.
-   Response quality is dependent on the performance of the chosen free-tier model.
-   Currently English-only, without multilingual support.
-   Lacks real-time integration with medical databases or official guidelines (e.g., NHS/WHO).

### Next Steps for Production

To enhance `HealthBot` for a production environment, future work could include:
-   Integrating a Retrieval Augmented Generation (RAG) pipeline with authoritative medical guidelines (e.g., NHS, WHO, NICE).
-   Replacing regex pre-filters with a more sophisticated LLM-based safety classifier.
-   Developing a user-friendly web interface (e.g., using Streamlit or Gradio).
-   Implementing user feedback mechanisms for continuous prompt improvement.
-   Establishing logging and auditing for all queries to ensure ongoing clinical safety review.

## ⚠️ Disclaimer

This chatbot is developed for **EDUCATIONAL purposes only**. It is **NOT** a medical device and must never replace professional medical advice, diagnosis, or treatment. Always consult a qualified healthcare professional for personal medical concerns.
