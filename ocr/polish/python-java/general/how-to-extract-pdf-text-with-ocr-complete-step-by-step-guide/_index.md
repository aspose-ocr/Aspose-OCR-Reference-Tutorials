---
category: general
date: 2026-03-26
description: Jak wyodrębnić tekst z PDF przy użyciu OCR. Dowiedz się, jak wczytać
  PDF jako obraz, rozpoznać tekst w PDF i wyodrębnić tekst z PDF za pomocą prostego
  przykładu w Pythonie.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: pl
og_description: Jak wyodrębnić tekst z PDF przy użyciu OCR. Ten przewodnik pokazuje,
  jak załadować PDF jako obraz, rozpoznać tekst w PDF i wyodrębnić tekst z PDF w Pythonie.
og_title: Jak wyodrębnić tekst z PDF przy użyciu OCR – pełny poradnik
tags:
- OCR
- Python
- PDF processing
title: Jak wyodrębnić tekst z PDF przy użyciu OCR – Kompletny przewodnik krok po kroku
url: /pl/python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyodrębnić tekst z PDF przy użyciu OCR – Kompletny przewodnik krok po kroku

Zastanawiałeś się kiedyś **jak wyodrębnić PDF** pliki, które w rzeczywistości są tylko zeskanowanymi obrazami? Nie jesteś sam — wielu programistów napotyka ten problem, gdy potrzebują przeszukiwalnej treści, a mają jedynie PDF‑y zawierające tylko obrazy. Dobre wieści? Kilka linijek kodu i solidna biblioteka OCR mogą w mgnieniu oka zamienić te obrazkowe PDF‑y na zwykły tekst.  

W tym samouczku przejdziemy przez **jak używać OCR**, aby wczytać PDF jako obraz, rozpoznać tekst w PDF i w końcu **wyodrębnić tekst z PDF** dokumentów dowolnej długości. Po zakończeniu będziesz mieć działający skrypt, jasne wyjaśnienie każdego kroku oraz kilka wskazówek, jak uniknąć typowych pułapek.

## Czego będziesz potrzebować

- Python 3.9 lub nowszy (kod działa także na 3.10+)  
- Pakiet Python `ocr` (lub dowolna kompatybilna biblioteka OCR udostępniająca `OcrEngine`, `OcrEngineMode` i `Imaging.Image`)  
- Wielostronicowy PDF, który chcesz przetworzyć (w demonstracji nazwijmy go `multi_page.pdf`)  
- Podstawowa znajomość środowisk wirtualnych (opcjonalnie, ale zalecane)

> **Pro tip:** Jeśli pracujesz w systemie Windows, rozważ użycie Anaconda Prompt; w macOS/Linux wystarczy proste `python -m venv venv && source venv/bin/activate`, aby wszystko zadziałało.

## Krok 1: Zainstaluj bibliotekę OCR

Najpierw pobierz pakiet OCR z PyPI. Poniższy przykład używa fikcyjnego pakietu `ocr`, który odzwierciedla API pokazane w kodzie, ale większość rzeczywistych bibliotek (np. `pytesseract` + `pdf2image`) działa w podobny sposób.

```bash
pip install ocr
```

Jeśli używasz innego silnika, zamień `ocr` na odpowiednią nazwę (np. `pip install pytesseract pdf2image`).

## Krok 2: Zainicjalizuj silnik OCR

Utworzenie instancji silnika jest podstawą **jak wyodrębnić PDF** tekst. Traktuj silnik jako mózg, który będzie interpretował piksele na każdej stronie PDF.

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **Dlaczego to ważne:** `set_engine_mode` pozwala wymienić szybkość na dokładność. `DEFAULT` to zrównoważony wybór; jeśli potrzebujesz wyższej precyzji, przełącz się na `HIGH_ACCURACY` (o ile biblioteka to obsługuje).

## Krok 3: Wczytaj PDF jako obiekt obrazu

OCR działa na obrazach, a nie na kontenerach PDF, więc najpierw musimy przekonwertować PDF do reprezentacji obrazu. Metoda `Imaging.Image.load` automatycznie obsługuje wielostronicowe PDF‑y.

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **Edge case:** Niektóre biblioteki akceptują tylko jednopostaciowy obraz. W takim przypadku trzeba by pętlić po każdej stronie przy użyciu `pdf2image.convert_from_path`. Nasze wywołanie `load` ukrywa tę złożoność, czyniąc **load pdf as image** jedną linijką kodu.

