---
category: general
date: 2026-03-18
description: Szybko wykonaj OCR na obrazie przy użyciu Pythona. Dowiedz się, jak rozpoznawać
  tekst z pliku PNG, wczytywać obraz do OCR i wyodrębniać słowa z obrazu w przewodniku
  krok po kroku.
draft: false
keywords:
- run OCR on image
- recognize text from png
- python OCR example
- extract words from image
- load image for OCR
language: pl
og_description: Uruchom OCR na obrazie przy użyciu Pythona. Ten poradnik pokazuje,
  jak rozpoznawać tekst z pliku PNG, wczytać obraz do OCR oraz wyodrębnić słowa z
  obrazu, wraz z pełnym przykładem kodu.
og_title: Wykonaj OCR na obrazie – Przewodnik Pythona
tags:
- OCR
- Python
- Image Processing
title: Uruchom OCR na obrazie – Kompletny przykład OCR w Pythonie
url: /pl/python-java/general/run-ocr-on-image-complete-python-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uruchom OCR na obrazie – Kompletny przykład OCR w Pythonie

Kiedykolwiek potrzebowałeś **run OCR on image** plików, ale nie wiedziałeś od czego zacząć? Nie jesteś sam; wielu programistów napotyka tę barierę, gdy po raz pierwszy zajmuje się wyodrębnianiem tekstu ze skanowanych dokumentów. W tym tutorialu przeprowadzimy Cię przez **Python OCR example**, które pozwala **recognize text from PNG** plików, **load image for OCR**, oraz **extract words from image** z oceną pewności – wszystko w kilku linijkach kodu.

Omówimy wszystko, co jest potrzebne: wymaganą bibliotekę, jak skonfigurować silnik, dlaczego każdy krok ma znaczenie i jak wygląda wynik. Po zakończeniu będziesz mógł wkleić ten fragment do własnego projektu i natychmiast wyciągać tekst z dowolnego obrazu. Bez zbędnego gadania, tylko praktyczne, gotowe do uruchomienia rozwiązanie.

## Co będzie potrzebne

Zanim zaczniemy, upewnij się, że masz:

- Python 3.8 lub nowszy zainstalowany  
- Pakiet `ocrengine` (lub dowolną bibliotekę udostępniającą klasę `OcrEngine`). Możesz go zainstalować poleceniem `pip install ocrengine` – dostosuj nazwę, jeśli używasz innej biblioteki OCR, takiej jak `pytesseract`.  
- Plik obrazu (PNG, JPG, itp.), który chcesz przetworzyć – w tym przewodniku użyjemy `invoice.png`.  

To wszystko. Bez ciężkich zależności, bez zewnętrznych usług, tylko czysty Python.

![run OCR on image example showing a scanned invoice](/images/run-ocr-on-image.png)

*Alt text: przykład uruchomienia OCR na obrazie – skanowana faktura w trakcie przetwarzania*

## Krok 1 – Zainstaluj i zaimportuj bibliotekę OCR

Na początek wprowadzimy silnik OCR do naszego środowiska i go zaimportujemy. Jeśli używasz hipotetycznego pakietu `ocrengine`, import wygląda tak:

```python
# Install the package (run once in your terminal)
# pip install ocrengine

# Import the OCR engine class
from ocrengine import OcrEngine
```

**Dlaczego to ważne:** Importowanie właściwej klasy daje dostęp do metod, które wywołamy później, takich jak `setImageFromFile` i `recognize`. Jeśli pominiesz ten krok, Python zgłosi `ModuleNotFoundError`, a Ty nie będziesz w stanie nawet załadować obrazu.

## Krok 2 – Utwórz instancję silnika OCR

