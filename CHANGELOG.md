# Changelog

Každá verze má v repozitáři tag `vX.Y.Z`. Pokud se někdy změní, co plugin na tvém počítači smí dělat (viz [SECURITY.md](SECURITY.md) — dnes žádné hooky, MCP servery ani spustitelné soubory), bude to vždy nová **hlavní** verze a první řádek jejího záznamu.

## 0.2.3 — 2026-09-30

- Pevné modely agentů místo `inherit`: `clarity-analyst` a `page-structure-analyst` na Sonnetu, `cro-strategist` na Opusu. Dřív agenti dědili model session (dnes většinou Opus, u někoho i Fable) a `inherit` navíc přebíjel proměnnou `CLAUDE_CODE_SUBAGENT_MODEL`.
- README: sekce Modely a jak si přepnout všechny agenty na jeden model.

## 0.2.2 — 2026-09-30

- Bezpečnost: doporučená instalace z pevné verze (tagu), sekce „Důvěra a aktualizace" v SECURITY.md, tenhle changelog.
- GitHub Action `guard`: build selže, když se v repu objeví hooky, MCP/LSP servery, spustitelné soubory, nečekané typy souborů nebo něco, co vypadá jako token.
- Funkčně beze změny oproti 0.2.1.

## 0.2.1 — 2026-09-29

- Kontrola mobilu: command na začátku ověří, že jde okno Chromu zmenšit (maximalizované okno změnu velikosti ignoruje, i když nástroj hlásí úspěch). Analytik struktury ověřuje skutečnou šířku a při neúspěchu vrátí signál `NEED-MOBILE-WINDOW` místo tichého pokračování.

## 0.2.0 — 2026-09-29

- Výstup ve třech dokumentech: **audit pro klienta** (do ~2 500 slov), **technická příloha** pro realizaci, **interní poznámky** (neposílat klientovi).
- Intake se ptá, co za klienta spravuješ ty (`spravujeme`) — doporučení z těch oblastí jsou v klientské verzi „co upravíme my".
- Analytik struktury prochází stránku i v mobilní šířce.
- Kontrola maskování v Clarity přímo v `/cro-operator:cro`; zákaz přepisovat osobní údaje do výstupů pro všechny agenty.
- Volitelné ověření klíčových čísel v GA4 a porovnání textů reklam se stránkou.

## 0.1.0 — 2026-09-28

- První verze: `/cro-operator:cro`, `/cro-operator:setup`, agenti `clarity-analyst`, `page-structure-analyst`, `cro-strategist`, skilly s metodikou a benchmarky pro 4 segmenty × 10 typů stránek, export do Wordu přes pandoc.
