---
category: general
date: 2026-07-05
description: Wyodrębnij tekst z obrazu za pomocą OCR w Pythonie. Dowiedz się, jak
  wczytać obraz do OCR, odczytać tekst z wybranego obszaru i wyekstrahować tekst z
  faktury przy użyciu kilku linijek kodu.
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: pl
og_description: Wyodrębnij tekst z obrazu za pomocą Python OCR. Ten przewodnik pokazuje,
  jak załadować obraz do OCR, odczytać tekst z regionu i szybko wyodrębnić tekst z
  faktury.
og_title: Wyodrębnij tekst z obrazu – odczytaj tekst z obszaru przy użyciu OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Wyodrębnij tekst z obrazu – odczytaj tekst z obszaru przy użyciu OCR
url: /pl/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnianie tekstu z obrazu – Odczyt tekstu z regionu przy użyciu OCR

Czy kiedykolwiek potrzebowałeś **wyodrębnić tekst z obrazu**, ale istotna jest tylko konkretna część — na przykład całkowita kwota na fakturze? Nie jesteś jedyny. W wielu rzeczywistych projektach będziesz musiał **odczytać tekst z regionu** zamiast analizować cały obraz. Na szczęście, kilka linijek Pythona pozwala wczytać obraz do OCR, zdefiniować region zainteresowania (ROI) i wyciągnąć dokładnie te znaki, które są potrzebne.

W tym samouczku przeprowadzimy Cię przez kompletny, działający przykład, który pokazuje, jak **wczytać obraz do OCR**, ustawić ROI i w końcu **wyodrębnić tekst z faktury**. Po zakończeniu będziesz mieć gotowy fragment kodu, który działa z dowolną popularną biblioteką OCR obsługującą rozpoznawanie oparte na regionie.

---

## Czego będziesz potrzebować

- Python 3.8+ (kod działa również na 3.10)  
- Pakiet OCR udostępniający klasę `OcrEngine` (w demonstracji użyjemy fikcyjnego modułu `ocr`; zamień go na `pytesseract`, `easyocr` lub dowolną bibliotekę oferującą obsługę ROI)  
- Przykładowy obraz — np. `invoice.png` — zawierający wyraźny, drukowany tekst  
- Podstawowa znajomość funkcji i klas w Pythonie (nie wymaga wiedzy z zakresu deep learning)

Jeśli już je masz, świetnie — zanurzmy się. Jeśli nie, pobierz najnowszego Pythona ze strony python.org i zainstaluj pakiet OCR za pomocą `pip install your-ocr-lib`.

![Przykład wyodrębniania tekstu z obrazu](extract-text-from-image.png "Wyodrębnianie tekstu z obrazu – demonstracja OCR opartego na regionie")

*Powyższy obraz ilustruje region (czerwony prostokąt), który będziemy celować, aby **wyodrębnić tekst z obrazu**.*

## Krok 1: Zainstaluj i zaimportuj bibliotekę OCR

Najpierw upewnij się, że biblioteka OCR jest dostępna w Twoim środowisku. Poniższy wzorzec importu działa dla większości pakietów udostępniających wysokopoziomową klasę `OcrEngine`.

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **Porada:** Jeśli używasz `pytesseract`, musisz osobno zainstalować binarkę Tesseract i ustawić `pytesseract.pytesseract.tesseract_cmd` na jej ścieżkę.

## Krok 2: Utwórz silnik OCR i ustaw język

Utworzenie silnika jest proste, ale określenie języka znacząco zwiększa dokładność, szczególnie w fakturach zawierających liczby i angielskie słowa.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

Dlaczego to robimy? Silnik OCR używa modeli językowych do przewidywania znaków; poinformowanie go, że ma oczekiwać języka angielskiego, zmniejsza fałszywe trafienia, takie jak pomyłka „0” na „O”.

## Krok 3: Wczytaj obraz do OCR

Teraz faktycznie **wczytujemy obraz do OCR**. Większość bibliotek akceptuje ścieżkę do pliku lub obiekt obrazu Pillow. Tutaj używamy wbudowanego loadera biblioteki dla prostoty.

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

Upewnij się, że ścieżka wskazuje właściwy katalog; częstym błędem jest zapomnienie o ścieżce względnej, gdy skrypt uruchamiany jest z innego katalogu roboczego.

