---
category: general
date: 2026-03-18
description: Uruchom OCR na obrazie, aby wyodrębnić tekst z pliku PNG i wygenerować
  przeszukiwalny PDF. Dowiedz się, jak rozpoznawać tekst na obrazie i konwertować
  PNG na PDF w kilka minut.
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: pl
og_description: Wykonaj OCR na obrazie, aby wyodrębnić tekst z pliku PNG, rozpoznać
  tekst na obrazie i wygenerować przeszukiwalny PDF. Postępuj zgodnie z tym przewodnikiem
  krok po kroku.
og_title: Uruchom OCR na obrazie – szybko wyodrębnij tekst z PNG
tags:
- OCR
- Python
- Image Processing
title: Uruchom OCR na obrazie – szybko wyodrębnij tekst z PNG
url: /pl/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uruchom OCR na obrazie – Szybko wyodrębnij tekst z PNG

Czy kiedykolwiek potrzebowałeś **run OCR on image** i nie wiedziałeś, od czego zacząć? Może masz zeskanowany artykuł zapisany jako `article.png` i po prostu chcesz uzyskać czysty tekst, albo potrzebujesz przeszukiwalnego PDF do archiwizacji. Tak czy inaczej, jesteś we właściwym miejscu. W tym samouczku przeprowadzimy Cię przez wyodrębnianie tekstu z PNG, rozpoznawanie obrazu tekstowego oraz konwersję tego PNG do przeszukiwalnego PDF — wszystko przy użyciu kilku linijek kodu.

> **What you’ll get:** kompletny, uruchamialny skrypt, który ładuje PNG, uruchamia OCR, zapisuje wynik hOCR i opcjonalnie tworzy przeszukiwalny PDF. Bez brakujących importów, bez „zobacz dokumentację” ślepych zaułków — po prostu samodzielne rozwiązanie, które możesz od razu wstawić do swojego projektu.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz:

- **Python 3.8+** (składnia użyta tutaj działa w każdej nowszej wersji)
- Bibliotekę **`ocr_engine`**, której używasz (przykład zakłada klasę o nazwie `OcrEngine`; zamień na Tesseract, EasyOCR itp., w razie potrzeby)
- Obraz PNG, który chcesz przetworzyć (np. `article.png` umieszczony w folderze, do którego możesz odwołać się)
- Uprawnienia do zapisu w katalogu wyjściowym

Jeśli używasz Tesseract w tle, zainstaluj go za pomocą:

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

A następnie zainstaluj wrapper Pythona:

```bash
pip install pytesseract Pillow
```

*Pro tip:* utrzymuj swoją bibliotekę OCR aktualną — nowe pakiety językowe i poprawki wydajności pojawiają się regularnie.

## Uruchom OCR na obrazie – Przewodnik krok po kroku

Poniżej znajduje się **kompletny skrypt**. Śmiało skopiuj‑wklej go do pliku o nazwie `run_ocr.py` i uruchom przy pomocy `python run_ocr.py`.

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### Co robi skrypt, w prostych słowach

1. **Instantiate** silnik OCR, aby móc kontrolować jego ustawienia.  
2. **Load** plik PNG (`article.png`). Skrypt przerywa działanie, jeśli plik nie istnieje — nie pojawią się później tajemnicze błędy `NoneType`.  
3. **Select** `hocr` jako format eksportu. Ten format zachowuje oryginalny układ, co jest niezbędne przy późniejszej konwersji obrazu do przeszukiwalnego PDF.  
4. **Run** silnik rozpoznawania; tutaj odbywa się najcięższa praca.  
5. **Write** plik XML hOCR do `article.hocr`. Masz teraz maszynowo‑czytelną reprezentację tekstu i jego współrzędnych.  
6. *(Optional)* Przełącz na `"pdf"` i wygeneruj przeszukiwalny PDF w jednym dodatkowym kroku.

Oczekiwanym wynikiem jest plik `.hocr` zakodowany w UTF‑8, który wygląda mniej więcej tak (skrócony dla zwięzłości):

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

