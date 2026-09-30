# Instalace krok za krokem

Počítej s 15–20 minutami. Kroky 1–5 jsou povinné, 6 doporučený, 7 volitelný.

---

## 1. Claude Code

Potřebuješ plán **Pro, Max, Team nebo Enterprise**. Free plán Claude Code nezahrnuje a Claude in Chrome nefunguje s API klíčem.

**Windows (PowerShell):**
```powershell
irm https://claude.ai/install.ps1 | iex
```

**macOS:**
```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Otevři nový terminál, spusť `claude` a přihlas se v prohlížeči. Ověření: `claude --version`.

Místo terminálu můžeš použít i [desktop aplikaci Claude](https://claude.com/download) (záložka Code) nebo rozšíření pro VS Code — plugin funguje ve všech.

**git** musí být nainstalovaný (plugin se stahuje z GitHubu):
- Windows: `winget install Git.Git`
- macOS: `xcode-select --install` (nebo `brew install git`)

---

## 2. Samostatný Chrome profil (doporučeno — čti proč)

Agent ovládá **skutečný Chrome** a vidí všechno, kde jsi v tom profilu přihlášený: e-mail, banku, reklamní účty. Při auditu čte cizí weby, a ty můžou obsahovat text, který se snaží AI zmanipulovat. Agenti mají zakázané cokoli měnit, ale nejlepší ochrana je, když v tom profilu **nic citlivého není**.

1. V Chromu vpravo nahoře klikni na ikonu profilu → **Přidat** → pojmenuj ho třeba „CRO“.
2. Všechny další kroky dělej **v tomhle profilu**.

---

## 3. Claude in Chrome

1. V profilu z kroku 2 nainstaluj rozšíření **Claude** z [Chrome Web Store](https://chromewebstore.google.com/detail/claude/fcoeoabgfenejglbffodgkkbkcdhcgfn) (min. verze 1.0.36).
2. Přihlas se v rozšíření **stejným Claude účtem** jako v Claude Code.
3. V Claude Code spusť:
   ```
   /chrome
   ```
   a zvol **Enabled by default**. (Jednorázově jde i `claude --chrome`.)
4. Restartuj Claude Code.

---

## 4. Přihlášení do Clarity — ve stejném Chromu

V profilu z kroku 2 otevři [clarity.microsoft.com](https://clarity.microsoft.com) a přihlas se účtem, který má přístup k projektu auditovaného webu.

- **Nemáš přístup?** Vlastník projektu tě přidá v Clarity → Settings → Team. Na čtení dashboardu admin práva nepotřebuješ — a čím nižší role, tím líp.
- **Maskování:** zkontroluj Settings → Masking. Nastavení **Balanced** nebo **Strict** zajistí, že se do nahrávek a screenshotů nedostanou osobní údaje návštěvníků.

Tenhle krok nemusíš dělat předem — `/cro-operator:cro` i `/cro-operator:setup` Clarity samy otevřou a když nejsi přihlášený, požádají tě o přihlášení přímo v tom tabu.

---

## 5. Instalace pluginu

Instaluj **pevnou verzi** (tag) — nic se pak nezmění bez tvého vědomí.

V terminálu:
```
claude plugin marketplace add HonzaKase/cro-operator#v0.2.3
claude plugin install cro-operator@honza-kase
```

Nebo uvnitř Claude Code:
```
/plugin marketplace add HonzaKase/cro-operator#v0.2.3
/plugin install cro-operator@honza-kase
```

Ověř, co se nainstalovalo: `claude plugin details cro-operator` → `Hooks (0)` a `MCP servers (0)`.

Restartuj Claude Code a spusť kontrolu:
```
/cro-operator:setup
```

---

## 6. pandoc — export do Wordu (doporučeno)

Bez pandocu zůstane audit jen v Markdownu.

- Windows: `winget install JohnMacFarlane.Pandoc`
- macOS: `brew install pandoc`

Po instalaci **restartuj terminál i Claude Code**, aby se pandoc objevil v PATH.

---

## 7. Clarity API (volitelné)

Audit funguje naplno i bez API — hlavní data jdou z dashboardu. API přidá rychlá čísla za poslední 3 dny (limit 10 dotazů denně).

1. Nainstaluj **Node.js**: Windows `winget install OpenJS.NodeJS.LTS`, macOS `brew install node`.
2. Clarity → projekt webu → **Settings → Data Export → Generate new API token** (vyžaduje admina projektu). Token je heslo — **nevkládej ho do chatu s Claudem**.
3. V terminálu přejdi do složky, kde budeš s tímhle klientem pracovat, a spusť (token vlož místo `VLOZ_TOKEN`):
   ```
   claude mcp add --scope local --env CLARITY_API_TOKEN=VLOZ_TOKEN --transport stdio clarity -- npx -y @microsoft/clarity-mcp-server@2.0.1
   ```
   - Server se **musí jmenovat `clarity`**.
   - `--scope local` = token platí jen pro tuhle složku a nikdy se necommituje. **Nepoužívej `--scope project`** — ten zapisuje do sdíleného `.mcp.json`.
   - Jeden token patří k jednomu Clarity projektu. Víc klientů = každý ve své složce se svým tokenem.
4. Restartuj Claude Code a ověř `claude mcp list` → `clarity: ✔ Connected`.

---

## První audit

```
/cro-operator:cro https://example.cz/
```

Command se doptá na segment, typ stránky a primární konverzi (navrhne je sám, ty jen potvrdíš). Běh trvá typicky 10–20 minut. Výstupy najdeš v `./cro/<klient>/analyzy/`.

---

## Aktualizace a odinstalace

- Aktualizace: přečti [CHANGELOG.md](../CHANGELOG.md), pak přejdi na nový tag:

```
claude plugin marketplace remove honza-kase
claude plugin marketplace add HonzaKase/cro-operator#vX.Y.Z
claude plugin install cro-operator@honza-kase
```

  Po aktualizaci znovu `claude plugin details cro-operator` → `Hooks (0)` a `MCP servers (0)`. Automatickou aktualizaci nezapínej.
- Odinstalace: `claude plugin uninstall cro-operator@honza-kase`, případně i `claude plugin marketplace remove honza-kase`.

---

## Řešení problémů

| Problém | Řešení |
|---|---|
| `/cro-operator:setup` hlásí, že Chrome není připojený | Rozšíření nainstalované a přihlášené? `/chrome` → Enabled by default → restart. Claude Code musí být přihlášený přes `/login`, ne API klíčem. |
| Agent otevírá Clarity nepřihlášenou, i když jsem přihlášený | Jsi přihlášený v **jiném Chrome profilu**, než kde běží rozšíření. Přihlas se v tabu, který agent otevřel. |
| Projekt webu v Clarity nevidím | Účet nemá přístup — požádej vlastníka projektu o přidání. |
| `marketplace add` visí nebo selže na SSH | Nastav proměnnou `CLAUDE_CODE_PLUGIN_PREFER_HTTPS=1` a zkus znovu. |
| Audit hlásí „mobil neověřen živě" nebo tě požádá o zmenšení okna | Okno Chromu je maximalizované a agent ho nemůže zúžit na mobilní šířku. Zruš maximalizaci (tlačítko mezi – a ×) a pokračuj. |
| Word se nevytvořil | Chybí pandoc nebo nebyl po instalaci restart. Markdown audit je hotový i tak. |
| `clarity` MCP: 401 | Neplatný nebo expirovaný token — vygeneruj nový. |
| `clarity` MCP: 429 | Vyčerpaný denní limit 10 dotazů — audit pojede z dashboardu. |
| Audit má u heatmap „nedostatek dat“ | Stránka má pod ~100 sessions ani za 90 dní. Audit je pak hlavně strukturní — to je záměr, ne chyba. |
