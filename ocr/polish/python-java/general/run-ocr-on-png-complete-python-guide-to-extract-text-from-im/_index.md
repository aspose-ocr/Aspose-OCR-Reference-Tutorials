---
category: general
date: 2026-01-12
description: Szybko uruchom OCR na plikach PNG przy użyciu Pythona. Dowiedz się, jak
  wyodrębnić tekst z obrazu i faktury oraz jak wczytać obraz do OCR przy użyciu Aspose.OCR.
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: pl
og_description: Wykonaj OCR na PNG natychmiast. Ten przewodnik pokazuje, jak wyodrębnić
  tekst z obrazu i faktury, załadować obraz do OCR oraz zapisać wyniki jako JSON i
  CSV.
og_title: Uruchom OCR na PNG – Pełny samouczek Pythona
tags:
- OCR
- Python
- Image Processing
title: Uruchom OCR na PNG – Kompletny przewodnik Pythona po wyodrębnianiu tekstu z
  obrazów
url: /pl/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uruchamianie OCR na PNG – Kompletny przewodnik Pythona do wyodrębniania tekstu z obrazów

Czy kiedykolwiek musiałeś **uruchomić OCR na plikach PNG**, ale nie wiedziałeś, która biblioteka da czyste, ustrukturyzowane wyniki? Nie jesteś sam. W wielu rzeczywistych projektach — pomyśl o automatyzacji faktur czy skanowaniu paragonów — pierwszym krokiem jest **wyodrębnienie tekstu z pliku obrazu**, a PNG jest powszechnym formatem, ponieważ zachowuje jakość bezstratną.

W tym tutorialu przeprowadzimy praktyczny przykład przy użyciu pakietu Aspose.OCR dla Pythona. Po zakończeniu przewodnika będziesz wiedział, jak **załadować obraz do OCR**, pobrać każdą linię tekstu, przekształcić te dane w schludny obiekt JSON oraz nawet wyeksportować je do CSV do dalszego przetwarzania. Bez zbędnych wstępów, tylko praktyczne, gotowe do uruchomienia rozwiązanie.

## Czego się nauczysz

- Jak zainstalować i zaimportować bibliotekę Aspose.OCR.  
- Dokładne kroki, aby **uruchomić OCR na PNG** i obsłużyć obiekt wyniku.  
- Sposoby **wyodrębniania tekstu z faktury** i formatowania wyjścia jako JSON lub CSV.  
- Porady dotyczące radzenia sobie z obrazami o niskim kontraście, dokumentami wielojęzycznymi oraz wskaźnikami pewności.  
- Pełny, gotowy do skopiowania i wklejenia kod, który możesz uruchomić już dziś.

> **Wymagania wstępne:** Python 3.8+ oraz podstawowa znajomość pip. Jeśli nigdy nie używałeś Aspose, nie martw się — ten przewodnik obejmuje wszystko, co potrzebne, aby rozpocząć.

---

## Krok 1 – Instalacja Aspose.OCR i przygotowanie środowiska

Zanim będziemy mogli **uruchomić OCR na PNG**, biblioteka musi być zainstalowana w Twoim systemie.

```bash
pip install aspose-ocr
```

> **Pro tip:** Użyj wirtualnego środowiska (`python -m venv venv`), aby utrzymać zależności w izolacji. Zapobiega to konfliktom wersji, gdy pracujesz nad wieloma projektami jednocześnie.

Po instalacji zaimportuj potrzebne moduły:

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

Tutaj wprowadzamy `asposeocr` do ciężkiej pracy oraz wbudowaną bibliotekę `json` do późniejszej serializacji.

---

## Krok 2 – Utworzenie silnika OCR i ustawienie języka

Silnik OCR to podstawowy komponent, który faktycznie odczytuje piksele. Dla większości angielskich faktur będziesz potrzebował pakietu językowego English:

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Dlaczego to ważne:** Określenie języka zawęża zestaw znaków, co zwiększa dokładność i przyspiesza przetwarzanie. Jeśli kiedykolwiek będziesz musiał obsługiwać wielojęzyczne faktury, po prostu zamień `ocr.Language.ENGLISH` na odpowiedni enum.

---

## Krok 3 – Załadowanie obrazu do OCR

Teraz **załadujemy obraz do OCR**. Metoda `Image.load` przyjmuje ścieżkę do pliku i działa z PNG, JPEG, BMP i innymi formatami.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **Edge case:** Jeśli PNG jest wyjątkowo duży (powyżej 5 MB), rozważ najpierw zmianę rozmiaru, aby utrzymać zużycie pamięci w rozsądnych granicach. Pillow może to zrobić w jednej linii:

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

---

