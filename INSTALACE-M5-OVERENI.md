# Ověření instalace Lokální Kolor 1.1.0

Ověřeno 24. října 2026 na MacBooku Air s Apple M5, 16 GB RAM a macOS 27.0.1.

## Čisté prostředí

Distribuční ZIP byl rozbalen do nové složky s mezerami v cestě. Instalátor připravil vlastní CPython 3.12.15 a nové virtuální prostředí z přibalených knihoven. Během testu byla síť zakázána pravidlem macOS sandboxu. Nepoužíval se Python ani knihovny původní aplikace.

- Instalace Pythonu a všech knihoven z lokálního balíčku: úspěch.
- MLX 0.32.4, MFLUX 0.23.0 a skutečný výpočet na Metal GPU: úspěch.
- Všech 28 automatických testů: úspěch (14,85 s).
- Kompletní model byl pro offline test zkopírován z již stažených vah; instalátor ověřil všechny soubory a jejich kontrolní součty. Nové stažení 4,6 GB v tomto testu nebylo opakováno.
- První skutečné kolorování veřejného testovacího snímku skimage.data.camera, 512 × 512, seed 42: úspěch bez internetu. Generování 33,60 s, přenos barev 0,49 s, špička alokací MLX 5,56 GB. Výstup 16bitový PNG v rozlišení originálu.
- Výpočetní maximální odchylka L* při přenosu barev: 0,0000029; údaj se týká pracovního obrazu před kvantizací při uložení.
- Obsah distribučních ZIPů, integrita ZIP a SHA-256: ověřeno. Bez uživatelských fotografií, výstupů, logů, cache, lokálních cest a modelových vah.

## Rozsah ověření

Jde o čistou instalaci v samostatné složce na současném M5. Instalace na druhém fyzickém Macu ani první povolení stažené aplikace v Gatekeeperu zde ověřeny nebyly. Aplikace není podepsaná ani notarizovaná certifikátem Apple.

Požadavky balíčku: Apple Silicon M5, macOS 26+, 16 GB RAM a přibližně 8 GiB volného místa. První stažení modelu vyžaduje internet, následné kolorování je lokální. Barvy zůstávají odhadem AI.
