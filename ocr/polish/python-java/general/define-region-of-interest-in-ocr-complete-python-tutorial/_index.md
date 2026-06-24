---
category: general
date: 2026-06-16
description: Zdefiniuj obszar zainteresowania w OCR, aby wyodrębnić hiszpański tekst
  z dowodów tożsamości. Dowiedz się, jak załadować obraz do OCR i efektywnie określić
  ROI.
draft: false
keywords:
- define region of interest
- load image for ocr
- how to specify roi
- extract id card text
- extract spanish text image
language: pl
og_description: Zdefiniuj obszar zainteresowania w OCR, aby wyodrębnić hiszpański
  tekst z dowodów tożsamości. Przewodnik krok po kroku dotyczący ładowania obrazów
  i określania ROI.
og_title: Zdefiniuj obszar zainteresowania w OCR – Kompletny samouczek Pythona
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Define region of interest in OCR to extract Spanish text from ID cards.
    Learn how to load image for OCR and specify ROI efficiently.
  headline: Define region of interest in OCR – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Zdefiniuj obszar zainteresowania w OCR – Kompletny samouczek Pythona
url: /pl/python-java/general/define-region-of-interest-in-ocr-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definiowanie regionu zainteresowania w OCR – Kompletny samouczek Pythona

Zastanawiałeś się kiedyś, jak **zdefiniować region zainteresowania w OCR**, aby odczytywać tylko tę część obrazu, której naprawdę potrzebujesz? W tym samouczku przeprowadzimy Cię krok po kroku przez to, a także pokażemy, jak **załadować obraz do OCR** i wyodrębnić hiszpański tekst z dowodu tożsamości w kilku linijkach Pythona.  

Jeśli kiedykolwiek patrzyłeś na zaszumiony skan i myślałeś: „Musi istnieć czystszy sposób, aby wyłapać pole imienia”, jesteś we właściwym miejscu. Po zakończeniu będziesz w stanie pobrać tekst z dowodu tożsamości, który Cię interesuje, bez uciążliwego tła.

## Czego się nauczysz

- Dlaczego powinieneś **zdefiniować region zainteresowania** przed uruchomieniem OCR.  
- Dokładne kroki, aby **załadować obraz do OCR** przy użyciu popularnego wrappera OCR w Pythonie.  
- Jak **określić ROI** przy użyciu współrzędnych pikseli.  
- Sposoby na **wyodrębnienie tekstu z dowodu tożsamości** w sposób niezawodny, nawet gdy językiem źródłowym jest hiszpański.  
- Wskazówki dotyczące obsługi przypadków brzegowych, takich jak obrócone karty lub skany o niskim kontraście.  

Nie wymagana jest wcześniejsza znajomość OCR — wystarczy działające środowisko Python 3 oraz plik JPEG dowodu tożsamości, który chcesz przetestować.

---

![Define region of interest illustration](placeholder.png){alt="Przykład definiowania regionu zainteresowania pokazujący podświetlony prostokąt na obrazie dowodu tożsamości"}

## Krok 1: Zainstaluj i zaimportuj bibliotekę OCR

Najpierw potrzebujesz biblioteki, która udostępnia klasę `OcrEngine` podobną do tej w pokazanym fragmencie. W tym przewodniku użyjemy fikcyjnego pakietu `ocr`, ale te same koncepcje mają zastosowanie do `pytesseract`, `easyocr` lub dowolnego wrappera, który pozwala ustawić język i ROI.

```bash
pip install ocr   # Replace with the actual package name you use
```

```python
# Import the library and any helper classes
import ocr
from ocr import Rectangle, Image
```

*Pro tip:* Jeśli używasz `pytesseract`, klasa `Rectangle` staje się prostą krotką `(left, top, width, height)`. Reszta przepływu pozostaje identyczna.

## Krok 2: Załaduj obraz do OCR

Teraz **załadujemy obraz do OCR**. Silnik oczekuje obiektu `ocr.Image`, więc wskazujemy mu plik zawierający dowód tożsamości. Upewnij się, że ścieżka jest absolutna lub względna względem katalogu roboczego Twojego skryptu.

```python
# Create the OCR engine instance
engine = ocr.OcrEngine()

# Tell the engine which language we’re interested in – Spanish in this case
engine.language = ocr.Language.SPANISH

# Load the source image that contains the text to be recognized
engine.image = Image.load_from_file("YOUR_DIRECTORY/id-card.jpg")
```

Jeśli obraz jest bardzo duży, rozważ najpierw zmianę rozmiaru; silniki OCR działają szybciej na obrazach o szerokości poniżej 1500 px.

## Krok 3: Jak określić ROI (Definiowanie regionu zainteresowania)

Oto serce samouczka: **określić ROI**. Region zainteresowania to po prostu prostokąt, który mówi silnikowi OCR: „Patrz tylko w obrębie tych granic pikseli”. Pomyśl o tym jak o narysowaniu ramki wokół pola imienia na dowodzie tożsamości.

```python
# Define the region of interest – left, top, width, height (all in pixels)
engine.region_of_interest = Rectangle(
    left=120,   # X‑coordinate of the left edge
    top=80,     # Y‑coordinate of the top edge
    width=340,  # Width of the box
    height=200  # Height of the box
)
```

Dlaczego te liczby? W naszym przykładowym obrazie imię znajduje się mniej więcej 120 px od lewej krawędzi i 80 px od górnej. Dostosuj je do układu kart, które przetwarzasz.  

*Przypadek brzegowy:* Jeśli karta jest obrócona o 90°, zamień `width` i `height` oraz odpowiednio dostosuj `left`/`top`, albo wstępnie obróć obraz przy pomocy Pillow przed przekazaniem go do silnika.

