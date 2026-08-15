---
category: general
date: 2026-03-28
description: Szybko wyodrębnij tekst z plików PNG przy użyciu Aspose OCR w Pythonie.
  Dowiedz się, jak konwertować tekst zeskanowanych stron przy użyciu równoległego
  rozpoznawania obrazu w Pythonie, aby uzyskać wysokowydajne wyniki.
draft: false
keywords:
- extract text from png
- convert scanned pages text
- parallel image recognition python
- recognize image text python
- async OCR batch processing
- Aspose OCR Python
language: pl
og_description: Szybko wyodrębnij tekst z plików PNG przy użyciu Aspose OCR w Pythonie.
  Ten przewodnik pokazuje, jak konwertować tekst zeskanowanych stron przy użyciu równoległego
  rozpoznawania obrazu w Pythonie, zapewniając wyniki o wysokiej prędkości.
og_title: Wyodrębnij tekst z PNG – szybkie równoległe OCR w Pythonie
tags:
- OCR
- Python
- Image Processing
- Concurrency
title: Wyodrębnij tekst z PNG – szybkie równoległe OCR w Pythonie i Aspose
url: /pl/python-java/general/extract-text-from-png-fast-parallel-ocr-with-python-and-aspo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnianie tekstu z PNG – Szybkie równoległe OCR w Pythonie

Czy kiedykolwiek potrzebowałeś **wyodrębnić tekst z PNG** i odkryłeś, że jednowątkowe OCR jest bolesnie wolne? Nie jesteś sam. Niezależnie od tego, czy digitalizujesz stos zeskanowanych paragonów, czy zamieniasz slajdy wykładowe w przeszukiwalne PDF‑y, wąskim gardłem jest zazwyczaj sam krok OCR.  

W tym samouczku pokażemy Ci kompletną, gotową do uruchomienia rozwiązanie, które **konwertuje tekst zeskanowanych stron** równolegle, wykorzystując asynchroniczny tryb wsadowy Aspose OCR wraz z `ThreadPoolExecutor` w Pythonie. Po zakończeniu będziesz w stanie **rozpoznawać tekst obrazu w stylu python**, obsługując dziesiątki obrazów w ułamku czasu, jaki zajęłaby prosta pętla.

> **Co wyniesiesz z tego**  
> * W pełni funkcjonalny skrypt, który wyodrębnia tekst z obrazów PNG równocześnie.  
> * Zrozumienie, dlaczego tryb asynchroniczny wsadowy przyspiesza działanie.  
> * Wskazówki dotyczące skalowania rozwiązania do większych obciążeń.

## Czego będziesz potrzebować

| Wymaganie | Powód |
|--------------|--------|
| Python 3.9+ | Nowoczesna składnia i wskazówki typów. |
| `aspose-ocr` i `aspose-storage` pakiety | Dostarczają silnik OCR oraz ładowarkę obrazów. |
| Folder z plikami PNG (np. zeskanowane strony) | Materiał źródłowy, który chcesz przetworzyć. |
| Podstawowa znajomość współbieżności w Pythonie | Przydatna, ale nieobowiązkowa; wszystko wyjaśnimy. |

Możesz zainstalować biblioteki Aspose za pomocą:

```bash
pip install aspose-ocr aspose-storage
```

> **Pro tip:** Utrzymuj pakiety aktualne (`pip list --outdated`), aby korzystać z najnowszych usprawnień wydajności.

## Krok 1: Inicjalizacja silnika Aspose OCR w trybie asynchronicznego wsadowego

