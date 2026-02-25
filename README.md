# ai-agent-n8n
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

Then open your browser and go to:
```
http://localhost:5678
```

You'll see the n8n interface. Create a free account (local, no cloud needed).

---

## Step 3: Your First AI Agent in n8n

We'll build a **"Research Assistant Agent"** that:
- Takes a question from you
- Thinks about it using an LLM (Groq is free & fast!)
- Searches the web for current info
- Gives you a summarized answer

### Get your free Groq API key:
Go to → [console.groq.com](https://console.groq.com) → Sign up → Create API Key → Copy it

### Build the workflow in n8n:

**Click "New Workflow" then add these nodes in order:**
```
[Chat Trigger] → [AI Agent] → [Groq LLM] + [Tools]
```

**Node by node:**

**1. Chat Trigger**
- Click `+` → search "Chat Trigger"
- This is your input — where you type questions
- No config needed, just add it

**2. AI Agent**
- Click `+` → search "AI Agent"
- Connect it to Chat Trigger
- This is the "brain" that decides what to do

**3. Connect Groq as the LLM**
- Inside AI Agent → click "Language Model" → select "Groq"
- Add credentials → paste your Groq API key
- Model: `llama-3.3-70b-versatile` (free, very capable)

**4. Add Tools to your Agent**
- Inside AI Agent → click "Add Tool"
- Add **"Wikipedia"** tool (built-in, no key needed)
- Add **"Calculator"** tool (built-in)

Your workflow looks like this:
```
[Chat Trigger]
      ↓
  [AI Agent] ←→ [Groq LLM]
      ↓              ↓
  [Wikipedia]   [Calculator]
      ↓
  [Answer back to user]
```

**5. Test it!**
- Click "Chat" button in n8n
- Ask: *"What is the latest news about AI agents?"*
- Watch it think → use Wikipedia → give you an answer 🎉

---

## Step 4: Push to GitHub

Once it works, export your workflow:
- Go to workflow → `...` menu → **Download**
- It saves as a `.json` file

Create a GitHub repo called `ai-agent-n8n` and add:
```
ai-agent-n8n/
├── README.md          ← explain what it does
├── workflow.json      ← your n8n workflow export
└── screenshots/       ← screenshot of your workflow
    └── agent-demo.png


# AI Research Assistant Agent 🤖

Built with n8n + Groq (LLaMA 3.3 70B)

## What it does
- Answers questions using AI reasoning
- Searches Wikipedia for real-time info
- Performs calculations automatically

## Tech Stack
- n8n (workflow orchestration)
- Groq API (LLaMA 3.3 70B) 
- Docker
- Tools: Wikipedia, Calculator

## How to run
1. Install Docker
2. Run: docker run -it -p 5678:5678 n8nio/n8n
3. Import workflow.json
4. Add your Groq API key