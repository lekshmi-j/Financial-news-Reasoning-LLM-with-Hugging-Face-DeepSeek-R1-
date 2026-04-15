# 🧠 Reasoning LLM with Hugging Face (DeepSeek-R1)

This project demonstrates how to run a reasoning-capable Large Language Model (LLM) locally using Hugging Face Transformers with 4-bit quantization, and apply it to analyze real-world financial news data.

It also includes an interactive Gradio interface to explore model reasoning and outputs.

---

## 🚀 Features

- Uses DeepSeek-R1 Distilled (1.5B) reasoning model
- Efficient inference with 4-bit quantization (bitsandbytes)
- Processes real-world dataset from Hugging Face
- Extracts reasoning (<think>) and final output separately
- Interactive UI using Gradio
- Supports GPU acceleration

---

## 🧩 Tech Stack

- Transformers (Hugging Face)
- PyTorch
- BitsAndBytes (4-bit quantization)
- Datasets (Hugging Face)
- Gradio

---

## 📂 Dataset

Dataset used:
KrossKinetic/all_news_finance_jsonl

Each sample contains:
- Title
- Description

These are combined into:

Title: <title>
Description: <description>

---

## ⚙️ Installation

Install required dependencies:

pip install transformers accelerate bitsandbytes torch datasets gradio

---

## 🔐 Hugging Face Login

from huggingface_hub import notebook_login
notebook_login()

---

## 🤖 Model

Model used:
deepseek-ai/DeepSeek-R1-Distill-Qwen-1.5B

This model supports reasoning via <think>...</think> tokens.

---

## ⚡ Model Loading (4-bit Quantization)

from transformers import AutoModelForCausalLM, BitsAndBytesConfig

quantization_config = BitsAndBytesConfig(load_in_4bit=True)

model = AutoModelForCausalLM.from_pretrained(
    model_id,
    torch_dtype="auto",
    device_map="auto",
    quantization_config=quantization_config
)

---

## 🧪 Prompt Format

The model follows a structured chat format:

<|im_start|>user
Your question here
<|im_end|>
<|im_start|>assistant
<think>

The output includes:
- Reasoning inside <think>...</think>
- Final answer after </think>

---

## 🧠 Output Parsing

You can separate reasoning and final output using a helper function:

def format_model_output(output):
    reason = ...
    final_output = ...
    return reason, final_output

---

## 📰 News Processing Pipeline

1. Load dataset from Hugging Face
2. Combine title and description
3. Sample random news entries
4. Pass to LLM for reasoning and analysis

---

## 🎛️ Gradio Interface

The UI allows:
- Fetching random news
- Analyzing news with the LLM

Example:

gr.Interface(
    fn=analyze_news_gradio,
    inputs="text",
    outputs="text"
)

---

## 💡 Use Cases

- Financial news analysis
- Sentiment reasoning
- Explain complex topics
- Chain-of-thought reasoning exploration
- Building reasoning-based AI applications

---

## ⚠️ Notes

- GPU is recommended for better performance
- 4-bit quantization significantly reduces memory usage
- Adjust max_new_tokens based on your requirements

---

## 📈 Future Improvements

- Add streaming output
- Fine-tune on domain-specific datasets
- Add evaluation metrics
- Deploy as a web app or API
- Integrate with vector databases (RAG)

---

## 🙌 Acknowledgements

- Hugging Face
- DeepSeek AI
- BitsAndBytes
