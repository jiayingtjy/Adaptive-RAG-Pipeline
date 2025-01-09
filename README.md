# Adaptive Retrieval-Augmented Generation (RAG) Pipeline

This project focuses on building an **Adaptive Retrieval-Augmented Generation (RAG)** pipeline. The strategy combines **(1) Query Analysis** with **(2) Self-RAG**, dynamically tailoring retrieval and generation processes to optimize efficiency and accuracy.

---

## Problem Description

While Retrieval-Augmented Generation (RAG) systems enhance response accuracy by combining generative capabilities of large language models (LLMs) with retrieval mechanisms, existing systems face key challenges:

1. **Handling Simple Queries:** Current systems often apply unnecessary computational overhead to simple queries, making them inefficient.
2. **Addressing Complex Queries:** These systems struggle with multi-step queries, leading to incomplete or suboptimal responses.

Real-world queries exhibit varying complexity levels, necessitating a dynamic and adaptive approach to optimize performance for diverse tasks.

---

## Solution

The **Adaptive RAG Pipeline** addresses these challenges by dynamically adjusting retrieval and generation strategies based on query complexity. This ensures:

- **Efficiency:** Simple queries are handled with lightweight or no retrieval, minimizing resource usage.
- **Accuracy:** Complex queries are tackled with iterative retrieval and multi-step reasoning to provide accurate and context-aware responses.
- **Adaptability:** A query classifier selects the optimal strategy (e.g., Self-RAG or web search) based on query complexity.

---

## Project Flow

To implement this pipeline, the project uses **state machines** for constructing and managing diverse RAG flows, leveraging LangGraph for flow engineering. Nodes and edges represent components of the pipeline, compiled into a cohesive architecture.

### **Phase 1: Pre-Retrieval**

1. **Indexing:** Prepare data for efficient retrieval by creating indexed representations of external knowledge bases.
2. **Query Analysis and Routing:**
   - If the query is related to the index, route it to **Self-RAG**.
   - If the query is unrelated to the index, route it to **web search**.

### **Phase 2A: Active Self-RAG**

Build nodes and edges for an **Active Self-RAG** process to handle queries related to the indexed data. This involves:

- **Active RAG:** Dynamically decides *when* and *what* to retrieve, rewrite, or re-retrieve based on query analysis and LLM reasoning.
- **Self-RAG:** Incorporates self-reflection and self-grading on retrieved documents and generated responses, improving quality through iterative refinement.

### **Phase 2B: Active Web Search**

Build nodes and edges for integrating web search into the pipeline for queries unrelated to the indexed data. Use retrieval and generation strategies tailored to external web-based information.

### **Phase 3: Graph Construction**

The Adaptive RAG pipeline uses a **state graph** to represent the flow of operations. This phase involves:

1. **Defining Nodes:** Each node represents a specific operation in the pipeline, such as retrieving documents, grading their relevance, or generating an answer.
2. **Adding Edges:** Edges connect nodes and define the sequence of operations. Conditional edges determine the next step based on the output of the current node, allowing for dynamic decision-making.
3. **Workflow Compilation:** All nodes and edges are compiled into a cohesive workflow using LangGraph, which supports flexible flow engineering and dynamic execution.

For example, the pipeline dynamically routes a query through nodes like `retrieve`, `grade_documents`, or `web_search`, depending on the query's complexity and relevance to indexed data.

### **Phase 4: Graph Usage**

In this phase, the constructed graph is executed to process user queries:

1. **Streaming Execution:** The graph is streamed iteratively, with each node updating the graph's state.
2. **Dynamic Routing:** Conditional edges ensure that queries are routed to the appropriate nodes (e.g., `web_search` for unrelated queries or `generate` for producing answers).
3. **State Updates:** Each node processes the input graph state and produces an updated state, which is passed to the next node.
4. **Final Generation:** The pipeline outputs a comprehensive response to the user’s query, whether retrieved from indexed data or web-based information.

This dynamic execution ensures an efficient and accurate response generation process, adapting seamlessly to the complexity of each query.

---

## Usage of RRR Framework

The project incorporates the **Rewriting, Re-ranking, and Re-retrieving (RRR)** framework within the Adaptive RAG pipeline to enhance retrieval and generation processes:

1. **Rewriting:** The Query Rewriter optimizes queries for better alignment with indexed data or retrieval mechanisms, especially when initial retrieval results are ambiguous or insufficient.
2. **Re-ranking:** The Retrieval Grader evaluates and prioritizes the relevance of retrieved documents, filtering out irrelevant ones to ensure high-quality inputs for answer generation.
3. **Re-retrieving:** The pipeline iteratively refines retrieval using the Transform Query node, which rewrites the question to address gaps in the initial retrieval phase.

By leveraging the RRR framework, the Adaptive RAG pipeline ensures a robust and adaptive retrieval process, balancing efficiency and accuracy for diverse query complexities.

---

## Referenced Paper

**Adaptive-RAG: Learning to Adapt Retrieval-Augmented Large Language Models through Question Complexity**  
[https://arxiv.org/abs/2403.14403](https://arxiv.org/abs/2403.14403)
