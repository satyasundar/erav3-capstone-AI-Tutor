# AI-Powered Learning Companion for Schoolchildren

### 🚀 Vision

We aim to build an **interactive, AI-based tutor** that **guides schoolchildren** through academic concepts using **conversational dialogue**, **visual understanding**, and **reasoning**, without giving direct answers.

Think of it as an **open-source version of Khanmigo or Claude for Education**: a tool that helps students **think critically**, **understand deeply**, and **learn independently** across subjects like math, science, and language arts.

---

### 🧩 Core Objectives

- **🧠 Custom Foundation Model** (3B–7B): Train a language model from scratch using educational datasets.
    
- **🖼️ Vision-Language Understanding**: Integrate a VLM like **SigLIP** or **CLIP** to analyze diagrams, figures, or handwritten math.
    
- **🧑‍🏫 Socratic AI Agent**: Design a reasoning agent that uses textbook knowledge and engages students in guided discussions.
    
- **📄 Curriculum-Aware**: Use school book PDFs and retrieval techniques to give accurate, curriculum-aligned help.
    
- **🌐 Deployed Web App**: Build and deploy the assistant via a **Streamlit UI**, powered by a **FastAPI backend** and **MCP** integration.


### 📦 Deliverables

1. **LLM Trained from Scratch**
    
    - Model size: 3B–7B parameters
        
    - Trained using Hugging Face datasets (e.g., `sciq`, `openbookqa`, `wikitext`)
        
    - Uses a pre-trained tokenizer to speed up development
        
2. **Multimodal Integration**
    
    - Pre-trained VLM (SigLIP or CLIP) integrated into the LLM
        
    - Capable of processing images alongside text
        
3. **AI Agent with Reasoning Tools**
    
    - Socratic prompting (guided questioning, not direct answers)
        
    - PDF-based RAG (retrieval-augmented generation)
        
    - Modular agent framework
        
4. **User-Facing UI**
    
    - Built with Streamlit
        
    - Chat interface with support for image upload
        
    - Friendly, kid-safe design
        
5. **MCP Integration + Deployment**
    
    - Backend wrapped in FastAPI
        
    - Integrates with MCP server for async communication
        
    - Fully deployed system (Streamlit Cloud + backend host)
