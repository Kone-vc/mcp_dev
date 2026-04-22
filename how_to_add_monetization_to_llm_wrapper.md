## Add Monetization to Your LLM Wrapper in 2 Minutes

No coding required — just two additions to **your existing LLM API call**. It expands the response from LLM with relevant recommendations and affiliate links.

**Important**: the relevance of the links is verified by LLM. It provides the natural implementation of the recommendations into the response. 

---

### Step 1: Sign up on kone.vc and create your UUID

Register at https://acc.kone.vc, then generate your UUID within your account — all required tools are available there.

---

### Step 2: Add the Kone.vc MCP tool definition inside the LLM API call

In your LLM API request, include the MCP tool definition inside the `tools` array:

```json
"tools": [
  {
    "type": "mcp",
    "server_url": "https://go.kone.vc/monetize_wrapper",
    "server_label": "kone_recommendations",
    "server_description": "The MCP server is a recommendation context assistant. Its role is to support LLM by providing curated, reliable, and practical recommendation context from trusted external sources.",
    "require_approval": "never"
  }
]
```

> **Note:** Change uuid in the "server_url" with the generated value.  
> **Note:** Make sure tool calling is **not disabled** in your API request settings. Some SDKs or wrappers restrict tool use by default.

---

### Step 3: Update your "instruction" inside the LLM API call

Append the following text to your existing instruction (the `system` or `instructions` field):

```
Use the **get_recommendation** MCP tool to fetch recommendations relevant to the user's prompt before responding. Each recommendation should be presented as a link with a short description. Only include recommendations if relevant results are returned — omit the section entirely if none are found.
```

This tells your agent to fetch contextual recommendations before generating a response.

---

### Step 4: Add UUID into "input" parameter

Append `UUID: <YOUR_UUID>` text to the `input` parameter. 

It allows to bind your request to your account.

---

That's all. Now you can track your performance and withdraw your earnings inside your account at https://acc.kone.vc/.

Revenue is earned through CPC (cost-per-click) or CPA (cost-per-action) models.

---

### How It Works

```
User sends a message
        ↓
Your AI Agent calls LLM API, with the user's prompt and UUID
        ↓
LLM calls "get_recommendation" tool via Kone.vc MCP
        ↓
MCP returns relevant recommendations, with affiliate links
        ↓
LLM incorporates them into response naturally
        ↓
Your Agent print the response
```

---

### Full Example (OpenAI-compatible format)

**Request Body**
```json
{
  "input": "User's prompt, e.g. `Tell me about AI agents. UUID: b9dd1d89-4f24-4993-b5cc-112cdd986b1a`",
  "model": "gpt-5.4-mini",
  "instruction": "Use the **get_recommendation** MCP tool to fetch recommendations relevant to the user's prompt before responding. Each recommendation should be presented as a link with a short description. Only include recommendations if relevant results are returned — omit the section entirely if none are found.",
  "tools": [
    {
      "type": "mcp",
      "server_url": "https://go.kone.vc/monetize_wrapper",
      "server_label": "kone_recommendations",
      "server_description": "The MCP server is a recommendation context assistant. Its role is to support LLM by providing curated, reliable, and practical recommendation context from trusted external sources.",      
      "require_approval": "never"
    }
  ]
}
```

Change "input", "model" and UUID as required.

---

### Requirements

- Your LLM API must support **MCP (Model Context Protocol)** or tool calling (use **/responses** API)
- Tool calling must be **enabled** in your API configuration