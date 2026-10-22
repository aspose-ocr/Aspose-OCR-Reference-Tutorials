---
category: general
date: 2026-07-05
description: Jak używać OCR w Pythonie, aby szybko konwertować pliki TIFF na tekst.
  Poznaj kroki biblioteki OCR w Pythonie do wyodrębniania tekstu z obrazów TIFF i
  budowania silnika OCR w Pythonie.
draft: false
keywords:
- how to use ocr
- ocr library python
- convert tiff to text
- extract text from tiff
- python ocr engine
language: pl
og_description: Jak używać OCR w Pythonie? Ten przewodnik pokazuje krok po kroku,
  jak konwertować pliki TIFF na tekst przy użyciu silnika OCR w Pythonie oraz biblioteki
  OCR w Pythonie.
og_title: Jak używać OCR w Pythonie – Pełne wyodrębnianie tekstu z plików TIFF
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  headline: How to Use OCR in Python – Extract Text from TIFF
  type: TechArticle
- description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  name: How to Use OCR in Python – Extract Text from TIFF
  steps:
  - name: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
    text: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
  - name: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
    text: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
  - name: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
    text: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Image Processing
title: Jak używać OCR w Pythonie – wyodrębnianie tekstu z pliku TIFF
url: /pl/python-java/general/how-to-use-ocr-in-python-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać OCR w Pythonie – Ekstrahowanie tekstu z TIFF

Zastanawiałeś się kiedyś **jak używać OCR w Pythonie**, aby zamienić zeskanowaną książkę na edytowalny tekst? Nie jesteś jedyny — programiści, badacze i hobbystowie napotykają ten sam problem przy pracy z wielostronicowymi obrazami TIFF. Dobra wiadomość? Dzięki **ocr library python** możesz uruchomić mały silnik OCR, skierować go na plik TIFF i w kilka sekund uzyskać czysty, przeszukiwalny tekst.

W tym samouczku przejdziemy przez wszystko, co potrzebne: instalację odpowiedniego pakietu, wczytanie wielostronicowego TIFF, uruchomienie silnika OCR i w końcu wypisanie zawartości każdej strony. Po zakończeniu będziesz w stanie **konwertować TIFF na tekst** oraz **wyodrębniać tekst z plików TIFF** bez wychodzenia z środowiska Pythona.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz:

- Python 3.9 lub nowszy (przykład testowano na 3.11)
- Aktualną wersję biblioteki `ocr` (lub dowolny kompatybilny `python ocr engine`, którego używasz)
- Wielostronicowy plik TIFF, który chcesz przetworzyć (nazwijmy go `scanned_book.tif`)
- Podstawową znajomość skryptów Pythona i wirtualnych środowisk

Nie potrzebujesz ciężkich zewnętrznych narzędzi — wystarczy pip i kilka linijek kodu.

## Zainstaluj OCR Library Python

Najpierw potrzebny jest solidny backend OCR. W tym przewodniku użyjemy fikcyjnego pakietu `ocr`, który dostarcza prostego API wysokiego poziomu, ale ten sam schemat działa z wrapperami opartymi na Tesseract, takimi jak `pytesseract`, lub komercyjnymi SDK.

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Pro tip:** Jeśli pracujesz w systemie Windows i pakiet wymaga natywnych binarek, upewnij się, że masz zainstalowany odpowiedni pakiet Visual C++ Redistributable. Instalator zazwyczaj ostrzeże Cię, jeśli czegoś brakuje.

## Jak używać silnika OCR w Pythonie

