---
category: general
date: 2026-06-22
description: Samouczek batch OCR w Pythonie pokazujący, jak uruchomić wielowątkowe
  OCR na folderze obrazów PNG przy użyciu Tesseract i pathlib. Naucz się szybkiego
  batchowego OCR obrazów w Pythonie.
draft: false
keywords:
- python batch ocr tutorial
- multithreaded OCR in Python
- tesseract OCR batch processing
- pathlib image handling
- OCR thread count optimization
language: pl
og_description: Samouczek batch OCR w Pythonie prowadzi Cię przez kompletny, uruchamialny
  skrypt, który przetwarza wiele plików PNG przy użyciu Tesseract i wielu wątków.
og_title: Samouczek wsadowkiego OCR w Pythonie – szybkie wielowątkowe OCR dla obrazów
  PNG
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  headline: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  type: TechArticle
- description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  name: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  steps:
  - name: '**Collects** every PNG with **pathlib image handling**.'
    text: '**Collects** every PNG with **pathlib image handling**.'
  - name: '**Spins up** a **multithreaded OCR in Python** worker pool.'
    text: '**Spins up** a **multithreaded OCR in Python** worker pool.'
  - name: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
    text: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
  - name: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
    text: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
  type: HowTo
tags:
- OCR
- Python
- Batch Processing
title: 'Samouczek wsadowego OCR w Pythonie: Efektywne przetwarzanie wielu plików PNG'
url: /pl/python-java/general/python-batch-ocr-tutorial-process-multiple-pngs-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# python batch ocr tutorial – Szybki wielowątkowy OCR dla obrazów PNG

Zastanawiałeś się kiedyś, jak **python batch ocr tutorial** przejść przez setki zrzutów ekranu PNG, nie dopuszczając do przegrzania procesora? Nie jesteś jedyny. Czy cyfryzujesz zeskanowane formularze, wyodrębniasz tekst z paragonów, czy budujesz przeszukiwalne archiwum, solidny potok batch OCR zaoszczędzi Ci godziny.

W tym przewodniku stworzymy mały, ale potężny skrypt, który zbierze wszystkie `*.png` w folderze, przekaże je do Tesseract za pomocą wielowątkowego procesora i zapisze wyniki w postaci czystego tekstu w uporządkowanym katalogu wyjściowym. Bez tajemniczych bibliotek — tylko `pathlib`, `concurrent.futures` i niezawodny `pytesseract`. Po zakończeniu będziesz mieć **python batch ocr tutorial**, który możesz skopiować i wkleić do dowolnego projektu.

## Czego się nauczysz

- Jak zbierać pliki obrazów przy użyciu **pathlib image handling**  
- Konfigurowanie **multithreaded OCR in Python** puli pracowników  
- Dostosowywanie **OCR thread count optimization** do rdzeni CPU  
- Zapisywanie każdego wyniku z przejrzystym schematem nazewnictwa do późniejszego wyszukiwania  
- Uruchamianie całości jako jednego, samodzielnego skryptu  

## Wymagania wstępne (Co potrzebujesz najpierw)

| Wymaganie | Dlaczego jest ważne |
|-------------|----------------|
| Python 3.9+ | Nowoczesna składnia (`pathlib`, f‑strings) |
| Tesseract 5.x zainstalowany i dostępny w `PATH` | Silnik OCR stojący za `pytesseract` |
| `pytesseract` (`pip install pytesseract`) | Nakładka Pythona dla Tesseract |
| `Pillow` (`pip install pillow`) | Ładowanie obrazów dla Tesseract |
| Folder plików PNG, które chcesz przetworzyć | Nasz cel **tesseract OCR batch processing** |

> **Wskazówka:** Jeśli używasz Windows, dodaj `C:\Program Files\Tesseract-OCR` do systemowego `PATH`, aby `pytesseract` mógł automatycznie znaleźć plik wykonywalny.

---

## Krok 1 – Zbierz wszystkie obrazy PNG (przy użyciu pathlib)

First things first: we need a list of every image we plan to run OCR on. `pathlib` makes this a one‑liner and keeps the code OS‑agnostic.

