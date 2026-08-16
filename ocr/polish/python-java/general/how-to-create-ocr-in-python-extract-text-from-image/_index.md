---
category: general
date: 2026-04-26
description: Jak szybko i niezawodnie stworzyć OCR. Dowiedz się, jak wyodrębnić tekst
  z obrazu, załadować obraz do OCR i uruchomić OCR na pliku PNG z własnym słownikiem.
draft: false
keywords:
- how to create OCR
- extract text from image
- extract text scanned document
- load image for OCR
- run OCR on png
language: pl
og_description: Jak stworzyć OCR w Pythonie i wyodrębnić tekst z obrazu. Ten przewodnik
  pokazuje, jak załadować obraz do OCR, uruchomić OCR na pliku PNG oraz używać własnego
  słownika.
og_title: Jak stworzyć OCR w Pythonie – szybkie wyodrębnianie tekstu
tags:
- OCR
- Python
- Image Processing
title: Jak stworzyć OCR w Pythonie – wyodrębnić tekst z obrazu
url: /pl/python-java/general/how-to-create-ocr-in-python-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak stworzyć OCR w Pythonie – Przewodnik krok po kroku

Zastanawiałeś się kiedyś **jak stworzyć OCR**, które potrafi odczytać Twoje zeskanowane PDF‑y, zrzuty ekranu lub odręczne notatki? Nie jesteś sam. W wielu rzeczywistych projektach musimy *wyodrębniać tekst z obrazów*, ale gotowe silniki często mają problemy ze słowami specyficznymi dla danej dziedziny.  

W tym samouczku zobaczysz kompletny, gotowy do uruchomienia przykład, który wczytuje obraz do OCR, stosuje własny słownik i w końcu **uruchamia OCR na plikach PNG**. Po zakończeniu będziesz mógł wyodrębniać tekst z dowolnego obrazu i dostosować silnik do własnej terminologii.

## Co obejmuje ten samouczek

* Instalacja małego, ale potężnego pakietu `aocr` (lub dowolnej kompatybilnej biblioteki).  
* Konfiguracja **własnego słownika**, aby terminy takie jak `aspocorp` czy `licensekey` były rozpoznawane.  
* **Wczytywanie obrazu do OCR**, niezależnie czy to PNG, JPEG, czy zeskanowana strona PDF.  
* Uruchamianie procesu OCR i wyświetlanie wyniku.  

Brak zewnętrznych linków do dokumentacji, tylko samodzielne rozwiązanie, które możesz skopiować‑wkleić i uruchomić już dziś.

### Wymagania wstępne

* Python 3.8 lub nowszy (kod używa f‑stringów).  
* Podstawowa znajomość wiersza poleceń – wpiszesz kilka poleceń `pip install`.  
* Plik obrazu (`technical_doc.png` w przykładzie) umieszczony w miejscu, do którego możesz odwołać się.  

Jeśli spełniasz te trzy warunki, możesz zaczynać.  

---

## Krok 1: Zainstaluj bibliotekę OCR

Najpierw potrzebujemy silnika OCR, który obsługuje programowalny obiekt konfiguracji. Pakiet `aocr` jest lekką nakładką na natywny silnik OCR i dobrze sprawdza się w demonstracjach.

```bash
# Install the library (run once)
pip install aocr
```

> **Wskazówka:** Jeśli używasz Windows i napotkasz błąd kompilacji, spróbuj `pip install aocr‑binary`, który dostarcza gotowe pliki binarne.

### Dlaczego zainstalować tę bibliotekę?

`aocr` daje nam bezpośredni dostęp do obiektu `config`, w którym możemy wstrzyknąć **własny słownik**. To sekretna przyprawa poprawiająca dokładność w niszowych słownictwach.

---

## Krok 2: Utwórz instancję silnika OCR i dodaj własny słownik

Teraz uruchamiamy silnik i informujemy go, które słowa ma traktować jako znane.

```python
from aocr import OcrEngine

# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Provide a custom dictionary to improve recognition of domain‑specific terms
ocr_engine.config.custom_dictionary = [
    "aspocorp",      # our company's brand name
    "ocrengine",    # the library name itself
    "licensekey"    # a common field in our contracts
]
```

### Dlaczego własny słownik ma znaczenie

Standardowe modele OCR są trenowane na ogólnych korpusach. Gdy model zobaczy „aspocorp”, może podzielić je na „aspo corp” lub całkowicie pominąć litery. Dostarczając własną listę, kierujemy rozpoznawanie w stronę dokładnej pisowni, którą potrzebujemy, co znacząco zmniejsza nakład pracy po przetworzeniu.

---

## Krok 3: Wczytaj obraz, który chcesz przetworzyć

Tutaj **wczytujemy obraz do OCR**. Metoda `Image.load` przyjmuje ciąg ścieżki i automatycznie określa typ pliku.

```python
import aocr

# Step 3: Load the image that contains the text you want to extract
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/technical_doc.png")
```

> **Przypadek brzegowy:** Jeśli źródłem jest wielostronicowy PDF, najpierw przekonwertuj każdą stronę na PNG (np. przy użyciu `pdf2image`) i podawaj je pojedynczo do silnika.

### Wskazówki dla lepszej jakości obrazu

* Utrzymuj rozdzielczość co najmniej 300 dpi.  
* Upewnij się, że obraz jest prawidłowo ustawiony; w razie potrzeby obróć go przy użyciu `Pillow`.  
* Przekształć kolorowe skany na odcienie szarości, aby zmniejszyć szumy.

