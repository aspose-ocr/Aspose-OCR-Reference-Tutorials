---
category: general
date: 2026-04-29
description: Extrahujte text z PDF pomocí Aspose OCR v Pythonu. Naučte se hromadné
  zpracování PDF pomocí OCR, převádějte text ze skenovaných PDF a řešte stránky s
  nízkou úrovní spolehlivosti.
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: cs
og_description: Extrahujte text z PDF pomocí Aspose OCR v Pythonu. Tento průvodce
  ukazuje hromadné zpracování OCR PDF, převod naskenovaného textu v PDF a práci s
  výsledky s nízkou důvěryhodností.
og_title: Extrahovat text z PDF – OCR PDF pomocí Pythonu
tags:
- OCR
- Python
- PDF processing
title: Extrahovat text z PDF – OCR PDF pomocí Pythonu
url: /cs/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z PDF – OCR PDF s Pythonem

Už jste někdy potřebovali **extrahovat text z PDF**, ale soubor je jen naskenovaný obrázek? Nejste v tom sami — mnoho vývojářů narazí na tuto překážku, když se snaží převést PDF na prohledávatelná data. Dobrá zpráva? S Aspose OCR pro Python můžete převést text naskenovaného PDF během několika řádků a dokonce spustit **batch OCR PDF processing**, když máte desítky souborů ke zpracování.

V tomto tutoriálu projdeme celým pracovním postupem: nastavení knihovny, spuštění OCR na jednom PDF, škálování na dávku a řešení stránek s nízkou důvěrou, abyste věděli, kdy je potřeba ruční revize. Na konci budete mít připravený skript, který extrahuje text z libovolného naskenovaného PDF, a pochopíte, proč se každý krok provádí.

## Co budete potřebovat

Než se ponoříme dál, ujistěte se, že máte:

- Python 3.8 nebo novější (kód používá f‑stringy, takže 3.6+ funguje, ale doporučujeme 3.8+).
- Licence Aspose OCR pro Python nebo klíč pro bezplatnou zkušební verzi (můžete jej získat na webu Aspose).
- Složka s jedním nebo více naskenovanými PDF, které chcete zpracovat.
- Mírné množství místa na disku pro vygenerované *.txt* zprávy.

A to je vše — žádné těžké externí závislosti, žádné gymnastiky s OpenCV. Engine Aspose OCR udělá těžkou práci za vás.

## Nastavení prostředí

Nejprve nainstalujte balíček Aspose OCR z PyPI:

```bash
pip install aspose-ocr
```

Pokud máte soubor licence (`Aspose.OCR.lic`), umístěte jej do kořenového adresáře projektu a aktivujte jej takto:

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **Tip:** Uchovávejte soubor licence mimo verzovací systém; přidejte jej do `.gitignore`, abyste předešli neúmyslnému zveřejnění.

## Provádění OCR na jednom PDF

Nyní extrahujme text z jednoho naskenovaného PDF. Hlavní kroky jsou:

1. Vytvořte instanci `OcrEngine`.
2. Nasmerujte ji na PDF soubor.
3. Získejte `OcrResult` pro každou stránku.
4. Zapište výstup plain‑textu na disk.
5. Uvolněte engine, aby se uvolnily nativní zdroje.

Zde je kompletní spustitelný skript:

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**Co uvidíte:** Pro každou stránku skript vypíše něco jako `Page 1: confidence 97.45%`. Pokud stránka spadne pod práh 80 %, objeví se varování, které vás upozorní, že OCR mohlo některé znaky vynechat.

### Proč to funguje

- **`OcrEngine`** je vstupní brána do nativní knihovny Aspose OCR; zajišťuje vše od předzpracování obrazu po rozpoznávání znaků.
- **`extract_from_pdf`** automaticky rasterizuje každou stránku PDF, takže nemusíte PDF převádět na obrázky sami.
- **Confidence scores** vám umožňují automatizovat kontrolu kvality — kritické při zpracování právních nebo zdravotnických dokumentů, kde je přesnost důležitá.

## Dávkové zpracování OCR PDF s Pythonem

Většina reálných projektů zahrnuje více než jeden soubor. Rozšíříme skript pro jeden soubor na **batch OCR PDF processing** pipeline, která prochází adresář, zpracuje každé PDF a uloží výsledky do odpovídající podadresáře.

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### Jak to pomáhá

- **Scalability:** Funkce projde složku jednou a vytvoří dedikovaný výstupní podadresář pro každé PDF. To udržuje pořádek, když máte desítky dokumentů.
- **Reusability:** `ocr_pdf_file` může být volána z jiných skriptů (např. webové služby), protože je čistou funkcí.
- **Error handling:** Skript vypíše přátelskou zprávu, pokud je vstupní složka prázdná, čímž vás ochrání před tichým selháním.

## Převod textu z naskenovaného PDF – Řešení okrajových případů

I když výše uvedený kód funguje pro většinu PDF, můžete narazit na několik zvláštností:

| Situace | Proč k tomu dochází | Jak to zmírnit |
|-----------|----------------|-----------------|
| **Šifrovaná PDF** | PDF je chráněno heslem. | Předejte heslo do `extract_from_pdf(pdf_path, password="yourPwd")`. |
| **Vícejazyčné dokumenty** | Aspose OCR má výchozí jazyk angličtinu. | Nastavte `ocr_engine.language = "spa"` pro španělštinu, nebo poskytněte seznam pro smíšené jazyky. |
| **Velmi velká PDF (>500 stránek)** | Spotřeba paměti stoupá, protože každá stránka je načtena do RAM. | Zpracovávejte PDF po částech pomocí `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` a cyklu. |
| **Špatná kvalita skenu** | Nízké DPI nebo silný šum snižuje důvěru. | Předzpracujte PDF pomocí `engine.image_preprocessing = True` nebo zvyšte DPI pomocí `engine.dpi = 300`. |

> **Pozor:** Zapnutí předzpracování obrazu může výrazně zvýšit čas CPU. Pokud spouštíte noční dávku, naplánujte dostatek času nebo spusťte samostatného pracovníka.

## Ověření výstupu

Po dokončení skriptu najdete strukturu složek podobnou:

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

Otevřete libovolný soubor `.txt`; měli byste vidět čistý text kódovaný v UTF‑8, který odráží původní naskenovaný obsah. Pokud zaznamenáte poškozené znaky, zkontrolujte nastavení jazyka PDF a ujistěte se, že jsou na stroji nainstalovány správné balíčky fontů.

## Vyčištění zdrojů

Aspose OCR se spoléhá na nativní DLL, takže je nezbytné po dokončení zavolat `engine.dispose()`. Zapomenutí tohoto kroku může vést k únikům paměti, zejména u dlouho běžících dávkových úloh.

```python
# Always the last line of your script
engine.dispose()
```

## Kompletní end‑to‑end příklad

Spojením všeho dohromady, zde je jeden

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}