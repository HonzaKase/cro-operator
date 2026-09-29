---
description: Zkontroluje, jestli je všechno připravené pro CRO audit (Claude in Chrome, přihlášení do Clarity, volitelně Clarity API a pandoc), a u každé chybějící věci ukáže přesný postup.
argument-hint: "[doména webu]  | volitelně, např. example.cz"
---

Tvoje role: **průvodce nastavením CRO Operatoru**. Projdi checklist, nic nepřeskakuj a na konci vypiš přehled. **Nic neinstaluj a nic neměň bez výslovného souhlasu uživatele** — jen kontroluješ a vysvětluješ.

Argumenty: `$ARGUMENTS` (volitelná doména webu, jehož Clarity projekt hledat).

**Komunikuješ česky.**

**⛔ Nikdy nežádej Clarity API token do chatu.** Token se vkládá jen do terminálu v příkazu níže. Když ho uživatel do chatu vloží, nezapisuj ho nikam a doporuč mu vygenerovat nový.

---

## Checklist

### 1. Claude in Chrome — POVINNÉ
Zavolej `mcp__claude-in-chrome__tabs_context_mcp`.
- ✅ Odpoví → Chrome je připojený.
- ❌ Nástroj chybí nebo selže → postup:
  1. Claude Code musí být přihlášený přes `/login` s plánem **Pro, Max, Team nebo Enterprise**. S API klíčem Claude in Chrome nefunguje.
  2. Doporučení: v Chromu si založ **samostatný profil** jen pro tuhle práci (vpravo nahoře ikona profilu → Přidat). Agent pracuje v prohlížeči se vším, kde jsi v něm přihlášený — ať v něm není e-mail, banka ani reklamní účty.
  3. V tom profilu nainstaluj rozšíření **Claude in Chrome** z Chrome Web Store a přihlas se v něm svým Claude účtem.
  4. V Claude Code spusť `/chrome` → „Enabled by default". Pak restartuj session a spusť `/cro-operator:setup` znovu.

### 2. Přihlášení do Clarity ve stejném Chromu — POVINNÉ
(Jen když je bod 1 ✅.) Otevři nový tab a přejdi na `https://clarity.microsoft.com/projects`. Přečti stránku.
- **Login obrazovka** → požádej uživatele, ať se přihlásí **v tom otevřeném tabu** a napíše „hotovo". Zkontroluj znovu.
- ✅ **Seznam projektů** → vypiš názvy projektů, které účet vidí. Když byla zadaná doména, ověř, že mezi nimi je její projekt.
- ❌ **Projekt webu chybí** → účet nemá přístup. Vlastník projektu ho musí přidat v Clarity (Settings → Team). Ke čtení dashboardu admin práva nejsou potřeba — a čím nižší role, tím líp.

Doporuč zkontrolovat v Clarity **Settings → Masking** — ať je nastavené „Balanced" nebo „Strict", aby se do nahrávek a screenshotů nedostaly osobní údaje návštěvníků.

### 3. Clarity API — VOLITELNÉ
Dashboard přes Chrome dává 90 dní dat a heatmapy. API přidá jen rychlá čísla za poslední 3 dny. Bez API audit funguje naplno.

Zjisti, jestli máš nástroje `mcp__clarity__*`.
- ✅ Jsou → API připojené. **Nevolej ho automaticky** (denní limit je 10 dotazů). Nabídni ověření tokenu jedním dotazem — jen na „ano".
- ⚪ Nejsou → vysvětli, jak API přidat, když o něj uživatel stojí:
  1. Potřebuje **Node.js** (ověř `node --version`; chybí → Windows `winget install OpenJS.NodeJS.LTS`, macOS `brew install node`).
  2. Clarity → projekt webu → **Settings → Data Export → Generate new API token** (vyžaduje admina projektu). Token je secret.
  3. **V terminálu** (ne v chatu), ve složce, kde bude s tímhle klientem pracovat, spustí:
     ```
     claude mcp add --scope local --env CLARITY_API_TOKEN=VLOZ_TOKEN --transport stdio clarity -- npx -y @microsoft/clarity-mcp-server@2.0.1
     ```
     - Server se **musí jmenovat `clarity`**, jinak ho agenti nenajdou.
     - `--scope local` drží token jen u tebe pro tuhle složku (v `~/.claude.json`) a nikdy ho necommituje. **Nikdy nepoužívej `--scope project`** — ten zapisuje do `.mcp.json`, který se sdílí.
     - Jeden token = jeden Clarity projekt. Víc klientů = každý ve své složce se svým tokenem.
     - Výstup `claude mcp get clarity` token vypisuje v čitelné podobě — nesdílej ho ani nescreenshotuj.
  4. Restart session, pak `/cro-operator:setup` znovu.

### 4. pandoc (export do Wordu) — DOPORUČENÉ
Ověř `pandoc --version`.
- ✅ → Word se vytvoří automaticky.
- ⚠️ Chybí → audit zůstane jen v Markdownu. Instalace: Windows `winget install JohnMacFarlane.Pandoc`, macOS `brew install pandoc`. Po instalaci restartuj terminál / Claude Code, aby se pandoc objevil v PATH.

### 5. GA4 a reklamní účty — VOLITELNÉ
Zjisti, jestli má session nástroje pro GA4, Google Ads, Meta nebo Sklik (jakýkoli připojený konektor, jen se podívej na dostupné nástroje, nic nevolej).
- ✅ Jsou → audit ověří klíčová čísla v GA4 a porovná texty reklam se stránkou (jen čtením).
- ⚪ Nejsou → nevadí; audit tyto body uvede jako otevřené k ověření.

### 6. Data a soukromí — INFORMACE
Připomeň jednou větou: data z Clarity a screenshoty klientova webu jdou během auditu do Claude (Anthropic). Když auditujete cizí web, má to být v souladu s dohodou s klientem.

---

## Výstup

Vypiš tabulku:

| # | Položka | Stav | Co udělat |
|---|---|---|---|
| 1 | Claude in Chrome | ✅ / ❌ | … |
| 2 | Clarity přihlášení + projekt | ✅ / ❌ | … |
| 3 | Clarity API (volitelné) | ✅ / ⚪ | … |
| 4 | pandoc (Word) | ✅ / ⚠️ | … |
| 5 | GA4 / reklamní účty (volitelné) | ✅ / ⚪ | … |

Když jsou 1 a 2 ✅: „Připraveno. Spusť `/cro-operator:cro <url>`."
