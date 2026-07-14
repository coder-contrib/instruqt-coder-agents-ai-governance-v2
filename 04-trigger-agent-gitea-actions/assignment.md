---
slug: trigger-agent-gitea-actions
id: yy33ebh3ek3m
type: challenge
title: Trigger an agent from CI
teaser: Kick off the same Coder Agent from a CI workflow — the forward-looking replacement
  for label-an-issue automation.
notes:
- type: text
  contents: |
    <style>@keyframes coder-blink{50%{opacity:0}}.coder-blink::after{content:'';display:inline-block;width:0.5em;height:1em;background:currentColor;margin-left:8px;vertical-align:text-bottom;animation:coder-blink 1.1s steps(1) infinite;}</style>
    <div style="background:#18171A;color:#FFFFFF;font-family:Geist,system-ui,-apple-system,'Segoe UI',sans-serif;text-align:center;padding:56px 32px;border-radius:4px;">
      <svg viewBox="0 0 425.93 200" width="96" style="display:block;margin:0 auto 24px;" xmlns="http://www.w3.org/2000/svg"><g fill="#FFFFFF"><rect x="263.75" y="5.41" width="162.18" height="189.24"/><path d="M0,100C0,38.92,51.89,0,123.25,0s111.35,33.78,112.7,83.51l-61.62,1.89c-1.62-27.57-26.03-45.68-51.08-45.14-34.32.74-59.73,23.51-59.73,59.73s25.41,58.65,59.73,58.65c25.05,0,48.91-17.3,51.62-44.86l61.62,1.35c-1.62,50.54-44.05,84.87-113.24,84.87S0,160.81,0,100Z"/></g></svg>
      <div style="font-family:'Geist Mono',ui-monospace,Menlo,Consolas,monospace;font-size:12px;letter-spacing:0.04em;text-transform:uppercase;color:#A19CC8;margin-bottom:14px;">Challenge 04 &middot; Trigger from CI</div>
      <div class="coder-blink" style="font-size:34px;font-weight:500;letter-spacing:-0.01em;line-height:1.12;margin-bottom:16px;">Same agent. From CI.</div>
      <div style="color:rgba(255,255,255,0.72);font-size:17px;max-width:560px;margin:0 auto;line-height:1.6;">Run a Gitea Actions workflow and watch it call the Coder Agents API — the agent opens a pull request with no one at the keyboard.</div>
    </div>
tabs:
- id: edyuo884qgwe
  title: Gitea
  type: service
  hostname: workshop
  path: /learner/memory-card-ai-demo/actions
  port: 8081
- id: uyxmhdatthfb
  title: Coder
  type: service
  hostname: workshop
  path: /
  port: 80
difficulty: intermediate
timelimit: 0
lab_config:
  default_layout_sidebar_size: 0
enhanced_loading: null
---

<span style="font-family:'Geist Mono',ui-monospace,Menlo,Consolas,monospace;font-size:12px;letter-spacing:0.04em;text-transform:uppercase;color:#A19CC8;">Coder Agents &middot; 04 — Trigger from CI</span>

So far you've driven the agent by hand from the chat UI. But the same control-plane agent is reachable from an API — which means you can trigger it from **CI**, not just a person at a keyboard. That's the modern, forward-looking pattern: a pipeline calls the **Coder Agents API** to do background work, rather than the old "label an issue → spin up a one-off task" loop. Your sandbox's Gitea ships **Gitea Actions** (GitHub-Actions-compatible), with a runner already registered and a `coder-agent` workflow already in the repo.

---

<h2 style="color: #7511E2; font-weight: 500;">Step 1: Open the Actions view</h2>

Open the **Gitea** tab — it lands directly on your repository's **Actions** view, right here in this window (no separate browser tab needed).

In the left sidebar you'll see one workflow, **`coder-agent.yml`**. It reads **"0 workflow runs / The workflow has no runs yet"** — that's expected, because you haven't run it yet; you will in the next step.

> [!NOTE]
> Want to see what the workflow actually does? Open the **`< > Code`** tab and browse to **`.gitea/workflows/coder-agent.yml`**. Its one job calls the Coder Agents API using a workshop-scoped token stored as a Gitea Actions secret, so nothing sensitive lives in the workflow file itself.

---

<h2 style="color: #7511E2; font-weight: 500;">Step 2: Run the workflow</h2>

Dispatch the workflow from the **Actions** tab:

1. Click **`coder-agent.yml`** in the left sidebar.
2. Click **Run workflow** (top-right) — a form drops down with the prompt **pre-filled** (the workflow's default).
3. Leave it as-is and click the blue **Run workflow** button.

```copy
Implement the 'Change the card back design' issue in the memory-card-ai-demo repo that is already cloned in your workspace: add a visible red diamond to the back face of every card that disappears when the card is flipped face-up. Create a feature branch named ci/card-back-design, commit your change, push the branch to origin, and open a pull request into main.
```

The prompt above is shown only for reference — you don't need to type anything.

> [!TIP]
> After you click **Run workflow**, the run appears in the Actions list. Gitea's page doesn't auto-update — click the **refresh icon** (top-right of the lab window) if it doesn't show within a few seconds.

The runner picks up the job in a container on the sandbox's Docker host and `curl`s the same **`POST /api/experimental/chats`** call the chat UI makes — so the CI-triggered run is governed and audited exactly like an interactive one (you'll see it in Challenge 6).

---

<h2 style="color: #7511E2; font-weight: 500;">Step 3: Watch the CI-triggered agent open a PR</h2>

1. Watch the run go **green** in the Actions tab (use the refresh icon if it's slow).
2. Give it a minute or two, then open **Pull Requests** in the Gitea tab.

A brand-new PR appears — from a **`ci/`-prefixed branch** (e.g. `ci/card-back-design`), opened by the **CI run**, not by you in the chat UI. From a single workflow dispatch, the agent provisioned a workspace, made the change, pushed the branch, and opened the PR. Behind that green check, the job called the **Coder Agents API** with a workshop-scoped CI token — the same governed endpoint the chat UI uses; a **pipeline**, not a person, kicked off the agent.

> [!NOTE]
> This run authenticates as a workshop **CI identity** — a machine, not your own identity. In **Challenge 6** you'll find this CI-triggered call in the AI Gateway audit, sitting right next to the prompts *you* ran by hand: human and machine activity, both governed and both attributed.

---

<h2 style="color: #7511E2; font-weight: 500;">Step 4: Review the agent chat under the Coder Admin user</h2>

1. Open the **Gitea** tab.
2. Click "Actions >> workflow run >> trigger-agent >> Show Chat URL"
<img src="https://play.instruqt.com/assets/tracks/1sxii7ayovnx/4807d54d384b0795386f577b9e2468b2/assets/Gitea.gif" width="1000"></img>
3. Click on the "Chat URL" to see the triggered agent chat in Coder (Admin User).

---

<h2 style="color: #7511E2; font-weight: 500;">Step 5: Confirm the CI run</h2>

Click **Check** — it confirms a Gitea Actions run exists **and** evidence the agent was triggered (the CI-triggered chat, or the `ci/`-prefixed pull request).

---

✅ The agent runs from CI, not just chat. Click **Check**, then continue to **Challenge 5** to inspect the workspace and prove what's *not* inside it.
