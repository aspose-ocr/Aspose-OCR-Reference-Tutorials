---
category: general
date: 2026-06-16
description: Wyodrębnij tekst z plików TIFF przy użyciu OCR w Pythonie. Dowiedz się,
  jak krok po kroku konwertować TIFF na tekst, obsługując wielostronicowe dokumenty
  z łatwością.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: pl
og_description: Wyodrębnij tekst z plików TIFF za pomocą OCR w Pythonie. Skorzystaj
  z tego przewodnika, aby przekonwertować TIFF na tekst, obsłużyć skany wielostronicowe
  i uzyskać czyste wyniki.
og_title: Wyodrębnij tekst z TIFF – Kompletny przewodnik Pythona
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: Wyodrębnij tekst z TIFF – Kompletny przewodnik Pythona
url: /pl/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnianie tekstu z TIFF – Kompletny przewodnik w Pythonie

Kiedykolwiek potrzebowałeś **wyodrębnić tekst z obrazów TIFF**, ale nie wiedziałeś od czego zacząć? Nie jesteś sam — wielu programistów napotyka ten problem przy pracy ze zeskanowanymi archiwami lub starszymi dokumentami. Dobra wiadomość? Kilka linijek Pythona pozwoli Ci **przekształcić TIFF w tekst** w mgnieniu oka, nawet gdy plik zawiera dziesiątki stron.

W tym tutorialu przejdziemy przez rzeczywisty przykład: wczytanie wielostronicowego TIFF, ustawienie języka OCR na francuski i wyciągnięcie rozpoznanego tekstu z każdej strony. Po zakończeniu będziesz mieć gotowy do uruchomienia skrypt, zrozumiesz, dlaczego każdy krok ma znaczenie, i będziesz wiedział, jak dostosować go do innych języków lub formatów obrazów.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz:

- Python 3.8 lub nowszy.
- Pakiet `ocr` (lub dowolną kompatybilną bibliotekę OCR oferującą klasę `OcrEngine`). Zainstalujesz go poleceniem `pip install ocr-lib` — zamień nazwę na rzeczywistą, której używasz.
- Wielostronicowy plik TIFF (np. `french-scans.tif`), który chcesz przetworzyć.
- Podstawową znajomość skryptów w Pythonie.

Bez ciężkich zależności, bez zewnętrznych usług — tylko czysty Python i silnik OCR.

---

## Krok 1: Skonfiguruj silnik OCR do **wyodrębniania tekstu z TIFF**

Najpierw potrzebujemy instancji silnika OCR i musimy określić, którego języka ma używać. W naszym przypadku materiał źródłowy jest po francusku, więc ustawimy język odpowiednio.

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**Dlaczego to ważne:**  
Ustawienie języka znacząco poprawia dokładność. Francuskie znaki takie jak „é” czy „ç” byłyby odczytywane jako ogólne symbole, gdyby silnik domyślnie używał angielskiego. Wybierając francuski, dostarczamy silnikowi właściwą mapę znaków.

> **Wskazówka:** Jeśli przetwarzasz dokumenty w wielu językach, możesz zmieniać `engine.language` w locie przed każdym wywołaniem `recognize()`.

---

## Krok 2: Wczytaj wielostronicowy TIFF, który chcesz **przekształcić w tekst**

TIFF może zawierać kilka klatek — myśl o każdej klatce jako o osobnej stronie. Biblioteka OCR abstrahuje to za nas, więc po prostu wskazujemy plik.

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**Uwaga na przypadki brzegowe:**  
Jeśli ścieżka do pliku jest nieprawidłowa lub TIFF jest uszkodzony, metoda `load_from_file` zgłosi wyjątek. W kodzie produkcyjnym otocz ją blokiem `try/except`:

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

---

## Krok 3: Uruchom OCR na całym dokumencie – rdzeń **wyodrębniania tekstu z TIFF**

Teraz pozwalamy silnikowi wykonać swoją magię. Wywołanie `recognize()` przetwarza wszystkie strony jednocześnie i zwraca bogaty obiekt wynikowy.

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**Co się dzieje pod maską?**  
Silnik iteruje po każdej klatce, stosuje wstępne przetwarzanie (prostowanie, binaryzację), uruchamia sieć neuronową i agreguje wynik. Ponieważ wywołaliśmy `recognize()` tylko raz, biblioteka może współdzielić zasoby między stronami, co jest szybsze niż ręczne pętlowanie.

---

## Krok 4: Wyciągnij rozpoznany tekst z wyniku JSON – **przekształć TIFF w tekst** strona po stronie

