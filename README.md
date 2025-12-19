# grk_langchain

This five-page summary covers **Topic 2 (Fundamentals & Components)** and **Topic 3 (Chains & LCEL)** as presented in the "Getting Started with LangChain" document.

---

### **Page 1: Introduction to the LangChain Framework**

**What is LangChain?**
LangChain is a specialized framework designed to facilitate the creation of applications powered by Large Language Models (LLMs). It addresses the need for a structured way to build complex AI systems by providing a modular architecture.

**Main Features:**
* **Components:** Modular building blocks that provide the necessary abstractions for working with LLMs.
* **Off-the-shelf Chains:** Pre-built configurations that allow developers to get started quickly with common tasks.

**The Underlying Logic:**
The document establishes that LLMs fundamentally function by predicting the next word in a sequence (e.g., "I love eating... pancakes"). LangChain provides the scaffolding to turn these predictions into functional tools like chatbots, search engines, and personalized tutors.

---

### **Page 2: Core Components — Models and Prompts**

To build any application in LangChain, you start with the basic components:

**1. Models**
Models serve as abstractions over LLM APIs, such as the OpenAI ChatGPT API. LangChain allows you to interface with different model types consistently.
* *Code Example Reference:* The document demonstrates using `from langchain_openai import ChatOpenAI` to initialize a model.



**2. Prompt Templates**
Instead of using hard-coded strings, LangChain uses Prompt Templates.
* **Definition:** These are abstractions over standard prompts sent to LLMs.
* **Functionality:** They allow for dynamic variables to be swapped into a prompt, making them reusable and consistent across different parts of an application.
* *Code Example Reference:* Uses `ChatPromptTemplate` from `langchain_core.prompts`.

---

### **Page 3: Output Parsers and the Chain Formula**

**3. Output Parsers**
LLMs return raw text strings, which are often difficult for software to process. Output Parsers solve this by:
* **Translation:** Converting raw LLM text into a "workable format" like a clean string or structured JSON.
* *Code Example Reference:* The `StrOutputParser` is used to ensure the final output is a standard string.

**The Definition of a Chain**
The document defines the foundational "formula" for LangChain development:
> **Chain = Model + Prompt + Output Parser**

Chains are the essential building blocks in LangChain. They allow developers to compose these abstractions to move from simple tasks to complex, multi-step AI workflows.

---

### **Page 4: LangChain Expression Language (LCEL)**

**Concept and Syntax**
Topic 3 introduces **LCEL**, a declarative language designed to streamline the composition of these chains.

* **Unix-like Pipe Syntax:** LCEL uses the pipe operator (`|`) to bind components together sequentially.
* **Logic:** The output of the first component (the prompt) becomes the input for the second (the model), and the model’s output is passed to the third (the output parser).



**Why use LCEL?**
It simplifies code readability and offers built-in support for:
* **Async/Streaming:** Improved performance for web applications.
* **Parallel Execution:** Running multiple steps at the same time.

---

### **Page 5: The "Runnable" Protocol and Interface**

To make custom chains functional and standardized, LangChain implements the **"Runnable"** protocol. This ensures that every chain built with LCEL follows a predictable interface.

**Standard Interface Methods:**
* **`invoke`:** Calls the chain on a single input.
* **`batch`:** Calls the chain on a list of multiple inputs.
* **`stream`:** Streams back chunks of the response as they are generated (useful for real-time AI typing effects).

**Async Capabilities:**
For every standard method, there is a corresponding asynchronous version (e.g., `ainvoke`, `abatch`, `astream`) to facilitate non-blocking operations in modern software environments.

The section concludes by noting that these basic components and the LCEL syntax are the primary tools that ease the creation of LLM-based applications.


```python?code_reference&code_event_index=2
import pypdf

def find_runnable_info(pdf_path):
    with open(pdf_path, 'rb') as f:
        reader = pypdf.PdfReader(f)
        runnable_pages = []
        for i, page in enumerate(reader.pages):
            text = page.extract_text()
            if "runnable" in text.lower():
                runnable_pages.append((i + 1, text))
    return runnable_pages

pdf_path = '20240221gettingstartedwithlangchainpresentation11731541351107.pdf'
info = find_runnable_info(pdf_path)

for page_num, text in info:
    print(f"--- PAGE {page_num} ---")
    print(text)


```

