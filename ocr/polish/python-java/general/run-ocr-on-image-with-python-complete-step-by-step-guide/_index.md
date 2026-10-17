---
category: general
date: 2026-06-06
description: Uruchom OCR na obrazie przy użyciu Pythona i zobacz wyniki pewności.
  Dowiedz się, jak filtrować słowa o niskiej pewności, ustawiać progi i radzić sobie
  z przypadkami brzegowymi.
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: pl
og_description: Uruchom OCR na obrazie w Pythonie, sprawdź poziomy pewności i odfiltruj
  słowa o niskiej pewności. Ten tutorial przeprowadzi Cię przez kompletny, gotowy
  do uruchomienia przykład.
og_title: Uruchom OCR na obrazie w Pythonie – pełny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Uruchom OCR na obrazie w Pythonie – Kompletny przewodnik krok po kroku
url: /pl/python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uruchom OCR na obrazie przy użyciu Pythona – Kompletny przewodnik krok po kroku

Czy kiedykolwiek potrzebowałeś **uruchomić OCR na obrazie** i nie byłeś pewien, jak uzyskać wiarygodny tekst? Nie jesteś sam — wielu programistów napotyka ten sam problem, gdy wyodrębnione słowa wyglądają niepewnie, a współczynnik pewności jest zagadką.  

W tym przewodniku od razu przejdziemy do działającego rozwiązania: zobaczysz, jak **uruchomić OCR na obrazie**, odczytać ogólną pewność i wyodrębnić słowa o niskiej pewności, które mogą wymagać ręcznej weryfikacji. Po zakończeniu będziesz mieć skrypt wielokrotnego użytku, zrozumiesz, dlaczego każda linia ma znaczenie, i będziesz wiedział, jak dostosować próg pewności dla własnych projektów.

## Co obejmuje ten tutorial

Przejdziemy przez cały przepływ pracy — od wczytania obrazu po wydrukowanie schludnego raportu słów, które spadły poniżej progu 80 % pewności. Po drodze omówimy:

* Wybór solidnego silnika OCR (użyjemy **EasyOCR**, popularnej biblioteki OCR w Pythonie)  
* Interpretację atrybutu `confidence`, który zwraca każdy wynik OCR  
* Filtrowanie słów przy użyciu własnego **progu pewności OCR**  
* Rozszerzenie skryptu o przetwarzanie wsadowe lub alternatywne silniki, takie jak **pytesseract**  

Nie wymagana jest wcześniejsza znajomość OCR, wystarczy podstawowa znajomość Pythona i działające środowisko (zalecany Python 3.9+).  

Gotowy, aby zamienić rozmyte zrzuty ekranu w czysty, przeszukiwalny tekst? Zaczynajmy.

---

## ## Jak uruchomić OCR na obrazie przy użyciu Pythona

Sednem tutorialu jest trzyetapowy fragment kodu, który odzwierciedla kod, który już widziałeś. Poniżej rozłożymy każdą linię, wyjaśnimy dlaczego jest użyta i podamy kompletny, gotowy do kopiowania skrypt.

### Krok 1: Zainstaluj i zaimportuj silnik OCR

Najpierw upewnij się, że biblioteka OCR jest dostępna. **EasyOCR** działa od razu dla wielu języków i podaje współczynnik pewności dla każdego słowa.

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*Dlaczego EasyOCR?* Zawiera model uczenia głębokiego wytrenowany na różnorodnych zestawach danych, więc zazwyczaj uzyskujesz wyższe wartości pewności niż starszy silnik Tesseract, szczególnie przy obrazach o mieszanej jakości.

> **Wskazówka:** Jeśli pracujesz w ograniczonym środowisku (np. mały kontener Docker), `pytesseract` może być lżejszy, ale utracisz część nowoczesnej dokładności, jaką zapewnia EasyOCR.

### Krok 2: Uruchom OCR na obrazie

Teraz faktycznie **uruchamiamy OCR na obrazie**. Metoda `recognize_image` z oryginalnego przykładu została zastąpiona wywołaniem `readtext` EasyOCR, które zwraca listę krotek `(bbox, text, confidence)`.

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

Każdy wpis w `ocr_results` wygląda tak:

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

Trzeci element (`0.92` w przykładzie) to współczynnik pewności w zakresie od 0 do 1.

### Krok 3: Podsumuj ogólną pewność

W przeciwieństwie do wcześniejszego fragmentu, który drukował pojedynczy atrybut `confidence`, EasyOCR podaje pewność dla każdego słowa. Aby uzyskać ogólne wyobrażenie, obliczymy ich średnią:

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*Dlaczego średnia?* Daje szybki przegląd stanu — jeśli ogólna pewność jest poniżej, powiedzmy, 70 %, prawdopodobnie musisz poprawić obraz (lepsze oświetlenie, wstępne przetwarzanie itp.).