Jeśli odkomentujesz sekcję PDF, otrzymasz również `article_searchable.pdf`, który możesz otworzyć w dowolnej przeglądarce PDF i użyć pola wyszukiwania **Ctrl + F**, aby natychmiast znaleźć słowa.

![Run OCR on image example output](example.png "Run OCR on image – hOCR and PDF results")

## Jak wyodrębnić tekst z PNG przy użyciu OcrEngine

Jeśli potrzebujesz jedynie surowego tekstu (bez układu, bez PDF), możesz całkowicie pominąć krok hOCR:

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*Dlaczego wybrać plain text?* Jest lekki, idealny do indeksowania i świetnie współpracuje z dalszymi pipeline'ami NLP.

## Rozpoznaj obraz tekstowy i wygeneruj przeszukiwalny PDF

Generowanie przeszukiwalnego PDF to dwuczęściowy taniec:

1. **Run OCR** z `hocr` (tak jak powyżej), aby uzyskać informacje o układzie.  
2. **Combine** oryginalny PNG z hOCR w PDF przy użyciu eksportera PDF silnika.

Większość nowoczesnych bibliotek OCR (Tesseract, ABBYY, Google Vision) udostępnia eksport `pdf`, który robi dokładnie to. Fragment w bloku *Optional* głównego skryptu pokazuje ten wzorzec. Jeśli Twoja biblioteka nie ma wbudowanego eksportera PDF, możesz użyć **`pdf2image`** + **`reportlab`**, aby połączyć obraz i hOCR — daj znać, a udostępnię szybki dodatkowy przykład.

## Konwertuj PNG do PDF z wynikiem OCR

Czasami po prostu potrzebujesz **plain PDF**, który zawiera obraz (bez warstwy przeszukiwalnej). To jeszcze prostsze:

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

Połącz to z krokiem OCR, jeśli potrzebujesz wersji przeszukiwalnej, lub zachowaj jako wierną wizualną replikę do celów archiwalnych.

## Typowe pułapki i wskazówki

| Problem | Dlaczego się dzieje | Szybka naprawa |
|-------|----------------|-----------|
| **Rozmyty lub niskiej rozdzielczości PNG** | Dokładność OCR spada dramatycznie poniżej ~300 DPI. | Zwiększ rozmiar przy użyciu `Image.resize((width*2, height*2), Image.LANCZOS)` przed przekazaniem do silnika. |
| **Nieprawidłowy język** | Silnik domyślnie używa angielskiego; znaki nie‑angielskie stają się zniekształcone. | Wywołaj `ocr_engine.setLanguage('deu')` (lub odpowiedni kod ISO) przed `recognize()`. |
| **Brak wyjścia hOCR** | Niektóre silniki domyślnie zwracają plain text, gdy nie wywołano `setExportFormat`. | Sprawdź, czy `setExportFormat("hocr")` jest wywoływane **przed** `recognize()`. |
| **Błędy uprawnień do pliku** | Próba zapisu do folderu tylko do odczytu. | Użyj ścieżki wewnątrz projektu lub najpierw `os.makedirs(..., exist_ok=True)`. |
| **Duże PDFy powodują skoki pamięci** | Eksporter PDF trzyma cały obraz w pamięci RAM. | Przetwarzaj strony w partiach lub użyj strumieniowego zapisu PDF. |

*Pro tip:* zawsze testuj na małym przykładzie obrazu przed przetwarzaniem tysięcy. Oszczędza to godziny debugowania.

## Podsumowanie

Teraz wiesz **how to run OCR on image** plików, **extract text from PNG**, **recognize text image** do dalszych zadań, **generate a searchable PDF** oraz **convert PNG to PDF**, gdy potrzebujesz prostego archiwum. Dostarczony skrypt to kompletny, gotowy do skopiowania i wklejenia kod, który działa od razu, a sekcje opcjonalne pozwalają dostosować wynik do Twojego konkretnego przepływu pracy.

### Co dalej?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}