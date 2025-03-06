# Project Overview

You are building a no-code tool for LangChain functionality. Users can add different components into a graph and connect them to build out various flows visually.

The backend will be developed using **Python FastAPI** and **LangChain**. 

The core idea is that nodes in the frontend graph will correspond to LangChain integrations, and data will be passed dynamically between connected nodes when the program runs.

For the frontend, you will use **Next.js 14, Tailwind CSS, React Flow, Lucide Icons, and ShadCN**.

The backend and database will be **deployed on Railway**, ensuring a scalable and easy-to-manage infrastructure.

---

## Core Functionalities

### User Management

- Users should be able to **sign up and log in**.
- Users should be able to **save different flows** to their accounts in **JSON format**.
- Users should be able to **store API keys and configurations** securely.

### Graph Editor

- A **drag-and-drop interface** where users can:
  - Add various **components (nodes)** to the workspace.
  - Connect nodes together via **edges**.
  - Click on a node to configure its properties and API integrations.
  - **Run the flow** from a specific node.
  - Delete individual nodes or entire flows.
  - Save and load flows from the database.

### Execution Engine

- When a user **executes a flow**, the backend should:
  - Process **each node sequentially** or **in parallel** (if needed).
  - Pass data between nodes dynamically.
  - Handle **API calls, data transformations, and conditions**.
  - Provide **execution logs** to help users debug.

### Backend Structure

- **Modular Node System**: Components should be designed to be **extendable** for future integrations.
- **Concurrency**: Support **async execution** for efficient performance.
- **Error Handling**: Implement **logging and fallback mechanisms** to prevent execution failures.
- **Database**: Use **PostgreSQL on Railway** for storing user data, flows, and API keys.
    - For development use SQLlite.
- **Authentication**: Implement **JWT-based authentication** with FastAPI.
- **Deployment**: Automatically deploy **FastAPI + PostgreSQL** on Railway via GitHub Actions.

## MVP version

General specs for all components.

- The user should be able to rename nodes.
- The user should be able to start a flow from any node.
- The output nodes must all be unique.
- The user must be able to add multiple of the same node in a flow.
- All nodes should be defined as input and output with the details of what they do abstracted.

The app should have components for:

*user input nodes*

- Prompt node
    - The user can type prompts into this and use {} syntax to define different variables.
    - Each variable a prompt node will have its own input the user can connect to for it.
    - Promopts should output a string to the next node formatting the variables with the prompt.

*output nodes*

- Output node
    - The output node should take in a string as input and output nothing.
    - The node should display the string passed into it.

- Multiple output node
    - The multiple output node should be able to take strings as an input and output nothing.
    - The node should display the strings passed into it appending each time new data is passed in. 
    - The node should have a clear button that clears the data it is storing.

*LLM nodes*

- OpenAi LLM node
    - The user can choose between different openai models with a dropdown menu.
    - The OpenAi LLM node takes a string as an input (for a prompt) and outputs the models response as a string.
- Anthropic LLM node
    - The user can choose between different anthropic models with a dropdown menu.
    - The Anthropic LLM node takes a string as an input (for the prompt) and outputs the models response as another string.
- Google LLM node
    - The user can choose between different google LLM models with a dropdown menu.
    - The Google LLM node takes a string as an input and output the models response as another string.

*File Processing nodes*

- PDF input node
    - The user can choose to upload a PDF to this node.
    - The node will use Langchains PDF functionality to get the text from the document.
    - The node will output a string of the text. This will not take any input.

*Text manipulation nodes*

- Text splitter node
    - This node will take in text as an input. 
    - The node then will split it using Langchains text splitter functionality.
    - For each batch of text, the remainder of the flow will be ran. E.g. if it splits long text into 20 parts the rest of the flow will be ran with each of the 20 parts one at a time.

*Databse nodes*

- Pinecone upload node
    - This node will take a string as an input.
    - The node wil allow the user to specify a pinecone index inside of it.
    - The node will allow the user to select between openai embeddings small or openai embeddings large.
    - The node will process that string into an embedding then upload it into the pinecone database.
    - The node will output successfully uploaded (string passed in) or failled to upload (string passed in).
- Pinecone retreival node
    - This node will take a string as an input.
    - The node will allow the user to specify a pinecone index.
    - The node will allow the user to specify a k value for how many results to return.
    - The node will allow the user to select between openai embeddings small or large.
    - The node willl process the string into an embedding and return the matches into another string as output.
