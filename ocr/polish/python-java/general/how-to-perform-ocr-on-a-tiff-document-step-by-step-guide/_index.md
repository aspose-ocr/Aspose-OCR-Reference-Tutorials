---
category: general
date: 2026-01-12
description: Jak szybko i dokładnie przeprowadzić OCR. Dowiedz się, jak uruchomić
  OCR na dokumencie, wyodrębnić tekst z pliku TIFF, załadować obraz do OCR i ustawić
  język OCR w Pythonie.
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: pl
og_description: Jak wykonać OCR w Pythonie. Ten samouczek pokazuje, jak uruchomić
  OCR na dokumencie, wyodrębnić tekst z pliku TIFF, załadować obraz do OCR i ustawić
  język OCR.
og_title: Jak wykonać OCR w dokumencie TIFF – Kompletny przewodnik
tags:
- OCR
- Python
- Image Processing
title: Jak wykonać OCR w dokumencie TIFF – Przewodnik krok po kroku
url: /pl/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonać OCR na dokumencie TIFF – Kompletny przewodnik

Zastanawiałeś się kiedyś **jak wykonać OCR** na zeskanowanym pliku TIFF, nie tracąc godzin na szukanie odpowiedniej biblioteki? Nie jesteś sam. Wielu programistów napotyka problem, gdy muszą wyodrębnić tekst z obrazów TIFF, szczególnie gdy liczy się wydajność i ustawienia językowe.

W tym tutorialu przejdziemy krok po kroku przez wszystko, co musisz wiedzieć: od instalacji pakietu OCR, przez wczytanie obrazu do OCR, ustawienie języka OCR, aż po **uruchomienie OCR na dokumencie** i uzyskanie czystego tekstu. Na końcu będziesz mieć gotowy skrypt, który możesz wkleić do dowolnego projektu.

> **Pro tip:** Choć w przykładzie używany jest ogólny moduł `ocr`, te same koncepcje mają zastosowanie do Tesseract, EasyOCR lub dowolnego nowoczesnego silnika OCR udostępniającego API w Pythonie.

---

## Czego będziesz potrzebować

- Python 3.8+ (dowolna nowsza wersja)
- Biblioteka OCR, która udostępnia klasę `OcrEngine` (przykład używa fikcyjnego pakietu `ocr`; zamień go na swoją rzeczywistą bibliotekę)
- Wielostronicowy plik TIFF, który chcesz przetworzyć (nazwijmy go `big_document.tif`)
- Maszyna z co najmniej 4 rdzeniami CPU, jeśli planujesz ustawić liczbę wątków

Bez zewnętrznych usług, bez kluczy chmurowych — tylko lokalny kod, który działa w kilka sekund.

---

![przykład wykonania OCR](/images/ocr-example.png "jak wykonać OCR na dokumencie TIFF")

*Tekst alternatywny obrazu: jak wykonać OCR na dokumencie TIFF – podgląd wyodrębnionego tekstu.*

---

## Krok 1: Zainstaluj i zaimportuj bibliotekę OCR

Na początek: zainstaluj bibliotekę na swoim komputerze. Większość pakietów OCR jest dostępna w PyPI, więc prosty `pip install` wystarczy.

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

Teraz zaimportuj potrzebne klasy. Jeśli używasz Tesseract, linia importu będzie wyglądała inaczej, ale reszta kodu pozostaje taka sama.

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*Dlaczego to ważne:* Wczesne importowanie właściwych symboli zapobiega konfliktom nazw później i sprawia, że skrypt jest łatwiejszy do odczytania.

---

## Krok 2: Utwórz i skonfiguruj silnik OCR (Ustaw język OCR)

Konfiguracja silnika to miejsce, w którym **ustawiasz język OCR** dla dokładnego rozpoznawania. Domyślnie jest to angielski, ale możesz przełączyć się na francuski, niemiecki lub tryb wielojęzyczny jednym wierszem.

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **Dlaczego 4 wątki?** Większość nowoczesnych laptopów ma co najmniej cztery rdzenie, a ograniczenie liczby wątków zapobiega przejęciu całego zasobu przez proces OCR — szczególnie przydatne, gdy skrypt działa na współdzielonym serwerze.

