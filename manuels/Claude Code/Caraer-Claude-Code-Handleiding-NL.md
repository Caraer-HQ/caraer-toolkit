# Claude Code + Caraer — Windows Handleiding

> **Versie 2026-v1 · september 2026**
> Koppel Claude Code aan je Caraer-account op Windows — in drie korte stappen.
> Duurt een paar minuten · Geen technische kennis nodig

## Voordat je begint heb je alleen nodig:

- Een Windows-computer met internetverbinding
- **Claude Code geïnstalleerd** — nog niet? Zie [Claude Code installeren](#claude-code-installeren) om dit eerst te doen
- Je Claude-account (die je gebruikt voor Claude / Claude Code)
- Je Caraer-inlog — het e-mailadres en wachtwoord dat je op caraer.com gebruikt

**De drie stappen:**

1. Koppel Caraer met één commando
2. Log in bij Caraer
3. Kies je bedrijf en maak een private app — klaar

*Eerste keer op deze computer? [Installeer eerst Claude Code](#claude-code-installeren).*

---

## Deel 1 — Caraer koppelen

### Stap 1 — Voeg de Caraer-koppeling toe

Open PowerShell: klik op de Windows Start-knop, typ `powershell` en druk op Enter. Er opent een blauw venster met witte tekst — hier typ je de commando's uit deze handleiding.

Kopieer het commando hieronder, plak het in PowerShell (plakken kan met een rechtermuisklik) en druk op Enter — **vervang daarbij `portaalnaam` door de naam van je Caraer-portaal**, bijvoorbeeld `caraer-gartenlux`. Het is één regel, en je hoeft dit maar één keer per portaal te doen.

```powershell
claude mcp add --transport http caraer-portaalnaam https://v2.api.caraer.com/api/v2/mcp
```

> Claude Code nog niet geïnstalleerd op deze computer? Doe eerst de drie stappen onder [Claude Code installeren](#claude-code-installeren).

### Stap 2 — Log in bij Caraer

Start Claude Code door `claude` te typen en op Enter te drukken. (De allereerste keer vraagt het je om in te loggen met je Claude-account — volg de instructies in de browser en ga daarna terug naar PowerShell.)

Typ daarna `/mcp` en druk op Enter, selecteer je **caraer-portaalnaam**-koppeling met de pijltjestoetsen en druk nogmaals op Enter. Je browser opent de Caraer-inlogpagina — log in met je Caraer e-mailadres en wachtwoord.

```
claude
/mcp
```

---

## Deel 2 — In de browser

### Stap 3 — Kies je bedrijf en maak een private app

Na het inloggen stelt Caraer twee korte vragen in hetzelfde browservenster. Beantwoord ze zo, en ga daarna terug naar het PowerShell-venster:

1. **Select a company** — kies het bedrijf waarvoor Claude Code moet werken uit de lijst en klik op **Continue**.
2. **Choose a private app** — selecteer **"Create a new private app"**, typ een naam in het Label-veld (bijvoorbeeld: *Claude Code*) en klik op **Continue**.

### ✅ Klaar!

Claude Code is nu gekoppeld aan Caraer. In de `/mcp`-lijst staat je caraer-portaalnaam-koppeling als "connected". Vanaf nu kun je `claude` gewoon starten vanuit PowerShell en het laten werken met je Caraer-vacatures, -campagnes en -kandidaten.

> Kom je er niet uit? Maak een screenshot van het PowerShell-venster en stuur het naar je Caraer-contactpersoon.

---

## Claude Code installeren

*Slechts één keer nodig, op een computer waar Claude Code nog niet op staat. Doe dit vóór Deel 1.*

### A — Open PowerShell

Klik op de Windows Start-knop (linksonder op je scherm), typ het woord `powershell` en druk op Enter.

### B — Installeer Claude Code

Kopieer het commando hieronder, plak het in het PowerShell-venster en druk op Enter. Wacht tot de installatie aangeeft dat hij klaar is (dit kan een minuut duren).

```powershell
irm https://claude.ai/install.ps1 | iex
```

### C — Herstart PowerShell en controleer of het werkt

Sluit het PowerShell-venster volledig en open een nieuw venster (Start-knop, typ `powershell`, Enter). Deze stap is belangrijk — het nieuwe venster zorgt ervoor dat het commando `claude` beschikbaar is.

Typ in het nieuwe venster het commando hieronder en druk op Enter:

```powershell
claude --version
```

Zie je een versienummer, dan is het gelukt — ga verder met Deel 1. Zie je in plaats daarvan *"claude is not recognized"*, gebruik dan de oplossing hieronder.

### Oplossing: "claude is not recognized"

Dit betekent dat Windows het programma nog niet kan vinden. Kopieer het commando hieronder in PowerShell, druk op Enter, sluit PowerShell en open opnieuw een nieuw venster. Daarna werkt `claude --version` wel.

```powershell
[Environment]::SetEnvironmentVariable('Path', "$env:USERPROFILE\.local\bin;" + [Environment]::GetEnvironmentVariable('Path','User'), 'User')
```
