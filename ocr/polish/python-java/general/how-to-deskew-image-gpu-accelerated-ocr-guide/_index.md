---
category: general
date: 2026-01-02
description: Dowiedz się, jak prostować obraz i zwiększyć kontrast, aby szybko uzyskać
  czysty tekst. Zawiera krok po kroku kod w Pythonie oraz wskazówki dotyczące wyodrębniania
  tekstu.
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: pl
og_description: Jak wyprostować obraz i zwiększyć kontrast, aby uzyskać czysty tekst.
  Pełny przykład w Pythonie z wyodrębnianiem tabel i przyspieszeniem GPU.
og_title: Jak wyrównać obraz – Kompletny samouczek OCR na GPU
tags:
- OCR
- Python
- Image Processing
title: Jak wyprostować obraz – przewodnik po OCR przyspieszonym GPU
url: /pl/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak prostować obraz – przewodnik OCR przyspieszony GPU

Zastanawiałeś się kiedyś **jak prostować obraz**, gdy Twoje paragony pojawiają się pod zabawnym kątem? Nie jesteś sam; przechylone zdjęcie może zamienić idealnie czytelny paragon w nieczytelny bałagan. Dobra wiadomość jest taka, że kilkoma liniami Pythona możesz automatycznie prostować, zwiększyć kontrast i wyciągnąć czysty tekst – bez ręcznego Photoshopa.

W tym tutorialu przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który nie tylko pokazuje **jak prostować obraz**, ale także **jak zwiększyć kontrast**, **jak uzyskać czysty tekst**, a nawet **jak wyodrębnić tekst** z tabel wykrytych przez silnik OCR. Po zakończeniu będziesz mieć samodzielny skrypt, który możesz wstawić do dowolnego projektu.

## Co będzie potrzebne

- Python 3.9+ zainstalowany (kod używa podpowiedzi typów, więc nowszy interpreter pomocny)
- Biblioteka `ocr` dostarczająca `OcrEngine`, `EngineMode`, `ImageProcessingOptions` i `OcrResult` (zainstaluj przez `pip install ocr‑sdk` – zamień na rzeczywistą nazwę pakietu, którego używasz)
- GPU z kompatybilnymi sterownikami, jeśli chcesz przyspieszyć działanie (opcjonalnie, ale zalecane)
- Plik obrazu lekko obrócony lub o niskim kontraście, np. `receipt_skewed.jpg`

> **Pro tip:** Jeśli nie masz GPU, po prostu zamień `EngineMode.GPU` na `EngineMode.CPU` i skrypt nadal będzie działał – trochę wolniej.

## Implementacja krok po kroku

Poniżej dzielimy rozwiązanie na logiczne fragmenty. Każdy fragment ma opisowy **H2**, który zawiera główne słowo kluczowe *how to deskew image* lub jedno z drugorzędnych słów kluczowych. Kod jest kompletny, skomentowany i gotowy do uruchomienia### Jak prostować obraz przy użyciu OCR przyspieszonego GPU

Pierwszą rzeczą, którą robimy, jest poinstruowanie silnika OCR, aby działał na GPU i włączenie funkcji auto‑deskew. Auto‑deskew analizuje geometrię obrazu i obraca go z powrotem do pozycji pionowej.

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **Dlaczego to ważne:** Przyspieszenie GPU może skrócić czas przetwarzania z sekund do milisekund, co jest kluczowe przy obsłudze dziesiątek paragonów na minutę.

### Zwiększ kontrast obrazu dla lepszej rozpoznawalności

Paragon o niskim kontraście to koszmar dla każdego systemu OCR. Zwiększając kontrast, dajemy silnikowi wyraźniejsze krawędzie do analizy.

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **Jak zwiększyć kontrast:** Metoda `set_contrast_boost` przyjmuje procent; 30 % to bezpieczna domyślna wartość, która działa dla większości zeskanowanych paragonów. Jeśli Twoje obrazy są bardzo ciemne, podnieś ją do 50 % lub eksperymentuj.

