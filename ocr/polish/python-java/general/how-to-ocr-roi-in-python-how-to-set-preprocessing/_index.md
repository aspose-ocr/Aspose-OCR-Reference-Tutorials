---
category: general
date: 2026-03-28
description: Jak wykonać OCR na ROI w Pythonie – Dowiedz się, jak ustawić opcje przetwarzania
  wstępnego, aby dokładnie wyodrębniać tekst z określonych obszarów obrazu.
draft: false
keywords:
- how to OCR ROI
- how to set preprocessing
- Aspose OCR Python
- ROI extraction
- image preprocessing OCR
language: pl
og_description: Jak wykonać OCR na ROI w Pythonie – Ten przewodnik pokazuje, jak ustawić
  wstępne przetwarzanie w celu niezawodnego wyodrębniania tekstu z określonych regionów
  obrazu.
og_title: Jak wykonać OCR ROI w Pythonie – Jak ustawić przetwarzanie wstępne
tags:
- OCR
- Python
- Aspose
title: Jak wykonać OCR ROI w Pythonie – Jak ustawić przetwarzanie wstępne
url: /pl/python-java/general/how-to-ocr-roi-in-python-how-to-set-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonać OCR ROI w Pythonie – Jak ustawić przetwarzanie wstępne

Zastanawiałeś się kiedyś **jak wykonać OCR ROI** na zaszumionym obrazie faktury bez wczytywania całej strony do pamięci? Nie jesteś jedyny. W wielu rzeczywistych projektach potrzebujemy tylko kilku pól — nazwy klienta, adresu, sum — więc skanowanie całego dokumentu jest przesadą.  

Dobre wieści? Dzięki Aspose OCR możesz powiedzieć silnikowi dokładnie **gdzie szukać** i nawet nakazać mu najpierw oczyścić obraz. W tym samouczku przeprowadzimy Cię przez **jak ustawić przetwarzanie wstępne**, zdefiniujemy Regiony Zainteresowania (ROIs) i wyodrębnimy czysty tekst w zaledwie kilku linijkach Pythona.

Po zakończeniu tego przewodnika będziesz mieć gotowy do uruchomienia skrypt, który wyodrębnia konkretne bloki z dowolnej faktury, paragonu lub formularza. Nie potrzebujesz dodatkowych narzędzi, tylko Aspose OCR i odrobinę logiki w Pythonie.

---

## Czego będziesz potrzebować

- **Python 3.8+** (kod działa na każdej nowszej wersji)  
- **Aspose OCR for Python via .NET** – zainstaluj przy pomocy `pip install aspose-ocr`  
- Przykładowy obraz (np. `invoice.png`) umieszczony w folderze, do którego możesz odwołać się  
- Podstawowa znajomość funkcji Pythona i składni obiektowo‑zorientowanej  

Jeśli już to masz, świetnie — przejdźmy od razu do kodu.

![How to OCR ROI diagram](ocr-roi.png "How to OCR ROI example")

*Alt text: diagram pokazujący ROI na obrazie faktury*

---

## Krok 1 – Inicjalizacja silnika OCR (Jak wykonać OCR ROI)

