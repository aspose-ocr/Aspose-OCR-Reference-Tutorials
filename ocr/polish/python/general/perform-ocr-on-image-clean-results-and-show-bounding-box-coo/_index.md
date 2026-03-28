---
category: general
date: 2026-03-28
description: Wykonaj OCR na obrazie i uzyskaj czysty tekst z współrzędnymi prostokątów
  ograniczających. Dowiedz się, jak wyodrębnić OCR, oczyścić OCR i wyświetlić wyniki
  krok po kroku.
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: pl
og_description: Wykonaj OCR na obrazie, oczyść wynik i wyświetl współrzędne ramki
  ograniczającej w zwięzłym samouczku.
og_title: Wykonaj OCR na obrazie – czyste wyniki i ramki ograniczające
tags:
- OCR
- Computer Vision
- Python
title: Wykonaj OCR na obrazie – czyste wyniki i wyświetl współrzędne ramki ograniczającej
url: /pl/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wykonaj OCR na obrazie – Oczyść wyniki i pokaż współrzędne prostokątów ograniczających

Czy kiedykolwiek musiałeś **wykonać OCR na plikach obrazu**, ale otrzymywałeś nieuporządkowany tekst i nie wiedziałeś, gdzie każde słowo znajduje się na zdjęciu? Nie jesteś sam. W wielu projektach — digitalizacja faktur, skanowanie paragonów czy proste wyodrębnianie tekstu — surowy wynik OCR to dopiero pierwszy krok. Dobra wiadomość? Możesz oczyścić ten wynik i natychmiast zobaczyć współrzędne prostokątów ograniczających każdą sekcję, nie pisząc mnóstwa kodu szablonowego.

W tym przewodniku przejdziemy przez **wyodrębnianie OCR**, uruchomienie **post‑procesora czyszczenia OCR** oraz w końcu **wyświetlenie współrzędnych prostokątów ograniczających** dla każdego oczyszczonego regionu. Po zakończeniu będziesz mieć pojedynczy, gotowy do uruchomienia skrypt, który zamieni rozmyte zdjęcie w uporządkowany, strukturalny tekst gotowy do dalszego przetwarzania.

## Czego będziesz potrzebować

- Python 3.9+ (składnia poniżej działa na 3.8 i nowszych)
- Silnik OCR obsługujący `recognize(..., return_structured=True)` – na przykład fikcyjna biblioteka `engine` użyta w przykładzie. Zamień ją na Tesseract, EasyOCR lub dowolne SDK zwracające dane o regionach.
- Podstawowa znajomość funkcji i pętli w Pythonie
- Plik obrazu, który chcesz zeskanować (PNG, JPG, itp.)

> **Pro tip:** Jeśli używasz Tesseract, funkcja `pytesseract.image_to_data` już zwraca prostokąty ograniczające. Możesz opakować jej wynik w mały adapter, który naśladuje API `engine.recognize` pokazane poniżej.

---

![perform OCR on image example](image-placeholder.png "perform OCR on image example")

*Alt text: diagram pokazujący, jak wykonać OCR na obrazie i zwizualizować współrzędne prostokątów ograniczających*

## Krok 1 – Wykonaj OCR na obrazie i uzyskaj strukturalne regiony

Pierwszym krokiem jest poproszenie silnika OCR o zwrócenie nie tylko zwykłego tekstu, ale także strukturalnej listy regionów tekstowych. Lista ta zawiera surowy ciąg znaków oraz prostokąt, który go otacza.

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**Dlaczego to ważne:**  
Gdy żądasz jedynie zwykłego tekstu, tracisz kontekst przestrzenny. Strukturalne dane pozwalają później **wyświetlić współrzędne prostokątów ograniczających**, dopasować tekst do tabel lub przekazać precyzyjne położenie do kolejnego modelu.

## Krok 2 – Jak oczyścić wynik OCR przy użyciu post‑procesora

Silniki OCR świetnie rozpoznają znaki, ale często pozostawiają zbędne spacje, artefakty podziału linii lub błędnie rozpoznane symbole. Post‑procesor normalizuje tekst, naprawia typowe błędy OCR i usuwa nadmiarowe białe znaki.

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

