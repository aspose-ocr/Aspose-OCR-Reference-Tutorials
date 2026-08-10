---
category: general
date: 2026-06-06
description: Jak wykonać OCR PDF i tworzyć przeszukiwalne pliki PDF z obrazów przy
  użyciu Pythona. Dowiedz się, jak dodać przeszukiwalny tekst i w kilka minut przekonwertować
  obraz na PDF/A.
draft: false
keywords:
- how to ocr pdf
- create searchable pdf
- add searchable text
- ocr image to pdf
- convert image to pdf/a
language: pl
og_description: Jak przeprowadzić OCR PDF krok po kroku. Dowiedz się, jak dodać tekst
  przeszukiwalny i przekonwertować obraz na PDF/A przy użyciu prostego skryptu w Pythonie.
og_title: Jak zrobić OCR PDF – szybki przewodnik tworzenia przeszukiwalnych PDF‑ów
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
title: Jak wykonać OCR PDF w Pythonie – Utwórz przeszukiwalny PDF z obrazów
url: /pl/python-java/general/how-to-ocr-pdf-in-python-create-searchable-pdf-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak OCR-ować PDF – Zamień zeskanowane obrazy w przeszukiwalne PDFy

Zastanawiałeś się kiedyś **jak OCR-ować PDF** gdy jedyne, co masz, to zeskanowany obraz faktury lub paragonu? Nie jesteś jedyny. W wielu biurach przychodząca dokumentacja pojawia się jako płaskie pliki PNG lub JPEG, a kolejny krok — uczynienie tej treści przeszukiwalną — wydaje się czarną skrzynką.  

The good news? With just a few lines of Python you can **create searchable PDF** files, **add searchable text**, and even **convert image to PDF/A** for long‑term archiving. In this tutorial we’ll walk through each step, explain why it matters, and give you a ready‑to‑run script that you can drop into any project.

> **Porada:** To samo podejście działa dla skanów wielostronicowych; po prostu iteruj po plikach, a silnik wykona ciężką pracę.

---

## Czego będziesz potrzebować

Before we dive in, make sure you have the following on your machine:

| Wymaganie | Dlaczego jest ważne |
|-------------|----------------|
| Python 3.9 or newer | Nowoczesna składnia i lepsze wsparcie bibliotek |
| `pdfium`‑based OCR engine (e.g., `pdfocr` or a commercial SDK) | Obsługuje zarówno rozpoznawanie obrazu, jak i generowanie PDF/A |
| An image file (PNG, JPEG, TIFF) you want to turn into a searchable PDF | Plik obrazu (PNG, JPEG, TIFF), który chcesz zamienić w przeszukiwalny PDF |
| Write permission to the output folder | Uprawnienia zapisu do folderu wyjściowego |

If you haven’t installed the OCR SDK yet, run:

```bash
pip install pdfocr   # replace with your vendor's package name
```

That’s it—no complex system dependencies, just a pip install.

## Jak OCR-ować PDF – Przegląd

At a high level the process consists of three simple actions:

1. **Recognize** the text inside the image while preserving the original graphics.  
2. **Export** the OCR result together with the original image as a **searchable PDF/A** (the archival‑friendly PDF flavour).  
3. **Validate** that the resulting file contains selectable, searchable text layered over the original picture.

Below you’ll see each step in code, with explanations of the *why* behind the commands.

## Krok 1: Rozpoznaj tekst z obrazu

First we ask the OCR engine to read the pixels and return a result object that holds both the raw image and the extracted text. Think of it as the engine “reading” the invoice for you.

