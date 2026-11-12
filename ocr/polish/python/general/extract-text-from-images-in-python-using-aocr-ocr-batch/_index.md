---
category: general
date: 2026-06-25
description: Wydobywaj tekst z obrazów przy użyciu biblioteki aocr w Pythonie – poznaj
  przetwarzanie wsadowe OCR, ustaw tryb rozpoznawania na drukowany i dodaj postprocesor
  AI.
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: pl
og_description: Wyodrębnij tekst z obrazów przy użyciu biblioteki aocr w Pythonie.
  Ten samouczek pokazuje OCR wsadowe, tryb rozpoznawania druku oraz opcjonalny postprocesor
  AI.
og_title: Wyodrębnianie tekstu z obrazów w Pythonie – Kompletny przewodnik aocr Batch
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: Wyodrębnij tekst z obrazów w Pythonie przy użyciu aocr OCR Batch
url: /pl/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnianie tekstu z obrazów w Pythonie przy użyciu aocr OCR Batch

Czy kiedykolwiek potrzebowałeś **wyodrębnić tekst z obrazów**, ale przytłoczyło cię dziesiątki drobnych kroków? Nie jesteś sam. Niezależnie od tego, czy digitalizujesz zeskanowane formularze, pobierasz dane z paragonów, czy tworzysz przeszukiwalne archiwum, uzyskanie niezawodnych wyników OCR w dużej skali może przypominać wspinaczkę pod górę.

Dobre wieści? Dzięki **bibliotece aocr** możesz uruchomić pełny **Python OCR batch** w zaledwie kilku linijkach. W tym przewodniku przeprowadzimy Cię przez tworzenie batcha OCR, ładowanie wszystkich obsługiwanych obrazów z folderu, wybór odpowiedniego **recognition mode printed**, a nawet dołączenie **AI postprocessora** dla dodatkowego zwiększenia dokładności. Po zakończeniu będziesz mieć gotowy do uruchomienia skrypt, który wyodrębnia tekst z obrazów i informuje, ile tekstu zostało przechwycone dla każdego pliku.

## Co się nauczysz

- Jak zainstalować i zaimportować pakiet `aocr`.
- Konfigurowanie `OcrBatch`, aby automatycznie obsługiwał tysiące plików.
- Wybór optymalnego trybu rozpoznawania dla drukowanych dokumentów.
- (Opcjonalnie) Podłączenie AI post‑processora w celu oczyszczenia szumnych wyników.
- Wyświetlanie ścieżki każdego pliku wraz z długością wyodrębnionego tekstu.
- Wskazówki dotyczące obsługi przypadków brzegowych, takich jak nieobsługiwane formaty lub puste strony.

### Wymagania wstępne

- Python 3.8 lub nowszy zainstalowany na twoim komputerze.  
- Podstawowa znajomość skryptów w Pythonie (pętle, importy itp.).  
- Dostęp do folderu ze zeskanowanymi obrazami (PNG, JPG, TIFF itp.).  

Jeśli masz to wszystko, zanurzmy się — nie są potrzebne żadne zewnętrzne usługi.

## Krok 1: Zainstaluj bibliotekę aocr

Na początek. Pakiet `aocr` nie jest częścią biblioteki standardowej, więc musisz go pobrać z PyPI.

```bash
pip install aocr
```

> **Wskazówka:** Użyj wirtualnego środowiska (`python -m venv .venv`), aby utrzymać zależności w izolacji.  

Po zainstalowaniu możesz zaimportować podstawowe klasy.

```python
# core imports
import aocr
```

## Krok 2: Utwórz instancję OCR Batch

`OcrBatch` jest silnikiem, który przeszuka twój katalog i będzie śledził każdy plik obrazu. Pomyśl o nim jak o taśmie produkcyjnej, która podaje obrazy do silnika OCR.

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

W tym momencie batch jest pusty, ale wypełnimy go w następnym kroku.

## Krok 3: Dodaj wszystkie obsługiwane obrazy z folderu (rekursywnie)

Prawdopodobnie masz zagnieżdżoną strukturę folderów — może jeden podfolder na klienta lub miesiąc. Metoda `add_folder` przechodzi drzewo za Ciebie, pobierając każdy obraz, który potrafi odczytać.

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

Zastąp `"YOUR_DIRECTORY/scanned_forms/"` rzeczywistą ścieżką w twoim systemie. Po tym wywołaniu `ocr_batch.file_paths` zawiera listę absolutnych nazw plików, a batch dokładnie wie, ile elementów będzie przetwarzał.

## Krok 4: Wybierz tryb rozpoznawania dla tekstu drukowanego

Silnik `aocr` obsługuje kilka trybów (handwritten, printed, mixed). Ponieważ pracujemy z czystymi, drukowanymi formularzami, ustaw tryb odpowiednio. Ta mała flaga może dramatycznie poprawić dokładność, ponieważ silnik pomija ciężkie heurystyki potrzebne dla skryptów kursywnych.

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **Dlaczego to ważne:** Tekst drukowany ma spójne linie bazowe i kształty znaków, co pozwala modelowi OCR zastosować bardziej precyzyjne słowniki znaków. Jeśli pozostawisz tryb na „auto”, możesz otrzymać dodatkowy szum przy skanach o niskiej rozdzielczości.