Jeśli tworzysz własny czyszczacz, rozważ:

- Usuwanie znaków nie‑ASCII (`re.sub(r'[^\x00-\x7F]+',' ', text)`)
- Zastępowanie wielu spacji jedną
- Użycie sprawdzania pisowni, np. `pyspellchecker`, aby naprawić oczywiste literówki

**Dlaczego warto się tym przejmować:**  
Uporządkowany ciąg znaków sprawia, że wyszukiwanie, indeksowanie i dalsze pipeline’y NLP są znacznie bardziej niezawodne. Innymi słowy, **jak oczyścić OCR** to często różnica między użytecznym zestawem danych a koszmarem.

## Krok 3 – Wyświetl współrzędne prostokątów ograniczających dla każdego oczyszczonego regionu

Teraz, gdy tekst jest czysty, iterujemy po każdym regionie, wypisując jego prostokąt i oczyszczony ciąg znaków. To właśnie w tym miejscu **wyświetlamy współrzędne prostokątów ograniczających**.

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**Przykładowy wynik**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

Możesz teraz przekazać te współrzędne do biblioteki rysującej (np. OpenCV), aby nałożyć prostokąty na oryginalny obraz, lub zapisać je w bazie danych do późniejszych zapytań.

## Pełny, gotowy do uruchomienia skrypt

Poniżej znajduje się kompletny program, który łączy wszystkie trzy kroki. Zamień wywołania `engine` na rzeczywiste wywołania Twojego SDK OCR.

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### Jak uruchomić

```bash
python perform_ocr.py sample_invoice.jpg
```

Powinieneś zobaczyć listę prostokątów ograniczających sparowanych z oczyszczonym tekstem, dokładnie taką jak w przykładowym wyniku powyżej.

## Najczęściej zadawane pytania i przypadki brzegowe

| Pytanie | Odpowiedź |
|----------|--------|
| **Co zrobić, jeśli silnik OCR nie obsługuje `return_structured`?** | Napisz cienki wrapper, który przekształci surowy wynik silnika (zwykle listę słów z koordynatami) w obiekty z atrybutami `text` i `bounding_box`. |
| **Czy mogę uzyskać wyniki wiarygodności (confidence)?** | Wiele SDK udostępnia metrykę wiarygodności dla każdego regionu. Dodaj ją do instrukcji drukowania: `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`. |
| **Jak obsłużyć tekst obrócony?** | Przetwórz obraz wstępnie przy użyciu `cv2.minAreaRect` z OpenCV, aby wyrównać go przed wywołaniem `recognize`. |
| **Co jeśli potrzebuję wyniku w formacie JSON?** | Serializuj `processed_result.regions` przy pomocy `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)`. |
| **Czy istnieje sposób na wizualizację prostokątów?** | Użyj OpenCV: `cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)` wewnątrz pętli, a potem `cv2.imwrite("annotated.jpg", img)`. |

## Podsumowanie

Właśnie nauczyłeś się **wykonywać OCR na obrazie**, czyścić surowy wynik i **wyświetlać współrzędne prostokątów ograniczających** dla każdego regionu. Trójstopniowy przepływ — rozpoznawanie → post‑procesowanie → iteracja — to wzorzec, który możesz wstawić do dowolnego projektu Pythona wymagającego niezawodnego wyodrębniania tekstu.

### Co dalej?

- **Eksploruj różne backendy OCR** (Tesseract, EasyOCR, Google Vision) i porównaj ich dokładność.
- **Zintegruj z bazą danych**, aby przechowywać dane regionów dla przeszukiwalnych archiwów.
- **Dodaj wykrywanie języka**, aby kierować każdy region do odpowiedniego sprawdzania pisowni.
- **Nałóż prostokąty na oryginalny obraz** w celu wizualnej weryfikacji (zobacz fragment OpenCV powyżej).

Jeśli napotkasz problemy, pamiętaj, że największy zysk pochodzi z solidnego kroku post‑procesowania; czysty ciąg znaków jest znacznie łatwiejszy do pracy niż surowy zlepek znaków.

Miłego kodowania i niech Twoje pipeline’y OCR będą zawsze schludne!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}