```text?code_stdout&code_event_index=2
--- PAGE 41 ---
LCEL - Runnables
To facilitate creation of custom chains, LangChain has implemented a
"Runnable" protocol.
41 / 117
--- PAGE 42 ---
LCEL - Runnables
To facilitate creation of custom chains, LangChain has implemented a
"Runnable" protocol.
The standard interface includes stream, invoke, and batch methods. Async
methods are also available
42 / 117
--- PAGE 43 ---
LCEL - Runnables
To facilitate creation of custom chains, LangChain has implemented a
"Runnable" protocol.
The standard interface includes stream, invoke, and batch methods. Async
methods are also available
The input type and output type vary by component:
43 / 117
--- PAGE 106 ---
LangServe Super Quick Intro
LangServe helps developers deploy LangChain runnables and chains as a
REST API.
106 / 117
--- PAGE 107 ---
LangServe Super Quick Intro
LangServe helps developers deploy LangChain runnables and chains as a
REST API.
It is integrated with FastAPI and uses pydantic for data validation.
107 / 117
--- PAGE 108 ---
LangServe Super Quick Intro
LangServe helps developers deploy LangChain runnables and chains as a
REST API.
It is integrated with FastAPI and uses pydantic for data validation.
It provides a client that can be used to call into runnables deployed on a
server.
108 / 117
--- PAGE 109 ---
LangServe Super Quick Intro
LangServe helps developers deploy LangChain runnables and chains as a
REST API.
It is integrated with FastAPI and uses pydantic for data validation.
It provides a client that can be used to call into runnables deployed on a
server.
Input and Output schemas automatically inferred from your LangChain
object, and enforced on every API call, with rich error messages
109 / 117
--- PAGE 110 ---
LangServe Super Quick Intro
LangServe helps developers deploy LangChain runnables and chains as a
REST API.
It is integrated with FastAPI and uses pydantic for data validation.
It provides a client that can be used to call into runnables deployed on a
server.
Input and Output schemas automatically inferred from your LangChain
object, and enforced on every API call, with rich error messages
Efficient /invoke/, /batch/ and /stream/ endpoints with support for many
concurrent requests on a single server
110 / 117
--- PAGE 111 ---
LangServe Super Quick Intro
LangServe helps developers deploy LangChain runnables and chains as a
REST API.
It is integrated with FastAPI and uses pydantic for data validation.
It provides a client that can be used to call into runnables deployed on a
server.
Input and Output schemas automatically inferred from your LangChain
object, and enforced on every API call, with rich error messages
Efficient /invoke/, /batch/ and /stream/ endpoints with support for many
concurrent requests on a single server
Playground page at /playground/ with streaming output and intermediate
steps
111 / 117
--- PAGE 112 ---
LangServe Super Quick Intro
LangServe helps developers deploy LangChain runnables and chains as a
REST API.
It is integrated with FastAPI and uses pydantic for data validation.
It provides a client that can be used to call into runnables deployed on a
server.
Input and Output schemas automatically inferred from your LangChain
object, and enforced on every API call, with rich error messages
Efficient /invoke/, /batch/ and /stream/ endpoints with support for many
concurrent requests on a single server
Playground page at /playground/ with streaming output and intermediate
steps
Built-in (optional) tracing to LangSmith, just add your API key (see
Instructions)
112 / 117
--- PAGE 113 ---
LangServe Super Quick Intro
LangServe helps developers deploy LangChain runnables and chains as a
REST API.
It is integrated with FastAPI and uses pydantic for data validation.
It provides a client that can be used to call into runnables deployed on a
server.
Input and Output schemas automatically inferred from your LangChain
object, and enforced on every API call, with rich error messages
Efficient /invoke/, /batch/ and /stream/ endpoints with support for many
concurrent requests on a single server
Playground page at /playground/ with streaming output and intermediate
steps
Built-in (optional) tracing to LangSmith, just add your API key (see
Instructions)
Use the client SDK to call a LangServe server as if it was a Runnable
running locally (or call the HTTP API directly)
113 / 117
--- PAGE 114 ---
LangServe Super Quick Intro
LangServe helps developers deploy LangChain runnables and chains as a
REST API.
It is integrated with FastAPI and uses pydantic for data validation.
It provides a client that can be used to call into runnables deployed on a
server.
Input and Output schemas automatically inferred from your LangChain
object, and enforced on every API call, with rich error messages
Efficient /invoke/, /batch/ and /stream/ endpoints with support for many
concurrent requests on a single server
Playground page at /playground/ with streaming output and intermediate
steps
Built-in (optional) tracing to LangSmith, just add your API key (see
Instructions)
Use the client SDK to call a LangServe server as if it was a Runnable
running locally (or call the HTTP API directly)
114 / 117
--- PAGE 115 ---
Final Q&A & Summary
LangServe helps developers deploy LangChain runnables and chains as a
REST API.
It is integrated with FastAPI and uses pydantic for data validation.
115 / 117

```

