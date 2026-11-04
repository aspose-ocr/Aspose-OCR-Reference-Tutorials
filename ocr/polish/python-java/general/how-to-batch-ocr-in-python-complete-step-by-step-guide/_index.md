---
category: general
date: 2026-06-28
description: Jak wykonywać OCR wsadowo w Pythonie. Naucz się przetwarzać OCR wielu
  obrazów, wyodrębniać tekst z plików PNG oraz konwertować obraz na tekst w pełnym
  samouczku OCR w Pythonie.
draft: false
keywords:
- how to batch OCR
- ocr multiple images
- extract text from png
- convert image to text
- python ocr tutorial
language: pl
og_description: Jak wykonywać OCR wsadowo w Pythonie, wyjaśnione w pierwszym zdaniu.
  Skorzystaj z tego tutorialu OCR w Pythonie, aby efektywnie wyodrębniać tekst z plików
  PNG.
og_title: Jak wykonać wsadowe OCR w Pythonie – Pełny przewodnik programistyczny
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  headline: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  name: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Why set the language?**'
    text: '**Why set the language?**'
  - name: '**Why use a batch operation?**'
    text: '**Why use a batch operation?**'
  - name: '**Why a ThreadPoolExecutor?**'
    text: '**Why a ThreadPoolExecutor?**'
  - name: '**Why enumerate the results?**'
    text: '**Why enumerate the results?**'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Jak wykonywać OCR wsadowo w Pythonie – Kompletny przewodnik krok po kroku
url: /pl/python-java/general/how-to-batch-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonywać OCR wsadowo w Pythonie – Kompletny przewodnik krok po kroku

Zastanawiałeś się kiedyś **jak wykonywać OCR wsadowo** stos zeskanowanych stron bez pisania pętli blokującej interfejs użytkownika? Nie jesteś jedyny. Przetwarzanie dziesiątek plików PNG jeden po drugim może przypominać obserwowanie schnącej farby, szczególnie gdy każde zdjęcie zajmuje sekundę lub dwie na dekodowanie.  

W tym samouczku pokażemy Ci czysty, nieblokujący sposób na **OCR wielu obrazów** jednocześnie, **wyodrębnianie tekstu z plików PNG** oraz **konwersję obrazu na tekst** przy użyciu nowoczesnego silnika OCR w Pythonie. Po zakończeniu będziesz mieć gotowy do uruchomienia skrypt, który możesz wkleić do dowolnego projektu – idealny do szybkiego *python ocr tutorial* lub produkcyjnego zadania wsadowego.

## Co zbudujesz

- Zainicjalizuj silnik OCR i ustaw jego język na łaciński (lub dowolny potrzebny język).  
- Przekaż silnikowi listę ścieżek do obrazów (PNG w naszym przykładzie).  
- Uruchom operację wsadową, która zwraca obiekt podobny do Future.  
- Pobierz wszystkie wyniki równocześnie przy użyciu puli wątków, pozostawiając główny wątek wolny.  
- Wydrukuj rozpoznany tekst dla każdej strony, ładnie oddzielony.

Bez ukrytej magii, po prostu czysty Python i zewnętrzna biblioteka OCR (użyjemy fikcyjnego pakietu `pyocr` w celach ilustracyjnych).  

**Wymagania wstępne**  
- Zainstalowany Python 3.8+.  
- Podstawowa znajomość funkcji Pythona i `concurrent.futures`.  
- Dostęp do biblioteki OCR udostępniającej klasę `OcrEngine` (np. `pip install pyocr`).  

Jeśli czegoś brakuje, zdobądź to teraz – jest to łatwiejsze niż myślisz.

---

## Jak wykonywać OCR wsadowo w Pythonie – Podstawowe koncepcje

Zanim zanurkujemy w kod, odpowiedzmy na pytanie „dlaczego” stojące za każdym krokiem.

1. **Dlaczego ustawia się język?**  
   Dokładność OCR rośnie gwałtownie, gdy silnik wie, jakie znaki ma oczekiwać. Łacina działa dla angielskiego, francuskiego, hiszpańskiego itp. W razie potrzeby przełącz na `Language.Japanese` lub `Language.Arabic`.

2. **Dlaczego używać operacji wsadowej?**  
   Wywołanie wsadowe pozwala silnikowi wewnętrznie planować pracę, często wykorzystując natywne wątki lub przyspieszenie GPU. Zwraca uchwyt, który możesz odpytać później, co oznacza, że nie blokujesz podczas przetwarzania każdego obrazu.

