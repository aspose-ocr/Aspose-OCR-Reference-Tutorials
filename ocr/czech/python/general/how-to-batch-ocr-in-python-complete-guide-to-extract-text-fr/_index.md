---
category: general
date: 2026-06-28
description: Jak provádět hromadné OCR v Pythonu — extrahovat text z obrázků a převádět
  naskenované stránky na text pomocí hromadného zpracování OCR.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: cs
og_description: Naučte se provádět hromadné OCR v Pythonu, extrahovat text z obrázků
  a převádět naskenované stránky na text pomocí efektivního hromadného zpracování
  OCR.
og_title: Jak provádět dávkové OCR v Pythonu – krok za krokem průvodce
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Jak provádět hromadné OCR v Pythonu – Kompletní průvodce extrakcí textu z obrázků
url: /cs/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provádět hromadné OCR v Pythonu – Kompletní průvodce extrakcí textu z obrázků

Pokud se ptáte **jak provádět hromadné OCR v Pythonu**, jste na správném místě. Tento tutoriál vám ukáže rychlý způsob, jak **extrahovat text z obrázků** a **převést naskenované stránky na text** pomocí jediné instance OCR enginu. Už žádné kopírování‑vkládání souboru po souboru – nechte kód udělat těžkou práci.

Provedeme vás vším, co potřebujete: instalace knihovny, načtení celé složky se skeny, spuštění hromadného OCR zpracování a elegantní zpracování výsledků. Na konci budete mít znovupoužitelný skript, který během několika sekund změní hromadu PNG nebo JPEG souborů na prohledávatelné textové soubory.

## Co budete potřebovat

Než se pustíme dál, ujistěte se, že máte:

* Python 3.9+ nainstalovaný (kód funguje i na 3.8, ale 3.9+ poskytuje nejnovější funkce typování).
* Moderní OCR knihovnu – zde používáme **Aspose.OCR for Python via .NET**, která poskytuje třídu `OcrEngine` ukázanou v původním úryvku.  
  ```bash
  pip install aspose-ocr
  ```
* Složku s naskenovanými stránkami (`page1.png`, `page2.png`, …). Všechno, co umí otevřít Pillow, bude fungovat, takže PDF, TIFF nebo BMP jsou také v pořádku.
* Trochu zvědavosti – pokud jste ještě nikdy neautomatizovali převod obrázku na text, brzy uvidíte, proč je hromadné OCR průlomové.

> **Pro tip:** Pokud dáváte přednost čistě Python knihovně, zaměňte `OcrEngine` za `pytesseract.image_to_string`. Ostatní logika zůstane stejná.

## Jak provádět hromadné OCR v Pythonu – krok za krokem

Níže je kompletní, spustitelný skript. Každý řádek je okomentován, abyste viděli *proč* je daný kus důležitý, ne jen *co* dělá.

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### Očekávaný výstup

Spuštění skriptu proti složce se třemi PNG skeny vytvoří něco jako:

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

Náhled ukazuje prvních 200 znaků každé stránky a celý text je uložen ve složce `ocr_output`.

## Extrahovat text z obrázků pomocí jediné instance enginu

Proč vytváříme **jednu** `OcrEngine` a znovu ji používáme? Vytvoření instance může být nákladné, protože načítá jazykové balíčky a nativní DLL. Sdílením stejné instance napříč dávkou získáte:

* **Úsporu paměti** – v RAM existuje jen jedna sada zdrojů.
* **Zrychlení** – engine zůstává „nahřátý“, čímž se vyhnete opakovanému inicializování.
* **Konzistenci** – stejné nastavení rozpoznávání platí pro každou stránku, což je zásadní, když chcete **extrahovat text z obrázků** se stejným rozložením.

Pokud potřebujete upravit rozpoznávání (např. zapnout kontrolu pravopisu nebo změnit jazyk), udělejte to *před* voláním `recognize_batch`. Všechny následující stránky tyto nastavení automaticky zdědí.

## Efektivně převést naskenované stránky na text

Jádro problému – **převést naskenované stránky na text** – je řešeno pomocí `engine.recognize_batch(images)`. Pod pokličkou knihovna zpracovává každý obrázek v poolu background threadů, takže na vícejádrových strojích dosáhnete téměř lineárního škálování. Několik věcí, na které je dobré myslet:

* **Kvalita obrázku má význam** – 300 dpi nebo vyšší dává nejlepší výsledky. Pokud jsou vaše skeny nízkého rozlišení, zvažte up‑sampling pomocí Pillow před předáním enginu.
* **Barva vs. odstíny šedi** – OCR enginy obvykle pracují rychleji na 8‑bitové šedé. Můžete přidat krok předzpracování:  
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **Podpora jazyků** – Aspose.OCR podporuje více než 40 jazyků. Nastavte `engine.language = "eng"` nebo `"fra"` před hromadným voláním, pokud nepracujete s angličtinou.

## Nejlepší postupy pro hromadné OCR zpracování

I když je výše uvedený kód již stručný, produkční hromadné OCR často vyžaduje několik dalších opatření:

| Problém | Doporučený přístup |
|---------|--------------------|
| **Velké dávky ( > 500 souborů )** | Rozdělit na bloky po 100–200 obrázcích, aby byl paměťový otisk přijatelný. |
| **Poškozené nebo nepodporované soubory** | Pomocná funkce `load_images` již zachytává výjimky a zapisuje varování; můžete také přidat fallback, který špatné soubory přeskočí nebo přesune. |
| **Sledování průběhu** | Zabalit `recognize_batch` do smyčky, která po každém obrázku vrátí výsledek, pokud knihovna poskytuje per‑image callbacky. |
| **Post‑zpracování** | Spustit kontrolu pravopisu nebo regex čištění na výsledných řetězcích pro zlepšení vyhledatelnosti. |
| **Paralelizace** | Pokud máte multi‑node prostředí, rozdělte složky mezi pracovníky a na konci sloučte výstupy `.txt`. |

Tyto tipy vám pomohou škálovat **hromadné OCR zpracování** od několika stránek až po tisíce, aniž by skript spadl.

## Často kladené otázky

**Q: Můžu to použít přímo s PDF?**  
A: Rozhodně. Nejprve převěďte každou PDF stránku na obrázek (např. pomocí `pdf2image`) a výsledný seznam předáte `recognize_batch`. Zbytek pipeline zůstane beze změny.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční kódové příklady s podrobným vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vlastních projektech.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}