```python
import pathlib

# Adjust the path to point at your source folder
source_dir = pathlib.Path("YOUR_DIRECTORY/batch_images")
image_files = list(source_dir.glob("*.png"))

print(f"Found {len(image_files)} PNG files to process.")
```

*Why `pathlib`?* It abstracts away Windows backslashes vs. Unix slashes, letting the same script run everywhere. This is the cornerstone of **pathlib image handling** in our tutorial.

*Dlaczego `pathlib`?* Abstrahuje on ukośniki Windows od ukośników Unix, pozwalając uruchomić ten sam skrypt wszędzie. To podstawa **pathlib image handling** w naszym tutorialu.

## Krok 2 – Zdefiniuj prostą klasę przetwarzania Batch OCR

Below is a lightweight wrapper that hides the threading boilerplate. It mirrors the pseudo‑code you saw earlier but is fully functional.

```python
import concurrent.futures
import pytesseract
from PIL import Image
import os

class BatchOcrProcessor:
    """Encapsulates multithreaded OCR logic."""

    def __init__(self):
        self.thread_count = os.cpu_count() or 4  # sensible default
        self.output_folder = pathlib.Path("ocr_results")
        self.output_folder.mkdir(parents=True, exist_ok=True)

    def set_thread_count(self, count: int):
        """Adjust the number of worker threads (OCR thread count optimization)."""
        if count < 1:
            raise ValueError("Thread count must be at least 1")
        self.thread_count = count
        print(f"Thread pool size set to {self.thread_count}")

    def set_output_folder(self, folder: str):
        """Where each OCR result will be saved (tesseract OCR batch processing)."""
        self.output_folder = pathlib.Path(folder)
        self.output_folder.mkdir(parents=True, exist_ok=True)
        print(f"Output folder set to {self.output_folder}")

    def _process_single(self, image_path: pathlib.Path):
        """Run OCR on a single image and write the text file."""
        try:
            img = Image.open(image_path)
            text = pytesseract.image_to_string(img)
            out_file = self.output_folder / f"{image_path.stem}.txt"
            out_file.write_text(text, encoding="utf-8")
            return f"✅ {image_path.name} → {out_file.name}"
        except Exception as exc:
            return f"❌ {image_path.name} failed: {exc}"

    def process(self, image_paths):
        """Run OCR on the entire batch using a thread pool."""
        print("🚀 Starting batch OCR...")
        with concurrent.futures.ThreadPoolExecutor(max_workers=self.thread_count) as executor:
            results = list(executor.map(self._process_single, image_paths))
        for line in results:
            print(line)
        print("🏁 Batch OCR completed.")
```

**Wyjaśnienie kluczowych wyborów**

- **ThreadPoolExecutor** zapewnia prawdziwe wielowątkowość dla zadań I/O, takich jak odczyt plików i wywoływanie zewnętrznego binarnego Tesseract.  
- Metoda `set_thread_count` to miejsce, w którym możesz eksperymentować z **OCR thread count optimization**; więcej wątków często oznacza większą przepustowość, aż do momentu, gdy rdzenie CPU zostaną nasycone.  
- Każdy obraz generuje plik `.txt` nazwany tak jak oryginalny PNG — idealny do późniejszego indeksowania lub wyszukiwania.

## Krok 3 – Połącz wszystko razem

Now we instantiate the processor, tweak the thread count, point it at our output folder, and finally hand it the list of images.

```python
if __name__ == "__main__":
    # 1️⃣ Gather PNGs (already done above)
    # 2️⃣ Create processor instance
    ocr_processor = BatchOcrProcessor()

    # 3️⃣ Configure thread pool – feel free to change 8 → your core count
    ocr_processor.set_thread_count(8)   # multithreaded OCR in Python

    # 4️⃣ Choose where results land
    ocr_processor.set_output_folder("YOUR_DIRECTORY/ocr_results")

    # 5️⃣ Run the batch – this call blocks until everything is done
    ocr_processor.process(image_files)

    # 6️⃣ All done – a friendly console message
    print("✅ All images processed. Check the ocr_results folder.")
```

