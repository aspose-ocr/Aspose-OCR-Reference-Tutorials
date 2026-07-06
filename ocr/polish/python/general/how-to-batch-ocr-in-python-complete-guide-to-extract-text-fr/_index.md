---
category: general
date: 2026-06-28
description: Jak wykonywać OCR wsadowo w Pythonie — wyodrębniać tekst z obrazów i
  konwertować zeskanowane strony na tekst przy użyciu przetwarzania OCR wsadowego.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: pl
og_description: Dowiedz się, jak wykonywać OCR wsadowo w Pythonie, wyodrębniać tekst
  z obrazów i konwertować zeskanowane strony na tekst przy użyciu efektywnego przetwarzania
  OCR w trybie wsadowym.
og_title: Jak wykonać wsadowe OCR w Pythonie – Przewodnik krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Jak wykonać OCR wsadowo w Pythonie – Kompletny przewodnik po wyodrębnianiu
  tekstu z obrazów
url: /pl/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonać wsadowe OCR w Pythonie – Kompletny przewodnik po wyodrębnianiu tekstu z obrazów

Jeśli zastanawiasz się **jak wykonać wsadowe OCR w Pythonie**, jesteś we właściwym miejscu. Ten samouczek pokazuje szybki sposób na **wyodrębnianie tekstu z obrazów** oraz **konwertowanie zeskanowanych stron na tekst** przy użyciu jednej instancji silnika OCR. Koniec z kopiowaniem i wklejaniem pliku po pliku — niech kod wykona ciężką pracę.

Przejdziemy przez wszystko, co potrzebne: instalację biblioteki, wczytanie całego folderu ze skanami, uruchomienie wsadowego przetwarzania OCR oraz eleganckie obsłużenie wyników. Po zakończeniu będziesz mieć wielokrotnego użytku skrypt, który w kilka sekund zamieni stos PNG‑ów lub JPEG‑ów w przeszukiwalne pliki tekstowe.

## Czego będziesz potrzebować

* Python 3.9+ zainstalowany (kod działa także na 3.8, ale 3.9+ daje najnowsze funkcje typowania).
* Nowoczesna biblioteka OCR — tutaj używamy **Aspose.OCR for Python via .NET**, która udostępnia klasę `OcrEngine` pokazanej w oryginalnym fragmencie.  
  ```bash
  pip install aspose-ocr
  ```
* Folder ze zeskanowanymi stronami (`page1.png`, `page2.png`, …). Wszystko, co Pillow potrafi otworzyć, będzie działać, więc PDF‑y, TIFF‑y czy BMP‑y również są w porządku.
* Odrobina ciekawości — jeśli nigdy nie automatyzowałeś konwersji obrazu na tekst, zaraz zobaczysz, dlaczego wsadowe OCR jest przełomem.

> **Pro tip:** Jeśli wolisz czysto‑Pythonową bibliotekę, zamień `OcrEngine` na `pytesseract.image_to_string`. Logika otaczająca pozostaje identyczna.

## Jak wykonać wsadowe OCR w Pythonie – Przewodnik krok po kroku

Poniżej znajduje się kompletny, gotowy do uruchomienia skrypt. Każda linia jest skomentowana, abyś mógł zobaczyć *dlaczego* dany fragment jest ważny, a nie tylko *co* robi.

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### Oczekiwany wynik

Uruchomienie skryptu na folderze z trzema skanami PNG daje coś w rodzaju:

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

Podgląd pokazuje pierwsze 200 znaków każdej strony, a pełny tekst znajduje się w katalogu `ocr_output`.

## Wyodrębnianie tekstu z obrazów przy użyciu jednego silnika

Dlaczego tworzymy **jedną** instancję `OcrEngine` i ponownie ją używamy? Inicjalizacja silnika może być kosztowna, ponieważ ładuje pakiety językowe i natywne DLL‑e. Udostępniając tę samą instancję w całej partii, uzyskasz:

* **Oszczędność pamięci** – w RAM znajduje się tylko jeden zestaw zasobów.
* **Zwiększenie szybkości** – silnik pozostaje „rozgrzany”, unikając powtarzanej inicjalizacji.
* **Spójność** – te same ustawienia rozpoznawania mają zastosowanie do każdej strony, co jest kluczowe, gdy chcesz **wyodrębniać tekst z obrazów** o jednolitym układzie.

Jeśli musisz dostosować rozpoznawanie (np. włączyć sprawdzanie pisowni lub zmienić język), zrób to *przed* wywołaniem `recognize_batch`. Wszystkie kolejne strony automatycznie odziedziczą te ustawienia.

## Efektywne konwertowanie zeskanowanych stron na tekst

Sedno problemu — **konwertowanie zeskanowanych stron na tekst** — rozwiązuje metoda `engine.recognize_batch(images)`. W tle biblioteka przetwarza każdy obraz w puli wątków, dzięki czemu uzyskujesz prawie liniowe skalowanie na maszynach wielordzeniowych. Kilka rzeczy, o których warto pamiętać:

* **Jakość obrazu ma znaczenie** – 300 dpi lub wyższe daje najlepsze rezultaty. Jeśli skany są niskiej rozdzielczości, rozważ zwiększenie rozdzielczości przy pomocy Pillow przed przekazaniem ich do silnika.
* **Kolor vs. odcienie szarości** – silniki OCR zazwyczaj działają szybciej na 8‑bitowych odcieniach szarości. Możesz dodać krok wstępnego przetwarzania:  
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **Wsparcie językowe** – Aspose.OCR obsługuje ponad 40 języków. Ustaw `engine.language = "eng"` lub `"fra"` przed wywołaniem partii, jeśli nie pracujesz w języku angielskim.

## Najlepsze praktyki przetwarzania wsadowego OCR

Choć powyższy kod jest już zwięzły, produkcyjne wsadowe OCR często wymaga kilku dodatkowych zabezpieczeń:

| Problem | Zalecane podejście |
|---------|--------------------|
| **Duże partie ( > 500 plików )** | Podziel na fragmenty po 100–200 obrazów, aby utrzymać umiarkowane zużycie pamięci. |
| **Uszkodzone lub nieobsługiwane pliki** | Pomocnicza funkcja `load_images` już przechwytuje wyjątki i loguje ostrzeżenie; możesz także dodać mechanizm pomijania lub przenoszenia wadliwych plików. |
| **Monitorowanie postępu** | Owiń `recognize_batch` w pętlę, która zwraca kontrolę po każdym obrazie, jeśli biblioteka udostępnia callbacki per‑obraz. |
| **Post‑przetwarzanie** | Uruchom sprawdzanie pisowni lub czyszczenie wyrażeń regularnych na otrzymanych łańcuchach, aby poprawić ich przydatność w dalszych wyszukiwaniach. |
| **Równoległość** | Jeśli masz środowisko wielowęzłowe, rozdziel foldery pomiędzy pracowników i scal wyniki `.txt` na końcu. |

Te wskazówki pomogą Ci skalować **przetwarzanie wsadowe OCR** od kilku stron do tysięcy, nie powodując awarii skryptu.

## Najczęściej zadawane pytania

**Q: Czy mogę używać tego bezpośrednio z plikami PDF?**  
A: Oczywiście. Najpierw skonwertuj każdą stronę PDF na obraz (np. przy użyciu `pdf2image`), a następnie przekaż otrzymaną listę do `recognize_batch`. Reszta potoku pozostaje niezmieniona.

## Co warto nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu wraz z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}