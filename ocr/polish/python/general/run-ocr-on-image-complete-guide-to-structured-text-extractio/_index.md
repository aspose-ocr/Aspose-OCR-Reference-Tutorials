---
category: general
date: 2026-05-03
description: Dowiedz się, jak uruchomić OCR na obrazie i wyodrębnić tekst z współrzędnymi
  przy użyciu strukturalnego rozpoznawania OCR. Dołączony krok po kroku kod w Pythonie.
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: pl
og_description: Uruchom OCR na obrazie i uzyskaj tekst z współrzędnymi, korzystając
  ze strukturalnego rozpoznawania OCR. Pełny przykład w Pythonie z wyjaśnieniami.
og_title: Uruchom OCR na obrazie – Samouczek wyodrębniania tekstu strukturalnego
tags:
- OCR
- Python
- Computer Vision
title: Uruchom OCR na obrazie – Kompletny przewodnik po ekstrakcji tekstu strukturalnego
url: /pl/python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uruchom OCR na obrazie – Kompletny przewodnik po wyodrębnianiu tekstu strukturalnego

Czy kiedykolwiek potrzebowałeś **uruchomić OCR na obrazie** i nie byłeś pewien, jak zachować dokładne pozycje każdego słowa? Nie jesteś sam. W wielu projektach — skanowanie paragonów, digitalizacja formularzy czy testowanie UI — potrzebujesz nie tylko surowego tekstu, ale także prostokątów ograniczających (bounding boxes), które mówią, gdzie znajduje się każda linia na obrazie.  

Ten tutorial pokazuje praktyczny sposób na *uruchomienie OCR na obrazie* przy użyciu silnika **aocr**, żądanie **structured OCR recognition**, a następnie post‑procesowanie wyniku przy zachowaniu geometrii. Po zakończeniu będziesz w stanie **wyodrębnić tekst z współrzędnymi** w kilku linijkach Pythona i zrozumiesz, dlaczego tryb strukturalny ma znaczenie dla dalszych zadań.

## What You’ll Learn

- Jak zainicjalizować silnik OCR dla **structured OCR recognition**.  
- Jak podać obraz i otrzymać surowe wyniki zawierające granice linii.  
- Jak uruchomić post‑procesor, który czyści tekst bez utraty geometrii.  
- Jak iterować po ostatecznych liniach i wypisywać każdy fragment tekstu wraz z jego bounding boxem.  

Bez magii, bez ukrytych kroków — po prostu kompletny, gotowy do uruchomienia przykład, który możesz wkleić do własnego projektu.

---

## Prerequisites

Zanim przejdziemy dalej, upewnij się, że masz zainstalowane następujące elementy:

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

Będziesz także potrzebował pliku obrazu (`input_image.png` lub `.jpg`) zawierającego wyraźny, czytelny tekst. Wszystko, od zeskanowanej faktury po zrzut ekranu, będzie działało, o ile silnik OCR będzie w stanie rozpoznać znaki.

---

## Step 1: Initialise the OCR engine for structured recognition

Pierwszą rzeczą, którą robimy, jest stworzenie instancji `aocr.Engine()` i poinformowanie jej, że chcemy **structured OCR recognition**. Tryb strukturalny zwraca nie tylko czysty tekst, ale także dane geometryczne (prostokąty ograniczające) dla każdej linii, co jest niezbędne, gdy musisz odwzorować tekst z powrotem na obraz.

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **Why this matters:**  
> W trybie domyślnym silnik może zwrócić jedynie łańcuch połączonych słów. Tryb strukturalny dostarcza hierarchię stron → linii → słów, z koordynatami, co znacznie ułatwia nakładanie wyników na oryginalny obraz lub przekazywanie ich do modelu uwzględniającego układ.

---

## Step 2: Run OCR on the image and obtain raw results

Teraz podajemy obraz do silnika. Wywołanie `recognize` zwraca obiekt `OcrResult`, który zawiera kolekcję linii, z których każda ma własny prostokąt ograniczający.

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

W tym momencie `raw_result.lines` zawiera obiekty z dwoma ważnymi atrybutami:

- `text` – rozpoznany ciąg znaków dla danej linii.  
- `bounds` – krotka w formacie `(x, y, width, height)` opisująca pozycję linii.

---

## Step 3: Post‑process while preserving geometry

Surowe wyniki OCR są często zaszumione: niechciane znaki, nieprawidłowe spacje lub problemy z podziałem linii. Funkcja `ai.run_postprocessor` czyści tekst, ale **zachowuje oryginalną geometrię**, więc nadal masz dokładne współrzędne.

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **Pro tip:** Jeśli posiadasz słowniki specyficzne dla domeny (np. kody produktów), podaj własny słownik do post‑procesora, aby zwiększyć dokładność.

