---
category: general
date: 2026-06-25
description: Przetwórz obraz do OCR i rozpoznaj tekst ze zeskanowanego dokumentu przy
  użyciu Pythona. Samouczek krok po kroku z pełnym kodem.
draft: false
keywords:
- preprocess image for OCR
- recognize text from scanned document
- Python OCR tutorial
- image deskewing Python
- OCR preprocessing tips
language: pl
og_description: Przetwórz obraz do OCR i rozpoznaj tekst ze zeskanowanego dokumentu
  przy użyciu Pythona. Skorzystaj z tego szczegółowego, gotowego do uruchomienia samouczka.
og_title: Przetwarzanie obrazu pod OCR w Pythonie – Kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  headline: Preprocess Image for OCR in Python – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  name: Preprocess Image for OCR in Python – Complete Guide
  steps:
  - name: Create an OCR Engine Instance
    text: '```python import ocr # <-- make sure the OCR library is installed'
  - name: Enable Automatic Deskewing and Binarization
    text: '```python # Step 2: Enable automatic deskewing and binarization to improve
      recognition engine.image_preprocessing = ocr.ImagePreProcessingOptions( auto_deskew=True,
      auto_binarize=True ) ```'
  - name: Load the Skewed Image You Want to Process
    text: '```python # Step 3: Load the skewed image you want to process image_path
      = "YOUR_DIRECTORY/skewed_document.jpg" image = ocr.Image.load(image_path) ```'
  - name: Perform OCR on the Pre‑processed Image
    text: '```python # Step 4: Perform OCR on the pre‑processed image result = engine.recognize(image)
      ```'
  - name: Output the Recognized Text
    text: '```python # Step 5: Output the recognized text print("Deskewed & binarized
      text:", result.text) ```'
  - name: 1. Handling Multiple Languages
    text: 'If your document contains both English and French, configure the engine
      before step 1:'
  - name: 2. Fine‑Tuning Binarization Thresholds
    text: 'Automatic binarization works for most cases, but some old photocopies need
      a custom threshold:'
  - name: 3. Extracting Layout Information
    text: 'Sometimes you need more than raw text—you want to know where each paragraph
      lives on the page. Many engines expose a `result.blocks` collection:'
  - name: 4. Processing a Batch of Files
    text: 'If you have a folder full of scanned PDFs converted to JPEGs, wrap the
      whole flow in a loop:'
  - name: 5. Dealing with Low‑Resolution Scans
    text: 'Low‑resolution images (< 150 dpi) often produce fuzzy characters. A quick
      remedy is to upscale using a high‑quality algorithm before feeding the image
      to the OCR engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Przetwarzanie obrazu pod OCR w Pythonie – Kompletny przewodnik
url: /pl/python-java/general/preprocess-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Przetwarzanie obrazu pod OCR w Pythonie – Kompletny przewodnik

Zastanawiałeś się kiedyś, jak **preprocess image for OCR**, aby tekst był czysty i wiarygodny? Nie jesteś sam — większość programistów napotyka ten sam problem, gdy zeskanowana strona jest krzywa lub kontrast jest niejednolity. Dobrą wiadomością jest to, że kilka linijek Pythona może wyprostować ten bałagan, binarizować obraz i zwrócić wyraźny, przeszukiwalny tekst.

W tym tutorialu przeprowadzimy Cię przez dokładne kroki, aby **preprocess image for OCR** *oraz* **recognize text from scanned document** plików, używając popularnej biblioteki OCR. Po zakończeniu będziesz mieć gotowy do uruchomienia skrypt, zrozumiesz, dlaczego każde ustawienie ma znaczenie, i będziesz wiedział, jak dostosować je do trudnych przypadków.

## Co będziesz potrzebować

- Python 3.8 lub nowszy (kod działa również na 3.10+)
- Pakiet OCR udostępniający klasy `OcrEngine`, `ImagePreProcessingOptions` i `Image` (np. fikcyjny moduł `ocr` użyty w przykładzie)
- Zeskanowany lub sfotografowany dokument, który jest nieco przechylony lub ma niski kontrast
- Ulubione IDE lub prosty terminal — bez ciężkiego interfejsu graficznego

To wszystko. Bez dodatkowych binarek, bez akrobacji z Dockerem. Zanurzmy się.

## Przetwarzanie obrazu pod OCR – Krok po kroku

