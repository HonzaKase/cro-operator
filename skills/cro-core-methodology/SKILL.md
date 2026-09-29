---
name: cro-core-methodology
description: >
  Use when doing CRO / conversion rate optimization work driven by Microsoft
  Clarity behavioral data — diagnosing friction, forming hypotheses, prioritizing,
  or measuring impact on any web page. Activates on: "Clarity", "Microsoft Clarity",
  "CRO", "conversion rate optimization", "heatmapa", "heatmap", "session recording",
  "rage clicks", "dead clicks", "quickbacks", "frustration signály", "scroll depth",
  "frikce na stránce", "konverzní optimalizace", "hypotéza CRO", "PIE", "ICE",
  "before/after měření", "A/B test CRO", "message match", "landing page optimalizace",
  "proč lidi nekonvertují". Foundation skill pro agenty clarity-analyst, page-structure-analyst
  a cro-strategist. Poskytuje CRO metodiku — Clarity signal→význam slovník,
  diagnostické čočky (NN/g + LIFT + Krug), prioritizaci (PIE/ICE), šablonu hypotézy
  a měřící framework (before/after vs A/B, dvojitý scorecard, statistická poctivost).
---

# CRO Core Methodology

Foundation skill pro Clarity-driven CRO systém. Drží **sdílenou metodiku**, kterou používají všichni tři agenti (`clarity-analyst`, `page-structure-analyst`, `cro-strategist`). Specifika podle typu stránky jsou ve skillu `cro-operator:cro-page-playbooks`.

**Komunikuješ česky.**

---

## ⛔ Tři nepřekročitelná pravidla metodiky

1. **Clarity je kvalitativní — říká „proč/kde", ne „kolik".** Nikdy netvrď lift jen z Clarity signálů. Kvantifikaci dělá GA4 / business metriky. Na nízkém trafficu je „2 týdny a vypadá to nahoru" **přiznaný směrový before/after read**, ne důkaz.
2. **Diagnostika ≠ návrh řešení.** Nejdřív se popíše frikce s důkazem, teprve pak hypotéza. Tohle oddělení drží kvalitu (analytik nesmí skočit k oblíbenému řešení).
3. **Víc čoček, ne jedna.** Jeden hodnotitel najde ~35 % problémů (NN/g data). Vždy projeď NN/g heuristiky + LIFT + page-type playbook, ne jen jednu optiku.

---

## 1. Clarity signál → význam (diagnostický slovník)

Každý signál má **více možných příčin** — neskákej k závěru, ověř pohledem na reálnou stránku.

| Signál | Co to je | Nejčastější příčiny (ověřit na stránce) |
|---|---|---|
| **Rage clicks** | Rychlé opakované kliky na jednom místě | Element vypadá klikatelně, ale není · je rozbitý · je pomalý (latence/JS) · uživatel čeká odezvu, která nepřichází |
| **Dead clicks** | Klik bez vizuální odezvy a bez navigace | Falešná afordance (vypadá interaktivně) · rozbitý element · latence · obrázek, u kterého lidé čekají zoom |
| **Quickbacks** | Návštěvník přejde na stránku a pod prahem času se vrátí zpět | Cíl okamžitě nesplnil očekávání · message mismatch (reklama/odkaz slíbil něco jiného) · pomalé/matoucí načtení |
| **Excessive scrolling** | Víc scrollování, než by mělo být | Špatný information scent · lidi nenajdou co hledají · klíčový obsah moc nízko · slabá hierarchie |
| **Script / JS errors** | JS chyby během session | Můžou být **kořenovou příčinou** rage/dead clicks (např. bug jen v Safari). Vždy prověř, jestli frustrace nesedí na chybu. |
| **Error clicks** | Kliky spojené s chybou | Rozbitá funkčnost v daném místě |
| **Nízká scroll depth na hero** | Lidi nedoscrollují | Value prop / klíčový obsah není vidět · hero moc vysoký · slabý důvod scrollovat dál |
| **Nízká CTR primárního CTA (area map)** | CTA dostává málo pozornosti | CTA neviditelné/slabé · konkuruje mu moc dalších prvků · špatné umístění |