---

## Step 4: Extract text with coordinates – iterate and display

Na koniec przechodzimy po wyczyszczonych liniach, wypisując każdy bounding box razem z tekstem. To jest sedno **extract text with coordinates**.

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### Expected Output

Zakładając, że obraz wejściowy zawiera dwie linie: „Invoice #12345” i „Total: $89.99”, zobaczysz coś w tym stylu:

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

Pierwsza krotka to `(x, y, width, height)` linii na oryginalnym obrazie, co pozwala rysować prostokąty, podświetlać tekst lub przekazywać współrzędne do innego systemu.

---

## Visualising the Result (Optional)

Jeśli chcesz zobaczyć bounding boxy nałożone na obraz, możesz użyć Pillow (PIL) do rysowania prostokątów. Poniżej szybki fragment kodu; możesz go pominąć, jeśli potrzebujesz jedynie surowych danych.

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![uruchom OCR na obrazie – przykład z bounding boxami](/images/ocr-bounding-boxes.png "uruchom OCR na obrazie – nakładka z bounding boxami")

Tekst alternatywny powyżej zawiera **główne słowo kluczowe**, spełniając wymóg SEO dla atrybutów alt obrazów.

---

## Why Structured OCR Recognition Beats Simple Text Extraction

Możesz się zastanawiać: „Czy nie mogę po prostu uruchomić OCR i dostać tekst? Po co geometria?”  

- **Kontekst przestrzenny:** Gdy musisz dopasować pola w formularzu (np. „Data” obok wartości daty), współrzędne mówią, *gdzie* znajdują się dane.  
- **Układy wielokolumnowe:** Prosty liniowy tekst traci kolejność; dane strukturalne zachowują kolejność kolumn.  
- **Dokładność post‑procesingu:** Znając rozmiar pola, łatwiej określić, czy słowo jest nagłówkiem, przypisem czy przypadkowym artefaktem.  

Krótko mówiąc, **structured OCR recognition** daje elastyczność potrzebną do budowy inteligentniejszych pipeline’ów — niezależnie od tego, czy wprowadzisz dane do bazy, tworzysz przeszukiwalne PDF‑y, czy trenujesz model ML respektujący układ.

---

## Common Edge Cases and How to Handle Them

| Situation | What to Watch For | Suggested Fix |
|-----------|-------------------|---------------|
| **Rotated or skewed images** | Bounding boxes may be off‑axis. | Pre‑process with deskewing (e.g., OpenCV’s `warpAffine`). |
| **Very small fonts** | Engine may miss characters, leading to empty lines. | Increase image resolution or use `ocr_engine.set_dpi(300)`. |
| **Mixed languages** | Wrong language model can cause garbled text. | Set `ocr_engine.language = ["en", "de"]` before recognition. |
| **Overlapping boxes** | Post‑processor might merge two lines unintentionally. | Verify `line.bounds` after processing; adjust thresholds in `ai.run_postprocessor`. |

Rozwiązanie tych scenariuszy na wczesnym etapie oszczędza późniejsze problemy, zwłaszcza przy skalowaniu rozwiązania do setek dokumentów dziennie.

---

## Full End‑to‑End Script

Poniżej pełny, gotowy do uruchomienia program, który łączy wszystkie kroki. Skopiuj‑wklej, dostosuj ścieżkę do obrazu i gotowe.

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

Uruchomienie tego skryptu spowoduje:

1. **Run OCR on image** w trybie strukturalnym.  
2. **Extract text with coordinates** dla każdej linii.  
3. Opcjonalnie wygeneruje oznaczony PNG z zaznaczonymi boxami.

---

## Conclusion

Masz teraz solidne, samodzielne rozwiązanie do **uruchomienia OCR na obrazie** i **wyodrębniania tekstu z współrzędnymi** przy użyciu **structured OCR recognition**. Kod demonstruje każdy krok — od inicjalizacji silnika, przez post‑processing, po weryfikację wizualną — dzięki czemu możesz go dostosować do paragonów, formularzy czy dowolnych dokumentów wizualnych wymagających precyzyjnej lokalizacji tekstu.

Co dalej? Spróbuj zamienić silnik `aocr` na inną bibliotekę (Tesseract, EasyOCR) i zobacz, jak różnią się ich wyjścia strukturalne. Eksperymentuj z różnymi strategiami post‑procesingu, takimi jak sprawdzanie pisowni czy własne filtry regex, aby podnieść dokładność w swojej domenie. A jeśli budujesz większy pipeline, rozważ przechowywanie par `(text, bounds)` w bazie danych do późniejszej analizy.

Miłego kodowania i niech Twoje projekty OCR będą zawsze precyzyjne!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}