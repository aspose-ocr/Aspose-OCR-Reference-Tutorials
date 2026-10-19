---
category: general
date: 2026-04-26
description: Jak przetwarzać wyniki OCR i wyodrębniać tekst z współrzędnymi. Poznaj
  rozwiązanie krok po kroku, wykorzystujące strukturalny wynik i korektę AI.
draft: false
keywords:
- how to post‑process OCR
- extract text with coordinates
- OCR structured output
- AI post‑processing OCR
- bounding box OCR
language: pl
og_description: Jak przetwarzać wyniki OCR i wyodrębniać tekst z współrzędnymi. Skorzystaj
  z tego kompleksowego poradnika, aby uzyskać niezawodny przepływ pracy.
og_title: Jak przetwarzać wyniki OCR – Kompletny przewodnik
tags:
- OCR
- Python
- AI
- Text Extraction
title: Jak przetwarzać wyniki OCR – wyodrębnić tekst z współrzędnymi w Pythonie
url: /pl/python/general/how-to-post-process-ocr-extract-text-with-coordinates-in-pyt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak przetwarzać wyniki OCR – wyodrębnić tekst z współrzędnymi w Pythonie

Czy kiedykolwiek potrzebowałeś **jak przetwarzać OCR** wyniki, ponieważ surowe wyjście było zaszumione lub nie wyrównane? Nie jesteś jedyny. W wielu rzeczywistych projektach — skanowanie faktur, digitalizacja paragonów czy nawet wzbogacanie doświadczeń AR — silnik OCR zwraca surowe słowa, ale nadal musisz je oczyścić i śledzić, gdzie każde słowo znajduje się na stronie. To właśnie tryb strukturalnego wyjścia połączony z napędzanym AI post‑procesorem błyszczy.

> **Wskazówka:** Jeśli używasz innej biblioteki OCR, poszukaj trybu „structured” lub „layout”; koncepcje pozostają takie same.

---

## Wymagania wstępne

| Wymaganie | Dlaczego jest ważne |
|-------------|----------------|
| Python 3.9+ | Nowoczesna składnia i wskazówki typów |
| `ocr` library that supports `OutputMode.STRUCTURED` (e.g., a fictional `myocr`) | Wymagana do danych bounding‑box |
| An AI post‑processing module (could be OpenAI, HuggingFace, or a custom model) | Poprawia dokładność po OCR |
| An image file (`input.png`) in your working directory | Źródło, które odczytamy |

Jeśli któreś z nich jest nieznane, po prostu zainstaluj pakiety zastępcze za pomocą `pip install myocr ai‑postproc`. Poniższy kod zawiera również awaryjne stuby, abyś mógł przetestować przepływ bez rzeczywistych bibliotek.

---

## Krok 1: Włącz tryb strukturalnego wyjścia dla silnika OCR  

Pierwszą rzeczą, którą robimy, jest poinstruowanie silnika OCR, aby zwrócił nam więcej niż zwykły tekst. Strukturalne wyjście zwraca każde słowo wraz z jego ramką ograniczającą i wynikiem pewności, co jest niezbędne do **wyodrębniania tekstu z współrzędnymi** później.

```python
# step1_structured_output.py
import myocr as ocr  # fictional OCR library

# Initialize the engine (replace with your actual init code)
engine = ocr.Engine()

# Switch to structured mode – this makes the engine emit word‑level data
engine.set_output_mode(ocr.OutputMode.STRUCTURED)

print("✅ Structured output mode enabled")
```

*Dlaczego to ważne:* Bez trybu strukturalnego otrzymałbyś tylko długi ciąg znaków i straciłbyś informacje przestrzenne potrzebne do nakładania tekstu na obrazy lub przekazywania do dalszej analizy układu.

---

## Krok 2: Rozpoznaj obraz i przechwyć słowa, ramki i pewność  

Teraz wprowadzamy obraz do silnika. Wynikiem jest obiekt zawierający listę obiektów słów, z których każdy udostępnia `text`, `x`, `y`, `width`, `height` oraz `confidence`.

```python
# step2_recognize.py
from pathlib import Path

# Path to your image
image_path = Path("YOUR_DIRECTORY/input.png")

# Perform OCR – returns a StructuredResult with .words collection
structured_result = engine.recognize_image(str(image_path))

print(f"🔎 Detected {len(structured_result.words)} words")
```

