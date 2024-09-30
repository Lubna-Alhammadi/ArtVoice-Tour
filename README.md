
ArtVoice Tour: Virtual Art Museum with Image and Text-Based Art Retrieval
Project Overview
The ArtVoice Tour is an interactive Virtual Art Museum, where users can explore famous artworks by:

Uploading an image of an artwork, or
Entering a description of a painting.
The system will provide:

The best matching artwork based on the uploaded image or description.
A detailed text description of the artwork, including its title and story.
A voice narration of the story, available in both English and Arabic.
Expected Outputs
Image Matching: When an image is uploaded, the system retrieves the best matching painting based on visual similarity.
Description Matching: When a description is entered, the system performs a semantic similarity search and returns the closest matching artwork.
Voice Narration: The story behind each artwork is narrated in either English or Arabic based on the user’s language preference.
Model Choices and Pipeline Explanations
CLIP Model (openai/clip-vit-base-patch32):

Why this model? CLIP is ideal for image-to-image matching because it generates rich embeddings for images. This model is used to compare the uploaded image with the stored images of famous artworks in the dataset.
Pipeline Role: CLIP processes the uploaded image and compares it to the dataset images, calculating similarity scores. The system then selects the best matching artwork based on these visual features.
Sentence-Transformer (sentence-transformers/all-MiniLM-L6-v2):

Why this model? MiniLM is optimized for semantic similarity and provides fast and efficient sentence embeddings. It’s perfect for comparing user-provided text descriptions with the artwork descriptions in the dataset.
Pipeline Role: This model encodes both the input description and the dataset descriptions into vectors. It then computes cosine similarity to find the closest match based on textual similarity.
Text-to-Speech (TTS) Model (kakao-enterprise/vits-ljs):

Why this model? VITS-LJS is chosen for its high-quality, natural-sounding English speech synthesis. It provides an engaging experience for English-speaking users who want to listen to the story behind the artwork.
Pipeline Role: The English story behind the artwork is converted into audio using this model, delivering a smooth and human-like narration.
Translation Models (Helsinki-NLP/opus-mt-ar-en and opus-mt-en-ar):

Why these models? The Helsinki-NLP models are renowned for their accuracy in translating between Arabic and English, making them the best choice for handling multilingual input and output. This ensures the system handles both English and Arabic seamlessly.
Pipeline Role: If a user provides input in Arabic, the opus-mt-ar-en model translates it to English for comparison. Similarly, the opus-mt-en-ar model translates the English output into Arabic for Arabic-speaking users.
Special Measures for Arabic Language Support
Arabic Text-to-Speech (TTS):

Why gTTS? Although MBZUAI/speecht5_tts_clartts_ar is a state-of-the-art model for Arabic TTS, it was not selected for this project due to several reasons:
Pronunciation issues: The model had difficulty correctly pronouncing city names and artist names, which is crucial for maintaining accuracy in a museum setting.
Silence periods: During testing, the model generated long periods of silence between words and sentences, which disrupted the flow of the narration and reduced the overall user experience.
Slower performance: gTTS is faster in generating audio output, improving the responsiveness of the application and providing a smoother user experience.
Simpler alternative: gTTS provides reliable, faster, high-quality Arabic speech synthesis and is easier to integrate, making it a more practical solution for this project.
How it works: After translation to Arabic, gTTS generates speech in Modern Standard Arabic, ensuring that Arabic-speaking users can enjoy clear, accurate, and fast narration of the artwork stories.
Language Detection:

The system automatically detects whether the input is in English or Arabic using language detection. This ensures seamless processing for users without requiring them to manually select their language.
Translation Pipeline:

The system incorporates both Arabic-to-English and English-to-Arabic translation models. This ensures users can interact with the system in Arabic, and receive both text and audio outputs in Arabic if preferred.
Right-to-Left (RTL) Text Display:

Special care has been taken to display Arabic text in right-to-left (RTL) format. HTML and CSS styling ensure that Arabic text is presented clearly and legibly, maintaining a user-friendly experience for Arabic-speaking users.
Usage
Upload an image of a famous artwork or enter a description of the painting.
Select the desired language for narration (English or Arabic).
View the best matching artwork, read its description, and listen to the story behind it.
Hugging Face Space
The project is hosted on Hugging Face Spaces and can be accessed here:

ArtVoice Tour on Hugging Face
