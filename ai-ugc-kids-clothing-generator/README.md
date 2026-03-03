# 🧸 AI UGC Kids Clothing Ad Generator
### n8n + OpenAI Vision + Gemini Image (via OpenRouter)

---

## 🚀 Overview

**AI UGC Kids Clothing Ad Generator** is an automated AI workflow built with n8n that transforms a static product image of kids/baby clothing into a realistic, lifestyle-style advertising image.

The system:

- Accepts an uploaded product image and description  
- Analyzes the clothing details (brand, colors, style)  
- Generates a structured and optimized AI image prompt  
- Sends the prompt + reference image to Gemini Image model  
- Returns a newly generated UGC-style image of a child wearing the exact same outfit  

The workflow ensures that clothing details remain 100% accurate while placing the child in a natural, relatable environment suitable for modern e-commerce and social media marketing.

---

## 🎯 Problem It Solves

E-commerce brands often only have product-only images (flat lay or mannequin shots) but need:

- Lifestyle marketing visuals  
- UGC-style creatives  
- Social media ad images  
- Realistic product presentation  

This workflow automates that entire transformation process using AI.

---

## 🏗️ Workflow Architecture

### 1️⃣ Form Submission (n8n Trigger)

- Upload clothing image (.jpg)  
- Provide short product description  

---

### 2️⃣ Google Drive Upload

- Stores uploaded image  
- Generates public `webContentLink` for AI processing  

---

### 3️⃣ Image Analysis (OpenAI Vision)

**Model:** `chatgpt-4o-latest`

Extracts:

- Brand name (if visible)  
- Color scheme (hex + descriptive name)  
- Font style  
- Outfit style  
- Visual description  

Returns structured YAML output.

---

### 4️⃣ AI Prompt Engineering Agent

**Model:** `gpt-4.1-mini`

Custom Role:
> Kids Clothing Image Edit Prompt Builder  

The agent:

- Preserves clothing details exactly  
- Adds realistic camera cues  
- Adds lifestyle setting and mood  
- Produces a structured JSON output  

Example:

```json
{
  "image_prompt": "adorable 5-year-old child wearing the exact outfit from uploaded image..."
}
```

---

### 5️⃣ Image Generation (Gemini via OpenRouter)

**Model:** `google/gemini-2.5-flash-image`

Inputs:
Generated structured image prompt
Reference product image

Output:
Base64 encoded image

---

### 6️⃣ Image Extraction & Conversion

- Extract base64 image
- Detect MIME type
- Convert to binary
- Output final PNG file

---

### 🔄 Logical Flow

Form → Google Drive → Vision Analysis → Prompt Generator → Gemini Image → Image Conversion → Final Output

---

## ✨ Key Features

📤 File upload via form
🧠 Vision-based product analysis
🎯 Structured prompt engineering
🔒 JSON-enforced output format
🖼️ AI image generation with reference preservation
🔄 Automatic base64 extraction and conversion
📦 Ready-to-use marketing visuals

---

### 🛠️ Tech Stack

- n8n (Workflow Automation)
- OpenAI Vision API
-GPT-4.1-mini
-OpenRouter API
-Google Gemini 2.5 Flash Image
-Google Drive API

---

### 🔐 Required Credentials

To run this workflow, you need:

- OpenAI API Key
- OpenRouter API Key
- Google Drive OAuth2 Credentials
- HTTP Bearer Authentication

---

### 📦 Use Cases

- Kids fashion e-commerce
- Shopify product marketing
- Social media ad generation
- UGC-style content creation
- AI-powered creative automation

---

### 🎨 Output Style Characteristics

- Realistic child model (age adapted to clothing)
- Natural indoor/outdoor lighting
- Handheld phone-style framing
- Slight imperfections for authentic UGC feel
- Exact clothing preservation (colors, patterns, logos)

---

### 📈 Scalability Potential

This workflow can be extended into:

- SaaS product for clothing brands
- Bulk product image generator
- Automated ad creative generator
- Shopify integration
- AI marketing pipeline

---

### 👩‍💻 Author

Fatima Zohra
Master’s Student in Artificial Intelligence for Digital Economy
Focused on AI automation, prompt engineering, and intelligent workflow systems.

---

### 📄 License

This project is for educational and portfolio purposes.
Ensure compliance with API provider terms for commercial use.

