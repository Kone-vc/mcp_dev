## Fetch recommendation links based on the user's intentions

Add just one call to your favourite LLM (Claude, ChatGPT, etc). It responses with relevant recommendations and affiliate links based on the user's prompt.

**Important**: the relevance of the links is verified by LLM. It provides the natural implementation of the recommendations into the response. 

---

### Step 1: Sign up on kone.vc and create your UUID

Register at https://acc.kone.vc, then generate your UUID within your account — all required tools are available there.

---

### Step 2: Add the /responses LLM API call

#### Response with plain text:

POST https://api.openai.com/v1/responses

**Headers**  
  Authorization Bearer ```YOUR-LLM-API-KEY```

**Request Body**
```json
{
  "input": "User's prompt, e.g. `Tell me about AI agents`",
  "model": "gpt-5.4-mini",
  "tools": [
    {
      "type": "mcp",
      "server_url": "https://go.kone.vc/recommend_<your-uuid>",
      "server_label": "kone_recommendations",
      "server_description": "The MCP server is a recommendation context assistant. Its role is to support LLM by providing curated, reliable, and practical recommendation context from trusted external sources.",
      "require_approval": "never"
    }
  ],
  "reasoning": {
    "effort": "none"
  },
  "tool_choice": "auto",
  "instructions": "Use the get_recommendations MCP tool to fetch recommendations relevant to the user's prompt before responding. Each recommendation should be presented as a link with a short description. Only include recommendations if relevant results are returned — omit the section entirely if none are found.",
  "service_tier": "default",
  "max_tool_calls": 1
}
```

#### Response with Structured Output (SO):

POST https://api.openai.com/v1/responses

**Headers**
  Authorization Bearer ```YOUR-LLM-API-KEY```

**Request Body**
```json
{
  "input": "User's prompt, e.g. `Tell me about AI agents`",
  "model": "gpt-5.4-mini",
  "tools": [
    {
      "type": "mcp",
      "server_url": "https://go.kone.vc/recommend_<your-uuid>",
      "server_label": "kone_recommendations",
      "server_description": "The MCP server is a recommendation context assistant. Its role is to support LLM by providing curated, reliable, and practical recommendation context from trusted external sources.",
      "require_approval": "never"
    }
  ],
  "reasoning": {
    "effort": "none"
  },
  "tool_choice": "auto",
  "instructions": "Use the get_recommendations MCP tool to fetch recommendations relevant to the user's prompt before responding. Each recommendation should be presented as a link with a short description. Only include recommendations if relevant results are returned — omit the section entirely if none are found.",
  "service_tier": "default",
  "max_tool_calls": 1,
  "text": {
    "format": {
      "name": "recommendation_links",
      "type": "json_schema",
      "schema": {
        "type": "object",
        "required": [
          "recommendation_links"
        ],
        "properties": {
          "recommendation_links": {
            "type": "array",
            "items": {
              "type": "object",
              "required": [
                "url_value",
                "url_title",
                "url_description"
              ],
              "properties": {
                "url_title": {
                  "type": "string"
                },
                "url_value": {
                  "type": "string"
                },
                "url_description": {
                  "type": "string"
                }
              },
              "additionalProperties": false
            },
            "description": "extract array of relevant recommendation links from get_recommendations MCP tool response."
          }
        },
        "additionalProperties": false
      }
    }
  }
}
```

> **Note:** Change "input", "model" and uuid in the "server_url" as you like.  
> **Note:** Use your own API key for ChatGPT or another LLM.  
> **Note:** Make sure tool calling is **not disabled** in your API request settings. Some SDKs or wrappers restrict tool use by default.

#### Full description of the **/responses** call

- [ChatGPT](https://developers.openai.com/api/reference/resources/responses/methods/create)
- [Claude](https://platform.claude.com/docs/en/api/openai-sdk)

---

### Step 3: Deliver the recommendations to users or AI agents

Use any convenient way to deliver the recommendations.

---

### Step 4: Access your earnings in your Kone VC account

Log in at https://acc.kone.vc/. Revenue is earned through CPC (cost-per-click) or CPA (cost-per-action) models.

Inside your account, you can track your performance and withdraw your earnings.

---

### How It Works

```
User/Agent sends a message
        ↓
Your AI Agent calls LLM API, with the user's prompt
        ↓
LLM calls "get_recommendations" tools via Kone.vc MCP
        ↓
MCP returns relevant recommendations, with affiliate links
        ↓
LLM incorporates them into response naturally
        ↓
Your Agent print the response
```

---

### Requirements

- Your LLM API must support **MCP (Model Context Protocol)** or tool calling (use /responses API)
- Tool calling must be **enabled** in your API configuration
- No registration needed to get started