## Krok 4: Rozpoznaj tekst na wszystkich stronach

Teraz następuje sedno **recognize PDF text**. Silnik skanuje każdą stronę, zwracając listę obiektów wyników — po jednym na stronę.

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

Każdy `page_result` zawiera metody takie jak `get_text()` (czysty tekst) oraz `get_confidence()` (opcjonalna miara jakości).  

> **Tip:** Jeśli potrzebujesz tylko pierwszej strony, wywołaj `recognize(pdf_image[0])` zamiast pomocnika obsługującego wiele stron.

## Krok 5: Przejdź przez wyniki i wypisz wyodrębniony tekst

Na koniec iterujemy po wynikach, drukując tekst każdej strony. To kończy **extract text from PDF** workflow.

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### Oczekiwany wynik

Jeśli `multi_page.pdf` zawiera trzy strony z słowami „Hello”, „World” i „Python”, zobaczysz:

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

To wszystko — Twój PDF jest teraz w pełni przeszukiwalny, a tekst gotowy do dalszego przetwarzania (indeksowanie, analiza sentymentu, cokolwiek potrzebujesz).

## Krok 6: Radzenie sobie z typowymi problemami

| Problem | Dlaczego się pojawia | Szybka naprawa |
|---------|----------------------|----------------|
| **Pusty wynik** | Strony PDF są zeskanowane w niskim DPI, co utrudnia rozpoznanie znaków. | Zwiększ rozdzielczość obrazu przed OCR: `pdf_image = pdf_image.resize(300)` (300 DPI to optymalny punkt). |
| **Śmieciowe znaki** | Alfabet nie‑łaciński wymaga pakietów językowych. | Załaduj odpowiedni model językowy: `ocr_engine.load_language('spa')` dla hiszpańskiego, itp. |
| **Wyciek pamięci przy dużych PDF‑ach** | Ładowanie wszystkich stron naraz zużywa RAM. | Przetwarzaj strony w partiach: `for img in pdf_image.split(batch=10): …` (pseudo‑kod). |
| **Niska wydajność** | Użycie `DEFAULT` w ogromnym dokumencie może być wolne. | Przełącz na tryb `FAST` lub uruchom OCR równolegle przy pomocy `concurrent.futures`. |

## Bonus: Zapis wyodrębnionego tekstu do pliku

Większość rzeczywistych pipeline’ów wymaga trwałego przechowywania tekstu. Oto mały pomocnik, który zapisuje wszystko do `output.txt`.

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

Teraz możesz podać `output.txt` do silnika wyszukiwania, bazy danych lub dowolnego modelu NLP.

## Złożenie wszystkiego razem – pełny skrypt

Poniżej znajduje się kompletny, gotowy do uruchomienia program. Skopiuj‑wklej, dostosuj ścieżki do plików i gotowe.

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

Uruchom go:

```bash
python extract_pdf_ocr.py
```

Powinieneś zobaczyć zawartość każdej strony wypisaną w konsoli, a na końcu potwierdzenie, że plik `extracted_text.txt` został utworzony.

## Zakończenie

Omówiliśmy **jak wyodrębnić PDF** tekst z dokumentów zawierających wyłącznie obrazy przy użyciu silnika OCR, od instalacji biblioteki po obsługę wyników wielostronicowych i zapisywanie wyjścia. Teraz wiesz **jak używać OCR**, jak **wczytać PDF jako obraz** oraz jak **rozpoznać tekst w PDF** w sposób niezawodny.  

Co dalej? Spróbuj przełączyć domyślny tryb silnika na ustawienie wysokiej dokładności, poeksperymentuj z pakietami językowymi dla wielojęzycznych PDF‑ów lub podłącz wyodrębniony tekst do indeksu pełnotekstowego, takiego jak Elasticsearch. Niebo jest granicą, gdy opanujesz podstawy wyodrębniania tekstu z plików PDF.

---

![przykład wyodrębniania pdf](images/ocr_flowchart.png){alt="diagram przepływu jak wyodrębnić pdf"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}