*Przypadek brzegowy:* Jeśli obraz jest pusty lub nieczytelny, `structured_result.words` będzie pustą listą. Dobrą praktyką jest sprawdzenie tego i obsłużenie tego w sposób elegancki.

---

## Krok 3: Uruchom post‑procesing oparty na AI, zachowując pozycje  

Nawet najlepsze silniki OCR popełniają błędy — pomyśl o „O” vs. „0” lub brakujących diakrytykach. Model AI wytrenowany na tekście specyficznym dla domeny może skorygować te błędy. Co najważniejsze, zachowujemy oryginalne współrzędne, aby układ przestrzenny pozostał nienaruszony.

```python
# step3_ai_postprocess.py
import ai_postproc as ai  # placeholder for your AI module

# The AI post‑processor expects the structured result and returns a new one
corrected_result = ai.run_postprocessor(structured_result)

print("🤖 AI post‑processing complete")
```

*Dlaczego zachowujemy współrzędne:* Wiele zadań dalszych (np. generowanie PDF, etykietowanie AR) zależy od dokładnego rozmieszczenia. AI modyfikuje tylko pole `text`, pozostawiając `x`, `y`, `width`, `height` niezmienione.

---

## Krok 4: Iteruj po poprawionych słowach i wyświetl ich tekst z współrzędnymi  

Na koniec iterujemy po poprawionych słowach i drukujemy każde słowo wraz z jego lewym górnym rogiem `(x, y)`. Spełnia to cel **wyodrębniania tekstu z współrzędnymi**.

```python
# step4_display.py
for recognized_word in corrected_result.words:
    # Using f‑string for clean formatting
    print(f"{recognized_word.text} (x:{recognized_word.x}, y:{recognized_word.y})")
```

**Oczekiwany wynik (przykład):**

```
Invoice (x:45, y:112)
Number (x:120, y:112)
12345 (x:190, y:112)
Total (x:45, y:250)
$ (x:120, y:250)
199.99 (x:130, y:250)
```

Każda linia pokazuje poprawione słowo i jego dokładną lokalizację na oryginalnym obrazie.

---

## Pełny działający przykład  

Poniżej znajduje się pojedynczy skrypt, który łączy wszystko razem. Możesz go skopiować‑wkleić, dostosować instrukcje importu do swoich rzeczywistych bibliotek i uruchomić bezpośrednio.

```python
# ocr_postprocess_demo.py
"""
Complete demo: how to post‑process OCR and extract text with coordinates.
Works with any OCR library exposing a structured output mode and an AI post‑processor.
"""

import sys
from pathlib import Path

# ----------------------------------------------------------------------
# 1️⃣ Imports – replace these with your real packages
# ----------------------------------------------------------------------
try:
    import myocr as ocr               # OCR engine with structured output
    import ai_postproc as ai          # AI correction module
except ImportError:  # Fallback stubs for quick testing
    class DummyWord:
        def __init__(self, text, x, y, w, h, conf):
            self.text = text
            self.x = x
            self.y = y
            self.width = w
            self.height = h
            self.confidence = conf

    class DummyResult:
        def __init__(self, words):
            self.words = words

    class StubEngine:
        class OutputMode:
            STRUCTURED = "structured"

        def set_output_mode(self, mode):
            print(f"[Stub] set_output_mode({mode})")

        def recognize_image(self, path):
            # Very simple fake OCR output
            sample = [
                DummyWord("Invoice", 45, 112, 60, 20, 0.98),
                DummyWord("Number", 120, 112, 55, 20, 0.96),
                DummyWord("12345", 190, 112, 40, 20, 0.97),
                DummyWord("Total", 45, 250, 50, 20, 0.99),
                DummyWord("$", 120, 250, 10, 20, 0.95),
                DummyWord("199.99", 130, 250, 55, 20, 0.94),
            ]
            return DummyResult(sample)

    class StubAI:
        @staticmethod
        def run_postprocessor(structured_result):
            # Pretend we corrected "12345" to "12346"
            for w in structured_result.words:
                if w.text == "12345":
                    w.text = "12346"
            return structured_result

    engine = StubEngine()
    ai = StubAI

# ----------------------------------------------------------------------
# 2️⃣ Enable structured output
# ----------------------------------------------------------------------
engine.set_output_mode(ocr.Engine.OutputMode.STRUCTURED)

# ----------------------------------------------------------------------
# 3️⃣ Recognize image
# ----------------------------------------------------------------------
image_path = Path("YOUR_DIRECTORY/input.png")
if not image_path.is_file():
    print(f"⚠️  Image not found at {image_path}. Using stub data.")
structured_result = engine.recognize_image(str(image_path))

# ----------------------------------------------------------------------
# 4️⃣ AI post‑processing
# ----------------------------------------------------------------------
corrected_result = ai.run_postprocessor(structured_result)

# ----------------------------------------------------------------------
# 5️⃣ Display results
# ----------------------------------------------------------------------
print("\n🗒️  Final OCR output with coordinates:")
for word in corrected_result.words:
    print(f"{word.text} (x:{word.x}, y:{word.y})")
```

