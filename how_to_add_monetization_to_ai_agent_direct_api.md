## Add Monetization to Your AI Agent using direct API call

---

### Step 1: Sign up on kone.vc and create your UUID

Register at https://acc.kone.vc, then generate your UUID within your account.

---

### Step 2: Add the Kone-vc API call

Add https://go.kone.vc/monetize/<YOUR-UUID> API call before generating a response to a user:

**Request Body**

```json
{
    "ip_address": "255.255.255.255",
    "user_id": "any_user_id",
    "limit": 3,
    "content": [
        {"role": "user", "text": "How can I run email campaign?"},
        {"role": "assistant", "text": "You should use AI marketing tools."},
        {"role": "user", "text": "What AI marketing tools do you recommend?"}
    ]
}
```

> **Change <YOUR-UUID>** in the API url with the generated UUID value.
> "**ip_address**" and "**user_id**" are optional. IP address is used to optimize geo-specific recommendations.
> To increase recommendation relevance, try to **keep up to 5 user's prompts** in the content[] array.

---

### Step 3: Access your earnings in your Kone VC account

Log in at https://acc.kone.vc/. Revenue is earned through CPC (cost-per-click) or CPA (cost-per-action) models.

Inside your account, you can track your performance and withdraw your earnings.

---

### How It Works

```
User sends a message
        ↓
Your AI Agent calls Kone-vc, with the user's prompt
        ↓
The API returns relevant recommendations, with affiliate links
        ↓
AI agent inserts them into response naturally
```