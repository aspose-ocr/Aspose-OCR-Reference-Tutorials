---
category: general
date: 2026-03-26
description: Dowiedz się, jak obracać obraz i wykonywać OCR w Pythonie. Ten przewodnik
  pokazuje także, jak wstępnie przetwarzać obraz pod OCR i efektywnie wyodrębniać
  tekst z obrazu.
draft: false
keywords:
- how to rotate image
- how to perform ocr
- preprocess image for ocr
- recognize text from image
- how to extract text from image
language: pl
og_description: Jak poprawnie obrócić obraz i następnie rozpoznać tekst z obrazu przy
  użyciu Aspose OCR. Postępuj zgodnie z tym szczegółowym poradnikiem, aby wstępnie
  przetworzyć obraz pod OCR i wyodrębnić tekst z obrazu.
og_title: Jak obrócić obraz i przeprowadzić OCR – Kompletny przewodnik Pythona
tags:
- Aspose
- Python
- Image Processing
- OCR
title: Jak obrócić obraz i wykonać OCR przy użyciu Aspose w Pythonie
url: /pl/python-java/general/how-to-rotate-image-and-perform-ocr-with-aspose-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak obrócić obraz i wykonać OCR przy użyciu Aspose w Pythonie

Kiedykolwiek zastanawiałeś się **how to rotate image**, aby silnik OCR naprawdę mógł odczytać tekst? Być może zeskanowałeś formularz, który skończył się po bokach, lub zdjęcie z kamery obróciło się o 90° zgodnie z ruchem wskazówek zegara. W takim wypadku tekst wygląda dobrze dla ludzkiego oka, ale silnik OCR widzi bałagan. Dobra wiadomość? To bułka z masłem, aby naprawić orientację, przyciąć interesujący Cię obszar i następnie wyodrębnić tekst — wszystko przy kilku linijkach Pythona i bibliotek Aspose.

W tym tutorialu przeprowadzimy Cię przez cały proces: od wczytania obróconego pliku TIFF, korekty jego orientacji, **preprocess image for OCR**, aż po **recognize text from image**. Po zakończeniu będziesz wiedział, **how to perform OCR** na dowolnym obrazie i będziesz w stanie **extract text from image** z pewnością.

## Czego będziesz potrzebować

- Python 3.8+ (kod działa z każdą nowszą wersją)
- pakiety `asposeocrjava` i `asposeimaging` zainstalowane za pomocą `pip`
- przykładowy obraz wymagający obrotu (np. `rotated_form.tif`)
- odrobina ciekawości dotyczącej przetwarzania obrazów

Nie są wymagane ciężkie frameworki — wystarczą dwa pakiety Aspose i odrobina logiki w Pythonie.

---

## Krok 1: Zainstaluj pakiety Aspose (How to Perform OCR)

Zanim będziemy mogli **rotate image** lub **recognize text from image**, potrzebujemy bibliotek, które faktycznie wykonują ciężką pracę.

```bash
pip install asposeocrjava asposeimaging
```

> **Pro tip:** Jeśli pracujesz za korporacyjnym proxy, dodaj `--proxy http://proxy:port` do polecenia. Pakiety są czystymi wrapperami Pythona wokół rdzenia Aspose .NET/Java, więc instalacja jest zazwyczaj natychmiastowa.

---

## Krok 2: Wczytaj plik źródłowy i obróć go – podstawowy krok „How to Rotate Image”

```python
from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

# Load the original, incorrectly oriented image
source_image = Image.load("YOUR_DIRECTORY/rotated_form.tif")

# Rotate 90° clockwise – this fixes the orientation for OCR
rotated_image = source_image.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)
```

> **Why rotate?** Większość silników OCR zakłada, że tekst czyta się od lewej do prawej i od góry do dołu. Jeśli bitmapa jest obrócona na bok, silnik zwróci albo bełkot, albo nic. Obrót wyrównuje siatkę pikseli do oczekiwanego porządku czytania, co dramatycznie zwiększa dokładność.

> **Edge case:** Jeśli nie jesteś pewien, czy obraz wymaga obrotu o 90°, 180° czy 270°, możesz sprawdzić `source_image.width` vs `source_image.height` lub użyć tagów orientacji `exif`. Metoda `rotate_flip` Aspose obsługuje także `ROTATE_180` i `ROTATE_270_CLOCKWISE`.

> **Image preview (optional):**  
> ![przykład jak obrócić obraz](/assets/rotate-demo.png "Jak obrócić obraz – przed i po obrocie")

---

## Krok 3: Przytnij obszar zainteresowania – Preprocess Image for OCR

Często potrzebujesz tylko małej części strony — na przykład pola podpisu lub bloku liczb. Przycięcie usuwa szumy i przyspiesza **how to perform OCR**.

```python
# Define the rectangle that encloses the text you care about
# (x=100, y=200, width=800, height=300) – adjust to your form
roi = Rectangle(100, 200, 800, 300)

# Crop the rotated image to that rectangle
roi_image = rotated_image.crop(roi)
```

> **Why crop?** Zmniejszenie rozmiaru obrazu ogranicza przestrzeń wyszukiwania silnika OCR, co zmniejsza liczbę fałszywych trafień i skraca czas przetwarzania. Pomaga to również, gdy plik źródłowy zawiera znaki wodne lub inne grafiki, które mogą mylić silnik.

> **Tip:** Jeśli pracujesz z wieloma polami, powtórz krok przycinania z różnymi prostokątami i uruchom OCR na każdym fragmencie osobno.

---

## Krok 4: Zainicjalizuj silnik OCR – rdzeń „How to Perform OCR”

