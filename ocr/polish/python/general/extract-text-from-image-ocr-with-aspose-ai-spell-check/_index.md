---
category: general
date: 2026-05-03
description: wyodrębniaj tekst z obrazu przy użyciu Aspose OCR i AI spell‑check. Dowiedz
  się, jak wykonać OCR obrazu, załadować obraz do OCR, rozpoznać tekst z faktury i
  zwolnić zasoby GPU.
draft: false
keywords:
- extract text from image
- how to ocr image
- load image for ocr
- release gpu resources
- recognize text from invoice
language: pl
og_description: wyodrębnij tekst z obrazu za pomocą Aspose OCR i AI spell‑check. Przewodnik
  krok po kroku opisujący, jak wykonać OCR obrazu, załadować obraz do OCR i zwolnić
  zasoby GPU.
og_title: wyodrębnianie tekstu z obrazu – Kompletny przewodnik po OCR i sprawdzaniu
  pisowni
tags:
- OCR
- Aspose
- AI
- Python
title: wyodrębnij tekst z obrazu – OCR z Aspose AI Spell‑Check
url: /pl/python/general/extract-text-from-image-ocr-with-aspose-ai-spell-check/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnianie tekstu z obrazu – Kompletny przewodnik OCR i sprawdzania pisowni

Czy kiedykolwiek potrzebowałeś **wyodrębnić tekst z obrazu**, ale nie byłeś pewien, która biblioteka zapewni zarówno szybkość, jak i dokładność? Nie jesteś jedyny. W wielu rzeczywistych projektach — myśl o przetwarzaniu faktur, digitalizacji paragonów lub skanowaniu umów — uzyskanie czystego, przeszukiwalnego tekstu z obrazu jest pierwszą przeszkodą.

Dobrą wiadomością jest to, że Aspose OCR w połączeniu z lekkim modelem Aspose AI może wykonać to zadanie w kilku linijkach Pythona. W tym samouczku przeprowadzimy Cię przez **jak wykonać OCR obrazu**, załadujemy obraz poprawnie, uruchomimy wbudowany procesor sprawdzania pisowni i w końcu **zwolnić zasoby GPU**, aby Twoja aplikacja była przyjazna dla pamięci.

Po zakończeniu tego przewodnika będziesz w stanie **rozpoznawać tekst z faktur** obrazów, automatycznie korygować typowe błędy OCR i utrzymać swój GPU w czystości dla kolejnej partii.

---

## Czego będziesz potrzebować

- Python 3.9 lub nowszy (kod używa podpowiedzi typów, ale działa także w starszych wersjach 3.x)
- pakiety `aspose-ocr` i `aspose-ai` (instaluj za pomocą `pip install aspose-ocr aspose-ai`)
- GPU z obsługą CUDA jest opcjonalny; skrypt przełączy się na CPU, jeśli nie zostanie wykryty.
- Przykładowy obraz, np. `sample_invoice.png`, umieszczony w folderze, do którego możesz odwołać się.

Brak ciężkich frameworków ML, brak ogromnych pobrań modeli — tylko mały, kwantowany model Q4‑K‑M, który wygodnie mieści się na większości GPU.

---

## Krok 1: Inicjalizacja silnika OCR – wyodrębnianie tekstu z obrazu

Pierwszą rzeczą, którą robisz, jest stworzenie instancji `OcrEngine` i określenie, jakiego języka oczekujesz. Tutaj wybieramy angielski i żądamy wyjścia w formacie plain‑text, co jest idealne do dalszego przetwarzania.

```python
import aocr  # Aspose OCR package
import aspose.ai as ai  # Aspose AI package

# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
ocr_engine.language = aocr.Language.English            # Choose any supported language
ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Plain text makes post‑processing easier
```

**Dlaczego to ważne:** Ustawienie języka ogranicza zestaw znaków, zwiększając dokładność. Tryb plain‑text usuwa informacje o układzie, które zazwyczaj nie są potrzebne, gdy chcesz po prostu wyodrębnić tekst z obrazu.

---

## Krok 2: Ładowanie obrazu do OCR – jak wykonać OCR obrazu

Teraz podajemy silnikowi rzeczywisty obraz. Pomocnicza funkcja `Image.load` obsługuje popularne formaty (PNG, JPEG, TIFF) i ukrywa szczegóły związane z operacjami we/wy.

```python
# Load the input image – this is the "load image for OCR" step
input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize(input_image)  # Returns the recognised text as a string
```

**Wskazówka:** Jeśli Twoje obrazy źródłowe są duże, rozważ ich zmniejszenie przed przekazaniem do silnika; mniejsze wymiary mogą zmniejszyć zużycie pamięci GPU, nie wpływając negatywnie na jakość rozpoznawania.

---

## Krok 3: Konfiguracja modelu Aspose AI – rozpoznawanie tekstu z faktury

Aspose AI dostarcza mały model GGUF, który można automatycznie pobrać. Przykład używa repozytorium `Qwen2.5‑3B‑Instruct‑GGUF`, kwantowanego do `q4_k_m`. Dodatkowo informujemy środowisko wykonawcze, aby przydzieliło 20 warstw na GPU, co równoważy szybkość i zużycie VRAM.

```python
# Model configuration – auto‑download a small Q4‑K‑M quantised model
model_config = ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "q4_k_m"
model_config.gpu_layers = 20  # Use 20 GPU layers when a GPU is available
```

