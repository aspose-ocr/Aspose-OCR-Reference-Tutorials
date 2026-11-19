---
category: general
date: 2026-07-05
description: Jak szybko prostować obraz. Dowiedz się, jak wstępnie przetwarzać obraz
  pod OCR, korygować jego obrót i konwertować skan na tekst w Pythonie.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- convert scan to text
- correct image rotation
language: pl
og_description: Jak prostować obraz i przygotować go do OCR. Ten przewodnik pokazuje,
  jak skorygować obrót obrazu i wyodrębnić tekst z obrazu przy użyciu Pythona.
og_title: Jak prostować obraz – krok po kroku przetwarzanie wstępne OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to deskew image quickly. Learn to preprocess image for OCR, correct
    image rotation, and convert scan to text with Python.
  headline: How to Deskew Image – Complete Guide for OCR Preprocessing
  type: TechArticle
tags:
- OCR
- image-processing
- Python
title: Jak wyprostować obraz – Kompletny przewodnik po przetwarzaniu wstępnym OCR
url: /pl/python-java/general/how-to-deskew-image-complete-guide-for-ocr-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyrównać obraz – Kompletny przewodnik po przetwarzaniu wstępnym OCR

Zastanawiałeś się kiedyś **jak wyrównać obraz**, który wygląda, jakby został zrobiony krzywym skanerem? Nie jesteś jedyny. W wielu rzeczywistych projektach pierwszą rzeczą, którą musisz zrobić, zanim będziesz mógł **wyodrębnić tekst z obrazu**, jest wyprostowanie tego skrzywienia.  

W tym samouczku przeprowadzimy Cię przez praktyczny, kompleksowy przykład, który **przetwarza obraz pod OCR**, koryguje rotację i w końcu **konwertuje skan na tekst** przy użyciu biblioteki OCR w Pythonie. Bez niejasnych odniesień, tylko działający skrypt, który możesz skopiować‑wkleić, oraz wskazówki dotyczące typowych pułapek.  

## Co osiągniesz

* Wczytaj dowolny zeskanowany plik JPEG lub PNG, który jest lekko przechylony.  
* Zastosuj filtr deskew i krok binarizacji, aby zwiększyć dokładność OCR.  
* Uruchom silnik OCR i **wyodrębnij tekst z obrazu** w sposób niezawodny.  
* Zrozum, dlaczego **poprawna rotacja obrazu** ma znaczenie dla dalszego wyodrębniania tekstu.  

### Wymagania wstępne

* Python 3.9+ zainstalowany na Twoim komputerze.  
* Pakiet OCR instalowalny przez pip, który naśladuje przestrzeń nazw `ocr` używaną w przykładzie (np. lekka nakładka na Tesseract).  
* Podstawowa znajomość funkcji Pythona i koncepcji przetwarzania obrazu.  

Jeśli masz to wszystko, zanurzmy się.

![how to deskew image example](deskew_before_after.png){alt="jak wyrównać obraz – przed i po korekcji"}

## Krok 1: Konfiguracja silnika OCR – Jak wyrównać obraz przy użyciu Pythona

Na początek potrzebujesz silnika OCR, który rozumie język Twojego dokumentu. Poniższy fragment pokazuje minimalny kod startowy, aby utworzyć silnik i poinformować go, że pracujesz z tekstem w języku angielskim.

```python
import ocr  # Assume this is a wrapper around your OCR backend

# Create an OCR engine instance and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH
```

*Dlaczego to ważne:*  Ustawienie języka silnika wpływa na zestaw znaków i słownik, którego używa. Pominięcie tego kroku może spowodować, że OCR błędnie zinterpretuje popularne słowa, szczególnie po **korekcji rotacji obrazu**.

## Krok 2: Wczytaj zeskanowany obraz, który chcesz wyprostować

Teraz wczytujemy plik do pamięci. Zastąp `"YOUR_DIRECTORY/skewed_scan.jpg"` ścieżką do własnego obrazu.

```python
# Load the raw scanned image
raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")
```

Jeśli obraz jest już w tablicy NumPy lub w obiekcie OpenCV `Mat`, możesz odpowiednio dostosować loader – kluczowe jest, aby obiekt udostępniał metodę `apply_filter` używaną później.

## Krok 3: Przetwarzanie obrazu pod OCR – Deskew i binaryzacja

Tutaj dzieje się magia. Łączymy dwa filtry:

1. **Deskew** – automatycznie wykrywa dominującą linię bazową tekstu i obraca obraz z powrotem do poziomu.  
2. **Binarize (Otsu)** – konwertuje obraz do czysto czarno‑białego, co dramatycznie zwiększa współczynniki rozpoznawania.  

```python
# Preprocess: deskew then binarize
preprocessed_image = (
    raw_image
    .apply_filter(ocr.Filter.deskew())          # <-- how to deskew image
    .apply_filter(ocr.Filter.binarize_otsu())  # improves OCR reliability
)
```

*Wskazówka:*  Jeśli zauważysz, że tekst nadal wygląda rozmycie po binaryzacji, spróbuj dostroić kontrast lub użyć innej metody progowania. Moduł `ocr.Filter` często zawiera `adaptive_threshold()` dla trudniejszych przypadków.

## Krok 4: Uruchom OCR – Wyodrębnij tekst z obrazu

Mając czyste, wyprostowane płótno, przekazujemy obraz do silnika. Obiekt wyniku zawiera rozpoznany ciąg znaków, oceny pewności oraz nawet ramki ograniczające, jeśli będą potrzebne później.