### Krok 4: Lista słów o niskiej pewności

Teraz następuje część, która bezpośrednio odpowiada wymaganiu „wypisz słowa, których pewność jest poniżej żądanego progu”. Ustawimy domyślnie **próg pewności OCR** na 0.80 (80 %), ale możesz go zmienić.

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

Pętla drukuje każde słowo, które nie przeszło progu, wraz z jego procentową pewnością. To dokładny odpowiednik oryginalnej pętli `for recognized_word in recognition_result.words`, ale teraz działa z formatem wyjściowym EasyOCR.

---

## ## Zrozumienie współczynników pewności OCR

Pewność nie jest magiczną liczbą; to szacunek modelu, jak bardzo jest pewny konkretnej transkrypcji. Oto kilka rzeczy, które warto mieć na uwadze:

| Sytuacja | Typowa pewność | Co zrobić |
|-----------|-------------------|------------|
| Czyste, wysokiej rozdzielczości skanowanie | 0.95 – 1.00 | Nie wymaga dodatkowej pracy |
| Lekka rozmycie lub nierówne oświetlenie | 0.80 – 0.94 | Rozważ lekkie wstępne przetwarzanie (zwiększenie kontrastu) |
| Silny szum, obrócony tekst | < 0.70 | Zastosuj wstępne przetwarzanie obrazu (prostowanie, odszumianie) lub przejdź na inny silnik OCR |

> **Uwaga:** Niektóre języki (np. pismo odręczne kursywą) naturalnie dają niższe wyniki. Dostosuj próg odpowiednio.

### Przypadki brzegowe i warianty

1. **Przetwarzanie wsadowe** – Jeśli potrzebujesz **uruchomić OCR na obrazie** w trybie masowym, otocz powyższą logikę pętlą iterującą po katalogu.  
2. **Wiele języków** – Przekaż listę taką jak `['en', 'fr']` do `easyocr.Reader`, a silnik wykryje oba.  
3. **Alternatywne silniki** – Chcesz wypróbować **pytesseract**? Zastąp blok czytnika następującym:

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   Następnie będziesz musiał zaggregować pewności poszczególnych znaków do wartości na słowo — trochę więcej pracy, ale wykonalne.

4. **Triki wstępnego przetwarzania** – Zastosowanie filtrów OpenCV (`cv2.threshold`, `cv2.GaussianBlur`) może zwiększyć pewność przy szumnych skanach.  

---

## ## Pełny, gotowy do uruchomienia skrypt

Poniżej znajduje się kompletny plik Python, który możesz dodać do swojego projektu. Zapisz go jako `ocr_report.py` i uruchom `python ocr_report.py`. Upewnij się, że ścieżka do obrazu wskazuje na istniejący plik.

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**Oczekiwany wynik** (twoje liczby będą się różnić):

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

Jeśli każde słowo przekroczy próg 80 %, zobaczysz przyjazny komunikat „All words meet the confidence threshold.”.

---

## ## Najczęściej zadawane pytania (FAQ)

**Q: Czy to działa z PDF‑ami?**  
A: Nie bezpośrednio. Najpierw przekonwertuj każdą stronę PDF na obraz (np. przy użyciu `pdf2image`), a następnie podaj PNG/JPEG do skryptu.

**Q: Moje liczby pewności są wszystkie niskie — co mogę zrobić?**  
A: Spróbuj wstępnego przetwarzania obrazu: zwiększ kontrast, usuń szumy tła lub obróć obraz do poziomej linii bazowej. EasyOCR akceptuje także parametr `contrast_ths`, który możesz dostosować.

**Q: Czy mogę wyeksportować wyniki do CSV?**  
A: Oczywiście. Po pętli niskiej pewności zapisz `ocr_results` przy użyciu `csv.DictWriter`, gdzie każdy wiersz zawiera `text`, `confidence` oraz współrzędne prostokąta ograniczającego.

**Q: Czy istnieje wersja przyspieszona GPU?**  
A: EasyOCR automatycznie używa CUDA, jeśli zainstalowano kompatybilny GPU i PyTorch. Sprawdź za pomocą `torch.cuda.is_available()` przed uruchomieniem skryptu.

---

## Zakończenie

**Uruchomiliśmy właśnie OCR na obrazie** przy użyciu Pythona, sprawdziliśmy ogólną pewność i wyodrębniliśmy wszystkie słowa o niskiej pewności, które wymagają

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}