**Degraded mode — běh bez připojených Clarity dat:**
Když není dostupný Clarity dashboard (Chrome nepřipojený, chybí přístup k projektu) ani Clarity API, **heuristický průchod nad živou stránkou pořád dává hodnotu** — ale drž hranici:
- ✅ **Užitečné i bez dat:** strukturální/obsahové frikce viditelné okem (carousel, headline padá v 5s testu, konkurující CTA, trust pod foldem, falešné afordance). Označ je jako **podezření k ověření**, ne potvrzené frikce.
- ⛔ **Už hádáš (nedělej to):** tvrdit konkrétní čísla (scroll depth 40 %, X rage clicks), řadit frikce podle „závažnosti" jako by změřené, nebo tvrdit že něco JE/NENÍ problém bez behaviorálního důkazu.
- Každý Clarity signál, který bys očekával, popiš jako *„tohle by potvrdil signál Y"* a označ `⚠️ NEOVĚŘENO`. Diagnostika v degraded mode = **prioritizované podezření**, ne závěr.

**Defenzivní parsování Clarity API:**
- Schéma frustration metrik **není spolehlivě zdokumentované** (Microsoft dokumentuje jen Traffic). Counts chodí jako **stringy**, ratia jako čísla — ošetři typy a chybějící klíče.
- **Consent Mode (od 10/2025):** EEA/UK/CH bez souhlasu = redukovaná data → Clarity counts ber jako **spodní hranici**, váž GA4 výš.
- API limit: 10 dotazů/den, 3 dny zpět, ≤1000 řádků. Pro občasnou analýzu jednoho webu OK; nezahazuj kvótu na zbytečné dotazy.

---

## 2. Diagnostické čočky (projeď všechny)

### 2.1 NN/g — 10 usability heuristik
Visibility of system status · match to real world · user control & freedom · consistency & standards · error prevention · recognition over recall · flexibility & efficiency · aesthetic & minimalist design · recognize/recover from errors · help & documentation.

### 2.2 LIFT model (převod pozorování na hypotézu)
Hodnoť stránku přes 6 faktorů kolem **Value Proposition**:
- **Relevance** — odpovídá stránka tomu, proč sem člověk přišel? (zdroj, reklama, dotaz)
- **Clarity** — je hodnota a další krok okamžitě jasný?
- **Anxiety** *(inhibitor)* — co vyvolává nejistotu/obavu? (chybí trust, nejasná cena, riziko)
- **Distraction** *(inhibitor)* — co odvádí od primární akce? (moc CTA, šum)
- **Urgency** — je důvod jednat teď?

Příklad mapování: dead clicks na statický hero obrázek = Clarity (falešná afordance) → fix snižuje Anxiety/Distraction.

### 2.3 Krug — 5s test
„Kde jsem? Co tu můžu udělat? Proč bych měl?" Když stránka neprojde za 5 s, je to Clarity/Relevance problém. Levná kvalitativní validace na nízkém trafficu: Krugův 3-user test + Clarity recordings.

---

## 3. Šablona hypotézy (povinný formát)

> **„Protože jsme pozorovali {Clarity signál + číslo}, věříme že {konkrétní změna} pro {stránka/audience} způsobí {predikovaná změna metriky}. Poznáme to podle {Clarity signal delta + GA4 metrika}."**

Každá hypotéza musí být **falsifikovatelná** a vázaná na konkrétní důkaz. Bez čísla a bez predikované metriky to není hypotéza, je to názor.

---

## 4. Prioritizace

### 4.1 PIE — výběr stránky (které stránce se věnovat)
- **Potential** — kolik prostoru pro zlepšení.
- **Importance** — kolik (hodnotného) trafficu sem teče.
- **Ease** — jak snadná je změna.
Skóre 1–10 každý, průměr → pořadí stránek.

### 4.2 ICE — pořadí hypotéz na stránce
- **Impact** — jak velký dopad když uspěje.
- **Confidence** — **odměňuje sílu důkazu.** Hypotéza opřená o silný Clarity signál + recording má vyšší Confidence než nápad „od boku".
- **Ease** — effort implementace.

### 4.3 Pravidla
- PIE vybírá stránku, ICE řadí hypotézy na ní.
- **~1 ze 4 slotů rezervuj pro odvážnější sázku** (ne mikro-tweak), zvlášť na nízkém trafficu.
- Po každém cyklu **přeskóruj** — Confidence roste/klesá s výsledky.

---

## 5. Měření přínosu

