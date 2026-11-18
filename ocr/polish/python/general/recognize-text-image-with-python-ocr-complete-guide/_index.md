---
category: general
date: 2026-06-28
description: Dowiedz się, jak rozpoznawać tekst na obrazach przy użyciu OCR w Pythonie,
  wyodrębniać pliki PNG z tekstem i drukować rozpoznany tekst z solidną obsługą błędów.
draft: false
keywords:
- recognize text image
- extract text png
- load image ocr
- process image ocr
- print recognized text
language: pl
og_description: Samouczek krok po kroku, jak rozpoznać tekst na obrazie w Pythonie,
  wyodrębnić tekst z pliku PNG i bezpiecznie wydrukować rozpoznany tekst.
og_title: Rozpoznawanie tekstu na obrazie w Python OCR – kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text image using Python OCR, extract text png
    files, and print recognized text with robust error handling.
  headline: recognize text image with Python OCR – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Rozpoznawanie tekstu na obrazie przy użyciu Python OCR – Kompletny przewodnik
url: /pl/python/general/recognize-text-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rozpoznawanie obrazu tekstowego w Python OCR – Kompletny przewodnik

Zastanawiałeś się kiedyś, jak **rozpoznać obraz tekstowy** w skrypcie Pythona bez wprowadzania ciężkiego frameworka? Nie jesteś sam. Wielu programistów potrzebuje szybkiego sposobu na *załadowanie obrazu OCR* zrzutu ekranu, zeskanowanego paragonu lub prostego pliku PNG i uzyskanie tekstu z powrotem.  

W tym samouczku podłączymy minimalny silnik OCR, dodamy własny logger, **załadujemy obraz OCR**, uruchomimy **przetwarzanie obrazu OCR**, i w końcu **wydrukujemy rozpoznany tekst**. Po zakończeniu będziesz mieć samodzielny skrypt, który może także **wyodrębnić tekst z plików png** na żądanie.

## Co wyniesiesz z tego tutorialu

- W pełni funkcjonalny fragment kodu Python, który tworzy silnik OCR, loguje każdy krok i elegancko obsługuje błędy.  
- Jasne wyjaśnienia *dlaczego* każda linia ma znaczenie — abyś mógł dostosować kod do Tesseract, EasyOCR lub dowolnego innego backendu.  
- Wskazówki dotyczące typowych pułapek (brakujące czcionki, uszkodzone PNG) oraz jak je debugować.  

### Wymagania wstępne

- Python 3.8+ zainstalowany  
- Biblioteka OCR udostępniająca klasę `OcrEngine` (przykład używa fikcyjnego, ale typowego API; zamień ją na `pytesseract`, `easyocr` itp.).  
- Obraz PNG, który chcesz przeanalizować, zapisany jako `input.png` w folderze, którym zarządzasz.  

> **Wskazówka:** Jeśli używasz `pytesseract`, najpierw zainstaluj systemowy binarny Tesseract (`sudo apt install tesseract-ocr` na Linux) a potem `pip install pytesseract pillow`.

---

## ## Rozpoznawanie obrazu tekstowego: Konfiguracja loggera

Dobry logger to nieśpiewany bohater każdej rury OCR. Informuje Cię *kiedy* silnik się uruchomił, *jaki* plik otworzył i *dlaczego* mógł się nie powieść.

```python
# Step 1: Define a simple logger for the OCR engine
def my_logger(level, message):
    """
    level: str – e.g., "INFO", "WARN", "ERROR"
    message: str – human‑readable description of the event
    """
    print(f"[{level}] {message}")
```

*Dlaczego to ma znaczenie:*  
Logger oddziela diagnostyczny output od rdzenia OCR, co ułatwia przekierowanie logów do pliku, usługi monitorującej lub nawet UI później.  

---

## ## Załaduj obraz OCR: Dostarczanie silnikowi PNG

Zanim silnik będzie mógł **przetwarzać obraz OCR**, potrzebuje odpowiedniego obiektu obrazu. Większość bibliotek akceptuje instancję Pillow `Image`.

```python
from PIL import Image

# Step 2: Create the OCR engine and attach the logger
ocr_engine = OcrEngine(logging=my_logger)

# Step 3: Load the image to be processed
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Image.from_file(image_path))
my_logger("INFO", f"Loaded image from {image_path}")
```

*Kluczowe punkty:*  

- **load image ocr** – `Image.from_file` ukrywa szczegóły dekodowania PNG.  
- Trzymaj ścieżkę konfigurowalną; twarde kodowanie sprawia, że skrypt jest kruchy.  
- Wywołanie loggera potwierdza, że obraz został pomyślnie odczytany, co jest przydatne, gdy plik jest brakujący lub uszkodzony.

---

## ## Przetwarzanie obrazu OCR: Rozpoznawanie tekstu

Teraz zaczyna się ciężka praca. Silnik skanuje bitmapę, stosuje sieci neuronowe lub heurystyki i zwraca ciąg Unicode.

```python
# Step 4: Recognize text from the image
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:
    # Step 5: Handle OCR errors gracefully
    my_logger("ERROR", f"OCR failed with code {e.code}: {e.message}")
    extracted_text = None
```

*Dlaczego otaczamy to w `try/except`:*  
OCR może wybuchnąć przy niskiej rozdzielczości PNG, nieobsługiwanych przestrzeniach kolorów lub brakujących danych językowych. Przechwycenie `OcrException` pozwala **wydrukować rozpoznany tekst** tylko wtedy, gdy faktycznie istnieje, unikając niejasnych śladów stosu dla użytkowników końcowych.

---

## ## Wydrukuj rozpoznany tekst i wyodrębnij tekst PNG