Teraz, gdy biblioteka jest gotowa, uruchomimy silnik OCR i skierujemy go na nasz plik TIFF. Poniższy fragment tworzy instancję silnika, ustawia język na angielski i przygotowuje go do przetwarzania wielostronicowego.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # You can switch to ocr.Language.FRENCH, etc.
```

**Dlaczego ustawiamy język?**  
Większość silników OCR używa modeli językowych, aby zwiększyć dokładność. Jeśli pominiesz ten krok, silnik przełączy się na model ogólny, który może błędnie rozpoznawać interpunkcję lub znaki specjalne.

## Wczytaj wielostronicowy obraz TIFF

Kolejnym krokiem jest wczytanie zeskanowanego dokumentu. Pomocnicza metoda `ocr.Image.load` rozumie stosy TIFF od razu, zwracając obiekt reprezentujący każdą stronę wewnętrznie.

```python
# Step 2: Load the multi‑page TIFF image containing the scanned book
tiff_path = "YOUR_DIRECTORY/scanned_book.tif"
tiff_image = ocr.Image.load(tiff_path)
```

> **Edge case:** Jeśli Twój TIFF używa kompresji (CCITT Group 4, LZW itp.) i biblioteka zgłasza błąd, spróbuj najpierw skonwertować go na wersję nieskompresowaną przy pomocy ImageMagick:
> ```bash
> convert scanned_book.tif -compress none scanned_book_uncompressed.tif
> ```

## Przeprowadź OCR na wszystkich stronach – konwertuj TIFF na tekst

Mając obiekt obrazu w ręku, silnik może teraz przetworzyć wszystkie strony jednocześnie. Ta metoda zwraca listę, w której każdy element zawiera wynik OCR dla jednej strony.

```python
# Step 3: Perform OCR on all pages of the image
page_results = engine.recognize_multi_page(tiff_image)
```

**Co się dzieje pod maską?**  
Funkcja `recognize_multi_page` iteruje po każdej rasteryzowanej stronie, uruchamia rozpoznawanie sieci neuronowej i łączy wynikowy tekst z ocenami pewności. To zasadniczo operacja wsadowa, która oszczędza konieczności ręcznego pisania pętli.

## Iteruj po wynikach – wyodrębnij tekst z TIFF

Na koniec wyświetlamy rozpoznany tekst. Możesz zapisać wynik do oddzielnych plików `.txt`, wprowadzić go do bazy danych lub przekazać do indeksu wyszukiwania — cokolwiek pasuje do Twojego workflow.

```python
# Step 4: Iterate through the results and display the recognized text for each page
for page_index, result in enumerate(page_results):
    print(f"Page {page_index + 1}:\n{result.text}\n")
```

### Oczekiwany wynik

```
Page 1:
Chapter 1
In the beginning...

Page 2:
The quick brown fox jumps over the lazy dog.

Page 3:
...

```

Każdy ciąg `result.text` zawiera surowy wynik OCR dla danej strony. Jeśli potrzebujesz zachować podziały wierszy, większość silników udostępnia `result.lines` jako listę stringów.

## Obsługa dużych plików TIFF – wskazówki i triki

Przetwarzanie TIFF‑a o 500 stronach może być intensywne pod względem pamięci. Oto kilka strategii, które pomogą utrzymać płynność:

1. **Podziel strony na partie** – zamiast `recognize_multi_page`, wywołuj `engine.recognize(page)` w generatorze, który zwraca jedną stronę na raz.  
2. **Dostosuj DPI** – obniżenie rozdzielczości obrazu (np. z 300 DPI do 200 DPI) zmniejsza obciążenie CPU, a przy większości drukowanego tekstu wpływa minimalnie na dokładność.  
3. **Równoległość** – jeśli Twój silnik OCR jest bezpieczny wątkowo, uruchom `concurrent.futures.ThreadPoolExecutor`, aby rozpoznawać wiele stron jednocześnie.

```python
import concurrent.futures

def ocr_page(page):
    return engine.recognize(page).text

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    texts = list(executor.map(ocr_page, tiff_image.pages))
```

## Zapisz wyodrębniony tekst do plików

Większość rzeczywistych pipeline’ów wymaga trwałego przechowywania. Poniżej znajdziesz zwięzły sposób na zapisanie tekstu każdej strony do osobnego pliku, zachowując kolejność stron.

```python
import pathlib

