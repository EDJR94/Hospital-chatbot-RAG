## 🤖 Langchain hospital chatbot
The overall workflow is as follows:

<img src='workflow.avif'>

## Neo4j Aura DB
Graph databases, such as Neo4j, are databases designed to represent and process data stored as a graph. Graph data consists of nodes, edges or relationships, and properties. Nodes represent entities, relationships connect entities, and properties provide additional metadata about nodes and relationships.

The relationships in this hospital is as follows:
![graph_relationships](https://github.com/user-attachments/assets/5222ffca-65a1-424d-9073-f33146ec921e)

This diagram shows you all of the nodes and relationships in the hospital system data. One useful way to think about this flowchart is to start with the Patient node and follow the relationships. A Patient has a visit at a hospital, and the hospital employs a physician to treat the visit which is covered by an insurance payer.


## Demo
![Demo](./langchain_rag_chatbot_demo.gif)

### 🛠️ How to run

Create a `.env` file in the root directory and add the following environment variables:

```.env
NEO4J_URI=<YOUR_NEO4J_URI>
NEO4J_USERNAME=<YOUR_NEO4J_USERNAME>
NEO4J_PASSWORD=<YOUR_NEO4J_PASSWORD>

OPENAI_API_KEY=<YOUR_OPENAI_API_KEY>
GOOGLE_API_KEY=<YOUR_OPENAI_API_KEY>
GOOGLE_EMBEDDING_MODEL=models/embedding-001

HOSPITALS_CSV_PATH=https://raw.githubusercontent.com/hfhoffman1144/langchain_neo4j_rag_app/main/data/hospitals.csv
PAYERS_CSV_PATH=https://raw.githubusercontent.com/hfhoffman1144/langchain_neo4j_rag_app/main/data/payers.csv
PHYSICIANS_CSV_PATH=https://raw.githubusercontent.com/hfhoffman1144/langchain_neo4j_rag_app/main/data/physicians.csv
PATIENTS_CSV_PATH=https://raw.githubusercontent.com/hfhoffman1144/langchain_neo4j_rag_app/main/data/patients.csv
VISITS_CSV_PATH=https://raw.githubusercontent.com/hfhoffman1144/langchain_neo4j_rag_app/main/data/visits.csv
REVIEWS_CSV_PATH=https://raw.githubusercontent.com/hfhoffman1144/langchain_neo4j_rag_app/main/data/reviews.csv

CHATBOT_URL=http://host.docker.internal:8000/hospital-rag-agent

HOSPITAL_AGENT_MODEL=gpt-4o-mini
HOSPITAL_CYPHER_MODEL=gpt-4o-mini
HOSPITAL_QA_MODEL=gpt-4o-mini

LANGCHAIN_TRACING_V2=true
LANGCHAIN_API_KEY=<YOUR_OPENAI_API_KEY>
PROJECT_NAME=neo4j-chatbot
LANGCHAIN_ENDPOINT=https://api.smith.langchain.com
```

The three `NEO4J_` variables are used to connect to your Neo4j AuraDB instance. Follow the directions [here](https://neo4j.com/cloud/platform/aura-graph-database/?ref=docs-nav-get-started) to create a free instance.

The chatbot uses OpenAI/Gemini LLMs, so you'll need to create an [OpenAI API key](https://realpython.com/generate-images-with-dalle-openai-api/#get-your-openai-api-key) and store it as `OPENAI_API_KEY`.

To host the API, go to `chatbot_api/src` then run `uvicorn main:app --host 0.0.0.0 --port 8000`

To host the Streamlit UI, go to `chatbot_frontend/src` then run `streamlit run main.py`
