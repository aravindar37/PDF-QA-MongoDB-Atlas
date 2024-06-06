# PDF-QA-MongoDB-Atlas
RAG chatbot which can be used to do Q&amp;A on the context of a PDF document with MongoDB Atlas as Vector Database

# Step 1

Install Python 3.10 from https://www.python.org/downloads/
Ensure that $PATH is updated and shows python bin path
Verify the Python version
`python --version`

Optionally you can install Anaconda(https://www.anaconda.com/download/success) to visually manage environments, dependencies etc. Conda also comes preloaded with lot of packages for data engineering.

# Step 2

Create a virtual environment in Python and activate it.
`python -m venv /path/to/new/virtual/environment`
`source /path/to/new/virtual/environment/bin/activate`


# Step 3

Install langflow and pymongo(if not present) in the activated virtual environment.
`pip install langflow`
`pip list`
`pip install pymongo`

# Step 4

Open a new terminal and run Langflow:
`python -m langflow run`

# Step 5

Install Ollama from https://ollama.com/download.

# Step 6

Pull llama3:8b and nomic-embed-text models to Ollama. From command-line run:
`ollama pull llama3:8b`
`ollama pull nomic-embed-text`

# Step 7

Run llama3:8b from command-line
`ollama run llama3:8b`

For this activity, llama3:8b will be used for augmenting the output whereas nomic-embed-text will be used as the embedding model. Embedding models do not need to be run. It is available through the rest API (example below):
`curl http://localhost:11434/api/embeddings -d '{ "model": "nomic-embed-text",  "prompt": "action-packed movie"}'`

# Step 8

Create a MongoDB Atlas cluster.

Create a database 'vector_search' in the cluster and create a collection 'pdf_text'.
Open the search tab and create an index 'pdf' with following description: 
` {"fields":[{"numDimensions":768,"path":"embedding","similarity":"cosine","type": "vector" }]}`
Create a database and collection for storing chat message history.

# Step 9

Open langflow (http://127.0.0.1:7860/flows).
Click on New Project > Import from JSON > Upload rag_pdf_qa_mongodb_atlas.json

The flow would look like below:
![alt text](https://github.com/aravindar37/PDF-QA-MongoDB-Atlas/blob/main/langflow.png?raw=true)

Update the pdf file path in PyPDFLoader flow element.

Update the cluster URI in MongoDB Atlas flow element.

Update the connection string, database and collection name in MongoDBChatMessageHistory flow element.

# Step 10

Execute the Langflow flow by clicking on the lighting button on the left bottom
Once execution is complete, Click on the Chat icon on the left bottom corner to bring up the chatbot and chat.

Note: The PyPDFLoader can be replaced by FileLoader, CSFLoader, DirectoryLoader, SlackDirectoryLoader etc. to load documents from different sources.
