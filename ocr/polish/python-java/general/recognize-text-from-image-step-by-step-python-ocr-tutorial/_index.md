---
category: general
date: 2026-03-26
description: Rozpoznawaj tekst z obrazu szybko, ucząc się, jak wczytać obraz do OCR
  i wyodrębnić dane z określonego obszaru. Skorzystaj z tego praktycznego przewodnika.
draft: false
keywords:
- recognize text from image
- load image for ocr
- OCR region of interest
- extract text from ROI
- Python OCR library
- image preprocessing for OCR
language: pl
og_description: Rozpoznawaj tekst z obrazu w Pythonie, ładując obraz do OCR, definiując
  obszar zainteresowania i wyodrębniając czysty tekst. Poznaj pełny przebieg.
og_title: Rozpoznawanie tekstu z obrazu – Kompletny przewodnik po OCR w Pythonie
tags:
- OCR
- Python
- Image Processing
title: Rozpoznawanie tekstu z obrazu – krok po kroku tutorial OCR w Pythonie
url: /pl/python-java/general/recognize-text-from-image-step-by-step-python-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznawanie tekstu z obrazu – Kompletny przewodnik po OCR w Pythonie

Kiedykolwiek potrzebowałeś **rozpoznać tekst z obrazu**, ale nie wiedziałeś, od czego zacząć? Może masz zeskanowany formularz, paragon lub zrzut ekranu i po prostu chcesz uzyskać słowa znajdujące się w określonym polu. Dobra wiadomość jest taka, że kilkoma liniami Pythona możesz wczytać obraz do OCR, skupić się na jednej regionie i wyciągnąć dokładny tekst, którego potrzebujesz — bez ręcznego kopiowania.

W tym samouczku przejdziemy przez cały proces: wczytanie obrazu, zdefiniowanie regionu zainteresowania (ROI), uruchomienie silnika OCR i wydrukowanie wyniku. Po zakończeniu będziesz mógł wstawić ten fragment kodu do dowolnego projektu, który wymaga wyodrębnienia tekstu z konkretnej części obrazu. Bez ciężkich potoków przetwarzania obrazu, po prostu czysty, czytelny kod, który działa już dziś.

## Prerequisites

- Python 3.8+ zainstalowany  
- Pakiet `ocr` (lub dowolna kompatybilna biblioteka OCR) – zainstaluj za pomocą `pip install ocr-lib` (zamień na rzeczywistą nazwę pakietu, którego używasz)  
- Obraz PNG/JPEG zawierający formularz, który chcesz odczytać  
- Podstawowa znajomość funkcji i klas w Pythonie  

Jeśli już czujesz się z tym komfortowo, świetnie — możesz przejść dalej. W przeciwnym razie złap szybką kawę i upewnij się, że powyższe elementy są gotowe; kolejne kroki zakładają ich dostępność.

## Step 1: Create an OCR Engine Instance – “recognize text from image” Core

Pierwszą rzeczą, której potrzebujemy, jest obiekt, który potrafi komunikować się z silnikiem OCR. Pomyśl o nim jako o mózgu, który później **rozpozna tekst z obrazu**.

```python
import ocr  # Import the OCR library

# Initialize the engine
ocr_engine = ocr.OcrEngine()
```

> **Why this matters:** Inicjalizacja silnika raz pozwala ponownie używać ustawień (takich jak pakiety językowe) w wielu obrazach, co zwiększa wydajność i utrzymuje kod w porządku.

## Step 2: Load Image for OCR – Bringing the Picture Into Memory

Teraz faktycznie **wczytujemy obraz do OCR**. Biblioteka udostępnia wygodną metodę statyczną, która odczytuje plik i zwraca obiekt zrozumiały dla silnika.

```python
# Load the source image (replace the path with your own)
image_path = "YOUR_DIRECTORY/form.png"
ocr_engine.set_image(ocr.Imaging.Image.load(image_path))
```

> **Pro tip:** Jeśli Twój obraz jest duży, rozważ jego zmniejszenie przed wczytaniem. Mniejsze obrazy przyspieszają OCR bez utraty dokładności w przypadku większości drukowanego tekstu.

## Step 3: Define the OCR Region of Interest (ROI)

Często nie potrzebujesz całej strony — tylko konkretnego pola, w którym użytkownik wpisał dane. Zdefiniowanie **regionu zainteresowania OCR** mówi silnikowi, aby ignorował resztę, co redukuje szum i przyspiesza przetwarzanie.

```python
# Define ROI: (left, top, width, height) in pixels
region_of_interest = ocr.Rectangle(120, 340, 560, 90)

# Register the ROI with the engine
ocr_engine.add_region_of_interest(region_of_interest)
```

> **Why focus on ROI?**  
> - **Speed:** Silnik skanuje mniej pikseli.  
> - **Accuracy:** Grafika w tle poza ROI może mylić rozpoznawanie znaków.  
> - **Simplicity:** Otrzymujesz czysty ciąg znaków, który dokładnie odpowiada interesującemu Cię polu.

