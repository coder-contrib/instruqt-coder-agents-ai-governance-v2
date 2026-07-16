---
slug: implement-and-pr
id: qzpkyuaikcjr
type: challenge
title: Watch it implement, test & open a PR
teaser: Let the agent finish the change and open a pull request — authored by your
  identity.
notes:
- type: text
  contents: |
    <style>@keyframes coder-blink{50%{opacity:0}}.coder-blink::after{content:'';display:inline-block;width:0.5em;height:1em;background:currentColor;margin-left:8px;vertical-align:text-bottom;animation:coder-blink 1.1s steps(1) infinite;}</style>
    <div style="background:#18171A;color:#FFFFFF;font-family:Geist,system-ui,-apple-system,'Segoe UI',sans-serif;text-align:center;padding:56px 32px;border-radius:4px;">
      <svg viewBox="0 0 425.93 200" width="96" style="display:block;margin:0 auto 24px;" xmlns="http://www.w3.org/2000/svg"><g fill="#FFFFFF"><rect x="263.75" y="5.41" width="162.18" height="189.24"/><path d="M0,100C0,38.92,51.89,0,123.25,0s111.35,33.78,112.7,83.51l-61.62,1.89c-1.62-27.57-26.03-45.68-51.08-45.14-34.32.74-59.73,23.51-59.73,59.73s25.41,58.65,59.73,58.65c25.05,0,48.91-17.3,51.62-44.86l61.62,1.35c-1.62,50.54-44.05,84.87-113.24,84.87S0,160.81,0,100Z"/></g></svg>
      <div style="font-family:'Geist Mono',ui-monospace,Menlo,Consolas,monospace;font-size:12px;letter-spacing:0.04em;text-transform:uppercase;color:#A19CC8;margin-bottom:14px;">Challenge 03 &middot; Implement &amp; PR</div>
      <div class="coder-blink" style="font-size:34px;font-weight:500;letter-spacing:-0.01em;line-height:1.12;margin-bottom:16px;">The agent ships. You review.</div>
      <div style="color:rgba(255,255,255,0.72);font-size:17px;max-width:560px;margin:0 auto;line-height:1.6;">Implementation, commit, and a pull request into your Gitea — every commit authored by your identity. The merge decision stays human.</div>
    </div>
tabs:
- id: k3d28vgax4fy
  title: Coder
  type: service
  hostname: workshop
  path: /
  port: 80
- id: cp3b7vcbjoiw
  title: Gitea
  type: service
  hostname: workshop
  path: /learner/memory-card-ai-demo/pulls
  port: 8081
- id: kn5kgfrq6kx9
  title: App Preview
  type: service
  hostname: workshop
  path: /
  port: 5173
difficulty: intermediate
timelimit: 0
enhanced_loading: null
---

<span style="font-family:'Geist Mono',ui-monospace,Menlo,Consolas,monospace;font-size:12px;letter-spacing:0.04em;text-transform:uppercase;color:#A19CC8;">Coder Agents &middot; 03 — Implement &amp; PR</span>

In the last challenge the agent provisioned a workspace and started a branch. Now you'll let the full loop play out — implement, verify, commit, and open a pull request — and see that every commit is authored by *your* identity, not a shared service account. That attribution is what makes the audit trail in the final challenge meaningful.

---

<h2 style="color: #7511E2; font-weight: 500;">Step 1: Let the agent finish and open a PR</h2>

Return to the **same Agents chat from Challenge 2** (don't start a new one) — it still has the repo, the feature branch, and the change in context. Send this follow-up:

```copy
Open a pull request into main in this repository with a clear title and description.
```

The agent commits on the feature branch and opens a PR into `main` in your sandbox's Gitea. Git identity comes from the workspace owner, so the commit and PR are attributed to **you**.

---

<h2 style="color: #7511E2; font-weight: 500;">Step 2: Review the pull request and confirm</h2>

Open the **Gitea** tab — it lands on your repository's **Pull Requests**.

[button label="Open Pull Requests in Gitea"](tab-1)

Open the PR the agent created. It has three tabs across the top:

- **Conversation** — the agent's PR description (what it changed and why).
- **Commits** — the commit on the feature branch, authored by **your** identity (carried through from the workspace).
- **Files Changed** — the actual diff against the card-back rendering.

You should see one **open** PR — from the agent's feature branch (e.g. `feature/add-countdown-timer…`) into **`main`**, opened by you. It's the same review experience your developers already know; the only difference is who wrote the code.

> [!TIP]
> Gitea's PR list doesn't auto-update — it's a static page until reloaded. If it looks empty, wait until the agent reports the PR is open, then click the **refresh icon** in the top-right of the lab window.

---

<h2 style="color: #7511E2; font-weight: 500;">Step 3: See your change in the running app</h2>

The workspace runs the memory-card app on a live Vite dev server. Open the **App Preview** tab to see the agent's change rendered in the browser.

[button label="Open the App Preview"](tab-2)

> [!NOTE]
> The preview serves the workspace's working tree. If it shows a loading error or looks stale, give the dev server a few seconds and click the lab window's **refresh** icon.

---

With that PR open, click **Check** — it verifies an open pull request into `main` exists.

✅ A pull request is open and your change is live in the preview. Continue to **Challenge 4** to trigger the same agent from CI.
