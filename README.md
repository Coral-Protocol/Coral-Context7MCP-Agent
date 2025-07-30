## [Context7 MCP Agent](https://github.com/Coral-Protocol/Coral-Context7MCP-Agent)

The Context7 MCP Agent is capable of retrieving Context7-compatible library IDs and fetching specific documentation on various topics related to those libraries.

## Responsibility

The Context7 MCP Agent is capable of extracting library information and documentation from Context7-compatible libraries, generating code examples, and creating comprehensive documentation references tailored to specific programming languages and frameworks.

Below are the tools and their descriptions:

**resolve-library-id**: This tool searches for library names and returns Context7-compatible library IDs. It tracks the app and coding styles you're using for records. Usage: Ask "Find the library ID for React" or "Get the Context7 ID for MongoDB" to retrieve the exact library identifier needed for documentation queries. You can also search for specific versions by saying "Get the ID for Next.js version 14" or "Find the library ID for Supabase".

**get-library-docs**: This tool fetches targeted documentation with parameters for specific library ID, topic focus, and token limits. It tracks the app and coding styles for logging. Usage: Ask "Get documentation about React hooks" or "Show me MongoDB authentication docs" to retrieve specific documentation sections. You can specify topics like 'hooks', 'routing', 'authentication' and control documentation length with token limits. Just provide the library ID first, then ask for the specific topic you need help with.

## Details
- **Framework**: LangChain
- **Tools used**: Context7 MCP Server Tools, Coral Server Tools
- **AI model**: OpenAI GPT-4o
- **Date added**: June 4, 2025
- **Reference**: [Context 7 Repo](https://github.com/upstash/context7)
- **License**: MIT

## Setup the Agent

### 1. Clone & Install Dependencies

<details>

Ensure that the [Coral Server](https://github.com/Coral-Protocol/coral-server) is running on your system. If you are trying to run Open Deep Research agent and require an input, you can either create your agent which communicates on the coral server or run and register the [Interface Agent](https://github.com/Coral-Protocol/Coral-Interface-Agent) on the Coral Server  


```bash
# In a new terminal clone the repository:
git clone https://github.com/Coral-Protocol/Coral-Context7MCP-Agent.git

# Navigate to the project directory:
cd Coral-Context7MCP-Agent

# Download and run the UV installer, setting the installation directory to the current one
curl -LsSf https://astral.sh/uv/install.sh | env UV_INSTALL_DIR=$(pwd) sh

# Create a virtual environment named `.venv` using UV
uv venv .venv

# Activate the virtual environment
source .venv/bin/activate

# install uv
pip install uv

# Install dependencies from `pyproject.toml` using `uv`:
uv sync
```

</details>

### 2. Configure Environment Variables

<details>

Get the API Key:
[OpenAI](https://platform.openai.com/api-keys)

```bash
# Create .env file in project root
cp -r .env_sample .env
```

Check if the .env file has correct URL for Coral Server and adjust the parameters accordingly.

</details>

## Run the Agent

You can run in either of the below modes to get your system running.  

- The Executable Model is part of the Coral Protocol Orchestrator which works with [Coral Studio UI](https://github.com/Coral-Protocol/coral-studio).  
- The Dev Mode allows the Coral Server and all agents to be separately running on each terminal without UI support.  

### 1. Executable Mode

Checkout: [How to Build a Multi-Agent System with Awesome Open Source Agents using Coral Protocol](https://github.com/Coral-Protocol/existing-agent-sessions-tutorial-private-temp) and update the file: `coral-server/src/main/resources/application.yaml` with the details below, then run the [Coral Server](https://github.com/Coral-Protocol/coral-server) and [Coral Studio UI](https://github.com/Coral-Protocol/coral-studio). You do not need to set up the `.env` in the project directory for running in this mode; it will be captured through the variables below.

<details>

For Linux or MAC:

```bash

registry:
  # ... your other agents
  context7_mcp_agent:
    options:
      - name: "MODEL_API_KEY"
        type: "string"
        description: "API key for the service"
      - name: "MODEL_NAME"
        type: "string"
        description: "What model to use (e.g 'gpt-4.1')"
        default: "gpt-4.1"
      - name: "MODEL_PROVIDER"
        type: "string"
        description: "What model provider to use (e.g 'openai', etc)"
        default: "openai"
      - name: "MODEL_MAX_TOKENS"
        type: "string"
        description: "Max tokens to use"
        default: "16000"
      - name: "MODEL_TEMPERATURE"
        type: "string"
        description: "What model temperature to use"
        default: "0.3"
    runtime:
      type: "executable"
      command: ["bash", "-c", "<replace with path to this agent>/run_agent.sh main.py"]
      environment:
        - option: "MODEL_API_KEY"
        - option: "MODEL_NAME"
        - option: "MODEL_PROVIDER"
        - option: "MODEL_MAX_TOKENS"
        - option: "MODEL_TEMPERATURE"
```
For Windows, create a powershell command (run_agent.ps1) and run:

```bash
command: ["powershell","-ExecutionPolicy", "Bypass", "-File", "${PROJECT_DIR}/run_agent.ps1","main.py"]
```

</details>

### 2. Dev Mode

Ensure that the [Coral Server](https://github.com/Coral-Protocol/coral-server) is running on your system and run below command in a separate terminal.

<details>

```bash
# Run the agent using `uv`:
uv run python main.py
```

You can view the agents running in Dev Mode using the [Coral Studio UI](https://github.com/Coral-Protocol/coral-studio) by running it separately in a new terminal.

</details>


## Example

<details>

```bash
# Input:
Context7 MCP instruction

# Output:
The desired output from the Context7 MCP execution
```

</details>

### Creator Details
- **Name**: Suman Deb
- **Affiliation**: Coral Protocol
- **Contact**: [Discord](https://discord.com/invite/Xjm892dtt3)

