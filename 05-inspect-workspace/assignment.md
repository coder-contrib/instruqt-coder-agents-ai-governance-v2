---
slug: inspect-workspace
id: yyulxqtjq5nx
type: challenge
title: Inspect the workspace — what's not there
teaser: Open a terminal in the workspace and prove there are no LLM keys and no agent
  binary inside.
notes:
- type: text
  contents: |
    <style>@keyframes coder-blink{50%{opacity:0}}.coder-blink::after{content:'';display:inline-block;width:0.5em;height:1em;background:currentColor;margin-left:8px;vertical-align:text-bottom;animation:coder-blink 1.1s steps(1) infinite;}</style>
    <div style="background:#18171A;color:#FFFFFF;font-family:Geist,system-ui,-apple-system,'Segoe UI',sans-serif;text-align:center;padding:56px 32px;border-radius:4px;">
      <svg viewBox="0 0 425.93 200" width="96" style="display:block;margin:0 auto 24px;" xmlns="http://www.w3.org/2000/svg"><g fill="#FFFFFF"><rect x="263.75" y="5.41" width="162.18" height="189.24"/><path d="M0,100C0,38.92,51.89,0,123.25,0s111.35,33.78,112.7,83.51l-61.62,1.89c-1.62-27.57-26.03-45.68-51.08-45.14-34.32.74-59.73,23.51-59.73,59.73s25.41,58.65,59.73,58.65c25.05,0,48.91-17.3,51.62-44.86l61.62,1.35c-1.62,50.54-44.05,84.87-113.24,84.87S0,160.81,0,100Z"/></g></svg>
      <div style="font-family:'Geist Mono',ui-monospace,Menlo,Consolas,monospace;font-size:12px;letter-spacing:0.04em;text-transform:uppercase;color:#A19CC8;margin-bottom:14px;">Challenge 05 &middot; Inspect the workspace</div>
      <div class="coder-blink" style="font-size:34px;font-weight:500;letter-spacing:-0.01em;line-height:1.12;margin-bottom:16px;">Open the box. Find nothing.</div>
      <div style="color:rgba(255,255,255,0.72);font-size:17px;max-width:560px;margin:0 auto;line-height:1.6;">No LLM keys. No agent binary. Inspect the workspace yourself — the absence is the feature.</div>
    </div>
tabs:
- id: klkuv6tyabzs
  title: Coder
  type: service
  hostname: workshop
  path: /
  port: 80
- id: hefqruqlrgg4
  title: App Preview
  type: service
  hostname: workshop
  path: /
  port: 5173
difficulty: intermediate
timelimit: 0
lab_config:
  default_layout_sidebar_size: 0
enhanced_loading: null
---

<span style="font-family:'Geist Mono',ui-monospace,Menlo,Consolas,monospace;font-size:12px;letter-spacing:0.04em;text-transform:uppercase;color:#A19CC8;">Coder Agents &middot; 05 — Inspect the workspace</span>

You've watched the agent ship a PR. Now prove the security claim by inspection. The whole pitch of Coder Agents is that the workspace is *pure compute* — the credentials, the agent code, and the model connection all live in the control plane. So if you open a terminal inside the workspace the agent used, you should find **no LLM API key and no agent binary** — the model connection lives entirely in the control plane. Let's confirm it rather than take it on faith.

---

<h2 style="color: #7511E2; font-weight: 500;">Step 1: Open a terminal in the workspace</h2>

In the **Coder** tab, open your running workspace and launch its **Terminal**. You'll be inside the same container the agent operated in. Everything below runs there.
![Screenshot 2026-06-18 at 11.48.38.png](https://play.instruqt.com/assets/tracks/1sxii7ayovnx/f3e43ffc4cdfb801bfa0920b2d4f51ec/assets/Screenshot%202026-06-18%20at%2011.48.38.png)
<img src="https://play.instruqt.com/assets/tracks/1sxii7ayovnx/7084ff9ce6312b60621e3e344a085e7c/assets/workspace-terminal.gif" width="1000"></img>

---

<h2 style="color: #7511E2; font-weight: 500;">Step 2: Look for LLM credentials — there are none</h2>

Search the environment and common credential locations for anything that looks like a model key:

```bash,copy
env | grep -iE 'ANTHROPIC|OPENAI|BEDROCK|AWS_SECRET|LLM|API_KEY' || echo "No LLM credentials found in the environment."
```

The grep comes back empty. The workspace was never handed a model key, because the workspace never talks to the model — the control plane does.

---

<h2 style="color: #7511E2; font-weight: 500;">Step 3: Look for an agent binary — there is none</h2>

Check for the coding-agent CLIs that a workspace-resident agent (the old "Coder Tasks" model) would have required:

```bash,copy
for b in claude codex goose aider cursor-agent; do command -v "$b" >/dev/null 2>&1 && echo "FOUND: $b" || echo "absent: $b"; done
```

Every one reports `absent`. There's no agent harness to patch, sandbox, or worry about — it simply isn't here.

---

<h2 style="color: #7511E2; font-weight: 500;">Step 4: Confirm the work is real, and identity is attached</h2>

The code change *is* here, and git knows who did it:

```bash,copy
cd /home/coder/memory-card-ai-demo && git log -1 --pretty='Author: %an <%ae>%nSubject: %s'
```

The commit is authored by your identity — the agent acted *as you*, with no privilege escalation and no shared bot account.

---

<h2 style="color: #7511E2; font-weight: 500;">Step 5: Record your inspection</h2>

Write the sentinel the check looks for:

```bash,copy
touch /tmp/.workshop-inspected && echo "Inspection recorded."
```

Then click **Check**.

> [!NOTE]
> Done inspecting? It's safe to close the workspace **terminal(s)** now — nothing later needs them. Challenge 6 uses only the **Coder** and **Grafana** tabs.

---

✅ No keys, no agent binary, identity attached. Click **Check**, then continue to **Challenge 6** to read the audit trail.