## Krok 4 – Uruchomienie OCR na PNG i przechwycenie wyniku

Gdy silnik jest gotowy, a obraz załadowany, czas **uruchomić OCR na PNG** i pobrać ustrukturyzowany wynik.

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

Obiekt `ocr_result` zawiera kolekcję elementów `OcrRegion`, z których każdy posiada rozpoznany tekst oraz wskaźnik pewności (0‑100). To właśnie tutaj uzyskasz szczegółowe dane potrzebne do **wyodrębniania tekstu z faktury**.

---

## Krok 5 – Konwersja wyniku do JSON i ładne wyświetlenie

Większość systemów downstream uwielbia JSON, więc przekształcimy wynik OCR w ładnie sformatowany ciąg znaków.

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### Przykładowe wyjście

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

Zauważ, że każda linia zawiera metrykę pewności — idealną do odfiltrowania wpisów o niskiej pewności, jeśli planujesz **wyodrębniać tekst z faktury** automatycznie.

---

## Krok 6 – Zapis danych OCR jako CSV (Jedna linia na tekst + pewność)

CSV jest idealny do arkuszy kalkulacyjnych lub szybkiego importu danych. Aspose oferuje jednowierszowy kod, który zapisuje wszystko do pliku CSV.

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

Wygenerowany plik CSV będzie wyglądał tak:

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

Teraz możesz otworzyć go w Excelu, Google Sheets lub wprowadzić do bazy danych.

---

## Bonus – Obsługa tekstu o niskiej pewności i dokumentów wielostronicowych PDF

### Filtrowanie według pewności

Jeśli chcesz tylko linie o wysokiej pewności, odfiltruj JSON przed zapisem:

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### Dokumenty wielostronicowe

Aspose.OCR automatycznie tworzy nowy wpis `page` dla każdej strony w wielostronicowym PNG lub PDF. Przejdź przez `ocr_data["pages"]`, aby przetworzyć je wszystkie — bez dodatkowego kodu.

---

## Pełny działający przykład

Poniżej znajduje się **kompletny skrypt**, który możesz skopiować, wkleić i uruchomić od razu. Zamień `YOUR_DIRECTORY` na folder, w którym znajduje się Twój plik PNG.

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

Uruchom skrypt poleceniem `python run_ocr.py`, a zobaczysz wyświetlenie JSON w konsoli, plik CSV na dysku oraz przefiltrowaną listę wpisów o wysokiej pewności.

---

## Najczęściej zadawane pytania

**P: Czy mogę użyć tego do wyodrębniania tekstu ze zeskanowanego paragonu zamiast faktury?**  
O: Oczywiście. Ten sam przepływ pracy działa — po prostu wskaż `image_path` na swój plik PNG z paragonem. Jeśli paragon jest w innym języku, zmień odpowiednio `engine.language`.

**P: Co jeśli mój PNG zawiera obrócony tekst?**  
O: Aspose.OCR automatycznie wykrywa orientację, ale w trudniejszych przypadkach możesz ręcznie obrócić obraz przy pomocy Pillow przed przekazaniem go do silnika.

**P: Czy potrzebna jest płatna licencja na Aspose.OCR?**  
O: Biblioteka oferuje darmowy tryb ewaluacyjny z watermarkiem na wyniku. Do użytku produkcyjnego potrzebna jest licencja, którą możesz uzyskać na stronie Aspose.

---

## Zakończenie

Omówiliśmy wszystko, co potrzebne, aby **uruchomić OCR na PNG** przy użyciu Pythona: instalację SDK, ładowanie obrazu, wyodrębnianie ustrukturyzowanego tekstu oraz zapisywanie wyniku jako JSON lub CSV. Niezależnie od tego, czy chcesz **wyodrębnić tekst z obrazu** w prostym skrypcie, czy **wyodrębnić tekst z faktury** w zautomatyzowanym potoku księgowym, powyższe kroki dają solidną, gotową do produkcji bazę.

Następnie możesz rozważyć:

- Integrację wyjścia CSV z bazą danych w celu masowego przechowywania faktur.  
- Dodanie post‑processingu przy użyciu wyrażeń regularnych, aby wyciągać daty, kwoty lub NIPy.  
- Skorzystanie z funkcji `ocr_engine.recognize_barcode`, jeśli Twoje faktury zawierają kody QR.

Spróbuj, dostosuj progi pewności i zobacz, jak Twój przepływ przetwarzania dokumentów staje się prosty jak bułka z masłem. Masz więcej pytań lub ciekawy przypadek użycia? zostaw komentarz poniżej — powodzenia w OCR!  

![przykład uruchamiania OCR na PNG](run-ocr-on-png.png "uruchamianie OCR na PNG – wizualny przykład wyniku OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}