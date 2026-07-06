---
category: general
date: 2026-06-19
description: Wyodrębnij tekst z obrazów przy użyciu Python OCR. Poznaj automatyczne
  wykrywanie języka, przetwarzanie równoległe i rozpoznawanie wsadowe w zwięzłym tutorialu.
draft: false
keywords:
- extract text from images
- Python OCR library
- automatic language detection
- parallel processing OCR
- batch image recognition
- ocr.OcrEngine usage
language: pl
og_description: Wyodrębniaj tekst z obrazów przy użyciu OCR w Pythonie. Ten przewodnik
  pokazuje automatyczne wykrywanie języka, przetwarzanie równoległe oraz rozpoznawanie
  wsadowe w jednym samouczku.
og_title: Wyodrębnianie tekstu z obrazów w Pythonie – pełny przewodnik OCR
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  headline: extract text from images in Python – Full OCR Guide
  type: TechArticle
- description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  name: extract text from images in Python – Full OCR Guide
  steps:
  - name: Python 3.8 or newer installed.
    text: Python 3.8 or newer installed.
  - name: The `ocr` package (`pip install ocr`).
    text: The `ocr` package (`pip install ocr`).
  - name: A folder of PNG (or JPG) images you want to process.
    text: A folder of PNG (or JPG) images you want to process.
  - name: Basic familiarity with Python functions and loops.
    text: Basic familiarity with Python functions and loops.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Wyodrębnianie tekstu z obrazów w Pythonie – pełny przewodnik OCR
url: /pl/python-java/general/extract-text-from-images-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# wyodrębnianie tekstu z obrazów w Pythonie – Pełny przewodnik OCR

Zastanawiałeś się kiedyś, jak **wyodrębnić tekst z obrazów** bez ręcznego przepisywania każdego słowa? Nie jesteś jedyny. Niezależnie od tego, czy digitalizujesz stare paragony, tworzysz przeszukiwalne archiwum dokumentów, czy po prostu bawisz się ciekawymi sztucznymi inteligencjami, umiejętność wyciągania tekstu ze zdjęć jest niezbędna dla każdego programisty Pythona współcześnie.

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który **wyodrębnia tekst z obrazów** przy użyciu popularnego silnika OCR. Omówimy automatyczne wykrywanie języka, równoległe przetwarzanie dla zwiększenia szybkości oraz rozpoznawanie obrazów w partiach, abyś mógł obsłużyć dziesiątki plików w kilka sekund. Brzmi jak to, czego potrzebujesz? Zanurzmy się.

## Czego się nauczysz

- Jak utworzyć instancję silnika OCR za pomocą `ocr.OcrEngine`.
- Włączenie **automatycznego wykrywania języka**, aby silnik sam wybierał odpowiedni język.
- Konfigurowanie **OCR z równoległym przetwarzaniem** przy użyciu własnej puli wątków.
- Uruchamianie **rozpoznawania obrazów w partiach** na liście plików.
- Wyświetlanie rozpoznanego tekstu dla każdego obrazu, gotowego do zapisania lub indeksacji.

Nie potrzebujesz żadnej zewnętrznej dokumentacji — wszystko, czego potrzebujesz, znajduje się tutaj, a kod działa od razu po zainstalowaniu pakietu `ocr` (zainstaluj go poleceniem `pip install ocr`).

## Wymagania wstępne

1. Python 3.8 lub nowszy zainstalowany.  
2. Pakiet `ocr` (`pip install ocr`).  
3. Folder z obrazami PNG (lub JPG), które chcesz przetworzyć.  
4. Podstawowa znajomość funkcji i pętli w Pythonie.

To wszystko — brak ciężkich zależności, żadnej magii GPU, po prostu czysty Python.

