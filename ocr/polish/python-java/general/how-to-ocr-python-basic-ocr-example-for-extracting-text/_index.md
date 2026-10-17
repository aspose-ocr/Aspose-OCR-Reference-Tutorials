---
category: general
date: 2026-04-26
description: 'jak używać OCR w Pythonie: naucz się wyodrębniać tekst z obrazu i odczytywać
  pliki TIFF w Pythonie przy użyciu podstawowego przykładu OCR. Szybki, gotowy do
  uruchomienia kod w zestawie.'
draft: false
keywords:
- how to ocr python
- extract text from image
- read tiff file python
- basic ocr example
- convert scanned image text
language: pl
og_description: 'jak zrobić OCR w Pythonie: przewodnik krok po kroku, który pokazuje,
  jak wyodrębnić tekst z obrazu, odczytać plik TIFF w Pythonie i konwertować tekst
  zeskanowanego obrazu przy użyciu prostego, uruchamialnego skryptu.'
og_title: jak zrobić OCR w Pythonie – podstawowy przykład OCR do wyodrębniania tekstu
tags:
- OCR
- Python
- Image Processing
title: Jak zrobić OCR w Pythonie – podstawowy przykład wyodrębniania tekstu
url: /pl/python-java/general/how-to-ocr-python-basic-ocr-example-for-extracting-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak zrobić OCR w Pythonie – Podstawowy przykład OCR do wyodrębniania tekstu

Zastanawiałeś się kiedyś **jak zrobić OCR w Pythonie**, gdy na biurku leży zeskanowany plik TIFF? Nie jesteś jedynym, który patrzy na mnóstwo plików graficznych i pyta: „Jak wyciągnąć z tego słowa?” Dobra wiadomość jest taka, że przekształcenie obrazu w zwykły tekst to bułka z masłem przy użyciu odpowiedniej biblioteki i kilku prostych kroków.

W tym samouczku przeprowadzimy Cię przez **podstawowy przykład OCR**, który odczytuje plik TIFF, wyodrębnia tekst i wyświetla go w konsoli. Po zakończeniu dokładnie będziesz wiedział, jak **wyodrębnić tekst z obrazu**, jak radzić sobie z specyfiką formatów TIFF oraz co dostosować, jeśli potrzebujesz **przekształcić zeskanowany tekst obrazu** w coś bardziej użytecznego. Bez ukrytej magii — po prostu prosty Python, który możesz skopiować‑wkleić i uruchomić już dziś.

## Czego będziesz potrzebował

- Python 3.9+ zainstalowany (najlepsza jest najnowsza stabilna wersja).
- Biblioteka OCR instalowana przez pip. W tym przewodniku użyjemy fikcyjnego pakietu `aocr`, który naśladuje popularne narzędzia takie jak Tesseract; później możesz zamienić go na `pytesseract` lub `easyocr`.
- Obraz TIFF, który chcesz przetworzyć – nazwij go `input.tiff` i umieść w folderze, do którego odwołasz się w kodzie.
- Podstawowa znajomość wiersza poleceń (tylko do instalacji pakietu).

To wszystko. Bez ciężkich zależności, bez kontenerów Docker, tylko kilka linii kodu.

## Krok 1 – Instalacja i import zależności (jak zrobić OCR w Pythonie)

Najpierw pobierz pakiet OCR. Otwórz terminal i uruchom:

```bash
pip install aocr
```

Jeśli wolisz rzeczywistą bibliotekę, zamień `aocr` na `pytesseract` i zainstaluj silnik Tesseract osobno.

Teraz zaimportujmy to, czego potrzebujemy. Klasa `Path` z `pathlib` zapewnia wygodny sposób pracy ze ścieżkami plików na różnych systemach operacyjnych.

```python
# Step 1: Import the Path class for handling file paths
from pathlib import Path

# Import the OCR engine and image loader from the chosen library
from aocr import OcrEngine, Image
```