Pierwszą rzeczą, którą robimy, jest stworzenie instancji `OcrEngine` i przełączenie jej na **asynchroniczny tryb wsadowy**. Ten tryb kolejkowuje żądania rozpoznawania wewnętrznie, pozwalając silnikowi przetwarzać wiele obrazów bez blokowania wątku Pythona.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the OCR engine
ocr_engine = aocr.OcrEngine()
# Enable async batch processing – crucial for parallel speed‑up
ocr_engine.batch_mode = aocr.BatchMode.ASYNC
```

*Dlaczego async?*  
Kiedy wywołujesz `recognize` w trybie synchronicznym, wywołanie blokuje się aż obraz zostanie w pełni przetworzony. W trybie async silnik może rozpocząć pracę nad następnym obrazem, podczas gdy bieżący nadal jest dekodowany, efektywnie nakładając pracę I/O i CPU.

## Krok 2: Lista plików PNG, które chcesz przetworzyć

Tutaj definiujemy kolekcję obrazów. W prawdziwym projekcie możesz generować tę listę dynamicznie (np. `glob.glob("*.png")`), ale jej jawne określenie ułatwia zrozumienie przykładu.

```python
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]
```

> **Uwaga:** Zamień `YOUR_DIRECTORY` na rzeczywistą ścieżkę, w której znajdują się Twoje skany PNG. Jeśli masz setki plików, rozważ użycie `os.listdir` i filtrowanie pod kątem `.png`.

## Krok 3: Napisz pomocniczą funkcję, która ładuje obraz i zwraca jego tekst

Funkcja pomocnicza abstrahuje dwustopniowy proces ładowania pliku przez **Aspose Storage**, a następnie przekazywania go do silnika OCR. Dodanie krótkiego docstringa sprawia, że funkcja jest samodokumentująca — przydatna przy przyszłej konserwacji.

```python
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the recognized text.
    """
    # Load the image using Aspose Storage (handles many formats)
    img = storage.Image.load(path)
    # Perform OCR; the result object contains the extracted text
    result = ocr_engine.recognize(img)
    return result.text
```

*Dlaczego osobna funkcja?*  
Utrzymuje kod thread‑pool w czystości i pozwala ponownie używać logiki w innych miejscach (np. w endpointzie Flask). Dodatkowo izolowanie I/O ułatwia debugowanie — jeśli konkretny plik się nie powiedzie, zobaczysz nazwę pliku w śladowym komunikacie wyjątku.

## Krok 4: Uruchom równoległe rozpoznawanie obrazów w Pythonie przy użyciu puli wątków

Teraz wprowadzamy `ThreadPoolExecutor`. Domyślnie uruchamiamy czterech pracowników, ale możesz dostosować `max_workers` w zależności od liczby rdzeni CPU i rozmiaru zestawu obrazów.

```python
from concurrent.futures import ThreadPoolExecutor, as_completed

with ThreadPoolExecutor(max_workers=4) as pool:
    # Submit each image to the pool; map futures back to filenames
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    
    # Process results as they finish (order may differ from input order)
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)
```

### Jak to zapewnia równoległe rozpoznawanie obrazów w Pythonie

* **ThreadPoolExecutor** tworzy pulę wątków pracowników, z których każdy wywołuje `recognize_image`.  
* Ponieważ silnik OCR działa w trybie asynchronicznego wsadowego, każdy wątek może przekazać pracę silnikowi, pozostając jednocześnie responsywnym.  
* `as_completed` zwraca future w kolejności ich zakończenia, więc otrzymujesz wyniki natychmiast po ich gotowości — idealne do strumieniowego przetwarzania dużych partii.

> **Typowy problem:** użycie `max_workers=1` niszczy cel równoległości. Na maszynie z 8 rdzeniami, `max_workers=8` często daje najlepszą przepustowość, ale przetestuj kilka wartości, aby znaleźć optymalny punkt dla swojego sprzętu.

## Krok 5: Zweryfikuj wyjście i obsłuż przypadki brzegowe

Gdy uruchomisz skrypt, powinieneś zobaczyć blok tekstu dla każdego PNG, poprzedzony nazwą pliku:

```
--- YOUR_DIRECTORY/page1.png ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- YOUR_DIRECTORY/page2.png ---
Sed do eiusmod tempor incididunt ut labore et dolore...

--- YOUR_DIRECTORY/page3.png ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Jeśli którykolwiek obraz się nie powiedzie (uszkodzony plik, nieobsługiwany format), blok `except` wypisze pomocny komunikat o błędzie zamiast awarii całej partii.

### Rozszerzanie rozwiązania

| Scenariusz | Sugerowana modyfikacja |
|----------|-----------------|
| **Tysiące stron** | Przełącz na `ProcessPoolExecutor`, aby wykorzystać wiele procesów CPU, lub podziel listę i przetwarzaj partie kolejno. |
| **Różne formaty obrazów (JPG, TIFF)** | Metoda `storage.Image.load` automatycznie wykrywa format, więc po prostu dodaj pliki do `input_images`. |
| **Potrzeba przechowywania wyników** | Zapisz `text` do pliku `.txt` lub wstaw do bazy danych w bloku `else`. |
| **Monitorowanie wydajności** | Otocz `recognize_image` timerem (`time.perf_counter`) i loguj czas trwania dla każdego pliku. |

## Pełny działający przykład (gotowy do kopiowania i wklejania)

Poniżej znajduje się kompletny skrypt, gotowy do umieszczenia w pliku o nazwie `parallel_ocr.py`. Żadne części nie brakuje — wszystko, czego potrzebujesz, jest tutaj.

```python
# parallel_ocr.py
import aspose.ocr as aocr
import aspose.storage as storage
from concurrent.futures import ThreadPoolExecutor, as_completed

# -------------------------------------------------
# Step 1: Initialize OCR engine in async batch mode
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.batch_mode = aocr.BatchMode.ASYNC   # enable asynchronous batch processing

# -------------------------------------------------
# Step 2: Define the PNG files you want to recognize
# -------------------------------------------------
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]

# -------------------------------------------------
# Step 3: Helper that loads an image and returns the recognized text
# -------------------------------------------------
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the OCR‑extracted text.
    """
    img = storage.Image.load(path)
    result = ocr_engine.recognize(img)
    return result.text

