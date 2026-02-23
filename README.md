# Instructions-for-me
You are a data ingestion assistant for a Retrieval Augmented Generation (RAG) system.

The system processes PDF, CSV, and XLSX files and converts them into text chunks for embeddings.

When a file is uploaded:

1. Detect the file type.

2. If the file is a PDF:
   
   - Use the existing document chunking process (paragraph or section based).

3. If the file is a CSV or XLSX:
   
   - Count the total number of rows (for XLSX count rows per sheet).
   
   - Choose chunking strategy based on dataset size:
     
     • If rows ≤ 20,000:
     Treat each row as one chunk.
     
     • If rows between 20,001 and 100,000:
     Group 10–20 rows per chunk.
     
     • If rows > 100,000:
     Group 25–50 rows per chunk.

4. Convert each row or row group into readable text including column names.

5. If XLSX:
   
   - Process each sheet separately.
   - Include sheet name in the chunk text.

6. Ensure chunks contain complete records and do not break rows.

7. Do not summarize, analyze, or remove values.
   Only convert structured data into clean text chunks ready for embeddings.



-------------------------------------


Build Agentic RAG Project
Build a complete production-style Agentic RAG system using Python.
The system must use an agent architecture where the LLM decides which tool to use and when to rewrite queries before retrieval.
Tech Requirements
Use FAISS for vector storage with multiple indexes
Use LangChain or LangGraph for agent orchestration
Use a modern LLM API (Groq or OpenAI compatible)
Build a simple chat UI using Streamlit
Modular Python project structure
Functional Requirements
Implement an Agentic RAG system with the following capabilities:
1️⃣ Multiple Knowledge Bases
Create three FAISS indexes:
research documents
study notes
FAQs
Each index should be loaded from separate folders.
2️⃣ Retrieval Tools
Expose each FAISS index as a separate tool:
search_research_db
search_notes_db
search_faq_db
The agent must dynamically choose which tool to use based on the query.
3️⃣ Query Rewriter Tool
Implement a query rewriting tool that reformulates vague or conversational queries into clear semantic search queries before retrieval.
Prompt should instruct the LLM to:
keep original intent
add specificity
optimize for semantic search
4️⃣ Agent Decision Loop
The agent must follow a reasoning loop:
Think → Decide Tool → Act → Observe → Answer
The agent should:
decide when to rewrite queries
decide which knowledge base to search
generate final response using retrieved context
5️⃣ Response Generation
Combine retrieved context with LLM reasoning to generate answers.
Include:
clear explanation
sources used
concise formatting
6️⃣ User Interface
Build a chat interface where users can:
ask questions
see responses
optionally see which tool was used
Project Structure
Create clean modular files:
app.py (Streamlit UI)
agent.py (agent setup)
tools.py (tool definitions)
vectorstore.py (FAISS setup)
prompts.py (all prompts)
config.py
data folders
requirements.txt
Non Functional Requirements
Write clean readable code
Add comments explaining logic
Make code runnable locally
Include logging of agent decisions
Handle errors gracefully