![przykład wyodrębniania tekstu z obrazów](https://example.com/ocr-demo.png "Zrzut ekranu pokazujący wynik wyodrębniania tekstu z obrazów")

*Alt text: zrzut ekranu demonstracji wyodrębniania tekstu z obrazów*

## Krok 1 – Konfiguracja silnika OCR (Główne słowo kluczowe w akcji)

Na początek: utwórz instancję silnika OCR. `ocr.OcrEngine()` to mózg całej operacji; wie, jak odczytywać znaki, linie i akapity.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

Dlaczego potrzebujemy wyraźnego silnika? Ponieważ **użycie ocr.OcrEngine** daje Ci precyzyjną kontrolę nad ustawieniami języka, wątkami i nie tylko. To najelastyczniejszy sposób na **wyodrębnianie tekstu z obrazów** w porównaniu do jednowierszowych pomocników.

## Krok 2 – Niech silnik automatycznie wykrywa języki

Większość bibliotek OCR wymaga podania języka, którego mają szukać. To w porządku przy projekcie jednojęzycznym, ale uciążliwe przy mieszanej partii językowej. Na szczęście pakiet `ocr` obsługuje **automatyczne wykrywanie języka**.

```python
# Step 2: Enable automatic language detection
engine.language = ocr.Language.Auto
```

Ustawienie `engine.language` na `ocr.Language.Auto` mówi silnikowi, aby „powąchał” każdy obraz i wybrał odpowiedni model językowy. Ten krótki wiersz oszczędza godziny ręcznej konfiguracji przy pracy z dokumentami międzynarodowymi.

## Krok 3 – Przyspiesz działanie dzięki równoległemu przetwarzaniu OCR

Masz cztery lub więcej rdzeni CPU? Dlaczego ich nie wykorzystać? Silnik może uruchomić pulę wątków, pozwalając na jednoczesne przetwarzanie wielu obrazów. To właśnie **równoległe przetwarzanie OCR** pokazuje swoją moc.

```python
# Step 3: Enable parallel processing with four worker threads
engine.set_thread_pool_size(4)
```

Śmiało dostosuj liczbę `4` do możliwości swojego komputera. Więcej wątków → szybsze przetwarzanie partii, ale pamiętaj, że każdy wątek zużywa pamięć, więc znajdź optymalny punkt dla swojego środowiska.

## Krok 4 – Zbierz obrazy, które chcesz przetworzyć

Teraz potrzebujemy listy ścieżek do plików. Możesz zbudować tę listę ręcznie, odczytać ją z CSV lub użyć `glob`. Dla przejrzystości zakodujemy krótką listę na stałe:

```python
# Step 4: Prepare a list of image files to be recognized
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
]
```

Zastąp `YOUR_DIRECTORY` rzeczywistą ścieżką w swoim systemie. Jeśli masz dziesiątki plików, szybkie `glob.glob("*.png")` wykona ciężką pracę.

## Krok 5 – Uruchom rozpoznawanie obrazów w partiach

Oto serce samouczka: jedno wywołanie, które przetwarza każdy obraz w `files` i zwraca listę obiektów wynikowych. To funkcja **rozpoznawania obrazów w partiach**, która czyni OCR na dużą skalę praktycznym.

```python
# Step 5: Perform batch recognition on all images
results = engine.recognize_batch(files)
```

W tle silnik rozdziela każdy plik na cztery wątki robocze, które skonfigurowaliśmy wcześniej, jednocześnie automatycznie wykrywając język dla każdego obrazu. Metoda zwraca listę, w której każdy element zawiera rozpoznany tekst oraz metadane.

## Krok 6 – Wyświetl (lub zapisz) wyodrębniony tekst

Na koniec przechodzimy po wynikach i drukujemy tekst. W prawdziwym projekcie prawdopodobnie zapiszesz to do bazy danych lub pliku CSV, ale wyświetlanie utrzymuje przykład prostym.

```python
# Step 6: Output the recognized text for each image
for result in results:
    print("---")
    print(f"File: {result.file_path}")
    print("Extracted Text:")
    print(result.text.strip())
    print("---\n")
```

**Oczekiwany wynik** (skrócony dla przejrzystości):

```
---
File: YOUR_DIRECTORY/doc1.png
Extracted Text:
Invoice #12345
Date: 2024‑03‑15
Total: $250.00
---
```

Każdy blok pokazuje nazwę pliku, po której następuje ciąg znaków wygenerowany przez OCR. Jeśli obraz zawiera wiele języków, zobaczysz odpowiednie znaki dzięki wcześniejszemu krokowi **automatycznego wykrywania języka**.

## Profesjonalne wskazówki i typowe pułapki

- **Jakość obrazu ma znaczenie** – rozmyte lub niskokontrastowe zdjęcia wygenerują śmieci. W razie potrzeby wstępnie przetwórz je za pomocą OpenCV (`cv2.threshold`, `cv2.resize`).  
- **Liczba wątków vs. I/O** – jeśli Twoje obrazy znajdują się na wolnym dysku sieciowym, więcej wątków może nie pomóc. Monitoruj użycie CPU przy pomocy `top` lub `Task Manager`.  
- **Obsługa Unicode** – `result.text` jest ciągiem Unicode. Przy zapisie do plików otwieraj je z `encoding="utf‑8"`, aby uniknąć `UnicodeEncodeError`.  
- **Zużycie pamięci** – duże pliki PDF mogą pochłaniać dużo RAMu. Jeśli napotkasz `MemoryError`, zmniejsz rozmiar puli wątków lub przetwarzaj obrazy w mniejszych partiach.

## Pełny działający skrypt

Poniżej znajduje się kompletny, gotowy do skopiowania i wklejenia skrypt, który zawiera wszystkie omówione kroki. Zapisz go jako `batch_ocr.py` i uruchom `python batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script to extract text from images using the ocr package.
Features:
- Automatic language detection
- Parallel processing with configurable thread pool
- Simple batch API for multiple files
"""

import ocr
import os
import sys

def main(image_dir: str, workers: int = 4):
    # Verify directory exists
    if not os.path.isdir(image_dir):
        print(f"Error: Directory '{image_dir}' does not exist.", file=sys.stderr)
        sys.exit(1)

    # Build list of PNG/JPG files
    supported_ext = (".png", ".jpg", ".jpeg", ".tif", ".tiff")
    files = [
        os.path.join(image_dir, f)
        for f in os.listdir(image_dir)
        if f.lower().endswith(supported_ext)
    ]

    if not files:
        print("No supported image files found in the directory.", file=sys.stderr)
        sys.exit(1)

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto          # automatic language detection
    engine.set_thread_pool_size(workers)         # parallel processing OCR

    # Perform batch recognition
    print(f"Processing {len(files)} files with {workers} workers...")
    results = engine.recognize_batch(files)

    # Output results
    for result in results:
        print("---")
        print(f"File: {result.file_path}")
        print("Extracted Text:")
        print(result.text.strip())
        print("---\n")

if __name__ == "__main__":
    # Example usage: python batch_ocr.py ./my_images 4
    if len(sys.argv) < 2:
        print("Usage: python batch_ocr.py <image_directory> [worker_count]")
        sys.exit(1)

    directory = sys.argv[1]
    worker_count = int(sys.argv[2]) if len(sys.argv) > 2 else 4
    main(directory, worker_count)
```

Uruchom go w ten sposób:

```bash
python batch_ocr.py ./my_images 4
```

Zobaczysz ładnie sformatowany blok tekstu dla każdego obrazu, co dowodzi, że możesz **wyodrębniać tekst z obrazów** na dużą skalę.

## Co dalej?

Teraz, gdy opanowałeś podstawy **wyodrębniania tekstu z obrazów** w Pythonie, rozważ dalsze eksploracje:

- **Post‑processing**: oczyszczanie wyników OCR przy użyciu wyrażeń regularnych lub bibliotek przetwarzania języka naturalnego.  
- **Konwersja do PDF**: wprowadź wyodrębnione ciągi do generatora PDF, aby uzyskać przeszukiwalne dokumenty.  
- **Usługi OCR w chmurze**: porównaj wyniki `ocr` lokalnie z Google Vision lub Azure OCR pod kątem dokładności w trudnych przypadkach.  
- **Interfejs GUI**: zbuduj małą aplikację Flask lub FastAPI, która pozwoli użytkownikom wgrywać obrazy i natychmiast widzieć wyodrębniony tekst.

Wszystkie te tematy opierają się na fundamencie **biblioteki OCR dla Pythona**, którą właśnie skonfigurowałeś, i korzystają z tych samych **trików równoległego przetwarzania OCR**, które zastosowaliśmy tutaj.

---

*Miłego kodowania! Jeśli napotkasz problemy, zostaw komentarz poniżej — zawsze chętnie pomogę rozwiązać trudności związane z OCR.*

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu wraz z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Wyodrębnianie tekstu z obrazu przy użyciu Aspose OCR – Przewodnik krok po kroku](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Wyodrębnianie tekstu z obrazów przy użyciu operacji OCR na folderach](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Wyodrębnianie tekstu z obrazu – Optymalizacja OCR z Aspose.OCR dla .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}