### 5.1 Rozhodovací pravidlo A/B vs before/after
- **Default = before/after** na Clarity signálech + GA4 cílech.
- **A/B zapni jen** když klíčová stránka překročí ~20k sessions/varianta v rozumném okně. Spolehlivý A/B chce řádově ~30k návštěvníků a stovky+ konverzí na variantu — na nízkém trafficu statisticky neproveditelné.
- Pro nízký traffic: dělej **odvážnější** (ne mikro) změny, měř **mikrokonverze** (form-start, scroll>75 %, add-to-cart), testuj na **nejsilnější stránce** jako proxy, validuj **kvalitativně**.

### 5.2 Dvojitý scorecard
- **Clarity signal deltas** *(rychlé, kvalitativní)*: méně rage/dead clicks, méně quickbacks, hlubší scroll ke klíčovému obsahu, méně JS errors, vyšší engagement time. Pohybují se rychle, na **směrový** závěr nepotřebují statistickou signifikanci.
- **GA4 / business** *(pomalé, kvantitativní)*: conversion rate, primární + mikrokonverze, bounce/exit.

### 5.3 Feedback loop (file-based, bez DB)
Po změně: ulož **before-snapshot** Clarity signálů + záznam do `cro-log.md` (status `proposed→approved→shipped→measuring→won/flat/lost`). Za 2–4 týdny: stáhni znovu → porovnej delty + (pokud je) GA4 → zapiš **výsledek + learning** → přeskóruj backlog. Baseline = snapshot v momentě změny (Clarity API jen 3 dny zpět → pro before/after stačí, pro dlouhý trend ne).

### 5.4 Statistická poctivost (varuj uživatele)
- Žádný lift jen z Clarity signálů.
- Nepeekovat-a-zastavovat (nafukuje false positives k 30 %+).
- Jakýkoli test min. **1 plný týden** (day-of-week bias), i když sample math říká dřív.
- Když se frustration signály po změně **nepohnou** → hypotéza byla špatně; revertuj/iteruj, nestav další na stejném předpokladu.

### 5.5 Datová dostatečnost — kdy data POUŽÍT a kdy NE
Málo sessions → data zkreslují. Postup:
1. **Nejdřív prodluž okno.** Clarity Data Export API vrací jen 3 dny, ale **dashboard (heatmapy/scroll mapy/recordings) umí 7/30/90 dní** — nastav delší rozsah, aby heatmapa nabrala objem. (Recordings retence ~30 dní.)
2. **Prahy použitelnosti per stránka** (heatmapa NENÍ statistický test, je kvalitativní — proto praktické podlahy, ne p-hodnoty):

| Sessions / stránka (v okně) | Agregátní heatmapy & míry (rage/dead/quickback %) |
|---|---|
| **< ~100** | **Nedůvěryhodné — NEPOUŽÍVAT jako nález, neopírat o ně doporučení.** Označit „nedostatek dat". |
| **~100–300** | Jen **směrově** — explicitně label „směrový, ne potvrzený". |
| **300+** | Rozumný směrový CRO read. |

3. **Recordings jsou výjimka** — i 5–15 nahrávek je kvalitativně užitečných **bez ohledu na objem** (jsou pozorování, ne statistika).
4. **Když ani po prodloužení okna není dost dat:** **upozorni a nepoužívej** řídké agregáty. Těžiště přesuň na **recordings + strukturní analýzu + best-practice playbooky**. V auditu napiš „data-driven read vyžaduje akumulaci sessions; zatím heuristický + strukturní audit". Neprezentuj rate spočítaný na pár desítkách sessions jako fakt.

---

## 6. Message-match diagnostika paid trafficu

Když Clarity ukáže **quickbacks / frustraci z paid zdroje** (source = google/meta, konkrétní kampaň), je to jen půlka diagnózy. Druhá půlka:
- Když jsou v session k dispozici nástroje **Google Ads** / **Meta Ads** (jakýkoli MCP konektor), command vytáhne **reálný ad copy + keyword/audience** dané kampaně a předá ho analytikovi. Když nejsou, zapiš to jako otevřenou otázku k ověření.
- Porovnej slib reklamy vs. co stránka skutečně doručí nad foldem.
- Mismatch (reklama slíbila X, landing page mluví o Y) = vysoce pravděpodobná příčina quickbacks → fix = message match (zrcadli ad copy, dynamic text replacement).

Bez **živého pohledu na stránku** (WebFetch / browser) je interpretace heatmapy hádání — element pod „dead clicks" musíš vidět, abys ho diagnostikoval.
