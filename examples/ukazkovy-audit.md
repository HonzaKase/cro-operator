# CRO audit — Ukázka IT s.r.o., homepage

**Stránka:** https://example.cz/ · **Typ:** homepage · **Segment:** B2B služby · **Primární konverze:** poptávka / rezervace konzultace
**Datum:** 29. 9. 2026 · **Datové okno:** posledních 90 dní (Microsoft Clarity), 30 dní (GA4)

> **Fiktivní ukázka.** Firma, web i všechna čísla jsou vymyšlené. Takhle vypadá klientská verze auditu z `/cro-operator:cro`. Detail pro realizaci je v [technické příloze](ukazkova-technicka-priloha.md).

## 1. Shrnutí

Homepage dnes lidi **nevede k poptávce, ale k odchodu**. Nejde o rozbitý web — chyby a frustrace jsou téměř nulové. Jde o pořadí obsahu: to, co přesvědčuje (nabídka, reference, formulář), leží tam, kam většina lidí nedojde. Opravy jsou proto hlavně obsahové, ne vývojářské.

| Ukazatel | Počítač | Mobil |
|---|---|---|
| Návštěvy (90 dní) | 2 140 | 1 309 |
| Dojdou aspoň do čtvrtiny stránky | 42 % | 55 % |
| Uvidí reference | 19 % | 24 % |
| Kliknou na „Nezávazná poptávka" | 0,9 % | 0,6 % |

**Tři hlavní zjištění:**

1. **Úvodní sekce lidi odrazuje.** Obecný nadpis a velká fotka zaberou víc než obrazovku; 58 % lidí na počítači odejde dřív, než se dozví, co firma dělá a pro koho. *Co s tím:* konkrétní nadpis s cílovkou a výsledkem, sekce do jedné obrazovky.
2. **Nejsilnější reference je schovaná v carouselu.** Případovou studii „výpadky serveru z 11 za rok na 0" v nahrávkách neviděl nikdo. *Co s tím:* dát ji staticky hned pod úvod.
3. **Chybí lehký první krok.** „Nezávazná poptávka" je pro majitele malé firmy při první návštěvě moc velký závazek. *Co s tím:* nabídnout 30min audit IT zdarma a ceník ke stažení.

## 2. Co návštěvníci reálně dělají

**Scroll útes pod úvodem.** Úvodní sekce zabírá na notebooku 1,4 obrazovky. Většina lidí se vrátí nebo odejde dřív, než uvidí první konkrétní informaci.

> 📷 Vložit screenshot: Clarity → Heatmaps → / → Scroll map (desktop, posledních 90 dní)

**Kliky jdou mimo tlačítka.** Lidé klikají na tři ikony u „Proč my", které nikam nevedou — čekají, že se dozví víc. Tlačítko poptávky dostane méně kliků než logo.

> 📷 Vložit screenshot: Clarity → Heatmaps → / → Click map (desktop, posledních 90 dní)

**Reference nikdo neprojde.** Carousel se sám posouvá po 4 sekundách; ze 14 prošlých nahrávek se ke 3. slidu nedostal nikdo.

**Formulář je až v patičce.** Vidí ho 11 % lidí na počítači a nejvíc jich odpadá u povinného „Počet zaměstnanců".

## 3. Doporučení

| # | Doporučení | Priorita | Náročnost | Kdo |
|---|---|---|---|---|
| 1 | Konkrétní úvodní sekce do jedné obrazovky | vysoká | malá | klient (web) |
| 2 | Nejsilnější reference staticky pod úvod | vysoká | malá | klient (web) |
| 3 | Lehký první krok: audit zdarma + ceník | vysoká | střední | klient (web) |
| 4 | Ikony „Proč my" rozvést do textu s důkazem | střední | malá | klient (web) |
| 5 | Formulář na 3 pole a výš na stránku (odvážnější změna) | střední | střední | klient (web) |
| — | Nastavit měření rezervací a stažení ceníku | předpoklad | malá | my |

