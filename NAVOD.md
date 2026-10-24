# Lokální Kolor — stručný návod

## Spuštění

Ve Finderu otevřete **Lokální Kolor.app** dvojklikem. Alternativou je `Spustit.command`. Před prvním spuštěním použijte `Instalovat.command`; poté není potřeba zadávat příkazy do Terminálu ani být administrátorem. Přemisťujte celou složku `LokalniKolor`, protože `.app` používá přibalený Python, knihovny a model v sousedních složkách.

## Jedna fotografie

1. Klikněte na **Otevřít fotografii…** nebo fotografii přetáhněte do okna. Podporované formáty jsou JPEG, PNG a jednostránkový TIFF.
2. Začněte velikostí **512 px**. Jde o velikost barevného návrhu; uložená fotografie zachová plné rozlišení originálu. 768 a 1024 px jsou podrobnější a potřebují více paměti i času.
3. V pokynech ponechte základní prompt a připojte známé skutečnosti o barvách. Například: `The coat is dark navy, the shirt is white, the car is burgundy red.` Model lépe rozumí konkrétním pokynům v angličtině. Doložené barvy jsou důležitější než dlouhý obecný popis.
4. Klikněte na **Vytvořit 3 varianty**. Varianty vzniknou se třemi různými seedy. První úloha načítá model; další fotografie se stejnými pokyny jej využijí z paměti.
5. Vyberte variantu **1–3** a nastavte sytost v rozsahu **0–150 %**. Změna sytosti nepouští znovu AI. Hodnota 0 % vytvoří neutrální obraz s původním jasem.
6. Prohlédněte si fotografie **Vedle sebe** nebo přepněte na **Před / po** a použijte posuvník pod obrazem. Zkontrolujte zejména pleť, vlasy, okraje oděvů a malé předměty.
7. Zvolte **PNG · 16 bitů** nebo **TIFF · 16 bitů**, klikněte na **Uložit…** a vyberte cílovou složku. JPEG je vhodný pro sdílení, ale jeho ztrátová komprese mění i jas.

Výstup má název `puvodni_nazev_kolor.png` (případně `.tiff` či `.jpg`). Při shodě názvu aplikace přidá číslo. Existující soubor ani originál nikdy nepřepíše. Výchozí složka výsledků je `vysledky/`; tlačítko **Otevřít výsledky** otevře naposledy vybranou složku.

## Dávka

Klikněte na **Zpracovat složku…**, vyberte vstupní a potom výstupní složku. Dávka používá právě zvolené pokyny, rozlišení, sytost, formát a seedy. Z každého snímku uloží tři finální barevné varianty; druhá a třetí mají přípony `_kolor_v2` a `_kolor_v3`.

Dávka prochází pouze soubory přímo ve zvolené složce. Podsložky neprochází. Názvy odpovídající vlastním výstupům `_kolor`, `_flux_seed…` a `_nahled_v…` vynechá, aby opakovaně nekolorovala výsledky. Jedna vadná fotografie nezastaví zbytek dávky; chyby jsou v závěrečném oznámení a souboru `davka*.json`.

Dávka ukládá také diagnostické podklady: `_flux_seed…` je generativní barevný návrh, `_nahled_v…` náhled a `*_mereni.json` obsahuje nastavení a měření. Pro archivaci používejte finální soubory **`*_kolor*`**. Surový FLUX návrh může měnit kresbu, a proto jej nepovažujte za věrnou finální fotografii.

## Zrušení a paměť

Tlačítko **Zrušit** ukončí výpočetní proces a uvolní jeho paměť. Rozpracovaná fotografie se neuloží jako finální výsledek; hotové soubory z předchozích snímků dávky zůstanou. Další úloha znovu načte model. Při změně promptu se také znovu načte nativní enkodér; mezi fotografiemi se stejným promptem zůstává obrazový model načtený.

Na tomto MacBooku Air M5 měl úsporný režim při 1024 px špičku přibližně 8,04 GB paměti MLX. Pro běžnou práci je výchozích 512 px vhodnější. U velmi velkých skenů spotřebuje další paměť přenos barev v plném rozlišení a náhledy. Pokud macOS zároveň používá další náročné aplikace, zvolte menší barevný návrh.

## Co výsledek zaručuje a co vyžaduje kontrolu

Finální jasová složka L* pochází z originálu; AI se používá pouze pro barevný návrh. Originál se neostří, nevyhlazuje a neprovádí se rekonstrukce obličeje. V testovaných 16bitových PNG byla maximální chyba L* menší než 0,001 na stupnici 0–100.

Barvy zůstávají odhadem. Bez konkrétního kontextu model například obarvil původně oranžový skafandr na zeleno. Pokyny s doloženou oranžovou barvou výsledek podstatně zlepšily. Ani shodný jas neprokazuje správnost barevných hranic: chybný návrh může obarvit nesprávnou část obličeje nebo předmětu. Takový výsledek nepoužívejte jako historický důkaz.

Všechny výpočty běží v tomto Macu, bez inferenčního API. Připravený model funguje bez internetu; bylo to ověřeno i s připojením zablokovaným na úrovni macOS.

Další podrobnosti jsou v `NASTAVENI.md` a `INSTALACE.md`.