3. **Dlaczego ThreadPoolExecutor?**  
   Obiekt Future, który otrzymujemy, jest *leniwy* – zaczyna pobierać wyniki dopiero, gdy o to poprosimy. Przekazując pulę wątków do `getAll`, pozwalamy Pythonowi pobierać tekst każdej strony równolegle, co znacząco skraca całkowity czas wykonania.

4. **Dlaczego enumerować wyniki?**  
   Kolejność wyników odpowiada kolejności ścieżek wejściowych, więc możemy bezpiecznie oznaczyć numer każdej strony.

Zrozumienie tych „dlaczego” pomaga dostosować wzorzec do innych bibliotek lub większych zestawów danych.

---

## Krok 1: Zainstaluj i zaimportuj wymagane pakiety

Najpierw upewnij się, że biblioteka OCR jest zainstalowana. Przykład używa ogólnego pakietu `pyocr`; zamień go na rzeczywistą bibliotekę, której preferujesz (np. `pytesseract`, `easyocr`).

```bash
pip install pyocr
```

Teraz zaimportuj wszystko, czego potrzebujesz.

```python
# Standard library imports
import concurrent.futures
from pathlib import Path

# Third‑party OCR library (hypothetical)
from pyocr import OcrEngine, Language
```

> **Wskazówka:** Użycie `Path` z `pathlib` sprawia, że Twój skrypt jest niezależny od systemu operacyjnego i łatwiejszy do odczytania.

---

## Krok 2: Utwórz silnik OCR i ustaw język

Tworzenie silnika jest proste. Zablokujemy go na łacinę w tym demo.

```python
# Step 2: Initialise the OCR engine
engine = OcrEngine()
engine.setLanguage(Language.Latin)   # Change to Language.YourChoice if needed
```

Wywołanie `setLanguage` jest opcjonalne w niektórych silnikach, ale to dobra praktyka. Informuje model OCR, aby skupił się na zestawie znaków, który Cię interesuje, poprawiając zarówno szybkość, jak i dokładność.

---

## Krok 3: Wymień pliki obrazów do przetworzenia (Wyodrębnianie tekstu z PNG)

Zbierz wszystkie pliki PNG, które chcesz przekonwertować. Użycie `Path.glob` pozwala wrzucić cały folder bez edytowania skryptu.

```python
# Step 3: Gather PNG images – this is the “extract text from png” part
image_dir = Path("YOUR_DIRECTORY")   # Replace with your actual folder
image_paths = sorted(image_dir.glob("*.png"))   # Returns a list of Path objects

# Convert Path objects to strings for the OCR library (if required)
image_paths = [str(p) for p in image_paths]

if not image_paths:
    raise FileNotFoundError("No PNG files found in the specified directory.")
```

> **Dlaczego to ważne:** Sortując listę, zapewniamy deterministyczną kolejność, co później dopasowuje każdy wynik do właściwego numeru strony.

---

## Krok 4: Uruchom operację OCR wsadową (Konwersja obrazu na tekst)

Teraz przekazujemy listę silnikowi. Metoda zwraca kontener podobny do Future, który odpyta się później.

```python
# Step 4: Start batch OCR – returns a Future‑like object
batch_future = engine.ocrBatch(image_paths)
```

Pod maską silnik może uruchomić własne wątki robocze lub nawet pipeline GPU. Wszystko, na czym nam zależy, to posiadanie uchwytu (`batch_future`), który wie, jak pobrać poszczególne wyniki.

---

## Krok 5: Pobierz wszystkie wyniki równocześnie (OCR wielu obrazów)

Tutaj naprawdę *wsadzamy* pracę w tryb wsadowy. Przekazując `ThreadPoolExecutor` do `getAll`, tekst każdej strony jest pobierany w osobnym wątku.

```python
# Step 5: Pull results using a thread pool – this speeds up OCR multiple images
with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    # getAll returns a list of Result objects in the same order as image_paths
    results = batch_future.getAll(executor)
```

Możesz dostosować `max_workers` w zależności od liczby rdzeni CPU lub zaleceń biblioteki OCR. Więcej pracowników ≠ zawsze szybciej – obserwuj zużycie CPU.

---

## Krok 6: Wyświetl rozpoznany tekst (Zakończenie tutorialu Python OCR)

Na koniec wydrukuj tekst każdej strony. Obiekt `Result` udostępnia `getText()` – dostosuj, jeśli Twoja biblioteka używa innej nazwy metody.

```python
# Step 6: Display the recognised text for each page
for i, result in enumerate(results):
    print(f"--- Page {i + 1} ---")
    print(result.getText())
    print()   # Blank line for readability
```

