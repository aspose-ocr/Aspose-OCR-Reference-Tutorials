---
category: general
date: 2026-07-05
description: Wyodrębnij tabelę z obrazu za pomocą Pythona OCR. Dowiedz się, jak wyodrębnić
  tabelę, przekonwertować obraz na TSV i opanuj techniki OCR tabeli w Pythonie.
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: pl
og_description: Wyodrębnij tabelę z obrazu przy użyciu OCR w Pythonie. Ten przewodnik
  pokazuje, jak wyodrębnić tabelę, przekonwertować obraz na TSV oraz używać narzędzi
  OCR do tabel w Pythonie.
og_title: Wyodrębnij tabelę z obrazu – konwertuj obraz na TSV w Pythonie
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  headline: Extract Table from Image – Convert Image to TSV in Python
  type: TechArticle
- description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  name: Extract Table from Image – Convert Image to TSV in Python
  steps:
  - name: Initialise the aocr OCR engine.
    text: Initialise the aocr OCR engine.
  - name: Attach the AI post‑processor.
    text: Attach the AI post‑processor.
  - name: Load a table image.
    text: Load a table image.
  - name: Perform structured OCR.
    text: Perform structured OCR.
  - name: Clean the results.
    text: Clean the results.
  - name: Export the table as a TSV file.
    text: Export the table as a TSV file.
  type: HowTo
tags:
- OCR
- Python
- Table Extraction
title: Wyodrębnij tabelę z obrazu – konwertuj obraz na TSV w Pythonie
url: /pl/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnij tabelę z obrazu – Konwertuj obraz do TSV w Pythonie

Zastanawiałeś się kiedyś, jak wyodrębnić tabelę z obrazu bez wyrywania sobie włosów? W tym samouczku przeprowadzimy Cię przez **jak wyodrębnić tabelę** z obrazu przy użyciu biblioteki `aocr`, a następnie przekształcimy te dane w schludny plik TSV. Bez magii, tylko kilka linijek Pythona i odrobina AI‑napędzanego post‑processingu.

Jeśli kiedykolwiek próbowałeś kopiować‑wklejać tabelę ze skanowanej faktury lub zrzutu ekranu i skończyło się to chaotycznym bałaganem, docenisz, dlaczego podejście oparte na OCR jest warte opanowania. Po zakończeniu będziesz mógł podać dowolny obraz tabeli do Pythona i otrzymać czyste, wartości oddzielone tabulacjami, gotowe do arkuszy kalkulacyjnych lub baz danych.

---

## Czego będziesz potrzebować

Zanim zanurkujemy, upewnij się, że masz następujące elementy na swoim komputerze:

| Wymaganie | Dlaczego jest ważne |
|-----------|---------------------|
| Python 3.9+ | Pakiet `aocr` jest przeznaczony dla nowoczesnych środowisk Python. |
| Biblioteka `aocr` (`pip install aocr`) | Dostarcza silnik OCR oraz AI post‑processor, którego użyjemy. |
| Plik obrazu zawierający tabelę (PNG, JPG, itp.) | Źródłowe dane, które będziemy wyodrębniać. |
| Opcjonalnie: wirtualne środowisko | Utrzymuje zależności w izolacji — zdecydowanie zalecane. |

Posiadanie tych elementów z wyprzedzeniem oszczędza przerwy w połowie przewodnika.

---

## Zainstaluj zależności

Najpierw zainstalujmy narzędzia OCR. Otwórz terminal i uruchom:

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **Pro tip:** Jeśli napotkasz błędy uprawnień, dodaj `--user` do polecenia `pip install` lub użyj `pipx` do instalacji globalnej.

---

## Krok 1 – Zainicjalizuj silnik OCR

Silnik jest sercem procesu. Myśl o nim jak o „mózgu”, który patrzy na każdy piksel i decyduje, jaki znak gdzie należy.

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

Dlaczego tworzymy instancję silnika zamiast wywołać jedną funkcję? Obiekt silnika pozwala nam później dołączyć własne post‑processory, dając precyzyjną kontrolę nad wynikiem — co jest niezbędne, gdy potrzebujesz **ocr table image python** precyzji.

---

## Krok 2 – Dołącz procesor AI

`aocr` dostarcza lekki AI post‑processor, który oczyszcza surowe wyniki OCR, zachowując jednocześnie granice komórek. Nie wymaga dodatkowych argumentów, co utrzymuje kod schludnym.

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

Jeśli pominiesz ten krok, nadal otrzymasz surowy tekst, ale struktura tabeli będzie szumna — pomyśl o arkuszu kalkulacyjnym, w którym każda komórka jest zagadką. Post‑processor wykonuje ciężką pracę, dopasowując tekst do oryginalnej siatki.

---

## Krok 3 – Załaduj obraz tabeli

Możesz załadować obraz z dowolnej ścieżki, ale dla przejrzystości użyjemy katalogu zastępczego. Zastąp `"YOUR_DIRECTORY/invoice_table.png"` faktyczną ścieżką do swojego pliku.

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **Note:** `aocr.Image` automatycznie wykrywa format obrazu i normalizuje kanały kolorów, więc nie musisz wstępnie przetwarzać pliku, chyba że jest poważnie uszkodzony.

