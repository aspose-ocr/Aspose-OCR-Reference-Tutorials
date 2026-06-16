---
category: general
date: 2026-03-26
description: Jak efektywnie przetwarzać OCR wsadowo w Pythonie — dowiedz się, jak
  wyodrębniać tekst z obrazów i konwertować PDF przy użyciu OCR z równoległym przetwarzaniem.
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: pl
og_description: Jak efektywnie przetwarzać OCR wsadowo — przewodnik krok po kroku,
  jak wyodrębnić tekst z obrazów, konwersja PDF do OCR i wsadowe przetwarzanie OCR
  przy użyciu Pythona.
og_title: 'Jak wykonywać OCR wsadowo: szybkie równoległe wyodrębnianie tekstu'
tags:
- OCR
- Python
- Parallel Computing
title: 'Jak przetwarzać OCR wsadowo: szybkie równoległe wyodrębnianie tekstu'
url: /pl/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak przetwarzać OCR wsadowo: szybkie równoległe wyodrębnianie tekstu

Zastanawiałeś się kiedyś **jak przetwarzać OCR wsadowo**, gdy masz dziesiątki zeskanowanych stron, zrzutów ekranu i plików PDF leżących wokół? Nie jesteś jedyny — większość programistów napotyka ten sam problem: przetwarzanie każdego pliku pojedynczo staje się bolesnym wąskim gardłem.  

Dobre wieści są takie, że możesz uruchomić kilka wątków pracowników, podać im wszystkie swoje pliki i obserwować, jak silnik OCR przetwarza wsad równolegle. W tym samouczku przeprowadzimy kompletny, gotowy do uruchomienia przykład, który pokazuje **wyodrębnianie tekstu z obrazów**, wykonuje **konwersję PDF OCR** oraz wykorzystuje **równoległe przetwarzanie OCR** dla zwiększenia szybkości.

> **Co wyniesiesz z tego**  
> * W pełni funkcjonalny skrypt w Pythonie, który przetwarza mieszany zestaw plików PNG, TIFF, PDF i JPG jednorazowo.  
> * Zrozumienie, dlaczego pula wątków przyspiesza zadania OCR o charakterze I/O‑bound.  
> * Wskazówki dotyczące obsługi błędów, dużych plików PDF oraz niestandardowych liczby wątków.  

## Wymagania wstępne

Zanim zanurkujemy, upewnij się, że masz:

| Wymaganie | Powód |
|-----------|-------|
| Python 3.8+ | Nowoczesna składnia & `concurrent.futures` |
| `ocr` library (lub dowolny kompatybilny wrapper OCR) | Udostępnia `OcrBatchProcessor` oraz obiekty wyników |
| Kilka przykładowych plików (PNG, TIFF, PDF, JPG) | Aby zobaczyć **wyodrębnianie tekstu z obrazów** w praktyce |
| Podstawowa znajomość wątków (opcjonalnie) | Przydatna, ale nieobowiązkowa |

Jeśli jeszcze nie zainstalowałeś pakietu `ocr`, uruchom:

```bash
pip install ocr-lib   # replace with the actual package name
```

Teraz, gdy środowisko jest gotowe, rozbijmy problem na części.

## Krok 1: Importuj pomocnicze funkcje i utwórz procesor wsadowy

Pierwszą rzeczą, której potrzebujemy, jest miejsce do zbierania wszystkich zadań OCR. Klasa `OcrBatchProcessor` robi dokładnie to — kolejkowuje elementy pracy i zwraca listę obiektów `Future`.

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*Dlaczego to ważne*: Importowanie `as_completed` pozwala nam reagować na każde zakończone zadanie natychmiast, zamiast czekać na najwolniejszy plik. To jest sedno **wsadowego przetwarzania OCR**.

## Krok 2: Dostosuj pulę pracowników do równoległego wykonywania

Domyślnie procesor może używać jednego wątku, co podważa sens wsadowania. Jawnie prosimy o czterech pracowników — możesz zwiększyć tę liczbę do liczby rdzeni CPU, które posiadasz.

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*Wskazówka*: W przypadku zadań I/O‑bound, takich jak OCR, często uzyskuje się malejące zyski po `CPU cores * 2`. Przetestuj kilka wartości i wybierz optymalny punkt.

## Krok 3: Dodaj do kolejki każdy plik, który chcesz poddać OCR

Tutaj dodajemy mieszankę plików obrazów i PDF. Metoda `add` po prostu zapisuje ścieżkę; rzeczywista praca nie rozpocznie się, dopóki nie wyślemy wsadu.

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

Jeśli potrzebujesz przetworzyć cały folder, szybka pętla `glob` zrobi robotę:

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## Krok 4: Uruchom zadania i zbierz obiekty Future

Wywołanie `submit_all` daje procesorowi zielone światło. Zwraca listę obiektów `Future` — traktuj je jako miejsca na wyniki, które pojawią się później.

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

W tym momencie silnik OCR pracuje w tle, każdy wątek żuje kolejny plik.

## Krok 5: Pobieraj wyniki, gdy tylko się zakończą

Używając `as_completed` iterujemy po obiektach Future w kolejności ich zakończenia, a nie w kolejności ich zgłoszenia. Dzięki temu nasz skrypt pozostaje responsywny, szczególnie gdy niektóre PDFy trwają dłużej niż proste PNG.

```python
# Step 5 – retrieve each result as it completes
for future in as_completed(ocr_futures):
    try:
        ocr_result = future.result()          # May raise if the job failed
        print("Batch result:\n", ocr_result.get_text())
    except Exception as exc:
        # Graceful error handling – you can log or retry here
        print(f"An OCR job failed: {exc}")
```

