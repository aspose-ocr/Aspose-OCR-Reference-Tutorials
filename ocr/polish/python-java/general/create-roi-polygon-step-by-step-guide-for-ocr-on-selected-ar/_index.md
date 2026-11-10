---
category: general
date: 2026-03-26
description: Utwórz wielokąt ROI, aby uruchomić OCR na wybranym obszarze. Dowiedz
  się, jak definiować wiele regionów, rejestrować je i wyodrębniać tekst za pomocą
  silnika OCR w Pythonie.
draft: false
keywords:
- create roi polygon
- ocr on selected area
- region of interest
- ocr engine
- python ocr example
language: pl
og_description: Utwórz wielokąt ROI i uruchom OCR na wybranym obszarze przy użyciu
  silnika Pythona. Pełny kod, wyjaśnienia i wskazówki w zestawie.
og_title: Utwórz wielokąt ROI – szybkie OCR w wybranym obszarze
tags:
- OCR
- Python
- Image Processing
title: Utwórz wielokąt ROI – Przewodnik krok po kroku dla OCR w wybranym obszarze
url: /pl/python-java/general/create-roi-polygon-step-by-step-guide-for-ocr-on-selected-ar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz wielokąt ROI – Pełny tutorial OCR na wybranym obszarze

Kiedykolwiek potrzebowałeś **utworzyć wielokąt ROI**, aby uruchomić OCR tylko na części obrazu, która ma znaczenie? Być może skanujesz paragony i interesują Cię tylko sumy, albo masz formularz, w którym tylko pole podpisu wymaga odczytu. W takich przypadkach **ocr on selected area** oszczędza czas i zwiększa dokładność.  

W tym przewodniku przejdziemy krok po kroku przez wszystko, co jest potrzebne: od zdefiniowania dwóch wielokątów, zarejestrowania ich w silniku OCR, po pobranie rozpoznanego tekstu w jednym czystym wywołaniu. Po zakończeniu będziesz mieć gotowy do uruchomienia skrypt oraz solidne zrozumienie, dlaczego skupianie się na regionach zainteresowania ma znaczenie.

## Czego się nauczysz

- Jak **utworzyć obiekty ROI polygon** przy użyciu typowej biblioteki OCR.
- Różnicę między definiowaniem jednego regionu a wieloma.
- Jak zarejestrować te regiony w silniku, aby wykonać `ocr on selected area`.
- Oczekiwany wynik i jak rozwiązywać typowe problemy (np. nakładające się ROI, puste wyniki).

### Wymagania wstępne

- Python 3.8+ zainstalowany.
- Biblioteka OCR udostępniająca klasy `Polygon`, `Point` oraz metodę `add_region_of_interest` (przykład używa fikcyjnego modułu `ocr`; zamień go na swoją rzeczywistą SDK, np. opakowania Tesseract‑Python lub EasyOCR).
- Przykładowy plik obrazu (`sample.png`) zawierający tekst w podanych poniżej współrzędnych.

> **Pro tip:** Jeśli używasz prawdziwej biblioteki, upewnij się, że obraz jest wczytany w tej samej przestrzeni współrzędnych (pochodzenie w lewym górnym rogu, X rośnie w prawo, Y rośnie w dół).  

---  

## Krok 1: Importuj moduł OCR i wczytaj obraz  

Najpierw zaimportuj pakiet OCR i odczytaj obraz, który chcesz przetworzyć.  

```python
import ocr  # Replace with your actual OCR library import
from pathlib import Path

# Load the image – adjust the path as needed
image_path = Path("sample.png")
ocr_engine = ocr.Engine(image_path)
```

*Dlaczego to ważne:* Silnik potrzebuje danych obrazu, zanim będziesz mógł dołączyć **ROI polygon**. Niektóre biblioteki pozwalają przekazać obraz później, ale wczesna inicjalizacja utrzymuje przepływ pracy schludnym.

## Krok 2: Zdefiniuj pierwszy wielokąt ROI  

Teraz tworzymy pierwszy region zainteresowania. Pomyśl o tym jak o narysowaniu prostokąta wokół nagłówka tabeli.  

```python
# Step 2: Define the first ROI polygon
first_roi = ocr.Polygon([
    ocr.Point(50, 20),   # top‑left
    ocr.Point(200, 20),  # top‑right
    ocr.Point(200, 80),  # bottom‑right
    ocr.Point(50, 80)    # bottom‑left
])
```

*Wyjaśnienie:*  
- `ocr.Point(x, y)` używa współrzędnych pikselowych.  
- Lista punktów jest uporządkowana zgodnie z ruchem wskazówek zegara, co wymaga większość silników.  
- Możesz dodać dowolną liczbę punktów, aby stworzyć nieregularne kształty; prostokąt to po prostu szczególny przypadek.

## Krok 3: Zdefiniuj dodatkowe wielokąty ROI (opcjonalnie)  

Nie musisz zatrzymywać się na jednym. Oto drugi wielokąt, który obejmuje pole podpisu niżej na stronie.  

```python
# Step 3: Define the second ROI polygon
second_roi = ocr.Polygon([
    ocr.Point(300, 150),
    ocr.Point(480, 150),
    ocr.Point(480, 210),
    ocr.Point(300, 210)
])
```

*Dlaczego dodać więcej?* Uruchamianie **ocr on selected area** dla wielu stref pozwala wyodrębnić różne fragmenty danych w jednym przebiegu, co jest znacznie szybsze niż przycinanie i przetwarzanie każdego fragmentu osobno.

## Krok 4: Zarejestruj ROI w silniku OCR  

Mając gotowe wielokąty, poinformuj silnik, które obszary ma skanować.  

