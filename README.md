# **Dynamic Query Routing and Workflow with LangChain**

This project demonstrates a dynamic query routing and retrieval system using LangChain, integrating **Wikipedia**, **Arxiv**, and a **vector store**. The system routes user queries to the appropriate data source and processes them in a graph-based workflow.

---

## **Features**

### **1. Dynamic Query Routing**
The system uses a language model to determine the best data source for a given question:
- **Wikipedia**: General knowledge questions.
- **Vector Store**: Domain-specific questions related to agents, prompt engineering, or adversarial attacks.

---

### **2. Tools and APIs Integration**
#### **Wikipedia Tool**
- Fetches concise information from Wikipedia.
- Uses the **`WikipediaAPIWrapper`** to limit the response to the top result with a maximum character count.

#### **Arxiv Tool**
- Queries the Arxiv API for academic papers.
- Results are constrained by character limits and top result filtering.

#### **Vector Store**
- Retrieves domain-specific documents from a pre-loaded vector store using embeddings.

---

### **3. Workflow with State Graph**
A graph-based approach is used to define and execute the query processing flow:
- **Start**: Accepts the user's question.
- **Routing**: Uses an LLM to decide whether to route the query to the vector store or Wikipedia.
- **Processing**:
  - **Wikipedia Search**: Queries Wikipedia and returns the result.
  - **Retrieve**: Fetches documents from the vector store.
- **End**: Outputs the retrieved information.

---

### **4. LangChain Utilities**
The following LangChain utilities power the system:
- **`StateGraph`**: Implements a graph-based workflow for dynamic execution.
- **`LangChain Community Tools`**: Provides wrappers for Wikipedia and Arxiv queries.
- **`ChatPromptTemplate`**: Defines the prompt for the routing logic.

---

## **Setup and Installation**

### **1. Clone the Repository**
```bash
git clone https://github.com/dilukshashamal/LangchainAstraDB_Chat.git
cd LangchainAstraDB_Chat
```

## **Install Dependencies**
Install the required Python libraries:
```bash
pip install langchain cassio langchain_community langchain_huggingface langchain_groq
```

## **Set Up Environment Variables**
- **`Groq API Key`**: Add your Groq API key to the environment variables.
- **`User-Agent`**: Define a custom USER_AGENT for web requests.

## **Usage**

### **Load Vector Store**
Preload the vector store with domain-specific documents. Refer to the following sample URLs in the code:
- Articles on agents, prompt engineering, and adversarial attacks.

### **Execute Workflow**
Run the graph workflow with a user query:
```bash
inputs = {
    "question": "What is agent?"
}
for output in app.stream(inputs):
    print(output)
```
## **Expected Output**
- **`Domain-Specific Query`**: Results from the vector store.
- **`General Query`**: A concise Wikipedia result.

