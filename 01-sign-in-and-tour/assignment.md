---
slug: sign-in-and-tour
id: 81adbmhftbsh
type: challenge
title: Sign in & tour Coder Agents
teaser: Log in to a self-hosted Coder, then ask the agent to list a repo's issues
  — with no workspace.
notes:
- type: text
  contents: |
    <style>@keyframes coder-blink{50%{opacity:0}}.coder-blink::after{content:'';display:inline-block;width:0.5em;height:1em;background:currentColor;margin-left:8px;vertical-align:text-bottom;animation:coder-blink 1.1s steps(1) infinite;}</style>
    <div style="background:radial-gradient(120% 140% at 85% 0%, rgba(240,141,255,0.22) 0%, rgba(117,17,226,0.18) 38%, transparent 70%),#18171A;color:#FFFFFF;font-family:Geist,system-ui,-apple-system,'Segoe UI',sans-serif;text-align:center;padding:56px 32px;border-radius:4px;">
      <svg viewBox="0 0 425.93 200" width="110" style="display:block;margin:0 auto 28px;" xmlns="http://www.w3.org/2000/svg"><g fill="#FFFFFF"><rect x="263.75" y="5.41" width="162.18" height="189.24"/><path d="M0,100C0,38.92,51.89,0,123.25,0s111.35,33.78,112.7,83.51l-61.62,1.89c-1.62-27.57-26.03-45.68-51.08-45.14-34.32.74-59.73,23.51-59.73,59.73s25.41,58.65,59.73,58.65c25.05,0,48.91-17.3,51.62-44.86l61.62,1.35c-1.62,50.54-44.05,84.87-113.24,84.87S0,160.81,0,100Z"/></g></svg>
      <div style="font-family:'Geist Mono',ui-monospace,Menlo,Consolas,monospace;font-size:12px;letter-spacing:0.04em;text-transform:uppercase;color:#A19CC8;margin-bottom:14px;">Coder Agents &amp; AI Governance &middot; Hands-on</div>
      <div class="coder-blink" style="font-size:38px;font-weight:500;letter-spacing:-0.01em;line-height:1.12;margin-bottom:18px;">Open by design.<br>Secure by default.</div>
      <div style="color:rgba(255,255,255,0.72);font-size:17px;max-width:560px;margin:0 auto;line-height:1.6;">Drive a self-hosted coding agent. Prove the workspace holds no keys and no agent binary. Audit every prompt through the AI Gateway. Six challenges, about an hour.</div>
      <div style="color:rgba(255,255,255,0.72);font-size:15px;margin-top:24px;">Click <b style="color:#FFFFFF;">Start</b> when you're ready.</div>
    </div>
tabs:
- id: bae2lyjqdas5
  title: Coder
  type: service
  hostname: workshop
  path: /
  port: 80
- id: wt8tizlbz5cf
  title: Gitea
  type: service
  hostname: workshop
  path: /learner/memory-card-ai-demo
  port: 8081
difficulty: intermediate
timelimit: 0
lab_config:
  default_layout_sidebar_size: 0
enhanced_loading: null
---

<span style="font-family:'Geist Mono',ui-monospace,Menlo,Consolas,monospace;font-size:12px;letter-spacing:0.04em;text-transform:uppercase;color:#A19CC8;">Coder Agents &middot; 01 — Sign in &amp; tour</span>

Your sandbox has spun up a complete, self-hosted Coder deployment: the control plane, a Postgres database, a private Gitea acting as your "GitHub," Amazon Bedrock wired in as the model provider, and a Grafana dashboard for later. The whole thing is yours alone and gets destroyed when you finish — nothing lingers afterward. In this first challenge you'll sign in and meet the single most important idea in Coder Agents: the agent can do useful work *before* any workspace exists, because the agent loop runs in the control plane, not in a workspace.

---

<h2 style="color: #7511E2; font-weight: 500;">Step 1: Sign in to Coder</h2>

1. Open the **Coder** tab (if it shows a brief loading page, give it a few seconds and refresh).
2. Click **Sign in with Gitea**. If Gitea asks you to authorize the application, click **Authorize**.

That's it. You land signed in as yourself. Coder uses the bundled Gitea as its login provider, so on first sign-in it creates your Coder account straight from your Gitea identity. Your real name and email ride along, which is what makes the audit trail in Challenge 6 a real "who did what" rather than a shared login.

> [!NOTE]
> Notice what you were *not* asked for: no model API key, no IDE extension, no agent CLI. Everything the agent needs lives server-side.
---

<h2 style="color: #7511E2; font-weight: 500;">Step 2: Open the Agents chat and check the model dropdown</h2>

1. After you sign in, your **Agents** access provisions automatically (a few seconds). If **Agents** isn't in the top navigation yet, refresh the Coder tab (upper right corner). ![Screenshot 2026-06-18 at 11.46.31.png](https://play.instruqt.com/assets/tracks/1sxii7ayovnx/34a10e6d0ab518425eb27b5955caebfe/assets/Screenshot%202026-06-18%20at%2011.46.31.png)
2. Open the **Agents** view, then open the **model dropdown** at the top of the message box.
<img src="https://play.instruqt.com/assets/tracks/1sxii7ayovnx/93acc8a5866df5b31790a5ab9050b0a7/assets/agents-tab.gif" width="500"></img>
This deployment serves three models straight from Amazon Bedrock:
![Screenshot 2026-06-18 at 11.50.58.png](https://play.instruqt.com/assets/tracks/1sxii7ayovnx/92902448f33dd425ee3bfa09e57595da/assets/Screenshot%202026-06-18%20at%2011.50.58.png)
| Model | Role |
|-------|------|
| **Claude Sonnet 4.6** | Quality — the default |
| **Claude Haiku 4.5** | Speed |
| **OpenAI gpt-oss-120b** | Open-weight option |

Switching models per prompt — two providers, governed centrally — is part of the story you'll audit in Challenge 6.

> [!NOTE]
> There are no model API keys a developer can see or copy. The control plane authenticates to Bedrock on the deployment's behalf — you just pick a model and type.

---

<h2 style="color: #7511E2; font-weight: 500;">Step 3: Ask a question that needs no workspace</h2>

Switch to Haiku 4.5 and paste the below prompt into the Agents chat and send it:
![Screenshot 2026-06-20 at 12.23.29.png](https://play.instruqt.com/assets/tracks/1sxii7ayovnx/a02efd7e5884219e31bfc1fb09eb2dda/assets/Screenshot%202026-06-20%20at%2012.23.29.png)

```text,copy
List the most poplular programming languages.
```

The agent answers in seconds and **never provisions a workspace** — You only utilize workspace resources when there's real work to do, like reading code or running tests.

---

<h2 style="color: #7511E2; font-weight: 500;">Step 4: Confirm you're in</h2>

You're authenticated, you can switch models, and you've seen the agent work without a workspace, Click **Check** — it confirms your login registered against the control plane.

---

✅ Signed in and oriented. Click **Check** to continue to **Challenge 2**, where you'll hand the agent a real issue to work.
