---
category: general
date: 2026-03-18
description: Wyodrębnij tekst z pliku PNG przy użyciu Pythona i Aspose OCR. Dowiedz
  się, jak załadować obraz do OCR, uruchomić OCR na wielu plikach oraz wykonać wsadowe
  rozpoznawanie obrazów z równoległym przetwarzaniem.
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: pl
og_description: Wyodrębnij tekst z pliku PNG przy użyciu Aspose OCR w Pythonie. Ten
  poradnik pokazuje, jak wczytać obraz do OCR, przetworzyć wiele plików OCR oraz uruchomić
  wsadowe OCR obrazów przy użyciu równoległego rozpoznawania.
og_title: Wyodrębnij tekst z PNG – Przewodnik po równoległym OCR
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: Wyodrębnianie tekstu z PNG – Przewodnik po równoległym OCR dla rozpoznawania
  obrazów wsadowych
url: /pl/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnianie tekstu z PNG – Przewodnik po równoległym OCR dla przetwarzania wsadowego obrazów

Kiedykolwiek potrzebowałeś **wyodrębnić tekst z PNG** plików, ale utknąłeś w miejscu, w którym pojedynczy obraz przetwarza się w nieskończoność? Nie jesteś sam. W wielu rzeczywistych projektach — pomyśl o skanerach faktur, cyfrowych paragonach czy narzędziach archiwizacyjnych — szybkość ma znaczenie, a przetwarzanie każdego PNG po kolei po prostu nie wystarczy.  

W tym przewodniku przeprowadzimy Cię przez kompletną, gotową do uruchomienia rozwiązanie, które **ładuje obraz do OCR**, uruchamia **ocr multiple files** w trybie **batch OCR images**, i wykorzystuje **parallel image recognition** z modułem `threading` w Pythonie. Po zakończeniu będziesz mieć skrypt, który wyciąga tekst z dowolnej liczby PNG w ciągu sekund, nie minut.

## Czego będziesz potrzebować

- Python 3.8 lub nowszy (pokazany składnik działa również na 3.10+).  
- Pakiet Aspose OCR for Java/Python (`aspose-ocr`). Możesz go zainstalować za pomocą `pip`.  
- Folder z kilkoma plikami PNG, które chcesz przetworzyć.  
- Umiarkowana ilość RAM — każdy wątek utrzymuje małą instancję silnika OCR, więc nawet laptop może uruchomić dziesiątki pracowników.

Bez zewnętrznych usług, kluczy w chmurze i tajemniczych plików konfiguracyjnych. Po prostu czysty kod Pythona, który możesz skopiować‑wkleić i uruchomić.

## Dlaczego wyodrębniać tekst z PNG równolegle?

Przetwarzanie PNG jest zależne od CPU: silnik OCR wykonuje szereg algorytmów analizy obrazu, które przetwarzają dane pikseli. Gdy masz dziesięć, dwadzieścia lub sto obrazów, całkowity czas wykonania jest w zasadzie sumą poszczególnych uruchomień.  

Tworząc wątek dla każdego pliku, pozwalamy systemowi operacyjnemu planować te obciążające CPU zadania równocześnie. Na maszynie wielordzeniowej często skraca to — o połowę lub nawet do jednej czwartej — rzeczywisty czas wykonania. Wadą jest nieco większe zużycie pamięci, ale w większości zadań wsadowych zysk w szybkości jest tego wart.

> **Pro tip:** Jeśli masz do czynienia ze setkami megabajtów obrazów, rozważ użycie `concurrent.futures.ProcessPoolExecutor` zamiast `threading`. Procesy zapewniają prawdziwy równoległość w interpreterze CPython ograniczonym przez GIL, kosztem nieco większego narzutu.

## Krok 1: Zainstaluj Aspose OCR dla Pythona

Na początek — zdobądźmy bibliotekę OCR na Twój system.

```bash
pip install aspose-ocr
```

Ta pojedyncza linia pobiera najnowsze binaria Aspose OCR oraz ich powiązania Pythona. Jeśli napotkasz błąd uprawnień, spróbuj dodać `--user` lub użyć środowiska wirtualnego.

## Krok 2: Ładowanie obrazu do OCR – funkcja pracownika

Teraz definiujemy podstawową procedurę, która będzie wykonywana w każdym wątku. Ona **ładuje obraz do OCR**, uruchamia rozpoznawanie i drukuje podgląd wyodrębnionego tekstu.

```python
import threading
from asposeocrjava import OcrEngine, OcrResult

def ocr_task(image_path: str):
    """
    Loads a PNG, runs OCR, and prints the first 100 characters of the result.
    Each thread creates its own OcrEngine instance to avoid state clashes.
    """
    # Initialise a fresh engine – this is cheap and thread‑safe.
    engine = OcrEngine()
    # Load image for OCR
    engine.setImageFromFile(image_path)

    # Perform the recognition – this is the CPU‑intensive part.
    result: OcrResult = engine.recognize()

    # Show a preview of the recognized text (first 100 characters)
    preview = result.getText()[:100].replace("\n", " ")
    print(f"[{image_path}] -> {preview}...")
```

Kilka rzeczy do zauważenia:

