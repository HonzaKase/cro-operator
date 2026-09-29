# Technická příloha — Ukázka IT s.r.o., homepage

> **Fiktivní ukázka.** Detail k [auditu pro klienta](ukazkovy-audit.md) — pro toho, kdo bude změny realizovat a měřit.

## 1. Data v detailu

| Signál | Desktop | Mobil | Jistota |
|---|---|---|---|
| Sessions (Clarity, 90 dní) | 2 140 | 1 309 | ✅ |
| Dosáhli 25 % stránky | 42 % | 55 % | ✅ |
| Dosáhli sekce „Reference" | 19 % | 24 % | ✅ |
| Kliky na „Nezávazná poptávka" | 0,9 % sessions | 0,6 % sessions | ✅ |
| Dead clicks | 38 | 12 | ⚠️ směrový (málo případů) |
| Rage clicks / JS chyby | 3 / 0 | 1 / 0 | ✅ |
| Odeslané poptávky (GA4, 30 dní) | 9 | 3 | ✅ |

**Scroll útes (desktop).** Hero má 1,4 obrazovky: fotka serverovny + nadpis „Vaše IT v bezpečných rukou". 58 % sessions skončí nebo se vrátí nahoru před první konkrétní informací. *Indikuje:* úvod neodpoví „jsem tu správně?" a nedá důvod scrollovat. Na mobilu je útes mírnější (55 % dojde do čtvrtiny), protože fotka se zmenší.

> 📷 Vložit screenshot: Clarity → Heatmaps → / → Scroll map (desktop, posledních 90 dní)

**Falešné afordance.** 38 dead clicks na ikonách štít / hodiny / sluchátko v sekci „Proč my". Tlačítko poptávky (šedý obrys na tmavé fotce) má méně kliků než logo. *Indikuje:* lidé chtějí k bodům víc informací; CTA je vizuálně slabé a žádá velký krok brzy.

> 📷 Vložit screenshot: Clarity → Heatmaps → / → Click map (desktop, posledních 90 dní)

**Carousel referencí.** Autoplay po 4 s; ze 14 nahrávek s dosažením sekce se ke 3. slidu nedostal nikdo, ovládali ho 2 lidé. *Indikuje:* nejsilnější důkaz nepracuje.

> 📷 Vložit screenshot: Clarity → Recordings → filtr URL `/` + „dosáhl sekce Reference" → ukázka nahrávky (desktop)

**Formulář.** Dosáhne ho 11 % desktop sessions; z nich 23 % začne vyplňovat a 9 % dokončí. Největší odpad u povinného selectu „Počet zaměstnanců". *Indikuje:* formulář je nízko a kvalifikuje příliš brzy.

> 📷 Vložit screenshot: Clarity → Heatmaps → / → Click map, oblast formuláře (desktop)

## 2. Struktura stránky

**Desktop dnes:**
1. Hero — fotka, obecný nadpis, tlačítko „Nezávazná poptávka" *(nad foldem jen z části)*
2. „Proč my" — tři ikony s jedním slovem
3. Služby — 6 dlaždic
4. Carousel referencí — 4 slidy, autoplay
5. „O nás" — historie firmy
6. Blog — 3 články
7. Poptávkový formulář (6 polí) + patička

**Mobil (390 px, ověřeno živě):** stejné pořadí; hero zabere 1,1 obrazovky; tlačítko poptávky je až na 2. obrazovce; telefon jen v patičce, bez `tel:` odkazu.

**Gap proti ideálu B2B služby × homepage:**

| Ideál (playbook) | Stav | Gap |
|---|---|---|
| Value prop do 5 s — co, pro koho, proč | Obecný nadpis bez cílovky a výsledku | ❌ |
| Trust brzy: loga, čísla, výsledky | Reference až 4. sekce, v carouselu | ❌ |
| Příklady místo kategorií | 6 obecných dlaždic | ◐ |
| Nízkorizikový první krok | Jen „Nezávazná poptávka" | ❌ |
| Konverzní prvek brzy v cestě | Formulář až na konci | ❌ |
| Přímé kontakty + kdo se ozve | Telefon jen v patičce, bez jména | ◐ |

## 3. Doporučení v plném řetězci

