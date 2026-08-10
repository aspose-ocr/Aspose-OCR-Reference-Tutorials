---
category: general
date: 2026-03-26
description: Dowiedz się, jak przeprowadzać OCR w Pythonie i łatwo wyodrębniać tekst
  z obrazu, odczytywać tekst ze skanu lub wyciągać tekst z faktury przy użyciu prostego
  OcrEngine.
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: pl
og_description: Jak wykonać OCR w Pythonie? Ten przewodnik pokaże Ci, jak wyodrębnić
  tekst z obrazu, odczytać tekst ze skanu i wyodrębnić tekst z faktury w kilka minut.
og_title: Jak wykonać OCR w Pythonie – Szybko wyodrębniaj tekst
tags:
- OCR
- Python
- Image Processing
title: Jak wykonać OCR w Pythonie – Szybko wyodrębniaj tekst
url: /pl/python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonać OCR w Pythonie – szybkie wyodrębnianie tekstu

Zastanawiałeś się kiedyś, **jak wykonać OCR** na zeskanowanym paragonie lub rozmytym PDF‑ie? Nie jesteś sam. W wielu projektach potrzeba **wyodrębnienia tekstu z obrazu** pojawia się szybciej niż później, a tradycyjne podejście „wpisz wszystko ręcznie” po prostu nie skaluje się.

W tym samouczku zobaczysz kompletny, gotowy do uruchomienia przykład, który pokazuje **jak używać OCR** do odczytu tekstu ze skanu, pobierania danych z faktury i nawet automatycznej korekcji pochylenia – wszystko w kilku linijkach Pythona.

## Czego się nauczysz

Przejdziemy przez wszystko, co musisz wiedzieć:

* Dokładne zależności i importy wymagane w projekcie.  
* Jak utworzyć i skonfigurować instancję `OcrEngine`.  
* Sposoby **wyodrębniania tekstu z obrazu**, **odczytywania tekstu ze skanu** i **wyodrębniania tekstu z faktury** przy użyciu tego samego silnika.  
* Typowe pułapki (zły język, brakujące pliki, duże obrazy) oraz jak ich unikać.  
* Oczekiwany wynik, abyś mógł zweryfikować, że OCR się powiódł.

Nie potrzebujesz zewnętrznych linków do dokumentacji – wszystko jest samodzielne, więc możesz skopiować‑wkleić kod i od razu zobaczyć rezultaty.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz:

* Python 3.8+ zainstalowany (pakiet `ocr` działa z każdą nowszą wersją).  
* Bibliotekę `ocr` dostępną (`pip install ocr‑engine` – zamień nazwę pakietu, jeśli jest inna).  
* Plik obrazu, który chcesz przetworzyć – w demonstracji użyjemy `invoice.png` znajdującego się w folderze `YOUR_DIRECTORY`.

To wszystko. Jeśli już to masz, możesz zaczynać.

## Krok 1: Instalacja i import modułu OCR

Na początek potrzebujemy biblioteki OCR. Jeśli jeszcze jej nie zainstalowałeś, uruchom następujące polecenie w terminalu:

```bash
pip install ocr-engine
```

Teraz importujemy moduł w naszym skrypcie.

```python
# Step 1: Import the OCR module
import ocr
```

> **Pro tip:** Utrzymuj wirtualne środowisko w porządku; zapobiega to konfliktom wersji, gdy później dodasz inne pakiety do przetwarzania obrazów.

## Krok 2: Utworzenie i konfiguracja silnika OCR

Utworzenie silnika jest tak proste, jak wywołanie jego konstruktora, ale prawdziwa moc tkwi w prawidłowej konfiguracji. Ustawimy język na angielski i włączymy automatyczną korekcję pochylenia, co jest niezbędne przy skanach faktur, które nie są idealnie wyrównane.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

Dlaczego włączamy `auto_skew`? Wiele skanerów tworzy obrazy odchylone o kilka stopni. Bez korekcji silnik może przegapić znaki, zamieniając czytelną fakturę w bełkot.

