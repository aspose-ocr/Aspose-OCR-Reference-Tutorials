---
category: general
date: 2026-06-06
description: OCR obrazu PNG w Pythonie – dowiedz się, jak wyodrębnić tekst z obrazu,
  uruchomić przykład OCR w Pythonie i nawet łatwo odczytać starogrecki tekst.
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: pl
og_description: OCR obrazu PNG w Pythonie wyjaśnione. Ten przewodnik pokazuje, jak
  wyodrębnić tekst z obrazu, uruchomić przykład OCR w Pythonie i z łatwością czytać
  starogrecki.
og_title: OCR obrazu PNG w Pythonie – Kompletny poradnik
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR obrazu PNG w Pythonie – Kompletny przewodnik krok po kroku
url: /pl/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR obrazu PNG w Pythonie – Pełny przewodnik krok po kroku

Zastanawiałeś się kiedyś, jak **OCR PNG image** pliki bezpośrednio z poziomu skryptu Pythona? Być może masz folder pełen zeskanowanych starożytnych rękopisów i potrzebujesz **extract text from image** plików bez ręcznego przepisywania wszystkiego. Dobra wiadomość: nie potrzebujesz doktoratu z widzenia komputerowego — wystarczy kilka linijek kodu i odpowiednia biblioteka, a w kilka sekund będziesz czytać starogrecki.

W tym samouczku przeprowadzimy **python OCR example**, które rozpoznaje tekst z PNG, ustawia język na grecki politoniczny i wypisuje wynik. Po zakończeniu dokładnie będziesz wiedział, jak **recognize image text**, radzić sobie z typowymi pułapkami i dostosować skrypt do innych języków lub formatów obrazów.

## Czego się nauczysz

- Zainstalować i skonfigurować bibliotekę OCR dla Pythona (pytesseract + Tesseract OCR)
- Utworzyć instancję silnika OCR i wczytać plik PNG
- Ustawić język rozpoznawania na grecki politoniczny, aby móc **read ancient greek**
- Wyświetlić rozpoznany tekst i rozwiązać typowe problemy
- Rozszerzyć skrypt o przetwarzanie wsadowe wielu plików PNG lub przełączenie na inny język

### Wymagania wstępne

| Wymaganie | Dlaczego jest ważne |
|-------------|----------------|
| Python 3.8+ | Nowa składnia i wskazówki typów |
| `pytesseract` package | Cienka nakładka na silnik Tesseract |
| Tesseract OCR binaries (≥ 5.0) | Rzeczywisty silnik, który wykonuje ciężką pracę |
| Greek language data (`grc.traineddata`) | Wymagane do poprawnego **read ancient greek** |
| A PNG image you want to analyse (e.g., `ancient_greek.png`) | Nasz cel dla demonstracji **ocr png image** |

Możesz zainstalować część Pythona za pomocą:

```bash
pip install pytesseract Pillow
```

A na Ubuntu/macOS dodałbyś sam silnik:

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

Nie zapomnij pobrać danych treningowych greckiego politonicznego:

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*(Ścieżka może się różnić; w razie potrzeby dostosuj `TESSDATA_PREFIX`.)*

---

## OCR PNG Image: Utwórz instancję silnika

Pierwszą rzeczą, której potrzebujemy, jest obiekt komunikujący się z Tesseract. W `pytesseract` silnik jest dostępny poprzez funkcje na poziomie modułu, ale dla przejrzystości opakujemy go w małą klasę. To odzwierciedla koncepcję „silnika”, którą widziałeś w oryginalnym fragmencie.

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**Dlaczego to opakować?**  
- Utrzymuje publiczne API identyczne z fragmentem, od którego zaczynałeś, co ułatwia migrację.  
- Umożliwia późniejsze dodanie logowania lub obsługi błędów bez modyfikacji głównego przepływu.  
- Pokazuje dobrą praktykę OOP — coś, co doceniają starsi programiści.

---

## Wyodrębnij tekst z obrazu: ustaw język na grecki politoniczny

Teraz, gdy mamy silnik, musimy powiedzieć mu, jakiego języka się spodziewać. Grecki politoniczny używa znaków diakrytycznych, które nie są objęte standardowymi danymi „greek”, więc wskazujemy Tesseract na plik treningowy `grc`.

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

Jeśli kiedykolwiek zechcesz **extract text from image** plików w innym języku, po prostu zamień `"grc"` na `"eng"` dla angielskiego, `"fra"` dla francuskiego itd. Ten sam wiersz działa dla każdego zainstalowanego języka.

