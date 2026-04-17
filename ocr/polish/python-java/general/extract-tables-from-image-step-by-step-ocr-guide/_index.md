---
category: general
date: 2026-03-26
description: Wyodrębnij tabele z obrazu i przekształć obraz w arkusz kalkulacyjny
  przy użyciu OCR w Pythonie. Dowiedz się, jak wczytać obraz do OCR, odczytać tabele
  i wyodrębnić dane tabeli.
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: pl
og_description: Wyodrębnij tabele z obrazu za pomocą OCR w Pythonie. Ten przewodnik
  pokazuje, jak wczytać obraz do OCR, odczytać tabele i przekonwertować je na arkusz
  kalkulacyjny.
og_title: Wyodrębnianie tabel z obrazu – Kompletny samouczek OCR
tags:
- OCR
- Python
- Data Extraction
title: Wyodrębnianie tabel z obrazu – Przewodnik OCR krok po kroku
url: /pl/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnianie tabel z obrazu – Kompletny samouczek OCR

Kiedykolwiek potrzebowałeś **wyodrębnić tabele z obrazu**, ale nie wiedziałeś, od czego zacząć? Nie jesteś sam. Wielu programistów napotyka problem, gdy PDF lub zrzut ekranu zawiera dane tabelaryczne, które muszą stać się edytowalnymi wierszami i kolumnami. Dobra wiadomość? Kilka linijek kodu w Pythonie, połączonych z solidnym silnikiem OCR, może zamienić ten obraz w użyteczny arkusz kalkulacyjny w kilka sekund.

W tym samouczku przejdziemy przez ładowanie obrazu do OCR, uruchomienie silnika rozpoznawania oraz wyciąganie każdej tabeli wiersz po wierszu. Po zakończeniu będziesz w stanie **convert image to spreadsheet**, a także zobaczysz, jak **ocr read tables** i **ocr extract table data** do dalszego przetwarzania. Bez ukrytej magii, tylko przejrzysty, działający kod, który możesz od razu wstawić do swojego projektu.

---

## Czego będziesz potrzebować

Zanim zaczniemy, upewnij się, że masz pod ręką:

- **Python 3.9+** – najnowsza stabilna wersja działa najlepiej.  
- Bibliotekę **`ocr`** (lub dowolny kompatybilny SDK OCR, który udostępnia `OcrEngine`, `Image` i metody związane z tabelami). Zainstaluj ją poleceniem `pip install ocr‑sdk` (zastąp rzeczywistą nazwą pakietu).  
- Plik obrazu (`.png`, `.jpg` itp.) zawierający wyraźnie wydrukowaną tabelę.  
- Opcjonalnie: **pandas**, jeśli chcesz od razu zapisać wyodrębnione dane do pliku CSV lub Excel (`pip install pandas`).

Masz wszystko? Świetnie — zaczynamy.

---

## Krok 1: Importowanie SDK OCR i przygotowanie środowiska

Na początek musimy zaimportować klasy OCR do naszego skryptu i skonfigurować mały pomocnik, który później przekształci surowe dane tabeli w DataFrame.

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**Dlaczego to ważne:** Importowanie `ocr` daje dostęp do `OcrEngine`, `Imaging.Image` oraz obiektów tabel, po których będziemy iterować. `pandas` nie jest wymagany do samego wyodrębniania, ale upraszcza część „convert image to spreadsheet”.

---

## Krok 2: Załaduj obraz, który chcesz przetworzyć

Teraz faktycznie **load image for OCR**. SDK oczekuje obiektu `Image`, więc opakujemy ścieżkę do pliku metodą pomocniczą `Image.load()`.

```python
# Step 2 – Load the image that contains a table
image_path = Path("YOUR_DIRECTORY/table_image.png")

# Verify the file exists early to avoid cryptic SDK errors
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Attach the image to the engine
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))
```

**Wskazówka:** Trzymaj pliki obrazów w dedykowanym folderze (`assets/` lub `data/`) i używaj ścieżek względnych. Dzięki temu skrypt będzie przenośny między maszynami.

---

## Krok 3: Uruchom proces rozpoznawania

Mając obraz podłączony, możemy w końcu nakazać silnikowi **ocr read tables**. Wywołanie `recognize()` zwraca obiekt wyniku, który zawiera wszystko, co silnik wykrył — bloki tekstu, linie i, co najważniejsze dla nas, tabele.

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**Dlaczego sprawdzamy:** Niektóre obrazy mogą być zaszumione lub granice tabeli słabe, co powoduje, że silnik ich nie wykryje. Zalogowanie ostrzeżenia daje wczesną informację zwrotną bez przerywania działania skryptu.

---

## Krok 4: Wyodrębnij wiersze i komórki każdej tabeli

Tutaj dzieje się prawdziwa magia. Przejdziemy po każdej wykrytej tabeli, wyciągniemy każdy wiersz, a następnie tekst każdej komórki. Wewnętrzne wyrażenie listowe sprawia, że kod jest zwięzły, ale i tak wyjaśnimy przebieg.

