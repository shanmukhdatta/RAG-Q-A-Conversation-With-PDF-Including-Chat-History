# 🧠 Conversational RAG with PDF Intelligence

<div align="center">

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Streamlit](https://img.shields.io/badge/Streamlit-1.28+-red.svg)
![LangChain](https://img.shields.io/badge/LangChain-Latest-green.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

### 🚀 Transform Your PDFs into Intelligent Conversational Agents

*Ask questions. Get answers. Never lose context.*

[Features](#-features) • [Quick Start](#-quick-start) • [Demo](#-how-it-works) • [Installation](#-installation) • [Usage](#-usage)

</div>

---

## 🎯 What Makes This Special?

Ever wished you could have a **real conversation** with your documents? Not just ask isolated questions, but engage in a flowing dialogue where the AI actually **remembers** what you discussed?

Welcome to the future of document interaction! 🎉

This isn't just another PDF reader. It's your intelligent research assistant that:
- 📚 **Understands context** from your entire conversation history
- 🧩 **Connects the dots** between multiple questions
- 💡 **Thinks like you do** - following the natural flow of discussion
- ⚡ **Responds instantly** with accurate, source-backed answers

---

## ✨ Features

### 🎭 The Core Magic

| Feature | What It Does |
|---------|--------------|
| **🔮 Context-Aware Conversations** | Remembers your entire chat history - ask follow-up questions naturally |
| **📄 Multi-PDF Support** | Upload multiple documents and query them simultaneously |
| **🧠 Smart Retrieval** | Advanced RAG (Retrieval Augmented Generation) for precise answers |
| **💬 Session Management** | Multiple conversation threads with unique session IDs |
| **⚡ Lightning Fast** | Powered by Groq's high-speed inference |
| **🎨 Beautiful UI** | Clean, intuitive Streamlit interface |

### 🛠️ Technical Superpowers

- **History-Aware Retrieval**: Questions are contextualized with previous conversation
- **Vector Embeddings**: Uses HuggingFace's `all-MiniLM-L6-v2` for semantic search
- **Chunking Strategy**: Smart document splitting with overlap for better context
- **Chroma DB**: Efficient vector storage and retrieval
- **LangChain Integration**: Seamless orchestration of LLM chains

---

## 🎬 How It Works

```mermaid
graph LR
    A[📄 Upload PDFs] --> B[✂️ Split & Chunk]
    B --> C[🔢 Create Embeddings]
    C --> D[💾 Store in Vector DB]
    D --> E[❓ Ask Question]
    E --> F[🔍 Retrieve Context]
    F --> G[🧠 LLM + History]
    G --> H[💬 Intelligent Answer]
    H --> I[📝 Update History]
    I --> E
```

### The Conversation Flow

1. **📤 Upload** - Drop your PDF files
2. **🔪 Process** - Documents are split into manageable chunks
3. **🎯 Embed** - Chunks are converted to vector embeddings
4. **💬 Chat** - Ask questions in natural language
5. **🧠 Remember** - Each question considers previous context
6. **🎓 Learn** - The system maintains conversation coherence

---

## 🚀 Quick Start

### Prerequisites

```bash
# You'll need:
- Python 3.8 or higher
- Groq API Key (get it free at groq.com)
- HuggingFace Token (for embeddings)
```

### ⚙️ Installation

1. **Clone the Repository**
```bash
git clone https://github.com/yourusername/conversational-rag-pdf.git
cd conversational-rag-pdf
```

2. **Create Virtual Environment**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install Dependencies**
```bash
pip install streamlit langchain langchain-groq langchain-huggingface
pip install langchain-chroma langchain-community pypdf python-dotenv
pip install chromadb sentence-transformers
```

4. **Set Up Environment Variables**
```bash
# Create .env file
echo "HF_TOKEN=your_huggingface_token_here" > .env
```

5. **Run the Application**
```bash
streamlit run app.py
```

---

## 📖 Usage

### Basic Workflow

1. **Launch the App**
   ```bash
   streamlit run app.py
   ```

2. **Enter Your Groq API Key**
   - Get your free key at [console.groq.com](https://console.groq.com)
   - Paste it in the password field

3. **Set Your Session ID**
   - Use default or create a unique session
   - Multiple sessions = Multiple independent conversations

4. **Upload PDF Files**
   - Click "Choose A PDF file"
   - Select one or multiple PDFs
   - Wait for processing (you'll see progress)

5. **Start Chatting!**
   - Type your question
   - Get contextual answers
   - Ask follow-ups naturally

### 💡 Pro Tips

**Make the Most of Conversation History:**
```
You: "What is the main conclusion of the study?"
AI: "The study concludes that X leads to Y..."

You: "What evidence supports this?"  ← Remembers "this" = previous conclusion
AI: "The evidence includes..."

You: "Are there any limitations?"  ← Knows we're still discussing the same study
AI: "Yes, the limitations are..."
```

**Session Management:**
- Use `session_id="project_alpha"` for project-specific chats
- Switch sessions to maintain separate conversation contexts
- Perfect for comparing different documents or topics

---

## 🏗️ Architecture

### Tech Stack

```
Frontend
├── Streamlit (Web UI)
└── Interactive Components

Backend
├── LangChain (Orchestration)
│   ├── ChatGroq (LLM)
│   ├── HuggingFaceEmbeddings
│   └── Chroma (Vector Store)
├── PyPDF (Document Loading)
└── RecursiveCharacterTextSplitter
```

### Key Components

| Component | Purpose | Configuration |
|-----------|---------|---------------|
| **ChatGroq** | LLM inference | Model: Gemma2-9b-It |
| **HuggingFace Embeddings** | Text vectorization | Model: all-MiniLM-L6-v2 |
| **Chroma** | Vector database | In-memory storage |
| **Text Splitter** | Document chunking | Size: 5000, Overlap: 500 |

### Prompt Engineering

**Contextualization Prompt:**
```
"Given a chat history and the latest user question which might 
reference context in the chat history, formulate a standalone 
question which can be understood without the chat history."
```

**QA System Prompt:**
```
"You are an assistant for question-answering tasks. Use the 
following pieces of retrieved context to answer the question. 
Keep the answer concise (max 3 sentences)."
```

---

## 🎨 Customization

### Adjust Chunk Size
```python
text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=5000,    # Increase for longer context
    chunk_overlap=500   # Adjust overlap for better continuity
)
```

### Change LLM Model
```python
llm = ChatGroq(
    groq_api_key=api_key,
    model_name="llama-3.1-70b-versatile"  # Try different models
)
```

### Modify Response Length
```python
system_prompt = (
    "Use five sentences maximum and provide detailed explanations."  # Customize here
)
```

---

## 🔧 Environment Variables

Create a `.env` file in the root directory:

```env
# Required
HF_TOKEN=your_huggingface_token_here

# Optional (can be entered in UI)
GROQ_API_KEY=your_groq_api_key_here
```

---

## 📊 Example Use Cases

### 📚 Academic Research
Upload research papers and have intelligent discussions about methodologies, findings, and implications.

### 📋 Legal Documents
Query contracts, agreements, and legal texts with contextual follow-up questions.

### 📖 Technical Documentation
Navigate complex technical manuals with conversational ease.

### 📰 Report Analysis
Upload multiple reports and compare insights across documents.

---

## 🐛 Troubleshooting

### Common Issues

**Problem:** "API Key Invalid"
```
Solution: Verify your Groq API key at console.groq.com
```

**Problem:** "Embeddings Error"
```
Solution: Check HF_TOKEN in .env file
        Ensure internet connection for model download
```

**Problem:** "PDF Not Loading"
```
Solution: Ensure PDF is not password-protected
        Check file size (keep under 50MB for best performance)
```

**Problem:** "Slow Processing"
```
Solution: Reduce chunk_size or number of documents
        Consider using a faster embedding model
```

---

## 🚦 Performance Tips

1. **Start Small**: Test with 1-2 PDFs before scaling up
2. **Optimize Chunks**: Balance chunk_size vs. retrieval accuracy
3. **Session Cleanup**: Clear old sessions to free memory
4. **Network**: Ensure stable connection for API calls

---

## 🗺️ Roadmap

- [ ] 🌐 Multi-language support
- [ ] 📊 Export chat history as PDF/Markdown
- [ ] 🎯 Highlighted source citations
- [ ] 🔄 Document update/refresh functionality
- [ ] 📈 Analytics dashboard
- [ ] 🎤 Voice input support
- [ ] 🌙 Dark mode UI

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. 🍴 Fork the repository
2. 🌿 Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. 💾 Commit your changes (`git commit -m 'Add AmazingFeature'`)
4. 📤 Push to the branch (`git push origin feature/AmazingFeature`)
5. 🎉 Open a Pull Request

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- **LangChain** - For the amazing RAG framework
- **Groq** - For lightning-fast LLM inference
- **HuggingFace** - For accessible embeddings
- **Streamlit** - For the beautiful UI framework
- **Chroma** - For efficient vector storage

---

<div align="center">

### ⭐ Star this repo if you find it helpful!

**Made with ❤️ and 🤖 by Shanmukh_datta**

[⬆ Back to Top](#-conversational-rag-with-pdf-intelligence)

</div>
