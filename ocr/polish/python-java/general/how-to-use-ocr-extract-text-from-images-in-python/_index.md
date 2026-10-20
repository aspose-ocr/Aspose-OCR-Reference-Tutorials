---
category: general
date: 2026-03-18
description: Jak używać OCR do wyodrębniania tekstu z obrazów – szybki przewodnik
  po rozpoznawaniu tekstu z plików PNG i wczytywaniu obrazów do OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: pl
og_description: Jak używać OCR do wyodrębniania tekstu z obrazów – dowiedz się, jak
  rozpoznawać tekst z plików PNG, wczytywać obraz do OCR i wyodrębniać tekst za pomocą
  prostego skryptu w Pythonie.
og_title: 'Jak używać OCR: wyodrębniaj tekst z obrazów w Pythonie'
tags:
- OCR
- Python
- Image Processing
title: 'Jak używać OCR: wyodrębnianie tekstu z obrazów w Pythonie'
url: /pl/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać OCR: Wyodrębniaj tekst z obrazów w Pythonie

Zastanawiałeś się kiedyś **jak używać OCR**, gdy masz niechlujny zrzut ekranu lub zeskanowany paragon? Nie jesteś sam — programiści nieustannie muszą wyciągać czytelny tekst ze zdjęć, szczególnie z plików PNG pochodzących z aplikacji mobilnych lub przesyłanych przez internet. W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który pokaże, jak **wyodrębnić tekst z obrazu**, **rozpoznać tekst z PNG** oraz **wczytać obraz do OCR** przy użyciu kilku linijek Pythona.

Omówimy wszystko, od instalacji odpowiedniej biblioteki po obsługę dokumentów wielojęzycznych, więc pod koniec będziesz dokładnie wiedział, *jak wyodrębnić tekst* z dowolnego obrazu, który podasz silnikowi. Bez niejasnych odniesień, tylko jasne, krok‑po‑kroku rozwiązanie, które możesz skopiować, wkleić i uruchomić.

## Czego się nauczysz

W kolejnych sekcjach:

1. Skonfigurujemy lekki silnik OCR (bez ciężkich zależności).  
2. Wczytamy plik obrazu — konkretnie PNG — do silnika.  
3. Włączymy automatyczne wykrywanie języka, aby silnik radził sobie z treściami wielojęzycznymi.  
4. Uruchomimy proces rozpoznawania i pobierzemy wynik w postaci czystego tekstu.  
5. Dostosujemy przepływ pracy do przypadków brzegowych, takich jak brakujące pliki lub nieobsługiwane formaty.

Jeśli znasz podstawy Pythona, jesteś gotowy. Nie wymaga się wcześniejszego doświadczenia z OCR, choć szybkie spojrzenie w dokumentację biblioteki nigdy nie zaszkodzi.

---

![How to use OCR on a PNG image](placeholder.png "How to use OCR on a PNG image – step-by-step guide")

## Jak używać OCR – wczytaj obraz i rozpoznaj tekst {#how-to-use-ocr}

### Krok 1: Zainstaluj bibliotekę OCR

Na początek potrzebujesz pakietu Pythona, który udostępnia klasę `OcrEngine`. Dla potrzeb tego samouczka użyjemy fikcyjnej, ale obrazującej biblioteki **SimpleOCR**, którą możesz zainstalować za pomocą pip:

```bash
pip install simple-ocr
```

> **Pro tip:** Jeśli pracujesz w wirtualnym środowisku (bardzo zalecane), aktywuj je przed uruchomieniem polecenia instalacji. Dzięki temu zależności projektu pozostaną uporządkowane.

### Krok 2: Zaimportuj silnik i utwórz instancję

Utworzenie silnika jest tak proste, jak wywołanie jego konstruktora. Traktuj silnik jako „mózg”, który później przetworzy podany mu obraz.

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

Dlaczego tworzymy nową instancję za każdym razem? Izolacja. Świeży silnik gwarantuje, że żadne pozostałe stany z poprzedniego uruchomienia nie zakłócą bieżącego rozpoznawania, co jest kluczowe przy przetwarzaniu wielu plików w partii.

### Krok 3: Wczytaj obraz, który chcesz przetworzyć

Teraz faktycznie **wczytujemy obraz do OCR**. Metoda `setImageFromFile` przyjmuje ścieżkę do dowolnego obrazu rastrowego; wskażemy na PNG o nazwie `mixed_doc.png`.

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

Jeśli plik nie zostanie znaleziony, `SimpleOCR` zgłosi czytelny `FileNotFoundError`. Możesz go przechwycić, aby wyświetlić przyjazny komunikat o błędzie:

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### Krok 4: Włącz automatyczne wykrywanie języka