Zanim będziemy mogli powiedzieć silnikowi *gdzie* szukać, potrzebujemy instancji procesora OCR. Ten obiekt przechowuje całą konfigurację i wykonuje przebieg rozpoznawania.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the engine – this is the entry point for all OCR work
ocr_engine = aocr.OcrEngine()
```

*Dlaczego to ważne*: Klasa `OcrEngine` ukrywa ciężką pracę (detekcja czcionek, analiza układu itp.). Tworząc jedną instancję silnika, unikasz ponownego inicjowania zasoboch wymagających dużej mocy dla każdego obrazu, co utrzymuje wydajność na wysokim poziomie.

---

## Krok 2 – Załaduj źródłowy obraz (Jak wykonać OCR ROI)

Aspose Storage ułatwia ładowanie obrazów. Wskaż ścieżkę do pliku i otrzymasz obiekt `Image` gotowy do przetworzenia.

```python
# Replace YOUR_DIRECTORY with the actual path where invoice.png lives
source_image = storage.Image.load("YOUR_DIRECTORY/invoice.png")
```

*Wskazówka*: Jeśli pracujesz ze strumieniami (np. obrazy przesyłane przez API webowe), możesz przekazać obiekt `BytesIO` do `Image.load` zamiast ścieżki do pliku.

---

## Krok 3 – Zdefiniuj Regiony Zainteresowania (ROIs)

Teraz odpowiadamy na kluczowe pytanie **jak wykonać OCR ROI**: informujemy silnik o dokładnych prostokątach zawierających interesujące nas dane. Każdy ROI jest definiowany przez lewy górny róg (`x`, `y`) oraz rozmiar (`width`, `height`).

```python
from aspose.ocr import Roi

# Each tuple is (x, y, width, height) in pixels
regions_of_interest = [
    Roi(50, 120, 400, 60),   # Customer name block
    Roi(50, 200, 400, 80)    # Address block
]
```

*Dlaczego używać ROI?*  
- **Szybkość** – Silnik pomija nieistotne części obrazu.  
- **Dokładność** – Skupiając się na małym obszarze, szumy w innych miejscach nie mylą rozpoznawania.  
- **Elastyczność** – Możesz dodać dowolną liczbę ROI; silnik zwraca listę wyników w tej samej kolejności.

---

## Krok 4 – Jak ustawić przetwarzanie wstępne dla lepszej dokładności OCR

Obrazy prosto ze skanerów lub telefonów często cierpią na pochylenie, niski kontrast lub nierówne oświetlenie. Aspose OCR oferuje obiekt `PreprocessingOptions`, który pozwala włączyć typowe poprawki przed uruchomieniem rozpoznawania.

```python
from aspose.ocr import PreprocessingOptions

preprocessing_options = PreprocessingOptions()
preprocessing_options.deskew = True          # Auto‑rotate tilted text
preprocessing_options.binarize = True        # Convert to black‑white for clarity
preprocessing_options.contrast = 1.5         # Boost contrast (1.0 = no change)
```

*Jak to pomaga*:  
- **Deskew** usuwa pochylenie, które sprawia, że kształty znaków są niejednoznaczne.  
- **Binarize** redukuje szumy kolorów, dostarczając silnikowi OCR czysty obraz binarny.  
- **Contrast** wzmacnia słabe kreski, co jest szczególnie przydatne przy wyblakłych paragonach.

Możesz eksperymentować z tymi flagami — wyłącz jedną i zobacz, czy wynik się zmieni. To właśnie istota **jak skutecznie ustawić przetwarzanie wstępne**.

---

## Krok 5 – Wykonaj OCR tylko w zdefiniowanych ROI

Mając silnik, obraz, ROI i przetwarzanie wstępne gotowe, czas wywołać `recognize`. Metoda zwraca obiekt `OcrResult`, który zawiera kolekcję `regions` — każdy element odpowiada kolejności ROI, którą podaliśmy.

```python
ocr_result = ocr_engine.recognize(
    source_image,
    rois=regions_of_interest,
    preprocessing=preprocessing_options
)
```

*Za kulisami*: Silnik przycina każdy ROI, stosuje pipeline przetwarzania wstępnego i uruchamia model rozpoznawania na oczyszczonym fragmencie. Ponieważ przekazaliśmy listę, wynik zachowuje tę samą kolejność, co ułatwia dalsze przetwarzanie.

---

## Krok 6 – Odczytaj i użyj wyodrębnionego tekstu (Jak wykonać OCR ROI)

Na koniec, iteruj po liście `regions` i wypisz — lub zapisz — rozpoznane ciągi znaków. Obiekt `Region` udostępnia właściwość `text`, która zawiera wynik w Unicode.

```python
for idx, region in enumerate(ocr_result.regions, start=1):
    print(f"Region {idx} text:")
    print(region.text)
    print("-" * 40)