```python
# Step 1: Recognize text from the image and keep the original graphics
result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

### Dlaczego to ważne

- **Zachowanie grafiki** oznacza, że układ wizualny (tabele, loga, pieczęcie) pozostaje dokładnie taki, jak zeskanowano.  
- Obiekt `result` zazwyczaj zawiera ukrytą warstwę tekstową, którą później wstawimy do PDF.  
- Użycie `recognize_image` zamiast `recognize_pdf` unika dodatkowego kroku konwersji, co przyspiesza przetwarzanie jednopostaciowych obrazów.

#### Typowe warianty

- Jeśli masz **wielostronicowy TIFF**, przekaż bezpośrednio ścieżkę do pliku; większość silników potraktuje każdą stronę jako osobny obraz.  
- Dla PDF‑ów, które już zawierają obrazy, możesz wywołać `engine.recognize_pdf("file.pdf")` i pominąć ten krok całkowicie.

## Krok 2: Eksportuj wynik OCR jako przeszukiwalny PDF/A

Now we take the `result` from step 1 and tell the engine to write a new file. The key flag here is *PDF/A*—the ISO‑standard version of PDF designed for long‑term preservation.

```python
# Step 2: Export the OCR result together with the original image as a searchable PDF/A
result.save_as_pdfa("YOUR_DIRECTORY/invoice_searchable.pdf")
```

### Dlaczego to ważne

- **Przeszukiwalny PDF**: Plik wyjściowy zawiera ukrytą, wybieralną warstwę tekstową. Teraz możesz używać Ctrl + F w dokumencie.  
- **Zgodność z PDF/A**: Niektóre organizacje (prawne, finansowe) wymagają PDF/A do ścieżek audytu; ten krok spełnia ten wymóg automatycznie.  
- Metoda także **dodaje przeszukiwalny tekst** bez spłaszczania obrazu, więc wierność wizualna pozostaje idealna.

#### Edge case: Need a regular PDF instead?

If you don’t care about PDF/A, replace `save_as_pdfa` with `save_as_pdf`. The rest of the workflow stays the same.

## Krok 3: Zweryfikuj przeszukiwalny PDF

A quick sanity check saves you from mysterious bugs later. Open the generated file in any PDF viewer, try selecting a word, and use the search function.

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

### Expected output

When you run the script, the console prints:

```
✅ PDF created successfully: YOUR_DIRECTORY/invoice_searchable.pdf
```

Opening the file, you should see the original invoice image with a faint, invisible text layer. Highlight any word and you’ll notice it’s selectable—**that’s the searchable text** you just added.

## Dodawanie przeszukiwalnego tekstu do istniejących PDF‑ów (Bonus)

Sometimes you already have a PDF but need to **add searchable text** to it. The same engine can overlay OCR results onto an existing PDF:

```python
# Bonus: Add searchable text to an existing PDF file
existing_pdf = engine.load_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result = engine.recognize_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result.apply_to(existing_pdf).save_as_pdfa("YOUR_DIRECTORY/old_scanned_searchable.pdf")
```

Here `apply_to` merges the hidden layer with the original pages, letting you **create searchable PDF** without re‑scanning.

## Częste pułapki i wskazówki

| Pułapka | Jak tego uniknąć |
|---------|-----------------|
| **Obrazy źródłowe o niskiej rozdzielczości** (< 150 dpi) | Zwiększ rozdzielczość lub poproś o skan w wyższej rozdzielczości; dokładność OCR drastycznie spada poniżej 150 dpi. |
| **Brak danych językowych** | Zainstaluj odpowiednie pakiety językowe dla swojego silnika OCR (`pip install pdfocr[eng,spa]`). |
| **Folder wyjściowy nie jest zapisywalny** | Uruchom skrypt z odpowiednimi uprawnieniami lub wybierz inny katalog. |
| **Walidacja PDF/A nie powiodła się** | Upewnij się, że nie osadzasz nieobsługiwanych czcionek ani JavaScript; większość SDK automatycznie radzi sobie z tym przy użyciu `save_as_pdfa`. |

## Pełny skrypt – rozwiązanie jednoplikowe

Below is a self‑contained script that ties everything together. Copy‑paste it, replace the placeholder paths, and you’re ready to **convert image to PDF/A** in seconds.

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

**Co robi ten skrypt:**  
1. Ładuje silnik OCR.  
2. Odczytuje wybrany obraz i wyodrębnia tekst.  
3. Zapisuje **przeszukiwalny PDF/A**, który możesz od razu rozpowszechniać lub archiwizować.  

Feel free to wrap the `main` logic in a function that processes a whole folder—just iterate over `os.listdir()` and repeat the three steps for each file.

## Kolejne kroki i powiązane tematy

Now that you’ve mastered **how to OCR PDF**, consider exploring these follow‑up ideas:

- **Przetwarzanie wsadowe:** Użyj `concurrent.futures`, aby OCR‑ować dziesiątki faktur równolegle.  
- **Wstrzykiwanie metadanych:** Dodaj daty utworzenia lub numery faktur do metadanych PDF, aby ułatwić indeksowanie.  
- **Hybrydowe PDFy:** Połącz przeszukiwalny tekst z osadzonymi oryginalnymi obrazami, tworząc „cyfrowego bliźniaka” dokumentu papierowego.  
- **Alternatywne formaty wyjściowe:** Eksportuj do **DOCX** lub **HTML**, jeśli systemy downstream potrzebują edytowalnych formatów.  

Each of these builds on the core concepts you just learned—recognize, export, verify.

## Podsumowanie

In a nutshell, you now know **how to OCR PDF** files by turning a simple image into a **searchable PDF/A** with just three lines of Python. The script handles the heavy lifting, preserves the original graphics, and gives you a standards‑compliant document that you can search, archive, or share.  

Give it a spin with your own invoices, receipts, or scanned contracts. If you hit any snags, drop a comment below or check the SDK’s official docs—they’re usually packed with extra examples. Happy coding, and enjoy the newfound ability to make any image instantly searchable! 

![Przykład OCR PDF pokazujący oryginalny obraz i nakładkę przeszukiwalnego PDF](placeholder.png "Przykład OCR PDF")

## Co warto nauczyć się dalej?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Jak OCR-ować PDF w .NET z Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Rozpoznawanie tekstu PDF – operacje OCR z Aspose.OCR dla Javy](/ocr/english/java/ocr-operations/)
- [Konwertowanie obrazów do PDF C# – zapisywanie wyniku OCR wielostronicowego](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}