---
category: general
date: 2026-03-26
description: Dowiedz się, jak uruchomić OCR na arabskich obrazach PNG i szybko wyodrębnić
  arabski tekst. Ten przewodnik pokazuje konwersję obrazu na tekst przy użyciu krok
  po kroku kodu w Pythonie.
draft: false
keywords:
- how to run ocr
- extract arabic text
- recognize arabic text
- convert image to text
- extract text from png
language: pl
og_description: Jak uruchomić OCR na arabskich obrazach PNG? Przeczytaj ten kompletny
  przewodnik, aby wyodrębnić arabski tekst, rozpoznać arabski tekst i przekształcić
  obraz w tekst przy użyciu Pythona.
og_title: Jak uruchomić OCR na arabskim pliku PNG – wyodrębnić tekst z obrazu
tags:
- OCR
- Python
- Arabic
title: Jak uruchomić OCR na arabskim pliku PNG – wyodrębnić tekst z obrazu
url: /pl/python-java/general/how-to-run-ocr-on-arabic-png-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak uruchomić OCR na arabskim PNG – wyodrębnić tekst z obrazu

Zastanawiałeś się kiedyś **jak uruchomić OCR** na obrazie zawierającym arabski skrypt? Może masz zeskanowany paragon, historyczny rękopis lub po prostu zrzut ekranu z posta w mediach społecznościowych i potrzebujesz tekstu w formacie przeszukiwalnym. Nie jesteś sam — programiści na całym świecie napotykają ten problem przy pracy z językami pisanymi od prawej do lewej.

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który pokazuje **jak uruchomić OCR** na pliku PNG, wyodrębnić arabski tekst i wydrukować wynik w konsoli. Bez niejasnych odnośników „zobacz dokumentację”; po prostu kod, który możesz skopiować‑wkleić, oraz wyjaśnienia, dlaczego każda linia ma znaczenie. Po zakończeniu będziesz w stanie **przekształcić obraz w tekst** niezawodnie, nawet gdy źródłem jest trudny arabski PNG.

> **Czego się nauczysz**
> - Skonfigurować silnik OCR w Pythonie dla języka arabskiego  
> - Wczytać obraz PNG i radzić sobie z typowymi pułapkami  
> - Rozpoznać arabski tekst i zweryfikować wynik  
> - Porady dotyczące **wyodrębniania arabskiego tekstu** z obrazów o różnej jakości  

Zanim zaczniemy, upewnij się, że masz zainstalowany Python 3.8+ oraz aktualną wersję biblioteki `ocr` (tej użytej w przykładzie). Jeśli używasz wirtualnego środowiska, aktywuj je teraz — to utrzyma zależności w porządku.

## Prerequisites

- Python 3.8 lub nowszy  
- pakiet `ocr` (`pip install ocr‑engine` – zamień na rzeczywistą nazwę pakietu)  
- Obraz PNG z arabskim tekstem (`arabic_doc.png`) umieszczony w miejscu, które możesz odwołać  
- Podstawowa znajomość funkcji i klas w Pythonie  

To wszystko. Bez ciężkich frameworków, bez kontenerów Docker — po prostu czysty Python.

## Krok 1: Zainstaluj i zaimportuj bibliotekę OCR

Najpierw najważniejsze. Potrzebujemy samego silnika OCR. Biblioteka, której użyjemy, udostępnia klasę `OcrEngine` z prostym API.

```python
# Install the library (run once in your terminal)
# pip install ocr-engine   # <-- replace with the correct package name

# Import the necessary classes
import ocr
from ocr import Imaging
```

*Dlaczego importujemy `Imaging` osobno?* Podmoduł `Imaging` zapewnia wygodną metodę `Image.load`, która rozumie PNG, JPEG i TIFF od razu. Pominięcie tego kroku zmusiłoby Cię do ręcznego obsługiwania surowych bajtów, co jest niepotrzebne w większości przypadków użycia.