## Step 4: Run the OCR Process – The Moment of Truth

Po skonfigurowaniu wszystkiego w końcu **rozpoznajemy tekst z obrazu** w zdefiniowanym ROI.

```python
# Execute OCR on the specified region
ocr_result = ocr_engine.recognize()
```

Jeśli silnik obsługuje wiele regionów, `ocr_result` będzie zawierał listę; w naszym przypadku jednego ROI jest to prosty obiekt z metodą `get_text()`.

## Step 5: Extract and Print the Text – Getting the Final Output

Teraz wyciągamy czysty ciąg znaków z obiektu wyniku i wyświetlamy go. To miejsce, w którym możesz podłączyć wynik do bazy danych, pliku CSV lub dowolnej logiki dalszej.

```python
# Retrieve the recognized text
extracted_text = ocr_result.get_text()

# Show the result
print("Text inside ROI:\n", extracted_text)
```

**Expected output** (przykład dla wypełnionego pola imienia):

```
Text inside ROI:
 John Doe
```

Jeśli silnik OCR zwróci dodatkowe spacje lub podziały linii, możesz je oczyścić za pomocą `.strip()` lub wyrażenia regularnego.

## Handling Common Edge Cases

| Situation                              | What to Do                                                               |
|----------------------------------------|--------------------------------------------------------------------------|
| **Low‑resolution image**               | Zwiększ rozdzielczość przy użyciu `Pillow` (`Image.resize`) przed wczytaniem. |
| **Skewed or rotated text**             | Zastosuj korekcję obrotu (`ocr.Imaging.Image.rotate`). |
| **Multiple languages**                | Ustaw pakiet językowy w silniku: `ocr_engine.set_language('eng+spa')`. |
| **No ROI defined**                     | Pomiń `add_region_of_interest`; silnik przetworzy cały obraz. |
| **Unexpected characters (e.g., commas)** | Przetwórz łańcuch po uzyskaniu: `extracted_text.replace(',', '')`. |

Te wskazówki utrzymują Twój potok **load image for OCR** odporny, nawet gdy materiał źródłowy nie jest idealny.

## Full Working Example – Copy, Paste, Run

Poniżej znajduje się kompletny skrypt, który możesz wkleić do pliku `.py` i uruchomić. Zawiera wszystkie importy, obsługę błędów oraz mały pomocnik weryfikujący istnienie obrazu.

```python
import os
import ocr

def recognize_text_from_image(image_path: str,
                              roi: tuple = (120, 340, 560, 90)):
    """
    Recognize text from a specific region of an image.

    Parameters
    ----------
    image_path : str
        Full path to the image file.
    roi : tuple
        (left, top, width, height) defining the region of interest.

    Returns
    -------
    str
        The extracted text, stripped of surrounding whitespace.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Step 1 – create engine
    engine = ocr.OcrEngine()

    # Step 2 – load image for OCR
    engine.set_image(ocr.Imaging.Image.load(image_path))

    # Step 3 – define ROI
    left, top, width, height = roi
    engine.add_region_of_interest(ocr.Rectangle(left, top, width, height))

    # Step 4 – run OCR
    result = engine.recognize()

    # Step 5 – extract text
    text = result.get_text().strip()
    return text


if __name__ == "__main__":
    # Adjust the path to point at your form image
    img_path = "YOUR_DIRECTORY/form.png"

    try:
        roi_text = recognize_text_from_image(img_path)
        print("Text inside ROI:\n", roi_text)
    except Exception as e:
        print("OCR failed:", e)
```

Uruchomienie tego skryptu wypisuje wyczyszczony ciąg znaków z ROI, dostarczając gotowy do użycia fragment danych.

## Conclusion

Masz teraz przejrzystą, kompleksową metodę **rozpoznawania tekstu z obrazu** poprzez najpierw **wczytanie obrazu do OCR**, zdefiniowanie precyzyjnego **regionu zainteresowania OCR**, a na końcu wyodrębnienie czystego tekstu. Podejście działa z dowolną biblioteką OCR w Pythonie, która podąża za przedstawionym wzorcem, i możesz je łatwo rozszerzyć o obsługę wielu ROI, różnych języków lub kroków wstępnego przetwarzania.

Następnie możesz zbadać:

- **przetwarzanie obrazu przed OCR** (progowanie, odszumianie), aby zwiększyć dokładność przy szumnych skanach.  
- Wykorzystanie wyniku **extract text from ROI** do wypełnienia pandas DataFrame w celu analizy danych hurtowych.  
- Przejście na usługę OCR w chmurze (Google Vision, Azure Computer Vision), gdy potrzebna jest wyższa niezawodność w skali.

Wypróbuj, dopasuj współrzędne prostokąta do własnych formularzy i obserwuj, jak automatyzacja przejmuje kontrolę. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}