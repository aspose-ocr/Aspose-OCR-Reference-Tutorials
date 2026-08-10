---
category: general
date: 2026-06-19
description: Jak wyodrębnić PDF za pomocą OCR w Pythonie – krok po kroku tutorial
  obejmujący wyodrębnianie tekstu z PDF, rozpoznawanie tekstu z obrazu oraz przykład
  OCR w Pythonie.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: pl
og_description: Jak wyodrębnić PDF za pomocą OCR w Pythonie. Dowiedz się, jak wyodrębnić
  tekst z PDF, rozpoznać tekst z obrazu i zobacz kompletny przykład OCR w Pythonie.
og_title: Jak wyodrębnić tekst z PDF przy użyciu OCR w Pythonie – pełny poradnik
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Jak wyodrębnić tekst z PDF przy użyciu OCR w Pythonie – Kompletny przewodnik
url: /pl/python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyodrębnić tekst z PDF przy użyciu OCR w Pythonie – Kompletny przewodnik

Zastanawiałeś się kiedyś **jak wyodrębnić PDF** zawartość, gdy plik jest jedynie zeskanowanym obrazem? Nie jesteś jedyny. W wielu rzeczywistych projektach — myśl o umowach, fakturach czy archiwach historycznych — otrzymany PDF nie zawiera tekstu, który można zaznaczyć. Dobra wiadomość? Kilka linijek Pythona może zamienić te jedynie obrazowe strony w przeszukiwalny, edytowalny tekst.

W tym tutorialu przeprowadzimy praktyczny **przykład OCR w Pythonie**, który odczytuje PDF, renderuje jego pierwszą stronę jako obraz, a następnie **wyodrębnia tekst z PDF** przy użyciu silnika OCR. Po zakończeniu dokładnie będziesz wiedział, jak **czytać PDF z OCR**, dlaczego każdy krok ma znaczenie i jak dostosować kod do dokumentów wielostronicowych lub różnych języków.

## Co się nauczysz

- Zainstaluj i skonfiguruj niezawodną bibliotekę OCR dla Pythona.  
- Konwertuj strony PDF na obrazy odpowiednie dla OCR.  
- **Rozpoznawaj tekst z obrazu** i uzyskaj czyste ciągi Unicode.  
- Typowe pułapki (PDF o niskiej rozdzielczości, obrócone strony) i jak ich unikać.  
- Rozszerz skrypt, aby obsługiwał wiele stron lub przetwarzanie wsadowe.

**Wymagania wstępne**: Python 3.8+, pip oraz podstawowa znajomość środowisk wirtualnych. Nie wymagana wcześniejsza znajomość OCR — po prostu podążaj za instrukcjami.

---

## ## Jak wyodrębnić tekst z PDF przy użyciu OCR w Pythonie

Ten nagłówek H2 zawiera nasze główne słowo kluczowe dokładnie tam, gdzie wyszukiwarki go uwielbiają. Zanurzmy się od razu w kod.

### Krok 1 – Zainstaluj wymagane pakiety

Najpierw potrzebujemy silnika OCR. Poniższy przykład używa popularnego pakietu **ocr** (cienka nakładka na Tesseract). Jeśli wolisz inny backend, koncepcje pozostają takie same.

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **Porada:** Na Linuksie będziesz także potrzebował binarki Tesseract: `sudo apt-get install tesseract-ocr`. Użytkownicy macOS mogą ją pobrać przez Homebrew: `brew install tesseract`.

### Krok 2 – Zainicjalizuj silnik OCR i ustaw język

Teraz uruchamiamy silnik i instruujemy go, aby szukał angielskich znaków. Możesz zamienić `ocr.Language.English` na dowolny obsługiwany kod języka.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**Dlaczego to ważne:** Określenie języka znacząco zwiększa dokładność, ponieważ silnik może zastosować słowniki i modele znaków specyficzne dla języka.

### Krok 3 – Wczytaj stronę PDF jako obraz

OCR działa na obrazach rastrowych, nie na obiektach PDF. Pomocnicza funkcja `ocr.Image.from_pdf` renderuje wybraną stronę do bitmapy. Dostosuj `page_number` dla innych stron (indeksowanie od 0).

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **Przypadek brzegowy:** Jeśli PDF zawiera grafikę wektorową zamiast zeskanowanych obrazów, możesz uzyskać wyraźne renderowanie. Dla skanów o niskiej rozdzielczości rozważ zwiększenie DPI: `ocr.Image.from_pdf(..., dpi=300)`.

### Krok 4 – Rozpoznaj tekst z wyrenderowanego obrazu

Oto serce **przykładu ocr w Pythonie**. Silnik przetwarza bitmapę i zwraca obiekt zawierający wyodrębniony ciąg znaków.

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

Atrybut `ocr_result.text` zawiera wynik w postaci zwykłego tekstu, zachowując podziały linii, gdy to możliwe.

### Krok 5 – Wydrukuj lub zapisz wyodrębniony tekst

Na koniec wypisujemy wynik. W rzeczywistej aplikacji prawdopodobnie zapisałbyś go do pliku lub bazy danych.

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

