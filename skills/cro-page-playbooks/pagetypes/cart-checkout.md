# Page type: Košík / checkout

*Primární autorita: Baymard (checkout UX benchmark a guidelines).*

## Primární cíl (rozliš košík vs checkout)
- **Košík** = rozhodovací/verifikační uzel: „Mám správné věci? Kolik to celkem stojí?" Minimalizuje **nejistotu o ceně/obsahu**. (42 % amerických online nakupujících někdy opustilo košík, protože „jen koukali / nebyli připravení koupit" — to NENÍ UX chyba; Baymard to z důvodů níže vyřazuje.)
- **Checkout** = transakční tunel: dokončit platbu s minimem tření. Minimalizuje **tření při placení**.
Záměna cílů (upsell v checkoutu, skrytá doprava v košíku) = systémová chyba.

## Ideální struktura
**Košík:** plný order cost už tady (položky + doprava/odhad + daně + total) · free-shipping threshold indikátor · inline edit (množství/varianta/smazat) · continue shopping sekundárně.
**Checkout (pořadí):** 1. **Guest checkout nejprominentnější** · 2. shipping/adresa (autofill, ZIP→město) · 3. doprava (volba + cena + **datum doručení**) · 4. platba (**digital wallets nahoře**, pak karta) · 5. review · 6. **account creation až na děkovačce**.
- **Nehoň počet kroků** — kvalita kroku > počet (Baymard). Multi-step s progress trackerem u hodně polí; single-column vždy; **enclosed checkout** (odebrat hlavní nav).
- **Počet polí:** průměrný checkout má 11,3 formulářových polí (Baymard 2024), většině e-shopů stačí **8**. Každé pole navíc obhaj.

## Must-have + umístění
Cart summary s plným totalem (sticky v checkoutu) · doprava transparentně (cena + datum) · guest checkout první · digital wallets above the fold · trust/security u pole karty · edit možnosti · return policy odkaz viditelně · progress indikátor · inline validace + jasné error hlášky.

## Informační hierarchie
1. **Total vč. dopravy a daní** — nejvyšší priorita, žádné překvapení později. 2. Doprava: cena + datum doručení. 3. Primární CTA dominantní, jeden na obrazovku. 4. Order summary prominentně, na mobilu **above the fold**. 5. Co se kupuje (verifikovatelné). 6. Rozptýlení (promo/upsell) vizuálně podřízené.

## Nejčastější selhání + čísla (Baymard, důvody opuštění)
**Příliš vysoké dodatečné náklady 40 %** · pomalé doručení 20 % · nedůvěra webu s kartou 19 % · **nucená registrace 18 %** · dlouhý/komplikovaný checkout 17 % · chyby/pády webu 17 % · nevyhovující vrácení 13 % · **nešlo předem zjistit celkovou cenu 12 %** · zamítnutá karta 10 % · málo platebních metod 9 %. *(Baymard, stav 09/2025, bez „jen koukal". Globální abandonment 70,22 %; lepší design = +35,26 % konverze.)*
⚠️ V agregátorech kolují starší ročníky průzkumu (např. 48 % / 26 %) — drž aktuální vydání Baymardu.

## Nejúčinnější fixy
Plná transparentnost nákladů co nejdřív + free-shipping threshold (40 % + 12 %) · prominentní guest checkout, účet až na děkovačce (18 %) · osekat pole k ~8, single column, autofill (17 %) · digital wallets nahoře (9 %) · delivery date místo „shipping speed" (20 %) · trust u karty + viditelná return policy (19 % + 13 %) · enclosed checkout.
**Co NEfunguje na UX-caused abandonment:** exit-intent popupy, slevy bez opravy UX, retargeting (léčí symptom).

## Mobil vs desktop
Checkout mobilně extra citlivý. Kontextové klávesnice (numpad karta, e-mail klávesnice) · autofill kriticky · dropdowny → text fieldy (stát, expirace) · digital wallets above the fold · order summary above the fold · card scanning · velké touch targety.

## Clarity signály
Rage clicks na „Zaplatit" (nereagující/visící submit, double-submit bez feedbacku) · dead clicks (statický trust badge, „cena" vypadající editovatelně) · quickbacks (náklad odhalený pozdě, matoucí krok) · scroll/excessive scroll (total/CTA pod foldem, hl. mobil) · **form field drop-off / „completed never submitted"** (validation friction / tichý backend fail) · JS errors (skript konflikt při submitu — koreluj s drop-off krokem).

## Citace
Baymard (Checkout Usability Report & Benchmark, Cart Abandonment Rate 09/2025 — https://baymard.com/lists/cart-abandonment-rate, Checkout form fields 2024 — https://baymard.com/blog/checkout-flow-average-form-fields), NN/g (Mobile Checkout, Carts/Checkout/Registration), Microsoft Clarity (Why Checkouts and Forms Fail). ⚠️ Split mobil/desktop a wallet uplift % = agregátory, ne Baymard — směrové. Čísla Baymardu ověřena 09/2026; signal→problém mapping = CRO interpretace nad Clarity definicemi.
