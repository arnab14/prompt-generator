# **AI Prompt Generator Web Application**

## **Description**

The AI Prompt Generator is a web application designed to help users create effective and tailored prompts for various AI models (like text or image generators). Users can input parameters such as topic, style, desired output format, constraints, and things to avoid, and the application leverages a Large Language Model (LLM) via the Google Gemini API to generate a high-quality prompt.

This project aims to solve the "blank page" problem when interacting with AI, making it easier to get desired results by crafting better initial instructions.

## **Features**

* **Dynamic Prompt Generation:** Uses Google Gemini (via LangChain) to generate prompts based on user inputs.  
* **User-Friendly Interface:** Simple HTML and JavaScript frontend for easy interaction, styled with Tailwind CSS.  
* **Customizable Inputs:**  
  * Prompt Type (e.g., General, Email Draft, Code Snippet)  
  * Target Model Type (Text, Image, Code)  
  * Topic/Subject  
  * Desired Style/Tone  
  * Desired Output Format (e.g., Paragraph, Bullet points, JSON)  
  * Desired Complexity (Default, Simple, Detailed)  
  * Constraints/Specific Instructions  
  * Things to Avoid (Negative Prompting)  
* **Backend Logic:** Python Flask server handles API requests and LangChain integration.  
* **Enhanced Meta-Prompting:** The backend uses a sophisticated meta-prompt to guide the LLM in generating high-quality, safe, and relevant prompts, including self-correction and hallucination avoidance techniques.  
* **Prompt History:** Saves recently generated prompts in the browser's local storage for easy reuse.  
* **Safety & Security:**  
  * API Key secured via .env file.  
  * Rate limiting on the API endpoint (Flask-Limiter).  
  * Basic input validation (e.g., length checks).  
  * Content moderation using Google Gemini's built-in safety settings.

## **Tech Stack**

* **Frontend:** HTML, Tailwind CSS, JavaScript (Fetch API)  
* **Backend:** Python, Flask, Flask-CORS, Flask-Limiter  
* **AI Integration:**  
  * LangChain (PromptTemplate, ChatGoogleGenerativeAI, StrOutputParser)  
  * Google Gemini API (gemini-2.5-pro-exp-03-25)  
  * google-generativeai (for safety settings)  
* **Environment Management:** python-dotenv

## **Setup and Installation**

1. **Clone the repository (if applicable) or create project files.**  
   \# If you have a git repo:  
   \# git clone \<repository-url\>  
   \# cd \<repository-name\>

2. **Create and activate a Python virtual environment:**  
   * On macOS/Linux:  
     python3 \-m venv venv  
     source venv/bin/activate

   * On Windows:  
     python \-m venv venv  
     .\\venv\\Scripts\\activate

3. Install dependencies:  
   Make sure you have a requirements.txt file with the following content:  
   Flask  
   langchain  
   langchain-google-genai  
   python-dotenv  
   Flask-CORS  
   Flask-Limiter  
   google-generativeai

   Then run:  
   pip install \-r requirements.txt

4. **Set up Environment Variables:**  
   * Create a file named .env in the root directory of the project.  
   * Add your Google AI Studio API key to the .env file:  
     GOOGLE\_API\_KEY="YOUR\_GEMINI\_API\_KEY"

   * Replace "YOUR\_GEMINI\_API\_KEY" with your actual API key.

## **How to Run**

1. **Ensure your virtual environment is activated.**  
2. Start the Flask backend server:  
   From the project's root directory, run:  
   python app.py

   The server should start, typically on http://127.0.0.1:5000/.  
3. **Open the frontend:**  
   * Navigate to the directory containing index.html.  
   * Open index.html directly in your web browser (e.g., by double-clicking it).  
4. **Use the Application:**  
   * Fill in the form fields in the browser.  
   * Click "Generate Prompt".  
   * The generated prompt will appear, and it will be added to the history.

## **API Endpoint**

* POST /generate-prompt: Accepts JSON payload with user inputs and returns the generated prompt.  
  * **Request Body (JSON example):**  
    {  
        "prompt\_type": "email\_draft",  
        "topic": "Follow up after a networking event",  
        "style": "Professional and friendly",  
        "target\_model": "text",  
        "constraints": "Keep it under 150 words, mention our shared interest in AI.",  
        "output\_format": "Paragraph",  
        "negative\_prompt": "Avoid overly casual language",  
        "complexity": "default"  
    }

  * **Success Response (JSON example):**  
    {  
        "generated\_prompt": "Draft a professional and friendly email to follow up with someone you met at a networking event. The email should be about your shared interest in AI and be under 150 words. Do not use overly casual language."  
    }

  * **Error Response (JSON example):**  
    {  
        "error": "Topic/Subject is required."  
    }

## **Future Enhancements (Potential)**

* Transition to a native mobile application (e.g., using Flutter and Firebase).  
* Implement user accounts for personalized history and settings.  
* Advanced prompt management features (saving, tagging, sharing).  
* More sophisticated content moderation and input analysis.