## Krok 3: Wykonanie OCR na wybranym obrazie

Teraz przekazujemy plik obrazu do silnika. Metoda `recognize_image` zwraca obiekt zawierający surowy tekst oraz (jeśli biblioteka je udostępnia) wyniki pewności.

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

Jeśli pracujesz w scenariuszu **odczytywania tekstu ze skanu**, po prostu zamień ścieżkę na skanowany PDF przekonwertowany do PNG lub JPEG. To samo wywołanie działa dla każdego formatu obrazu obsługiwanego przez podległą bibliotekę.

## Krok 4: Inspekcja i wykorzystanie wyodrębnionego tekstu

Wypiszmy surowy wynik OCR. W rzeczywistym potoku przetwarzania faktur prawdopodobnie sparsujesz ten ciąg, wyodrębnisz pozycje, sumy i daty, ale na razie szybki podgląd potwierdzi, że OCR się powiódł.

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**Oczekiwany wynik (skrócony dla przejrzystości):**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

Jeśli wynik wygląda na zniekształcony, sprawdź, czy obraz jest wyraźny i czy `engine.language` odpowiada językowi dokumentu.

## Krok 5: Obsługa typowych przypadków brzegowych

### Duże obrazy

Przetwarzanie skanu 5000 × 5000 pikseli może pochłaniać dużo pamięci. Szybkim sposobem na złagodzenie tego problemu jest zmniejszenie rozmiaru obrazu przed przekazaniem go do silnika:

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### Wiele języków

Jeśli musisz **wyodrębnić tekst z obrazu**, który zawiera zarówno angielski, jak i hiszpański, możesz ustawić listę języków:

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

Silnik spróbuje rozpoznać znaki z obu zestawów.

### Obsługa błędów

Nigdy nie zakładaj, że plik istnieje. Owiń wywołanie w blok `try‑except`, aby wyświetlić przyjazny komunikat:

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## Odniesienie wizualne

Poniżej zrzut ekranu przykładowej faktury użytej w demonstracji. Zauważ niewielkie nachylenie – dokładnie to, co naprawia `auto_skew`.

![jak wykonać OCR na fakturze](/images/ocr-example.png)

*Tekst alternatywny:* jak wykonać OCR na obrazie faktury pokazując automatyczną korekcję pochylenia.

## Pełny, gotowy do uruchomienia przykład

Łącząc wszystko w jedną całość, oto prosty skrypt, który możesz uruchomić z wiersza poleceń. Obejmuje instalację, konfigurację, obsługę błędów oraz prosty krok post‑processingu, który zapisuje wyodrębniony tekst do pliku `output.txt`.

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

Uruchomienie `python full_ocr_demo.py` wypisze wyodrębniony tekst w konsoli i zapisze go w `output.txt`. Stamtąd możesz zastosować wyrażenia regularne, zapisywać do CSV lub dowolną inną logikę potrzebną do **automatyzacji wyodrębniania tekstu z faktury**.

## Zakończenie

Masz teraz solidne, kompleksowe rozwiązanie **jak wykonać OCR** w Pythonie. Tworząc `OcrEngine`, konfigurując język i korekcję pochylenia oraz obsługując kilka praktycznych przypadków brzegowych, możesz niezawodnie **wyodrębniać tekst z obrazu**, **odczytywać tekst ze skanu** i **wyodrębniać tekst z faktury** bez przeszukiwania rozproszonej dokumentacji.

Co dalej? Spróbuj przetworzyć batch plików w pętli, eksperymentuj z różnymi językami lub podłącz wynik do biblioteki generującej PDF, aby tworzyć przeszukiwalne dokumenty. Niebo jest granicą, a kod, który właśnie zobaczyłeś, to solidna platforma startowa.

Masz pytania dotyczące konkretnego formatu pliku lub potrzebujesz pomocy przy dostosowywaniu progów pewności? zostaw komentarz poniżej – chętnie pomogę dopracować Twój potok OCR!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}