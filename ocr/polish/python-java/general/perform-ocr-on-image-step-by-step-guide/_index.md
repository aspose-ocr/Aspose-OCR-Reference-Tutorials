---
category: general
date: 2026-03-18
description: Wykonaj OCR na obrazie, aby szybko wyodrębnić tekst z obrazu. Dowiedz
  się, jak załadować obraz do OCR, utworzyć silnik OCR i poprawić dokładność OCR dzięki
  opcjom językowym.
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: pl
og_description: Wykonaj OCR na obrazie dzięki temu szczegółowemu przewodnikowi. Dowiedz
  się, jak załadować obraz do OCR, stworzyć silnik OCR i poprawić dokładność OCR,
  aby uzyskać niezawodne wyodrębnianie tekstu.
og_title: Wykonaj OCR na obrazie – Kompletny samouczek programowania
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Wykonaj OCR na obrazie – Przewodnik krok po kroku
url: /pl/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wykonaj OCR na obrazie – Kompletny samouczek programistyczny

Kiedykolwiek potrzebowałeś **wykonać OCR na obrazie**, ale nie wiedziałeś, którą bibliotekę wybrać ani jak uzyskać wiarygodne wyniki? Nie jesteś sam. W tym przewodniku przejdziemy przez wszystko, co potrzebne, aby **wyodrębnić tekst z obrazu**, od wczytania zdjęcia po dostosowanie opcji językowych, abyś mógł **poprawić dokładność OCR** na każdym etapie.

Omówimy, jak **wczytać obraz do OCR**, jak **utworzyć silnik OCR**, oraz dlaczego każde ustawienie ma znaczenie. Po zakończeniu będziesz mieć gotowy do uruchomienia skrypt, który wypisze rozpoznany tekst, i zrozumiesz „dlaczego” stojące za każdą linijką – bez niejasnych „zobacz dokumentację” skrótów. Zanurzmy się.

## Czego będziesz potrzebować

- Python 3.8+ (kod używa f‑stringów i podpowiedzi typów)
- Hipotetyczny pakiet `ocr_lib` – zainstaluj go poleceniem `pip install ocr_lib`
- Plik obrazu zawierający wyraźny, drukowany tekst (np. `lab_report.png`)
- Podstawowy edytor tekstu lub IDE (VS Code, PyCharm, cokolwiek lubisz)

Jeśli już to masz, świetnie – jesteś gotowy. Jeśli nie, pobierz Pythona ze strony python.org i uruchom polecenie pip; zajmie to tylko chwilę.

![perform OCR on image example](/images/ocr-example.png)

*Alt text: wykonaj OCR na obrazie – przykładowy wynik pokazujący wyodrębniony tekst.*

## Krok 1: Utwórz silnik OCR – Jak **create OCR engine** w Pythonie

Zanim możliwe będzie rozpoznanie, biblioteka potrzebuje obiektu silnika, który przechowuje konfigurację i stan w czasie działania. Pomyśl o silniku jako o mózgu operacji.

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**Dlaczego to ważne:** Wczesne zainicjowanie silnika pozwala później dołączyć opcje językowe i jednocześnie buforuje wewnętrzne modele, co przyspiesza kolejne wywołania.

## Krok 2: Wczytaj obraz do OCR – Poprawny sposób **load image for OCR**

Teraz, gdy mamy silnik, musimy podać mu coś do odczytania. Metoda `setImageFromFile` przyjmuje ścieżkę systemową; ścieżka może być absolutna lub względna względem katalogu roboczego skryptu.

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**Pro tip:** Używaj ścieżki absolutnej lub `os.path.join`, aby uniknąć niespodzianek „plik nie znaleziony”, gdy skrypt uruchamiany jest z innego folderu.

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## Krok 3: Popraw dokładność OCR – Dostosowanie **language options** aby **improve OCR accuracy**

Domyślne OCR działa, ale słownictwo specyficzne dla danej dziedziny (np. żargon laboratoryjny) często je dezorientuje. Dostarczając własny słownik i czarną listę, zmniejszasz pomyłki, takie jak mylenie „0” z „O”.

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**Dlaczego to pomaga:** Słownik informuje model OCR, że „HPLC” jest prawidłowym tokenem, zapobiegając rozdzieleniu słowa na bezużyteczne fragmenty. Czarna lista mówi modelowi, aby traktował niejednoznaczne symbole jako szum, co bezpośrednio **poprawia dokładność OCR**.

## Krok 4: Wykonaj OCR na obrazie – Główne wywołanie **perform OCR on image**

Po przygotowaniu silnika i podłączeniu obrazu, czas na faktyczne rozpoznanie tekstu. Ten krok zwraca obiekt `OcrResult`, który możesz przeglądać pod kątem surowego tekstu, wskaźników pewności lub prostokątów ograniczających.

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

Jeśli obraz jest rozmyty, zobaczysz niższe liczby pewności w wyniku. To sygnał, aby przed podaniem obrazu do silnika przeprowadzić wstępne przetwarzanie (np. zwiększyć kontrast).

## Krok 5: Wyodrębnij tekst z obrazu – Pobranie ostatecznego ciągu znaków

Na koniec pytamy `OcrResult` o jego reprezentację tekstową. Metoda `getText()` zwraca zwykły ciąg znaków gotowy do dalszego przetwarzania (zapisywania do pliku, wprowadzania do bazy danych itp.).

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**Oczekiwany wynik:** Zakładając, że `lab_report.png` zawiera prostą tabelę, możesz zobaczyć coś takiego:

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

To już część **extract text from image** zakończona.

## Pełny działający przykład – Połącz wszystko razem

Poniżej znajduje się pojedynczy skrypt, który scala elementy z poprzednich sekcji. Możesz go skopiować do pliku `run_ocr.py` i uruchomić poleceniem `python run_ocr.py`.

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### Szybka lista kontrolna weryfikacji

| ✅ | Element |
|---|------|
| ✔️ | Silnik został utworzony (`create OCR engine`) |
| ✔️ | Obraz został wczytany (`load image for OCR`) |
| ✔️ | Opcje językowe zostały ustawione (`improve OCR accuracy`) |
| ✔️ | OCR zostało wykonane (`perform OCR on image`) |
| ✔️ | Tekst został wyodrębniony (`extract text from image`) |

Uruchom skrypt i obserwuj konsolę. Jeśli zobaczysz blok „OCR Output” z zawartością Twojego raportu, pomyślnie **wykonałeś OCR na obrazie**.

## Typowe pułapki i jak ich unikać

| Problem | Dlaczego się pojawia | Rozwiązanie |
|-------|----------------|-----|
| **Rozmyte wejście** | Model OCR nie rozróżnia znaków | Przetwórz wstępnie za pomocą OpenCV: `cv2.GaussianBlur` lub zwiększ DPI |
| **Nieprawidłowy język** | Domyślny język może być ustawiony na inny niż angielski | Wywołaj `engine.setLanguage("eng")` przed `recognize()` |
| **Brak terminów w słowniku** | Słowa specyficzne dla dziedziny stają się zniekształcone | Dodaj je poprzez `setDictionary` jak pokazano w Kroku 3 |
| **Czarna lista znaków powoduje |  |  |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}