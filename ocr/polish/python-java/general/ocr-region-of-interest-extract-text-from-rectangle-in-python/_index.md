---
category: general
date: 2026-05-31
description: Poznaj, jak używać regionu zainteresowania OCR do wczytywania obrazu
  i wyodrębniania tekstu z prostokąta, co jest idealne do rozpoznawania kwoty na fakturze.
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: pl
og_description: Opanuj obszar zainteresowania OCR, aby wczytać obraz do OCR, wyodrębnić
  tekst z prostokąta i rozpoznać tekst z faktury w jednym samouczku.
og_title: OCR – Obszar zainteresowania – Przewodnik krok po kroku w Pythonie
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR Region of Interest – Wyodrębnij tekst z prostokąta w Pythonie
url: /pl/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Region of Interest – Wyodrębnianie tekstu z prostokąta w Pythonie

Zastanawiałeś się kiedyś, jak **ocr region of interest** konkretną część zeskanowanej faktury, nie przekazując całej strony do silnika? Nie jesteś pierwszym, który patrzy na rozmazany paragon i myśli: „Jak wyodrębnić kwotę, która znajduje się gdzieś w prawym dolnym rogu?” Dobra wiadomość jest taka, że możesz powiedzieć bibliotece OCR dokładnie, gdzie ma szukać, co znacząco zwiększa zarówno szybkość, jak i dokładność.

W tym przewodniku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który pokaże, jak **load image for OCR**, zdefiniować **region of interest**, a następnie **extract text from rectangle**, aby w końcu **recognize text from invoice** i odpowiedzieć na klasyczne pytanie „jak wyodrębnić kwotę”. Bez niejasnych odniesień — tylko konkretny kod, jasne wyjaśnienia i kilka profesjonalnych wskazówek, które chciałbyś znać wcześniej.

---

## Co zbudujesz

Pod koniec tego samouczka będziesz mieć mały skrypt w Pythonie, który:

1. Wczytuje obraz faktury z dysku.  
2. Zaznacza prostokątny ROI, w którym znajduje się całkowita kwota.  
3. Uruchamia OCR tylko w obrębie tego ROI.  
4. Wyświetla oczyszczony ciąg kwoty.  

Wszystko to działa z dowolną biblioteką OCR obsługującą ROI — tutaj użyjemy fikcyjnego, ale reprezentatywnego pakietu `SimpleOCR`, który naśladuje popularne narzędzia takie jak Tesseract czy EasyOCR. Śmiało możesz go zamienić; koncepcje pozostają takie same.

## Wymagania wstępne

- Zainstalowany Python 3.8+ (`python --version` powinien wyświetlać ≥3.8).  
- Pakiet OCR instalowalny przez pip (np. `pip install simpleocr`).  
- Obraz faktury (PNG lub JPEG) umieszczony w folderze, do którego możesz odwołać się.  
- Podstawowa znajomość funkcji i klas w Pythonie (nic skomplikowanego).

Jeśli już je masz, świetnie — zanurzmy się. Jeśli nie, najpierw zdobądź obraz; pozostałe kroki są niezależne od rzeczywistej zawartości pliku.

## Krok 1: Wczytaj obraz do OCR

Pierwszą rzeczą, której potrzebuje każdy przepływ pracy OCR, jest bitmapa do odczytu. Większość bibliotek udostępnia prostą metodę `load_image`, przyjmującą ścieżkę do pliku. Oto jak to zrobić z naszym silnikiem `SimpleOCR`:

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Pro tip:** Używaj ścieżek bezwzględnych lub `os.path.join`, aby uniknąć niespodzianek „plik nie znaleziony” podczas uruchamiania skryptu z innego katalogu roboczego.

## Krok 2: Zdefiniuj OCR Region of Interest

Zamiast pozwalać silnikowi skanować całą stronę, mówimy mu *dokładnie*, gdzie znajduje się kwota. To jest krok **ocr region of interest** i jest kluczem do niezawodnego wyodrębniania, szczególnie gdy dokument zawiera zaszumione nagłówki lub stopki.

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

Dlaczego te liczby? `x` i `y` to przesunięcia w pikselach od lewego górnego rogu, natomiast `width` i `height` opisują rozmiar prostokąta. Jeśli nie jesteś pewien, otwórz obraz w dowolnym edytorze, włącz linijkę i zanotuj współrzędne. Wiele IDE pozwala nawet wyświetlić pozycję kursora podczas najechania.

## Krok 3: Wyodrębnij tekst z prostokąta

Teraz, gdy ROI jest ustawiony, prosimy silnik o **recognize text from invoice**, ale ograniczony do prostokąta, który właśnie dodaliśmy. Wywołanie zwraca obiekt wyniku, który zazwyczaj zawiera surowy ciąg znaków, oceny pewności i czasami ramki ograniczające.

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

Za kulisami, `recognize()` iteruje po każdym ROI, przycina ten fragment, uruchamia model OCR i łączy wyniki. Dlatego zdefiniowanie precyzyjnego regionu **extract text from rectangle** może zaoszczędzić sekundy czasu przetwarzania przy zadaniach wsadowych.

