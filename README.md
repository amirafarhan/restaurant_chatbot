Restaurant Menu RAG Chatbot 🍽️🤖

A Retrieval-Augmented Generation (RAG) chatbot built with LangChain, ChromaDB, Hugging Face Embeddings, and Qwen LLM to answer restaurant menu-related questions intelligently.

The chatbot loads menu data from a JSON file, converts it into vector embeddings, stores them in ChromaDB, and uses semantic search + LLM generation to answer user questions about menu items, categories, prices, and descriptions.

🚀 Features
Load menu data from a JSON file
Create structured documents using LangChain
Generate embeddings with Sentence Transformers
Store vectors in ChromaDB
Semantic similarity search for menu retrieval
Category-level and item-level retrieval
Interactive chatbot interface
Context-aware responses using RetrievalQA
Lightweight local LLM using Qwen2.5
🛠️ Tech Stack
Python
LangChain
ChromaDB
Hugging Face Transformers
Sentence Transformers
Qwen2.5 Instruct Model
📂 Project Structure
project/
│
├── menu.json                # Restaurant menu dataset
├── app.py                   # Main chatbot application
├── chroma_menu_db/          # Persisted Chroma vector database
├── requirements.txt         # Project dependencies
└── README.md                # Project documentation
📦 Installation
1. Clone the repository
git clone https://github.com/your-username/restaurant-rag-chatbot.git
cd restaurant-rag-chatbot
2. Create virtual environment
Windows
python -m venv venv
venv\Scripts\activate
Mac/Linux
python3 -m venv venv
source venv/bin/activate
3. Install dependencies
pip install -r requirements.txt

Or install manually:

pip install langchain langchain-community langchain-chroma langchain-huggingface chromadb sentence-transformers transformers accelerate
📄 Example menu.json
{
  "Drinks": [
    {
      "name": "Coca Cola",
      "description": "Cold soft drink",
      "price": 2.5
    },
    {
      "name": "Orange Juice",
      "description": "Fresh natural juice",
      "price": 4
    }
  ],
  "Pizza": [
    {
      "name": "Margherita",
      "description": "Cheese pizza with tomato sauce",
      "price": 12
    }
  ]
}
▶️ Run the Project
python app.py
💬 Example Usage
Ask about the menu: what drinks do you have?
Example Response
Bot:
- Coca Cola: Cold soft drink - $2.5
- Orange Juice: Fresh natural juice - $4
🧠 How It Works
1. Load Menu Data

The application reads menu items from menu.json.

2. Create Documents

Each menu item is converted into a LangChain Document.

Example:

Document(
    page_content="""
    Category: Drinks
    Name: Coca Cola
    Description: Cold soft drink
    Price: 2.5
    """
)
3. Generate Embeddings

Using:

sentence-transformers/all-MiniLM-L6-v2

to convert text into semantic vectors.

4. Store in ChromaDB

Embeddings are stored locally in:

./chroma_menu_db
5. Retrieve Relevant Documents

The retriever performs semantic similarity search:

retriever = vectorstore.as_retriever(
    search_type="similarity",
    search_kwargs={"k": 10}
)
6. Generate AI Response

The retrieved context is sent to the Qwen model to generate answers.

🤖 Model Used
Embedding Model
sentence-transformers/all-MiniLM-L6-v2
Language Model
Qwen/Qwen2.5-0.5B-Instruct
📌 Prompt Engineering

The chatbot uses a custom prompt template:

You are a helpful restaurant menu assistant.

Use ONLY the menu context below to answer questions.

This ensures responses stay grounded in the menu data.

🔍 Retrieval Types

The project creates:

Item-level documents
Category-level documents

This improves semantic retrieval for:

Specific item questions
Category-wide queries
📈 Future Improvements
Add Streamlit or Gradio UI
Add multilingual support
Add voice assistant integration
Use larger LLMs for better responses
Deploy with Docker
Add filtering by price/category
Support online ordering
🧪 Example Questions
What pizzas do you have?
How much is Coca Cola?
Tell me about Margherita pizza
Do you have burgers?
⚠️ Notes
The model runs locally and may require a good CPU/GPU.
First run may take time because models are downloaded automatically.
ChromaDB is recreated each time the script runs.
❤️ Acknowledgments

Built using:

LangChain
Hugging Face
ChromaDB
Sentence Transformers
Qwen Models
📜 License

This project is licensed under the MIT License.

👩‍💻 Author

Developed by Amira Mohamed 🚀
