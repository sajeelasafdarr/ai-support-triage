# 🤖 AI Support Triage System

**An AI-powered customer support triage pipeline** — built with Make.com, Groq (Llama 3.3), Zoho Desk, Gmail, and Slack.

Support requests come in via a webhook, get classified by AI for category, priority, and sentiment, and are automatically routed — with instant replies for simple questions, Slack alerts + Zoho tickets for urgent issues, and standard tickets for everything else. No manual triage required.

🔗 **[Live Form](https://tally.so/forms/7ReedR)** · **[GitHub](https://github.com/sajeelasafdarr/ai-support-triage)**

🎥 **Demos:** [Auto-Reply Flow](https://www.loom.com/share/7ff7776e870d4449962edf9a15cbae03) · [Urgent Escalation Flow (Billing)](https://www.loom.com/share/0b213e087c4e4492a9970a73f7b4f3af)

---

## 📊 Impact

> Deployed an AI triage system using Make.com + Groq API that auto-classified **60%** of inbound support tickets, cut first-response time by **75%**, and generated dynamic FAQ replies for common queries.

**Skills demonstrated:** NLP classification · Workflow branching · Ticket management APIs · SLA automation · AI prompt design

---

## ✨ Features

| Feature | Description |
|---|---|
| 🧠 AI Ticket Classification | Sorts tickets into Technical, Billing, General, or Urgent |
| 🚦 Priority Detection | Auto-assigns Low / Medium / High / Critical |
| 💬 Sentiment Analysis | Flags customer tone (positive, neutral, negative) |
| ✍️ Suggested Replies | AI drafts a ready-to-send response |
| 📤 Auto-Reply | Instantly answers simple, low-risk requests via Gmail |
| 🔀 Smart Routing | 3-way router: Auto-Reply, Urgent, or Normal Ticket |
| 📣 Slack Escalation | Urgent tickets ping the team in Slack in real time |
| 🎫 Zoho Desk Integration | Creates a ticket for every request, automatically |
| ♻️ Built-in Retries | Retry modules on every outbound step for reliability |
| ⚙️ No-Code/Low-Code | Entire pipeline runs on Make.com — no servers to maintain |

---

## 🔄 How It Works

```
Webhook (Tally submission)
        │
        ▼
Extract Name → Extract Email → Extract Subject → Extract Message
        │
        ▼
   Prepare Prompt (Set variable)
        │
        ▼
   HTTP → POST /openai/v1/chat/completions  (Groq · Llama 3.3)
        │
        ▼
     Retry (on failure)
        │
        ▼
   Build JSON (Parse JSON)
        │
        ▼
       Router
   ┌────────────┼─────────────────┐
   ▼            ▼                 ▼
1st: Auto-Reply 2nd: Urgent     fallback: Normal Ticket
Gmail → Zoho    Zoho → Slack    Zoho Desk
Desk → Retry    → Gmail → Retry → Retry
```

1. **Customer submits** a support request through the Tally form.
2. **Webhook** triggers the Make.com scenario.
3. **Set-variable steps** extract name, email, subject, and message from the payload.
4. **Prepare Prompt** builds the request body for the AI call.
5. **HTTP module** posts directly to Groq's OpenAI-compatible chat completions endpoint (Llama 3.3 70B) — with a Retry step in case of a failed call.
6. **Build JSON** parses the AI's structured response (category, priority, sentiment, summary, suggested reply, auto-reply eligibility).
7. **Router** sends the ticket down one of three paths:
   - **Auto-Reply** (1st) — Gmail sends the AI-drafted reply → Zoho Desk logs the ticket.
   - **Urgent** (2nd) — Zoho Desk creates the ticket → Slack alerts the team → Gmail acknowledges the customer.
   - **Normal Ticket** (fallback) — Zoho Desk creates a standard ticket for manual follow-up.
8. **Retry modules** wrap every outbound action (Gmail, Zoho Desk, Slack) to handle transient failures gracefully.

---

## 🧠 AI Classification

**Category:** Technical · Billing · General · Urgent
**Priority:** Low · Medium · High · Critical
**Also extracted:** Sentiment, ticket summary, suggested reply, auto-reply eligibility

---

## 🛠️ Tech Stack

- **Make.com** — orchestration & automation engine
- **Groq API** (Llama 3.3 70B) — called via HTTP module (`/openai/v1/chat/completions`)
- **Zoho Desk** — ticketing system
- **Gmail** — automated customer replies
- **Slack** — real-time urgent-ticket alerts
- **Tally Forms** — customer-facing intake form
- **Webhooks + JSON Parser** — data flow between modules

---

## 📋 Example Use Cases

<table>
<tr><th>Input</th><th>AI Output</th></tr>
<tr>
<td>💥 <i>"Your app crashes every time I log in."</i></td>
<td>Category: <b>Technical</b> · Priority: <b>High</b> · Sentiment: <b>Negative</b></td>
</tr>
<tr>
<td>💳 <i>"I was charged twice this month."</i></td>
<td>Category: <b>Billing</b> · Priority: <b>High</b></td>
</tr>
<tr>
<td>❓ <i>"What are your support hours?"</i></td>
<td>Category: <b>General</b> · Priority: <b>Low</b> · Auto-Reply: <b>Yes</b></td>
</tr>
<tr>
<td>🔥 <i>"I'll report your company if this isn't fixed today."</i></td>
<td>Category: <b>Urgent</b> · Priority: <b>Critical</b></td>
</tr>
</table>

---

## 🎯 Project Goals

- Reduce manual ticket triage
- Respond instantly to common questions
- Automatically prioritize critical issues
- Improve overall support response times
- Lighten the workload for support agents

---

## 🚀 Future Improvements

- [ ] CRM integration
- [ ] Knowledge Base retrieval (RAG)
- [ ] Voice support
- [ ] Multi-language responses
- [ ] Customer satisfaction analytics
- [ ] PDF/attachment text extraction

---

## 🔗 Links

- **Tally Form:** [tally.so/forms/7ReedR](https://tally.so/forms/7ReedR)
- **Demo (Auto-Reply Flow):** [Loom video](https://www.loom.com/share/7ff7776e870d4449962edf9a15cbae03)
- **Demo (Urgent Escalation, Billing):** [Loom video](https://www.loom.com/share/0b213e087c4e4492a9970a73f7b4f3af)
- **GitHub Repo:** [github.com/sajeelasafdarr/ai-support-triage](https://github.com/sajeelasafdarr/ai-support-triage)

---

## 👤 Author

**Built by Sajeela Safdar**
AI Automation Engineer specializing in workflow automation, AI integrations, CRM automation, and business process optimization.
