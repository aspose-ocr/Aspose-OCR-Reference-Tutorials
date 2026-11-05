---
category: general
date: 2026-03-18
description: Wykonaj OCR na obrazie i wyodrębnij odręczny tekst ze zdjęcia. Dowiedz
  się, jak przetworzyć odręczny obraz, wyodrębnić tekst z pliku JPG i rozpoznać tekst
  ze zdjęcia.
draft: false
keywords:
- perform OCR on image
- convert handwritten image
- extract text from jpg
- extract handwritten text
- recognize text from photo
language: pl
og_description: Wykonaj OCR na obrazie, aby wyodrębnić odręczny tekst ze zdjęcia.
  Ten poradnik pokazuje, jak przetworzyć odręczny obraz i rozpoznać tekst z plików
  JPG.
og_title: Wykonaj OCR na obrazie – Kompletny przewodnik po odręcznym tekście
tags:
- OCR
- Python
- Handwriting Recognition
title: Wykonaj OCR na obrazie – przekształć odręczny obraz w tekst
url: /pl/python/general/perform-ocr-on-image-convert-handwritten-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wykonaj OCR na obrazie – Pełnostackowe wyodrębnianie odręcznego tekstu

Kiedykolwiek potrzebowałeś **wykonać OCR na obrazie**, ale nie byłeś pewien, czy silnik poradzi sobie z niechlujnym pismem ręcznym? Nie jesteś sam. W wielu rzeczywistych aplikacjach — pomyśl o skanerach paragonów czy narzędziach do notatek — natrafisz na zdjęcia bazgrołów, które trzeba przekształcić w zwykły tekst.  

W tym przewodniku pokażemy, jak **konwertować odręczne obrazy**, **wyodrębniać tekst z jpg** i nawet **rozpoznawać tekst ze strumieni zdjęć** przy użyciu małej biblioteki w stylu Pythona o nazwie `ocr`. Po zakończeniu będziesz mieć gotowy skrypt, który wyciągnie każde słowo z odręcznej notatki, niezależnie od tego, jak drżące było pióro.

## Czego będziesz potrzebować

- Python 3.8+ (kod działa na każdym nowoczesnym interpreterze)
- Hipotetyczny pakiet `ocr` – zainstaluj go poleceniem `pip install ocr-lib` (zastąp rzeczywistą nazwą pakietu, którego używasz)
- Czytelne zdjęcie odręcznej notatki zapisane jako `note.jpg` (lub w innym formacie obrazu)
- Odrobina ciekawości — nie wymagana jest zaawansowana wiedza z zakresu ML

To wszystko. Bez zewnętrznych usług, bez kluczy API, tylko lokalny silnik, który może **wykonać OCR na obrazie**.

![perform OCR on image screenshot](example.png)

*Alt text: zrzut ekranu przedstawiający kod w edytorze z skryptem OCR.*

## Implementacja krok po kroku

Poniżej dzielimy proces na małe fragmenty. Każdy nagłówek zawiera słowo kluczowe, abyś mógł szybko przeglądać, a każdy blok wyjaśnia **dlaczego** robimy to, co robimy — nie tylko **co**.

### Krok 1: Zainstaluj i zweryfikuj bibliotekę OCR

Zanim będziesz mógł **wykonać OCR na obrazie**, biblioteka musi być dostępna w twoim środowisku. Otwórz terminal i uruchom:

```bash
pip install ocr-lib
```

> **Pro tip:** Jeśli pracujesz w wirtualnym środowisku (bardzo zalecane), najpierw je aktywuj. Dzięki temu twoje zależności będą uporządkowane i unikniesz konfliktów wersji.

Po instalacji upewnijmy się, że Python może zaimportować pakiet:

```python
try:
    import ocr
    print("OCR library loaded successfully.")
except ImportError as e:
    raise SystemExit("Failed to import ocr library. Did you run pip install?") from e
```

Jeśli zobaczysz komunikat o sukcesie, jesteś gotowy, aby **konwertować odręczne obrazy**.

### Krok 2: Utwórz instancję silnika i wybierz tryb odręczny

Większość silników OCR domyślnie rozpoznaje tekst drukowany. Ponieważ chcemy **wyodrębniać odręczny tekst**, musimy wyraźnie przełączyć tryb. Ten krok jest kluczowy, ponieważ odręczne pismo często wymaga innego przetwarzania wstępnego (np. wygładzania kresek).

```python
# Step 2: Initialize the OCR engine
engine = ocr.OcrEngine()

# Tell the engine we’re dealing with handwriting
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

print("Engine configured for handwritten recognition.")
```

*Dlaczego to ważne:* Znaki odręczne mogą znacznie różnić się rozmiarem i pochyleniem. Ustawiając `RecognitionMode.HANDWRITTEN`, silnik używa modelu wytrenowanego na próbkach pisma kursywnego, co drastycznie zwiększa dokładność.

### Krok 3: Załaduj zdjęcie, które chcesz przeanalizować

Teraz faktycznie **wykonujemy OCR na obrazie**. Metoda `load_image` przyjmuje ścieżkę lub obiekt podobny do pliku. Dla demonstracji załadujemy plik JPEG, ale to samo wywołanie działa dla PNG, BMP czy nawet stron PDF.

```python
# Step 3: Load the image file (replace the path with yours)
image_path = "YOUR_DIRECTORY/note.jpg"
engine.load_image(image_path)

print(f"Image '{image_path}' loaded into the OCR engine.")
```

Jeśli twój obraz znajduje się w chmurze, najpierw go pobierz lub przekaż strumień `BytesIO` — `ocr` jest na tyle elastyczny, że obsłuży oba przypadki.