*Dlaczego używać `Path`?* Ponieważ ukrywa różnice w separatorach (`/` vs `\`) i pozwala łączyć katalogi bez martwienia się o system operacyjny. Ten drobny szczegół często oszczędza problemy, gdy później przeniesiesz skrypt na serwer CI.

## Krok 2 – Utworzenie instancji silnika OCR (podstawowy przykład OCR)

Następnie uruchom silnik OCR. Pomyśl o `OcrEngine` jako o mózgu, który odczyta obraz i zwróci znaki.

```python
# Step 2: Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

Większość bibliotek OCR pozwala tutaj dostosować język, DPI lub progi pewności. Dla tego **podstawowego przykładu OCR** pozostaniemy przy ustawieniach domyślnych, ale później możesz zbadać `ocr_engine.config`, jeśli potrzebujesz obsługiwać dokumenty wielojęzyczne.

## Krok 3 – Załadowanie obrazu TIFF (odczyt pliku TIFF w Pythonie)

Tutaj wkracza część **odczyt pliku TIFF w Pythonie**. Pliki TIFF mogą mieć wiele stron, ale `Image.load` domyślnie pobierze pierwszą stronę — idealne dla jednosktronicowego skanu.

```python
# Step 3: Load the image you want to recognize
# Using a generic placeholder path makes it easy to adapt the example
ocr_engine.image = Image.load(Path("YOUR_DIRECTORY/input.tiff"))
```

Zastąp `"YOUR_DIRECTORY"` rzeczywistym folderem, w którym znajduje się `input.tiff`. Jeśli nie jesteś pewien, gdzie uruchamia się skrypt, `Path.cwd()` wypisuje bieżący katalog roboczy — przydatne przy debugowaniu problemów ze ścieżkami.

## Krok 4 – Uruchomienie procesu OCR (wyodrębnianie tekstu z obrazu)

Teraz dzieje się magia. Wywołanie `process()` przesyła obraz przez potok OCR i zwraca obiekt wyniku.

```python
# Step 4: Run the OCR process to extract text from the image
ocr_result = ocr_engine.process()
```

Za kulisami silnik może konwertować obraz na odcienie szarości, stosować progowanie i podawać go do sieci neuronowej. Nie musisz zarządzać tymi krokami; biblioteka ukrywa je przed Tobą.

## Krok 5 – Wyświetlenie rozpoznanego tekstu (przekształcenie zeskanowanego tekstu obrazu)

Na koniec wypisz tekst. W prawdziwych projektach prawdopodobnie zapiszesz go do pliku lub bazy danych, ale drukowanie utrzymuje przykład schludnym.

```python
# Step 5: Print the recognized text to the console
print(ocr_result.text)
```

Gdy uruchomisz skrypt, powinieneś zobaczyć coś podobnego do:

```
Hello, world!
This is a sample scanned document.
```

Jeśli wynik jest nieczytelny, sprawdź ponownie, czy obraz źródłowy jest wyraźny i czy język OCR odpowiada tekstowi.

## Pełny działający skrypt

Łącząc wszystko razem, oto kompletny, gotowy do uruchomienia program:

```python
# Full script: how to ocr python – basic OCR example

from pathlib import Path
from aocr import OcrEngine, Image  # Replace with your OCR library if needed

def main():
    # Initialize the OCR engine
    ocr_engine = OcrEngine()

    # Load the TIFF image (adjust the path as needed)
    image_path = Path("YOUR_DIRECTORY/input.tiff")
    if not image_path.is_file():
        raise FileNotFoundError(f"Could not find {image_path}. Make sure the file exists.")
    
    ocr_engine.image = Image.load(image_path)

    # Perform OCR
    ocr_result = ocr_engine.process()

    # Output the extracted text
    print("=== OCR Output ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

### Oczekiwany wynik

```
=== OCR Output ===
Your scanned document’s text appears here, line by line.
```

Jeśli potrzebujesz **przekształcić zeskanowany tekst obrazu** w przeszukiwalny PDF, możesz przekazać `ocr_result.text` do generatora PDF, takiego jak `reportlab` — ale to już osobny samouczek.

## Częste pułapki i wskazówki profesjonalistów

- **Skanowanie o niskiej rozdzielczości**: OCR ma problemy poniżej 150 DPI. Jeśli Twój TIFF jest rozmyty, najpierw zwiększ rozdzielczość przy pomocy Pillow (`Image.open(...).resize(...)`).
- **Wiele stron**: Dla wielostronicowych TIFF‑ów iteruj po `Image.load_multi_page()` (jeśli Twoja biblioteka to obsługuje) i łącz wyniki.
- **Obsługa języków**: Wiele silników domyślnie używa angielskiego. Ustaw `ocr_engine.language = "spa"` dla hiszpańskiego, na przykład.
- **Obsługa białych znaków**: OCR często dodaje niechciane podziały linii. Użyj `str.splitlines()` lub wyrażeń regularnych, aby oczyścić wynik.
- **Wydajność**: Przy przetwarzaniu hurtowym, ponownie używaj jednej instancji `OcrEngine` zamiast tworzyć nową dla każdego pliku.

## Rozszerzanie przykładu

Teraz, gdy opanowałeś **jak zrobić OCR w Pythonie** dla pojedynczego obrazu, rozważ następujące kolejne kroki:

1. **Przetwarzanie wsadowe** – Przejdź przez katalog z plikami TIFF i zapisz każdy wynik do pliku `.txt`.
2. **Integracja z Pandas** – Przechowuj wyodrębniony tekst wraz z metadanymi dla szybkiej analizy.
3. **Podejście hybrydowe** – Połącz OCR z bibliotekami NLP, takimi jak `spaCy`, aby wyodrębnić jednostki (nazwy, daty, kwoty) ze zeskanowanych faktur.
4. **Alternatywne formaty plików** – Zamień `Image.load` na `Image.from_bytes`, aby obsługiwać obrazy pochodzące z API lub bazy danych.

Wszystkie te pomysły opierają się na podstawowej idei **wyodrębniania tekstu z obrazu** i **przekształcania zeskanowanego tekstu obrazu** w coś, co maszyny mogą zrozumieć.

## Zakończenie

Przeszliśmy przez przejrzysty, kompleksowy **podstawowy przykład OCR**, który pokazuje **jak zrobić OCR w Pythonie**, jak **odczytać plik TIFF w Pythonie** oraz jak **wyodrębnić tekst z obrazu** przy użyciu zaledwie kilku linii. Skrypt jest samodzielny, zawiera obsługę błędów i bezpośrednio wypisuje wynik, co czyni go solidną bazą dla każdego projektu, który potrzebuje przekształcić zeskanowane dokumenty w edytowalny tekst.

Śmiało eksperymentuj — zamień backend OCR, dostosuj przetwarzanie wstępne lub podłącz wynik do dalszego przepływu pracy. Nie ma granic, gdy możesz niezawodnie **przekształcić zeskanowany tekst obrazu** w przeszukiwalne dane.

Masz pytania dotyczące przypadków brzegowych, pakietów językowych lub optymalizacji wydajności? zostaw komentarz poniżej i szczęśliwego kodowania! 

![how to ocr python example](/images/ocr-python-example.png "Screenshot of how to ocr python script output")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}