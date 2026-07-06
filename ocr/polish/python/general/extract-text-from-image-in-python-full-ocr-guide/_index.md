---
category: general
date: 2026-06-25
description: Wyodrębnij tekst z obrazu za pomocą OCR w Pythonie. Dowiedz się, jak
  wczytać obraz do OCR, wykonać OCR w Pythonie i przekształcić paragon do formatu
  JSON w kilku prostych krokach.
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: pl
og_description: Wyodrębnij tekst z obrazu za pomocą OCR w Pythonie. Ten samouczek
  poprowadzi Cię przez ładowanie obrazu do OCR, wykonywanie OCR w Pythonie oraz konwertowanie
  paragonu na JSON.
og_title: Wyodrębnij tekst z obrazu w Pythonie – Pełny przewodnik po OCR
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: Wyodrębnianie tekstu z obrazu w Pythonie – Kompletny przewodnik OCR
url: /pl/python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnianie tekstu z obrazu w Python – Pełny przewodnik OCR

Kiedykolwiek potrzebowałeś **wyodrębnić tekst z obrazu**, ale nie wiedziałeś, od czego zacząć? W tym samouczku przeprowadzimy Cię przez **ładowanie obrazu do OCR**, **wykonywanie OCR w Pythonie** oraz **konwersję paragonu do JSON** — wszystko przy użyciu kilku linijek kodu.

Jeśli kiedykolwiek budowałeś aplikację skanującą paragony, tracker wydatków lub po prostu chcesz zautomatyzować wprowadzanie danych, zobaczysz, dlaczego opanowanie tego przepływu to prawdziwa zmiana gry. Po zakończeniu będziesz mieć działający skrypt, który odczytuje zdjęcie paragonu i zwraca czysty ładunek JSON gotowy do dalszych usług.

## Czego się nauczysz

Omówimy każdy krok, od instalacji biblioteki `aocr` po obsługę surowego wyniku. Konkretnie dowiesz się, jak:

1. **Utworzyć instancję silnika OCR** – punkt wejścia dla całej pracy rozpoznawania.  
2. **Załadować obraz do OCR** – poinformować silnik, który plik ma odczytać.  
3. **Wybrać format eksportu** – JSON lub XML, wybierzemy JSON, ponieważ jest łatwiejszy w użyciu.  
4. **Uruchomić rozpoznawanie** – faktycznie wykonać OCR w Pythonie.  
5. **Wydrukować lub zapisać wynik** – skonwertować paragon do JSON i zobaczyć wyjście.

Nie wymagana jest wcześniejsza znajomość OCR; wystarczy podstawowa konfiguracja Pythona i plik obrazu (paragon, ulotka, cokolwiek potrzebujesz).  

---

![Diagram przedstawiający przepływ wyodrębniania tekstu z obrazu przy użyciu Python OCR](extract-text-from-image-python-ocr.png){alt="wyodrębnianie tekstu z obrazu przy użyciu Python OCR"}

## Wyodrębnianie tekstu z obrazu – krok po kroku OCR w Pythonie

Poniżej znajduje się kompletny, gotowy do uruchomienia skrypt. Skopiuj go do pliku o nazwie `receipt_ocr.py` i uruchom `python receipt_ocr.py`.

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### Dlaczego to działa

- **Instancja silnika** – `aocr.OcrEngine()` kapsułkuje wszystkie ciężkie operacje (ładowanie modelu, wstępne przetwarzanie itp.).  
- **Ładowanie obrazu** – `engine.load_image()` informuje bibliotekę, który bitmap ma analizować; możesz podać JPEG, PNG lub nawet wielostronicowe PDF‑y.  
- **Format eksportu** – ustawienie `engine.export_format` na `aocr.ExportFormat.JSON` sprawia, że wynik jest strukturalnym ciągiem znaków, idealnym dla API oczekujących JSON.  
- **Wywołanie rozpoznawania** – `engine.recognize()` uruchamia w tle inferencję sieci neuronowej; zwraca ciąg JSON zawierający wykryte bloki tekstu, oceny pewności i informacje o układzie.  

---

## Ładowanie obrazu do OCR przy użyciu aocr

Jeśli zastanawiasz się, czy obraz wymaga specjalnego wstępnego przetwarzania, krótką odpowiedzią jest **nie** — `aocr` radzi sobie z większością typowych przypadków (regulacja kontrastu, prostowanie) automatycznie. Możesz jednak zwiększyć dokładność, stosując:

- Upewnienie się, że obraz ma co najmniej 300 dpi.  
- Przycięcie nieistotnych krawędzi.  
- Konwersję do odcieni szarości przed podaniem (opcjonalnie, `engine.load_image()` zrobi to za Ciebie).

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*Pro tip:* Jeśli paragon zawiera dużo szumów, dodatkowy krok powyżej może zwiększyć **perform OCR in Python** dokładność o zauważalną wartość.

---

## Wybór formatu eksportu i konwersja paragonu do JSON

Możesz się zastanawiać: „Dlaczego nie po prostu uzyskać czysty tekst?” Ponieważ JSON zachowuje hierarchiczną strukturę (linie, słowa, ramki ograniczające). Dzięki temu znacznie łatwiej jest później mapować pola takie jak *kwota całkowita* czy *data*.

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

Gdy uruchomisz skrypt, `json_result` będzie wyglądał mniej więcej tak (skrócony dla przejrzystości):

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

Masz teraz **convert receipt to JSON** ładunek, który możesz od razu wprowadzić do bazy danych, endpointu REST lub modelu uczenia maszynowego.

---

## Uruchomienie rozpoznawania i pobranie wyników

Ostatni krok — faktyczne wykonanie OCR — jest tak prosty, jak wywołanie `recognize()`. Biblioteka w tle:

1. Przesyła obraz przez wstępnie wytrenowaną sieć konwolucyjną.  
2. Dekoduje wyjście sieci na czytelne znaki.  
3. Pakietuje wszystko w wybranym formacie (JSON w naszym przypadku).

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

Jeśli chcesz zapisać wynik zamiast go wyświetlać, po prostu zapisz go do pliku:

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*Edge case:* Niektóre paragony zawierają znaki spoza ASCII (np. „€”). Upewnij się, że otwierasz plik z kodowaniem UTF‑8, jak pokazano powyżej, aby uniknąć zniekształconego tekstu.

---

## Pełny działający przykład (wszystkie kroki w jednym skrypcie)

Łącząc wszystko razem, oto finalny skrypt, który możesz uruchomić od początku do końca:

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

Uruchom go przy pomocy:

```bash
python receipt_ocr.py
```

Powinieneś zobaczyć linię potwierdzającą oraz, w tym samym folderze, plik `receipt_output.json` zawierający ustrukturyzowane dane.

---

## Podsumowanie

Teraz wiesz, **jak wyodrębnić tekst z obrazu** przy użyciu Pythona, **jak ładować obraz do OCR**, **jak wykonać OCR w Pythonie** oraz **jak skonwertować paragon do JSON** dla dalszego przetwarzania. Ten end‑to‑end przepływ jest lekki, wymaga tylko pakietu `aocr` i może być wstawiony do dowolnego potoku automatyzacji.

Co dalej? Spróbuj zmienić format eksportu na XML, eksperymentuj z różnymi technikami wstępnego przetwarzania obrazu lub zbuduj małe API Flask, które przyjmuje przesłany paragon i natychmiast zwraca ładunek JSON. Niebo jest granicą, gdy już opanujesz podstawy.

Masz pytania lub napotkałeś problem? zostaw komentarz poniżej i powodzenia w kodowaniu!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}