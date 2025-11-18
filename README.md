# project-portfolio
Portfolio of chatbot projects

🧠 # Project Description

This project implements an AI-powered WhatsApp chatbot using Infobip as the messaging provider, Gemini as the language model, and a vector-embedding layer to add contextual knowledge.
The server runs locally and is exposed to the internet through ngrok.

The system receives WhatsApp messages, retrieves relevant information via semantic search, and automatically sends back context-aware responses.

⚙️ # System Architecture
WhatsApp → Infobip → Webhook (ngrok) → Local Server
         → Vector Search → Gemini → Infobip → User

🚀 # Workflow (Step-by-Step)
1. # Webhook Implementation

I created an HTTP endpoint (webhook) in Python to receive inbound WhatsApp messages from Infobip.
This endpoint processes the JSON payload sent by Infobip whenever a user sends a message.

2. # Exposing the Local Server with ngrok

Since the project runs locally, I used ngrok to create a public URL:

ngrok http 8000


This ngrok URL acts as the callback endpoint for Infobip.

3. # Infobip WhatsApp Webhook Configuration

Inside the Infobip portal, I added the ngrok URL as the:

Webhook for Inbound Messages

This allows Infobip to forward every WhatsApp message directly to my local server.

4. # Inbound Message Processing

When the webhook receives a new message:

I extract the sender’s phone number

I retrieve the text content

I format the request to pass it into the AI pipeline

5. # Creating Kambista Knowledge Embeddings

Before integrating the chatbot, I converted internal Kambista documentation into vector embeddings to enable semantic search.

This included:

Generating embeddings for all content

Storing the vectors

Implementing cosine similarity search

This lets the chatbot respond using real company information.

6. # Retrieval-Augmented Generation (RAG)

When a user sends a message:

The server performs vector similarity search to fetch the most relevant knowledge snippets

It builds an enhanced prompt containing:

The user’s message

The retrieved context

System instructions / constraints

7. # Response Generation with Gemini

The enriched prompt is sent to the Gemini model, which generates a coherent and context-aware reply aligned with Kambista’s information.

8. # Sending the Response Back Through Infobip

Finally, the generated response is sent back to the user via the Infobip WhatsApp API, completing the full conversational loop.
