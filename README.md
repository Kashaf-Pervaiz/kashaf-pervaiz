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