**Oczekiwany wynik** (skrócony dla zwięzłości):

```
Batch result:
 The quick brown fox jumps over the lazy dog.
...
Batch result:
 Invoice #12345
 Date: 2026-03-01
 Total: $1,234.56
...
```

Każdy blok odpowiada tekstowej reprezentacji oryginalnego pliku. Jeśli wykonujesz **konwersję PDF OCR**, tekst będzie zawierał wszystko, co silnik OCR potrafił odczytać z każdej strony.

## Obsługa przypadków brzegowych i typowych pułapek

| Sytuacja | Na co zwrócić uwagę | Szybka naprawa |
|----------|---------------------|----------------|
| Uszkodzony obraz | `future.result()` podnosi `OSError` | Obejmij w `try/except` (zobacz kod powyżej) |
| Bardzo duże pliki PDF ( > 100 MB ) | Presja pamięci, wolniejsze wątki | Zwiększ `thread_count` umiarkowanie lub najpierw podziel PDF na rozdziały |
| Dokumenty wielojęzyczne | Domyślny model OCR może błędnie rozpoznawać | Przekaż wskazówki językowe do `OcrBatchProcessor`, jeśli biblioteka to obsługuje |
| Potrzeba zachowania układu | Zwykłe `get_text()` traci kolumny | Użyj `ocr_result.get_hocr()` lub podobnej metody uwzględniającej układ |

### Wskazówka: Niestandardowa liczba wątków w zależności od typu pliku

Jeśli wiesz, że większość twojego obciążenia to PDFy, możesz przydzielić więcej wątków dla nich i mniej dla małych PNG. Niektóre biblioteki pozwalają przekazać `priority` dla każdego zadania; w przeciwnym razie możesz utworzyć dwa osobne wsady — jeden dla obrazów, drugi dla PDFów — i uruchomić je równocześnie.

## Przegląd wizualny (opcjonalnie)

![how to batch ocr workflow diagram](https://example.com/ocr-workflow.png "how to batch ocr workflow")

*Diagram ilustruje przepływ od wykrywania plików → tworzenia wsadu → równoległego wykonania → agregacji wyników.*

## Pełny skrypt, który możesz skopiować i wkleić

Poniżej znajduje się cały program, gotowy do wstawienia do pliku `.py`. Zawiera wszystkie powyższe fragmenty kodu oraz mały pomocnik, który automatycznie wykrywa obsługiwane pliki w katalogu.

```python
#!/usr/bin/env python3
"""
How to Batch OCR – Complete Example
-----------------------------------
This script demonstrates parallel OCR processing of mixed image and PDF files.
It shows how to extract text from images, perform pdf ocr conversion, and
handle errors gracefully.
"""

from concurrent.futures import as_completed
import pathlib, fnmatch, sys
import ocr  # replace with your actual OCR library import

def discover_files(root_dir):
    """Yield paths of supported OCR files under *root_dir*."""
    for path in pathlib.Path(root_dir).rglob("*"):
        if fnmatch.fnmatch(path.suffix.lower(), ".png") \
           or fnmatch.fnmatch(path.suffix.lower(), ".tif") \
           or fnmatch.fnmatch(path.suffix.lower(), ".pdf") \
           or fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
            yield str(path)

def main(directory, workers=4):
    # 1️⃣ Initialise batch processor
    ocr_batch = ocr.OcrBatchProcessor()
    ocr_batch.set_thread_count(workers)

    # 2️⃣ Queue every discovered file
    for file_path in discover_files(directory):
        ocr_batch.add(file_path)

    # 3️⃣ Submit all jobs
    futures = ocr_batch.submit_all()

    # 4️⃣ Process results as they arrive
    for fut in as_completed(futures):
        try:
            result = fut.result()
            print("=== OCR RESULT ===")
            print(result.get_text())
            print("\n---\n")
        except Exception as e:
            print(f"[ERROR] OCR failed for a job: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-files>")
        sys.exit(1)
    main(sys.argv[1])
```

Zapisz to jako `batch_ocr.py`, wskaż folder zawierający twoje skany i obserwuj, jak konsola wypełnia się wyodrębnionym tekstem.  

### Dlaczego to działa

* **Thread pool** – OCR w dużej mierze czeka na operacje I/O dysku i wywołania zewnętrznego silnika, więc wiele wątków utrzymuje CPU zajęte.  
* **`as_completed`** – Otrzymujesz wyniki natychmiast, gdy są gotowe, co jest idealne dla informacji zwrotnej w UI lub potoków strumieniowych.  
* **Error isolation** – Jeden uszkodzony plik nie zniszczy całego wsadu; blok `try/except` izoluje błędy.

## Zakończenie

W skrócie, teraz wiesz **jak przetwarzać OCR wsadowo** używając `concurrent.futures` w Pythonie wraz z biblioteką OCR obsługującą przetwarzanie wsadowe. Konfigurując umiarkowaną pulę wątków, kolejkowując każdy obsługiwany plik i pobierając wyniki w miarę ich zakończenia, osiągasz szybkie **równoległe przetwarzanie OCR** bez utraty niezawodności.  

Od tego momentu możesz:

* Podłączyć wyjście do indeksu wyszukiwania w celu szybkiego odnajdywania dokumentów.  
* Rozszerzyć skrypt, aby zapisywał każdy wynik do pliku `.txt` obok oryginału.  
* Zastąpić wbudowaną pulę wątków `asyncio`, jeśli twoja biblioteka OCR oferuje asynchroniczne API.  

Kontynuuj eksperymenty — wymień na Tesseract, Azure Cognitive Services lub Google Vision, a zobaczysz, że ten sam wzorzec działa. Szczęśliwego OCR-owania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}