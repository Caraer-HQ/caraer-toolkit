# Claude Code + Caraer — Windows Setup Manual

> **Version 2026-v1 · September 2026**
> Connect Claude Code to your Caraer account on Windows — in three short steps.
> Takes a few minutes · No technical knowledge needed

## Before you start, you only need:

- A Windows computer with an internet connection
- **Claude Code installed** — not yet? See [Installing Claude Code](#installing-claude-code) to install it first
- Your Claude account (the one you use for Claude / Claude Code)
- Your Caraer login — the e-mail address and password you use on caraer.com

**The three steps:**

1. Connect Caraer with one command
2. Log in to Caraer
3. Pick your company and create a private app — done

*First time on this computer? [Install Claude Code](#installing-claude-code) first.*

---

## Part 1 — Connect Caraer

### Step 1 — Add the Caraer connection

Open PowerShell: click the Windows Start button, type `powershell`, and press Enter. A blue window with white text opens — this is where you type the commands from this guide.

Copy the command below, paste it into PowerShell (a right-click pastes), and press Enter — **replacing `portalname` with the name of your Caraer portal**, for example `caraer-gartenlux`. It is one single line, and you only need to do this once per portal.

```powershell
claude mcp add --transport http caraer-portalname https://v2.api.caraer.com/api/v2/mcp
```

> Claude Code not installed yet on this computer? Do the three steps under [Installing Claude Code](#installing-claude-code) first.

### Step 2 — Log in to Caraer

Start Claude Code by typing `claude` and pressing Enter. (The very first time it asks you to log in to your Claude account — follow the browser instructions, then return to PowerShell.)

Then type `/mcp` and press Enter, select your **caraer-portalname** connection with the arrow keys, and press Enter again. Your browser opens the Caraer login page — log in with your Caraer e-mail and password.

```
claude
/mcp
```

---

## Part 2 — In the browser

### Step 3 — Pick your company and create a private app

After logging in, Caraer asks two short questions in the same browser window. Answer them like this, then go back to the PowerShell window:

1. **Select a company** — choose the company Claude Code should work for from the list and click **Continue**.
2. **Choose a private app** — select **"Create a new private app"**, type a name in the Label box (for example: *Claude Code*), and click **Continue**.

### ✅ You're done!

Claude Code is now connected to Caraer. In the `/mcp` list, your caraer-portalname connection shows as "connected". From now on you can simply start `claude` from PowerShell and ask it to work with your Caraer vacancies, campaigns and candidates.

> Stuck on a step? Screenshot the PowerShell window and send it to your Caraer contact person.

---

## Installing Claude Code

*Only needed once, on a computer that does not have Claude Code yet. Do this before Part 1.*

### A — Open PowerShell

Click the Windows Start button (bottom-left of your screen), type the word `powershell`, and press Enter.

### B — Install Claude Code

Copy the command below, paste it into the PowerShell window, and press Enter. Wait until the installation says it is finished (this can take a minute).

```powershell
irm https://claude.ai/install.ps1 | iex
```

### C — Restart PowerShell and check it works

Close the PowerShell window completely, then open a new one (Start button, type `powershell`, Enter). This step matters — the new window is what makes the `claude` command available.

In the new window, type the command below and press Enter:

```powershell
claude --version
```

If you see a version number, it worked — continue with Part 1. If you see *"claude is not recognized"* instead, use the fix below.

### Fix: "claude is not recognized"

This means Windows cannot find the program yet. Copy the command below into PowerShell, press Enter, then close PowerShell and open a new window again. After that, `claude --version` will work.

```powershell
[Environment]::SetEnvironmentVariable('Path', "$env:USERPROFILE\.local\bin;" + [Environment]::GetEnvironmentVariable('Path','User'), 'User')
```