Większość nowoczesnych silników OCR dostarcza pakiety językowe. Przekazując `"multilingual"` informujemy silnik, aby samodzielnie wykrył tekst i automatycznie wybrał odpowiedni model językowy. Jest to szczególnie przydatne, gdy Twój PNG zawiera mieszankę angielskiego i hiszpańskiego, na przykład.

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

Jeśli znasz język z góry, możesz zamienić `"multilingual"` na konkretny kod, taki jak `"eng"` lub `"spa"`, aby przyspieszyć przetwarzanie.

### Krok 5: Uruchom proces rozpoznawania

Tutaj odbywa się najcięższa praca. `recognize()` skanuje obraz, stosuje segmentację, uruchamia sieć neuronową i wewnętrznie buduje bufor tekstowy.

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

Za kulisami silnik wykonuje:

- **Pre‑processing** (prostowanie, binaryzacja)  
- **Analizę układu** (wykrywanie kolumn, tabel)  
- **Klasyfikację znaków** (przy użyciu modelu deep‑learningowego)  

Wszystko to jest ukryte, dlatego potrzebujesz tylko jednej linijki.

### Krok 6: Pobierz i wyświetl rozpoznany tekst

Na koniec pobieramy obiekt wyniku i wyciągamy czysty ciąg znaków. To właśnie moment, w którym **wyodrębniasz tekst z obrazu**.

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**Oczekiwany wynik** (skrócony dla przejrzystości):

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

Jeśli obraz nie zawiera rozpoznawalnych znaków, `text` będzie pustym ciągiem. Możesz to obsłużyć w następujący sposób:

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

---

## Wyodrębnianie tekstu z obrazu – obsługa typowych przypadków brzegowych

### Wiele języków w jednym pliku

Gdy dokument miesza języki, ustawienie `"multilingual"` zazwyczaj radzi sobie dobrze. Jednak jeśli zauważysz błędne rozpoznania, możesz ręcznie określić listę zapasową:

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### Format nie‑PNG

Mimo że skupiamy się na **rozpoznawaniu tekstu z PNG**, `SimpleOCR` akceptuje także JPEG, BMP i TIFF. Wystarczy zmienić rozszerzenie pliku w `setImageFromFile`. W przypadku stosów TIFF możesz potrzebować wybrać konkretną stronę:

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### Duże pliki i zużycie pamięci

Jeśli przetwarzasz skany o rozdzielczości w gigapikselach, rozważ zmianę rozmiaru przed OCR:

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

Zmniejszenie rozmiaru redukuje obciążenie pamięci, zachowując jednocześnie wystarczającą szczegółowość dla dokładnego rozpoznania.

### Debugowanie nieudanych wczytań

Czasami obraz wygląda w porządku, ale jest uszkodzony wewnętrznie. Włącz szczegółowe logowanie, aby zobaczyć, co silnik „widzi”:

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

---

## Kompletny, gotowy do uruchomienia skrypt

Poniżej znajduje się pełny program, który łączy wszystkie elementy. Skopiuj go do pliku o nazwie `ocr_demo.py`, dostosuj placeholder `YOUR_DIRECTORY` i uruchom `python ocr_demo.py`.

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

Uruchomienie tego skryptu powinno wypisać wersję tekstową tego, co znajduje się w `mixed_doc.png`. Śmiało zamień plik na dowolny inny obraz — **jak wyodrębnić tekst** działa tak samo.

---

## Zakończenie

Właśnie przeszliśmy przez **jak używać OCR** w Pythonie, aby **wyodrębnić tekst z plików obrazów**, ze szczególnym uwzględnieniem **rozpoznawania tekstu z PNG** oraz praktycznych kroków, aby **wczytać obraz do OCR**. Powyższy fragment to samodzielne rozwiązanie: zainstaluj pakiet, podaj plik, włącz wykrywanie wielojęzyczne, uruchom silnik i pobierz wynik.

Od tego momentu możesz:

- Zintegrować skrypt z usługą webową przyjmującą przesyłane przez użytkowników pliki.  
- Przetwarzać wsadowo folder PDF‑ów przekonwertowanych na PNG.  
- Dodać post‑processing (np. czyszczenie regexem, sprawdzanie pisowni), aby zwiększyć dokładność.

Pamiętaj, że jakość OCR zależy od przejrzystości obrazu, odpowiednich pakietów językowych i czasem od dodatkowego wstępnego przetwarzania — więc eksperymentuj

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}