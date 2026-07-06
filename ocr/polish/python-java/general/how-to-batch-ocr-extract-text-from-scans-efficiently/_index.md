---
category: general
date: 2026-04-26
description: Jak przetwarzać dokumenty wsadowo przy użyciu OCR i wyodrębniać tekst
  ze skanów w Pythonie. Naucz się krok po kroku przetwarzania wsadowego z OcrEngine,
  aby uzyskać wynik w formacie JSON.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: pl
og_description: Jak przetwarzać wsadowo OCR swoich zeskanowanych plików i wyodrębniać
  tekst ze skanów w jednym skrypcie. Pełny kod, wskazówki i obsługa przypadków brzegowych.
og_title: Jak wykonywać OCR wsadowo – szybki przewodnik Pythona
tags:
- OCR
- Python
- Automation
title: Jak wykonywać OCR wsadowo – Efektywne wyodrębnianie tekstu ze skanów
url: /pl/python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonać batch OCR – Efektywne wyodrębnianie tekstu ze skanów

Zastanawiałeś się kiedyś **how to batch OCR** góry zeskanowanych PDF‑ów bez utraty zdrowia? Nie jesteś sam — programiści ciągle pytają: *„Jak mogę wyodrębnić tekst ze skanów w jednym kroku?”* Dobra wiadomość jest taka, że kilka linijek Pythona może zamienić tę żmudną czynność w płynną, zautomatyzowaną pipeline.

W tym tutorialu przejdziemy krok po kroku przez kompletną, gotową do uruchomienia rozwiązanie, które **wyodrębnia tekst ze skanów**, zapisuje wyniki jako JSON i daje szybki kontrolny podgląd na końcu. Bez zewnętrznych usług, bez magii — tylko czysty Python, klasa `OcrEngine` i odrobina obsługi folderów.

## Co zyskasz po przeczytaniu

- W pełni funkcjonalny skrypt, który **batches OCR** nad dowolnym folderem obrazów.  
- Jasne wyjaśnienia *dlaczego* każda linijka istnieje, nie tylko *co* robi.  
- Wskazówki dotyczące obsługi pustych folderów, plików nie‑obrazowych i dużych partii.  
- Sposób na weryfikację, że wyjściowy JSON faktycznie zawiera wyodrębniony tekst.

### Wymagania wstępne (minimum)

| Wymaganie | Dlaczego to ważne |
|-----------|-------------------|
| Python 3.8+ | Nowoczesna składnia i podpowiedzi typów |
| `OcrEngine` library (or a compatible wrapper) | Główna funkcjonalność OCR |
| Katalog z zeskanowanymi plikami obrazów (PNG, JPG, TIFF) | Dane wejściowe |
| Uprawnienia do zapisu w folderze wyjściowym | Zapis wyników JSON |

Jeśli już masz to wszystko, świetnie — zanurzmy się.

![how to batch OCR workflow](image-placeholder.png){alt="jak wykonać batch OCR"}

## Krok 1 – Inicjalizacja silnika OCR (how to batch OCR)

Zanim będziemy mogli coś przetworzyć, potrzebujemy instancji silnika OCR. To „mózg”, który odczyta każdy obraz i zwróci tekst. Inicjalizacja go raz i ponowne użycie w całej partii to najefektywniejszy wzorzec.

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **Dlaczego warto używać tej samej instancji?**  
> Tworzenie nowego silnika dla każdego pliku powodowałoby wielokrotne ładowanie ciężkich modeli do pamięci, co dramatycznie spowalnia batch. Jedna instancja utrzymuje model w RAM i pozwala przetworzyć tysiące obrazów bez zauważalnego spowolnienia.

## Krok 2 – Wskazanie folderu ze skanami (extract text from scans)

Twoje skany znajdują się gdzieś na dysku. Powiedzmy skryptowi, gdzie ich szukać. Użycie ścieżek bezwzględnych eliminuje niespodzianki typu „plik nie znaleziony”, gdy skrypt uruchomiony jest z innego katalogu roboczego.

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **Pro tip:**  
> Jeśli pracujesz w Windows, ukośniki (`/`) działają bez problemu z `os.path.abspath`, więc nie musisz uciekać backslashy.

## Krok 3 – Wybór miejsca na wyniki JSON

Prawdopodobnie chcesz mieć uporządkowany folder na wyniki OCR. Trzymanie wyjścia oddzielnie od źródła ułatwia późniejsze czyszczenie lub podanie JSON‑a do kolejnej pipeline.

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **Dlaczego tworzyć folder programowo?**  
> Gwarantuje to, że skrypt nie wykrzyknie błędu, jeśli katalog nie istnieje, a `exist_ok=True` sprawia, że operacja jest idempotentna — możesz uruchamiać skrypt wiele razy bez błędów.

## Krok 4 – Uruchomienie procesu batch (how to batch OCR)