Jeśli rozpoznanie się powiodło, wyświetlamy wynik i opcjonalnie zapisujemy go do pliku `.txt`, który odzwierciedla oryginalną nazwę PNG.

```python
if extracted_text:
    # Step 6: Print the recognized text
    print("Recognized text:", extracted_text)
    my_logger("INFO", "Printed recognized text to console")

    # Optional: Save extracted text for later use
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
```

*Co otrzymujesz:*  

- **print recognized text** – natychmiastowa wizualna informacja zwrotna w terminalu.  
- Plik `.txt` obok, który efektywnie **extract text png** do dalszego przetwarzania (indeksowanie wyszukiwania, wprowadzanie danych itp.).

---

## ## Typowe przypadki brzegowe i jak sobie z nimi radzić

| Sytuacja | Objaw | Rozwiązanie |
|-----------|---------|-----|
| PNG jest tylko w odcieniach szarości | OCR zwraca pusty ciąg | Konwertuj do RGB (`Image.convert("RGB")`) przed podaniem do silnika. |
| Język nieobsługiwany | `OcrException` z kodem `LANG_NOT_FOUND` | Zainstaluj pakiet językowy (np. `tesseract‑lang‑fra` dla francuskiego) i ustaw `ocr_engine.language = "fra"`. |
| Bardzo duży obraz ( > 5 MB ) | Wolne rozpoznawanie lub błąd pamięci | Zmniejsz rozmiar przy użyciu `image.thumbnail((2000, 2000))` przed `set_image`. |
| Nieoczekiwane znaki | Zniekształcony wynik | Upewnij się, że obraz jest naprawdę PNG; niektóre pliki udają PNG, ale są w rzeczywistości JPEG. Użyj `Image.verify()`, aby zweryfikować. |

---

## ## Pełny działający przykład (gotowy do kopiowania)

```python
# -*- coding: utf-8 -*-
"""
Complete script to recognize text image using a generic OCR engine.
Replace OcrEngine, OcrException with the concrete classes from your library.
"""

from PIL import Image

# ----------------------------------------------------------------------
# 1️⃣  Logger definition
# ----------------------------------------------------------------------
def my_logger(level: str, message: str) -> None:
    """Simple console logger."""
    print(f"[{level}] {message}")

# ----------------------------------------------------------------------
# 2️⃣  Engine creation & image loading
# ----------------------------------------------------------------------
ocr_engine = OcrEngine(logging=my_logger)   # <- adapt to your library

image_path = "YOUR_DIRECTORY/input.png"
try:
    img = Image.open(image_path)
    img.verify()                     # sanity check the PNG
    img = Image.open(image_path)     # reopen after verify
    ocr_engine.set_image(img)
    my_logger("INFO", f"Loaded image from {image_path}")
except Exception as load_err:
    my_logger("ERROR", f"Failed to load image: {load_err}")
    raise SystemExit(1)

# ----------------------------------------------------------------------
# 3️⃣  Text recognition
# ----------------------------------------------------------------------
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:            # replace with actual exception class
    my_logger("ERROR", f"OCR failed ({e.code}): {e.message}")
    extracted_text = None

# ----------------------------------------------------------------------
# 4️⃣  Output handling
# ----------------------------------------------------------------------
if extracted_text:
    print("Recognized text:", extracted_text)          # ✅ print recognized text
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
else:
    my_logger("WARN", "No text extracted; check image quality.")
```

**Oczekiwany output w konsoli (szczęśliwa ścieżka):**

```
[INFO] Loaded image from YOUR_DIRECTORY/input.png
[INFO] OCR succeeded
Recognized text: Invoice #12345
Total Amount: $1,250.00
Date: 2026‑06‑01
[INFO] Saved extracted text to YOUR_DIRECTORY/input.txt
```

Jeśli coś pójdzie nie tak, zobaczysz wyraźną linię `[ERROR]` z przyczyną, dzięki własnemu loggerowi.

---

## ## Kolejne kroki i tematy powiązane

- **extract text png** z partii: opakuj skrypt w pętlę `for`, która przechodzi przez drzewo katalogów.  
- **process image ocr** z wstępnym przetwarzaniem (prostowanie, zwiększanie kontrastu) przy użyciu OpenCV przed podaniem do silnika.  
- Przejdź na usługę OCR w chmurze (Google Vision, Azure Read), zamieniając implementację `OcrEngine` — Twój otaczający kod pozostaje taki sam.  
- Naucz się **print recognized text** do PDF‑ów przy użyciu `reportlab` dla automatycznego generowania raportów.  

---

## Podsumowanie

Właśnie przeszliśmy przez kompaktowy, gotowy do produkcji sposób na **rozpoznawanie obrazu tekstowego** w Pythonie, od ładowania PNG po **wydrukowanie rozpoznanego tekstu** i zapis wyniku. Dzięki wstrzyknięciu małego loggera, obsłudze wyjątków i opcjonalnemu zapisywaniu wyjścia, skrypt jest gotowy zarówno do szybkich eksperymentów, jak i integracji w większych pipeline’ach.

Wypróbuj go na własnych zrzutach ekranu, baw się przetwarzaniem obrazu i wkrótce będziesz wyodrębniać tekst z dowolnego PNG, który poddasz. Masz pytania? zostaw komentarz — powodzenia w OCR!  

![przykład rozpoznawania obrazu tekstowego](placeholder.png)


## Co powinieneś nauczyć się dalej?


Poniższe samouczki obejmują tematy ściśle powiązane, które budują na technikach przedstawionych w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Wyodrębnij tekst z obrazu przy użyciu Aspose OCR – Przewodnik krok po kroku](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Jak wykonać wyodrębnianie tekstu obrazu z strumienia przy użyciu Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Konwertuj obraz na tekst – Wykonaj OCR na obrazie z URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}