## Krok 4: Wykonaj OCR w obrębie ROI

Po zdefiniowaniu ROI silnik zignoruje wszystko poza prostokątem. To nie tylko przyspiesza przetwarzanie, ale także zmniejsza liczbę fałszywych trafień spowodowanych grafiką w tle.

```python
# Run OCR only inside the defined ROI
roi_result = engine.recognize()
```

Wywołanie `recognize()` zwraca obiekt zawierający rozpoznany tekst, wyniki pewności oraz ramki ograniczające dla każdego słowa.

## Krok 5: Wyodrębnij tekst z dowodu tożsamości (i zweryfikuj wynik w języku hiszpańskim)

Na koniec **wyodrębniamy tekst z dowodu tożsamości** z wyniku ROI i drukujemy go. Ponieważ wcześniej ustawiliśmy język na hiszpański, silnik OCR zastosuje słowniki specyficzne dla tego języka, poprawiając dokładność znaków diakrytycznych takich jak „ñ” czy „á”.

```python
# Output the recognized text from the ROI
print("ROI text:", roi_result.text)
```

### Oczekiwany wynik

```
ROI text: JUAN PÉREZ GARCÍA
```

Jeśli zobaczysz zniekształcone znaki, sprawdź ponownie, czy obraz rzeczywiście jest w języku hiszpańskim i czy pliki danych językowych biblioteki OCR są zainstalowane.

## Typowe pułapki i jak ich unikać

| Objaw | Prawdopodobna przyczyna | Rozwiązanie |
|---------|--------------|-----|
| Zwrócono pusty ciąg | ROI nie przecina żadnego tekstu | Sprawdź współrzędne w przeglądarce obrazu; użyj `engine.debug_draw_roi()`, jeśli jest dostępne. |
| Wiele nieprawidłowych znaków | Nieprawidłowy pakiet językowy | Ponownie zainstaluj dane językowe hiszpańskiego lub przełącz na `ocr.Language.AUTO`. |
| Niskie wyniki pewności | Obraz jest rozmyty lub o niskim kontraście | Wstępnie przetwórz za pomocą OpenCV – zastosuj `cv2.GaussianBlur` i `cv2.threshold`. |
| OCR działa na całym obrazie pomimo ROI | Używanie starszej wersji biblioteki | Uaktualnij do najnowszej wersji pakietu `ocr`; starsze wersje ignorowały ROI. |

## Rozszerzenie przykładu: wiele ROI

Czasami trzeba pobrać więcej niż jedno pole (np. imię i numer dowodu). Wzorzec pozostaje ten sam: zmień `engine.region_of_interest` i ponownie wywołaj `recognize()`.

```python
# ROI for the ID number (different coordinates)
engine.region_of_interest = Rectangle(120, 300, 340, 80)
id_result = engine.recognize()
print("ID Number:", id_result.text)
```

Możesz także przetwarzać wsadowo listę prostokątów, jeśli biblioteka to obsługuje, co oszczędza dodatkowe wywołania silnika OCR.

## Pełny działający skrypt

Łącząc wszystko razem, oto gotowy do uruchomienia skrypt, który **definiuje region zainteresowania**, **ładuje obraz do OCR** i **wyodrębnia hiszpański tekst** z dowodu tożsamości.

```python
import ocr
from ocr import Rectangle, Image

def extract_name_from_id(image_path):
    """
    Loads an image, defines a ROI around the name field,
    runs OCR in Spanish, and returns the recognized text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.SPANISH
    engine.image = Image.load_from_file(image_path)

    # Adjust these numbers to match your card layout
    engine.region_of_interest = Rectangle(left=120, top=80, width=340, height=200)

    result = engine.recognize()
    return result.text.strip()

if __name__ == "__main__":
    name = extract_name_from_id("YOUR_DIRECTORY/id-card.jpg")
    print("Extracted Name:", name)
```

Uruchom skrypt, a w konsoli powinno pojawić się imię. Zmień wartości prostokąta, aby celować w inne pola, i będziesz mieć wielokrotnego użytku narzędzie do dowolnego dokumentu typu dowód tożsamości.

## Kolejne kroki

- **Przetwarzanie wsadowe:** Przejdź przez folder z dowodami tożsamości i zapisz każde wyodrębnione imię do pliku CSV.  
- **Wykrywanie języka:** Pozwól użytkownikowi wybrać język dynamicznie; `ocr.Language.AUTO` może być przydatny.  
- **Post‑przetwarzanie:** Zastosuj wyrażenia regularne, aby usunąć typowe błędy OCR (np. zamień „0” na „O”, gdy pojawia się w nazwiskach).  

Opanowując **definiowanie regionu zainteresowania**, odblokowałeś potężny sposób na **wyodrębnianie tekstu z dowodu tożsamości** szybko i dokładnie, szczególnie przy dokumentach w języku hiszpańskim.

---

### TL;DR

Pokażemy Ci, jak **zdefiniować region zainteresowania w OCR**, **załadować obraz do OCR** i **określić ROI**, aby **wyodrębnić hiszpański tekst** z dowodu tożsamości. Pełny przykład działa w mniej niż minutę i można go dostosować do dowolnego układu, zmieniając kilka współrzędnych. Wypróbuj, zmień prostokąt i zobacz, jak OCR skupia się jak laser.

Happy coding!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu oraz szczegółowe wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Jak wyodrębnić tekst z obrazu przygotowując prostokąty w OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Wyodrębnianie tekstu z obrazu w C# z wyborem języka przy użyciu Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Wyodrębnianie tekstu z obrazu – optymalizacja OCR z Aspose.OCR dla .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}