output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for i, result in enumerate(page_results, start=1):
    file_path = output_dir / f"page_{i:03}.txt"
    file_path.write_text(result.text, encoding="utf-8")
    print(f"Saved page {i} to {file_path}")
```

Teraz masz czysty katalog z plikami `.txt` gotowymi do indeksowania lub dalszego przetwarzania NLP.

## Podgląd obrazu – wizualne wykorzystanie wyników OCR

Jeśli chcesz zobaczyć nakładkę OCR na oryginalnym obrazie (przydatne przy debugowaniu), wiele bibliotek pozwala rysować ramki ograniczające. Oto szybki przykład z użyciem Pillow:

```python
from PIL import ImageDraw

for page, result in zip(tiff_image.pages, page_results):
    draw = ImageDraw.Draw(page)
    for word in result.words:          # Assume `result.words` gives bounding boxes
        draw.rectangle(word.box, outline="red")
    page.show()   # Opens the annotated page
```

![How to use OCR in Python – OCR overlay on a TIFF page](ocr_overlay_example.png)

*Alt text:* How to use OCR in Python – visual overlay of recognized text on a TIFF page.

## Typowe pułapki i jak ich unikać

| Problem | Dlaczego się pojawia | Rozwiązanie |
|---------|----------------------|-------------|
| Zniekształcone znaki | Nieprawidłowy model językowy | Ustaw `engine.language` na właściwy enum |
| Brakujące strony | Kompresja TIFF nieobsługiwana | Najpierw skonwertuj do nieskompresowanego TIFF |
| Niska wydajność | Wysokie DPI + przetwarzanie jednowątkowe | Obniż DPI lub włącz przetwarzanie wielowątkowe |
| Pusty wynik | Obraz zbyt ciemny/ma niski kontrast | Wstępnie przetwórz go, zwiększ kontrast (`opencv` lub `Pillow`) |

Rozwiązanie tych problemów na wczesnym etapie oszczędza godziny debugowania później.

## Kolejne kroki – wyjście poza podstawowe wyodrębnianie

Teraz, gdy opanowałeś podstawy **jak używać OCR w Pythonie**, rozważ dalsze eksploracje:

- **Generowanie PDF** – połącz wyodrębniony tekst z `reportlab`, aby odtworzyć przeszukiwalne PDF‑y.  
- **Wykrywanie języka** – automatycznie przełączaj `engine.language` przy pomocy `langdetect`.  
- **Wyodrębnianie danych strukturalnych** – użyj wyrażeń regularnych lub spaCy, aby wyciągnąć daty, nazwy lub tabele z surowego tekstu.  
- **Alternatywne backendy OCR** – zamień `ocr` na `pytesseract` lub `easyocr`, jeśli potrzebujesz wsparcia wielu języków.

Każdy z tych tematów naturalnie łączy się z drugorzędnymi słowami kluczowymi **ocr library python**, **convert tiff to text**, **extract text from tiff** oraz **python ocr engine**, dając solidną bazę do bardziej zaawansowanych projektów.

---

### Podsumowanie

Omówiliśmy **jak używać OCR w Pythonie** od instalacji po przetwarzanie wielostronicowe, pokazując dokładnie, jak **konwertować TIFF na tekst** i **wyodrębniać tekst z TIFF** przy użyciu prostego **python OCR engine**. Pełny, gotowy do uruchomienia przykład powinien działać od razu dla większości standardowych plików TIFF, a podane wskazówki pomogą skalować rozwiązanie do większych dokumentów lub integrować OCR w szerszych pipeline’ach.

Wypróbuj to na własnych zeskanowanych książkach, paragonach lub archiwalnych obrazach — a potem eksperymentuj z pomysłami z sekcji „Kolejne kroki”. Powodzenia w kodowaniu i niech Twoje wyniki OCR będą zawsze precyzyjne!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz szczegółowe wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to extract text from tiff with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}