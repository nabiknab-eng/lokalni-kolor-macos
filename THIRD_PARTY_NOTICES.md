# Součásti třetích stran a licence

Tento přehled popisuje veřejný instalátor bicolor 1.9.1. Licence jednotlivých součástí platí samostatně; tento text nepřelicencovává vlastní zdrojový kód bicolor ani neomezuje práva udělená licencemi knihoven.

## Co obsahuje stažený ZIP

- Zdrojové soubory bicolor, nativní spouštěč a malý nativní pomocný program pro HEIC, ikona a české návody.
- Připnutý samostatný runtime CPython od projektu python-build-standalone. CPython používá licenci Python Software Foundation a související historické licence. Původní licenční soubory zůstávají součástí runtime archivu a rozbaleného prostředí `.python/`. Přesný původ a kontrolní součet uvádí `scripts/python-runtime.json`.
- Připnutý balíček MFLUX, licence MIT, Copyright (c) 2026 Filip Strand. Úplný text je ve `vendor/MFLUX-LICENSE.txt`, revize a původ ve `vendor/MFLUX-REVISION.json`.
- Informativní kopie licenčních oznámení závislostí ve složce `licenses/`.

Veřejný ZIP **neobsahuje binární balíčky Qt/PySide6 ani ostatní PyPI wheels**. Instalátor je stáhne přímo z oficiálního registru PyPI podle připnutých verzí a SHA-256. Modelové váhy se rovněž nestahují z tohoto repozitáře, ale přímo z připnuté revize Hugging Face. Uživatel nemusí ručně instalovat Python ani hledat jednotlivé balíčky.

## AI model a výpočet

- **FLUX.2 Klein 4B** od Black Forest Labs: Apache License 2.0. Používá se pouze tento původní model a jeho 4bitová MLX kvantizace. [Původní model a licence](https://huggingface.co/black-forest-labs/FLUX.2-klein-4B), [použitá MLX kvantizace](https://huggingface.co/mlx-community/flux2-klein-4b-4bit). Přesná revize a očekávané kontrolní součty jsou v `scripts/model-manifest.json`. Úplný text licence je v `modely/LICENSE-Apache-2.0.txt`.
- **MFLUX**: MIT, viz výše a [zdrojový projekt](https://github.com/mflux-community/mflux).
- **Apple MLX** a související MLX Metal balíček: MIT; [zdrojový projekt](https://github.com/ml-explore/mlx). Binární balíčky instaluje PyPI, původní oznámení zůstávají v nainstalovaných balíčcích.

Vydání neobsahuje FLUX 3, Qwen-Image-Edit, další kolorizační model ani filmové emulace.

## Rozhraní Qt for Python

Rozhraní používá dynamicky načítané knihovny **PySide6 Essentials / Shiboken6 / Qt for Python**. Jejich konkrétní licence a oznámení uvádí [oficiální licenční přehled Qt for Python](https://doc.qt.io/qtforpython-6/licenses.html) a licenční soubory nainstalovaných balíčků. Používané základní moduly mají mimo jiné licenci GNU LGPL verze 3; další alternativní podmínky příslušných součástí tím nejsou nahrazeny.

Qt a PySide6 nejsou vestavěny do binárního spouštěče bicolor. Instalátor je stáhne z PyPI a uloží jako běžné dynamické knihovny do `.venv/lib/python3.12/site-packages/`. Kompatibilní vlastní sestavu lze nainstalovat do téhož prostředí; `kolor/` a `bootstrap.py` jsou dostupné v podobě zdrojových souborů. Není zaveden zákaz ladění nebo nahrazení knihovny pro výkon práv podle LGPL. Použití názvu Qt neznamená podporu či schválení aplikace společností Qt.

## HEIC / HEIF

Veřejné vydání používá **systémové ImageIO a CoreGraphics v macOS**. Pomocný program `vendor/macos-heif-arm64` je sestaven ze zveřejněného souboru `scripts/macos_heif.m` a dynamicky používá pouze systémové frameworky a knihovny macOS. Zpracovává hlavní snímek, orientaci a barevný profil; výstup je 8bitový SDR HEIC.

Do instalátoru se **nepřibaluje pillow-heif, libheif, libde265 ani x265** a nejsou to závislosti veřejného vydání. Toto rozlišení je důležité: zdrojový pillow-heif má BSD-3-Clause, ale jeho běžné binární wheels zahrnují x265 a jsou podle vlastního licenčního oznámení GPLv2. Veřejné vydání tyto binární knihovny nenabízí. [Licenční oznámení pillow-heif upstream](https://github.com/bigcat88/pillow_heif/blob/master/LICENSES_bundled.txt).

Systémové frameworky a kodeky macOS se nekopírují do ZIPu. Jejich používání se řídí podmínkami systému macOS; aplikace neposkytuje samostatnou licenci k technologiím Apple nebo k případným patentům.

## Fotografie, profily a ostatní knihovny

- **Pillow**: HPND / historická PIL licence, včetně dalších příslušných oznámení. [Projekt](https://python-pillow.github.io/).
- **LittleCMS**: MIT, dynamická součást balíčku Pillow; používá se pro ICC převody. [Projekt](https://github.com/mm2/Little-CMS).
- **NumPy**: BSD-3-Clause a licence přibalených numerických knihoven; **SciPy**: BSD-3-Clause a licence přibalených součástí; **scikit-image**: BSD-3-Clause. Původní licence a oznámení jsou součástí jejich oficiálních balíčků.
- **OpenCV / opencv-python**: Apache License 2.0 pro současný OpenCV a další licence volitelných či přibalených knihoven konkrétního wheelu. [Licenční přehled OpenCV](https://opencv.org/license/). Přehled se nesmí vykládat jako přelicencování celého wheelu jedinou licencí.
- **tifffile**: BSD-3-Clause; **psutil**: BSD-3-Clause.
- **Hugging Face Hub, Transformers, Tokenizers, Safetensors, SentencePiece** a ostatní připnuté pomocné balíčky: licence a oznámení příslušného konkrétního projektu. Přesné verze všech instalovaných závislostí jsou v `requirements.lock` a hashovém instalačním manifestu. Informativní soupis kopií licencí je v `licenses/DEPENDENCIES.json`; rozhodující úplné texty zůstávají i v oficiálních stažených balíčcích.

Profil sRGB se připravuje pomocí LittleCMS. **Adobe RGB (1998)** ICC profil se čte ze systémového ColorSync v macOS; aplikace vlastní kopii tohoto profilu nedistribuuje. Názvy Adobe RGB, HEIC, Qt a dalších technologií patří jejich příslušným vlastníkům.

Distribuce neobsahuje uživatelské fotografie, barevné výsledky, osobní nastavení, pracovní náhledy ani lokální diagnostické záznamy. Případné malé soubory v `tests/data/` zobrazují pouze uměle vytvořené barevné testovací plochy.
