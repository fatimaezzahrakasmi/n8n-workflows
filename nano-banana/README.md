<img width="1252" height="536" alt="image" src="https://github.com/user-attachments/assets/ef46e71e-39e0-4bb8-a36e-8a2621facda5" />
This workflow allows users to input a simple description of a scene, and then automatically transforms that input into a cinematic, hyper-realistic prompt optimized for multiple text-to-image and text-to-video models (Flux, MidJourney, Stable Diffusion, Runway Gen-3 Alpha, Pika Labs).
The final generated prompt is sent to OpenRouter’s API (using Google Gemini 2.5 Flash image preview), which produces an AI-generated image.

🚀 Features

Interactive form submission for user input
Automatic prompt expansion using an LLM (Google Gemini via n8n LangChain nodes)
Enforced structured JSON output to keep responses consistent
HTTP request to OpenRouter for multimodal generation
Image returned as binary file for easy download or further use in workflows

📌 Workflow Steps:

1. On Form Submission
   Node: Form Trigger
   Purpose: Collects user input through a form.
   Field:
     Input → short description of the scene (e.g., “A baby eats a banana”).

--------------------------------------------------------------------------------------------------------------------------------------------------------------------
2. Basic LLM Chain

Node: Basic LLM Chain
Purpose: Expands the short user input into a detailed, cinematic description.
Connected to:
   Google Gemini Chat Model (as the LLM)
   Structured Output Parser (for clean JSON response).

-------------------------------------------------------------------------------------------------------------------------------------------------------------------
3. Google Gemini Chat Model (as the LLM)

<img width="660" height="687" alt="image" src="https://github.com/user-attachments/assets/675711eb-1cfd-4f82-b561-de7b1387ada9" />

📜 Prompt Template: 

TASK:  
You are an expert AI prompt designer. Your mission is to expand the short user input into a vivid, cinematic, hyper-realistic first-frame prompt. The output should be highly descriptive, visually immersive, and optimized for both text-to-image and text-to-video models, including Flux, MidJourney, Stable Diffusion, Runway Gen-3 Alpha, and Pika Labs.  

User Input: {{ $json.Input }}

FINAL INSTRUCTIONS:  
- The result must be fewer than 500 characters.  
- Return only one JSON object in the format:  
{ "prompt": "Generated text output here..." }

--------------------------------------------------------------------------------------------------------------------------------------------------------------------
4. Structured Output Parser
   for clean JSON response.

<img width="493" height="748" alt="image" src="https://github.com/user-attachments/assets/aeb4b7b7-e5f0-407f-984f-bb185cf715da" />

Output Parser JSON Schema:

{
   "type": "object",
   "properties": {
      "prompt": { "type": "string" }
   },
   "required": ["prompt"]
}

--------------------------------------------------------------------------------------------------------------------------------------------------------------------
5. HTTP Request (OpenRouter API)

<img width="682" height="535" alt="image" src="https://github.com/user-attachments/assets/082179b9-9fde-420b-9136-fd44b9fb684a" />

   Node: http Request
   
   Purpose: Sends the expanded prompt to OpenRouter to generate an image.
   
   Request body:

{
   "model": "google/gemini-2.5-flash-image-preview:free",
   "modalities": ["image", "text"],
   "messages" [
      {
         "role": "user",
         "content": "{{ $json.output.prompt }}"
      }
   ]
}
   
--------------------------------------------------------------------------------------------------------------------------------------------------------------------
6. Edit Fields

   Node: set
   
   Purpose: Extracts the AI-generated image URL and processes fields:
   
     - image_full → full image URL
     - image_raw → base64-encoded image
     - image_type → file type (e.g., png, jpeg)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------
7. Convert to File

   Node: n8n-nodes-base.convertToFile

   Purpose: Converts the raw base64 image into a downloadable binary file.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------
⚡ Setup Instructions

- Import this workflow JSON into your n8n instance.
- Configure credentials:
- Google Gemini (API)
- OpenRouter API
- Activate the workflow.
- Submit text descriptions via the form, and receive AI-generated images.
  
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
## License

This workflow is open-source and free to use. Modify it as needed for your personal or professional projects.