### 3.1 Konkrétní úvodní sekce do jedné obrazovky
**Co jsme zjistili:** 58 % lidí na počítači nedojde do čtvrtiny stránky; nadpis „Vaše IT v bezpečných rukou" by mohl použít kterýkoli konkurent.
**Co doporučujeme:** nadpis s cílovkou a výsledkem, např. „Správa IT pro firmy do 50 lidí — odpovíme do 30 minut, platíte fixně za uživatele". Místo fotky serverovny lidé z týmu. Celá sekce do jedné obrazovky.
**Proč:** obsah nad ohybem dostává většinu času stráveného na stránce (NN/g) a homepage musí do 5 sekund říct, co to je a pro koho.
**Jak poznáme, že to funguje:** víc lidí dojde do čtvrtiny stránky (dnes 42 %).

### 3.2 Nejsilnější reference staticky pod úvod
**Co jsme zjistili:** reference vidí 19 % lidí a tu nejsilnější nikdo.
**Co doporučujeme:** carousel zrušit; pod úvod jednu referenci s číslem, jménem a fotkou klienta a řadu 4–6 log.
**Proč:** u B2B služeb jsou případové studie s čísly nejsilnější argument při rozhodování; carousely lidé přeskakují jako reklamu (NN/g).
**Jak poznáme, že to funguje:** víc lidí dojde k referencím a klikne na celou případovou studii.

### 3.3 Lehký první krok: audit zdarma + ceník
**Co jsme zjistili:** na poptávku klikne 0,9 % návštěv; jiná cesta neexistuje.
**Co doporučujeme:** hlavní tlačítko „Rezervovat 30min audit IT zdarma" (se jménem technika) a vedle „Stáhnout ceník".
**Proč:** konkrétní nízkorizikový krok funguje líp než obecné „Kontaktujte nás" a snižuje obavu z prvního kontaktu (LIFT).
**Jak poznáme, že to funguje:** rezervace a stažení ceníku (měření nastavíme my).

### 3.4 Ikony „Proč my" rozvést do textu s důkazem
**Co jsme zjistili:** lidé na ikony klikají, ale nic se nestane.
**Co doporučujeme:** ke každé ikoně jednu větu s důkazem, např. „Odezva do 30 minut — průměr za 2025: 14 minut".
**Proč:** prvek, který vypadá klikatelně a nereaguje, zvyšuje nejistotu a odvádí pozornost od hlavní akce.
**Jak poznáme, že to funguje:** kliky naprázdno v té oblasti zmizí.

### 3.5 Formulář na 3 pole a výš na stránku
**Co jsme zjistili:** formulář vidí 11 % lidí; odpadají u „Počet zaměstnanců".
**Co doporučujeme:** 3 pole (jméno, kontakt, zpráva) hned pod služby; zbytek doptat v hovoru; nad formulář „Ozve se vám Petr, do 30 minut".
**Proč:** v B2B má první kontakt chtít jen nutné minimum; kvalifikace patří do hovoru.
**Jak poznáme, že to funguje:** víc lidí formulář začne i dokončí.

## 4. Postup a měření

1. **Týden 1:** my nastavíme měření rezervací a stažení ceníku.
2. **Týden 1–2:** doporučení 1–3 najednou (hlavně texty a pořadí sekcí).
3. **Druhá vlna:** doporučení 4–5.
4. **Vyhodnocení:** porovnání před a po, 2–4 týdny po nasazení; pak znovu audit na stejnou stránku. Na A/B test je návštěvnost malá.

## 5. Výhrady

- Clarity ukazuje, **kde a proč** lidé odcházejí, ne kolik poptávek změny přinesou. To ověříme v GA4.
- Kvůli souhlasu s cookies Clarity nevidí všechny návštěvníky — čísla jsou spodní hranice.
- Kliky naprázdno na ikonách (38) jsou na hranici spolehlivosti, berte je jako směr.
