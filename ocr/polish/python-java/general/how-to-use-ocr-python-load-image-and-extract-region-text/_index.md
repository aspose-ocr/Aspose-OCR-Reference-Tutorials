---
category: general
date: 2026-06-25
description: Jak używać OCR w Pythonie – dowiedz się, jak wczytać obraz do OCR, rozpoznać
  tekst w regionie i szybko wyodrębnić tekst z regionu.
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: pl
og_description: 'Jak korzystać z OCR w Pythonie – krok po kroku: wczytywanie obrazu,
  rozpoznawanie tekstu w określonym obszarze i wyodrębnianie numeru faktury.'
og_title: 'Jak używać OCR w Pythonie: załaduj obraz i wyodrębnij tekst z regionu'
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 'Jak używać OCR w Pythonie: wczytaj obraz i wyodrębnij tekst z regionu'
url: /pl/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać OCR w Pythonie: wczytaj obraz i wyodrębnij tekst z regionu

**Jak używać OCR w Pythonie** jest prostsze, niż myślisz. Czy zdarzyło Ci się patrzeć na zeskanowaną fakturę i zastanawiać się, jak wyciągnąć sam numer faktury, nie przetwarzając całej strony? Nie jesteś sam — wielu programistów napotyka ten problem, gdy po raz pierwszy zaczyna pracę z rozpoznawaniem znaków optycznych. W tym przewodniku przejdziemy przez wczytanie obrazu do OCR, zdefiniowanie prostokąta, rozpoznanie tekstu w tym regionie oraz wyodrębnienie tekstu z regionu. Po zakończeniu będziesz mieć gotowy do uruchomienia skrypt, który izoluje dowolny fragment tekstu, którego potrzebujesz.

> *Pro tip:* Jeśli pracujesz z plikami PDF, najpierw przekonwertuj każdą stronę na obraz — większość bibliotek OCR najlepiej radzi sobie z PNG/JPEG.

## Czego będziesz potrzebować

- Python 3.8+ (zalecana najnowsza stabilna wersja)  
- Biblioteka OCR udostępniająca klasę `OcrEngine` (np. **ocr** z `pip install ocr-lib`)  
- Przykładowy obraz — tutaj użyjemy `invoice.png` umieszczonego w folderze, którym zarządzasz  
- Podstawowa znajomość prostokątów (x, y, szerokość, wysokość)  

Brak ciężkich zależności, brak wymaganego GPU — tylko czysta praca na CPU, co zapewnia przenośność.

---

## Jak używać OCR: inicjalizacja silnika (Krok 1)

Zanim jakikolwiek tekst zostanie odczytany, potrzebujesz instancji silnika OCR. Pomyśl o niej jak o mózgu, który będzie analizował wzorce pikseli.

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Dlaczego to ważne:* Inicjalizacja silnika ładuje modele językowe i ustawia domyślne konfiguracje. Pominięcie tego kroku spowoduje wyjątek w momencie wywołania `recognize_region`.

---

## Wczytaj obraz do OCR (Krok 2)

Teraz, gdy silnik jest gotowy, podaj mu obraz. Metoda `Image.load` biblioteki obsługuje popularne formaty i normalizuje bitmapę.

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

Jeśli plik nie zostanie znaleziony, Python zgłosi `FileNotFoundError`. Upewnij się, że ścieżka jest absolutna lub względna względem katalogu roboczego skryptu.  

*Przypadek brzegowy:* Niektóre silniki OCR oczekują obrazu w odcieniach szarości. Jeśli zauważysz niską dokładność, najpierw skonwertuj obraz:

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

---

## Rozpoznaj tekst w regionie (Krok 3)

Definiowanie regionu to moment, w którym mówisz silnikowi, *gdzie* ma szukać. `Rectangle` przyjmuje wartości zmiennoprzecinkowe dla precyzji podpikselowej, co może się przydać przy skanach wysokiej rozdzielczości.

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – lewy górny róg prostokąta (w pikselach)  
- **width, height** – rozmiar prostokąta  