Obiekt wynikowy można zserializować do JSON. W tym JSON znajdziesz tablicę `pages`, z której każda zawiera pole `text`.

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

Teraz mamy czystą listę Pythona, w której każdy element odpowiada wynikowi OCR jednej strony.

---

## Krok 5: Wydrukuj lub zapisz tekst dla każdej strony – ostatni element **wyodrębniania tekstu z TIFF**

Przejdźmy przez strony i wyświetlmy wyodrębniony tekst. Możesz także zapisać każdą stronę do osobnego pliku `.txt`, jeśli wolisz.

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### Oczekiwany wynik (przykład)

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

Jeśli OCR się powiódł, zobaczysz czysty blok francuskich zdań dla każdej strony. Jeśli zauważysz zniekształcone znaki, sprawdź ponownie ustawienie języka lub rozważ zwiększenie rozdzielczości obrazu przed OCR.

---

## Radzenie sobie z typowymi problemami przy **przekształcaniu TIFF w tekst**

| Problem | Dlaczego się pojawia | Szybka naprawa |
|---------|----------------------|----------------|
| **Pusta tablica `pages`** | TIFF nie został poprawnie wczytany lub nie zawiera klatek. | Sprawdź ścieżkę do pliku i upewnij się, że TIFF nie jest jednokartą PNG podszywającą się pod TIFF. |
| **Zniekształcone znaki** | Nieprawidłowy język lub niska jakość obrazu. | Ustaw właściwy `engine.language` i wstępnie przetwórz obraz (np. zwiększ DPI). |
| **Wzrost zużycia pamięci przy dużych TIFF** | Ładowanie wszystkich stron naraz pochłania RAM. | Przetwarzaj w partiach: wczytaj jedną klatkę, rozpoznaj, usuń przed przejściem do kolejnej. |
| **Błędy Unicode przy drukowaniu** | Kodowanie konsoli nie obsługuje znaków akcentowanych. | Użyj `print(page["text"].encode('utf-8').decode('utf-8'))` lub skonfiguruj terminal na UTF‑8. |

---

## Rozszerzanie skryptu: od **wyodrębniania tekstu z TIFF** do przetwarzania wsadowego

Teraz, gdy masz solidne podstawy, rozważ następujące kroki:

1. **Konwersja wsadowa** – Owiń cały przepływ w funkcję `def ocr_tiff(path):` i iteruj po katalogu plików TIFF.
2. **Zapis do plików** – Zamiast drukować, zapisz tekst każdej strony do `page_{i}.txt` lub połącz wszystko w jeden dokument.
3. **Alternatywne silniki OCR** – Jeśli potrzebujesz wyższej dokładności, zamień `ocr.OcrEngine()` na Tesseract (`pytesseract`) lub Azure Cognitive Services — zachowaj tę samą logikę „wyodrębniania tekstu z TIFF”.
4. **Post‑processing** – Uruchom sprawdzanie pisowni, wykrywanie języka lub czyszczenie regexem, aby uporządkować surowy wynik OCR.

---

## Pełny, gotowy do uruchomienia skrypt

Poniżej znajduje się kompletny kod, gotowy do skopiowania i wklejenia. Zawiera podstawową obsługę błędów oraz opcjonalny zapis tekstu każdej strony do osobnych plików.

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

Uruchom ten skrypt, wskaż `tiff_file` na swój dokument i obserwuj, jak konsola wypełnia się czystymi francuskimi zdaniami. Jeśli podasz `out_folder`, znajdziesz tam serię plików `page_#.txt` gotowych do dalszego przetwarzania.

---

## Zakończenie

Właśnie **wyodrębniliśmy tekst z plików TIFF** przy użyciu prostego przepływu OCR w Pythonie i teraz wiesz, jak **przekształcić TIFF w tekst** w sposób niezawodny. Od inicjalizacji silnika z odpowiednim językiem, po iterację po wynikach JSON każdej strony — każdy krok został wyjaśniony wraz z „dlaczego”, abyś mógł dostosować ten wzorzec do innych języków, formatów obrazów czy większych zadań wsadowych.

Co dalej? Spróbuj zamienić backend OCR na Tesseract, poeksperymentuj z różnymi pakietami językowymi lub zintegrować wynik z bazą danych przeszukiwalną. Nie ma granic, gdy możesz pewnie zamienić zeskanowane obrazy w przeszukiwalny tekst.

Śmiało zostaw komentarz, jeśli napotkasz problemy lub masz pomysły na dalsze usprawnienia. Szczęśliwego kodowania!

## Co warto nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz szczegółowe wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}