```

**Oczekiwany wynik (przykład)**:

```
Region 1 text:
John Doe
----------------------------------------
Region 2 text:
123 Maple Street
Springfield, IL 62704
----------------------------------------
```

Jeśli tekst wygląda na zniekształcony, wróć do **jak ustawić przetwarzanie wstępne**: może zwiększ `contrast` lub wyłącz `binarize` dla kolorowych logo.

---

## Typowe pułapki i porady profesjonalistów

| Problem | Dlaczego się pojawia | Naprawa (Jak ustawić przetwarzanie wstępne) |
|---------|----------------------|--------------------------------------------|
| Zniekształcony tekst pojawia się jako bełkot | `deskew` wyłączony lub obraz zbyt obrócony | Włącz `preprocessing_options.deskew = True` |
| Liczby zamieniają się w kropki lub przypadkowe znaki | Niski kontrast lub agresywna binaryzacja | Obniż `contrast` (np. `1.2`) lub ustaw `binarize = False` |
| Współrzędne ROI przesunięte o kilka pikseli | Różna DPI lub skalowanie skanera | Użyj narzędzia (np. Paint.NET) do zmierzenia dokładnych pozycji pikseli lub dodaj mały margines (`+5` pikseli) do każdego ROI |
| Pusty wynik dla regionu | ROI poza granicami obrazu | Sprawdź wymiary obrazu: `source_image.width`, `source_image.height` |

---

## Rozszerzanie rozwiązania (Jak wykonać OCR ROI w różnych scenariuszach)

- **Dynamiczne ROI**: Jeśli Twoje faktury mają zmienne układy, możesz najpierw wykonać szybkie OCR całej strony, aby znaleźć słowa kluczowe („Customer:”, „Address:”), a następnie obliczyć ROI w locie.  
- **Przetwarzanie wsadowe**: Owiń powyższe kroki w funkcję i iteruj po folderze z obrazami. Pamiętaj, aby ponownie używać tej samej instancji `ocr_engine`, aby utrzymać niskie zużycie pamięci.  
- **Eksport do JSON**: Zamiast drukować, zbuduj słownik i zapisz go przy pomocy `json.dumps`; to upraszcza integrację z dalszymi systemami (np. z systemem ERP).

```python
import json

def extract_invoice_fields(image_path):
    img = storage.Image.load(image_path)
    result = ocr_engine.recognize(
        img,
        rois=regions_of_interest,
        preprocessing=preprocessing_options
    )
    data = {f"field_{i+1}": r.text.strip() for i, r in enumerate(result.regions)}
    return data

print(json.dumps(extract_invoice_fields("invoice.png"), indent=2))
```

---

## Zakończenie

Masz teraz kompletny, gotowy do uruchomienia przykład, który pokazuje **jak wykonać OCR ROI** w Pythonie, jednocześnie opanowując **jak ustawić przetwarzanie wstępne** dla optymalnej dokładności. Ograniczając silnik do dokładnych prostokątów, które Cię interesują, i czyszcząc obraz wcześniej, uzyskasz szybsze, czystsze wyniki — idealne do automatyzacji faktur, digitalizacji formularzy lub każdego scenariusza, w którym liczy się tylko fragment strony.

Gotowy na kolejny krok? Spróbuj dostosować współrzędne ROI dla innego typu dokumentu lub eksperymentuj z dodatkowymi flagami przetwarzania wstępnego, takimi jak `sharpen` czy `noise_reduction`. Elastyczność Aspose OCR pozwala dostosować pipeline do praktycznie każdej jakości obrazu.

Jeśli napotkasz problem, sprawdź wyjście konsoli pod kątem pustych regionów i wróć do ustawień przetwarzania wstępnego. Szczęśliwego kodowania i niech Twój OCR będzie zawsze dokładny!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}