Uruchomienie skryptu powinno wyświetlić coś podobnego do:

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

To kompletny **wyodrębnianie tekstu z pdf** przy użyciu OCR.

---

## ## Rozpoznawanie tekstu z obrazu – Dostosowywanie dokładności

Jeśli interesuje Cię tylko **rozpoznawanie tekstu z obrazu** (np. JPEG paragonu), możesz pominąć krok konwersji PDF:

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

**Wskazówki dla lepszych wyników:**

- **Wstępne przetwarzanie** obrazu: konwersja do odcieni szarości, zastosowanie progowania lub prostowanie (deskew). Pillow ułatwia to.
- **Zwiększ DPI** podczas renderowania PDF: wyższa rozdzielczość dostarcza silnikowi OCR więcej szczegółów.
- **Włącz konfigurację silnika OCR** dla segmentacji stron (`ocr_engine.config = "--psm 6"` dla jednolitych bloków).

## ## Czytanie PDF z OCR – Obsługa wielu stron

Większość umów rozciąga się na kilka stron. Iterowanie po każdej stronie jest proste:

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

Ta funkcja **czyta PDF z OCR**, konkatenatuje wynik i wstawia wyraźny znacznik podziału strony. Następnie możesz przekazać `full_text` do indeksu wyszukiwania lub zapisać jako plik `.txt`.

## ## Typowe problemy i jak je naprawić

| Objaw | Prawdopodobna przyczyna | Rozwiązanie |
|---------|--------------|-----|
| Zniekształcone znaki, dużo `?` | Nieprawidłowy język lub brak plików danych językowych | Zainstaluj właściwy pakiet językowy Tesseract (`tesseract-ocr-<lang>`) i ustaw `ocr_engine.language`. |
| Brakujące linie lub przycięte słowa | Niska rozdzielczość DPI (poniżej 150) | Renderuj PDF w 300 DPI lub wyżej (`dpi=300`). |
| Tekst jest obrócony lub do góry nogami | Zeskanowana strona nie jest prawidłowo ustawiona | Użyj `ocr.Image.deskew(page_image)` przed rozpoznaniem. |
| Wolne przetwarzanie dużych PDF‑ów | Przetwarzanie stron kolejno w jednym wątku | Zrównoleglij przy użyciu `concurrent.futures.ThreadPoolExecutor`. |

## ## Rozszerzanie przykładu OCR w Pythonie

- **Eksport do PDF/A**: Po wyodrębnieniu możesz osadzić tekst z powrotem w przeszukiwalnym PDF przy użyciu `reportlab` lub `pypdf2`.
- **Wykrywanie języka**: Użyj `langdetect` na wyniku OCR, aby dynamicznie przełączać `ocr_engine.language`.
- **Przetwarzanie wsadowe**: Przejdź po katalogu za pomocą `os.listdir` i zastosuj `extract_all_pages` do każdego pliku.

## ## Oczekiwany wynik i weryfikacja

Gdy uruchomisz skrypt na wyraźnym skanie w języku angielskim, powinieneś zobaczyć czysty blok tekstu z prawidłową interpunkcją. Zweryfikuj przez:

1. Porównanie kilku linii z oryginalnym zeskanowanym obrazem.  
2. Uruchomienie prostego liczenia słów (`len(ocr_result.text.split())`), aby upewnić się, że wynik nie jest pusty.  
3. Opcjonalnie, przekazanie wyniku do sprawdzania pisowni, np. `pyspellchecker`, aby wykryć błędy OCR.

## Podsumowanie

Omówiliśmy **jak wyodrębnić PDF** zawartość, gdy tradycyjne parsowanie zawodzi, przedstawiliśmy pełny **przykład ocr w Pythonie** i wyjaśniliśmy, jak **rozpoznawać tekst z obrazu** oraz **czytać PDF z OCR** zarówno dla pojedynczych, jak i wielostronicowych scenariuszy. Dzięki powyższym fragmentom kodu możesz teraz zamienić dowolny zeskanowany PDF w przeszukiwalny, edytowalny tekst — bez ręcznego przepisywania.

Kolejne kroki? Spróbuj zamienić język na hiszpański (`ocr.Language.Spanish`) lub eksperymentuj z technikami wstępnego przetwarzania obrazu, aby zwiększyć dokładność. Jeśli budujesz system zarządzania dokumentami, rozważ indeksowanie wyodrębnionego tekstu w Elasticsearch dla błyskawicznego wyszukiwania.

Masz pytania lub napotkałeś dziwny PDF? zostaw komentarz i szczęśliwego kodowania!  

![How to extract PDF using OCR in Python](image.png "How to extract PDF using OCR in Python")

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletny działający kod z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Wyodrębnij tekst z obrazu przy użyciu Aspose OCR – przewodnik krok po kroku](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Rozpoznaj tekst PDF – operacje OCR z Aspose.OCR dla Java](/ocr/english/java/ocr-operations/)
- [Wyodrębnij tekst z obrazu w C# z wyborem języka przy użyciu Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}