---
category: general
date: 2026-06-19
description: Wyodrębnij tekst z obrazów w Pythonie za pomocą prostego silnika OCR.
  Dowiedz się, jak konwertować zeskanowane obrazy na tekst, rozpoznawać tekst na zdjęciach
  oraz efektywnie wyświetlać pliki graficzne w Pythonie.
draft: false
keywords:
- extract text from images
- convert scanned images to text
- recognize text from pictures
- list image files python
language: pl
og_description: Wyodrębnij tekst z obrazów w Pythonie przy użyciu lekkiego silnika
  OCR. Ten przewodnik pokazuje, jak przekształcić zeskanowane obrazy w tekst, rozpoznać
  tekst na zdjęciach oraz wypisać pliki graficzne w Pythonie w kilku krokach.
og_title: Wyodrębnianie tekstu z obrazów w Pythonie – Pełny przewodnik po wsadowym
  OCR
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Extract text from images in Python with a simple OCR engine. Learn
    how to convert scanned images to text, recognize text from pictures, and list
    image files python efficiently.
  headline: Extract Text from Images in Python – Full Batch OCR Guide
  type: TechArticle
tags:
- Python
- OCR
- Image Processing
title: Wyodrębnianie tekstu z obrazów w Pythonie – Pełny przewodnik po OCR wsadowym
url: /pl/python-java/general/extract-text-from-images-in-python-full-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnianie tekstu z obrazów w Pythonie – Kompletny przewodnik po OCR wsadowym

Kiedykolwiek potrzebowałeś **wyodrębnić tekst z obrazów**, ale nie wiedziałeś, od czego zacząć? Nie jesteś sam — programiści stale stają przed wyzwaniem przekształcania zeskanowanych PDF‑ów, sfotografowanych paragonów czy zrzutów ekranu w tekst możliwy do przeszukiwania. W tym tutorialu przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który pokazuje, jak **zamienić zeskanowane obrazy na tekst**, rozpoznać tekst ze zdjęć oraz **list image files python**‑style. Po zakończeniu będziesz mieć wielokrotnego użytku skrypt, który przetwarza cały folder jednorazowo.

Omówimy wszystko, co potrzebne: wymagane biblioteki, dlaczego każdy krok ma znaczenie, obsługę przypadków brzegowych i trochę rozwiązywania problemów. Nie musisz przeszukiwać zewnętrznych dokumentacji; kod poniżej jest samodzielny, a wyjaśnienia odpowiadają zarówno na „jak”, jak i „dlaczego”. Otwórz ulubione IDE i zaczynamy.

---

## Co zbudujesz

- Zainicjalizujesz silnik OCR (do ilustracji użyjemy pakietu `ocr`).
- Przeskanujesz katalog i **list image files python**‑style, filtrując PNG, JPG i TIFF.
- Wykonasz operację **batch OCR** na wszystkich znalezionych obrazach.
- Wydrukujesz wyodrębniony tekst dla każdego pliku, wyraźnie oznaczony.

> **Pro tip:** Jeśli nie masz zainstalowanej biblioteki `ocr`, możesz zamienić ją na `pytesseract` przy kilku drobnych zmianach — logika pozostaje ta sama.

---

## Wymagania wstępne

- Python 3.8+ (skrypt używa f‑stringów i adnotacji typów).
- Biblioteka OCR udostępniająca `OcrEngine` z metodą `recognize_batch`. W tym przewodniku zakładamy fikcyjny pakiet `ocr`, ale wzorzec działa z prawdziwymi bibliotekami.
- Folder zawierający pliki graficzne, które chcesz przetworzyć (`.png`, `.jpg`, `.tif`).

---

## Krok 1 – Instalacja i import wymaganych modułów

Najpierw upewnij się, że pakiet OCR jest dostępny. Jeśli używasz prawdziwej biblioteki, takiej jak `pytesseract`, zamień import odpowiednio.

```python
# Install the fictional OCR package (skip if using pytesseract)
# pip install ocr-package

import os
import ocr  # <-- replace with your actual OCR library
from typing import List
```