Teraz, gdy biblioteka jest gotowa, potrzebujemy obiektu silnika, który będzie przechowywał konfigurację i stan procesu rozpoznawania.

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()
```

*Pro tip:* Niektóre silniki OCR pozwalają dostosować modele językowe lub ustawienia DPI w tym miejscu. Dla podstawowego **python OCR example** domyślne ustawienia działają dobrze, ale jeśli masz skany o niskiej rozdzielczości, rozważ ich zmianę tutaj.

## Krok 3 – Załaduj obraz, który chcesz przetworzyć

Kolejnym logicznym krokiem jest **load image for OCR**. Wskazujesz silnikowi ścieżkę do pliku PNG (lub innego obsługiwanego formatu), który ma zostać przeanalizowany.

```python
# Step 3: Load the image you want to process
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice.png")
```

**Co się dzieje w tle?** Silnik odczytuje dane pikseli, konwertuje je do formatu zrozumiałego dla algorytmu rozpoznawania i przechowuje wewnętrznie. Jeśli ścieżka do pliku jest nieprawidłowa, otrzymasz `FileNotFoundError`, więc sprawdź, czy obraz rzeczywiście istnieje.

## Krok 4 – Uruchom algorytm rozpoznawania

Po załadowaniu obrazu w końcu **run OCR on image**, aby wyodrębnić treść tekstową.

```python
# Step 4: Run the recognition algorithm to obtain results
ocr_result = ocr_engine.recognize()
```

W tym momencie silnik skanuje bitmapę, stosuje dopasowanie wzorców i zwraca obiekt zawierający każde wykryte słowo, linię oraz metrykę pewności.

## Krok 5 – Przejdź po rozpoznanych słowach i wyświetl pewność

Najbardziej przydatną częścią każdego przepływu OCR jest **the confidence** dla każdego wyodrębnionego tokenu. Informuje ona, jak bardzo silnik jest pewny co do danego słowa, co pozwala odfiltrować wyniki o niskiej pewności, jeśli zajdzie taka potrzeba.

```python
# Step 5: Iterate over each recognized word and display its text with confidence
for recognized_word in ocr_result.getWords():
    word_text = recognized_word.getText()
    confidence = recognized_word.getConfidence()   # 0‑100%
    print(f"Word: '{word_text}' – confidence: {confidence}%")
```

**Oczekiwany wynik** (przykład):

```
Word: 'Invoice' – confidence: 98%
Word: 'Number' – confidence: 95%
Word: ':' – confidence: 92%
Word: '2023-07-15' – confidence: 97%
Word: 'Total' – confidence: 96%
Word: ':' – confidence: 93%
Word: '$' – confidence: 88%
Word: '1,250.00' – confidence: 94%
```

Teraz możesz dokładnie zobaczyć **what words were extracted from the image** i jak wiarygodne jest każde wykrycie. To jest sedno każdego **extract words from image** pipeline.

## Obsługa typowych przypadków brzegowych

### Co zrobić, gdy obraz jest w odcieniach szarości?

Niektóre silniki OCR działają lepiej na obrazach kolorowych. Jeśli zauważysz niską pewność we wszystkich wynikach, spróbuj przekonwertować PNG na wersję czarno‑białą o wyższym kontraście przed przekazaniem go silnikowi. Pillow może w tym pomóc:

```python
from PIL import Image, ImageOps

img = Image.open("YOUR_DIRECTORY/invoice.png")
bw = ImageOps.grayscale(img).point(lambda x: 0 if x < 128 else 255, '1')
bw.save("YOUR_DIRECTORY/invoice_bw.png")
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice_bw.png")
```

### Praca z wieloma językami

Jeśli dokument zawiera zarówno angielski, jak i hiszpański, będziesz chciał **recognize text from PNG** przy użyciu modelu wielojęzycznego. Większość silników pozwala ustawić listę języków podczas inicjalizacji:

```python
ocr_engine = OcrEngine(languages=["eng", "spa"])
```

### Filtrowanie słów o niskiej pewności

Czasami potrzebujesz tylko słów z pewnością powyżej, powiedzmy, 90 %. Proste filtrowanie wygląda tak:

```python
high_confidence_words = [
    w.getText()
    for w in ocr_result.getWords()
    if w.getConfidence() >= 90
]
print(high_confidence_words)
```

## Pełny, gotowy do uruchomienia skrypt

Łącząc wszystko razem, oto pojedynczy skrypt, który możesz skopiować‑wkleić i od razu uruchomić (wystarczy podmienić ścieżkę do swojego PNG).

```python
# run_ocr_on_image.py
# -------------------------------------------------
# Complete Python OCR example: load image for OCR,
# run OCR on image, and extract words from image.
# -------------------------------------------------