Możesz się zastanawiać, jak uzyskać te liczby. Szybki sposób to otworzyć obraz w dowolnym edytorze (np. GIMP lub Paint.NET) i użyć narzędzia zaznaczania, aby odczytać współrzędne.  

*Dlaczego nie po prostu OCR całej strony?* Ograniczenie obszaru zmniejsza szum, przyspiesza przetwarzanie i znacząco podnosi dokładność przy małych polach, takich jak numery faktur.

---

## Jak wyodrębnić tekst z regionu (Krok 4)

Po ustawieniu regionu poproś silnik o rozpoznanie tylko tego fragmentu. Obiekt wynikowy zawiera surowy tekst oraz współczynniki pewności.

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

Jeśli silnik OCR obsługuje wiele języków, możesz podać opcjonalny kod języka:

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*Typowy problem:* Niektóre silniki zwracają listę słów zamiast jednego łańcucha znaków. W takich przypadkach połącz je:

```python
text = " ".join(region_result.words)
```

---

## Wyświetl wyodrębniony numer faktury (Krok 5)

Na koniec wydrukuj — lub zapisz — wyodrębniony tekst. Możesz także poddać łańcuch dalszej obróbce, aby usunąć zbędne białe znaki lub znaki nienumeryczne.

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

Uruchomienie skryptu z prawidłowo ustawionym prostokątem powinno zwrócić coś w stylu:

```
Invoice number: 20231578
```

Jeśli otrzymujesz „śmieciowe” znaki, sprawdź ponownie współrzędne prostokąta lub rozważ zwiększenie rozdzielczości obrazu.

---

## Pełny działający przykład

Łącząc wszystko w całość, oto samodzielny skrypt, który możesz skopiować i uruchomić:

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

Zapisz plik jako `extract_invoice.py`, zamień `YOUR_DIRECTORY` na rzeczywistą ścieżkę folderu i uruchom:

```bash
python extract_invoice.py
```

Powinieneś zobaczyć numer faktury wypisany w konsoli.

---

## Najczęściej zadawane pytania

**P: Co zrobić, jeśli numer faktury jest wydrukowany ozdobną czcionką?**  
O: Większość nowoczesnych silników OCR radzi sobie z szeroką gamą czcionek, ale możesz zwiększyć dokładność, trenując własny model językowy lub wstępnie przetwarzając obraz (np. stosując filtr progowy).

**P: Czy mogę wyodrębnić wiele pól jednocześnie?**  
O: Oczywiście. Zdefiniuj listę obiektów `Rectangle` — po jednym dla każdego pola — i iteruj po nich, zapisując każdy wynik w słowniku.

**P: Czy to działa na wielostronicowych PDF‑ach?**  
O: Najpierw skonwertuj każdą stronę na obraz (przy użyciu `pdf2image` lub podobnego narzędzia), a następnie zastosuj tę samą ekstrakcję region‑based dla każdej strony.

---

## Podsumowanie

W tym samouczku omówiliśmy **jak używać OCR** w Pythonie, aby wczytać obraz, rozpoznać tekst w określonym regionie i wyodrębnić tekst z tego regionu — idealne rozwiązanie do pobierania numerów faktur, identyfikatorów zamówień lub dowolnych małych fragmentów danych ze zeskanowanych dokumentów. Izolując obszar zainteresowania zyskujesz szybkość, dokładność i mniejsze problemy z późniejszą obróbką.

Gotowy na kolejny krok? Spróbuj rozszerzyć skrypt, aby **wczytywać obrazy do OCR** z folderu z fakturami wsadowymi lub eksperymentuj z **rozpoznawaniem tekstu w regionie** dla innych pól, takich jak daty i sumy. Ten sam wzorzec się sprawdza — wystarczy zmienić współrzędne prostokąta.

Jeśli napotkasz jakiekolwiek trudności lub masz pomysły na ulepszenia, zostaw komentarz poniżej. Miłego kodowania i niech Twoje potoki OCR będą zawsze precyzyjne!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu oraz wyjaśnienia krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}