> **Dlaczego to ważne:** Importowanie `os` zapewnia obsługę ścieżek niezależną od platformy, a `typing.List` pomaga w autouzupełnianiu w IDE i przyszłej rozbudowie.

---

## Krok 2 – **Extract Text from Images**: Inicjalizacja silnika OCR

Utworzenie silnika to pierwszy krok w każdej pracy z OCR. Ustawiamy także język na automatyczne wykrywanie, aby silnik mógł radzić sobie z dokumentami wielojęzycznymi.

```python
def create_engine() -> ocr.OcrEngine:
    """
    Initializes the OCR engine with automatic language detection.
    Returns:
        An instance of ocr.OcrEngine ready for batch processing.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto  # Auto‑detect language
    return engine
```

> **Wyjaśnienie:** Dzięki umieszczeniu tworzenia silnika w funkcji kod pozostaje modularny. Jeśli później będziesz musiał dostosować DPI lub tryb OCR, zmienisz to tylko w jednym miejscu.

---

## Krok 3 – **List Image Files Python**: Zbieranie plików z katalogu

Teraz musimy zlokalizować każde zdjęcie, które chcemy przetworzyć. Poniższe wyrażenie listowe odzwierciedla typowy wzorzec „list image files python”.

```python
def get_image_files(input_dir: str) -> List[str]:
    """
    Scans `input_dir` and returns a list of absolute paths
    for files ending with .png, .jpg, or .tif (case‑insensitive).
    """
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]
```

> **Obsługa przypadków brzegowych:** Funkcja ignoruje podkatalogi (możesz dodać rekurencję później) i automatycznie odrzuca ukryte pliki, ponieważ zazwyczaj nie kończą się one obsługiwanymi rozszerzeniami.

---

## Krok 4 – **Convert Scanned Images to Text**: Uruchomienie batch OCR

Większość bibliotek OCR oferuje metodę wsadową, która jest znacznie szybsza niż przetwarzanie pojedynczych obrazów. Oto jak ją wywołać.

```python
def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    """
    Sends a list of image file paths to the OCR engine for batch recognition.
    Returns a list of OcrResult objects, preserving order.
    """
    # The fictional `recognize_batch` returns a list of results matching input order
    return engine.recognize_batch(image_paths)
```

> **Dlaczego batch?** Przesyłanie wszystkich obrazów naraz zmniejsza narzut (np. wielokrotne ładowanie modelu OCR) i często zapewnia lepsze wykorzystanie CPU/GPU.

---

## Krok 5 – **Recognize Text from Pictures**: Wyświetlenie wyników

Na koniec iterujemy po sparowanych nazwach plików i wynikach OCR, wypisując przejrzysty nagłówek dla każdego obrazu.

```python
def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    """
    Prints the extracted text for each image, prefixed with the file name.
    """
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        # Some OCR engines store the plain text in a `.text` attribute
        print(result.text.strip())
        print()  # Blank line for readability
```

> **Wskazówka:** `strip()` usuwa białe znaki na początku i końcu, które OCR często dodaje.

---

## Pełny skrypt – Połącz wszystko razem

Poniżej znajduje się kompletny, gotowy do uruchomienia program. Zapisz go jako `batch_ocr.py` i uruchom `python batch_ocr.py <your_folder>`.

```python
#!/usr/bin/env python3
"""
Batch OCR script – extracts text from images in a given folder.
Usage: python batch_ocr.py /path/to/images
"""

import sys
import os
import ocr  # Replace with your OCR library if different
from typing import List

def create_engine() -> ocr.OcrEngine:
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto
    return engine

def get_image_files(input_dir: str) -> List[str]:
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]

def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    return engine.recognize_batch(image_paths)

def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        print(result.text.strip())
        print()

def main() -> None:
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <input_directory>")
        sys.exit(1)

    input_dir = sys.argv[1]

    if not os.path.isdir(input_dir):
        print(f"Error: '{input_dir}' is not a valid directory.")
        sys.exit(1)

    engine = create_engine()
    image_files = get_image_files(input_dir)

    if not image_files:
        print("No supported image files found in the directory.")
        sys.exit(0)

    ocr_results = run_batch_ocr(engine, image_files)
    display_results(image_files, ocr_results)

if __name__ == "__main__":
    main()
```