**Za kulisami:** Kwantowany model zajmuje około 1,5 GB na dysku, co jest ułamkiem pełnoprecyzyjnego modelu, a mimo to zachowuje wystarczającą subtelność językową, aby wykrywać typowe błędy OCR.

---

## Krok 4: Inicjalizacja AsposeAI i podłączenie procesora sprawdzania pisowni

Aspose AI zawiera gotowy procesor sprawdzania pisowni. Po podłączeniu, każdy wynik OCR zostanie automatycznie oczyszczony.

```python
# Initialise AsposeAI and attach the built‑in spell‑check post‑processor
ocr_ai = ai.AsposeAI(model_config)  # Pass the config we just built
ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})  # Empty dict → default settings
```

**Dlaczego używać procesora post‑processingowego?** Silniki OCR często mylą „Invoice” z „Invo1ce” lub „Total” z „T0tal”. Sprawdzanie pisowni uruchamia lekki model językowy na surowym ciągu znaków i koryguje te błędy, bez konieczności tworzenia własnego słownika.

---

## Krok 5: Uruchomienie procesora sprawdzania pisowni na wyniku OCR

Po podłączeniu wszystkiego, jedno wywołanie zwraca poprawiony tekst. Drukujemy także zarówno oryginalną, jak i oczyszczoną wersję, abyś mógł zobaczyć różnicę.

```python
# Run the spell‑check post‑processor on the OCR result
corrected_text = ocr_ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Corrected:", corrected_text)
```

Typowy wynik dla faktury może wyglądać tak:

```
Original : Invo1ce #12345
Date: 2023/07/15
Total: $1,250.00
...
Corrected: Invoice #12345
Date: 2023/07/15
Total: $1,250.00
...
```

Zauważ, że „Invo1ce” zamieniło się w poprawne słowo „Invoice”. To moc wbudowanego sprawdzania pisowni AI.

---

## Krok 6: Zwolnienie zasobów GPU – bezpieczne zwalnianie zasobów GPU

Jeśli uruchamiasz to w długotrwałej usłudze (np. w API webowym przetwarzającym dziesiątki faktur na minutę), musisz zwolnić kontekst GPU po każdej partii. W przeciwnym razie pojawią się wycieki pamięci i w końcu błędy „CUDA out of memory”.

```python
# Release GPU resources – crucial to avoid memory leaks
ocr_ai.free_resources()
```

**Pro tip:** Wywołaj `free_resources()` wewnątrz bloku `finally` lub menedżera kontekstu, aby zawsze się wykonał, nawet w przypadku wystąpienia wyjątku.

---

## Pełny działający przykład

Połączenie wszystkich elementów daje Ci samodzielny skrypt, który możesz wkleić do dowolnego projektu.

```python
# extract_text_from_image.py
import aocr
import aspose.ai as ai

def main():
    # Step 1: Initialise OCR engine
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain

    # Step 2: Load image for OCR
    input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
    raw_text = ocr_engine.recognize(input_image)

    # Step 3: Configure Aspose AI model
    model_cfg = ai.AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 20

    # Step 4: Initialise AI and attach spell‑check
    ocr_ai = ai.AsposeAI(model_cfg)
    ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})

    # Step 5: Run spell‑check
    corrected_text = ocr_ai.run_postprocessor(raw_text)

    print("Original :", raw_text)
    print("Corrected:", corrected_text)

    # Step 6: Release GPU resources
    ocr_ai.free_resources()

if __name__ == "__main__":
    main()
```

Zapisz plik, dostosuj ścieżkę do swojego obrazu i uruchom `python extract_text_from_image.py`. Powinieneś zobaczyć wyczyszczony tekst faktury wypisany w konsoli.

---

## Najczęściej zadawane pytania (FAQ)

**Q: Czy to działa na maszynach tylko z CPU?**  
A: Zdecydowanie tak. Jeśli nie wykryto GPU, Aspose AI przełącza się na wykonanie na CPU, choć będzie wolniejsze. Możesz wymusić CPU, ustawiając `model_cfg.gpu_layers = 0`.

**Q: Co jeśli moje faktury są w języku innym niż angielski?**  
A: Zmień `ocr_engine.language` na odpowiednią wartość wyliczeniową (np. `aocr.Language.Spanish`). Model sprawdzania pisowni jest wielojęzyczny, ale możesz uzyskać lepsze wyniki przy modelu specyficznym dla języka.

**Q: Czy mogę przetwarzać wiele obrazów w pętli?**  
A: Tak. Po prostu przenieś kroki ładowania, rozpoznawania i post‑processingu do pętli `for`. Pamiętaj, aby wywołać `ocr_ai.free_resources()` po pętli lub po każdej partii, jeśli ponownie używasz tej samej instancji AI.

**Q: Jak duży jest rozmiar pobieranego modelu?**  
A: Około 1,5 GB dla wersji kwantowanej `q4_k_m`. Jest buforowany po pierwszym uruchomieniu, więc kolejne wykonania są natychmiastowe.

---

## Podsumowanie

W tym samouczku pokazaliśmy, jak **wyodrębnić tekst z obrazu** przy użyciu Aspose OCR, skonfigurować mały model AI, zastosować procesor sprawdzania pisowni i bezpiecznie **zwolnić zasoby GPU**. Przepływ pracy obejmuje wszystko, od ładowania obrazu po sprzątanie po sobie, zapewniając niezawodny pipeline dla scenariuszy **rozpoznawania tekstu z faktur**.

Kolejne kroki? Spróbuj zamienić sprawdzanie pisowni na własny model ekstrakcji encji

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}