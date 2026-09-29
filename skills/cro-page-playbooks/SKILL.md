---
name: cro-page-playbooks
description: >
  Use when analyzing or auditing a specific page type and business segment in a CRO /
  Clarity workflow — loads the matching segment + page-type benchmark. Two-axis:
  SEGMENT (e-commerce, B2B služby, poradenství, SaaS) × PAGE TYPE (homepage, produkt/PDP,
  kategorie, pricing, lead-gen/landing, content, služba, košík/checkout, děkovačka, kontakt).
  Activates on those segment and page-type names. Companion skillu cro-core-methodology.
  Drží výzkumem podložené benchmarky „jak má vypadat dobrá stránka" (ideální struktura,
  must-have prvky, informační hierarchie, nejčastější selhání, fixy, Clarity signály) —
  s citacemi (Baymard, NN/g, CXL, LIFT, Luke W., Unbounce). Načítej přes progressive
  disclosure — jen relevantní segment + page-type.
---

# CRO Page Playbooks — dvouosý benchmark

Companion k `cro-core-methodology`. Tohle je **zdroj „ideálu"**, proti kterému `page-structure-analyst` měří gap a `cro-strategist` cituje best practices. Ideál je **výzkumem podložený** (Baymard / NN/g / CXL / LIFT / Luke W. / Unbounce), ne názor modelu.

**Komunikuješ česky.**

## Dvě osy — načti vždy oba kusy

Stránku určují **dvě osy**: jaký **segment** (business model) a jaký **typ stránky**. Načti **relevantní segment + relevantní page-type** a zkombinuj je.

### Osa 1 — Segmenty (`segments/`)
| Segment | Soubor |
|---|---|
| E-commerce | `segments/ecommerce.md` |
| B2B služby | `segments/b2b-services.md` |
| Poradenství / profesionální služby | `segments/consulting.md` |
| SaaS | `segments/saas.md` |

### Osa 2 — Typy stránek (`pagetypes/`)
| page_type | Soubor |
|---|---|
| homepage | `pagetypes/homepage.md` |
| produkt (PDP) | `pagetypes/product.md` |
| kategorie / listing | `pagetypes/category.md` |
| pricing / ceník | `pagetypes/pricing.md` |
| lead-gen / landing | `pagetypes/lead-gen.md` |
| content / blog | `pagetypes/content.md` |
| služba | `pagetypes/service.md` |
| košík / checkout | `pagetypes/cart-checkout.md` |
| děkovačka / potvrzení | `pagetypes/thank-you.md` |
| kontaktní stránka | `pagetypes/contact.md` |

## Jak používat
1. Z `cro-config.md` / kontextu zjisti **segment** a **page_type** stránky.
2. Načti **jen** odpovídající `segments/<X>.md` + `pagetypes/<Y>.md` (progressive disclosure — šetří kontext).
3. Segment dává konverzní logiku a co znamená trust; page-type dává ideální strukturu/sekce. Kombinuj — page-typy mají i segmentové poznámky.

## Disciplína citací
Každý „ideál" v playbících má oporu. Když je číslo z **agenturního blogu** (ne z primárního výzkumu jako Baymard/NN/g/Unbounce/Forrester), je v playbooku označené `⚠️` — používej ho jako **směr/hypotézu**, ne jako tvrdé fakt do klientského auditu. Kde je segmentově specifický výzkum tenký, playbook to přiznává.