### D1 · Konkrétní hero do jedné obrazovky
- **Zjištění:** 58 % desktop sessions nedojde do 25 % stránky; nadpis je zaměnitelný.
- **Vyvození:** návštěvník nepozná, že je na správném místě.
- **Zadání:** H1 s cílovkou a výsledkem („Správa IT pro firmy do 50 lidí — odpovíme do 30 minut, platíte fixně za uživatele"); podnadpis s jedním číslem; fotka týmu místo serverovny; výška sekce ≤ 100vh na 1366×768.
- **Proč:** 57 % času na stránce připadá na obsah nad ohybem (NN/g, Scrolling and Attention); 5s test (Krug, NN/g Homepage Design).
- **Hypotéza:** Protože 58 % lidí odchází před první konkrétní informací, věříme, že konkrétní a kratší hero zvýší podíl dosažení 25 % stránky. Poznáme to podle scroll depth v Clarity.
- **ICE:** 8 · 8 · 9 → 8,3 · **Effort:** malý · **Měření:** scroll do 25 % (výchozí 42 % desktop / 55 % mobil), kliky na CTA v heru.

### D2 · Reference staticky pod hero
- **Zjištění:** reference vidí 19 %; 3. slide nikdo.
- **Zadání:** zrušit carousel; 1 case study s číslem + jméno, pozice, fotka; řada 4–6 log; odkaz „Celá případová studie".
- **Proč:** case studies s čísly = nejsilnější aktivum v B2B (playbook B2B služby); carousely mají nízkou interakci (NN/g; ⚠️ starší data o ~1 % prokliku, princip platí).
- **ICE:** 7 · 8 · 9 → 8,0 · **Effort:** malý · **Měření:** dosažení sekce (výchozí 19 %), kliky na case study.

### D3 · Nízkorizikový první krok
- **Zjištění:** CTA 0,9 % sessions; jediná cesta.
- **Zadání:** primární CTA „Rezervovat 30min audit IT zdarma" (plná barva, jméno technika, rezervační kalendář); sekundární „Stáhnout ceník" (PDF).
- **Proč:** specifický nízkorizikový krok > „Kontaktujte nás" (playbook Poradenství / B2B; LIFT — Anxiety).
- **ICE:** 8 · 7 · 6 → 7,0 · **Effort:** střední · **Měření:** kliky na obě CTA, rezervace, stažení (události viz měřicí plán).

### D4 · Ikony „Proč my" s důkazem
- **Zjištění:** 38 dead clicks (⚠️ směrový signál).
- **Zadání:** ke každé ikoně jednu větu s ověřitelným číslem, nebo odkaz na detail.
- **Proč:** dead clicks = falešná afordance (metodika; LIFT Distraction).
- **ICE:** 5 · 5 · 9 → 6,3 · **Effort:** malý · **Měření:** dead clicks v oblasti.

### D5 · Formulář na 3 pole, výš (odvážnější změna)
- **Zjištění:** formulář vidí 11 %; odpad u „Počet zaměstnanců".
- **Zadání:** pole jméno / e-mail nebo telefon / zpráva; umístit pod služby; nad formulář „Ozve se vám Petr, do 30 minut v pracovní době"; telefon jako `tel:` odkaz.
- **Proč:** v B2B první kontakt jen minimum (playbook Kontakt; ⚠️ HubSpot 4→3 pole je kontextové číslo); rychlost reakce zvyšuje kvalifikaci (⚠️ starší studie, směr platí).
- **ICE:** 7 · 6 · 7 → 6,7 · **Effort:** střední · **Měření:** form start / submit, odpad po polích.

## 4. Měřicí plán

- **Před změnou doměřit (GA4):** `generate_lead` pro odeslání formuláře (dnes existuje), nově `book_consultation` (rezervace) a `file_download` pro ceník; parametr umístění CTA (`hero` / `formular`).
- **Výchozí hodnoty:** scroll 25 % = 42 / 55 %; dosažení referencí 19 / 24 %; CTA 0,9 / 0,6 % sessions; poptávky 12 za 30 dní.
- **Metoda:** před/po (návštěvnost pod hranicí pro A/B), měřit 4 týdny, desktop i mobil zvlášť.

## 5. Wireframe spec

1. **Hero (max. 1 obrazovka):** H1 s cílovkou a výsledkem · podnadpis s číslem · CTA „Rezervovat 30min audit IT zdarma" · sekundární „Stáhnout ceník" · tvář technika
2. **Důkaz:** 1 reference s číslem, jménem a fotkou · 4–6 log
3. **Služby:** 3 balíčky místo 6 dlaždic, každý „pro koho" + cena „od"
4. **Jak začínáme:** audit → převzetí → provoz
5. **Formulář (3 pole)** + kdo se ozve a kdy + přímý telefon a e-mail
6. **Další reference**
7. **O nás** (zkrácené) · blog · patička

## 6. Otevřené body k ověření

- Má firma souhlas klienta s uvedením jména a fotky u reference?
- Je reálná průměrná odezva 14 minut podložená daty z helpdesku?
