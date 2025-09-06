# Baby Podcast Workflow

<img width="1629" height="651" alt="image" src="https://github.com/user-attachments/assets/b657cfd0-1205-4bb9-b32d-e6a36d6c5525" />

This n8n workflow generates a short **baby podcast video**. It combines:
- A form for user input,
- AI-generated text (podcast script),
- AI-generated image (baby podcaster),
- AI text-to-speech (audio),
- Video generation with Hedra API,
- And finally delivers the result via Telegram.

---

## 🎬 Workflow Overview

1. **Form Trigger**  
   - Users fill out a form selecting:
     - Baby Ethnicity  
     - Baby Hairstyle  
     - Topic of Discussion  
     - Extras (optional, e.g., "wearing a hat")  

2. **Podcast Script (Text Generation)**  
   - Uses OpenRouter + LLM Chain to create a **Joe Rogan style monologue** (500 characters).  
   - Text is then passed to ElevenLabs API to generate **audio speech**.  

3. **Image Generation (Baby Podcaster)**  
   - A second LLM Chain creates a prompt for Runware AI.  
   - Runware generates an image of the baby podcast host.  
   - The image is uploaded as an asset in Hedra.  

4. **Audio Upload**  
   - Audio file from ElevenLabs is uploaded to Hedra as an audio asset.  

5. **Video Generation (Hedra)**  
   - Hedra combines the **image** + **audio** into a 5-second **podcast-style baby video**.  
   - Includes studio setting, podcast mic, and warm lighting.  

6. **Delivery**  
   - The final video is fetched and automatically sent to a Telegram chat.  

---

## 🔑 Required Credentials

- **OpenRouter API** – for text generation.  
- **ElevenLabs API** – for text-to-speech (baby podcast audio).  
- **Runware API** – for AI image generation.  
- **Hedra API** – for asset creation and final video generation.  
- **Telegram Bot API** – for sending the finished video.  

---

## 🛠️ Setup Instructions

1. Import this workflow into n8n.  
2. Add the required API credentials in **n8n Credentials Manager**.  
3. Configure:
   - Form Trigger URL → share with users.  
   - Telegram `chatId` → replace with your target chat ID.  
4. Activate workflow.  

---

## ✨ Example Output

- **Form Input:**  
  - Ethnicity: *Asian*  
  - Hairstyle: *Curly*  
  - Topic: *Artificial Intelligence*  
  - Extras: *Wearing a hat*  

- **Output:**  
  - A **500-character podcast rant** in Joe Rogan’s style.  
  - A **cute AI baby image** with curly hair wearing headphones.  
  - A **generated 5-second podcast video**.  
  - The video is **sent via Telegram**.  

---

## 📌 Notes

- Processing takes ~1–2 minutes due to Hedra asset generation & wait nodes.  
- You can adjust video **duration, resolution, or prompts** inside the workflow.  
- Use the sticky notes inside n8n to keep the workflow organized.