## Krok 5: (Opcjonalnie) Dołącz AI Post‑Processor

Jeśli twoje skany cierpią na rozmycie, niski kontrast lub nietypowe czcionki, AI post‑processor może oczyścić surowe wyjście OCR przed przekazaniem go do systemów downstream. Metoda `set_ai_postprocessor` oczekuje obiektu implementującego interfejs `process(text: str) -> str`.

Poniżej znajduje się minimalny przykład użycia fikcyjnej klasy `SimpleCleaner`. W praktyce możesz podłączyć transformer HuggingFace, własny model językowy lub nawet regułowy korektor ortograficzny.

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

Jeśli pominiemy ten krok, batch po prostu zwróci surowe ciągi OCR.

## Krok 6: Uruchom OCR na całym batchu i zbierz wyniki

Teraz zaczyna się ciężka praca. Metoda `run` iteruje po każdym pliku, uruchamia silnik OCR, przekazuje wynik przez opcjonalny AI post‑processor i zwraca listę ciągów — po jednym na obraz.

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

Ponieważ metoda zwraca zwykłą listę Pythona, możesz traktować ją jak każdą inną kolekcję — przechowywać, zapisać do CSV lub wprowadzić do bazy danych.

## Krok 7: Wyświetl ścieżkę każdego pliku wraz z długością wyodrębnionego tekstu

Szybka kontrola poprawności to wydrukowanie, ile znaków zostało wyodrębnionych z każdego pliku. Jeśli strona jest pusta lub OCR się nie powiódł, zobaczysz długość `0`.

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

Typowy wynik wygląda tak:

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

Widząc flagę `0`, od razu wiesz, które pliki wymagają ponownego sprawdzenia (może są uszkodzone lub wcale nie są obrazem).

## Obsługa typowych przypadków brzegowych

### 1. Nieobsługiwane typy plików

`aocr` cicho pomija pliki, których nie może zdekodować. Jeśli podejrzewasz, że masz wśród nich PDF-y lub BMP-y, odfiltruj je wcześniej:

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. Duże batchy i zużycie pamięci

Przetwarzanie tysięcy skanów wysokiej rozdzielczości może zwiększyć zużycie pamięci. Zminimalizuj to, przetwarzając w partiach:

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. Puste lub niskokontrastowe strony

Jeśli strona zwraca mniej niż 10 znaków, możesz oznaczyć ją do ręcznej weryfikacji:

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## Pełny działający przykład

Łącząc wszystko razem, oto skrypt, który możesz skopiować i od razu uruchomić. Zapisz go jako `batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**Oczekiwany wynik** (skrócony dla zwięzłości):

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

Uruchom go za pomocą:

```bash
python batch_ocr.py
```

Jeśli wszystko jest poprawnie skonfigurowane, zobaczysz linię dla każdego obrazu, każda podająca liczbę znaków wyodrębnionego tekstu.

## Najczęściej zadawane pytania

**P:** Działa to na PDF-ach?  
**O:** Nie od razu. `aocr` obsługuje tylko obrazy rastrowe. Najpierw skonwertuj PDF-y na PNG/TIFF (np. przy użyciu `pdf2image`).

**P:** Czy mogę zmienić tryb rozpoznawania na odręczny?  
**O:** Oczywiście — wystarczy zamienić `aocr.RecognitionMode.PRINTED` na `aocr.RecognitionMode.HANDWRITTEN`. Spodziewaj się wolniejszego czasu działania, ale lepszych wyników na odręcznych notatkach.

**P:** Co jeśli potrzebuję wsparcia wielojęzycznego?  
**O:** Biblioteka dostarcza pakiety językowe. Zainstaluj żądany moduł językowy (`pip install aocr-lang-fr` dla francuskiego itp.) i ustaw `ocr_batch.language = "fr"` przed uruchomieniem.

## Kolejne kroki i powiązane tematy

- **Przetwarzanie równoległe:** Owiń wykonanie batcha w `concurrent.futures.ThreadPoolExecutor`, aby wykorzystać wiele rdzeni CPU.  
- **Przechowywanie wyników:** Zapisz `ocr_results` do CSV lub bazy danych SQLite dla analiz downstream.  
- **Integracja z chmurowym AI:** Zamień `SimpleCleaner` na model transformer z HuggingFace dla najnowocześniejszej korekty ortograficznej.  
- **Dostrajanie aocr:** Jeśli masz własny zestaw czcionek, zbadaj `aocr.Trainer`, aby poprawić dokładność trybu drukowanego.  

---

To wszystko — masz teraz solidny

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Wyodrębnianie tekstu z obrazu przy użyciu Aspose OCR – przewodnik krok po kroku](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Wyodrębnianie tekstu z obrazów przy użyciu operacji OCR na folderach](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Jak przetwarzać wsadowo obrazy OCR przy użyciu listy w Aspose.OCR dla .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}