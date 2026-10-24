# Lokální AI kolorování fotografií

Vytvořili jsme lokální aplikaci pro macOS, která doplňuje barvy do černobílých fotografií. Používá **FLUX.2 Klein 4B** ve 4bitové kvantizaci prostřednictvím **MFLUX a Apple MLX**. Výpočet běží na GPU přes Metal; po úvodním stažení modelu funguje bez internetu.

## Jak funguje

1. Model vytvoří tři barevné návrhy fotografie pomocí různých seedů. Prompt lze upravit a doplnit známé barvy oděvů či předmětů.
2. Aplikace převede originál i návrh do barevného prostoru CIELAB. **Jasovou složku L* zachová z originálu a z návrhu převezme pouze barvy a*, b*.**
3. Barvy přepočítá do původního rozlišení a filtruje podle hran originálu. Barvy mimo rozsah sRGB upraví snížením sytosti při zachování jasu.
4. Uživatel vybere variantu, nastaví sytost a uloží výsledek. Originální soubor se nikdy nepřepisuje.

## Co jsme připravili

- Aplikaci **Lokální Kolor.app** spouštěnou dvojklikem, s vlastním Pythonem a lokálně uloženým modelem.
- Otevření a přetažení JPEG, PNG a TIFF, porovnání vedle sebe i posuvníkem před/po.
- Tři barevné varianty, sytost 0–150 %, úpravu promptu, dávkové zpracování a zrušení úlohy.
- Export do 16bitového PNG/TIFF nebo JPEG, český návod a dokumentaci.
- Úsporný provoz: obrazový model zůstává mezi snímky načtený, výsledek kódování promptu se uchovává a textový enkodér se uvolní.
- Opravu verze 1.0.1: chybějící instalační metadata MFLUX již nezastaví první kolorování.

## Ověření a omezení

Na MacBooku Air M5 s 16 GB RAM jsme ověřili skutečný běh na Metal GPU, provoz s blokovanou sítí, dávku, exporty i zrušení výpočtu. Prošlo **23 automatických testů**. Jedna varianta při 512 px trvala přibližně 21 sekund; při 1024 px přibližně 89 sekund se špičkou paměti MLX kolem 8 GB. Finální obraz zachovává rozlišení originálu.

V testovaných 16bitových PNG byla maximální odchylka L* menší než 0,001 na stupnici 0–100. **Barvy jsou však odhadem, nikoliv zaručenou rekonstrukcí historické skutečnosti.** Model například zvolil zelený skafandr místo původního oranžového; doplnění doložené barvy do promptu pomohlo. Barevné hranice je potřeba vizuálně zkontrolovat. Pro přesné zachování jasu používejte PNG nebo TIFF, protože JPEG je ztrátový.
