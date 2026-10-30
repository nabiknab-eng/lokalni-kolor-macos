# bicolor 1.9.1 — ovládání a práce s fotografiemi

[Popis programu](README.md) · [Instalace](INSTALACE.md)

## Jak kolorování funguje

AI nejprve vytvoří malý barevný vzor. Program z něj převezme barvy a přenese je na původní fotografii, podle jejího jasu a hran. Geometrie, kresba a zrno vycházejí z původního snímku. Velikost vzoru se proto liší od velikosti výsledku: například fotografie 4000 × 3000 pixelů se uloží v těchto rozměrech i při vzoru 512 px.

Ze samotné černobílé fotografie obvykle nelze určit skutečné barvy. Výsledky jsou odhadem. Model může zaměnit oděv, pleť nebo pozadí; doložené barvy připiš do pokynů a výsledek vždy zkontroluj.

## Otevření a základní nastavení

| Ovladač | Co dělá |
| --- | --- |
| **Otevřít fotografii…** | Otevře jeden snímek. Fotografii lze také přetáhnout do okna. Nový vstup nahradí neuložené varianty aktuální fotografie. |
| **Dávkové zpracování…** | Otevře samostatný dialog pro více souborů. Zadání složek a spuštění dávky jsou popsané níže. |
| **Název fotografie** | Ukazuje aktuální soubor. Dlouhý název se zkrátí uprostřed; celý je v nápovědě po najetí myší. |
| **Negativ** | Vratně digitálně převrátí černobílý negativ. Přepnutí zahodí dosavadní neuložené barevné varianty. Pokud ještě žádné varianty nejsou, lze uložit samotný pozitiv. |
| **Barevný vzor** | Velikost barevného návrhu AI: **512, 768 nebo 1024 px**. Výchozích 512 px je nejúspornější. Vyšší hodnota může změnit návrh barev, ale nezaručuje lepší výsledek. |
| **Počet variant** | Vytvoří **1 až 3** návrhy. Více variant znamená více výpočtů. Změna čísla sama nezačne kolorovat. |
| **Seedy** | Startovní čísla generátoru náhody, oddělená čárkami. Počet odpovídá zvolenému počtu variant. Seznam se při změně počtu doplní nebo zkrátí. |
| **Vytvořit … variantu / varianty** | Spustí nové kolorování podle aktuálního vstupu, vzoru, seedů a pokynů. Předchozí neuložené návrhy nahradí. |
| **Sytost** v záložce Kolorování | Síla přenosu barev do výsledku, v rozsahu **0–150 %**. Výchozí je 100 %, při 0 % je obraz neutrální. Změna hotové varianty nepouští AI znovu. |
| **Pokyny a doložené barvy** | Textové zadání pro AI. Ponech základní instrukce a doplň konkrétní známé barvy nebo požadované přirozené podání. |

Negativ je jednoduché převrácení. Neodstraňuje oranžovou masku barevného filmu a neprovádí kalibraci skeneru ani automatickou tonální rekonstrukci.

### Co znamenají seedy

Výchozí seedy jsou `42, 43, 44`. Číslo neznamená kvalitu, sílu ani konkrétní barvu. Vyšší seed není lepší. Každý seed musí být celé číslo **0–4294967295**, seedy musí být různé a musí jich být právě zvolený počet.

Pro srovnání dvou textových zadání můžeš nechat stejné seedy. Příklad vlastního zadání je `7, 125, 8000`. Pokud rozepsaný seznam není platný, oprav jej před spuštěním; program jej při změně počtu svévolně nepřepíše.

### Příklady doplnění pokynů

Základní text žádá přirozené kolorování při zachování původní fotografie. Na jeho konec přidej krátké věty. Angličtina odpovídá výchozímu zadání, například:

| Co chceš upřesnit | Příklad |
| --- | --- |
| Oděv | `The woman's coat is navy blue. Her blouse is ivory white.` |
| Více osob | `The man on the viewer's left wears a brown jacket. The child wears a light blue shirt.` |
| Pleť | `Use natural skin colors with subtle variation. Keep shaded skin subdued, without green or purple casts.` |
| Pozadí | `The plaster wall is warm off-white. The window frames are dark green.` |
| Předmět | `The bicycle frame is dark red. The leather saddle is brown.` |

Osobu nebo předmět určuj polohou a jasnými znaky. Popis nemusí model vždy dodržet a samotný text nezaručí přesnou hranici barev. Změna pokynů začne platit až po novém stisknutí **Vytvořit**.

## Záložka Kolorování