---

## Krok 4 – Wykonaj strukturalny OCR

Teraz silnik skanuje obraz i zwraca surowy obiekt tabeli. Obiekt ten zawiera wiersze, kolumny oraz surowy tekst dla każdej komórki.

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

Dlaczego używamy `recognize_structured` zamiast ogólnego wywołania `recognize`? Wariant strukturalny stara się wywnioskować granice wierszy/kolumn, dając wynik w postaci macierzy, który jest znacznie łatwiejszy do konwersji na TSV później.

---

## Krok 5 – Oczyść dane przy użyciu procesora AI

Uruchomienie post‑processora udoskonala surowy wynik: usuwa zbędne znaki, scala podzielone fragmenty i zapewnia prawidłowe wyrównanie tekstu w każdej komórce.

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

Jeśli przejrzysz `processed_table.table`, zobaczysz listę wierszy, przy czym każdy wiersz jest listą obiektów `Cell`. Każdy `Cell` ma atrybut `.text` zawierający wyczyszczony ciąg znaków.

---

## Krok 6 – Wyeksportuj tabelę jako TSV

Ostatni krok to przekształcenie przetworzonych danych w plik wartości oddzielonych tabulacjami (TSV) — dokładnie tego potrzebujesz, gdy chcesz **convert image to TSV** dla Excela lub Google Sheets.

```python
import csv

# Define the output TSV path
tsv_path = "extracted_table.tsv"

# Open the file and write rows as tab‑separated values
with open(tsv_path, "w", newline="", encoding="utf-8") as tsv_file:
    writer = csv.writer(tsv_file, delimiter="\t")
    for row in processed_table.table:
        # Extract text from each cell and write the row
        writer.writerow([cell.text for cell in row])

print(f"✅ Table successfully saved to {tsv_path}")
```

Uruchomienie skryptu wypisuje każdy wiersz w konsoli (jeśli wolisz) i zapisuje czysty plik TSV, który możesz otworzyć w dowolnym programie arkusza kalkulacyjnego.

### Szybka weryfikacja

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

Powinieneś zobaczyć starannie wyrównane kolumny, na przykład:

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

Jeśli wynik wygląda na pomieszany, sprawdź jakość obrazu (ostrość, kontrast) i rozważ dostosowanie ustawień silnika OCR — `engine.set_config(...)` pozwala regulować modele językowe i progi pewności.

---

## Obsługa typowych przypadków brzegowych

| Sytuacja | Sugerowane rozwiązanie |
|----------|------------------------|
| **Obrócony obraz** | Wstępnie obróć używając `Pillow` (`Image.rotate`) przed przekazaniem go do `aocr`. |
| **Niski kontrast** | Zastosuj wyrównanie histogramu (`cv2.equalizeHist`), aby zwiększyć czytelność. |
| **Scalone komórki** | Przetwórz TSV, aby podzielić komórki na podstawie znanych separatorów lub użyj flagi `merge_cells=False`, jeśli jest dostępna. |
| **Wielostronicowe PDF‑y** | Najpierw przekonwertuj każdą stronę na obraz (`pdf2image`) i uruchom pipeline w pętli. |

Te drobne poprawki utrzymują Twój **ocr table image python** workflow odporny na różnorodne materiały źródłowe.

---

## Pełny skrypt – Kompleksowe rozwiązanie

Poniżej znajduje się kompletny, gotowy do uruchomienia skrypt, który łączy wszystkie omówione kroki. Zapisz go jako `extract_table.py` i uruchom `python extract_table.py`.

```python
#!/usr/bin/env python3
"""
Extract Table from Image – Convert Image to TSV (Python)

This script demonstrates how to:
1. Initialise the aocr OCR engine.
2. Attach the AI post‑processor.
3. Load a table image.
4. Perform structured OCR.
5. Clean the results.
6. Export the table as a TSV file.

Author: Your Name
Date: 2026-07-05
"""

import aocr
import csv
import sys
from pathlib import Path

def main(image_path: str, output_tsv: str = "extracted_table.tsv"):
    # Step 1 – Initialise engine
    engine = aocr.OcrEngine()

    # Step 2 – Attach AI post‑processor
    engine.set_post_processor(ai.run_postprocessor, None)

    # Step 3 – Load image
    if not Path(image_path).is_file():
        sys.exit(f"❌ Image not found: {image_path}")
    image = aocr.Image.from_file(image_path)

    # Step 4 – Structured OCR
    raw_table = engine.recognize_structured(image)

    # Step 5 – Clean with post‑processor
    processed_table = engine.run_postprocessor(raw_table)

    # Step 6 – Write TSV
    with open(output_tsv, "w", newline="", encoding="utf-8") as tsv_file:
        writer = csv.writer(tsv_file, delimiter="\


## Co warto nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Wyodrębnij tekst z obrazu za pomocą Aspose OCR – Przewodnik krok po kroku](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Jak wyodrębnić tabelę z obrazu przy użyciu Aspose.OCR dla .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Jak wyodrębnić tekst z obrazu przygotowując prostokąty w OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}