Poniżej znajduje się podstawowy przepływ podzielony na pięć wyraźnych etapów. Każdy etap zawiera **dlaczego** to robimy, dokładny **kod** oraz krótkie **wyjaśnienie**, co dzieje się pod maską.

### Krok 1: Utwórz instancję silnika OCR

```python
import ocr  # <-- make sure the OCR library is installed

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Dlaczego to ważne:*  
Obiekt `OcrEngine` jest mózgiem operacji. Przechowuje konfigurację taką jak pakiety językowe, progi pewności i — co najważniejsze dla nas — flagi przetwarzania obrazu. Utworzenie go najpierw daje nam czystą kartę do włączenia kolejnych trików.

### Krok 2: Włącz automatyczne prostowanie i binaryzację

```python
# Step 2: Enable automatic deskewing and binarization to improve recognition
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
```

*Dlaczego to ważne:*  
- **Deskewing** (prostowanie) obraca obraz tak, aby linie tekstu stały się poziome. Silniki OCR mają trudności, gdy linia bazowa nachyla się o więcej niż kilka stopni.  
- **Binarization** (binarizacja) przekształca obraz w czystą czarno‑białą wersję, usuwając szumy tła, które mogą mylić klasyfikatory znaków.  
Obie opcje są *automatyczne* w wielu nowoczesnych bibliotekach, ale nadal trzeba je włączyć — stąd wyraźne przypisanie.

> **Wskazówka:** Jeśli Twoje obrazy źródłowe są już idealnie wyrównane, możesz ustawić `auto_deskew=False`, aby zaoszczędzić milisekundę czasu przetwarzania.

### Krok 3: Załaduj przechylony obraz, który chcesz przetworzyć

```python
# Step 3: Load the skewed image you want to process
image_path = "YOUR_DIRECTORY/skewed_document.jpg"
image = ocr.Image.load(image_path)
```

*Dlaczego to ważne:*  
Metoda `Image.load` odczytuje plik do pamięci i opakowuje go w obiekt, który rozumie silnik OCR. Wyciąga także metadane takie jak DPI, które mogą wpływać na domyślny współczynnik skalowania przy prostowaniu.

> **Przypadek brzegowy:** Jeśli obraz jest wielostronicowym TIFF, będziesz musiał iterować po każdej stronie lub użyć pomocnika takiego jak `ocr.MultiPageImage.load`. Te same ustawienia przetwarzania obrazu mają zastosowanie do każdej strony.

### Krok 4: Wykonaj OCR na przetworzonym obrazie

```python
# Step 4: Perform OCR on the pre‑processed image
result = engine.recognize(image)
```

*Dlaczego to ważne:*  
W tym momencie silnik stosuje kroki prostowania i binaryzacji, które włączyliśmy wcześniej, a następnie uruchamia swoją sieć neuronową (lub klasyczny pipeline w stylu Tesseract) na oczyszczonym bitmapie. Zwrócony obiekt `result` zazwyczaj zawiera czysty tekst, wyniki pewności oraz czasami dane pozycyjne dla każdego słowa.

> **Co zrobić, jeśli tekst jest nadal zniekształcony?**  
Sprawdź rozdzielczość obrazu: OCR działa najlepiej przy 300 dpi lub wyższym. Jeśli źródło ma niższą rozdzielczość, rozważ zwiększenie rozmiaru przed załadowaniem lub poproś o oryginalny skan od źródła dokumentu.

### Krok 5: Wyświetl rozpoznany tekst

```python
# Step 5: Output the recognized text
print("Deskewed & binarized text:", result.text)
```

*Dlaczego to ważne:*  
`result.text` jest zwykłym ciągiem znaków reprezentującym wszystko, co silnik mógł odczytać. Wydrukowanie go jest przydatne do szybkiego debugowania; w prawdziwej aplikacji prawdopodobnie zapisałbyś go do pliku `.txt`, bazy danych lub przekazał do kolejnego potoku NLP.

---

## Rozpoznawanie tekstu ze zeskanowanego dokumentu – wykraczając poza podstawy

Teraz, gdy podstawowy potok działa, przyjrzyjmy się kilku typowym wariacjom, które możesz napotkać, próbując **recognize text from scanned document** obrazów w praktyce.

### 1. Obsługa wielu języków

Jeśli Twój dokument zawiera zarówno angielski, jak i francuski, skonfiguruj silnik przed krokiem 1:

```python
engine = ocr.OcrEngine(languages=["eng", "fra"])
```

Większość silników OCR akceptuje kody ISO‑639‑2; załadowanie dodatkowych pakietów językowych wprowadza niewielkie obciążenie, ale znacząco poprawia dokładność na stronach wielojęzycznych.

### 2. Dostosowywanie progów binaryzacji

Automatyczna binaryzacja działa w większości przypadków, ale niektóre stare fotokopie wymagają niestandardowego progu:

```python
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=False,          # turn off auto
    binarization_threshold=180   # manual threshold (0‑255)
)
```

Eksperymentuj z wartościami od 120 do 220, aż tło zniknie, nie usuwając słabych znaków.

### 3. Ekstrahowanie informacji o układzie

Czasami potrzebujesz więcej niż surowy tekst — chcesz wiedzieć, gdzie każdy akapit znajduje się na stronie. Wiele silników udostępnia kolekcję `result.blocks`:

```python
for block in result.blocks:
    print(f"Block at ({block.x}, {block.y}) size {block.width}x{block.height}")
    print(block.text)