```python
# Step 4: Register the ROIs
ocr_engine.add_region_of_interest(first_roi)
ocr_engine.add_region_of_interest(second_roi)
```

*Ważna uwaga:* Niektóre SDK wymagają wywołania metody `clear_regions()` przed dodaniem nowych, jeśli ponownie używasz silnika dla innego obrazu.

## Krok 5: Uruchom OCR i pobierz tekst  

Na koniec uruchom rozpoznawanie. Silnik będzie patrzył wyłącznie wewnątrz dodanych wielokątów.  

```python
# Step 5: Perform OCR on the defined regions
recognized_text = ocr_engine.recognize().get_text()
print("=== Recognized Text ===")
print(recognized_text)
```

**Oczekiwany wynik** (zakładając, że `sample.png` zawiera słowa „Invoice Total: $123.45” w pierwszym ROI i „Signature: John Doe” w drugim):

```
=== Recognized Text ===
Invoice Total: $123.45
Signature: John Doe
```

Jeśli wynik jest pusty, sprawdź, czy współrzędne faktycznie przecinają tekst oraz czy rozdzielczość obrazu odpowiada systemowi współrzędnych.

## Przypadki brzegowe i typowe pułapki  

| Sytuacja                                 | Na co zwrócić uwagę                              | Naprawa / obejście                                 |
|------------------------------------------|--------------------------------------------------|----------------------------------------------------|
| **Nakładające się ROI**                  | Tekst może zostać zwrócony dwukrotnie.           | Utrzymuj wielokąty rozłączne lub deduplikuj wynik. |
| **ROI poza granicami obrazu**            | Silnik może zgłosić błąd lub zwrócić nic.       | Ogranicz współrzędne do `0 ≤ x < width`, `0 ≤ y < height`. |
| **Bardzo małe ROI**                      | Dokładność OCR spada z powodu niewystarczającej liczby pikseli. | Rozszerz wielokąt o kilka pikseli lub najpierw zwiększ rozdzielczość obrazu. |
| **Kształt nierektangularny**             | Niektóre silniki obsługują tylko wypukłe wielokąty. | Podziel złożone kształty na kilka wypukłych ROI. |
| **Zmiana rozmiaru obrazu**               | Na sztywno zapisane współrzędne stają się nieprawidłowe. | Oblicz współrzędne ROI względnie do wymiarów obrazu (np. w procentach). |

## Pełny działający przykład  

Poniżej znajduje się kompletny skrypt, który możesz skopiować i uruchomić (zamień `ocr` na swoją rzeczywistą bibliotekę).  

```python
import ocr                      # <- your OCR library
from pathlib import Path

# -------------------------------------------------
# Configuration
# -------------------------------------------------
IMAGE_PATH = Path("sample.png")

# -------------------------------------------------
# Initialize OCR engine with the image
# -------------------------------------------------
engine = ocr.Engine(IMAGE_PATH)

# -------------------------------------------------
# Define ROI polygons
# -------------------------------------------------
first_roi = ocr.Polygon([
    ocr.Point(50, 20), ocr.Point(200, 20),
    ocr.Point(200, 80), ocr.Point(50, 80)
])

second_roi = ocr.Polygon([
    ocr.Point(300, 150), ocr.Point(480, 150),
    ocr.Point(480, 210), ocr.Point(300, 210)
])

# -------------------------------------------------
# Register ROIs
# -------------------------------------------------
engine.add_region_of_interest(first_roi)
engine.add_region_of_interest(second_roi)

# -------------------------------------------------
# Run OCR on the selected areas
# -------------------------------------------------
result = engine.recognize().get_text()

print("=== Recognized Text ===")
print(result)
```

Uruchom go poleceniem `python ocr_roi_example.py`, a powinieneś zobaczyć wyodrębnione ciągi znaków z dwóch zdefiniowanych stref.

## Kolejne kroki  

- **Dynamiczne generowanie ROI:** Zamiast sztywno kodować współrzędne, użyj przetwarzania obrazu (np. wykrywania konturów w OpenCV), aby automatycznie lokalizować tabele lub pola.  
- **Post‑processing:** Usuń białe znaki, zastosuj wyrażenia regularne lub przekształć liczby do odpowiednich typów danych.  
- **Przetwarzanie wsadowe:** Iteruj po folderze obrazów, ponownie używając tych samych definicji ROI, jeśli układ jest spójny.  

Jeśli interesuje Cię **ocr on selected area** w bardziej złożonych dokumentach — myśl o wielostronicowych PDF‑ach lub skanach formularzy — przyjrzyj się bibliotekom, które wspierają rejestrację ROI po stronie każdej strony.  

---  

### Przegląd wizualny  

![Diagram showing two ROI polygons on a sample image](roi_diagram.png){alt="przykład tworzenia wielokąta ROI pokazujący dwa wybrane obszary"}

Diagram ilustruje, jak dwa prostokąty (niebieski i zielony) nakładają się na podstawowy obraz, podkreślając dokładnie to, co silnik OCR odczyta.

---  

## Zakończenie  

Właśnie **utworzyliśmy obiekty ROI polygon**, zarejestrowaliśmy je w silniku OCR i wykonaliśmy `ocr on selected area` w czystym, powtarzalnym skrypcie. Ograniczając silnik do interesujących Cię stref, skracasz czas przetwarzania, podnosisz dokładność i upraszcza się dalsza obsługa danych.  

Wypróbuj to na własnych obrazach — dostosuj współrzędne, dodaj kolejne wielokąty lub podłącz wynik do bazy danych. Gdy opanujesz OCR oparty na regionach, nie ma granic, co możesz osiągnąć.  

Masz pytania lub chcesz podzielić się ciekawym przypadkiem użycia? zostaw komentarz poniżej i powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}