Teraz serce sprawy: nakazujemy `ocr_engine` przejść przez każdy plik w `input_dir`, wykonać OCR i zapisać JSON w `output_dir`. Flaga `format="json"` mówi silnikowi, aby zserializował wynik w ustrukturyzowany sposób, który uwielbiają downstreamowe narzędzia.

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### Co się dzieje pod maską?

1. **Odkrywanie plików** – Silnik skanuje `input_folder` rekurencyjnie, pomijając ukryte pliki.  
2. **Walidacja plików** – Do modelu OCR trafiają tylko obsługiwane rozszerzenia obrazów (`.png`, `.jpg`, `.tif` itp.).  
3. **Wykonanie OCR** – Każdy obraz jest przekazywany do silnika OCR; tekst, współczynniki pewności i dane układu są zbierane.  
4. **Serializacja JSON** – Wynik zapisywany jest do pliku o tej samej nazwie bazowej, ale z rozszerzeniem `.json` w `output_folder`.

> **Obsługa przypadków brzegowych:**  
> - **Pusty folder:** Silnik loguje „No files found” i kończy działanie łagodnie.  
> - **Uszkodzony obraz:** Pomija plik, zapisuje wpis błędu w `batch_errors.log` i kontynuuje.  
> - **Ogromny batch (10 k+ plików):** Zużycie pamięci pozostaje niskie, ponieważ każdy obraz jest przetwarzany niezależnie.

## Krok 5 – Potwierdzenie zakończenia konwersji

Prosta instrukcja `print` daje natychmiastowy feedback w konsoli. W produkcyjnych pipeline’ach możesz zamienić ją na wywołanie loggera lub powiadomienie e‑mailowe.

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

Gdy zobaczysz tę linię, możesz bezpiecznie przyjrzeć się folderowi `json_output`. Każdy plik JSON będzie wyglądał mniej‑więcej tak:

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

Teraz możesz podać te pliki JSON do bazy danych, indeksu wyszukiwania lub dowolnego narzędzia analitycznego.

## Najczęściej zadawane pytania (i szybkie odpowiedzi)

**Q: Co zrobić, jeśli muszę przetwarzać PDF‑y zamiast obrazów?**  
A: Najpierw skonwertuj każdą stronę PDF‑a na obraz (np. przy użyciu `pdf2image`) i umieść powstałe pliki PNG/JPG w `input_dir`. Logika batch OCR pozostaje niezmieniona.

**Q: Czy mogę zmienić format wyjścia na zwykły tekst?**  
A: Oczywiście. Zamień `format="json"` na `format="txt"` i silnik zapisze plik `.txt` zawierający wyłącznie wyodrębniony tekst.

**Q: Moje skany są w wielu podfolderach — czy skrypt będzie rekurencyjny?**  
A: Tak. `batch_process` domyślnie przechodzi drzewo katalogów. Jeśli potrzebujesz płaskiego wyjścia, ustaw `flatten=True` (jeśli biblioteka to obsługuje) lub po‑procesuj nazwy plików JSON.

**Q: Jak obsłużyć skrypty nie‑łacińskie?**  
A: Zainicjalizuj `OcrEngine` z parametrem językowym, np. `OcrEngine(lang="spa+eng")`. Pętla batch nie wymaga żadnych zmian.

## Pro Tips & Common Pitfalls

- **Rozmiar batcha ma znaczenie:** Jeśli zauważysz skoki CPU, wstaw prostą `time.sleep(0.1)` pomiędzy plikami.  
- **Logowanie:** Zamień wywołanie `print` na moduł `logging` w Pythonie, aby uchwycić znaczniki czasu i poziomy błędów.  
- **Kolizje nazw plików:** Jeśli dwa skany mają tę samą nazwę bazową, ale znajdują się w różnych podfolderach, pliki JSON nadpiszą się. Dodaj hash względnej ścieżki do nazwy wyjściowej, aby tego uniknąć.  
- **Wycieki pamięci:** Niektóre backendy OCR trzymają natywne zasoby. Wywołaj `ocr_engine.close()` na końcu skryptu, jeśli biblioteka udostępnia metodę czyszczenia.

## Pełny skrypt – Gotowy do kopiowania i wklejenia

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**Oczekiwany output w konsoli**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

Możesz zweryfikować JSON, otwierając dowolny plik w `json_output` w edytorze tekstu lub wczytując go w Pythonie:

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

Powinieneś zobaczyć surowy tekst wyodrębniony przez OCR wypisany w konsoli.

## Podsumowanie

Właśnie omówiliśmy **how to batch OCR** całego katalogu zeskanowanych obrazów i **extract text from scans** do czystych, maszynowo czytelnych plików JSON. Podejście jest celowo proste: skonfiguruj silnik raz, wskaż folder i pozwól bibliotece wykonać ciężką pracę. Stąd możesz:

- Podłączyć JSON

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}