```python
# Perform recognition on the preprocessed image
recognition_result = engine.recognize(preprocessed_image)

# Print the raw text output
print(recognition_result.text)
```

Typowy wynik wygląda następująco:

```
Invoice #12345
Date: 2026-07-01
Total: $1,250.00
Thank you for your business!
```

Zauważ, jak podziały linii idealnie się zgadzają? To korzyść płynąca z **poprawnej rotacji obrazu** – OCR nie musi już zgadywać orientacji linii.

## Krok 5: Połącz wszystko – Skrypt jednoplikowy do konwersji skanu na tekst

Poniżej znajduje się pełny, działający skrypt, który łączy wszystkie omówione elementy. Zapisz go jako `deskew_ocr.py` i uruchom `python deskew_ocr.py`.

```python
#!/usr/bin/env python3
"""
Complete example: how to deskew image, preprocess it for OCR,
and extract text from a scanned document.
"""

import ocr  # Replace with your actual OCR library import

def main():
    # 1️⃣ Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Load the image (change path as needed)
    raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")

    # 3️⃣ Preprocess – deskew then binarize
    preprocessed = (
        raw_image
        .apply_filter(ocr.Filter.deskew())          # how to deskew image
        .apply_filter(ocr.Filter.binarize_otsu())  # preprocess image for OCR
    )

    # 4️⃣ Recognize text
    result = engine.recognize(preprocessed)

    # 5️⃣ Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

### Dlaczego to działa

* **Deskew najpierw** – obracanie obrazu przed binaryzacją zapewnia, że algorytm progowania działa na płaskim horyzoncie.  
* **Binarize po deskew** – metoda Otsu zakłada dwumodalny histogram; przechylona strona zniszczyłaby to założenie.  
* **Model języka angielskiego** – informuje OCR, jakich znaków się spodziewać, redukując fałszywe trafienia.  

Jeśli musisz obsłużyć inne języki, po prostu zamień `ocr.Language.ENGLISH` na odpowiedni enum.

## Częste pytania i przypadki brzegowe

| Pytanie | Odpowiedź |
|----------|--------|
| *Co zrobić, jeśli skan jest do góry nogami?* | Filtr `deskew()` zazwyczaj wykrywa również rotację o 180°. Jeśli nie zadziała, wywołaj `apply_filter(ocr.Filter.rotate(180))` przed deskew. |
| *Mój dokument zawiera kolorowe grafiki – czy binaryzacja je usunie?* | Tak. W przypadku mieszanej zawartości rozważ użycie tylko `ocr.Filter.deskew()`, a następnie uruchom OCR na kolorowym obrazie. Nadal możesz wyodrębnić tekst, zachowując grafiki. |
| *Czy mogę przetwarzać batch plików?* | Owiń logikę w pętlę, odczytuj każdą ścieżkę pliku z listy i zapisz każde `result.text` w osobnym pliku `.txt`. |
| *Jak poprawić dokładność przy skanach o niskiej rozdzielczości?* | Zwiększ rozdzielczość obrazu przy użyciu filtru bikubicznego **przed** deskew, a następnie zastosuj filtr wyostrzający. Więcej pikseli daje silnikowi OCR lepsze wskazówki. |

## Bonus: Wizualna weryfikacja deskew

Jeśli chcesz zobaczyć przed‑ i po‑korekcję obok siebie, dodaj krótki fragment Matplotlib:

```python
import matplotlib.pyplot as plt

def show_comparison(original, processed):
    fig, axs = plt.subplots(1, 2, figsize=(10, 4))
    axs[0].imshow(original.to_numpy(), cmap='gray')
    axs[0].set_title('Original')
    axs[0].axis('off')

    axs[1].imshow(processed.to_numpy(), cmap='gray')
    axs[1].set_title('Deskewed & Binarized')
    axs[1].axis('off')
    plt.show()

show_comparison(raw_image, preprocessed)
```

Widok poprawionego wyrównania może być uspokajający, szczególnie gdy debugujesz trudny batch skanów.

## Zakończenie

Omówiliśmy **jak wyrównać obraz**, dlaczego **przetwarzanie obrazu pod OCR** jest niezbędne oraz jak **wyodrębnić tekst z obrazu**, aby w końcu **przekonwertować skan na tekst**. Przepływ pracy — wczytaj → deskew → binarize → rozpoznaj — zapewnia, że OCR widzi czystą, prostą stronę, co przekłada się na wyższą dokładność i mniej ręcznych poprawek.  

Co dalej w Twojej podróży z OCR? Spróbuj eksperymentować z:

* Różnymi pakietami językowymi (`ocr.Language.FRENCH` itp.).  
* Dodaniem kroku analizy układu w celu wykrycia kolumn lub tabel.  
* Eksportowaniem wyników OCR do przeszukiwalnych PDF-ów przy użyciu biblioteki PDF.  

Śmiało zostaw komentarz, jeśli napotkasz problem, lub podziel się własnymi modyfikacjami w obsłudze szczególnie uparcie skanowanych dokumentów. Szczęśliwego kodowania i niech Twoje obrazy zawsze będą idealnie wypoziomowane!  

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i eksplorować alternatywne podejścia implementacyjne w własnych projektach.

- [Jak używać AspOCR: Filtry przetwarzania obrazu OCR dla .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Wyodrębnij tekst z obrazu w C# z wyborem języka przy użyciu Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Jak wykonać OCR obrazu – Przeprowadź OCR na obrazie w rozpoznawaniu obrazów OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}