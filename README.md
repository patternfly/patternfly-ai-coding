# PatternFly Cursor Setup

This repository provides a curated setup to kickstart PatternFly application development using [Cursor](https://cursor.sh/) and the `patternfly-react-seed` project. It includes:

*   **Cursor Rules:** A detailed rule file (`.cursor/rules/patternfly-react-seed-setup.mdc`) that guides the AI assistant (and the user) through the entire setup process for `patternfly-react-seed`, including environment checks, cloning, dependency installation, starting the development server, and best practices for PatternFly development (like class naming, using utility classes, and chatbot implementation).
*   **Context Files:**
    *   `patternfly-chatbot.txt`: Provides extensive context about the PatternFly chatbot components, structure, and API, used by the AI to assist with chatbot implementation.
    *   `patternfly-react-component-groups.txt`: Offers context on PatternFly React Component Groups.

## Purpose

The main goal of this repository is to provide a shared, version-controlled environment that makes it easy for developers to:
1.  Get a `patternfly-react-seed` project up and running quickly.
2.  Leverage Cursor's AI capabilities with pre-configured rules and rich context for PatternFly development.
3.  Ensure a consistent setup and development approach when working with PatternFly and Cursor, especially for features like the chatbot.

## How to Use This Setup

1.  **Prerequisites:**
    *   Ensure you have [Cursor](https://cursor.sh/) installed.
    *   Ensure you have Node.js and npm (or a Node version manager like `nvm`) installed and configured in your environment. The included Cursor rule has detailed steps for this.

2.  **Clone this Repository:**
    ```bash
    git clone <your-repository-url-here>
    cd patternfly-cursor-setup
    ```

3.  **Open in Cursor:**
    *   Open the `patternfly-cursor-setup` directory as your project in Cursor.

4.  **Interact with the AI Assistant:**
    *   The AI assistant will automatically be aware of the rules in the `.cursor/rules/` directory and the attached context files (`patternfly-chatbot.txt`, `patternfly-react-component-groups.txt`).
    *   **Start the process:** You can instruct the AI to begin the setup. For example, say:
        ```
        "I'd like to vibe code a PatternFly UI using the patternfly-react-seed setup rule."
        ```
        or
        ```
        "Let's use the 'patternfly-react-seed-setup' rule to start a new PatternFly project."
        ```
    *   **Follow the AI's guidance:** The AI will then use the `patternfly-react-seed-setup.mdc` rule to guide you (and itself) through:
        *   Cloning the `patternfly-react-seed` repository (this will be a new directory, likely inside `patternfly-cursor-setup` or wherever you choose).
        *   Ensuring your Node.js/npm environment is ready.
        *   Installing dependencies for `patternfly-react-seed`.
        *   Starting the `patternfly-react-seed` development server (the rule recommends you do this in a separate terminal for best visibility).
        *   Optionally, indexing PatternFly documentation and code repositories within Cursor for enhanced AI context.

5.  **Develop your PatternFly Application:**
    *   Once the `patternfly-react-seed` project is running, you can continue to work with the AI assistant to build UI components, implement features (like the chatbot, using the specific guidance in the rule), and modify the application. The rule also contains general PatternFly development best practices and troubleshooting tips learned during its creation.

## The `patternfly-react-seed-setup.mdc` Rule

This core rule file guides the setup and development process. Key aspects include:
*   Environment prerequisite checks (Node.js, npm, nvm).
*   Step-by-step cloning of `patternfly-react-seed`.
*   Dependency installation.
*   Instructions for starting the development server, with a recommendation for the user to run it in a separate terminal.
*   Troubleshooting tips for common setup issues.
*   Guidelines for indexing external PatternFly documentation and source code for Cursor's context.
*   General PatternFly development best practices (class naming, utility CSS).
*   Specific, detailed instructions for implementing the PatternFly Chatbot, including:
    *   Prioritizing the `patternfly-chatbot.txt` context file.
    *   Using `@patternfly/chatbot` as the package.
    *   Guidance on import paths (especially dynamic imports for sub-components).
    *   Recommendations to use official PatternFly demo code snippets when available.
    *   CSS import and `stylePaths.js` considerations.
    *   References to official PatternFly demo pages for different chatbot styles (basic, embedded).

By following this setup, you and your team can benefit from a consistent, AI-assisted start to your PatternFly projects.