# Building an AI Chatbot tailored towards UIUC students

This ML-ai project is to develop an AI-chatbot tailored for UIUC students by training a preexisting model. There will be a frontend web component with a simple chat-response feature to provide students with info about classes, how to do stuff around campus, etc.

## Plan

1. Clearly define Objective(s)
    * University chatbot should answer FAQ's, provide campus info, assist with course enrollment, offer resources, and provide general guidance.
    * extra: Chatbot could be familiar with specific UIUC culture (ex. jokes about hidden Dairy Queen at Altgeld)
2. Select an Open Source framework
    * Probably Llama, Rasa
3. Data collection and preprocessing
    * Historical chat logs, reddit maybe, University sites, any other UIUC database.
4. Model training
    * Define chatbot intents, entities, and dialogue flow. Train model using preprocessed data, fine tuning model.
5. Integrate UIUC resources
    * Connect to University sites, databases, campus maps, event calendars, etc.
6. UI development
7. Testing and Iteration based on feedback from users.
8. Maintenance and updates based on newer information
9. DOCUMENTATION (throughout entire process)


## Tools

Entirely software
- Frontend for website: React, Svelte, Vue
- Choice of Model: LLama 2, maybe gpt
- Frameworks: Python, LLamaindex, Langchain, possiblly Rasa
- Replicate (if needed)

## Cost considerations
- No explicit hardware required
- Hosting our website or custom language model (use [replicate](https://replicate.com/) for running model on cloud)
- Premium services for accessing certain API keys
- Roughly **$100** for hosting purposes, **$50** for premium services for a total of **$150** (this would be per month, but we don't necessarily need these services for many months).
  
## Resources

Some videos creating ai chatbots with custom knowledge base
- https://youtu.be/sUSw9MaPm2M
- https://youtu.be/iGZ0cV-SRLI
