# Lokální Kolor pro macOS M5

Lokální kolorování černobílých fotografií pomocí FLUX.2 Klein 4B, MFLUX a Apple MLX/Metal. Finální obraz přebírá z AI pouze barvy; jasová struktura a rozlišení pocházejí z originálu.

## Instalace na druhý Mac

Požadavky: **Apple Silicon M5, alespoň 16 GB RAM, macOS 26 nebo novější a přibližně 8 GiB volného místa**. První stažení modelu vyžaduje internet. Potom zpracování funguje offline.

1. Otevřete [poslední vydání](https://github.com/nabiknab-eng/lokalni-kolor-macos/releases/latest) a stáhněte **LokalniKolor-1.1.0-macOS-arm64.zip**.
2. ZIP rozbalte. Celou složku `LokalniKolor` přesuňte do stálého místa, například do své složky Aplikace. Samotnou `.app` od ostatních souborů neoddělujte.
3. Dvojklikem spusťte **Instalovat.command**. V Terminálu se automaticky připraví prostředí a stáhnou i ověří váhy modelu (asi 4,6 GB). Žádné příkazy nemusíte psát.
4. Po dokončení se aplikace otevře. Další spuštění: dvojklik na **Lokální Kolor.app**.

Balíček vydání obsahuje vlastní Python a instalační knihovny. Nepotřebuje Homebrew, Xcode, globální balíčky, administrátorské oprávnění ani přihlášení k inferenční službě. Menší archiv `LokalniKolor-1.1.0-source.zip` obsahuje zdrojový kód a stejný instalátor; při jeho použití se navíc stáhne Python a knihovny.

Aplikace není notarizovaná certifikátem Apple. macOS může po stažení požadovat ruční schválení otevření; postup je v [instalačním návodu](INSTALACE.md). Instalátor automaticky neodstraňuje ochranu stažených souborů.

## Použití

Otevřete nebo přetáhněte JPEG, PNG či TIFF, upravte prompt a klikněte na **Vytvořit 3 varianty**. Vyberte variantu, sytost a porovnejte výsledek s originálem. Pro přesné zachování jasu ukládejte **16bitový PNG nebo TIFF**. JPEG je ztrátový. Výstup se jmenuje `puvodni_nazev_kolor`; existující soubory se nepřepisují.

**Barvy jsou odhad.** Doložené barvy oblečení či předmětů doplňte do promptu a zkontrolujte barevné hranice. Zachování L* není zárukou historicky správných barev.

## Dokumentace a zdroje

- [Návod k aplikaci](NAVOD.md), [instalace a odinstalace](INSTALACE.md), [stručné shrnutí](SHRNUTI.md), [technické podrobnosti](NASTAVENI.md).
- Původní model: [Black Forest Labs FLUX.2 Klein 4B](https://huggingface.co/black-forest-labs/FLUX.2-klein-4B); [použitá 4bitová MLX kvantizace](https://huggingface.co/mlx-community/flux2-klein-4b-4bit), revize `860e87183ceb29e39627c0612ebd66d8ea66e68c`.
- MFLUX 0.23.0, commit `a3b21fcaa88726b2267bd42bfc2e2d722f7d5a47`; MLX 0.32.4. Přesné závislosti jsou v `requirements.lock`, licence ve [THIRD-PARTY.md](THIRD-PARTY.md).
- Úplný zdrojový kód, testy a instalační skripty jsou v archivu `LokalniKolor-1.1.0-source.zip` přiloženém k vydání. Uživatelské fotografie, výsledky, logy, cache a váhy se na GitHub nenahrávají.

## Vývoj

Po instalaci lze v této složce volitelně spustit:

```sh
.venv/bin/python -m pytest -q
.venv/bin/python scripts/check_installation.py
.venv/bin/python -m kolor.cli vstup.jpg --output vysledky
```

Distribuční ZIP sestaví `scripts/build_release.py`; stažené binární knihovny jsou určeny pro macOS arm64. Výpočty modelu na jiných platformách se nepoužívají.
