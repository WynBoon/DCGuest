🧠 DCGuest_Agent — AI Code Builder
Overview
DCGuest_Agent is an autonomous AI system built using CrewAI, OpenAI, and Pinecone.
It plans, retrieves, and builds code automatically from a project specification — with minimal manual intervention.

Architecture
1. 📝 Planner Agent
Reads a project spec (local file or GitHub).

Decomposes it into structured tasks (tasks.json):

ID

Title

Description

Priority

Acceptance Criteria

2. 📚 Chunking + Embedding
Project files are recursively chunked into small parts.

Chunks are embedded using OpenAI text-embedding-ada-002.

Embeddings are stored in Pinecone (dc-guest index).

3. 🔍 Retriever
Takes task descriptions or queries.

Fetches the top relevant project chunks using Pinecone search.

4. 👷 Builder Agent
Reads tasks.json.

For each task:

Retrieves relevant project chunks.

Generates code using OpenAI models.

Saves output into generated_code_task_{ID}.txt.

Current Stack
Purpose	Technology
Agents	CrewAI
Embedding	OpenAI (text-embedding-ada-002)
Vector Database	Pinecone (new pinecone SDK)
Code Generation	OpenAI GPT Models
Development	Python 3.10+, tqdm, json

Setup
1. Install Requirements
bash
Copy
Edit
pip install crewai pinecone openai tqdm
2. Environment Variables
Set your API keys either through a .env file or directly in your scripts:

bash
Copy
Edit
# .env file example
OPENAI_API_KEY=your-openai-key
PINECONE_API_KEY=your-pinecone-key
Or hardcode them during local testing (not recommended for production).

Scripts
Script	Purpose
planner.py	Plan the project into tasks
chunk_project.py	Chunk project files into text chunks
embed_chunks_to_pinecone.py	Upload embeddings to Pinecone
retriever.py	Retrieve similar project chunks
builder.py	Build code from tasks

Future Enhancements
🛠️ Automatic GitHub commit of generated code

✅ Unit test generation based on Acceptance Criteria

🔍 Evaluation agent for code review

🚀 Multi-agent parallel building

Notes
Using the latest OpenAI SDK syntax (openai>=1.0.0).

Using the latest Pinecone SDK (pinecone package, not pinecone-client).

Retrieval system fully supports recursive subfolder scanning.
