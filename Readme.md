# Keploy CodeIndexer - GSoC 2025 Project

## Overview

A comprehensive AI-powered codebase intelligence system developed during Google Summer of Code 2025 under **Keploy**. This project enables semantic understanding and natural language interaction with large codebases, significantly enhancing Keploy's test generation capabilities through context-aware AI assistance.

## 🚀 Key Features

- **Semantic Code Understanding** - Uses Tree-sitter for AST parsing and pgvector for intelligent code indexing
- **Natural Language Queries** - Ask questions about your codebase in plain English
- **Context-Aware Test Generation** - Enhanced AI-powered test generation with codebase context
- **MCP Integration** - Seamless IDE integration through Model Context Protocol
- **Incremental Processing** - Efficient handling of large codebases with change detection

## 🛠️ Technology Stack

- **Backend**: Go, PostgreSQL with pgvector, Tree-sitter
- **AI Models**: Qodo-Embed-1-1.5B (embeddings), Gemini API (conversations)
- **Protocols**: Model Context Protocol (MCP), REST APIs
- **Tools**: tiktoken-go (token management), SHA-256 (change detection)

## 📋 Quick Start

### 1. Index Your Codebase

```bash
# Initial setup
keploy embed --source-path="/your/project"

# Force complete reindexing
keploy embed --force-reindex
```

### 2. Query Your Code

```bash
# Ask questions about your codebase
keploy converse "How does the authentication middleware work?"
keploy converse "What are the main entry points to this application?"
keploy converse "Show me all database models and their relationships"
```

## 🏗️ Architecture

```
CLI Commands → Service Factory → Embed Service → AI Client → LLM API
                                              ↓
                              MCP Server → Protocol Handler
```

**Workflow:**

1. **Embedding Phase**: Parse code → Generate embeddings → Store in vector database
2. **Conversation Phase**: Process question → Search embeddings → Generate AI response

## 🎯 Use Cases

- **Code Exploration** - Understand unfamiliar codebases quickly
- **Documentation** - Auto-generate documentation from code analysis
- **Code Reviews** - Get context about changes and their implications
- **Onboarding** - Help new developers understand existing systems
- **Test Generation** - Create better tests with full codebase context

## 👥 Contributors

**GSoC 2025 Contributor:** [Sparsh Gupta](https://github.com/ayesparshh)  
**Mentors:** Ayush, Sarthak  
**Organization:** [Keploy](https://github.com/keploy/keploy)

## 📖 Project Links

- [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2025/projects/wIsioRXL)
- [Main Repository](https://github.com/keploy/keploy)
- [Project Blog](https://gsoc-codeindexer-keploy.hashnode.dev/preview/6884a0fe77c16b6d6b08d367)
- [Final Report](./Final-report.md)

---

\*This project enhances Keploy's testing capabilities by adding intelligent codebase understanding, making test generation more context-aware and developer-
