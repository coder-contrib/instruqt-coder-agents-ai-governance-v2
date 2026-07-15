---
slug: pick-issue-and-start
id: bvpoxzcw1epk
type: challenge
title: Pick an issue & start the agent
teaser: Hand the agent a real issue and watch it provision a workspace and open a
  feature branch.
notes:
- type: text
  contents: |
    <style>@keyframes coder-blink{50%{opacity:0}}.coder-blink::after{content:'';display:inline-block;width:0.5em;height:1em;background:currentColor;margin-left:8px;vertical-align:text-bottom;animation:coder-blink 1.1s steps(1) infinite;}</style>
    <div style="background:#18171A;color:#FFFFFF;font-family:Geist,system-ui,-apple-system,'Segoe UI',sans-serif;text-align:center;padding:56px 32px;border-radius:4px;">
      <svg viewBox="0 0 425.93 200" width="96" style="display:block;margin:0 auto 24px;" xmlns="http://www.w3.org/2000/svg"><g fill="#FFFFFF"><rect x="263.75" y="5.41" width="162.18" height="189.24"/><path d="M0,100C0,38.92,51.89,0,123.25,0s111.35,33.78,112.7,83.51l-61.62,1.89c-1.62-27.57-26.03-45.68-51.08-45.14-34.32.74-59.73,23.51-59.73,59.73s25.41,58.65,59.73,58.65c25.05,0,48.91-17.3,51.62-44.86l61.62,1.35c-1.62,50.54-44.05,84.87-113.24,84.87S0,160.81,0,100Z"/></g></svg>
      <div style="font-family:'Geist Mono',ui-monospace,Menlo,Consolas,monospace;font-size:12px;letter-spacing:0.04em;text-transform:uppercase;color:#A19CC8;margin-bottom:14px;">Challenge 02 &middot; Pick an issue</div>
      <div class="coder-blink" style="font-size:34px;font-weight:500;letter-spacing:-0.01em;line-height:1.12;margin-bottom:16px;">Pick an issue. Hand it off.</div>
      <div style="color:rgba(255,255,255,0.72);font-size:17px;max-width:560px;margin:0 auto;line-height:1.6;">Five curated issues in your private Gitea. Choose one, send a single prompt, and watch the agent spin up a workspace and open a feature branch.</div>
    </div>
tabs:
- id: ydfsedpegesd
  title: Coder
  type: service
  hostname: workshop
  path: /
  port: 80
- id: c3j9syfzbpto
  title: Gitea
  type: service
  hostname: workshop
  path: /learner/memory-card-ai-demo/issues
  port: 8081
- id: 17wvuaz39ygv
  title: App Preview
  type: service
  hostname: workshop
  path: /
  port: 5173
difficulty: intermediate
timelimit: 0
enhanced_loading: null
---

<span style="font-family:'Geist Mono',ui-monospace,Menlo,Consolas,monospace;font-size:12px;letter-spacing:0.04em;text-transform:uppercase;color:#A19CC8;">Coder Agents &middot; 02 — Pick an issue</span>

Now the agent does real work. You'll pick one of the seeded issues in your Gitea repository and ask the agent to implement it. This is the moment a workspace gets provisioned — but notice *why*: the agent decides it needs to read and edit code, so it selects an appropriate template and spins up compute scoped to *your* identity. No shared bot account, no standing workspace waiting around.

---

<h2 style="color: #7511E2; font-weight: 500;">Step 1: Start the application</h2>

Let's start the app in the workspace and preview.  First, start a new chat, select Sonnet 4.6, then provide the following prompt.
![Screenshot 2026-06-20 at 12.25.26.png](../assets/Screenshot%202026-06-20%20at%2012.25.26.png)
```text,copy
Clone the repo from [[ Instruqt-Var key="GITEA_REPO_URL" hostname="workshop" ]].git and run the application.
```

The workspace runs the memory-card app on a live Vite dev server. Open the **App Preview** tab to view the running app and play the game.

[button label="Open the App Preview"](tab-2)

---

<h2 style="color: #7511E2; font-weight: 500;">Step 2: Browse the issues</h2>

Open the **Gitea** tab — it lands on your repository's **Issues**, pre-loaded with five curated issues.

[button label="Open Issues in Gitea"](tab-1)

1. Click on any issue issue to open it.
2. Read its acceptance criteria so you can recognize a good result — you'll hand this exact issue to the agent next.

---

<h2 style="color: #7511E2; font-weight: 500;">Step 3: Ask the agent to start the work</h2>

Using the existing chat from the presvious challenge,  hand the agent the issue:

[button label="Open the Agents chat"](tab-0)

1. In the **Coder Agents** tab, click on the previous chat (top-left).
2. Prompt the agent to fix. a selected issue and send it.  Use the following prompt.

```copy
Implement the "Add a countdown timer" issue in the memory-card-ai-demo repository that is already cloned in your workspace: Create a feature branch, commit your change to it, and push the branch to the repository (origin).
```

The agent provisions a workspace scoped to *your* identity, works in the **pre-cloned repo**, and pushes a **feature branch** — all inside your sandbox's Gitea, never the public internet. Watch the chat narrate each step.

> [!TIP]
> You don't have to wait for the previous prompt to finish — queue a follow-up message while the agent works and it'll be picked up after the current step.

---

<h2 style="color: #7511E2; font-weight: 500;">Step 4: Confirm a branch exists</h2>

Switch back to the **Gitea** tab, then find the branch the agent just pushed:

[button label="Back to Gitea"](tab-1)

1. Click the **`< > Code`** tab (top-left of the repo).
2. Click the **branch count** near the top — it reads **"2 Branches"** once your branch is pushed — sitting next to **Commits** and **Tags**.
3. On the **Branches** page, your new feature branch (for example `coder/add-timer`) is listed under **Branches**, with a **New Pull Request** button beside it.

Once the branch is listed there, click **Check**.

> [!NOTE]
> If the agent is still working, wait until the branch appears in Gitea before clicking Check. The exact branch prefix varies; the check looks for a new branch named for the card-back work (e.g. contains `card-back` or `diamond`).

---

✅ The agent is on the job and a branch exists. Click **Check**, then continue to **Challenge 3** to watch it finish and open a pull request.