Based on the provided document, the **Runnable** protocol is a core architectural feature of LangChain designed to standardize how custom chains are built, executed, and deployed.

Here is a detailed breakdown of the **Runnable** protocol as described in the slides:

### **1. Purpose and Definition**

* **Facilitates Custom Chains:** The protocol was implemented specifically to make it easier for developers to create their own custom chains within the LangChain framework.
* **Standard Interface:** It provides a uniform way to interact with any component or chain, regardless of its internal complexity.

### **2. The Standard Interface (Methods)**

Every Runnable object supports a specific set of methods that allow for different types of execution:

* **`invoke`:** Calls the chain or component on a single input to get a single output.
* **`batch`:** Efficiently calls the chain on a list of multiple inputs.
* **`stream`:** Streams back chunks of the response as they are generated, rather than waiting for the full response.
* **Async Support:** For modern application needs, the protocol includes asynchronous versions of all these methods (e.g., `ainvoke`, `abatch`, and `astream`).

### **3. Inputs and Outputs**

* The document notes that while the interface is standardized, the **input type and output type vary by component**. This allows the same protocol to be applied to prompt templates, models, and output parsers even though they handle different data types.

### **4. Role in Deployment (LangServe)**

The Runnable protocol is the foundation for deployment through **LangServe**:

* **REST API Mapping:** LangServe automatically turns LangChain runnables into REST APIs with specific endpoints that match the protocol: `/invoke/`, `/batch/`, and `/stream/`.
* **Schema Inference:** LangServe automatically infers the input and output schemas directly from the Runnable object, ensuring data validation via Pydantic.
* **Remote Execution:** It provides a client SDK that allows a developer to call a remotely deployed chain "as if it was a Runnable running locally".

### **5. Integration with LCEL**

* Runnables are the primary "units" used in **LangChain Expression Language (LCEL)**. By following this protocol, different components can be piped together (using `|`) because they all share the same underlying execution logic.


Here is the 20-question quiz covering **LangChain Fundamentals & LCEL** (Slides 15–46) in a standard Markdown format.

---

### **LangChain Fundamentals and LCEL Quiz**

**1. According to the document, what is the primary purpose of the LangChain framework?**
* A) To train new Large Language Models from scratch.
* B) To provide a database for storing vector embeddings only.
* **C) To facilitate the creation of applications based on Large Language Models.**
* D) To replace the need for API keys when using OpenAI.
* *Rationale: The slides define LangChain as a framework that eases the creation of LLM-based applications.*

**2. Which component is described as an abstraction over LLM APIs like the ChatGPT API?**
* **A) Models**
* B) Output Parsers
* C) Prompt Templates
* D) AgentExecutor
* *Rationale: Models are the specific building blocks providing interfaces to LLM providers.*

**3. What is the main benefit of using "Prompt Templates" instead of standard hard-coded strings?**
* **A) They allow for dynamic variables to be swapped into a consistent format.**
* B) They automatically translate prompts into multiple languages.
* C) They reduce the cost of API calls by compressing the text.
* D) They prevent the LLM from hallucinating entirely.
* *Rationale: Prompt Templates are abstractions that allow for dynamic inputs while maintaining a reusable structure.*

**4. What is the primary function of an "Output Parser" in LangChain?**
* **A) To translate raw LLM output into a workable format like a string or JSON.**
* B) To check the spelling and grammar of the LLM’s response.
* C) To send the LLM response back to the user via email.
* D) To encrypt the data before it is stored in a database.
* *Rationale: Output Parsers take unstructured text and convert it into a format usable by code.*

**5. According to the document's "formula," what are the three components of a basic Chain?**
* **A) Model + Prompt + Output Parser**
* B) Input + Process + Output
* C) Prompt + LLM + Vector Store
* D) FastAPI + Pydantic + Runnable
* *Rationale: This is the core formula provided for building blocks in the framework (Slide 32).*

**6. What does the acronym LCEL stand for?**
* **A) LangChain Expression Language**
* B) Large Component Execution Logic
* C) Language Coding and Evaluation Library
* D) Latent Chain Embedding Layer
* *Rationale: LCEL is the declarative language used to compose chains.*

