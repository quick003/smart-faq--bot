# 🧩 Smart FAQ/Support Bot – Multi‑Tenant with Login, Upload & Feedback

> A ready-to-use, document-based FAQ/Support chatbot built using LangChain, ChromaDB, and Ollama.  
> Each user gets their own isolated knowledgebase. Admin can create users and manage document ingestion.

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1WE_2LGOx4zqLBFYmhn5-sfldMgXp46XU?usp=sharing)

---

## 🌟 Features

- 🔐 **User Login & Isolation**: Each user has their own vector DB – answers are strictly scoped to their own uploaded documents.
- 📤 **Multi-format Upload**: Supports PDFs, CSVs, DOCX, TXT, and Markdown.
- ⚙️ **Admin Portal**: The `admin` user (default: admin/admin) can create new users via a simple interface.
- 🤖 **Chatbot with Source-based RAG**: Accurate answers using Retrieval-Augmented Generation (RAG) with document chunking.
- 💬 **Chat History**: Retains chat session for each user.
- 📁 **Local Vector Persistence**: Stores per-user Chroma DB for fast reloading.
- 👍 **Feedback Ready**: Easy to extend with thumbs-up/down feedback or fine-tuning triggers.

---

## 🔧 Tech Stack

| Layer          | Tool/Lib                         |
|----------------|----------------------------------|
| LLM            | Ollama (`mistral:7b`)            |
| Embeddings     | Ollama (`nomic-embed-text`)      |
| Vector DB      | ChromaDB                         |
| RAG Framework  | LangChain                        |
| UI             | Gradio                           |
| Document Parsing | LangChain loaders + `unstructured` |
| Deployment     | Google Colab Notebook            |

---

## 🚀 How to Use

1. **Open in Google Colab**  
   → [Click here to run the notebook](https://colab.research.google.com/drive/1WE_2LGOx4zqLBFYmhn5-sfldMgXp46XU?usp=sharing)

2. **Run Cells Sequentially**  
   Let the setup complete – it installs dependencies and pulls Ollama models.

3. **Admin Login (First Tab)**  
   Default admin credentials:
   Username: admin
   Password: admin
Use this tab to create new users.

4. **Login & Upload (Second Tab)**  
- Login as any created user.
- Upload documents (PDF, DOCX, CSV, TXT, or MD).
- Click **Index Documents** to store them in your private vector DB.

5. **Ask Questions (Third Tab)**  
- Chat with your personal support bot.
- Answers are grounded strictly in your uploaded files.

---

## 📂 File Structure

```text
📁 /tmp/faq_multi_<id>/
┣ 📄 users.json              # Stores user credentials (SHA256 hashed)
┣ 📁 user_<username>/        # Per-user Chroma vector store
┃ ┣ 📄 chroma.sqlite         # Vector DB
┃ ┣ 📁 index/                # Index files
┃ ┗ 📄 uploaded docs         # Original uploaded files
```
## 🛠️ Customization Ideas

- 👍 **Add a Feedback Button**  
  Let users rate responses with thumbs-up/down to collect feedback and improve your model or fine-tune later.

- 📁 **Enforce Upload Limits / User Quotas**  
  Limit the number or size of files per user to prevent misuse or manage compute cost.

- 🔐 **Secure Passwords with Bcrypt**  
  Replace SHA‑256 with `bcrypt` via [`passlib`](https://passlib.readthedocs.io/) for secure, salted password storage.

- 🚀 **Deploy as a Web Service (Dockerized)**  
  Package the notebook as a web app with Docker, and disable `share=True` in Gradio to control access.

- 📝 **Highlight Sources in Responses**  
  Show which document chunk contributed to the answer using footnotes or expandable source blocks.

---

## 🧠 Future Add-ons

- 🔁 **Streamed Responses**  
  Enable token-by-token streaming using `streaming=True` in Ollama + Gradio `Chatbot` generator updates.

- 🌐 **Embeddable Widget**  
  Build a website-ready chat widget (iframe or JS) that connects to your hosted backend FAQ bot.

- 🗂 **Multi-file Summarization**  
  Let users ask for a “summary of all uploaded policies” using a map-reduce prompt chain.

- ✉️ **Email Notifications**  
  Notify users via email when new documents are uploaded or existing ones change (diff-aware alerts).
