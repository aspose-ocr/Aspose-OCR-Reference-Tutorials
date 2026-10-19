---
category: general
date: 2026-06-06
description: Jak provést OCR PDF a vytvořit prohledávatelné PDF soubory z obrázků
  pomocí Pythonu. Naučte se přidat prohledávatelný text a převést obrázek na PDF/A
  během několika minut.
draft: false
keywords:
- how to ocr pdf
- create searchable pdf
- add searchable text
- ocr image to pdf
- convert image to pdf/a
language: cs
og_description: Jak provádět OCR PDF krok za krokem. Naučte se přidat prohledávatelný
  text a převést obrázek na PDF/A pomocí jednoduchého Python skriptu.
og_title: Jak OCR PDF – rychlý průvodce tvorbou prohledávatelných PDF
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  headline: How to OCR PDF in Python – Create Searchable PDF from Images
  type: TechArticle
- description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  name: How to OCR PDF in Python – Create Searchable PDF from Images
  steps:
  - name: Why this matters
    text: '- **Preserving graphics** means the visual layout (tables, logos, stamps)
      stays exactly as the scanner captured it. - The `result` object typically contains
      a hidden text layer that we’ll later embed into the PDF. - Using `recognize_image`
      instead of `recognize_pdf` avoids an extra conversion step, '
  - name: Why this matters
    text: '- **Searchable PDF**: The output file contains a hidden, selectable text
      layer. You can now Ctrl + F through the document. - **PDF/A compliance**: Some
      organizations (legal, finance) require PDF/A for audit trails; this step satisfies
      that rule automatically. - The method also **adds searchable text'
  - name: Expected output
    text: 'When you run the script, the console prints:'
  type: HowTo
tags:
- OCR
- PDF
- Python
- Automation
title: Jak provést OCR PDF v Pythonu – Vytvořit prohledávatelný PDF z obrázků
url: /cs/python-java/general/how-to-ocr-pdf-in-python-create-searchable-pdf-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak OCR PDF – Převést naskenované obrázky na prohledávatelné PDF

Už jste se někdy zamysleli, **jak OCR PDF** soubory, když máte jen naskenovaný obrázek faktury nebo účtenky? Nejste v tom sami. V mnoha kancelářích přicházejí papírové dokumenty jako ploché PNG nebo JPEG a další krok – učinit obsah prohledávatelným – se zdá jako černá skříňka.  

Dobrá zpráva? Pouhých několik řádků Pythonu vám umožní **vytvořit prohledávatelné PDF** soubory, **přidat prohledávatelný text**, a dokonce **převést obrázek na PDF/A** pro dlouhodobé archivování. V tomto tutoriálu projdeme každý krok, vysvětlíme, proč je důležitý, a poskytneme vám připravený skript, který můžete vložit do jakéhokoli projektu.

> **Pro tip:** Stejný přístup funguje pro vícestránkové skeny; stačí projít soubory ve smyčce a engine udělá těžkou práci.

---

## Co budete potřebovat

Než se pustíme dál, ujistěte se, že máte na svém počítači následující:

| Požadavek | Proč je důležité |
|-------------|----------------|
| Python 3.9 nebo novější | Moderní syntaxe a lepší podpora knihoven |
| `pdfium`‑based OCR engine (např. `pdfocr` nebo komerční SDK) | Zvládá jak rozpoznávání obrazu, tak generování PDF/A |
| Obrázkový soubor (PNG, JPEG, TIFF), který chcete převést na prohledávatelné PDF | Zdroj textu |
| Zápisové oprávnění do výstupní složky | Aby skript mohl uložit nové PDF |

Pokud jste ještě nenainstalovali OCR SDK, spusťte:

```bash
pip install pdfocr   # replace with your vendor's package name
```

A to je vše – žádné složité systémové závislosti, jen pip install.

---

## Jak OCR PDF – Přehled

Na vysoké úrovni proces sestává ze tří jednoduchých akcí:

1. **Recognize** text uvnitř obrázku při zachování původní grafiky.  
2. **Export** OCR výsledek spolu s původním obrázkem jako **searchable PDF/A** (archivně přátelský typ PDF).  
3. **Validate** že výsledný soubor obsahuje výběrový, prohledávatelný text vrstvený nad původním obrázkem.  

Níže uvidíte každý krok v kódu, s vysvětlením *proč* za jednotlivými příkazy.

## Krok 1: Rozpoznat text z obrázku

Nejprve požádáme OCR engine, aby přečetl pixely a vrátil objekt výsledku, který obsahuje jak surový obrázek, tak extrahovaný text. Představte si to jako engine, který „čte“ fakturu za vás.

