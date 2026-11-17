---
category: general
date: 2026-06-22
description: Uzyskaj współrzędne prostokąta ograniczającego z obrazów przy użyciu
  Pythona. Dowiedz się, jak wyodrębnić tekst z obrazu w Pythonie za pomocą Aspose
  OCR i parsowania JSON w kilka minut.
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: pl
og_description: Uzyskaj współrzędne prostokąta ograniczającego z obrazów przy użyciu
  Pythona. Ten przewodnik pokazuje, jak wyodrębnić tekst z obrazu w Pythonie za pomocą
  Aspose OCR i przetworzyć dane układu.
og_title: Uzyskaj współrzędne prostokąta ograniczającego z OCR w Pythonie – pełny
  tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  headline: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  type: TechArticle
- description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  name: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - An active Aspose.OCR for Python
      license or a free trial (the library works without a license but adds a watermark).
      - `pip install aspose-ocr` (the package name on PyPI). - A sample image called
      `invoice.png` placed in a folder you can reference.'
  - name: 1. Convert Bounding Boxes to Simple Rectangles
    text: 'If your downstream tool expects `(x, y, width, height)` instead of eight
      points, add a helper:'
  - name: 2. Handle Multi‑Page PDFs
    text: 'Aspose OCR can accept PDF streams. Replace the image loading line with:'
  - name: 3. Visualize Bounding Boxes
    text: 'If you want to see the boxes drawn on the original image, use Pillow:'
  type: HowTo