## Krok 2: Utwórz instancję silnika OCR

Teraz tworzymy instancję silnika. Traktuj ten obiekt jako „mózg”, który będzie przetwarzał obraz.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

> **Pro tip:** Jeśli planujesz przetwarzać wiele obrazów kolejno, używaj tej samej instancji `ocr_engine`. Przechowuje ona w pamięci modele językowe, co przyspiesza kolejne rozpoznania.

## Krok 3: Ustaw język na arabski

Arabski nie jest łaciński; ma własny zestaw znaków, kierunek od prawej do lewej i kontekstowe kształtowanie. Dlatego musimy wyraźnie poinformować silnik, który model językowy ma załadować.

```python
# Step 3: Set the language to Arabic (language code "ar")
ocr_engine.set_language("ar")
```

Jeśli zapomnisz tej linii, silnik domyślnie użyje angielskiego i otrzymasz zniekształcony wynik — coś, co widziałem zbyt często.

## Krok 4: Wczytaj swój obraz PNG

Tutaj naprawdę zaczyna się część **przekształcania obrazu w tekst**. Wczytamy plik PNG zawierający arabski skrypt.

```python
# Step 4: Load the image that contains the Arabic text
image_path = "YOUR_DIRECTORY/arabic_doc.png"   # replace with your actual path
ocr_engine.set_image(Imaging.Image.load(image_path))
```

### Typowe przypadki brzegowe

| Problem | Objaw | Rozwiązanie |
|-------|---------|-----|
| Obraz jest zbyt ciemny | Wynik zawiera wiele pustych miejsc | Przetwórz wstępnie za pomocą Pillow (`ImageEnhance.Brightness`) |
| PNG ma kanał alfa | Niektóre silniki OCR błędnie odczytują przezroczyste piksele | Konwertuj do RGB (`image.convert("RGB")`) przed wczytaniem |
| Tekst jest obrócony | Rozpoznany tekst jest do góry nogami | Obróć obraz (`image.rotate(90, expand=True)`) przed przekazaniem do silnika |

## Krok 5: Uruchom proces rozpoznawania

Gdy wszystko jest gotowe, w końcu prosimy silnik o wykonanie zadania.

```python
# Step 5: Run the recognition process
ocr_result = ocr_engine.recognize()
```

Metoda `recognize` zwraca obiekt zawierający surowy ciąg Unicode, oceny pewności i ramki ograniczające. Dla większości programistów wystarczy sam tekst.

## Krok 6: Wyświetl rozpoznany arabski tekst

Teraz drukujemy wynik. W prawdziwej aplikacji możesz zapisać go do pliku, bazy danych lub przekazać do API tłumaczenia.

```python
# Step 6: Output the recognized text
print(ocr_result.get_text())
```

Gdy uruchomisz skrypt, powinieneś zobaczyć arabskie znaki wyświetlone w konsoli (upewnij się, że Twój terminal obsługuje Unicode). Jeśli widzisz znaki zapytania lub puste ciągi, sprawdź ponownie ustawienie języka i jakość obrazu.

### Oczekiwany wynik

```
هذا نص عربي من صورة PNG تم استخراجها باستخدام OCR.
```

Jeśli wynik wygląda podobnie do powyższego wiersza, gratulacje — udało Ci się **wyodrębnić arabski tekst** z PNG!

## Pełny działający przykład

Poniżej znajduje się cały skrypt, gotowy do skopiowania‑wklejenia. Zamień `YOUR_DIRECTORY/arabic_doc.png` na ścieżkę do własnego pliku.

```python
import ocr
from ocr import Imaging

def main():
    # Create OCR engine
    ocr_engine = ocr.OcrEngine()
    
    # Set Arabic language
    ocr_engine.set_language("ar")
    
    # Load the PNG image
    image_path = "YOUR_DIRECTORY/arabic_doc.png"
    ocr_engine.set_image(Imaging.Image.load(image_path))
    
    # Recognize text
    ocr_result = ocr_engine.recognize()
    
    # Print the extracted Arabic text
    print(ocr_result.get_text())

if __name__ == "__main__":
    main()
```