**Oczekiwany wynik (przykład)**

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna...

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco...
```

Jeśli którykolwiek obraz się nie powiedzie, większość silników zwróci pusty ciąg lub podniesie wyjątek – możesz otoczyć pętlę blokiem `try/except`, aby elegancko obsłużyć przypadki brzegowe.

---

## Pełny skrypt – Gotowy do uruchomienia

Poniżej znajduje się kompletny, samodzielny skrypt. Skopiuj i wklej go do pliku o nazwie `batch_ocr.py`, dostosuj `YOUR_DIRECTORY` i uruchom `python batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script – processes all PNG files in a directory.
Demonstrates how to batch OCR, OCR multiple images, extract text from PNG,
and convert image to text using a Python OCR engine.
"""

import concurrent.futures
from pathlib import Path

# Replace with your actual OCR library import
from pyocr import OcrEngine, Language

def main():
    # Initialise OCR engine
    engine = OcrEngine()
    engine.setLanguage(Language.Latin)

    # Locate PNG files
    image_dir = Path("YOUR_DIRECTORY")          # <‑‑ change this
    image_paths = sorted(image_dir.glob("*.png"))
    image_paths = [str(p) for p in image_paths]

    if not image_paths:
        raise FileNotFoundError("No PNG files found in the specified directory.")

    # Start batch OCR
    batch_future = engine.ocrBatch(image_paths)

    # Retrieve results concurrently
    with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
        results = batch_future.getAll(executor)

    # Print each page's recognised text
    for i, result in enumerate(results):
        print(f"--- Page {i + 1} ---")
        print(result.getText())
        print()

if __name__ == "__main__":
    main()
```

Zapisz, uruchom i obserwuj, jak konsola wypełnia się wyodrębnionym tekstem. Proste, szybkie i w pełni asynchroniczne.

---

## Częste pułapki i jak ich unikać

| Problem | Dlaczego się pojawia | Rozwiązanie |
|---------|----------------------|-------------|
| **Brak wyjścia** – puste ciągi | Silnik OCR nie znalazł żadnego tekstu (obraz zbyt zaszumiony) | Wstępnie przetwórz obrazy: binaryzuj, prostuj lub zwiększ DPI |
| **`FileNotFoundError`** | Nieprawidłowa ścieżka katalogu lub brak plików PNG | Sprawdź ponownie `YOUR_DIRECTORY` i upewnij się, że pliki kończą się na `.png` |
| **Wysokie użycie CPU** | `max_workers` ustawiony zbyt wysoko dla Twojej maszyny | Zmniejsz `max_workers` lub włącz przyspieszenie GPU, jeśli jest wspierane |
| **Zniekształcony Unicode** | Silnik domyślnie używał innego języka | Wywołaj `engine.setLanguage(Language.Latin)` (lub odpowiedni) przed wsadowym OCR |

---

## Rozszerzanie tutorialu – Kolejne kroki

- **OCR wielu obrazów** w innych formatach (JPEG, TIFF) – po prostu zmień wzorzec glob.  
- **Wyodrębnij tekst z PNG** i wprowadź go do indeksu wyszukiwania (np. Elasticsearch).  
- **Konwertuj obraz na tekst** w celu generowania PDF przy użyciu `reportlab` lub `PyPDF2`.  
- **Równoległość na wielu maszynach** przy użyciu `multiprocessing` lub kolejki zadań takiej jak Celery dla ogromnych zbiorów danych.  

Każdy z tych tematów naturalnie rozwija **python ocr tutorial**, który właśnie ukończyłeś.

---

## Zakończenie

Przeszliśmy przez **jak wykonywać OCR wsadowo** na kolekcji plików PNG, pokazaliśmy moc API zorientowanego na wsadowe przetwarzanie i przedstawiliśmy, jak **wyodrębnić tekst z PNG** przy użyciu podejścia opartego na puli wątków. Pełny skrypt powyżej jest gotowy do produkcji, a Ty masz teraz solidną bazę dla każdego projektu Pythona intensywnie wykorzystującego OCR.

Wypróbuj go, dostosuj ustawienia języka i może nawet zamień `pyocr` na `pytesseract` – wzorzec pozostaje ten sam. Masz pytania lub chcesz podzielić się ciekawym przypadkiem użycia? Dodaj komentarz i kontynuujmy rozmowę.

*Szczęśliwego kodowania!*

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Wyodrębnij tekst z obrazu przy użyciu Aspose OCR – przewodnik krok po kroku](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Wyodrębnij tekst z obrazów przy użyciu operacji OCR na folderach](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Jak wykonywać OCR wsadowo na obrazach z listą w Aspose.OCR dla .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}