```python
# Step 1: Recognize text from the image and keep the original graphics
result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

### Proč je to důležité

- **Preserving graphics** znamená, že vizuální rozvržení (tabulky, loga, razítka) zůstane přesně tak, jak jej zachytil skener.  
- Objekt `result` obvykle obsahuje skrytou textovou vrstvu, kterou později vložíme do PDF.  
- Použití `recognize_image` místo `recognize_pdf` eliminuje další krok konverze, což urychluje zpracování pro jednostránkové obrázky.  

#### Běžné varianty

- Pokud máte **vícestránkový TIFF**, předávejte přímo cestu k souboru; většina engineů bude každou stránku považovat za samostatný obrázek.  
- Pro PDF, které již obsahují obrázky, můžete zavolat `engine.recognize_pdf("file.pdf")` a tento krok úplně přeskočit.

## Krok 2: Exportovat OCR výsledek jako prohledávatelné PDF/A

Nyní vezmeme `result` z kroku 1 a řekneme engine, aby zapsal nový soubor. Klíčovým příznakem zde je *PDF/A* – verze PDF podle normy ISO určená pro dlouhodobé uchování.

```python
# Step 2: Export the OCR result together with the original image as a searchable PDF/A
result.save_as_pdfa("YOUR_DIRECTORY/invoice_searchable.pdf")
```

### Proč je to důležité

- **Searchable PDF**: Výstupní soubor obsahuje skrytou, výběrovou textovou vrstvu. Nyní můžete v dokumentu použít Ctrl + F.  
- **PDF/A compliance**: Některé organizace (právní, finanční) vyžadují PDF/A pro auditní stopy; tento krok automaticky splňuje toto pravidlo.  
- Metoda také **přidává prohledávatelný text** bez zploštění obrázku, takže vizuální věrnost zůstává dokonalá.  

#### Okrajový případ: Potřebujete běžné PDF místo toho?

Pokud vám PDF/A nevadí, nahraďte `save_as_pdfa` za `save_as_pdf`. Zbytek pracovního postupu zůstane stejný.

## Krok 3: Ověřit prohledávatelné PDF

Rychlá kontrola vám ušetří pozdější záhadné chyby. Otevřete vygenerovaný soubor v libovolném PDF prohlížeči, zkuste vybrat slovo a použijte funkci hledání.

```python
# Step 3: The file "invoice_searchable.pdf" now contains selectable text layered over the original invoice image
import subprocess, os

pdf_path = "YOUR_DIRECTORY/invoice_searchable.pdf"
if os.path.exists(pdf_path):
    print(f"✅ PDF created successfully: {pdf_path}")
    # Optionally open the file (works on macOS, Windows, Linux with appropriate commands)
    subprocess.run(["open", pdf_path] if os.name == "posix" else ["start", pdf_path], shell=True)
else:
    print("❌ Something went wrong – PDF not found.")
```

### Očekávaný výstup

Po spuštění skriptu konzole vypíše:

```
✅ PDF created successfully: YOUR_DIRECTORY/invoice_searchable.pdf
```

Po otevření souboru byste měli vidět původní obrázek faktury s jemnou, neviditelnou textovou vrstvou. Zvýrazněte libovolné slovo a uvidíte, že je výběrové – **to je prohledávatelný text**, který jste právě přidali.

## Přidání prohledávatelného textu do existujících PDF (Bonus)

Někdy již máte PDF, ale potřebujete do něj **přidat prohledávatelný text**. Ten samý engine může překrýt OCR výsledky na existující PDF:

```python
# Bonus: Add searchable text to an existing PDF file
existing_pdf = engine.load_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result = engine.recognize_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result.apply_to(existing_pdf).save_as_pdfa("YOUR_DIRECTORY/old_scanned_searchable.pdf")
```

Zde `apply_to` sloučí skrytou vrstvu s původními stránkami, což vám umožní **vytvořit prohledávatelné PDF** bez opětovného skenování.

## Běžné úskalí a tipy

| Úskalí | Jak se mu vyhnout |
|---------|-----------------|
| **Nízké rozlišení zdrojových obrázků** (< 150 dpi) | Zvětšete nebo požádejte o sken s vyšším rozlišením; přesnost OCR dramaticky klesá pod 150 dpi. |
| **Chybějící jazyková data** | Nainstalujte příslušné jazykové balíčky pro váš OCR engine (`pip install pdfocr[eng,spa]`). |
| **Výstupní složka není zapisovatelná** | Spusťte skript s dostatečnými oprávněními nebo vyberte jiný adresář. |
| **Selhání validace PDF/A** | Ujistěte se, že nevkládáte nepodporované fonty nebo JavaScript; většina SDK automaticky tuto situaci řeší při použití `save_as_pdfa`. |

## Kompletní skript – Jednosouborové řešení

Níže je samostatný skript, který spojuje vše dohromady. Zkopírujte a vložte jej, nahraďte zástupné cesty a budete připraveni **převést obrázek na PDF/A** během několika sekund.

```python
#!/usr/bin/env python3
"""
How to OCR PDF – Complete script to create a searchable PDF/A from an image.
Works with any OCR engine exposing `recognize_image` and `save_as_pdfa`.
"""