Jeśli potrzebujesz innego języka, po prostu zamień `ocr.Language.ENGLISH` na `ocr.Language.FRENCH`, `ocr.Language.SPANISH` itd.

---

## Krok 3: Wczytaj obraz do OCR (Load Image for OCR)

Teraz **wczytujemy obraz do OCR**. Metoda `Image.load` odczytuje plik TIFF do pamięci, automatycznie obsługując dokumenty wielostronicowe.

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*Przypadek brzegowy:* Jeśli plik jest bardzo duży, możesz wyczerpać pamięć RAM. W takiej sytuacji rozważ wczytywanie jednej strony na raz przy pomocy `Image.load_page(page_number)` (jeśli biblioteka to obsługuje).

---

## Krok 4: Uruchom OCR na dokumencie

Gdy silnik jest gotowy, a obraz wczytany, czas **uruchomić OCR na dokumencie**. Metoda `process` wykonuje ciężką pracę i zwraca obiekt wyniku.

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

Za kulisami silnik dzieli obraz na bloki tekstu, uruchamia model rozpoznawania i scala wyniki. Wywołanie jest blokujące, co oznacza, że skrypt czeka, aż cały TIFF zostanie przetworzony — idealne dla zadań wsadowych.

---

## Krok 5: Wyodrębnij tekst z TIFF i zweryfikuj wynik

Na koniec **wyodrębniamy tekst z TIFF**, odwołując się do atrybutu `text` wyniku. Wypiszmy pierwsze 200 znaków jako szybki test.

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**Oczekiwany wynik (przykład):**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

Jeśli potrzebujesz pełnego tekstu, po prostu użyj `ocr_result.text`. Do dalszego przetwarzania możesz zapisać go do pliku `.txt`:

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

---

## Pełny działający przykład

Łącząc wszystko razem, oto gotowy do uruchomienia skrypt. Zamień nazwę pakietu zastępczego na tę, którą faktycznie zainstalowałeś.

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

Uruchom skrypt poleceniem:

```bash
python ocr_tiff_example.py
```

Powinieneś zobaczyć podgląd wydrukowany w konsoli oraz plik o nazwie `extracted_text.txt` zawierający pełną transkrypcję.

---

## Często zadawane pytania i przypadki brzegowe

- **Co zrobić, gdy TIFF zawiera wiele stron?**  
  Większość silników OCR traktuje każdą stronę jako osobny obraz wewnętrznie. `ocr_result.text` będzie zawierał znak nowej linii pomiędzy stronami. Jeśli potrzebujesz obsługi per‑strona, iteruj z `Image.load_page(page_number)`.

- **Czy mogę przetworzyć PNG lub JPEG zamiast TIFF?**  
  Oczywiście. Metoda `Image.load` zazwyczaj akceptuje każdy format obsługiwany przez Pillow lub bazową bibliotekę. Wystarczy zmienić rozszerzenie pliku.

- **Mój tekst jest zniekształcony — czy powinienem zmienić język?**  
  Tak. Krok **ustaw język OCR** jest kluczowy dla dokumentów nie‑angielskich. Upewnij się, że pakiet językowy jest zainstalowany (np. `tesseract‑lang‑fra` dla francuskiego).

- **Brak pamięci?**  
  Zmniejsz `set_memory_limit` lub przetwarzaj strony pojedynczo. Niektóre silniki pozwalają także na zmniejszenie rozdzielczości obrazu przed rozpoznaniem.

---

## Zakończenie

Oto on — zwięzły, w pełni funkcjonalny przewodnik, **jak wykonać OCR** na pliku TIFF przy użyciu Pythona. Omówiliśmy wszystko: od instalacji biblioteki, konfiguracji silnika (w tym **ustaw język OCR**), **wczytanie obrazu do OCR**, **uruchomienie OCR na dokumencie**, aż po **wyodrębnienie tekstu z TIFF**.  

Śmiało eksperymentuj: zmieniaj liczbę wątków, przełączaj języki lub podsyłaj wynik OCR do pipeline’u przetwarzania języka naturalnego. Możliwości są nieograniczone, gdy opanujesz podstawy.

Masz więcej pytań? zostaw komentarz poniżej i powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}