```

### 4. Przetwarzanie wsadu plików

Jeśli masz folder pełen zeskanowanych PDF‑ów przekonwertowanych na JPEGy, otocz cały przepływ pętlą:

```python
import pathlib

folder = pathlib.Path("YOUR_DIRECTORY")
for img_file in folder.glob("*.jpg"):
    img = ocr.Image.load(str(img_file))
    txt = engine.recognize(img).text
    (folder / f"{img_file.stem}.txt").write_text(txt, encoding="utf-8")
    print(f"Processed {img_file.name}")
```

Pętla ponownie używa tej samej instancji `engine`, co jest bardziej wydajne niż tworzenie jej od nowa dla każdego pliku.

### 5. Radzenie sobie z niską rozdzielczością skanów

Obrazy o niskiej rozdzielczości (< 150 dpi) często generują rozmyte znaki. Szybkim rozwiązaniem jest zwiększenie rozmiaru przy użyciu wysokiej jakości algorytmu przed przekazaniem obrazu do silnika OCR:

```python
from PIL import Image as PilImage

pil_img = PilImage.open("low_res.jpg")
upscaled = pil_img.resize((pil_img.width * 2, pil_img.height * 2), PilImage.LANCZOS)
upscaled.save("upscaled.jpg")
image = ocr.Image.load("upscaled.jpg")
```

Zwiększanie rozmiaru nie stworzy magicznie szczegółów, ale krok binaryzacji może działać na ostrzejszych krawędziach, dając niewielki przyrost.

## Oczekiwany wynik

Uruchomienie oryginalnego pięcioetapowego skryptu na umiarkowanie przechylonym skanie 300 dpi powinno wydrukować coś w rodzaju:

```
Deskewed & binarized text: 
Dear Customer,

Thank you for your recent purchase. Please find your receipt attached.

Best regards,
Acme Corp.
```

Jeśli zobaczysz zniekształcone znaki, sprawdź ponownie flagi przetwarzania, rozdzielczość obrazu i konfigurację języka.

## Podsumowanie

Omówiliśmy wszystko, co potrzebne do **preprocess image for OCR** i **recognize text from scanned document** przy użyciu Pythona. Zaczynając od nowej instancji silnika, włączyliśmy automatyczne prostowanie i binaryzację, załadowaliśmy przechylony obraz, przeprowadziliśmy rozpoznanie i wydrukowaliśmy czysty tekst. Po drodze zbadaliśmy wsparcie wielojęzyczne, ręczne dostrajanie progów, ekstrakcję układu, przetwarzanie wsadowe oraz obejścia dla niskiej rozdzielczości.

Wypróbuj skrypt na własnych skanach — może to być stos paragonów, ręcznie wypełniony formularz lub stara wycinka gazety. Gdy poczujesz się pewnie, spróbuj dodać generowanie PDF‑ów lub przekazać wynik do indeksu wyszukiwania. Nie ma ograniczeń.

**Gotowy na kolejne wyzwanie?** Sprawdź nasze tutoriale o *„Extract Tables from Scanned PDFs with Python”* oraz *„Train Custom OCR Models with TensorFlow”*, aby dalej rozwijać swoją skrzynkę narzędziową do automatyzacji dokumentów.

Szczęśliwego kodowania i niech Twój OCR zawsze będzie wyraźny!

## Co powinieneś się nauczyć dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}