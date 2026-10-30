# bicolor 1.9.1

**Lokální AI kolorování černobílých fotografií pro Mac s Apple Silicon.**

bicolor vytvoří jednu až tři barevné varianty a přenese jejich barvy na původní fotografii. Rozměry, kresba a zrno výsledku vycházejí z originálu. Fotografie se zpracovávají v Macu, bez cloudového kolorování a bez předplatného API.

[Instalace](INSTALACE.md) · [Podrobný návod a ovladače](NAVOD.md) · [Co je nového](CHANGELOG.md)

**[Stáhnout aktuální instalaci pro Mac](https://github.com/nabiknab-eng/lokalni-kolor-macos/releases/latest)**

## Stažení a požadavky

V části **[Releases](https://github.com/nabiknab-eng/lokalni-kolor-macos/releases/latest) → Assets** stáhni **`bicolor-1.9.1-macOS-arm64.zip`**. ZIP obsahuje instalační složku; Python ani knihovny nemusíš instalovat samostatně; instalátor vše připraví automaticky.

Pro instalaci nepoužívej automatické soubory **Source code (zip/tar.gz)** ani **Code → Download ZIP**. Jsou určené k prohlížení zdrojů a neobsahují připravenou distribuční sestavu.

| Požadavek | Hodnota |
| --- | --- |
| Mac | Apple Silicon, M1 nebo novější |
| Systém | macOS 26 nebo novější |
| Paměť | alespoň 16 GB RAM |
| Disk | doporučeno alespoň 12 GiB volného místa pro instalaci; další prostor pro fotografie a výsledky |
| Připojení | potřebné při první instalaci knihoven (asi 314 MB) a modelu (přibližně 4,62 GB) |

Rozbal ZIP, přesuň **celou složku** na trvalé místo a spusť **Instalovat.command**. Po dokončení spouštěj **bicolor.app**. Přibalené prostředí Pythonu se rozbalí do této složky. Instalátor automaticky stáhne připnuté knihovny z PyPI (asi 314 MB) a jeden model z Hugging Face (4,62 GB); kontroluje jejich SHA-256. Podrobnosti a postup při blokaci macOS jsou v [návodu k instalaci](INSTALACE.md).

## První fotografie

1. Klikni na **Otevřít fotografii…** nebo snímek přetáhni do okna.
2. Pro začátek nech **Barevný vzor 512 px** a zvol **1 variantu**.
3. Do **Pokynů a doložených barev** případně připiš známé barvy oděvů, předmětů a okolí.
4. Klikni na **Vytvořit 1 variantu**. Pro porovnání můžeš příště vytvořit až tři.
5. Zkontroluj výsledek, především pleť a barevné hranice při zoomu **100 %**.
6. Vyber barevný prostor, formát a klikni na **Uložit kolorování…**. Pro další úpravy a zachování jemných tónů zvol 16bitový PNG nebo TIFF.

## Co program umí

- **Kolorování:** originál vlevo, vybraná barevná varianta vpravo. Barvy můžeš zeslabit nebo zesílit sytostí.
- **Úpravy:** porovnání vybrané varianty při sytosti 100 % s výsledkem táhel **Sytost, Jas, Kontrast a Teplota**.
- **Jedna až tři varianty:** vlastní seedy a textové zadání pro AI. Přepínač variant zůstává nad fotografiemi vedle zoomu.
- **Negativ:** vratné digitální převrácení černobílého negativu; pozitiv lze také samostatně uložit.
- **Zoom:** přizpůsobení oknu, 12,5–800 %, společné posouvání obou obrazů. Při 100 % odpovídá pixel fotografie fyzickému pixelu displeje.
- **Dávkové zpracování:** jasně označená vstupní a výstupní složka, souhrn počtu výsledků a samostatné tlačítko **Spustit dávku**.
- **Zapamatované složky:** poslední vstup a výstup se sdílejí mezi jednotlivými fotografiemi a dávkami a obnovují se po restartu.
- **Rychlé náhledy:** hotové varianty a jejich úpravy se uchovávají v omezené paměti; při zoomu se připravuje viditelný výřez. Ukládání vždy počítá celý výsledek z původních dat.

Barevný vzor AI má volby **512, 768 a 1024 px**. Tento údaj omezuje velikost návrhu barev, nikoli rozlišení uložené fotografie. Používá se jeden model **FLUX.2 Klein 4B v 4bitové MLX podobě**.

## Formáty a barvy

**Vstupy:** JPG/JPEG/JPE/JFIF, PNG, TIF/TIFF, HEIC/HEIF/HIF, BMP, WebP a AVIF. Stejné přípony platí pro dialog, přetažení i dávku; velikost písmen nerozhoduje. Limit vstupu je 80 milionů pixelů.

| Výstup | Vlastnosti |
| --- | --- |
| PNG | 16 bitů na kanál, bezeztrátový |
| TIFF | 16 bitů na kanál, bezeztrátový |
| JPEG | 8 bitů na kanál, ztrátový |
| HEIC | 8 bitů na kanál, ztrátový |

Všechny výstupy používají vybraný **Adobe RGB (1998)** nebo **sRGB** s vloženým ICC profilem. Originály a existující výsledky se nepřepisují; při shodě názvu se přidá číslo. HEIC se zpracovává jako hlavní SDR fotografie. HDR gain mapy ani hloubkové mapy se nevyužívají a vyšší bitová hloubka HEIC se nezachovává.

**Dávka ukládá pouze hotové čisté kolorované varianty při sytosti 100 %.** Nepřebírá individuální nastavení táhel a do výstupní složky nepřidává pracovní náhledy ani diagnostiku.

## Co od výsledků čekat

Barvy jsou odhadem, nikoli důkazem skutečných historických barev. Známé barvy je vhodné uvést v zadání. Přenos podle hran může zaměnit sousední plochy podobného jasu, například pleť a pozadí; konečný výsledek vždy zkontroluj.

Program nepřidává generativní detaily a nemá odstraňování zrna. Negativ neodstraňuje oranžovou masku barevného filmu. Zmenšený náhled je přibližný; pro jemné hrany použij 100% detail. [Podrobnosti a řešení problémů](NAVOD.md).

## Soukromí a licence součástí

Instalátor stáhne knihovny z PyPI a model z Hugging Face; běžné kolorování a úpravy potom probíhají lokálně a fotografie se neodesílají ke cloudovému zpracování.

Původní model [FLUX.2 Klein 4B](https://huggingface.co/black-forest-labs/FLUX.2-klein-4B) a použitá [4bitová MLX varianta](https://huggingface.co/mlx-community/flux2-klein-4b-4bit) uvádějí licenci Apache 2.0. [MFLUX](https://github.com/mflux-community/mflux/blob/main/LICENSE) používá licenci MIT. Knihovny a model mají vlastní licenční podmínky; jejich úplné znění a další oznámení jsou součástí distribuce a shrnuje je [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md). HEIC používá systémové kodeky macOS. Licence modelu automaticky neurčuje licenci celé aplikace.