- questions:
  - answer: For large documents, consider streaming the JSON or processing page‑by‑page
      to keep memory usage low.
    question: What if the JSON is huge?
  - answer: Low contrast or handwritten text often trips OCR engines. Pre‑process
      the image (increase contrast, binarize) before feeding it to Aspose.
    question: Why are some words missing?
  - answer: Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`
      to receive a `"characters"` array with its own `boundingBox`.
    question: Can I get character‑level coordinates?
  - answer: Absolutely. (0, 0) is the top‑left corner of the image.
    question: Is the coordinate system zero‑based?
  type: FAQPage
tags:
- OCR
- Python
- JSON
- Image Processing
title: Uzyskaj współrzędne prostokąta ograniczającego z OCR w Pythonie – Kompletny
  przewodnik
url: /pl/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pobierz współrzędne prostokąta ograniczającego z OCR w Pythonie – Kompletny przewodnik

Czy kiedykolwiek potrzebowałeś **pobrać współrzędne prostokąta ograniczającego** dla każdego słowa na zeskanowanej fakturze, ale nie wiedziałeś od czego zacząć? Nie jesteś sam. W wielu projektach automatyzacji musisz zlokalizować tekst na obrazie, aby go podświetlić, zamazać lub przekazać do dalszej analizy. Dobra wiadomość? Kilka linijek Pythona i Aspose.OCR pozwoli Ci pobrać zarówno tekst **jak i** jego dokładną pozycję w jednym przebiegu.

W tym tutorialu przeprowadzimy Cię przez praktyczny przykład, który pokaże, jak **wyodrębnić tekst z obrazu w stylu python** i następnie zagłębić się w dane układu JSON, aby wyciągnąć te prostokąty ograniczające. Bez zbędnych wstępów, tylko działający skrypt, wyjaśnienia, dlaczego każdy krok ma znaczenie, oraz wskazówki, jak uniknąć typowych pułapek.

---

## Co zbudujesz

1. Ładuje obraz (np. fakturę w formacie PNG) do Aspose OCR.  
2. Konfiguruje silnik, aby generował informacje o układzie w formacie JSON.  
3. Parsuje JSON do słownika Pythona.  
4. Iteruje po każdym rozpoznanym słowie, wypisując jego tekst **oraz** współrzędne prostokąta ograniczającego.  

Zobaczysz także, jak dostosować kod do wielostronicowych PDF‑ów, różnych formatów obrazów oraz własnych systemów współrzędnych.

### Wymagania wstępne

- Python 3.8+ zainstalowany na Twoim komputerze.  
- Aktywna licencja Aspose.OCR for Python lub darmowa wersja próbna (biblioteka działa bez licencji, ale dodaje znak wodny).  
- `pip install aspose-ocr` (nazwa pakietu w PyPI).  
- Przykładowy obraz o nazwie `invoice.png` umieszczony w folderze, do którego możesz odwołać się.  

To wszystko—bez ciężkich frameworków, bez zewnętrznych usług. Zanurzmy się.

---

## Krok 1: Zainstaluj i zaimportuj wymagane biblioteki

Najpierw upewnij się, że pakiet Aspose OCR oraz wbudowany moduł `json` są dostępne. Moduł `json` jest dostarczany z Pythonem, więc musimy jedynie zainstalować Aspose.

```bash
pip install aspose-ocr
```

Teraz zaimportuj je w swoim skrypcie:

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **Dlaczego to ważne:** Importowanie `aspose.ocr` daje dostęp do wysokowydajnego silnika OCR, natomiast `json` pozwala przekształcić surowy ciąg układu w natywny słownik Pythona, co ułatwia nawigację.

---

## Krok 2: Utwórz silnik OCR i załaduj swój obraz

Silnik jest sercem procesu. Tworzysz jego instancję, a następnie wskazujesz mu obraz, który ma zostać zeskanowany.

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **Wskazówka:** Zastąp `"YOUR_DIRECTORY/invoice.png"` ścieżką absolutną lub względną wskazującą na rzeczywisty plik. Jeśli plik nie zostanie znaleziony, Aspose zgłosi `FileNotFoundError`, więc sprawdź pisownię.

---

## Krok 3: Skonfiguruj silnik, aby zwracał dane układu w formacie JSON

Aspose OCR może zwrócić zwykły tekst, JSON tylko z OCR lub pełny JSON układu, który zawiera współrzędne słów, linii, a nawet pojedynczych znaków. Do **pobrania współrzędnych prostokąta ograniczającego** potrzebujemy JSON układu.

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **Dlaczego JSON?** JSON jest niezależny od języka, czytelny dla człowieka i łatwo mapuje się na słowniki Pythona. JSON układu zawiera tablicę `"words"`, w której każdy element przechowuje tekst oraz tablicę `boundingBox` z ośmioma liczbami (cztery punkty narożne).

---

## Krok 4: Uruchom rozpoznawanie i pobierz surowy ciąg JSON

Teraz faktycznie uruchamiamy OCR. Metoda `recognize()` zwraca obiekt `OcrResult`, z którego możemy wyodrębnić ciąg JSON.

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

Jeśli wydrukujesz `layout_json`, zobaczysz coś w rodzaju:

```json
{
  "words": [
    {
      "text": "Invoice",
      "boundingBox": [12, 34, 112, 34, 112, 58, 12, 58]
    },
    {
      "text": "#12345",
      "boundingBox": [130, 34, 210, 34, 210, 58, 130, 58]
    }
    // ... more words ...
  ]
}
```

> **Przypadek brzegowy:** Niektóre obrazy mogą generować puste tablice `"words"` jeśli silnik OCR nie wykryje żadnego tekstu. W takim przypadku sprawdź jakość obrazu (kontrast, rozdzielczość) przed kontynuacją.

---

## Krok 5: Sparsuj JSON do słownika Pythona

Praca z natywnymi strukturami Pythona jest znacznie łatwiejsza niż manipulowanie ciągami. Użyj funkcji `json.loads()`, aby przekształcić ciąg.

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

Teraz `layout_data["words"]` jest listą słowników, z których każdy reprezentuje słowo i jego prostokąt ograniczający.

---

## Krok 6: Iteruj po słowach i **pobierz współrzędne prostokąta ograniczającego**

Oto sedno naszego tutorialu: iterowanie po każdym słowie, wyodrębnianie tekstu i wypisywanie współrzędnych. To właśnie miejsce, w którym **pobieramy współrzędne prostokąta ograniczającego**.

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**Przykładowe wyjście** (Twoje liczby będą się różnić w zależności od obrazu):

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **Dlaczego format ośmiu punktów?** Cztery narożniki (górny‑lewy, górny‑prawy, dolny‑prawy, dolny‑lewy) pozwalają narysować wielokąt wokół słowa, nawet jeśli tekst jest pochyły. Jeśli potrzebujesz tylko prostego prostokąta, możesz obliczyć `x_min = min(x1, x2, x3, x4)`, `y_min = min(y1, y2, y3, y4)`, `width = max(x…) - x_min` oraz `height = max(y…) - y_min`.

---

## Opcjonalne ulepszenia

### 1. Konwertuj prostokąty ograniczające na proste prostokąty

Jeśli Twoje narzędzie downstream oczekuje `(x, y, width, height)` zamiast ośmiu punktów, dodaj pomocniczą funkcję:

```python
def box_to_rect(box):
    xs = box[0::2]  # extract x coordinates
    ys = box[1::2]  # extract y coordinates
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min, x_max - x_min, y_max - y_min)