# -------------------------------------------------
# Step 4: Run OCR on all images concurrently using a thread pool
# -------------------------------------------------
with ThreadPoolExecutor(max_workers=4) as pool:
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)

# -------------------------------------------------
# Step 5: Output is printed to the console.
# -------------------------------------------------
```

Zapisz plik, dostosuj placeholder `YOUR_DIRECTORY` i uruchom:

```bash
python parallel_ocr.py
```

Powinieneś zobaczyć wyodrębniony tekst dla każdego PNG w konsoli, tak jak pokazano wcześniej.

## Podsumowanie

Właśnie pokazaliśmy, jak efektywnie **wyodrębnić tekst z PNG** łącząc asynchroniczny tryb wsadowy Aspose OCR z `ThreadPoolExecutor` w Pythonie. Skrypt konwertuje tekst zeskanowanych stron równolegle, dając skalowalny sposób na **rozpoznawanie tekstu obrazu w stylu python** bez konieczności pisania własnej puli wątków od podstaw.

Jeśli jesteś gotów pójść dalej, spróbuj:

* Przechowywania wyników w przeszukiwalnej bazie SQLite.  
* Dodania wstępnego przetwarzania obrazu (prostowanie, odszumianie) za pomocą OpenCV przed OCR.  
* Wdrożenia skryptu jako mikroserwisu za pośrednictwem endpointu Flask lub FastAPI.

Pamiętaj, kluczem do wysokowydajnego OCR nie jest tylko szybszy silnik — chodzi także o dostarczanie pracy silnikowi w sposób maksymalizujący współbieżność. Dzięki przedstawionemu wzorcowi możesz obsłużyć dziesiątki, a nawet setki skanów PNG przy minimalnych zmianach w kodzie.

Szczęśliwego kodowania i niech Twoje PDF‑y zawsze będą przeszukiwalne!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}