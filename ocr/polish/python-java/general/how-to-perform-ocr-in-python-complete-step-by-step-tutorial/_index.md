---
category: general
date: 2026-03-26
description: Dowiedz się, jak wykonać OCR w Pythonie i rozpoznawać tekst z plików
  graficznych. Ten przewodnik pokazuje, jak wyodrębnić tekst z plików PNG i szybko
  przekształcić obraz w tekst.
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: pl
og_description: Jak wykonać OCR w Pythonie? Skorzystaj z tego przewodnika, aby rozpoznać
  tekst z obrazu, wyodrębnić tekst z pliku PNG i przekształcić obraz w tekst przy
  użyciu licencji próbnej.
og_title: Jak wykonać OCR w Pythonie – Kompletny poradnik
tags:
- OCR
- Python
- Image Processing
title: Jak wykonać OCR w Pythonie – Kompletny samouczek krok po kroku
url: /pl/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonać OCR w Pythonie – Kompletny przewodnik krok po kroku  

Zastanawiałeś się kiedyś **jak wykonać OCR** na zdjęciu, które właśnie zrobiłeś telefonem? Nie jesteś sam — programiści na całym świecie potrzebują niezawodnego sposobu rozpoznawania tekstu z plików graficznych, bez konieczności walki z złożonymi natywnymi bibliotekami.  

W tym samouczku przeprowadzimy praktyczny przykład, który pokazuje **jak wykonać OCR**, **rozpoznawać tekst z obrazu** oraz **wyodrębniać tekst z PNG** przy użyciu lekkiego wrappera w Pythonie. Po zakończeniu będziesz w stanie **konwertować obraz na tekst** w kilku linijkach kodu i nie będziesz musiał martwić się problemami z licencjonowaniem, ponieważ użyjemy wbudowanego trybu próbnego.  

## Czego się nauczysz  

* Jak skonfigurować licencję próbną dla silnika OCR (bez podawania ścieżki do pliku).  
* Dokładna kolejność wywołań do obiektów **recognize text from image**.  
* Sposoby **extract text from PNG** oraz radzenie sobie z typowymi problemami, takimi jak brak czcionek.  
* Wskazówki dotyczące skalowania rozwiązania przy przejściu z licencji próbnej na produkcyjną.  

**Wymagania wstępne** – potrzebujesz Pythona 3.8+ oraz pakietu `ocr` (instalowalnego poleceniem `pip install ocr`). Nie są wymagane żadne inne zewnętrzne narzędzia.  

---  