**Uruchamianie skryptu**

```bash
python ocr_postprocess_demo.py
```

Jeśli masz zainstalowane rzeczywiste biblioteki, skrypt przetworzy twój `input.png`. W przeciwnym razie implementacja stub pozwoli zobaczyć oczekiwany przepływ i wynik bez żadnych zewnętrznych zależności.

---

## Najczęściej zadawane pytania (FAQ)

| Pytanie | Odpowiedź |
|----------|--------|
| *Czy to działa z Tesseract?* | Sam Tesseract nie udostępnia trybu strukturalnego od razu, ale wrappery takie jak `pytesseract.image_to_data` zwracają ramki ograniczające, które możesz przekazać do tego samego post‑procesora AI. |
| *Co jeśli potrzebuję prawego dolnego rogu zamiast lewego górnego?* | Każdy obiekt słowa udostępnia również `width` i `height`. Oblicz `x2 = x + width` i `y2 = y + height`, aby uzyskać przeciwległy róg. |
| *Czy mogę przetwarzać wiele obrazów wsadowo?* | Oczywiście. Owiń kroki w pętli `for image_path in Path("folder").glob("*.png"):` i zbieraj wyniki dla każdego pliku. |
| *Jak wybrać model AI do korekcji?* | Do ogólnego tekstu działa mały GPT‑2 dostrojony na błędy OCR. Do danych specyficznych dla domeny (np. recept medycznych) wytrenuj model sekwencja‑do‑sekwencji na sparowanych danych zaszumionych‑czystych. |
| *Czy wynik pewności jest przydatny po korekcji AI?* | Możesz nadal zachować oryginalną pewność do debugowania, ale AI może zwrócić własny wynik pewności, jeśli model to obsługuje. |

## Przypadki brzegowe i najlepsze praktyki  

1. **Puste lub uszkodzone obrazy** – zawsze weryfikuj, że `structured_result.words` nie jest pusty przed kontynuacją.  
2. **Skrypty niełacińskie** – upewnij się, że silnik OCR jest skonfigurowany na docelowy język; post‑procesor AI musi być wytrenowany na tym samym skrypcie.  
3. **Wydajność** – korekcja AI może być kosztowna. Buforuj wyniki, jeśli będziesz ponownie używać tego samego obrazu, lub uruchom krok AI asynchronicznie.  
4. **System współrzędnych** – biblioteki OCR mogą używać różnych początków (lewy górny vs. lewy dolny). Dostosuj odpowiednio przy nakładaniu na PDF‑y lub płótna.  

## Podsumowanie  

Masz teraz solidny, kompleksowy przepis na **jak przetwarzać OCR** i niezawodne **wyodrębnianie tekstu z współrzędnymi**. Dzięki włączeniu strukturalnego wyjścia, przekazaniu wyniku przez warstwę korekcji AI i zachowaniu oryginalnych ramek ograniczających, możesz przekształcić zaszumione skany OCR w czysty, świadomy przestrzennie tekst gotowy do dalszych zadań, takich jak generowanie PDF, automatyzacja wprowadzania danych czy nakładki rzeczywistości rozszerzonej.

Gotowy na kolejny krok? Spróbuj zamienić stub AI na wywołanie OpenAI `gpt‑4o‑mini`, lub zintegrować pipeline z FastAPI

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}