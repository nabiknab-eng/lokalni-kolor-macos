# Instalace bicolor 1.9.1

[Popis programu](README.md) · [Ovládání a práce s fotografiemi](NAVOD.md)

## Před instalací

Tato sestava vyžaduje **Mac s Apple Silicon M1 nebo novějším, macOS 26 nebo novější a alespoň 16 GB RAM**. Pro instalaci doporučujeme alespoň **12 GiB volného místa**, navíc prostor na vlastní fotografie a výsledky. První instalace potřebuje internet ke stažení přibližně **314 MB knihoven z PyPI** a **4,62 GB modelových souborů z Hugging Face**.

Samostatná instalace Pythonu, Homebrew ani vývojářských nástrojů není potřeba. Balíček obsahuje vlastní běhové prostředí Pythonu. Instalátor automaticky stáhne přesně připnuté knihovny z oficiálního PyPI a ověří jejich SHA-256; vše připraví uvnitř složky programu. Nepotřebuje přístupový token Hugging Face ani účet pro cloudové AI API.

## Postup

1. Na GitHubu otevři **[Releases](https://github.com/nabiknab-eng/lokalni-kolor-macos/releases/latest)** a v části **Assets** stáhni **`bicolor-1.9.1-macOS-arm64.zip`**. Ve stejném vydání je kontrolní součet SHA-256.
2. ZIP rozbal ve Finderu. Vzniklou složku **bicolor-1.9.1** přesuň na trvalé místo, kde máš právo zapisovat, například do své složky Aplikace.
3. Uvnitř této složky spusť **Instalovat.command**. Otevře se okno Terminálu s průběhem instalace.
4. Nech instalátor dokončit ověření balíčku, přípravu prostředí, kontrolu Metal GPU a stažení modelu. Složku během instalace nepřejmenovávej ani nepřesouvej.
5. Po hlášení o dokončení spouštěj **bicolor.app** dvojklikem. Instalační příkaz není potřeba pouštět při každém použití.

**Automatické Source code (zip/tar.gz) ani Code → Download ZIP nejsou instalátor.** Vyber výslovně výše uvedený soubor `bicolor-1.9.1-macOS-arm64.zip` v Assets.

**Ponech celou instalační složku pohromadě.** Soubor bicolor.app potřebuje sousední programové soubory, prostředí, knihovny a model. Při pozdějším přesouvání nejprve aplikaci zavři a přesuň celou složku.

## Pokud spuštění zablokuje macOS

Tato distribuce nemá podpis Apple Developer ID ani notarizaci Apple. macOS proto může při prvním otevření instalátoru nebo aplikace zobrazit upozornění na neověřeného vývojáře.

Po pokusu o spuštění otevři **Nastavení systému → Soukromí a zabezpečení**. Pokud této konkrétní stažené kopii důvěřuješ a ověřil jsi její původ, použij pro ni **Přesto otevřít** a potvrď následující systémový dialog. Postup popisuje [oficiální návod Apple](https://support.apple.com/102445).

Pokud systém hlásí poškozený nebo neúplný soubor, stáhni balíček znovu a porovnej jeho kontrolní součet. U spravovaného pracovního Macu mohou spuštění omezovat pravidla správce.

## Co se instaluje a stahuje

| Součást | Zdroj a umístění |
| --- | --- |
| Aplikace a běhové prostředí Pythonu | Přibalené v instalačním ZIPu; instalují se do jeho složky |
| Knihovny včetně Qt/PySide6 a MLX | První instalace automaticky stáhne přesně určené balíčky z PyPI, asi 314 MB; kontroluje SHA-256 |
| Model FLUX.2 Klein 4B q4 | První instalace stáhne veřejné soubory z Hugging Face, přibližně 4,62 GB |
| Modelové váhy | `modely/flux2-klein-4b-4bit` uvnitř instalační složky |
| Předvolby a pracovní soubory | `runtime` uvnitř instalační složky |

Model je připnutý na konkrétní revizi `860e87183ceb29e39627c0612ebd66d8ea66e68c` repozitáře [mlx-community/flux2-klein-4b-4bit](https://huggingface.co/mlx-community/flux2-klein-4b-4bit/tree/860e87183ceb29e39627c0612ebd66d8ea66e68c). Instalátor ověřuje instalační balíček, všech 63 balíčků knihoven a všech 13 modelových souborů pomocí SHA-256. Úplné licenční texty přibalených součástí jsou součástí distribuce; přehled je v [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).

Po dokončení instalace se při běžném kolorování nic dalšího nestahuje. Fotografie a jejich textové zadání se zpracovávají v Macu.

## Přerušené stažení

Znovu spusť **Instalovat.command** ve stejné složce. Instalátor ověří přítomné soubory a pokračuje ve stahování chybějících nebo neúplných vah. Kvůli běžnému přerušení není potřeba mazat celou instalaci.

Na Macu s 16 GB RAM pro první fotografii použij barevný vzor **512 px** a **1 variantu**. Před náročnějším výpočtem zavři ostatní aplikace s vysokou spotřebou paměti.

## Aktualizace

1. Ulož rozpracované výsledky a bicolor zavři.
2. Nové vydání rozbal do samostatné složky a proveď jeho instalaci.
3. Původní složku ponech, dokud novou verzi neověříš.

Nemíchej ručně knihovny a programové soubory různých vydání. Instalační složka obsahuje také lokální předvolby; nová samostatná složka začíná vlastními předvolbami.

## Odinstalace

Zavři bicolor. Vlastní fotografie a výsledky, které chceš zachovat, přesuň mimo instalační složku. Potom celou složku programu přesuň do Koše. Obsahuje také stažený model, prostředí, předvolby a pracovní soubory. Fotografie uložené v jiných adresářích tím nejsou dotčené.