```python
# Step 4 – Iterate over detected tables and collect data
all_tables = []   # Will hold a list of pandas DataFrames

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")

    rows_data = []   # Temporary storage for this table's rows

    for row_obj in table_obj.get_rows():
        # Extract text from each cell in the current row
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    # Convert the raw list of rows into a DataFrame
    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    # Print a human‑readable version to the console
    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))
```

**Co się dzieje?**  

- `enumerate(..., start=1)` podaje przyjazny numer tabeli do logowania.  
- `row_obj.get_cells()` zwraca obiekty komórek; `cell.get_text()` pobiera tekst zdekodowany przez OCR.  
- Przechowujemy wiersze w `rows_data`, a następnie przekazujemy je do `pandas.DataFrame`, który automatycznie dopasowuje kolumny.  
- Blok `print` odzwierciedla **essential output** pokazany w oryginalnym fragmencie, dzięki czemu możesz od razu zweryfikować wyniki.

**Obsługa przypadków brzegowych:** Jeśli wiersz ma inną liczbę komórek niż pozostałe, `pandas` wypełni brakujące miejsca `NaN`. Później możesz wyczyścić DataFrame za pomocą `df.fillna('')`, jeśli wolisz puste ciągi.

---

## Krok 5: Zapisz wyodrębnione tabele do arkusza kalkulacyjnego

Mając listę DataFrames, konwersja ich do skoroszytu Excel (lub plików CSV) to pestka. To spełnia cel „convert image to spreadsheet”.

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**Dlaczego Excel?** Większość użytkowników biznesowych preferuje `.xlsx`. Jeśli wolisz CSV, zamień pętlę na `df.to_csv(f"table_{idx}.csv", index=False)`.

---

## Pełny, gotowy do uruchomienia skrypt

Łącząc wszystko razem, oto kompletny program, który możesz skopiować i uruchomić.

```python
import ocr
from pathlib import Path
import pandas as pd
import logging

logging.basicConfig(level=logging.INFO)

# ---------- Configuration ----------
image_path = Path("YOUR_DIRECTORY/table_image.png")
output_path = Path("extracted_tables.xlsx")
# ----------------------------------

# Verify image exists
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Initialize OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))

# Run recognition
ocr_result = ocr_engine.recognize()

if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
    exit(0)

all_tables = []

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")
    rows_data = []

    for row_obj in table_obj.get_rows():
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))

# Save to Excel
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        df.to_excel(writer, sheet_name=f"Table_{idx}", index=False)

logging.info(f"All tables saved to {output_path}")
```

**Oczekiwany wynik w konsoli** (przy prostej tabeli 2×3):

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

A w folderze skryptu znajdziesz plik `extracted_tables.xlsx`, każda tabela na osobnym arkuszu.

---

## Najczęściej zadawane pytania i wskazówki

| Pytanie | Odpowiedź |
|----------|--------|
| **Czy mogę użyć innej biblioteki OCR?** | Oczywiście. Schemat pozostaje ten sam: load image → recognize → iterate over `get_tables()`. Wystarczy zamienić import i nazwy obiektów. |
| **Co zrobić, gdy mój obraz jest zaszumiony?** | Wstępnie przetwórz go w OpenCV (progowanie, prostowanie) przed przekazaniem do silnika OCR. Redukcja szumu często poprawia dokładność **ocr extract table data**. |
| **Czy muszę instalować `openpyxl`?** | Tak, `pandas` używa go w tle do zapisu Excela. Zainstaluj poleceniem `pip install openpyxl`. |
| **Jak obsłużyć scalone komórki?** | Niektóre SDK udostępniają `cell.is_merged()`; możesz wykrywać i ręcznie propagować wartość na cały zakres scalony. |
| **Czy istnieje sposób na wyodrębnienie tylko wybranych tabel?** | Filtruj po `table_obj.get_confidence()` lub sprawdzaj słowa kluczowe w nagłówkach przed przetworzeniem. |

---

## Podsumowanie

Masz teraz kompletną, end‑to‑end rozwiązanie do **extract tables from image**, konwersji wyniku do schludnego arkusza kalkulacyjnego oraz obsługi wielu tabel na jednym obrazie. Skrypt pokazuje, jak **load image for OCR**, **ocr read tables** i **ocr extract table data**, pozostając jednocześnie elastycznym wobec rzeczywistych wariantów.

Co dalej? Spróbuj podać silnikowi OCR stronę PDF przetworzoną na obraz, lub eksperymentuj z różnymi językami i czcionkami. Możesz także przesłać DataFrames bezpośrednio do bazy danych lub narzędzia raportowego — jedynym ograniczeniem jest Twoja wyobraźnia.

Jeśli ten przewodnik okazał się pomocny, podziel się nim, dodaj gwiazdkę do repozytorium, które hostuje SDK, lub zostaw komentarz z własnymi trikami. Szczęśliwego kodowania i niech Twoje tabele zawsze będą perfekcyjnie parsowane!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}