import os
import subprocess

# ----------------------------------------------------------------------
# CONFIGURATION – change these paths to match your environment
# ----------------------------------------------------------------------
INPUT_IMAGE = "YOUR_DIRECTORY/invoice.png"
OUTPUT_PDF  = "YOUR_DIRECTORY/invoice_searchable.pdf"

# ----------------------------------------------------------------------
# INITIALIZE THE OCR ENGINE (replace with your SDK's init call)
# ----------------------------------------------------------------------
# Example for a fictional `pdfocr` package:
# from pdfocr import Engine
# engine = Engine(api_key="YOUR_API_KEY")
# If you use a different library, adjust the import and init accordingly.
engine = Engine()  # placeholder – insert real initialization here

def main():
    # Step 1 – Recognize the image
    print(f"🔎 Recognizing text from {INPUT_IMAGE} …")
    result = engine.recognize_image(INPUT_IMAGE)

    # Step 2 – Save as searchable PDF/A
    print(f"💾 Saving searchable PDF/A to {OUTPUT_PDF} …")
    result.save_as_pdfa(OUTPUT_PDF)

    # Step 3 – Verify the file exists
    if os.path.isfile(OUTPUT_PDF):
        print("✅ Success! Searchable PDF/A created.")
        # Open the file for a quick visual check (optional)
        try:
            if os.name == "posix":
                subprocess.run(["open", OUTPUT_PDF])
            else:
                subprocess.run(["start", OUTPUT_PDF], shell=True)
        except Exception:
            pass
    else:
        print("❌ Error: PDF not created.")

if __name__ == "__main__":
    main()
```

**Co tento skript dělá:**  
1. Načte OCR engine.  
2. Načte vybraný obrázek a extrahuje text.  
3. Zapíše **prohledávatelné PDF/A**, které můžete okamžitě distribuovat nebo archivovat.  

Neváhejte zabalit logiku `main` do funkce, která zpracuje celý adresář – stačí iterovat přes `os.listdir()` a opakovat tři kroky pro každý soubor.

## Další kroky a související témata

Nyní, když ovládáte **jak OCR PDF**, zvažte následující nápady:

- **Dávkové zpracování:** Použijte `concurrent.futures` k OCR desítek faktur paralelně.  
- **Vkládání metadat:** Přidejte data vytvoření nebo čísla faktur do metadat PDF pro snazší indexaci.  
- **Hybridní PDF:** Kombinujte prohledávatelný text s vloženými originálními obrázky pro „digitální dvojče“ papírového dokumentu.  
- **Alternativní výstupy:** Exportujte do **DOCX** nebo **HTML**, pokud downstream systémy potřebují editovatelné formáty.  

Každý z nich staví na základních konceptech, které jste se právě naučili – rozpoznat, exportovat, ověřit.

## Shrnutí

Stručně řečeno, nyní víte **jak OCR PDF** soubory tím, že jednoduchý obrázek převedete na **prohledávatelné PDF/A** pomocí pouhých tří řádků Pythonu. Skript provádí těžkou práci, zachovává původní grafiku a poskytuje vám dokument splňující standardy, který můžete prohledávat, archivovat nebo sdílet.  

Vyzkoušejte to na vlastních fakturách, účtenkách nebo naskenovaných smlouvách. Pokud narazíte na problémy, zanechte komentář níže nebo si prohlédněte oficiální dokumentaci SDK – obvykle obsahuje spoustu dalších příkladů. Šťastné programování a užívejte si nově získanou schopnost učinit jakýkoli obrázek okamžitě prohledávatelným! 

![Příklad OCR PDF ukazující původní obrázek a překrytí prohledávatelným PDF](placeholder.png "How to OCR PDF example")

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak OCR PDF v .NET s Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Rozpoznat text PDF – OCR operace s Aspose.OCR pro Java](/ocr/english/java/ocr-operations/)
- [Převod obrázků na PDF C# – Uložit vícestránkový OCR výsledek](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}