🧸 AI UGC Kids Clothing Ad Generator (n8n + OpenRouter + Gemini Image)
📌 Overview

### This workflow automatically generates realistic UGC-style advertising images for kids' clothing.

## A user uploads:

A product image (kids/baby clothes)

A short description

The system:

Uploads the image to Google Drive

Analyzes the product visually (brand, colors, style, etc.)

Generates a precise image prompt that preserves the exact clothing details

Sends the prompt + reference image to Gemini Image (via OpenRouter)

Returns a newly generated image of a child wearing the exact same outfit in a natural lifestyle setting

The result: authentic, ad-ready lifestyle visuals while preserving product accuracy.

🚀 Features

📤 Form-based image upload

☁️ Google Drive integration

🧠 AI image analysis (product or character detection)

🎯 Structured prompt generation (JSON enforced)

🖼️ Image generation using google/gemini-2.5-flash-image

🔄 Automatic base64 extraction and file conversion

📦 Ready for UGC-style marketing use

🏗️ Workflow Architecture
1️⃣ Form Trigger

Collects:

Image description

Product image (.jpg)

Node: On form submission

2️⃣ Upload to Google Drive

Stores uploaded image

Returns webContentLink for AI processing

Node: Upload file

3️⃣ Image Analysis (OpenAI Vision)

Model: chatgpt-4o-latest

Detects whether the image shows:

A product

A character

Or both

Returns structured YAML:

Brand name

Color scheme (hex + name)

Font style

Outfit style

Visual description

Node: Analyze image

4️⃣ AI Prompt Engineering Agent

Uses:

gpt-4.1-mini

Structured Output Parser (JSON enforced)

Role:

Kids Clothing Image Edit Prompt Builder

The agent:

Keeps clothes 100% identical

Adds realistic camera cues

Adds setting and mood

Generates ≤120 word image prompt

Returns clean JSON:

{
  "image_prompt": "..."
}

Nodes:

OpenAI Chat Model

Image Prompt Generator

Structured Output Parser

5️⃣ Image Generation (Gemini via OpenRouter)

Endpoint:

https://openrouter.ai/api/v1/chat/completions

Model:

google/gemini-2.5-flash-image

Inputs:

Generated image prompt

Reference image URL

Output:

Base64 image

Node: HTTP Request

6️⃣ Image Extraction & Conversion

Extract base64

Detect MIME type

Convert to binary file

Output final PNG

Nodes:

Edit Fields

Convert to File

🔐 Required Credentials

You must configure:

✅ OpenAI API

✅ OpenRouter API

✅ Google Drive OAuth2

✅ HTTP Bearer Auth (for OpenRouter)

🧩 How It Works (Flow Summary)
Form → Google Drive Upload → Vision Analysis → Prompt Generator 
→ Gemini Image Generation → Base64 Extraction → PNG Output
🎯 Use Cases

Kids fashion e-commerce

UGC-style ad generation

Shopify product marketing

Social media creatives

Product visualization at scale

⚙️ Customization Options

You can easily modify:

Style realism level

Background type

Camera aesthetics

Age range

Ethnicity diversity

Ad mood (playful, premium, cozy, etc.)

📦 Output Example

Final result:

A realistic child wearing the exact uploaded outfit

Natural lighting

Slight imperfections (authentic feel)

Lifestyle setting

Ad-ready visual
