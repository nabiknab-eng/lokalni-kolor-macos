# Zdroje a licence

- Model Black Forest Labs [FLUX.2-klein-4B](https://huggingface.co/black-forest-labs/FLUX.2-klein-4B), Apache 2.0. [Použitá komunitní kvantizace MLX](https://huggingface.co/mlx-community/flux2-klein-4b-4bit), konkrétní revize v `modely/flux2-klein-4b-4bit/REVISION.json`.
- [MFLUX](https://github.com/mflux-community/mflux), MIT; přesná revize a hash lokálního balíčku ve `vendor/MFLUX-REVISION.json`, licence ve stejné složce.
- [Apple MLX](https://github.com/ml-explore/mlx), MIT. Výpočet modelu používá pouze MLX/Metal.
- [PySide6 / Qt for Python](https://doc.qt.io/qtforpython-6/licenses.html), LGPLv3/GPLv3 a komerční licence. Zde jsou použity dynamické knihovny balíčku PySide6-Essentials. Licence a oznámení dodavatelů jsou součástí nainstalovaného balíčku `.venv/lib/python3.12/site-packages/PySide6` a jeho `.dist-info`. Tyto knihovny lze nahradit kompatibilní vlastní sestavou. Vlastní aplikační zdrojový kód je přiložen ve složce `kolor/`.
- [CPython](https://www.python.org/), PSF licence; licenční texty jsou součástí oficiálního runtime archivu v `vendor/python-runtime.tar.gz` a jeho rozbalené složky `.python/`.
- NumPy, OpenCV, Pillow, SciPy, scikit-image, psutil, tifffile, Hugging Face Hub, Transformers (pouze tokenizér) a další závislosti: verze jsou v `requirements.lock`; jejich původní licenční soubory zůstávají v `.venv/lib/python3.12/site-packages/`.
- Automatické testy používají veřejná demonstrační data scikit-image: snímek camera (CC0, Lav Varshney) a astronaut (NASA, public domain). Fotografie uživatele nejsou součástí distribuce.

Použitá technická dokumentace: [MFLUX FLUX.2](https://github.com/mflux-community/mflux/blob/a3b21fcaa88726b2267bd42bfc2e2d722f7d5a47/src/mflux/models/flux2/README.md), [konkrétní API editace](https://github.com/mflux-community/mflux/blob/a3b21fcaa88726b2267bd42bfc2e2d722f7d5a47/src/mflux/models/flux2/variants/edit/flux2_klein_edit.py). API bylo ověřeno i importem a introspekcí lokální instalace.