## Krok 4: Zdefiniuj region zainteresowania (ROI)

Definiowanie ROI jest sednem **odczytu tekstu z regionu**. Wyobraź sobie to jako narysowanie prostokąta wokół części faktury zawierającej całkowitą kwotę.

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` i `top` reprezentują współrzędne X i Y lewego górnego rogu prostokąta.  
- `width` i `height` określają rozmiar prostokąta.  
- Możesz eksperymentować z różnymi wartościami, używając przeglądarki obrazu, która wyświetla współrzędne pikseli.

> **Dlaczego ROI ma znaczenie:** Przeprowadzanie OCR na całej stronie marnuje cykle CPU i często wprowadza szumy z niepowiązanego tekstu, tabel lub grafiki. Skupiając się na regionie, uzyskasz czystsze wyniki i szybsze przetwarzanie.

## Krok 5: Wykonaj OCR na określonym regionie

Po skonfigurowaniu wszystkiego, w końcu **wyodrębniamy tekst z obrazu** — ale tylko w obrębie zdefiniowanego ROI.

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

Metoda `recognize` zwraca obiekt, który zazwyczaj zawiera surowy ciąg znaków, wyniki pewności oraz czasem ramki ograniczające dla każdego słowa. Dla naszych potrzeb potrzebny jest tylko czysty tekst.

## Krok 6: Wyświetl wyodrębniony tekst

Wydrukujmy wynik i zobaczmy, co otrzymaliśmy. Ten krok demonstruje **wyodrębnianie tekstu z faktury** w rzeczywistym scenariuszu.

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### Oczekiwany wynik

```
Text inside ROI:
Total Amount: $1,245.67
```

Jeśli Twoja faktura ma inny układ, zobaczysz dowolny tekst znajdujący się wewnątrz prostokąta — być może numer faktury, datę lub referencję zamówienia.

## Krok 7: Zawijanie wszystkiego w funkcję wielokrotnego użytku (opcjonalnie)

Aby rozwiązanie było wielokrotnego użytku w wielu fakturach, zamknij logikę w funkcję. To także ilustruje **OCR na regionie** jako ogólne narzędzie.

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

Teraz możesz wywołać funkcję z dowolną fakturą:

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

## Częste pułapki i jak ich unikać

| Problem | Dlaczego się pojawia | Rozwiązanie |
|---------|----------------------|-------------|
| **Pusty wynik** | ROI nie obejmuje faktycznie żadnego tekstu (błędne współrzędne). | Sprawdź ponownie wartości pikseli w edytorze obrazu; dodaj wizualną nakładkę debugującą. |
| **Śmieciowe znaki** | Niska rozdzielczość obrazu lub słaby kontrast. | Wstępnie przetwórz obraz: konwertuj do odcieni szarości, zastosuj progowanie (`cv2.threshold`). |
| **Nieprawidłowy język** | Silnik domyślnie używa języka bez potrzebnego zestawu znaków. | Jawnie ustaw `ocr_engine.language` na `ENGLISH` lub odpowiednią lokalizację. |
| **Opóźnienie wydajności** | Wielokrotne uruchamianie OCR na dużych obrazach. | Zmień rozmiar obrazu przed wczytaniem lub najpierw przytnij ROI i przetwarzaj tylko ten fragment. |

## Rozszerzenie przykładu: wiele ROI

Czasami faktura zawiera kilka pól, które są potrzebne — np. **wyodrębnić tekst z faktury** zarówno dla całkowitej kwoty, jak i daty faktury. Możesz iterować po liście prostokątów:

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

Ten wzorzec utrzymuje kod w czystości i ułatwia późniejsze dodawanie kolejnych regionów.

## Podsumowanie

Właśnie omówiliśmy kompletny, od‑a‑do przepływ pracy do **wyodrębniania tekstu z obrazu** przy użyciu OCR w Pythonie, koncentrując się na konkretnym regionie. **Wczytując obraz do OCR**, definiując **region zainteresowania** i wywołując silnik, możesz niezawodnie **odczytywać tekst z regionu** — idealne do pobierania sum z faktur, dat z paragonów lub dowolnych innych danych lokalnych.

Śmiało eksperymentuj

## Co powinieneś nauczyć się dalej?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}