```python
# Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

> **Behind the scenes:** Aspose OCR wykorzystuje kombinację Tesseract i własnej analizy obrazu. Utworzenie silnika raz i ponowne użycie go dla wielu obrazów jest bardziej wydajne niż tworzenie nowego obiektu przy każdym użyciu.

---

## Krok 5: Przekaż przycięty obraz i rozpoznaj tekst – How to Extract Text from Image

```python
# Set the cropped image as the input for OCR
ocr_engine.set_image(roi_image)

# Run the recognition process
result = ocr_engine.recognize()

# Extract the plain text
extracted_text = result.get_text()
print(extracted_text)
```

### Oczekiwany wynik

Jeśli ROI zawiera frazę „Invoice #12345 – Paid”, zobaczysz coś podobnego do:

```
Invoice #12345 – Paid
```

Jeśli OCR ma problemy, możesz otrzymać dodatkowe spacje lub błędnie odczytane znaki (np. „Invo1ce #I2345 – Pa1d”). Wtedy wchodzą w grę triki **preprocess image for OCR** — takie jak dostosowanie kontrastu lub zastosowanie binaryzacji. Aspose oferuje dodatkowe filtry, które możesz łączyć przed krokiem 5, ale podstawowy przepływ powyżej działa dla większości czystych skanów.

---

## Krok 6: Opcjonalnie – Dostosuj ustawienia OCR (Advanced “How to Perform OCR”)

```python
# Example: Restrict recognition to English alphanumerics only
ocr_engine.get_recognition_settings().set_recognition_language("en")
ocr_engine.get_recognition_settings().set_characters_blacklist("!@#$%^&*()")
```

> **When to use:** Użyj tego, gdy dokument zawiera wiele ozdobnych symboli, które nie są istotne. Czarna lista zmniejsza liczbę fałszywych wykryć.

---

## Pełny skrypt end‑to‑end

Łącząc wszystko razem, oto gotowy do uruchomienia skrypt, który **how to rotate image**, **preprocess image for OCR**, i w końcu **recognize text from image**:

```python
# -*- coding: utf-8 -*-
"""
Complete example: rotate, crop, and OCR an image with Aspose.
Author: Your Name
Date: 2026-03-26
"""

from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

def ocr_rotated_image(
    input_path: str,
    output_path: str = None,
    crop_rect: Rectangle = Rectangle(100, 200, 800, 300)
) -> str:
    """
    Loads an image, rotates it 90° clockwise, crops the region of interest,
    runs OCR, and returns the extracted text.

    Parameters
    ----------
    input_path : str
        Path to the original (possibly rotated) image file.
    output_path : str, optional
        If provided, saves the processed (rotated + cropped) image for inspection.
    crop_rect : Rectangle, optional
        Rectangle defining the ROI. Adjust to match your document layout.

    Returns
    -------
    str
        The plain text extracted from the ROI.
    """
    # Load and rotate
    src = Image.load(input_path)
    rotated = src.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)

    # Crop to region of interest
    roi = rotated.crop(crop_rect)

    # Optionally save the processed image for debugging
    if output_path:
        roi.save(output_path)

    # OCR
    engine = OcrEngine()
    engine.set_image(roi)
    result = engine.recognize()
    return result.get_text()

if __name__ == "__main__":
    text = ocr_rotated_image(
        "YOUR_DIRECTORY/rotated_form.tif",
        output_path="processed_roi.png"
    )
    print("=== Extracted Text ===")
    print(text)
```

Uruchomienie tego skryptu wypisuje rozpoznany tekst w konsoli i zapisuje wizualizację przetworzonego ROI jako `processed_roi.png`. Możesz otworzyć ten PNG, aby zweryfikować, że obrót i przycięcie zachowały się zgodnie z oczekiwaniami.

---

## Częste pytania i pułapki

| Pytanie | Odpowiedź |
|----------|--------|
| **What if the image is already upright?** | Krok obrotu jest idempotentny — obrót prawidłowo ustawionego obrazu o 90° oczywiście go zepsuje, więc powinieneś sprawdzić `source_image.width` vs `height` lub użyć danych orientacji EXIF przed wywołaniem `rotate_flip`. |
| **My OCR output contains extra line breaks.** | Użyj `result.get_text().replace("\n", " ").strip()` aby oczyścić, lub włącz `ocr_engine.get_recognition_settings().set_remove_line_breaks(True)`. |
| **Can I process PDFs directly?** | Tak — Aspose Imaging może wczytać strony PDF jako obrazy (`Image.load("file.pdf")`), po czym stosujesz te same kroki obrotu i OCR. |
| **Is there a way to batch‑process many files?** | Owiń `ocr_rotated_image` w pętlę po katalogu lub użyj `concurrent.futures` w Pythonie do równoległego przetwarzania. |
| **How do I handle languages other than English?** | Ustaw język rozpoznawania za pomocą `ocr_engine.get_recognition_settings().set_recognition_language("fr")` dla francuskiego itd. |

## Podsumowanie

Omówiliśmy **how to rotate image** prawidłowo, **preprocess image for OCR** poprzez przycinanie, oraz w końcu **how to perform OCR**, aby **recognize text from image** i **extract text from image** przy użyciu bibliotek Python Aspose. Pełny skrypt demonstruje praktyczny, gotowy do produkcji przepływ pracy, który możesz wstawić do dowolnego potoku automatyzacji.

Jeśli jesteś gotowy iść dalej, wypróbuj:

- **Image enhancement** (kontrast, binarizacja) przed OCR
- **Multiple ROI extraction** dla formularzy z wieloma polami
- **Batch processing** całych folderów zeskanowanych dokumentów
- **Integration** z systemami downstream (np. wprowadzanie wyekstrahowanych danych do bazy danych)

Śmiało dostosuj kod do własnych potrzeb i powodzenia w kodowaniu! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}