---

## Krok 4: Uruchom proces OCR na pliku PNG

Po skonfigurowaniu silnika i wczytaniu obrazu, w końcu **uruchamiamy OCR na PNG**.

```python
# Step 4: Run the OCR process
ocr_result = ocr_engine.process()
```

Wywołanie `process()` zwraca obiekt zawierający rozpoznany tekst, oceny pewności oraz ramki ograniczające dla każdego słowa.

---

## Krok 5: Wyświetl rozpoznany tekst

Najprostszym sposobem, aby zobaczyć, co silnik znalazł, jest wydrukowanie atrybutu `text`.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### Oczekiwany wynik

Jeśli `technical_doc.png` zawiera zdanie *„The Aspocorp licensekey expires on 2025‑12‑31.”*, konsola powinna wyświetlić:

```
The Aspocorp licensekey expires on 2025-12-31.
```

Zauważ, jak własny słownik zachował nazwę marki w niezmienionej formie — coś, co standardowy OCR mógłby zniekształcić.

---

## Pełny działający przykład (gotowy do kopiowania i wklejania)

Poniżej znajduje się cały skrypt, gotowy do zapisania jako `run_ocr.py`. Wystarczy zamienić ścieżkę zastępczą na lokalizację swojego obrazu.

```python
# run_ocr.py
# -------------------------------------------------
# Complete example showing how to create OCR,
# load an image, apply a custom dictionary,
# and extract text from a PNG file.
# -------------------------------------------------

from aocr import OcrEngine
import aocr

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Add domain‑specific words
    ocr_engine.config.custom_dictionary = [
        "aspocorp",
        "ocrengine",
        "licensekey"
    ]

    # 3️⃣ Load the image you want to process
    #    (Make sure the path points to a real file)
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    ocr_engine.image = aocr.Image.load(image_path)

    # 4️⃣ Run the OCR engine
    ocr_result = ocr_engine.process()

    # 5️⃣ Print the extracted text
    print("=== Extracted Text ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

Uruchom go w terminalu:

```bash
python run_ocr.py
```

Powinieneś zobaczyć wyodrębniony tekst wydrukowany w konsoli, dokładnie tak jak w poprzednim przykładzie.

---

## Najczęściej zadawane pytania (FAQ)

| Question | Answer |
|----------|--------|
| **Czy mogę wyodrębnić tekst ze zeskanowanego PDF?** | Tak. Najpierw przekonwertuj każdą stronę na PNG (lub TIFF), a następnie podaj obrazy do tego samego skryptu. |
| **Co jeśli mój obraz jest JPEG zamiast PNG?** | Metoda `Image.load` obsługuje JPEG, BMP, TIFF i PNG od razu. Wystarczy zmienić rozszerzenie pliku. |
| **Jak poprawić dokładność przy skanach o niskim kontraście?** | Wstępnie przetwórz przy użyciu `Pillow` – zwiększ kontrast, zastosuj binaryzację lub użyj `opencv` do prostowania. |
| **Czy istnieje sposób na uzyskanie ocen pewności dla każdego słowa?** | `ocr_result` zawiera `words` – każde słowo ma atrybut `confidence`, który możesz iterować. |
| **Czy mogę uruchomić to na serwerze bez interfejsu graficznego?** | Oczywiście. `aocr` nie ma zależności GUI, co czyni go idealnym dla potoków CI. |

---

## Kolejne kroki i powiązane tematy

Teraz, gdy wiesz **jak stworzyć OCR** i **wyodrębniać tekst z obrazów**, rozważ dalsze zagadnienia:

* **Techniki wstępnego przetwarzania** – `load image for OCR` to tylko pierwszy krok; użyj `opencv` do odszumiania lub wyostrzania.  
* **Przetwarzanie wsadowe** – iteruj po katalogu PNG‑ów, aby wygenerować przeszukiwane archiwum.  
* **Wsparcie wielojęzyczne** – dodaj pakiety językowe do silnika, jeśli potrzebujesz czytać dokumenty po francusku lub niemiecku.  
* **Integracja z Elasticsearch** – indeksuj wyodrębniony tekst, aby umożliwić pełnotekstowe wyszukiwanie w zeskanowanych zasobach.  

Każde z tych rozszerzeń opiera się na podstawowym wzorcu, który właśnie omówiliśmy, więc przejście będzie bezproblemowe.

---

## Podsumowanie

W ciągu kilku minut odpowiedzieliśmy na pytanie **jak stworzyć OCR**, które niezawodnie **wyodrębnia tekst z obrazów**, szczególnie PNG, i pokazaliśmy, jak **wczytać obraz do OCR**, zastosować **własny słownik** oraz **uruchomić OCR na PNG** bez żadnych zewnętrznych usług.  

Uruchom skrypt, dostosuj słownik do własnego żargonu i będziesz mieć solidną podstawę dla każdego projektu digitalizacji dokumentów.  

Jeśli napotkasz jakiekolwiek problemy, zostaw komentarz poniżej — chętnie pomogę. I nie zapomnij podzielić się swoimi sukcesami; społeczność najlepiej uczy się na rzeczywistych przykładach.  

**Gotowy, aby zautomatyzować swoje dokumenty?** Pobierz kod, dostosuj go i zacznij przekształcać piksele w przeszukiwalny tekst już dziś!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}