Uruchom go poleceniem `python run_ocr.py` (lub jakąkolwiek nazwą nadałeś plikowi). Jeśli wszystko jest poprawnie zainstalowane, zobaczysz arabskie zdanie wydrukowane w konsoli.

## Jak uruchomić OCR na różnych formatach obrazów

Ten sam kod działa dla JPEG, TIFF lub BMP — wystarczy zmienić rozszerzenie pliku. Metoda `Image.load` automatycznie wykrywa format, więc możesz **przekształcić obraz w tekst** bez dodatkowego kodu.

```python
# Example for a JPEG file
ocr_engine.set_image(Imaging.Image.load("sample.jpg"))
```

Pamiętaj, że jakość obrazu źródłowego silnie wpływa na dokładność kroku **rozpoznawania arabskiego tekstu**. Obrazy o wysokiej rozdzielczości i niskiej kompresji dają najlepsze wyniki.

## Wyodrębnianie tekstu z PNG: wskazówki dla lepszej dokładności

1. **DPI ma znaczenie** – Celuj w co najmniej 300 dpi. Niższe DPI często prowadzi do pominięcia znaków.  
2. **Kontrast jest królem** – Użyj narzędzi przetwarzania obrazu (np. OpenCV), aby zwiększyć kontrast przed przekazaniem obrazu do silnika OCR.  
3. **Usuwanie szumów** – Małe plamki mogą mylić model; filtracja medianowa pomaga.  

Oto szybki fragment kodu używający Pillow do poprawy PNG przed OCR:

```python
from PIL import Image, ImageEnhance, ImageFilter

def preprocess_png(path):
    img = Image.open(path).convert("L")          # grayscale
    img = ImageEnhance.Contrast(img).enhance(2)  # boost contrast
    img = img.filter(ImageFilter.MedianFilter()) # denoise
    return img

# Use the preprocessed image
prepped = preprocess_png("arabic_doc.png")
ocr_engine.set_image(Imaging.Image.from_pil(prepped))
```

## Najczęściej zadawane pytania

**P: Czy to działa z innymi językami od prawej do lewej niż arabski?**  
O: Zdecydowanie. Wystarczy zmienić kod języka (`"ar"` → `"he"` dla hebrajskiego, `"fa"` dla perskiego) i silnik załaduje odpowiedni model.

**P: Co zrobić, jeśli muszę wyodrębnić tekst z wielu PNG w folderze?**  
O: Przejdź pętlą po plikach, używaj tej samej instancji `ocr_engine` i zbieraj wyniki w liście lub zapisz każdy do osobnego pliku `.txt`.

**P: Czy mogę uzyskać oceny pewności dla każdego słowa?**  
O: Tak. `ocr_result` często udostępnia metodę `get_confidences()`. Połącz każdą pewność z odpowiadającym słowem w celu kontroli jakości.

## Kolejne kroki

Teraz, gdy wiesz **jak uruchomić OCR** na arabskich PNG, rozważ następujące pomysły:

- **Przetwarzanie wsadowe:** Połącz skrypt z `os.listdir`, aby **wyodrębnić arabski tekst** z całego katalogu.  
- **Post‑processing:** Użyj bibliotek `arabic_reshaper` i `python-bidi`, aby poprawnie wyświetlać wynik od prawej do lewej w PDF‑ach.  
- **Integracja:** Przekaż wyodrębniony tekst do indeksu wyszukiwania (np. Elasticsearch), aby zeskanowane dokumenty były przeszukiwalne.  

Każdy z tych tematów opiera się na podstawach przedstawionych tutaj i pomoże przekształcić prosty skrypt **przekształcania obrazu w tekst** w gotowy do produkcji potok.

---

![how to run OCR on Arabic PNG](

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}