## Krok 4: Jak wyodrębnić kwotę – Oczyść wynik

OCR nie jest doskonały; często otrzymasz zbędne spacje, znaki nowej linii lub nawet błędnie odczytane znaki (np. „S” zamiast „5”). Szybkie `strip()` i małe wyrażenie regularne zazwyczaj rozwiązują problem dla wartości pieniężnych.

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **Dlaczego to ważne:** Jeśli planujesz wprowadzić kwotę do bazy danych lub bramki płatności, potrzebujesz przewidywalnego formatu. Usuwanie białych znaków i filtrowanie znaków nienumerycznych zapobiega błędom w dalszych etapach.

## Krok 5: Recognize Text from Invoice – Pełny skrypt

Łącząc wszystko razem, oto kompletny, gotowy do uruchomienia skrypt. Zapisz go jako `extract_amount.py` i uruchom `python extract_amount.py`.

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### Oczekiwany wynik

```
Amount: 1,245.67
```

Jeśli ROI jest źle wyrównany, możesz zobaczyć coś w stylu `Amount: 1245.6S` — zauważ zbędne „S”. Dostosuj współrzędne prostokąta i uruchom ponownie, aż wynik będzie czysty.

## Częste pułapki i przypadki brzegowe

| Problem | Dlaczego się dzieje | Rozwiązanie |
|---------|----------------------|-------------|
| **ROI za mały** | Tekst kwoty zostaje obcięty, co prowadzi do częściowego rozpoznania. | Zwiększ `width`/`height` o ~10‑20 % i przetestuj ponownie. |
| **Nieprawidłowe DPI** | Skanowanie w niskiej rozdzielczości (≤150 dpi) obniża dokładność OCR. | Przeskaluj obraz do 300 dpi przed wczytaniem lub poproś skaner o wyższą rozdzielczość. |
| **Wiele walut** | Wyrażenie regularne wybiera pierwszą grupę liczbową, która może być numerem faktury. | Udoskonal wyrażenie regularne, aby szukało symboli walut (`$`, `€`, `£`) przed cyframi. |
| **Obrócone faktury** | Silniki OCR zakładają pionowy tekst; obrócone strony psują rozpoznawanie. | Zastosuj korekcję obrotu (`ocr_engine.rotate(90)`) przed dodaniem ROI. |
| **Szum w tle** | Cienie lub pieczęcie mylą model. | Wstępnie przetwórz obraz prostym progowaniem (`cv2.threshold`) lub użyj filtru odszumiającego. |

Rozwiązywanie tych przypadków brzegowych już na początku zaoszczędzi Ci godziny debugowania później.

## Porady dla projektów w rzeczywistym świecie

- **Batch Processing:** Przetwarzaj pętlą folder z fakturami, obliczaj ROI dynamicznie (np. na podstawie wykrywania szablonu) i zapisuj wyniki w CSV.  
- **Template Matching:** Jeśli obsługujesz kilka układów faktur, utrzymuj mapę JSON `template_id → ROI coordinates`. Zmieniaj ROI w oparciu o szybki klasyfikator układu.  
- **Parallel Execution:** Użyj `concurrent.futures.ThreadPoolExecutor` do równoczesnego uruchamiania wielu instancji OCR — świetne dla wysokowolumenowych pipeline'ów back‑office.  
- **Confidence Filtering:** Większość wyników OCR zawiera ocenę pewności. Odrzuć wyniki poniżej progu (np. 85 %) i oznacz je do ręcznej weryfikacji.

## Zakończenie

Omówiliśmy wszystko, co potrzebne, aby **ocr region of interest**, **load image for OCR**, **extract text from rectangle**, a w końcu **recognize text from invoice**, aby odpowiedzieć na klasyczne pytanie **how to extract amount**. Skrypt jest zwięzły, a jednocześnie na tyle elastyczny, aby dostosować się do różnych formatów dokumentów, języków i backendów OCR.

Teraz, gdy opanowałeś podstawy, rozważ rozszerzenie przepływu: dodaj skanowanie kodów kreskowych, zintegrować z parserem PDF lub przesłać wyodrębnioną kwotę do API księgowego. Nie ma ograniczeń, a przy dobrze zdefiniowanym ROI zawsze uzyskasz szybsze i czystsze wyniki.

Jeśli napotkasz problem, zostaw komentarz poniżej — powodzenia w OCR!

![przykład regionu zainteresowania OCR](https://example.com/ocr_roi_example.png "przykład regionu zainteresowania OCR")


## Co powinieneś nauczyć się dalej?

- [Jak wyodrębnić tekst z obrazu, przygotowując prostokąty w OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Wyodrębnij tekst z obrazu w Java z Aspose.OCR Tryb wykrywania obszarów](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Wyodrębnij tekst z obrazu – optymalizacja OCR z Aspose.OCR dla .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}