Vlevo je **Originál**, případně **Pozitiv z negativu**; vpravo **Kolorováno**. Vyber jednu z hotových variant tlačítky **Varianta 1 / 2 / 3** vpravo nad fotografiemi. Zvýrazněné číslo označuje aktuální variantu. Po najetí na číslo se zobrazí seed a čas generování.

Samotné přepnutí hotové varianty nepouští AI znovu. Při změně sytosti nebo výřezu může být potřeba dopočítat nový náhled. Ovládání může být během přípravy nového podkladu dočasně zablokované.

**Uložit kolorování…** uloží vybranou variantu s hodnotou sytosti z této záložky.

## Záložka Úpravy

Vlevo je pevná reference **Varianta · sytost 100 %**, vpravo **Upraveno**. Reference patří právě vybrané variantě a nemění ji sytost z první záložky ani nastavení čtyř táhel.

| Táhlo | Výchozí hodnota | Rozsah | Účinek |
| --- | ---: | ---: | --- |
| **Sytost** | 100 % | 0–150 % | Zeslabí nebo zesílí barvy. Při 0 % odstraní i barevný posun teploty. |
| **Jas** | 0 | −50 až +50 | Ztmaví nebo zesvětlí obraz. |
| **Kontrast** | 0 % | −100 až +100 % | Záporné hodnoty zjemní rozdíly světel a stínů, kladné je zesílí. |
| **Teplota** | 0 | −100 až +100 | Doleva chladnější, doprava teplejší podání. Hodnota je relativní posun, nikoli teplota v kelvinech. |

Při výchozích hodnotách jsou oba obrazy stejné. Každý přepočet vychází z pevné reference, takže se chyby nesčítají opakovaným posouváním. Při změně varianty zůstanou polohy táhel zachované a vztáhnou se k její vlastní referenci.

**Uložit úpravy…** uloží celý pravý obraz se všemi čtyřmi hodnotami. Sytost z první záložky se do tohoto výsledku nepřidává.

## Zoom a porovnání

| Ovladač nebo gesto | Účinek |
| --- | --- |
| **Přizpůsobit oknu** | Ukáže celou fotografii podle dostupného místa. |
| **12,5–800 %** | Pevné zvětšení; při **100 %** odpovídá jeden pixel fotografie jednomu fyzickému pixelu displeje, i na Retině. |
| **− / +** | Postupně mění zoom. |
| **Kolečko myši** | Mění zoom. |
| **Tažení zvětšeného obrazu** | Společně posouvá oba porovnávané výřezy. |
| **Dvojklik** | Přepne mezi 100 % a přizpůsobením oknu. |
| **Posun dvěma prsty na trackpadu** | Ve zvětšeném pohledu posouvá výřez. S Ctrl nebo ⌘ mění zoom. |

Náhled se počítá pro displej, při zoomu pro viditelný výřez. Připravené obrazy a jejich úpravy se uchovávají v omezené paměti pro rychlejší návrat. Zmenšený náhled se může na jemných kontrastních hranách mírně lišit od zmenšeného finálního exportu. Pro posouzení těchto míst použij 100% detail.

Uložení vždy znovu připraví celý přesný obraz z původních dat. Rozměry souboru neomezují velikost okna, zoom ani zmenšený náhled.

## Uložení a barevné prostory

Blok **Uložení** je připnutý dole vlevo a zůstává dostupný v obou záložkách. Před uložením vyber formát a barevný prostor.

| Volba | Kdy ji použít |
| --- | --- |
| **Adobe RGB (1998)** | Pro další práci v editoru se správou barev a postup, který s Adobe RGB počítá. Je výchozí volbou. |
| **sRGB** | Pro běžné sdílení a zobrazení. |
| **PNG · 16 bitů** | Bezeztrátový soubor pro jemné tóny, kresbu a další úpravy. |
| **TIFF · 16 bitů** | Bezeztrátový soubor pro fotografický pracovní postup. |
| **JPEG · 8 bitů** | Menší ztrátový soubor pro sdílení. |
| **HEIC · 8 bitů** | Menší ztrátový soubor pro prostředí podporující HEIC. |
| **Otevřít výsledky** | Otevře poslední výstupní složku ve Finderu. |

Vzorky se při exportu skutečně převedou do vybraného prostoru a vloží se ICC profil. Náhled používá sRGB. Adobe RGB nepřidává nové doložené barvy ani detaily nad rámec návrhu AI.

Originál se nepřepisuje. Výstup má například jméno `foto_kolor.png`, upravený snímek `foto_upraveno.png` nebo samostatný pozitiv `foto_pozitiv.png`. Při shodě názvu vznikne další očíslovaný soubor.

