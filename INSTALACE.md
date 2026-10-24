# Instalace, přenos a odinstalace

## Požadavky

- Apple Silicon M5, alespoň 16 GB sjednocené paměti.
- macOS 26 nebo novější; běžná uživatelská oprávnění a možnost spouštět vlastní aplikace.
- Přibližně 8 GiB volného místa. Váhy zabírají asi 4,6 GB, knihovny a Python další prostor.
- Internet při prvním stažení vah; při instalaci ze zdrojového ZIPu také pro Python a knihovny. Soukromý repozitář vyžaduje při stahování vydání GitHub přihlášení s přístupem k repozitáři. Samotná aplikace přihlášení nepotřebuje.

## Doporučený postup

Stáhněte z GitHub Releases soubor `LokalniKolor-1.1.0-macOS-arm64.zip`, rozbalte jej a celou složku uložte na stálé zapisovatelné místo. Dvojklikem otevřete `Instalovat.command`. Skript ověří architekturu, systém a kontrolní součty, rozbalí vlastní Python, vytvoří izolované prostředí, nainstaluje přibalené knihovny a ověří výpočet na Metal GPU. Nakonec stáhne a ověří veřejné modelové váhy a otevře aplikaci.

Terminál se používá pouze k zobrazení průběhu instalace; žádné příkazy se ručně nezadávají. Výpočty později spouštějte dvojklikem na `Lokální Kolor.app`. Model se zbytečně znovu nestahuje. Přerušené stahování velkých vah pokračuje z dočasného souboru při opětovném spuštění instalace.

Pokud macOS oznámí, že aplikaci nebo skript nemůže otevřít kvůli neověřenému vývojáři, použijte standardní postup macOS pro povolení konkrétní stažené aplikace v **Nastavení systému → Soukromí a zabezpečení → Přesto otevřít**. Volba se může zobrazit až po prvním pokusu o otevření. Ve spravovaném firemním Macu může být potřeba souhlas správce s použitím vlastní aplikace. Instalátor neobchází Gatekeeper a nevypíná systémové ochrany.

## Co obsahuje složka

- `.python/`: vlastní CPython 3.12, oficiální sestava python-build-standalone pro Apple Silicon.
- `.venv/`: lokální knihovny, včetně MFLUX a MLX; systémový Python se nemění.
- `wheelhouse/`: instalační balíčky přibalené do vydání. Ve zdrojovém repozitáři nejsou.
- `modely/flux2-klein-4b-4bit/`: kompletní lokální váhy. Soubory LFS se ověřují SHA-256.
- `runtime/`: pracovní návrhy, cache a logy; `vysledky/`: výchozí výsledky. Tyto složky zůstávají pouze na vašem Macu.

Výpočet používá nativní Qwen3-4B textový enkodér, uložený embedding promptu a úsporný strip VAE dekodér. PyTorch není nainstalován; MFLUX se instaluje z přiloženého, hashovaného wheelu bez jeho volitelně nepotřebných automatických závislostí. `pip check` může kvůli metadatům MFLUX hlásit chybějící torch. Skutečná inference probíhá v MLX a je ověřena samostatně.

## Přenos již nainstalované aplikace bez internetu

Ukončete aplikaci a přeneste **celou složku včetně skrytých `.python` a `.venv` a složky `modely`**, nejlépe pomocí archivu vytvořeného Finderem. Potom aplikaci otevřete v nové poloze. Spouštěč opravuje cesty prostředí automaticky. Pokud je potřeba znovu připravit prostředí z přibalených knihoven, `Instalovat.command --offline` provede kontrolu bez stahování; tento volitelný argument se zadává v Terminálu.

Neodstraňujte soubory `.dist-info` z `.venv`; obsahují informace o instalovaných knihovnách. Aplikace umí chybějící diagnostická metadata MFLUX bezpečně nahradit údaji z připnutého manifestu, ale správně dokončená instalace je vždy obnoví.

## Diagnostika a odinstalace

`Diagnostika.command` ověří knihovny, model a malý skutečný výpočet na Metal GPU bez generování fotografie. Chyby aplikace jsou v `runtime/aplikace.log` a `runtime/worker.log`.

Pro odinstalaci aplikaci ukončete, uchovejte vlastní výsledky a celou složku přesuňte do Koše. Neinstaluje se systémová služba ani automatické spouštění. Výsledky uložené v jiných složkách zůstanou zachované.