for word in layout_data["words"]:
    rect = box_to_rect(word["boundingBox"])
    print(f"'{word['text']}' rectangle {rect}")
```

### 2. Obsługa wielostronicowych PDF‑ów

Aspose OCR może przyjmować strumienie PDF. Zastąp linię ładowania obrazu następującą:

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

Iteruj `set_page_number` dla każdej strony, zbierając współrzędne dla każdej z nich.

### 3. Wizualizacja prostokątów ograniczających

Jeśli chcesz zobaczyć prostokąty narysowane na oryginalnym obrazie, użyj Pillow:

```python
from PIL import Image, ImageDraw

img = Image.open("YOUR_DIRECTORY/invoice.png")
draw = ImageDraw.Draw(img)

for word in layout_data["words"]:
    box = word["boundingBox"]
    # Pillow expects a list of tuples [(x1,y1), (x2,y2), ...]
    polygon = [(box[i], box[i+1]) for i in range(0, len(box), 2)]
    draw.line(polygon + [polygon[0]], fill="red", width=2)

img.show()
```

Teraz zobaczysz czerwone obramowania wokół każdego rozpoznanego słowa—idealne do debugowania lub nakładek UI.

---

## Częste pytania i pułapki

- **Co zrobić, jeśli JSON jest ogromny?** Dla dużych dokumentów rozważ strumieniowanie JSON lub przetwarzanie strona po stronie, aby utrzymać niskie zużycie pamięci.  
- **Dlaczego niektóre słowa są pomijane?** Niski kontrast lub odręczny tekst często sprawiają problemy silnikom OCR. Przetwórz wstępnie obraz (zwiększ kontrast, binaryzuj) przed przekazaniem go do Aspose.  
- **Czy mogę uzyskać współrzędne na poziomie znaków?** Tak—ustaw `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`, aby otrzymać tablicę `"characters"` z własnym `boundingBox`.  
- **Czy system współrzędnych jest zerowy?** Tak. (0, 0) to lewy górny róg obrazu.

---

## Pełny skrypt – gotowy do skopiowania i uruchomienia

Poniżej znajduje się kompletny, działający przykład, który łączy wszystkie kroki. Zapisz go jako `extract_bboxes.py` i uruchom `python extract_bboxes.py`.

```python
import aspose.ocr as ocr
import json

# -------------------------
# 1️⃣ Initialize OCR engine
# -------------------------
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))

# -------------------------------------------------
# 2️⃣ Ask for JSON layout output (contains bounding boxes)
# -------------------------------------------------
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)

# -------------------------
# 3️⃣ Run recognition
# -------------------------
result = engine.recognize()
layout_json = result.get_json()

# -------------------------
# 4️⃣ Parse JSON
# -------------------------
layout_data = json.loads(layout_json)

# -------------------------
# 5️⃣ Helper to turn 8‑point box into rectangle (optional)
# -------------------------
def box_to_rect(box):
    xs = box[0::2]
    ys = box[1::2]
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}