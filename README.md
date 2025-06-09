# PatternFly AI Coding Support

This repository provides indexed documentation and contextual resources to support any AI model while coding with PatternFly. Its purpose is to make best practices, guidelines, and component documentation easily accessible for AI-assisted development—whether you use Cursor, Copilot, ChatGPT, or any other AI coding tool.

## Goal

The primary aim is to offer a comprehensive, AI-friendly knowledge base and starting point for developing PatternFly applications. By indexing relevant documentation and providing context files, this repo ensures that any AI model can deliver accurate, consistent, and best-practice guidance while you code.

## Core Components

The core components of this repository are the README and markdown files found throughout the project. These files provide indexed documentation, guidelines, and best practices to support AI-assisted PatternFly development, regardless of which AI coding tool you use.

> **Recommendation:**
> When using any AI coding tool, always instruct it to reference the README and markdown documentation in this repository while generating PatternFly code. This ensures the code follows best practices, guidelines, and the latest standards indexed here.

> **Tip:**
> For the most up-to-date PatternFly documentation, consider using the context7 MCP server as a documentation source. It provides the latest PatternFly resources for AI-assisted coding and ensures your code leverages current APIs and best practices.

> **How to set up context7 MCP server:**
> 1. Ensure you have Node.js v18+ and an MCP-compatible client (e.g., Cursor, VS Code with MCP extension, Windsurf, Claude Desktop).
> 2. Add context7 as an MCP server in your client's configuration. For example, in Cursor, add this to your `~/.cursor/mcp.json`:
>    ```json
>    {
>      "mcpServers": {
>        "context7": {
>          "command": "npx",
>          "args": ["-y", "@upstash/context7-mcp@latest"]
>        }
>      }
>    }
>    ```
> 3. Save and restart your client/editor.
> 4. For more details and setup instructions for other editors, see the official guide: https://github.com/upstash/context7#installation