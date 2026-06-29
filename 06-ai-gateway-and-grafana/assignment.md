---
slug: ai-gateway-and-grafana
id: 3tzxvs9r5y4e
type: challenge
title: AI Gateway — audit, attribution & Grafana
teaser: Answer "who did what, when, why" in the Coder UI and a Grafana dashboard.
notes:
- type: text
  contents: |
    <style>@keyframes coder-blink{50%{opacity:0}}.coder-blink::after{content:'';display:inline-block;width:0.5em;height:1em;background:currentColor;margin-left:8px;vertical-align:text-bottom;animation:coder-blink 1.1s steps(1) infinite;}</style>
    <div style="background:#18171A;color:#FFFFFF;font-family:Geist,system-ui,-apple-system,'Segoe UI',sans-serif;text-align:center;padding:56px 32px;border-radius:4px;">
      <svg viewBox="0 0 425.93 200" width="96" style="display:block;margin:0 auto 24px;" xmlns="http://www.w3.org/2000/svg"><g fill="#FFFFFF"><rect x="263.75" y="5.41" width="162.18" height="189.24"/><path d="M0,100C0,38.92,51.89,0,123.25,0s111.35,33.78,112.7,83.51l-61.62,1.89c-1.62-27.57-26.03-45.68-51.08-45.14-34.32.74-59.73,23.51-59.73,59.73s25.41,58.65,59.73,58.65c25.05,0,48.91-17.3,51.62-44.86l61.62,1.35c-1.62,50.54-44.05,84.87-113.24,84.87S0,160.81,0,100Z"/></g></svg>
      <div style="font-family:'Geist Mono',ui-monospace,Menlo,Consolas,monospace;font-size:12px;letter-spacing:0.04em;text-transform:uppercase;color:#A19CC8;margin-bottom:14px;">Challenge 06 &middot; AI Gateway audit</div>
      <div class="coder-blink" style="font-size:34px;font-weight:500;letter-spacing:-0.01em;line-height:1.12;margin-bottom:16px;">Every prompt. Audited.</div>
      <div style="color:rgba(255,255,255,0.72);font-size:17px;max-width:560px;margin:0 auto;line-height:1.6;">Read the full audit trail — attributed to your GitHub identity — in Coder's AI Sessions and a Grafana dashboard.</div>
    </div>
tabs:
- id: s1u9ykzgntd2
  title: Coder
  type: service
  hostname: workshop
  path: /
  port: 80
- id: t6m0bneqp5gd
  title: Grafana
  type: service
  hostname: workshop
  path: /d/coder-ai-gateway
  port: 3001
difficulty: intermediate
timelimit: 0
lab_config:
  default_layout_sidebar_size: 0
enhanced_loading: null
---

<span style="font-family:'Geist Mono',ui-monospace,Menlo,Consolas,monospace;font-size:12px;letter-spacing:0.04em;text-transform:uppercase;color:#A19CC8;">Coder Agents &middot; 06 — AI Gateway audit</span>

Everything you just did flowed through the **AI Gateway** — the controls layer of the AI Governance Add-On. Every prompt, every model call, every tool invocation, and every token was intercepted and recorded against your identity. This is the answer to the question every CISO and compliance team asks: *who ran what, when, and why?* You'll read that answer twice — once in the Coder UI for forensic depth, once in Grafana for the exec-friendly view.

---

<h2 style="color: #7511E2; font-weight: 500;">Step 1: Open AI Sessions in Coder</h2>

In the **Coder** tab, open **Admin settings → AI Sessions** (the gateway's session list). Each row is one session:
<img src="https://play.instruqt.com/assets/tracks/1sxii7ayovnx/7a1c5ac75e7caf3a5b9bf9b0def46dd2/assets/admin-ai-sesh.gif" width="200"></img>
- **initiator** — your own GitHub identity, not a shared service account
- **provider** — shown as the model vendor (e.g. **Anthropic**); every call still routes through the gateway to Bedrock
- **client** (Coder Agents), last prompt, token usage, thread count, and tool-call count

Then drill in:

1. Click a session, then expand a step to see its **agentic loop** — the **tool calls**, **token usage**, timing, and any **errors**.
2. Click **Back** (top-left) to return to the list.

The tools depend on the work: Challenge 1's issue scan shows the **GitHub MCP server**; the Challenge 2–4 coding work shows the **workspace tools** used to edit and push. This is the forensic record — it tells you whether an action came from a human prompt or a model decision.

---

<h2 style="color: #7511E2; font-weight: 500;">Step 2: Filter by user, client, and model</h2>

Back on the AI Sessions list, use the filters to slice the audit trail:

- by **user** (the initiator)
- by **client** (here, Coder Agents)
- by **model** (Claude Sonnet 4.6, Haiku 4.5, or gpt-oss-120b — two providers, one governed gateway)
- plus free-text **search**, and a **Filters** toggle for **All sessions** vs **My sessions**

Leave it on **All sessions** and notice you see *everyone's* activity — your own GitHub identity right beside the **CI service identity** from Challenge 4. Human and machine usage side by side, attributable to a specific initiator, is the auditor's whole job. In a real deployment with many developers and tools (Coder Agents plus Cursor, Claude Code, Codex…) pointed at the same gateway, this is how a platform team audits AI usage org-wide from one place.

---

<h2 style="color: #7511E2; font-weight: 500;">Step 3: See it visually in Grafana</h2>

Open the **Grafana** tab — it lands directly on the **Coder AI Gateway — Audit & Attribution** dashboard.

[button label="Open the Grafana dashboard"](tab-1)

> [!NOTE]
> If the dashboard is slow to load on first open, give it a few seconds and refresh — Grafana provisions it at startup.

This is Coder's **official AI Gateway dashboard**, reading the audit tables directly and rendering the same story for an exec audience:

- **usage leaderboards** — tokens per user, top models, top clients
- an **approximate cost table** — token usage joined against live model pricing
- **interceptions over time**
- a **prompts & tool-calls** detail table

Every row is attributed to a real **GitHub username**, and you can filter by user, provider, model, and time.

> [!NOTE]
> If a panel shows "No data," it just means the gateway hasn't recorded an interception attributable to your account yet. Send one quick prompt through the Agents chat (any prompt will do) and refresh the dashboard — your activity from Challenges 2–4 should already be there.

---

<h2 style="color: #7511E2; font-weight: 500;">Step 4: Confirm the audit trail is populated</h2>

When you can see your own activity in either the Coder AI Sessions view or the Grafana dashboard, click **Check**. It confirms the AI Gateway recorded at least one request attributable to this sandbox.

---

✅ Centralized credentials, full attribution, visual audit. You've now seen the complete Coder Agents + AI Governance story — from the agent loop in the control plane to the audit trail in Grafana. Click **Check** to finish.
