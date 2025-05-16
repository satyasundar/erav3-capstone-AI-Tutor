⚙️ Phase 1: Pre-Training (Week 1–2)

1. Define Datasets

  1.1 Identify suitable Hugging Face datasets:
     sciq, openbookqa, math_qa, wikitext, bookcorpus
  1.2 Filter datasets relevant for school curriculum (Grades 4–10)
  
  1.2 Preprocess:
    1.2.1 Clean/standardize formatting
    1.2.2 Ensure all examples follow instruction-style format
  
  1.3 Store as HF datasets.Dataset objects

2. Tokenizer

  2.1 Use a pre-trained tokenizer (e.g., GPT-NeoX tokenizer):
  2.1.1 Load using Hugging Face's AutoTokenizer
  
  2.2 Ensure tokenizer supports pad token, eos token
  
  2.3 Tokenize and cache dataset for faster training

3. Define Model Code

  3.1 Use Hugging Face transformers library
  3.2 Choose architecture: GPT-style decoder-only model (3B–7B)
  3.3 Validate with toy dataset in Colab:
    3.3.1 Sample small dataset
    3.3.2 Run forward pass + loss

4. Add Training Utilities

  4.1 Multi-GPU support using accelerate or deepspeed
  4.2 Add config flags:
    4.2.1 gradient_accumulation_steps, fp16, save_strategy
  4.3 Add model checkpointing and resumption
  4.4 Logging via wandb or tensorboard
  4.5 Evaluation script on held-out validation set

5. AWS Setup

  5.1 EC2 instance: g5.12xlarge (A10G x4) or p4d.24xlarge (A100 x8)
  5.2 Attach 1 TB EBS volume for training data and checkpoints
  5.3 Upload datasets/checkpoints to S3
  5.4 Use tmux for long-running training jobs

🎯 Phase 2: Fine-Tuning / SFT (Week 2–3)

6. Prepare Curriculum-Aligned PDFs

  6.1 Convert school book PDFs to text using OCR tools (e.g., PyMuPDF, Tesseract)
  6.2 Segment chapters, align with subjects
  6.3 Format into instruction–response format
  6.4 Optional: Store in FAISS index for retrieval

7. Fine-Tuning (SFT)

  7.1 Use LoRA/QLoRA to save memory (via peft)
  7.2 Train on PDF-derived examples
  7.3 Add callbacks for evaluation
  7.4 Save final fine-tuned checkpoint

🖼️ Phase 3: VLM Integration (Week 3)

8. Load Vision Model

  8.1 Use SigLIP or CLIP (pre-trained from Hugging Face)
  8.2 Add preprocessing pipeline (resize, normalize, patchify)
  8.3 Encode image into embeddings

9. Multimodal Fusion

  9.1 Combine text + vision inputs:
     Concatenate embeddings OR
     Use cross-attention layers if supported
     
  9.2 Validate fusion with toy examples (e.g., image question-answering)

🤖 Phase 4: Agent Logic (Week 4)

10. Agent Design

  10.1 Build prompt templates:
        Use Socratic questioning: "What do you know?", "Why might that be?"
        
  10.2 Add retrieval module:
    10.2.1 Use FAISS index of textbooks
    10.2.2 Return top-3 chunks per query
    
  10.3 Wrap agent in modular Python function

🌐 Phase 5: Backend + Frontend (Week 4)

  11. Backend API (FastAPI)
  
    11.1 Endpoint: /chat, /upload_image, /context
    11.2 Load LLM + vision encoder
    11.3 Async generation with streaming tokens
    11.4 Add health check + logging endpoints

12. MCP Integration

  12.1 Add support for message queue (MCP server)
  12.2 Handle bi-directional communication
  12.3 Store logs/session history for context continuity

13. Frontend (Streamlit UI)

  13.1 Layout:
    13.1.1 Left: Chat window
    13.1.2 Right: Image input and subject selector
  
  13.2 Show intermediate reasoning steps
  13.3 Add accessibility features (font size, contrast)

🚀 Phase 6: Deployment + QA (Week 5)

14. Deployment

    14.1 Host backend on EC2 or Hugging Face Spaces (for demo)
    14.2 Host frontend on Streamlit Cloud or EC2
    14.3 Secure endpoints via token auth

15. QA + Testing

    15.1 Test across subjects: Math, Science, Reading
    15.2 Simulate classroom use
    15.3 Evaluate for correctness, engagement, and helpfulness

16. Final Report

    16.1 Document architecture and stack
    16.2 Make demo video
    16.3 Describe limitations + future work (e.g., safety, bias)

