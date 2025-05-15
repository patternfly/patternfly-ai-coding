# PatternFly Cursor Setup

This repository accelerates PatternFly application development using [Cursor](https://cursor.sh/) by leveraging the `patternfly-react-seed` project, a dedicated Cursor rule, and contextual information files.

## Goal

The primary aim is to provide a streamlined, consistent, and AI-enhanced starting point for developing PatternFly applications with Cursor, ensuring best practices are easily accessible and applicable.

## Core Components

*   **Cursor Rule (`.cursor/rules/patternfly-react-seed-setup.mdc`):** Guides AI and users through `patternfly-react-seed` setup, development best practices (including PatternFly Chatbot implementation), and general PatternFly UI construction.
*   **Context Files:**
    *   `patternfly-chatbot.txt`: Provides rich context for AI-assisted PatternFly Chatbot development.
    *   `patternfly-react-component-groups.txt`: Offers information on PatternFly React Component Groups.
*   Include detailed steps and considerations for implementing the PatternFly Chatbot, heavily utilizing `patternfly-chatbot.txt`.
*   Suggest indexing relevant PatternFly documentation for enhanced AI awareness.

## Quick Start

1.  **Prerequisites:**
    *   [Cursor](https://cursor.sh/) installed.
    *   Node.js and npm installed (or `nvm` active). The Cursor rule includes environment checks.

2.  **Clone This Repository:**
    ```bash
    git clone https://github.com/nicolethoen/patternfly-cursor-setup.git
    cd patternfly-cursor-setup
    ```

3.  **Open in Cursor:**
    *   Open the `patternfly-cursor-setup` directory as your project in Cursor.

4.  **Initiate Setup with AI:**
    *   The AI assistant will be aware of the project's rule and context files.
    *   **Example Prompt:** Tell the AI:
        ```
        "Use the 'patternfly-react-seed-setup' rule to start a new PatternFly project."
        ```
    *   **AI Guidance:** The AI will then guide you through:
        *   Cloning the `patternfly-react-seed` repository.
        *   Performing Node.js/npm environment checks.
        *   Installing dependencies for `patternfly-react-seed`.
        *   Starting the `patternfly-react-seed` development server (recommended in a separate terminal).

5.  **Develop Your PatternFly Application:**
    *   With `patternfly-react-seed` running, continue leveraging the AI, guided by the rule and context files, to build UI components and features.

## About the `patternfly-react-seed-setup.mdc` Rule

This central rule file is designed to:

*   Automate and guide the initial environment and `patternfly-react-seed` project scaffolding.
*   Provide instructions for launching the development server.
*   Offer PatternFly development best practices (e.g., class naming, utility CSS usage).
*   Include detailed steps and considerations for implementing the PatternFly Chatbot, heavily utilizing `patternfly-chatbot.txt`.
*   Suggest indexing relevant PatternFly documentation for enhanced AI awareness.
