# Claude Code Skill: Submit Agent to Eliza.FYI

This document defines the automated workflow for Claude Code to submit AI agent configurations to the Eliza.FYI marketplace.

## Skill Overview
**Name:** `submit_eliza_agent`
**Goal:** Automate the submission of an agent's metadata to the Eliza.FYI backend API.
**Endpoint:** `https://api.eliza.fyi/api/agent/submit`
**Method:** `POST`

## Implementation Logic

When a user requests to "submit", "publish", or "list" an agent, Claude should follow these steps:

### 1. Information Gathering
Extract or prompt the user for the following required fields:
- **Name:** The display name of the agent.
- **Username:** A unique handle (alphanumeric and underscores).
- **Bio:** A text description of the agent's personality and purpose.
- **Avatar URL:** A direct link to an image file (PNG/JPG).
- **External URL:** The ElizaCloud chat interface link (e.g., `https://www.elizacloud.ai/dashboard/chat?characterId=...`).

### 2. Payload Construction
Format the gathered data into the following JSON structure:

```json
{
  "name": "Agent Name",
  "username": "agent_handle",
  "bio": "Agent biography text...",
  "avatarUrl": "https://example.com/path/to/image.png",
  "externalUrl": "https://www.elizacloud.ai/dashboard/chat?characterId=...",
  "topics": ["Community", "External"],
  "style": {
    "all": [],
    "chat": [],
    "post": []
  }
}
```

### 3. Execution Command
Claude can execute the submission using a `curl` command via `run_shell_command`:

```bash
curl -X POST https://api.eliza.fyi/api/agent/submit \
     -H "Content-Type: application/json" \
     -d 
{
           "name": "...",
           "username": "...",
           "bio": "...",
           "avatarUrl": "...",
           "externalUrl": "..."
         }
```

### 4. Verification
- **Success (200 OK):** Inform the user that the agent has been successfully listed.
- **Error (400/500):** Parse the error message and assist the user in fixing the missing or invalid fields.

## Usage Example for Claude
"Claude, please submit my agent 'Satoshi' with username 'satoshi_ Nakamoto', bio 'Founder of Bitcoin', avatar 'https://bit.ly/satoshi-img', and chat link 'https://www.elizacloud.ai/chat?id=123' to the marketplace."