- **Dlaczego nowy `OcrEngine` na wątek?** Silnik przechowuje wewnętrzne bufory; współdzielenie jednej instancji spowodowałoby warunki wyścigu i zniekształcony wynik.  
- **Dlaczego usuwamy znaki nowej linii?** Gdy logujemy do konsoli, utrzymuje to linię schludną.  
- **Obsługa błędów?** W produkcji opakowałbyś ciało w `try/except` i ewentualnie logował do pliku — coś, co omówimy później.

## Krok 3: Lista plików PNG, które chcesz przetworzyć

Możesz zakodować listę na stałe, ale bardziej elastycznym podejściem jest skanowanie katalogu. Poniżej ręcznie wymieniamy trzy pliki dla przejrzystości; zamień ścieżki na własny folder.

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

Jeśli wolisz automatyczne wykrywanie:

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

Ta mała zmiana pozwala **wyodrębnić tekst z PNG** w trybie masowym bez konieczności modyfikacji kodu źródłowego przy każdym uruchomieniu.

## Krok 4: Konfiguracja ocr multiple files z batch OCR images

Teraz tworzymy wątek dla każdego obrazu. To jest serce wzorca **batch OCR images**.

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

Wyrażenie listowe utrzymuje kod zwięzły, a każdy obiekt `Thread` przechowuje funkcję docelową i jej argument (`image_path`).  

> **Side note:** Moduł `threading` Pythona używa natywnych wątków systemu operacyjnego, więc na laptopie z 4‑rdzeniami zazwyczaj zobaczysz do czterech wątków naprawdę działających jednocześnie; reszta będzie planowana w miarę zwalniania rdzeni.

## Krok 5: Uruchomienie równoległego rozpoznawania obrazu

Uruchomienie pracowników jest proste: iterujemy po liście i wywołujemy `start()`. Następnie czekamy, aż każdy wątek zakończy się, używając `join()`.

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

Gdy skrypt zakończy się, zobaczysz serię linii podobnych do:

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

Ten wynik potwierdza, że każdy PNG został przetworzony i wyodrębniony tekst jest dostępny do dalszego przetwarzania (np. zapisania w bazie danych lub przekazania do potoku NLP).

## Krok 6: Weryfikacja wyników i obsługa przypadków brzegowych

### Sprawdzanie pustych wyników

Czasami obraz jest zbyt zaszumiony lub silnik OCR nie wykrywa żadnych znaków. Szybka kontrola może uchronić Cię przed późniejszymi błędami.

```python
def ocr_task(image_path: str):
    engine = OcrEngine()
    engine.setImageFromFile(image_path)

    result: OcrResult = engine.recognize()
    text = result.getText().strip()

    if not text:
        print(f"[{image_path}] -> No text detected.")
    else:
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")
```

### Ograniczanie liczby jednoczesnych wątków

Jeśli uruchamiasz to na skromnym VM, tworzenie setek wątków może przytłoczyć planistę. Możesz ograniczyć równoległość za pomocą semafora:

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### Zapisywanie wyników do pliku

Zamiast drukować, możesz chcieć CSV z nazwą pliku i wyodrębnionym tekstem:

```python
import csv
output_path = "ocr_results.csv"

with open(output_path, "w", newline="", encoding="utf-8") as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(["filename", "extracted_text"])

    def ocr_task(image_path: str):
        engine = OcrEngine()
        engine.setImageFromFile(image_path)
        text = engine.recognize().getText().strip()
        writer.writerow([image_path, text])
```

Upewnij się, że otwierasz CSV **jednokrotnie** poza funkcją wątku, aby uniknąć warunków wyścigu; zapisujący `csv` jest bezpieczny dla wątków przy prostych zapisach.

## Pełny działający przykład

Łącząc wszystko razem, oto pojedynczy skrypt, który możesz umieścić w pliku o nazwie `batch_ocr.py` i uruchomić:

```python
import threading
import pathlib
import csv
from asposeocrjava import OcrEngine, OcrResult

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_DIR = pathlib.Path("YOUR_DIRECTORY")   # <-- change this
OUTPUT_CSV = "ocr_results.csv"
MAX_WORKERS = 8                               # adjust based on your CPU

# ----------------------------------------------------------------------
# Helper: OCR worker
# ----------------------------------------------------------------------
sema = threading.Semaphore(MAX_WORKERS)

def ocr_task(image_path: str, writer):
    """
    Extract text from a single PNG using Aspose OCR.
    This function is designed to run inside a thread.
    """
    with sema:                     # limit concurrent threads
        engine = OcrEngine()
        engine.setImageFromFile(image_path)

        result: OcrResult = engine.recognize()
        text = result.getText().strip()

        # Write to CSV (thread‑safe because writer is shared)
        writer.writerow([image_path, text])

        # Also print a short preview for quick debugging
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")

# ----------------------------------------------------------------------
# Main routine
# ----------------------------------------------------------------------
def main():
    # Discover all PNG files
    image_files = sorted(str(p) for p in IMAGE_DIR.glob("*.png"))
    if not image_files:
        print("No PNG files found in", IMAGE_DIR)
        return

    # Open CSV once, share the writer with all threads
    with open(OUTPUT_CSV, "w", newline="", encoding="utf-8") as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(["filename", "extracted_text"])

        # Create a thread for each image
        threads = [
            threading.Thread(target=ocr_task, args=(path, writer))
            for path in image_files

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}