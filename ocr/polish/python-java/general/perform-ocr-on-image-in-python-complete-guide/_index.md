---
category: general
date: 2026-06-22
description: Wykonaj OCR na obrazie przy użyciu Pythona w zaledwie kilku linijkach.
  Dowiedz się, jak wczytać obraz do OCR, rozpoznać tekst z pliku PNG i efektywnie
  korzystać z silnika OCR.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: pl
og_description: Wykonaj OCR na obrazie szybko przy użyciu Pythona. Ten tutorial pokazuje,
  jak załadować obraz do OCR, rozpoznać tekst z pliku PNG oraz używać silnika OCR
  z pewnością.
og_title: Wykonaj OCR na obrazie w Pythonie – Przewodnik krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Wykonaj OCR na obrazie w Pythonie – Kompletny przewodnik
url: /pl/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wykonaj OCR na obrazie w Pythonie – Kompletny przewodnik

Czy kiedykolwiek potrzebowałeś **perform OCR on image** plików, ale utknąłeś już przy pierwszej linii kodu? Nie jesteś sam. W tym przewodniku pokażemy dokładnie, jak **load image for OCR**, skonfigurować lekką **OCR engine**, i w końcu **recognize text from PNG** przy użyciu kilku poleceń.

Omówimy wszystko, od instalacji biblioteki po dostosowanie whitelisty, tak aby w skanie przetrwały tylko cyfry i wielkie litery. Po zakończeniu będziesz mieć gotowy do uruchomienia skrypt, który możesz wrzucić do dowolnego projektu — bez tajemnic, bez zbędnego balastu.

## Czego się nauczysz

- Jak **use OCR engine** programowo w Pythonie.  
- Dokładne kroki, aby **load image for OCR** z lokalnego folderu.  
- Dlaczego i jak ograniczyć rozpoznawanie do własnego zestawu znaków.  
- Jak **recognize text from PNG** i bezpiecznie obsłużyć wynik.  

**Prerequisites:** Zainstalowany Python 3.7+, terminal, z którym czujesz się komfortowo, oraz obraz (np. `serial-number.png`), który chcesz odczytać. Wcześniejsze doświadczenie z OCR nie jest wymagane.

---

## Perform OCR on Image – Initialize the OCR Engine

Pierwszą rzeczą, którą musisz zrobić, jest utworzenie instancji OCR engine. Traktuj silnik jako mózg, który analizuje piksele i przekształca je w znaki.

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Why this matters:* Bez silnika nie ma czego przetwarzać obraz. Klasa `OcrEngine` łączy wszystkie ciężkie operacje — pre‑processing, segmentację i klasyfikację znaków — w jednym obiekcie, którego możesz ponownie używać.

---

## Load Image for OCR – Provide the PNG File

Teraz, gdy silnik istnieje, musisz podać mu obraz, który chcesz odczytać. Biblioteka oczekuje obiektu `ImageStream`, który możesz utworzyć bezpośrednio z ścieżki pliku.

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*Pro tip:* Trzymaj obraz w formacie o wysokim kontraście (czarny tekst na białym tle) i unikaj artefaktów kompresji; mogą one zakłócić działanie algorytmu OCR.

---

## Restrict Characters – Whitelist Digits and Uppercase Letters

Często interesuje Cię tylko podzbiór znaków — na przykład numer seryjny zawierający wyłącznie A‑Z i 0‑9. Ustawiając whitelist, informujesz silnik, aby ignorował wszystko inne, co znacząco zwiększa dokładność.

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*What’s happening under the hood?* Silnik tworzy filtr, który odrzuca wszystkie glify nieobecne w whitelist przed ostatecznym etapem klasyfikacji. Jest to szczególnie przydatne, gdy obraz zawiera szumy lub dekoracyjny tekst, którego nie potrzebujesz.

---

## Recognize Text from PNG – Run the OCR Process

Gdy silnik jest gotowy, a obraz załadowany, możesz w końcu **perform OCR on image**. Wywołanie `recognize()` uruchamia pełny pipeline i zwraca obiekt wyniku.

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

Jeśli interesuje Cię wydajność, metoda zazwyczaj kończy się w ciągu kilku setek milisekund dla PNG o wymiarach 300 × 200 px na nowoczesnym laptopie.

---

## Output and Verify – Get the Recognized Text

Ostatnim krokiem jest wyodrębnienie czystego tekstu z obiektu wyniku. Wszystko, co nie pasuje do whitelist, jest automatycznie odrzucane, więc otrzymujesz czysty ciąg gotowy do dalszego przetwarzania.

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*Typical output:* `AB12C3D4E5` (zakładając, że obraz zawierał dokładnie ten numer seryjny).  

Jeśli wyjście jest puste lub zniekształcone, sprawdź ponownie jakość obrazu i whitelist; częstym pułapką jest przypadkowe pominięcie potrzebnych znaków.

---

## Edge Cases & Common Gotchas

| Sytuacja | Co sprawdzić | Sugerowana poprawka |
|-----------|---------------|---------------|
| **File not found** | Błąd w ścieżce lub brak pliku | Użyj `os.path.abspath`, aby zweryfikować pełną ścieżkę przed wywołaniem `set_image`. |
| **Low contrast image** | Tekst zlewa się z tłem | Zastosuj prosty próg (`Pillow` lub `OpenCV`) przed przekazaniem obrazu do silnika. |
| **Unexpected characters** | Whitelist jest zbyt restrykcyjny | Dodaj brakujące znaki do ciągu whitelist. |
| **Large images** | Wolne rozpoznawanie | Zmień rozmiar obrazu do maksymalnie 1024 px szerokości; jakość OCR zazwyczaj pozostaje wysoka. |

---

## Full Script – Ready to Run

Poniżej znajduje się kompletny, samodzielny skrypt, który łączy wszystkie elementy. Zapisz go jako `ocr_demo.py`, zamień `YOUR_DIRECTORY` na rzeczywisty folder i uruchom `python ocr_demo.py`.

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*Expected console output* (gdy PNG zawiera `SN12345`):

```
Recognized text: SN12345
```

---

## Zakończenie

Teraz wiesz dokładnie, jak **perform OCR on image** pliki w Pythonie, od **loading image for OCR** po **recognize text from PNG**, a na końcu wyodrębnić czysty wynik przy użyciu konfigurowalnego **OCR engine**. Podejście jest proste, rozszerzalne i działa od razu dla większości skanów w stylu numerów seryjnych.

Co dalej? Spróbuj zamienić whitelist na małe litery, eksperymentuj z różnymi formatami obrazów (JPEG, BMP) lub zintegrować skrypt z potokiem przetwarzania wsadowego. Ten sam schemat — engine → image → settings → recognize → output — obowiązuje praktycznie w każdym zadaniu OCR, które napotkasz.

Masz pytania lub nietypowy obraz, który odmawia współpracy? zostaw komentarz poniżej i powodzenia w kodowaniu! 

![Diagram illustrating the steps to perform OCR on image using Python](https://example.com/ocr-flow.png "Diagram showing how to perform OCR on image with a Python OCR engine")


## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Konwertuj obraz na tekst – wykonaj OCR na obrazie z URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Jak używać AspOCR: przetwarzanie wstępne filtrów OCR obrazu dla .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Jak wyodrębnić tekst z obrazu poprzez przygotowanie prostokątów w OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}