### Oczekiwany wynik

Zakładając, że w folderze znajdują się `invoice1.png` i `receipt.jpg`, możesz zobaczyć:

```
--- invoice1.png ---
Invoice #12345
Date: 2024‑04‑01
Total: $256.78

--- receipt.jpg ---
Store: Coffee Corner
Item: Latte
Price: $4.50
```

Każdy blok jest wyraźnie oznaczony, co ułatwia dalsze przetwarzanie (np. zapisywanie do bazy danych).

---

## Rozwiązywanie typowych problemów

| Problem | Dlaczego się pojawia | Szybka naprawa |
|---------|----------------------|---------------|
| **Brak wyświetlanego tekstu** | Język OCR nie został wykryty lub obraz ma zbyt niski kontrast. | Wymuś język (`engine.language = ocr.Language.English`) lub wstępnie przetwórz obrazy (zwiększ kontrast). |
| **Błąd pamięci przy dużych partiach** | Silnik próbuje załadować wszystkie obrazy jednocześnie. | Podziel `image_files` na fragmenty (`batch_size = 20`) i wywołuj `recognize_batch` wielokrotnie. |
| **Nieobsługiwany format pliku** | Dodałeś `.gif` lub `.bmp`. | Rozszerz krotkę `supported_exts` lub skonwertuj obrazy do PNG/JPG wcześniej. |
| **Zniekształcone znaki Unicode** | OCR zwraca bajty zamiast łańcuchów. | Upewnij się, że biblioteka OCR zwraca Unicode (`result.text.decode('utf‑8')` w razie potrzeby). |

---

## Rozszerzanie przepływu pracy

Teraz, gdy potrafisz **extract text from images**, rozważ następujące kolejne kroki:

- **Eksport do CSV** – Zapisz każdą nazwę pliku i wyodrębniony tekst w arkuszu kalkulacyjnym do dalszej analizy.
- **Przetwarzanie równoległe** – Użyj `concurrent.futures.ThreadPoolExecutor`, aby obsługiwać wiele partii jednocześnie.
- **Integracja z chmurowym OCR** – Zamień lokalny silnik na Google Vision lub Azure OCR, aby uzyskać wyższą dokładność przy skomplikowanych układach.
- **Dodaj wstępne przetwarzanie obrazu** – Biblioteki takie jak Pillow lub OpenCV mogą prostować, odszumiewać lub progować obrazy przed OCR, zwiększając wyniki.

Wszystkie te pomysły naturalnie wykorzystują te same podstawowe funkcje, które zbudowaliśmy, więc nie musisz zaczynać od zera.

---

## Zakończenie

Przeszliśmy razem przez kompletną metodę **extract text from images** w Pythonie, obejmując wszystko od **list image files python** po **recognize text from pictures** i w końcu **convert scanned images to text** w schludnym trybie wsadowym. Skrypt jest celowo prosty, a jednocześnie na tyle elastyczny, że może służyć jako podstawa większych projektów — czy to digitalizujesz paragony, budujesz przeszukiwalne archiwum, czy tworzysz potok ekstrakcji danych.

Wypróbuj go, dopasuj kroki wstępnego przetwarzania i obserwuj, jak rośnie dokładność OCR. Jeśli napotkasz problemy, wróć do tabeli „Rozwiązywanie typowych problemów” — większość z nich rozwiązuje się drobną zmianą konfiguracji.

Gotowy na kolejny wyzwanie? Spróbuj dodać krok konwersji PDF‑na‑obraz przy użyciu `pdf2image`, a następnie podaj te obrazy bezpośrednio do tego samego potoku. Nie ma granic, gdy łączysz OCR z bogatym ekosystemem Pythona.

Miłego kodowania i niech Twój tekst zawsze będzie czytelny!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz wyczerpujące wyjaśnienia krok po kroku, pomagające opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}