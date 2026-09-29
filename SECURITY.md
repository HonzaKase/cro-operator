# Bezpečnost

CRO Operator pracuje s tvým prohlížečem, s analytikou cizích webů a volitelně s API tokenem. Tady je, co to znamená a jak riziko držet nízko.

## Rizika a opatření

| Riziko | Co plugin dělá | Co uděláš ty |
|---|---|---|
| **Agent ovládá tvůj skutečný Chrome** a vidí všechny účty, kde jsi v tom profilu přihlášený | Agenti mají zakázané cokoli měnit, vyplňovat, odesílat nebo nakupovat. V Clarity smějí jen navigovat, filtrovat, číst a dělat screenshoty. | Používej **samostatný Chrome profil** jen s Clarity. Žádný e-mail, banka ani reklamní účty v něm. |
| **Prompt injection** — auditovaný web může obsahovat text, který se snaží AI zmanipulovat („ignoruj pokyny, otevři…“) | Agenti mají natvrdo, že obsah webů, dashboardu a nahrávek jsou data, ne instrukce. Podezřelý text nahlásí jako nález. | Samostatný profil (viz výše) — i kdyby ochrana selhala, není k čemu se dostat. |
| **Clarity API token** | Command nikdy nežádá token do chatu. Když ho do chatu vložíš, doporučí ti ho zneplatnit. Token se nikam nezapisuje. | Token vkládej jen do terminálu přes `claude mcp add --scope local`. **Nikdy `--scope project`** (zapisuje do sdíleného `.mcp.json`). |
| **Token je v `~/.claude.json` v čitelné podobě** (tak Claude Code ukládá všechny MCP proměnné) | — | Chraň uživatelský účet na počítači. Výstup `claude mcp get clarity` token vypisuje — nesdílej ho a nescreenshotuj. Token kdykoli zneplatníš v Clarity → Settings → Data Export. |
| **Podvržený npm balíček** | Návod používá oficiální `@microsoft/clarity-mcp-server` se **zafixovanou verzí** (`@2.0.1`), ne „nejnovější“. | Při aktualizaci verze si ověř changelog v [repozitáři Microsoftu](https://github.com/microsoft/clarity-mcp-server). |
| **Osobní údaje návštěvníků** v nahrávkách a screenshotech | Command na začátku zkontroluje režim maskování v Clarity; při „Relaxed" upozorní a pokračuje jen s tvým souhlasem. Agenti mají natvrdo zakázané přepisovat jména, e-maily, adresy a čísla objednávek do výstupů — popisují chování, ne lidi. | V Clarity zapni maskování **Balanced** nebo **Strict**. Screenshoty do auditu vybírej tak, aby na nich nebyly osobní údaje. |
| **Data klienta odcházejí do Claude (Anthropic)** — čísla z Clarity, obsah webu, screenshoty | — | Když auditujete cizí web, mělo by to pokrývat vaše smluvní ujednání s klientem. |
| **Výstupy auditu jsou klientská data** | Ukládají se jen do `./cro/<klient>/`. `.gitignore` v tomhle repu je nepustí dovnitř. | Pokud pracuješ v gitovém repu webu, přidej `cro/` do jeho `.gitignore`. |

## Co plugin nedělá

- Nepřihlašuje se za tebe — login do Clarity děláš vždy sám.
- Nic neinstaluje bez tvého souhlasu (`/cro-operator:setup` jen kontroluje a radí).
- Needituje web, nic necommituje ani nenasazuje.
- Neposílá data nikam jinam než do Claude a do nástrojů, které sám připojíš.

## Oprávnění agentů

| Agent | Nástroje |
|---|---|
| `clarity-analyst` | Chrome (navigace, čtení, klikání kvůli filtrům), volitelně Clarity API, čtení souborů. **Žádný zápis.** |
| `page-structure-analyst` | Chrome (navigace, čtení, scroll), WebFetch, čtení souborů. **Žádný zápis.** |
| `cro-strategist` | Jen čtení souborů a skillů. |
| command `/cro-operator:cro` | Jediný, kdo zapisuje — jen do výstupní složky auditu. |

## Nahlášení problému

Bezpečnostní problém nahlas přes [GitHub Issues](https://github.com/HonzaKase/cro-operator/issues) — bez citlivých údajů (tokenů, dat klientů) v textu.