![przykład wykonania OCR](https://example.com/ocr-demo.png "jak wykonać OCR w Pythonie – wyświetlony rozpoznany tekst")  

*Tekst alternatywny obrazu: jak wykonać OCR w Pythonie – przykładowy wynik*  

## Krok 1 – Aktywacja licencji próbnej (bez podawania ścieżki do pliku)  

Zanim silnik będzie mógł cokolwiek odczytać, potrzebuje ważnej licencji. Tryb próbny jest idealny do eksperymentów i małych projektów.  

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*Dlaczego to ważne:* Obiekt licencji informuje bibliotekę OCR, że działasz w środowisku sandbox. Jeśli pominiesz ten krok, silnik zgłosi `LicenseError` w momencie wywołania `recognize()`.  

**Wskazówka:** Gdy przejdziesz na płatną licencję, zamień powyższe dwie linie na `ocr.License("path/to/your/license.key").apply()`.  

## Krok 2 – Utworzenie instancji silnika OCR  

Teraz, gdy licencja próbna jest aktywna, tworzymy główny silnik. Pomyśl o nim jak o „mózgu”, który przyjrzy się obrazowi i zdecyduje, jakie znaki znajdują się w którym miejscu.  

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*Dlaczego to ważne:* `OcrEngine` przechowuje konfigurację, taką jak pakiety językowe i ustawienia DPI. Możesz je później dostosować, ale domyślne ustawienia działają dla większości PNG‑ów zawierających tylko język angielski.  

## Krok 3 – Załaduj PNG, który chcesz przetworzyć  

Tutaj **rozpoznajemy tekst z obrazu**. Metoda `ocr.Imaging.Image.load()` obsługuje PNG, JPEG, BMP i kilka innych formatów.  

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*Przypadek brzegowy:* Jeśli Twój PNG używa palety indeksowanej (co jest częste w zrzutach ekranu), loader automatycznie przekształci go do 24‑bitowego bufora RGB. Ta konwersja może nieznacznie wpłynąć na wydajność, ale zapewnia dokładne wyniki OCR.  

## Krok 4 – Uruchom OCR i pobierz tekst  

Na koniec prosimy silnik, aby wykonał swoją pracę, a następnie pobieramy wynik w postaci zwykłego tekstu.  

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**Oczekiwany wynik** (przykład dla prostego obrazu zawierającego „Hello World”):  

```
Hello World
```

Jeśli obraz zawiera wiele linii, wynik zachowa podziały wierszy, co ułatwia przekazywanie go do dalszych procesów, takich jak parsowanie CSV czy potoki NLP.  

## Opcjonalnie: Dostosowanie w celu uzyskania lepszej dokładności  

* **Pakiety językowe:** `ocr_engine.set_language("eng")` (domyślnie) lub `"fra"` dla francuskiego.  
* **Skalowanie DPI:** `ocr_engine.set_dpi(300)` może poprawić wyniki przy skanach o niskiej rozdzielczości.  
* **Pre‑przetwarzanie:** Zastosowanie progowania binarnego (`ocr.Imaging.Image.threshold()`) przed `set_image` często daje czystszy tekst na zaszumionym tle.  

Te drobne zmiany są przydatne, gdy przechodzisz od szybkiej demonstracji do produkcyjnego **ocr tutorial python**, który przetwarza setki plików dziennie.  

## Pełny skrypt – gotowy do kopiowania i wklejania  

Poniżej znajduje się kompletny, gotowy do uruchomienia skrypt, który łączy wszystkie powyższe kroki. Zapisz go jako `run_ocr.py` i zamień `YOUR_DIRECTORY/sample1.png` na ścieżkę do własnego pliku PNG.  

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

Uruchom go z wiersza poleceń:  

```bash
python run_ocr.py
```

Powinieneś zobaczyć wyodrębniony tekst wypisany w konsoli. Jeśli otrzymasz pusty ciąg, sprawdź ponownie, czy obraz rzeczywiście zawiera wyraźny, wysokokontrastowy tekst oraz czy licencja próbna została zastosowana bez błędów.  

## Częste pytania i pułapki  

* **„Czy to działa z JPEG?”** – Zdecydowanie tak. Metoda `load()` automatycznie wykrywa format, więc możesz zamienić PNG na JPEG bez zmian w kodzie.  
* **„Co jeśli obraz jest obrócony?”** – Silnik może automatycznie wykrywać orientację, ale dla najlepszych rezultatów możesz wstępnie obrócić go przy pomocy `input_image.rotate(90)` przed `set_image`.  
* **„Czy mogę przetwarzać wiele obrazów w pętli?”** – Tak. Po prostu przenieś wywołania ładowania i `recognize()` do pętli `for`; ta sama instancja `ocr_engine` może być ponownie użyta, co oszczędza niewielką ilość narzutu.  

## Kolejne kroki – od demonstracji do produkcji  

Teraz, gdy wiesz **jak wykonać OCR**, rozważ następujące tematy uzupełniające:  

* **Przetwarzanie wsadowe** – Połącz ten skrypt z `os.listdir()`, aby **wyodrębnić tekst z PNG** w trybie masowym.  
* **Integracja z PDF** – Użyj `pdf2image` do konwersji stron PDF na PNG, a następnie podaj je do tego samego potoku.  
* **Post‑przetwarzanie** – Zastosuj wyrażenia regularne lub dopasowanie rozmyte, aby oczyścić typowe błędy rozpoznawania OCR (np. „0” vs „O”).  

Każdy z nich opiera się na podstawowej idei **konwertowania obrazu na tekst** i zwiększa przydatność Twojego przepływu pracy OCR.  

---  

### TL;DR  

Omówiliśmy wszystko, co musisz wiedzieć, aby **jak wykonać OCR** w Pythonie: aktywować licencję próbną, utworzyć silnik, załadować PNG, uruchomić rozpoznawanie i wydrukować wynik. Dzięki kilku linijkom kodu możesz **rozpoznawać tekst z obrazu**, **wyodrębniać tekst z PNG** i **konwertować obraz na tekst** dla dowolnej aplikacji downstream.  

Spróbuj, dostosuj ustawienia DPI lub języka i pozwól silnikowi wykonać ciężką pracę. Szczęśliwego kodowania!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}