Running the script will produce output similar to:

```
Found 42 PNG files to process.
Thread pool size set to 8
Output folder set to YOUR_DIRECTORY/ocr_results
🚀 Starting batch OCR...
✅ invoice_001.png → invoice_001.txt
✅ receipt_2023-04-15.png → receipt_2023-04-15.txt
...
🏁 Batch OCR completed.
✅ All images processed. Check the ocr_results folder.
```

Each `.txt` contains the raw OCR output. Open any file and you’ll see the extracted text ready for indexing, sentiment analysis, or whatever comes next.

Każdy plik `.txt` zawiera surowy wynik OCR. Otwórz dowolny plik, a zobaczysz wyodrębniony tekst gotowy do indeksowania, analizy sentymentu lub czegokolwiek, co nastąpi dalej.

## Krok 4 – Typowe pułapki i jak ich unikać

| Objaw | Prawdopodobna przyczyna | Rozwiązanie |
|---------|--------------|-----|
| Puste pliki `.txt` | Tesseract nie znajduje danych językowych lub obraz jest zbyt ciemny | Zainstaluj pakiety językowe (`tesseract-ocr-eng`) i przetwórz obrazy (zwiększ kontrast). |
| `UnicodeDecodeError` przy odczycie wyników | Wyjście zawiera znaki nie‑UTF‑8 | Zapisuj pliki z `encoding="utf-8"` (już w kodzie) lub użyj `errors="ignore"` jako szybkie obejście. |
| Wzrost zużycia CPU, brak przyspieszenia | Liczba wątków przekracza fizyczne rdzenie | Zredukuj `set_thread_count` do `os.cpu_count()` lub niższej wartości. |
| `FileNotFoundError` przy otwieraniu obrazu | Ścieżka zawiera znaki nie‑ASCII w Windows | Dodaj przedrostek `r` do łańcucha lub używaj bezpośrednio obiektów `pathlib` (tak jak my). |

## Krok 5 – Rozszerzanie tutorialu (kolejne kroki)

- **Dodaj przetwarzanie obrazu** przy użyciu OpenCV (`cv2`) w celu poprawy dokładności OCR (np. prostowanie, progowanie).  
- **Równoległość na wielu maszynach** przy użyciu `multiprocessing` lub prostej kolejki zadań takiej jak RabbitMQ dla ogromnych obciążeń.  
- **Integracja z silnikiem wyszukiwania** (Elasticsearch), aby wyodrębniony tekst był przeszukiwalny w czasie rzeczywistym.  
- **Zamień Tesseract na chmurowe API OCR** (Google Vision, Azure Computer Vision), jeśli potrzebujesz wyższej dokładności przy ręcznym piśmie.

All of these ideas build on the foundation you now have: a clean, **python batch ocr tutorial** that works out of the box.

---

## Zakończenie

You’ve just built a complete **python batch ocr tutorial** that:

1. **Zbiera** każdy PNG przy użyciu **pathlib image handling**.  
2. **Uruchamia** **multithreaded OCR in Python** pulę pracowników.  
3. **Optymalizuje** liczbę wątków dla Twojego sprzętu (**OCR thread count optimization**).  
4. **Zapisuje** każdy wynik do dedykowanego folderu (**tesseract OCR batch processing**).  

The script is ready to drop into any pipeline, whether you’re processing receipts, legal documents, or a mountain of screenshots. Play with the thread count, throw in image pre‑processing, or hook the output into a database—your choice.

Got questions? Feel free to comment below, and happy coding!

![Diagram przepływu python batch ocr tutorial przetwarzającego wiele plików PNG równolegle](/images/python-batch-ocr-workflow.png){.center width=600 alt="Diagram przepływu python batch ocr tutorial"}

---


## Co powinieneś nauczyć się dalej?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Samouczek Aspose OCR – Rozpoznawanie znaków optycznych](/ocr/english/)
- [Jak przetwarzać wsadowo obrazy OCR z listą w Aspose.OCR dla .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Wyodrębnianie tekstu z obrazu w C# z wyborem języka przy użyciu Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}