# CRO Operator

Plugin pro [Claude Code](https://code.claude.com), který z **Microsoft Clarity** udělá CRO audit stránky. Agent si sám otevře Clarity dashboard ve tvém Chromu, roztáhne datové okno na 90 dní, přečte heatmapy, scroll mapy a nahrávky, projde celou stránku odshora dolů a sestaví audit ve formátu:

> **vaše data ukazují tohle → vyvozujeme z toho tohle → doporučujeme tyhle kroky → protože (best practice + zdroj)**

Výstupem jsou dva dokumenty v Markdownu i ve Wordu: **krátký audit pro klienta** (přečte se za 15 minut) a **technická příloha** pro toho, kdo změny realizuje. Ukázka na fiktivní firmě: [audit pro klienta](examples/ukazkovy-audit.md) ([.docx](examples/ukazkovy-audit.docx)) · [technická příloha](examples/ukazkova-technicka-priloha.md).

## Proč přes dashboard, a ne přes API

Clarity API heatmapy nevrací vůbec a vidí jen poslední 3 dny. V dashboardu je 90 dní a vizuální heatmapy. U testovaného webu to byl rozdíl **84 vs. 3 449 sessions**. Heatmapu jako data přes API nedává žádný běžný nástroj (Hotjar, Smartlook, PostHog a spol. mají stejný problém), takže agent jde tam, kde data reálně jsou — do dashboardu přes [Claude in Chrome](https://code.claude.com/docs/en/chrome).

## Jak to funguje

```
/cro-operator:cro https://example.cz/
  │
  ├─ kontrola: Chrome připojený? Clarity přihlášená? vidím projekt webu?
  ├─ intake: segment, typ stránky, primární konverze (doptá se po jedné otázce)
  │
  ├─ clarity-analyst ─────────┐   heatmapy, scroll mapy, nahrávky, frustrační signály
  ├─ page-structure-analyst ──┤   wireframe celé stránky (desktop i mobil) vs. ideál pro segment
  │                           ▼
  ├─ volitelně: ověření v GA4, texty reklam vedoucích na stránku
  └─ cro-strategist ──→ audit pro klienta + technická příloha (+ interní poznámky)
```

- **Tři agenti** — dva sbírají (data a struktura, jen čtou), třetí skládá audit.
- **Benchmarky** pro 4 segmenty (e-commerce, B2B služby, poradenství, SaaS) × 10 typů stránek (homepage, produkt, kategorie, ceník, landing page, obsah, služba, košík/checkout, děkovačka, kontakt). Opřené o Baymard, NN/g, CXL, LIFT, Unbounce; směrová čísla jsou označená ⚠️.
- **Metodika** — Clarity signál → význam, NN/g heuristiky + LIFT + Krugův 5s test, prioritizace PIE/ICE, poctivost ohledně velikosti vzorku (pod ~100 sessions agregáty nepoužívá jako nález).

## Co potřebuješ

| | Povinné? | Poznámka |
|---|---|---|
| Claude **Pro, Max, Team nebo Enterprise** | ✅ | Claude in Chrome nefunguje s API klíčem ani na free plánu |
| [Claude Code](https://code.claude.com/docs/en/setup) (CLI, desktop app nebo VS Code) + `git` | ✅ | git kvůli instalaci pluginu z GitHubu |
| Chrome + rozšíření **Claude in Chrome** | ✅ | ideálně v samostatném Chrome profilu |
| Přístup do **Microsoft Clarity** projektu webu | ✅ | stačí čtení, admin není potřeba |
| **pandoc** | doporučené | pro export do Wordu |
| Clarity API token + Node.js | volitelné | přidá rychlá čísla za 3 dny, audit funguje i bez něj |
| GA4 / Google Ads / Meta konektor | volitelné | když je máš v Claude Code připojené, audit ověří čísla v GA4 a porovná sliby reklam se stránkou |

## Instalace (zkrácená)

```
claude plugin marketplace add HonzaKase/cro-operator
claude plugin install cro-operator@honza-kase
```

Pak v Claude Code:

```
/cro-operator:setup
```

Setup projde checklist (Chrome, přihlášení do Clarity, API, pandoc) a u každé chybějící věci ukáže přesný postup. Celý návod krok za krokem pro Windows i macOS: **[docs/INSTALL.md](docs/INSTALL.md)**.

## Použití

```
/cro-operator:cro https://example.cz/
/cro-operator:cro https://example.cz/cenik nazev-klienta
```

Výstupy se ukládají do `./cro/<klient>/` v aktuální složce:

```
cro/<klient>/
├── cro-config.md                      segment, konverze, Clarity projekt, seznam stránek
├── cro-log.md                         historie auditů a before-snapshot pro měření
└── analyzy/
    ├── 2026-09-29_homepage_audit.md (.docx)               pro klienta
    ├── 2026-09-29_homepage_technicka-priloha.md (.docx)   pro realizaci
    ├── 2026-09-29_homepage_interni.md                     jen pro tvůj tým, když je co psát
    ├── 2026-09-29_homepage_raw-clarity.md
    └── 2026-09-29_homepage_raw-struktura.md
```

Máš-li v `CLAUDE.md` vlastní pravidla, kde ukládat kontext klientů (nebo má složka klienta vlastní index auditů), command se řídí jimi.

Command se na začátku zeptá i na to, **co za klienta spravuješ ty** (třeba reklamy nebo měření). Doporučení z těch oblastí pak v klientské verzi nestojí jako úkol pro klienta, ale jako „co upravíme my".

## Co to neumí (a je dobré vědět předem)

- **Screenshoty heatmap do Wordu vkládáš sám.** Agent je v Chromu vidí a čte, ale neumí je uložit do souboru. V auditu najdeš na správných místech značku `📷 Vložit screenshot: Clarity → …` s přesnou navigací.
- **Clarity říká kde a proč, ne kolik.** Audit netvrdí konkrétní nárůst konverzí — kvantifikace patří do GA4 nebo A/B testu.
- **Na málo navštěvovaných stránkách** (pod ~100 sessions za 90 dní) je audit hlavně strukturní a heuristický. Agent to v auditu přizná.
- **Benchmarky jsou globální.** Česká specifika (Heureka, Zásilkovna, GoPay, dobírka…) zatím chybí.
- **Audit, ne stavba.** Doporučení a případný wireframe nové verze ano, úpravy webu ne.
- Rozhraní i výstupy jsou **česky**.

## Bezpečnost v kostce

Agent pracuje ve tvém skutečném Chromu. Proto: **samostatný Chrome profil jen pro tuhle práci**, token jen do terminálu (nikdy do chatu) a zapnuté maskování v Clarity. Agenti mají zakázané cokoli měnit — v Clarity i na auditovaném webu. Detaily: **[SECURITY.md](SECURITY.md)**.

## Aktualizace

```
claude plugin update cro-operator@honza-kase
```

Nebo v Claude Code `/plugin` → Marketplaces → `honza-kase` → Enable auto-update.

## Licence a autor

[MIT](LICENSE) · Honza Kaše — [LinkedIn](https://www.linkedin.com/in/jan-kase/). Chyby a nápady do [Issues](https://github.com/HonzaKase/cro-operator/issues).
