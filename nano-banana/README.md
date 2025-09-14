# Cinematic Scene Prompt → AI Image Workflow

<img width="1252" height="536" alt="image" src="https://github.com/user-attachments/assets/ef46e71e-39e0-4bb8-a36e-8a2621facda5" />

This n8n workflow allows users to input a **simple scene description**, which is then automatically expanded into a **cinematic, hyper-realistic prompt**.  
The optimized prompt is suitable for **text-to-image and text-to-video models** (Flux, MidJourney, Stable Diffusion, Runway Gen-3 Alpha, Pika Labs).  
Finally, the expanded prompt is sent to **OpenRouter’s API** (Google Gemini 2.5 Flash image preview), which generates an **AI image**.

---

## 🚀 Features

- 📝 **Interactive form submission** for user input  
- 🤖 **Automatic prompt expansion** using Google Gemini LLM  
- 📋 **Structured JSON output** for consistent responses  
- 🌐 **OpenRouter API integration** for multimodal generation  
- 📂 **Image returned as binary file** for download or use in other workflows  

---

## 📌 Workflow Steps

### On Form Submission
- **Node:** `Form Trigger`  
- **Purpose:** Collects user input through a form.  
- **Field:**  
  - `Input` → short description of the scene (e.g., *“A baby eats a banana”*).  

---

### Basic LLM Chain
- **Node:** `Basic LLM Chain`  
- **Purpose:** Expands the short user input into a detailed, cinematic description.  
- **Connected to:**  
  - `Google Gemini Chat Model` (LLM)  
  - `Structured Output Parser` (for clean JSON response).  

<img width="660" height="687" alt="image" src="https://github.com/user-attachments/assets/675711eb-1cfd-4f82-b561-de7b1387ada9" />

**Prompt Template:**  

TASK:
You are an expert AI prompt designer. Your mission is to expand the short user input into a vivid, cinematic, hyper-realistic first-frame prompt. The output should be highly descriptive, visually immersive, and optimized for both text-to-image and text-to-video models, including Flux, MidJourney, Stable Diffusion, Runway Gen-3 Alpha, and Pika Labs.

User Input: {{ $json.Input }}

FINAL INSTRUCTIONS:

- The result must be fewer than 500 characters.
- Return only one JSON object in the format:
- { "prompt": "Generated text output here..." }

---

## Structured Output Parser
- **Purpose:** Ensures clean and valid JSON response.  
- **Schema:**

{
  "type": "object",
  "properties": {
    "prompt": { "type": "string" }
  },
  "required": ["prompt"]
}

<img width="493" height="748" alt="image" src="https://github.com/user-attachments/assets/aeb4b7b7-e5f0-407f-984f-bb185cf715da" />

---

### HTTP Request → OpenRouter API
Node: HTTP Request

Purpose: Sends the expanded prompt to OpenRouter for image generation.

Request Body:

json
Copy code
{
  "model": "google/gemini-2.5-flash-image-preview",
  "modalities": ["image", "text"],
  "messages": [
    {
      "role": "user",
      "content": "{{ $json.output.prompt }}"
    }
  ]
}

<img width="680" height="677" alt="image" src="https://github.com/user-attachments/assets/2ef45a52-5e1e-43c1-a33b-d1a2995fb60d" />


---

### Edit Fields
Node: Set

Purpose: Extracts and processes output fields:
- image_full → full image URL
- image_raw → base64-encoded image
- image_type → file type (e.g., png, jpeg)

---

### Convert to File
Node: Convert to File

Purpose: Converts base64-encoded image into a downloadable binary file.

---

## ⚡ Setup Instructions
- Import this workflow JSON into your n8n instance.
- Configure credentials:
    - Google Gemini (API)
    - OpenRouter API
- Activate the workflow.
- Submit text descriptions via the form.
- Receive AI-generated cinematic images automatically.

# Example Input → Output
Input:

A baby eats a banana

Expanded Prompt (LLM):

A cinematic close-up of a baby with soft golden lighting, sitting in a high chair, joyfully eating a ripe banana. Ultra-realistic textures, detailed facial expressions, professional studio photography style.

Output:

🎨 Hyper-realistic AI image returned as both URL + downloadable file

---
Youtup Video:
https://youtu.be/b4Kd7EvlnL4

### 📜 License
This workflow is open-source and free to use.
Feel free to modify it for your personal or professional projects.

  

