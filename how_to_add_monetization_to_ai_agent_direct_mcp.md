## Add Monetization to Your AI Agent using MCP server

Give your customers intention-based recommendations, with URLs and descriptions, and start earning.

---

### Step 1: Sign up on kone.vc and create your UUID

Register at https://acc.kone.vc, then generate your UUID within your account — all required tools are available there.

---

### Step 2: Connect to Kone.vc MCP server

```json
{
  "mcpServers": {
    "kone_monetizer": {
      "url": "https://go.kone.vc/monetize_agent",
    }
  }
}
```

---

### Step 3: Run "get_recommend" MCP tool

```json
{
    "id": 0,
    "method": "tools/call",
    "params": {
      "name": "get_recommendation",
      "arguments": {
        "uuid": "YOUR_UUID",
        "prompt": "USER PROMPT"     
      }
    }
}
```

Response contains array of recommendations, with URLs and descriptions. Translate these recommendations to your users.

```json
{
    "id": 0,
    "jsonrpc": "2.0",
    "result": {
        "structuredContent": {
            "recommendation_links": [
                {
                    "url_description": "Service 1 description",
                    "url_title": "Service 1 title",
                    "url_value": "Service 1 url"
                }
            ]
        }
    }
}
```

---

### Step 4: Access your earnings in your Kone VC account

Log in at https://acc.kone.vc/. Revenue is earned through CPC (cost-per-click) or CPA (cost-per-action) models.

Inside your account, you can track your performance and withdraw your earnings.

---

### How It Works

```
User sends a message
        ↓
Your AI Agent calls "get_recommend" MCP tool
        ↓
MCP returns relevant recommendations, with affiliate links
        ↓
Your Agent print the response
```