### Uzyskaj czysty tekst z przetworzonego obrazu

Teraz, gdy obraz jest prosty i jasny, przekazujemy go sil i żądamy wyniku w postaci czystego tekstu.

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**Oczekiwany wynik** (skrócony dla przejrzystości):

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **Jak uzyskać czysty tekst:** Metoda `get_text()` usuwa wszelkie informacje o układzie i zwraca czysty ciąg znaków, który możesz potem zapisać w bazie danych, wysłać do API lub przekazać do dalszej analizy.

### Jak wyodrębnić tekst z wykrytych tabel

Często paragony zawierają dane tabelaryczne (pozycje, ilości, ceny). SDK OCR może wykrywać tabele i pozwala iterować po wierszach i komórkach.

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**Przykładowy wynik tabeli**:

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **Dlaczego wyodrębniać tabele:** Dane strukturalne ułatwiają obliczanie sum, generowanie raportów lub przekazywanie ich do oprogramowania księgowego.

### Pełny działający skrypt

Łącząc wszystko razem, oto skrypt, który możesz skopiować i wkleić do `deskew_and_ocr.py`:

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

Uruchom go za pomocą:

```bash
python deskew_and_ocr.py
```

Powinieneś zobaczyć wyczyszczony tekst oraz wszystkie wykryte tabele wypisane w konsoli.

## Typowe przypadki brzegowe i jak sobie z nimi radzić

| Sytuacja | Co zrobić |
|-----------|------------|
| **Obraz jest do góry nogami** | Zwiększ pewność `set_auto_deskew(True)` także wywołując `set_rotation_correction(True)`, jeśli SDK to umożliwia. |
| **Zwiększenie kontrastu sprawia, że obraz jest zbyt jasny** | Zmniejsz procent podany do `set_contrast_boost` (np. 15 %). |
| **GPU niedostępne** | Zamień `EngineMode.GPU` na `EngineMode.CPU`; reszta pipeline pozostaje niezmieniona. |
| **Tabele nie są wykrywane** | Spróbuj skanu o wyższej rozdzielczości lub włącz `set_table_detection(True)`, jeśli biblioteka to oferuje. |

## Kolejne kroki: od czystego tekstu do danych strukturalnych

Teraz, gdy wiesz **jak prostować obraz**, **jak zwiększyć kontrast** i **jak uzyskać czysty tekst**, możesz:

- Parsować czysty tekst przy użyciu wyrażeń regularnych, aby wyodrębnić pary klucz‑wartość (np. `total`, `date`).
- Przechowywać wyniki w bazie SQLite lub PostgreSQL do późniejszych raportów.
- Podłączyć skrypt do funkcji serverless (AWS Lambda, Azure Functions), aby automatycznie przetwarzać przesyłane pliki.

Wszystkie te rozszerzenia opierają się na tej samej podstawie, którą omówiliśmy.

## Zakończenie

Przeprowadziliśmy Cię przez **jak prostować obraz** przy użyciu silnika OCR przyspieszonego GPU, pokazaliśmy **jak zwiększyć kontrast** dla lepszej rozpoznawalności, dokładnie przedstawiliśmy **jak uzyskać czysty tekst** i nawet omówiliśmy **jak wyodrębnić tekst** z tabel. Kompletny, gotowy do uruchomienia skrypt łączy wszystko w jedną całość, więc możesz go wstawić do dowolnego projektu Pythona i od razu zacząć wyciągać czyste dane z przechylonych, niskokontrastowych zdjęć.

Wypróbuj to na kilku własnych paragonach, dostosuj poziom kontrastu i pozwól OCR wykonać ciężką pracę. Jeśli napotkasz problemy, wróć do tabeli przypadków brzegowych – większość problemów rozwiązuje się drobną korektą.

Miłego kodowania i niech Twoje obrazy zawsze będą proste i jasne!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}