## ⚙️ Phase 1: Pre-Training (Week 1–2)

### 1. Define Datasets

    1.1  Identify suitable Hugging Face datasets:
    		1.1.1 Datasets like sciq, openbookqa, math_qa, wikitext, bookcorpus
    		1.1.2 Filter datasets relevant for school curriculum
    		1.1.3 Need to check if Cosmo dataset can be used for pretraining

    1.2  Preprocess:
    		1.2.1 Clean and standardize formatting
    		1.2.2 Ensure all examples follow instruction-style format

    1.3 Store as HF datasets.Dataset

### 2. Tokenizer

    2.1 Use a pre-trained tokenizer. LLM suggested GPT-NeoX tokenizer. Need  to discuss and select.
    2.2 Load using HuggingFace's AutoTokenizer
    2.3 Ensure tokenizer supports pad token, eos token etc.
    2.4 Tokenize and cache datasets for faster training

### 3. Define Model code

    3.1 Choose architecture(decoder-only) for the model.
    	3.1.1 We can get the model config from HF
    	3.1.2 Look at the parameter count to be between 3B - 7B as per budget
    	3.1.3 Ask the LLM to generate base code from model config
    	3.1.4 Modify the base code as per our need

    3.2 Enhancd the code to include below features
    	3.2.1 Multi-GPU support - accelerate or deepspeed suggested by LLM
    	or some other technique.
    	3.2.2 gradient accumulation steps
    	3.2.3 fp16
    	3.2.4 save strategy
    	3.2.5 Logging via wandb or tensorboard
    	3.2.5 weight watchers (incase needed)
    	3.2.6 Implement with SkyPilot to better run on AWS

### 4. Dev Testing of Model Code

    4.1 Base code with above features to run on small dataset in colab
    4.2 Prepare a small dataset
    4.3 Run the model code on Colab with small dataset
    4.3 Test for
    	- Forward pass
    	- Loss
    	- gradient accumulation
    	- Save intermediate model checkpoint
    	- Resume training from checkpoint
    	- Check for proper logs and items to capture in the log

    4.4 Evaluation script on held-out validation set

### 5. AWS Setup

    5.1 Decide on EC2 Instance [List the choices and discuss on it]
    5.2 Setup EBS volume for training data and checkpoints
    5.3 Upload datasets and checkpoints to S3
    5.4 Use tmux effectively to manage sessions

## 🎯 Phase 2: Fine-Tuning / SFT (Week 2–3)

### 6. Prepare Curriculum-Aligned PDFs

    6.1 Convert school book PDFs to text using OCR tools
    (e.g., PyMuPDF, Tesseract)
    6.2 Segment chapters, align with subjects
    6.3 Format into instruction–response format
    6.4 Store in FAISS index for retrieval

### 7. Fine-Tuning (SFT)

    7.1 Use LoRA/QLoRA to save memory (via peft)
    7.2 Train on PDF-derived examples
    7.3 Add callbacks for evaluation
    7.4 Fine-tuning for Socratic behaviour:
    Not giving direct answers but to nudges learners to
    think critically by giving context and hints.
    7.5 Fine-tuning for Agentic output - Function calling
    7.6 Save final fine-tuned checkpoint

## 🖼️ Phase 3: VLM Integration (Week 3)

### 8. Load Vision Model

    8.1 Use SigLIP or CLIP (pre-trained from Hugging Face)
    8.2 Add preprocessing pipeline (resize, normalize, patchify)
    8.3 Encode image into embeddings

## 9. Multimodal Fusion

    9.1 Combine Text+Vision input:
    	- Concatenate embeddings OR
    	- Use cross-attention layers if supported (need to check on this)
    9.2 Validate fusion with toy examples (e.g., image question-answering)

## 🤖 Phase 4: Agent Logic (Week 4)

### 10. Agent Design

    10.1 Build prompt templates:
    		Use Socratic questioning: "What do you know?", "Why might that be?"
    10.2 Add retrieval module:
    	10.2.1 Use FAISS index of textbooks
    	10.2.2 Return top-3 chunks per query

    10.3 Wrap agent in modular python functions
    10.4 Setup MCP server and tools integration

## 🌐 Phase 5: Backend + Frontend (Week 4)

### 11. Bankend API (FastAPI)

    11.1 Endpoint: /chat, /upload_image, /context
    11.2 Load LLM + vision encoder
    11.3 Async generation with streaming tokens
    11.4 Add health check + logging endpoints

### 12. MCP Integration

    12.1 Add support for message queue (MCP server)
    12.2 Handle bi-directional communication
    12.3 Store logs/session history for context continuity

### 13. Frontend (Streamlit UI)

    13.1 Layout:
    	- Left : Chat Window
    	- Right : Image output and subject selector

    13.2 Show intermediate reasoning steps
    13.3 Add accessibility features (font size, contrast)

## 🚀 Phase 6: Deployment + QA (Week 5)

### 14. Deployment

    14.1 Host backend on EC2 or Hugging Face Spaces (for demo)
    14.2 Try to implement vLLM optimisation while serving
    14.3 Host frontend on Streamlit Cloud or EC2
    14.4 Secure endpoints via token auth

### 15. QA + Testing

    15.1 Test across subjects: Math, Science, Reading
    15.2 Simulate classroom use
    15.3 Evaluate for correctness, engagement, and helpfulness

## 16. Final Report

    16.1 Document architecture and stack
    16.2 Make demo video
    16.3 Describe limitations + future work (e.g., safety, bias)
