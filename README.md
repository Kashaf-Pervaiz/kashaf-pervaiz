# 🌌 PrismAI

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Build Status](https://img.shields.io/badge/build-passing-brightgreen.svg)]()
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-orange.svg)]()
[![Coverage](https://img.shields.io/badge/coverage-98%25-green.svg)]()

> **PrismAI** is a high-performance, lightweight, edge-ready orchestration engine designed for running ultra-fast, multi-agent AI workflows with zero external dependencies.

---

## 🚀 Key Features

- **⚡ Sub-millisecond Overhead:** Built from the ground up using a highly-optimized asynchronous rust-core compiled to WebAssembly / Native.
- **🤖 Native Multi-Agent Orchestration:** Define complex hierarchies, peer-to-peer agent networks, and sequential/parallel chains with minimal declarative code.
- **🌐 Edge-Native:** Runs seamlessly in Cloudflare Workers, Vercel Edge, AWS Lambda, or embedded directly inside browser contexts.
- **🛡️ Type-Safe Declarations:** Complete end-to-end type safety for inputs, outputs, tool execution, and state transitions.
- **🔌 Pluggable Providers:** Out-of-the-box support for OpenAI, Anthropic, Cohere, local LLaMA instances, and custom self-hosted endpoints.

---

## 📦 Installation

Get started with **PrismAI** using your favorite package manager:

```bash
# Using npm
npm install @prism-ai/core

# Using pnpm (Recommended)
pnpm add @prism-ai/core

# Using yarn
yarn add @prism-ai/core
```

---

## 🛠️ Quick Start

Creating your first multi-agent team is as simple as defining agents, registering tools, and establishing a workflow topology.

```typescript
import { PrismEngine, Agent, Tool } from '@prism-ai/core';

// 1. Define a quick tool
const searchWeb = new Tool({
  name: "searchWeb",
  description: "Searches the web for up-to-date technological information",
  execute: async ({ query }) => {
    return `Results for: ${query} - PrismAI is trending!`;
  }
});

// 2. Define your specialized agents
const researcher = new Agent({
  name: "Researcher",
  role: "Lead Research Specialist",
  instructions: "Gather accurate data on current trends.",
  tools: [searchWeb]
});

const writer = new Agent({
  name: "Writer",
  role: "Technical Content Editor",
  instructions: "Synthesize findings from the Researcher into cohesive markdown summaries."
});

// 3. Initialize the Engine and orchestrate workflow
const engine = new PrismEngine({
  agents: [researcher, writer],
  topology: "sequential", // researcher -> writer
  verbose: true
});

// 4. Execute
const result = await engine.run({
  task: "Find the latest updates on Edge WebAssembly engines and summarize them."
});

console.log(result.output);
```

---

## 📐 Architecture Overview

PrismAI abstracts complex state-machine routing into a simple directed-acyclic-graph (DAG) architecture:

```
[User Task] ──> [ Orchestrator ] 
                       │
         ┌─────────────┴─────────────┐
         ▼                           ▼
   [Agent: Researcher] ◄───────► [Agent: Writer]
         │                           │
   [Tool: Search]              [Tool: Format]
         │                           │
         └─────────────┬─────────────┘
                       ▼
               [Structured Output]
```

---

## ⚙️ Configuration & Environment Variables

Create a `.env` file in your root folder:

```env
PRISM_API_KEY=your_prism_api_key_here
OPENAI_API_KEY=your_openai_key_here
ANTHROPIC_API_KEY=your_anthropic_key_here
PRISM_LOG_LEVEL=info
```

---

## 🧪 Running Tests

PrismAI has a comprehensive test suite using Vitest.

```bash
# Run unit tests
pnpm test

# Run coverage report
pnpm test:coverage
```

---

## 🤝 Contributing

We love contributions! Whether you're reporting a bug, suggesting a feature, or submitting a Pull Request, please follow these steps:

1. **Fork** the repository.
2. **Create** your feature branch: `git checkout -b feature/amazing-feature`.
3. **Commit** your changes: `git commit -m 'Add some amazing feature'`.
4. **Push** to the branch: `git push origin feature/amazing-feature`.
5. **Open** a Pull Request.

Please read our [Contributing Guidelines](CONTRIBUTING.md) and [Code of Conduct](CODE_OF_CONDUCT.md) before getting started.

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

---

<p align="center">
  Built with ❤️ by the PrismAI Open Source Community.
</p>
