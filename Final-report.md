# Keploy CodeIndexer for Large Codebases

## Final Work Report for the Google Summer of Code 2025 under `Keploy` for the CodeIndexer project

<p align="center">
<img src="https://github.com/keploy.png" height="300px">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</p>

## Contributor Info

<div container>
<table>
<tr>
<td width="600px">
&#8226; Name - Sparsh Gupta <br />
&#8226; Organization - <a href="https://github.com/keploy/keploy" target="_blank">Keploy</a><br />
&#8226; Email - <a href="mailto:sparshgupta1001@gmail.com" target="_blank">sparshgupta1001@gmail.com</a><br />
&#8226; GitHub - <a href="https://github.com/ayesparshh" target="_blank">ayesparshh</a><br />
</td>
<td>
<a href="https://github.com/ayesparshh"><img src="https://github.com/ayesparshh.png" height="250px" width="250px;" alt=""/></a>
</td>
</tr>
</table>
</div>

## Mentors' Info

- **Mentor:** Ayush
- **Assisting Mentor:** Sarthak

<br />

## Project Details

The [**Keploy CodeIndexer**](https://github.com/keploy/keploy) project is "_a comprehensive codebase intelligence system_" that enables semantic understanding and natural language interaction with large codebases. The existing implementation of Keploy's test generation lacked context-aware capabilities, making it difficult to generate high-quality tests that understand the broader codebase architecture and dependencies.

The CodeIndexer project implements a sophisticated embedding-based system using modern technologies like **Tree-sitter** for AST parsing, **PostgreSQL with pgvector** for vector storage, and advanced AI models for semantic understanding. This significantly enhances the test generation process by providing rich contextual information and enables users to have natural language conversations with their codebase.

The project focuses on implementing three core components: the **"Embed Service"** for intelligent code indexing, the **"Converse Interface"** for natural language codebase interaction, and the **"MCP Integration"** for seamless IDE integration.

<br />

## GSoC Project Page

- [GSoC 2025 with Keploy - CodeIndexer for Large Codebases](https://summerofcode.withgoogle.com/programs/2025/projects/wIsioRXL)

## Project Repository

- [keploy/keploy](https://github.com/keploy/keploy)

## GSoC Blogs

- [GSoC 2025 with Keploy | CodeIndexer Project Updates](https://gsoc-codeindexer-keploy.hashnode.dev/preview/6884a0fe77c16b6d6b08d367)

<br />

## Work Summary

### **1. Developing the Core Embed Service Architecture**

At the foundation of the CodeIndexer project, I implemented the comprehensive embed service that serves as the backbone for all semantic understanding capabilities. The service consists of multiple interconnected components:

- **Service Layer (service.go)**: Implemented the main EmbedService struct that orchestrates the entire indexing pipeline, managing database connections, parser instances, and coordinating between different components.

- **AI Client Integration (ai_client.go)**: Developed the AI client interface that handles communication with embedding models and large language models, supporting multiple providers and enabling flexible model switching.

- **Database Management**: Integrated PostgreSQL with pgvector extension for efficient vector storage and similarity search using HNSW (Hierarchical Navigable Small World) indexing.

### **2. Implementing Intelligent Code Parsing and Chunking**

One of the most critical aspects of the project was developing a semantic understanding of code structure:

- **Code Parser (codeparser.go)**: Built on top of Tree-sitter, this component generates Abstract Syntax Trees (AST) for Go, Python, and JavaScript files. The parser identifies Points of Interest (POIs) such as functions, methods, and classes, providing semantic understanding beyond simple text processing.

- **Semantic Chunker (chunker.go)**: Implemented intelligent code chunking that respects code boundaries and maintains semantic coherence. The chunker uses the AST information to create meaningful chunks that preserve function integrity and provide proper context for AI models.

### **3. Building the Repository Mapping System**

To provide comprehensive codebase understanding, I developed a repository mapping system:

- **Repository Map (repo_map.go)**: Created a system that builds a complete map of the codebase structure, tracking file relationships, dependencies, and maintaining an overview of the entire project architecture.

- **File Hash Management**: Implemented efficient change detection using SHA-256 hashing to avoid reprocessing unchanged files, significantly improving performance for large codebases.

### **4. Implementing Parallelized Processing Pipeline**

To handle large codebases efficiently, I designed and implemented a multi-stage concurrent processing pipeline:

- **File Discovery Workers**: Concurrent workers that walk the directory tree and identify code files
- **Chunking Pipeline**: Parallel processing of files using worker pools for parsing and chunking
- **Embedding Generation**: Batch processing of chunks for efficient AI API utilization
- **Database Storage**: Optimized bulk insert operations for vector storage

The pipeline architecture ensures maximum throughput while maintaining system stability and resource efficiency.

### **5. Creating the Converse Interface**

Developed a natural language interface that allows developers to query their codebase using conversational AI, enabling intuitive code exploration and understanding.

### **6. Implementing MCP (Model Context Protocol) Integration**

Developed MCP server capabilities for seamless IDE integration:

- **MCP Server (mcp/server.go)**: Implemented the Model Context Protocol server that enables direct integration with development environments like VS Code
- **Converse Handler (mcp/converse_handler.go)**: Created handlers for processing IDE requests and providing contextual code assistance

### **7. Enhanced Test Generation Integration**

Integrated the embed service with Keploy's existing unit test generation system:

- **Context Enhancement**: The UTGen service now leverages the embed service to provide rich contextual information when generating tests
- **Semantic Search**: Before generating tests for a file, the system searches for similar code patterns and related functions across the entire codebase
- **Intelligent Prompting**: Enhanced AI prompts with relevant code context, significantly improving test quality and coverage

### **8. CLI Interface Development**

Developed comprehensive command-line interfaces for user interaction:

- **Converse Command (converse.go)**: Implemented interactive CLI for natural language codebase queries
  - Command structure: `keploy converse "how does the user authentication work?"`
  - Service integration through dependency injection and ServiceFactory pattern
  - Comprehensive input validation and error handling
- **Embed Command (embed.go)**: Created CLI for codebase indexing and embedding generation
  - Support for incremental processing with `--force-reindex` flag
  - Integration with global configuration settings
  - Optimized workflow for CI/CD pipeline integration

### **9. Advanced Token Management System**

Implemented sophisticated token counting and management:

- **Token Counting (utils.go)**: Integrated tiktoken-go for accurate token counting with fallback to "cl100k_base" encoding
- **Context Limit Management**: Ensures optimal use of LLM context windows
- **Prompt Optimization**: Intelligent prompt construction to maximize information density within token limits

## Technical Implementation

### Technologies Used

- **Golang**: Core implementation language
- **Tree-sitter**: For AST generation and code parsing
- **PostgreSQL with pgvector**: Vector database for similarity search
- **Qodo/Qodo-Embed-1-1.5B**: Embedding model for semantic understanding
- **Gemini API**: Large language model for conversation and test generation
- **tiktoken-go**: Token counting for precise context management
- **Model Context Protocol (MCP)**: Standardized AI model interaction protocol

### Technical Architecture Components

**Core Service Layer:**

- **Service.go**: Main EmbedService orchestrator managing database connections and component coordination
- **AI Client**: Multi-provider LLM interface with flexible model switching capabilities
- **Code Parser**: Tree-sitter based AST generation for Go, Python, and JavaScript
- **Semantic Chunker**: Intelligent code chunking respecting function boundaries and semantic coherence
- **Repository Map**: Complete codebase structure mapping with dependency tracking
- **Prompt Builder**: Dynamic prompt construction for optimal AI interactions

**CLI Interface:**

- **Converse Command**: Interactive natural language querying with examples like:
  ```bash
  keploy converse "How does the authentication middleware work?"
  keploy converse "What are the main entry points to this application?"
  ```
- **Embed Command**: Codebase indexing with incremental processing:
  ```bash
  keploy embed --source-path="/project"
  keploy embed --force-reindex
  ```

**Data Flow Architecture:**

```
CLI Commands → Service Factory → Embed Service → AI Client → LLM API
                                              ↓
                              MCP Server → Protocol Handler
```