Poslední **vstupní a výstupní složka** se pamatují i po restartu a sdílejí se s dávkou. Zrušení samotného výběru složky nic nepřepíše. Pokud dříve zapamatovaná složka není dostupná, nabídne se dostupné výchozí umístění.

## Dávkové zpracování

1. Nejdřív v hlavním okně nastav **Barevný vzor**, **Počet variant**, **Seedy**, **Pokyny**, výstupní formát a barevný prostor. Pro negativy nastav také **Negativ**.
2. Klikni na **Dávkové zpracování…**.
3. Zkontroluj **Vstupní složku — původní fotografie** a **Výstupní složku — uložené výsledky**. Předvyplňují se poslední použité adresáře, případně je změň.
4. Zkontroluj počet vstupů, počet variant na fotografii a celkový počet výsledků.
5. Stiskni **Spustit dávku**. Pouhý výběr složek výpočet nespustí.

Dávka ukládá **pouze čisté kolorované varianty při sytosti 100 %**, bez následných úprav táhly. Každý snímek dostane zvolený počet variant ve vybraném formátu a ICC prostoru. Do cílové složky se nepřidávají pracovní náhledy, návrhy AI ani diagnostické JSON soubory.

Nastavení pokynů, seedů, velikosti vzoru a přepínače **Negativ** platí pro celou dávku. Pro rozdílná zadání nebo smíšené pozitivy a negativy připrav samostatné dávky.

Podsložky se neprocházejí. Soubory s názvy odpovídajícími vlastním vygenerovaným výsledkům program vynechává; pro přehlednost používej zvláštní vstupní a výstupní složku. Dávka nabízí spuštění až při platných složkách a alespoň jednom podporovaném vstupu.

**Zrušit** v dialogu zavře nastavení bez spuštění. Pokud jsi v něm předtím vybral nové platné adresáře, zůstanou zapamatované. Tlačítko **Zrušit** během samotného zpracování zastaví výpočet; již uložené výsledky zůstanou. Další výpočet může znovu načítat model.

## Podporované vstupy a omezení

Vstupní přípony jsou **.jpg, .jpeg, .jpe, .jfif, .png, .tif, .tiff, .heic, .heif, .hif, .bmp, .webp a .avif**. Velikost písmen nerozhoduje. Limit fotografie je **80 milionů pixelů**.

Z HEIC/HEIF se používá hlavní SDR fotografie a zohledňuje se její orientace. Výstup HEIC je 8bitový; vyšší vstupní bitová hloubka, HDR gain mapy a hloubkové mapy se tímto pracovním postupem nezachovávají. Vícestránkový TIFF a animované vstupy nejprve rozlož na samostatné snímky. Částečně průhledné fotografie nejprve sluč s pozadím.

Přenos podle jasu a hran nerozpoznává dokonale hranice skutečných objektů. Dvě plochy podobného jasu mohou přijmout barvu ze sousedství. Více variant, menší sytost a přesnější pokyny mohou pomoci s výběrem, ale nejsou zárukou správné pleti nebo historicky přesné barvy.

## Kdy je potřeba nový výpočet AI

| Změna | Nové stisknutí Vytvořit |
| --- | --- |
| Jiná fotografie, pokyny, seedy nebo velikost vzoru | Ano |
| Jiný počet budoucích variant | Ano, pro vytvoření nových návrhů |
| Výběr již hotové varianty | Ne |
| Sytost, jas, kontrast nebo teplota hotové varianty | Ne |
| Zoom nebo posun | Ne |
| Formát a barevný prostor při uložení | Ne |

## Běžné potíže

**Málo paměti nebo zastavený výpočet:** zavři ostatní náročné aplikace, vyber 512 px a jednu variantu. Paměťová ochrana může zastavit pracovní proces; již uložené výsledky zachová.

**Přepnutí nebo nové nastavení chvíli trvá:** připravené obrazy se vracejí z paměti. Nová varianta, dosud nepřipravená sytost nebo výřez vyžadují výpočet náhledu. První načtení modelu po spuštění bývá delší než další práce.

**Nečekané barvy:** ověř jinou variantu, sniž sytost a upřesni zadání. Jasové hrany nejsou úplnou informací o skutečných objektech.

**Chybí model nebo instalace není dokončená:** znovu spusť **Instalovat.command** ve stejné složce. [Instalační postup](INSTALACE.md).

Před otevřením jiné fotografie, novým generováním nebo zavřením si vybraný výsledek ulož. Program automaticky neobnovuje rozpracované neuložené varianty jako projekt.