# Install the library first:
# pip install ocrengine pillow   # pillow only needed for optional preprocessing

from ocrengine import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the target PNG (replace with your own file)
    image_path = "YOUR_DIRECTORY/invoice.png"
    ocr_engine.setImageFromFile(image_path)

    # 3️⃣ Run recognition
    ocr_result = ocr_engine.recognize()

    # 4️⃣ Print each word with its confidence
    print("\n--- OCR Results ---")
    for word in ocr_result.getWords():
        text = word.getText()
        conf = word.getConfidence()
        print(f"Word: '{text}' – confidence: {conf}%")

if __name__ == "__main__":
    main()
```

Uruchom go za pomocą:

```bash
python run_ocr_on_image.py
```

Powinieneś zobaczyć listę słów i procenty pewności wypisane w konsoli, dokładnie tak jak pokazano wcześniej.

## Najczęściej zadawane pytania

**Czy to działa z plikami JPG lub TIFF?**  
Oczywiście. Metoda `setImageFromFile` akceptuje każdy format, który potrafi zdekodować podstawowa biblioteka, więc możesz **run OCR on image** pliki typu JPG, TIFF, BMP itp.

**Czy mogę przetwarzać wiele obrazów w pętli?**  
Tak. Umieść kroki ładowania i rozpoznawania wewnątrz pętli `for` iterującej po liście ścieżek do plików. Pamiętaj tylko, aby ponownie zainicjalizować silnik, jeśli biblioteka wymaga nowej instancji dla każdego obrazu.

**Co zrobić, gdy potrzebuję tekstu jako jednego ciągu znaków, a nie pojedynczych słów?**  
Większość obiektów wynikowych OCR udostępnia metodę `getText()`, która zwraca cały dokument. Przykład:

```python
full_text = ocr_result.getText()
print(full_text)
```

## Kolejne kroki i tematy pokrewne

Teraz, gdy wiesz, jak **run OCR on image**, rozważ dalsze eksploracje:

- **Post‑processing**: Użyj wyrażeń regularnych, aby oczyścić daty, kwoty lub identyfikatory wyodrębnione z faktur.  
- **Przetwarzanie wsadowe**: Połącz skrypt z `os.listdir()`, aby obsłużyć całe foldery zeskanowanych dokumentów.  
- **Alternatywne biblioteki**: `pytesseract` to popularna biblioteka open‑source; przepływ pracy jest podobny — wystarczy zamienić wywołania silnika.  
- **Eksport wyników**: Zapisz wyodrębnione słowa i oceny pewności do CSV, aby móc je dalej analizować.

Każde z tych rozszerzeń buduje się bezpośrednio na fundamencie, który tutaj stworzyliśmy, pozwalając przekształcić surowe dane OCR w użyteczną informację.

---

### TL;DR

Pokazaliśmy zwięzły **python OCR example**, który demonstruje, jak **load image for OCR**, **run OCR on image** i **extract words from image** z raportowaniem pewności. Pełny skrypt jest gotowy do uruchomienia, a Ty masz już wiedzę, aby dostosować go do dowolnego projektu, który wymaga **recognize text from PNG** (lub innych formatów). Wypróbuj, dostosuj progi pewności i zobacz, jak Twoje aplikacje stają się świadome tekstu w kilka minut. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}