---

## Rozpoznaj tekst obrazu: uruchom OCR na PNG

Po ustawieniu języka podajemy PNG do silnika. Oryginalny przykład używał sztywno zakodowanej ścieżki; uczynimy to nieco bardziej elastycznym, używając obiektów `Path`.

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**Wskazówki i przypadki brzegowe**

- **File not found** – otocz wywołanie w `try/except FileNotFoundError`, aby wyświetlić przyjazny komunikat.  
- **Low‑resolution PNG** – rozważ wstępne przetworzenie (np. zmiana rozmiaru, binaryzacja) przy użyciu Pillow przed OCR.  
- **Non‑Greek text** – Tesseract nadal spróbuje zdekodować, ale dokładność gwałtownie spada. Zawsze dopasowuj język.

---

## Wyświetl rozpoznany tekst

Na koniec wypisujemy wynik. W prawdziwym projekcie możesz zapisać go do bazy danych, pliku CSV lub nawet przekazać do potoku tłumaczeniowego.

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

Gdy uruchomisz skrypt na wyraźnym skanie starożytnego greckiego napisu, powinieneś zobaczyć coś podobnego do:

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

Jeśli wynik wygląda na zniekształcony, sprawdź ponownie, czy plik **greek.traineddata** znajduje się w odpowiednim folderze i czy PNG nie jest zbyt zaszumiony.

---

## Pełny działający przykład (wszystkie kroki w jednym skrypcie)

Poniżej znajduje się kompletny, gotowy do uruchomienia program. Zapisz go jako `ocr_greek.py` i uruchom `python ocr_greek.py`.

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**Oczekiwany wynik** (skrócony dla zwięzłości):

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

Jeśli zobaczysz poprawne greckie znaki, gratulacje — pomyślnie wykonałeś operację **ocr png image** w Pythonie!

---

## Częste pytania i profesjonalne wskazówki

### Jak poprawić dokładność przy zaszumionym PNG?

- Konwertuj obraz do odcieni szarości: `img = img.convert('L')`
- Zastosuj prog binarny: `img = img.point(lambda x: 0 if x < 128 else 255, '1')`
- Zwiększ rozdzielczość za pomocą `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`

Te kroki często zamieniają koszmar **recognize image text** w czysty wynik.

### Czy mogę przetwarzać cały folder PNG‑ów?

Oczywiście. Owiń wywołanie `recognize_image` w pętlę `for` iterującą po `Path.glob("*.png")`. Przechowaj każdy wynik w słowniku lub zapisz do CSV do późniejszej analizy.

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### Co zrobić, jeśli potrzebuję wyodrębnić tylko liczby?

Przekaż własny ciąg **config** do `image_to_string`:

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

W ten sposób możesz **extract text from image** pliki zawierające tabele, numery seryjne lub znaczniki czasu.

### Czy istnieje sposób na uzyskanie ocen pewności?

Tak — użyj `pytesseract.image_to_data`, który zwraca TSV z poziomem pewności dla każdego słowa. Możesz odfiltrować tokeny o niskiej pewności przed złożeniem ostatecznego ciągu.

---

## Rozszerzanie samouczka

Teraz, gdy opanowałeś podstawy, rozważ zgłębienie następujących powiązanych tematów:

- **Batch OCR with multiprocessing** – przyspiesz przetwarzanie dużych zbiorów PNG.  
- **Hybrid OCR + NLP pipelines** – automatycznie przetłumacz wyodrębniony starogrecki na współczesny angielski.  
- **Alternative engines** – wypróbuj `easyocr` lub metody oparte na `opencv` dla konkretnych przypadków użycia.  
- **Cloud OCR services** – Google Vision, Azure Computer Vision lub AWS Textract do skalowania bezserwerowego.  

Każdy z nich opiera się na podstawowym **python ocr example**, który właśnie omówiliśmy, więc będziesz czuł się pewnie, zagłębiając się dalej.

---

## Podsumowanie

Przekształciliśmy prosty fragment w solidny przepływ pracy **ocr png image** w Pythonie. Tworząc `OcrEngine`, ustawiając język na grecki politoniczny, podając PNG i wypisując wynik, teraz wiesz, jak **extract text from image** pliki, **recognize image text**, a nawet **read ancient greek**.

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i zbadać alternatywne podejścia implementacyjne w własnych projektach.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}