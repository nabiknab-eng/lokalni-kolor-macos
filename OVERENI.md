# Ověření veřejné sestavy bicolor 1.9.1

Ověřeno 31. října 2026.

- Instalační ZIP byl rozbalen do nové složky s mezerami v názvu. Python se připravil automaticky z přibaleného archivu.
- Všech 63 připnutých knihoven se skutečně stáhlo přímo z oficiálního PyPI a prošlo kontrolou SHA-256.
- Metal GPU a nativní HEIC s Adobe RGB byly ověřeny na Macu Apple M5.
- Celá instalace byla následně přejmenována a znovu prošla kontrolou spouštěče, HEIC a Metal.
- Čtrnáct nativních kodekových testů ověřilo orientaci, hlavní snímek, průhlednost, 10bitový SDR vstup, sRGB/Adobe RGB a ochranu originálů.
- Model se během této čisté instalační kontroly nestahoval znovu. Všech 13 dříve stažených souborů připnuté revize, celkem 4 619 702 304 bajtů, prošlo kontrolou SHA-256.
- Tato distribuční kontrola neopakovala AI inferenci. MFLUX a kolorizační model zůstávají stejné jako ve funkční lokální aplikaci.
- Instalační i zdrojový ZIP prošly kontrolou CRC, kontrolních součtů a seznamu přibalených souborů. Neobsahují osobní fotografie, výsledky, předvolby, tokeny ani modelové váhy.

Minimální podporovaná konfigurace je Apple Silicon M1 nebo novější, 16 GB RAM a macOS 26 nebo novější. Jiný fyzický Mac M1 nebyl při této distribuční kontrole k dispozici. Pro první výpočet na 16GB Macu doporučujeme barevný vzor 512 px a jednu variantu.

MFLUX ve svých obecných metadatech uvádí také Torch. Tato MLX sestava jej neinstaluje; používá Metal a pouze tokenizér Transformers s USE_TORCH=0. Běžný pip check proto může uvést tuto známou obecnou závislost, přestože kontrola skutečně používaných modulů a Metal prošla.

Úplný programový kód a spouštěcí soubory jsou v bicolor-1.9.1-source.zip. Automatické archivy Source code na stránce GitHub Releases nejsou instalační balíček.