### Krok 4: Uruchom proces rozpoznawania

Po przygotowaniu silnika i załadowaniu obrazu w pamięci, w końcu **wykonujemy OCR na obrazie** i pobieramy surowy tekst.

```python
# Step 4: Execute recognition
extracted_text = engine.recognize()

print("=== Extracted Text ===")
print(extracted_text)
```

Wywołanie `recognize()` zwraca zwykły ciąg Unicode. W większości przypadków możesz od razu zapisać go do pliku `.txt`, przekazać do potoku przetwarzania języka naturalnego lub wyświetlić w interfejsie GUI.

### Krok 5: Opcjonalnie – Oczyść lub poddaj wynik dalszemu przetwarzaniu

OCR odręczny nie jest doskonały; często pojawiają się niechciane podziały linii lub błędnie odczytane znaki. Szybki krok czyszczenia może poprawić wyniki w dalszych etapach.

```python
# Step 5: Simple post‑processing (optional)
def tidy(text):
    # Collapse multiple spaces, strip leading/trailing whitespace
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(extracted_text)

print("\n=== Cleaned Text ===")
print(clean_text)
```

Śmiało podłącz sprawdzacze pisowni, modele językowe lub własne wyrażenia regularne, zależnie od domeny.

### Pełny skrypt – Gotowy do skopiowania i wklejenia

Łącząc wszystko razem, oto kompletny, uruchamialny program, który **wyodrębnia odręczny tekst** z JPEG i wypisuje schludny rezultat.

```python
# -*- coding: utf-8 -*-
"""
Complete example: Perform OCR on image to extract handwritten text.
"""

# -------------------------------------------------
# Step 1: Import the OCR library and create an engine
# -------------------------------------------------
import ocr

engine = ocr.OcrEngine()

# -------------------------------------------------
# Step 2: Set the engine to recognize handwritten text
# -------------------------------------------------
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

# -------------------------------------------------
# Step 3: Load the image you want to analyze
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/note.jpg"   # <-- change this to your file
engine.load_image(image_path)

# -------------------------------------------------
# Step 4: Perform recognition and output the extracted text
# -------------------------------------------------
raw_text = engine.recognize()
print("=== Raw OCR Output ===")
print(raw_text)

# -------------------------------------------------
# Step 5: Optional cleanup for nicer display
# -------------------------------------------------
def tidy(text):
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(raw_text)
print("\n=== Cleaned OCR Output ===")
print(clean_text)
```

**Oczekiwany wynik** (twój rzeczywisty tekst będzie oczywiście inny):

```
=== Raw OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3

=== Cleaned OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3
```

Jeśli zobaczysz bełkot, sprawdź jakość obrazu (dobre oświetlenie, minimalne rozmycie) i upewnij się, że używasz trybu `HANDWRITTEN`. Te dwa czynniki odpowiadają za większość błędów rozpoznawania.

## Najczęściej zadawane pytania (FAQ)

| Pytanie | Odpowiedź |
|----------|-----------|
| **Czy mogę użyć tego do wyodrębniania tekstu z PNG?** | Oczywiście. `engine.load_image("scan.png")` działa tak samo. |
| **Co jeśli mój obraz jest stroną PDF?** | Najpierw skonwertuj stronę na obraz (np. przy pomocy `pdf2image`), a potem przekaż go silnikowi. |
| **Czy biblioteka jest bezpieczna wątkowo?** | Tak, możesz tworzyć osobne obiekty `OcrEngine` dla każdego wątku. |
| **Czym różni się to od `pytesseract`?** | `ocr` ukrywa binarkę Tesseract i zawiera wbudowany model odręczny, więc nie musisz instalować zewnętrznych plików wykonywalnych. |
| **Jak mogę **wyodrębniać tekst z JPG** w trybie masowym?** | Owiń skrypt w pętlę lub użyj `engine.load_image` dla każdego pliku i zbieraj wyniki w liście lub CSV. |

## Przypadki brzegowe i najlepsze praktyki

1. **Zdjęcia o niskim kontraście** – Zwiększ kontrast programowo przed załadowaniem lub użyj `engine.apply_preprocessing('contrast', level=2)`.
2. **Mieszane drukowane i odręczne** – Wykonaj dwa przebiegi: najpierw z `HANDWRITTEN`, potem z `PRINTED`, i połącz wyniki.
3. **Duże obrazy** – Zmniejsz rozdzielczość do ok. 1500 px szerokości; silniki OCR zazwyczaj działają szybciej przy mniejszych buforach, nie tracąc przy tym dokładności.
4. **Znaki Unicode** – Biblioteka zwraca ciągi UTF‑8, więc możesz obsługiwać emotikony, litery z akcentami czy symbole matematyczne od razu.

## Podsumowanie

Przeszliśmy razem przez konkretny przykład, jak **wykonać OCR na obrazie**, skupiając się na odręcznych notatkach. Instalując pakiet `ocr`, konfigurując silnik w trybie `HANDWRITTEN`, ładując zdjęcie i wywołując `recognize()`, możesz **konwertować odręczne obrazy** na czysty, przeszukiwalny tekst.  

Od tego momentu możesz **wyodrębniać tekst z jpg** w trybie masowym, podsyłać wynik do aplikacji do notatek lub połączyć go z syntezą mowy dla dostępności. Możliwości są nieograniczone, a powyższy kod daje solidną bazę do dalszych eksperymentów.

Masz własny pomysł — może inny format pliku lub ciekawy trik przetwarzania wstępnego? Dodaj komentarz i kontynuujmy dyskusję. Szczęśliwego kodowania i miłego przekształcania bazgrołów w cyfrowe złoto!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}