**7. In LCEL, which symbol is used to pipe components together?**
* **A) The pipe operator ( | )**
* B) The arrow operator ( -> )
* C) The double colon ( :: )
* D) The plus sign ( + )
* *Rationale: LCEL utilizes the Unix-like pipe operator to connect the output of one component to the input of the next.*

**8. What happens in the LCEL chain `chain = prompt | model | output_parser`?**
* **A) The output of the prompt template is passed as the input to the model.**
* B) All three components are executed simultaneously in parallel.
* C) The model modifies the prompt before it is sent to the parser.
* D) The prompt is sent directly to the parser, bypassing the model.
* *Rationale: The pipe ensures a sequential flow from left to right.*

**9. Which method in the "Runnable" protocol is used to call a chain on a single input?**
* **A) invoke**
* B) batch
* C) stream
* D) call
* *Rationale: The `invoke` method is the standard way to trigger a Runnable with one input.*

**10. What is the purpose of the "batch" method in LangChain?**
* **A) To call the chain on a list of inputs efficiently.**
* B) To divide a long document into smaller text chunks.
* C) To permanently store data in a database.
* D) To repeat the same input 10 times to ensure accuracy.
* *Rationale: Batching allows multiple data points to be processed through the same logic in one operation.*

**11. Which feature of the "Runnable" protocol allows users to see the output as it is being generated?**
* **A) stream**
* B) async
* C) invoke
* D) parallel
* *Rationale: `stream` sends back chunks of the response as they are produced.*

**12. How does LangChain handle asynchronous operations within the Runnable protocol?**
* **A) By providing methods like ainvoke and astream.**
* B) By requiring a separate library called "LangAsync."
* C) By only supporting synchronous calls to avoid complexity.
* D) By automatically converting all functions into threads.
* *Rationale: LangChain includes native async versions of its standard methods (Slide 42).*

**13. According to slide 33, what are the "building blocks" of LangChain?**
* **A) Chains**
* B) Embeddings
* C) Vector Databases
* D) REST APIs
* *Rationale: The text states "Chains are the building blocks in LangChain."*

**14. Which Python class from the document is used to create a model for OpenAI's chat API?**
* **A) ChatOpenAI**
* B) OpenAIModel
* C) GPTAbstraction
* D) LangModel
* *Rationale: The code snippets specifically show `ChatOpenAI` imported from `langchain_openai`.*

**15. What is the purpose of the "Runnable" protocol implemented by LangChain?**
* **A) To facilitate the creation of custom chains with a standard interface.**
* B) To make the Python code run 50% faster.
* C) To allow chains to run on any operating system without Python installed.
* D) To automatically generate documentation for the code.
* *Rationale: Standardizing the interface ensures all chains can be used interchangeably.*

**16. Why does LCEL support "Parallel Execution"?**
* **A) To run multiple tasks at the same time and improve application performance.**
* B) To make sure the LLM produces two different answers for every question.
* C) To ensure that the code is more difficult for competitors to copy.
* D) To allow the chain to run on both Mac and Windows simultaneously.
* *Rationale: Parallel execution allows independent operations to run simultaneously to save time.*

**17. Which component would you use to ensure the LLM's raw response is always returned as a clean string?**
* **A) StrOutputParser**
* B) CleanStringTemplate
* C) OutputModel
* D) ParserChain
* *Rationale: `StrOutputParser` is the tool for translating raw output into a standard string.*

**18. What is the relationship between LCEL and chains?**
* **A) LCEL is the language used to compose and connect the pieces of a chain.**
* B) LCEL is a replacement for the concept of chains.
* C) Chains are only used if you decide NOT to use LCEL.
* D) LCEL is the name of the database where chains are stored.
* *Rationale: LCEL provides the syntax (pipes) to define how components interact within a chain.*

**19. In the context of LangChain, what is a "Runnable"?**
* **A) A standard interface that makes it easy to define and call custom chains.**
* B) A specific type of high-speed hardware for AI.
* C) An automated bot that tests the code for errors.
* D) A data format used for saving prompt templates.
* *Rationale: It is an abstraction for something that can be executed using a consistent set of commands.*

**20. Based on the document, why is LCEL described as "declarative"?**
* **A) It allows developers to describe what the chain should do rather than writing complex logic for every step.**
* B) Because every variable must be declared before it is used.
* C) Because it makes the chain permanent and unchangeable once written.
* D) Because it relies on the "Declare" keyword to start every chain.
* *Rationale: Declarative style focuses on the "what" (composing the sequence) rather than the "how" (internal implementation).*

