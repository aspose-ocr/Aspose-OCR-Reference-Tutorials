---
category: general
date: 2026-03-28
description: Dowiedz się, jak uruchomić OCR na obrazie, automatycznie pobrać model
  Hugging Face, oczyścić tekst OCR i skonfigurować model LLM w Pythonie przy użyciu
  Aspose OCR Cloud.
draft: false
keywords:
- run OCR on image
- download hugging face model
- clean OCR text
- configure LLM model
language: pl
og_description: Uruchom OCR na obrazie i oczyść wynik przy użyciu automatycznie pobranego
  modelu Hugging Face. Ten przewodnik pokazuje, jak skonfigurować model LLM w Pythonie.
og_title: Uruchom OCR na obrazie – Kompletny samouczek Aspose OCR Cloud
tags:
- OCR
- Python
- LLM
- HuggingFace
title: Uruchom OCR na obrazie przy użyciu Aspose OCR Cloud – Kompletny przewodnik
  krok po kroku
url: /pl/python/general/run-ocr-on-image-with-aspose-ocr-cloud-full-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uruchom OCR na obrazie – Kompletny samouczek Aspose OCR Cloud

Czy kiedykolwiek musiałeś wykonać OCR na plikach graficznych, a surowy wynik wyglądał jak nieuporządkowany bałagan? Z mojego doświadczenia największym problemem nie jest samo rozpoznawanie – to czyszczenie. Na szczęście Aspose OCR Cloud pozwala podłączyć post‑procesor LLM, który może *automatycznie wyczyścić tekst OCR*. W tym samouczku przeprowadzimy Cię przez wszystko, czego potrzebujesz: od **pobrania modelu z Hugging Face** po skonfigurowanie LLM, uruchomienie silnika OCR i ostateczne wypolerowanie wyniku.

Po zakończeniu tego przewodnika będziesz mieć gotowy do uruchomienia skrypt, który:

1. Pobiera kompaktowy model Qwen 2.5 z Hugging Face (automatycznie pobierany dla Ciebie).  
2. Konfiguruje model tak, aby część sieci działała na GPU, a reszta na CPU.  
3. Wykonuje silnik OCR na obrazie odręcznej notatki.  
4. Używa LLM do wyczyszczenia rozpoznanego tekstu, dając wynik czytelny dla człowieka.

> **Wymagania wstępne** – Python 3.8+, pakiet `asposeocrcloud`, GPU z co najmniej 4 GB VRAM (opcjonalnie, ale zalecane) oraz połączenie internetowe do pierwszego pobrania modelu.

---

## Czego będziesz potrzebować

- **Aspose OCR Cloud SDK** – zainstaluj za pomocą `pip install asposeocrcloud`.  
- **Przykładowy obraz** – np. `handwritten_note.jpg` umieszczony w lokalnym folderze.  
- **Wsparcie GPU** – jeśli masz GPU obsługujące CUDA, skrypt przeniesie 30 warstw na GPU; w przeciwnym razie automatycznie przełączy się na CPU.  
- **Uprawnienia do zapisu** – skrypt buforuje model w `YOUR_DIRECTORY`; upewnij się, że folder istnieje.

---

## Krok 1 – Skonfiguruj model LLM (pobierz model z Hugging Face)

Pierwszą rzeczą, którą robimy, jest poinformowanie Aspose AI, skąd pobrać model. Klasa `AsposeAIModelConfig` obsługuje automatyczne pobieranie, kwantyzację i przydział warstw GPU.

```python
import asposeocrcloud as ocr
from asposeocrcloud.ai import AsposeAI, AsposeAIModelConfig

# ----------------------------------------------------------------------
# Step 1: Model configuration – this will download the model if it’s missing
# ----------------------------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                           # Enables auto‑download
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF", # Repo on Hugging Face
    hugging_face_quantization="int8",                     # Small footprint, fast inference
    gpu_layers=30,                                        # 30 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY"               # Cache folder (optional)
)
```

**Dlaczego to ważne** – Kwantyzacja do `int8` dramatycznie zmniejsza zużycie pamięci (≈ 4 GB vs 12 GB). Podzielenie modelu między GPU a CPU pozwala uruchomić LLM o 3 miliardach parametrów nawet na skromnym RTX 3060. Jeśli nie masz GPU, ustaw `gpu_layers=0`, a SDK utrzyma wszystko na CPU.

> **Wskazówka:** Pierwsze uruchomienie pobierze ~ 1,5 GB, więc daj mu kilka minut i stabilne połączenie.

---

## Krok 2 – Zainicjalizuj silnik AI z konfiguracją modelu

Teraz uruchamiamy silnik Aspose AI i przekazujemy mu właśnie stworzoną konfigurację.

```python
# ----------------------------------------------------------------------
# Step 2: Initialise the AI engine – pulls the model if needed
# ----------------------------------------------------------------------
ocr_ai = AsposeAI()
ocr_ai.initialize(model_config)  # This call blocks until the model is ready
```

**Co się dzieje pod maską?** SDK sprawdza `directory_model_path` pod kątem istniejącego modelu. Jeśli znajdzie pasującą wersję, ładuje ją natychmiast; w przeciwnym razie pobiera plik GGUF z Hugging Face, rozpakowuje go i przygotowuje pipeline inferencyjny.

---

## Krok 3 – Utwórz silnik OCR i podłącz post‑procesor AI

Silnik OCR wykonuje ciężką pracę rozpoznawania znaków. Podłączając `ocr_ai.run_postprocessor`, włączamy **czyszczenie tekstu OCR** automatycznie po rozpoznaniu.

```python
# ----------------------------------------------------------------------
# Step 3: Build the OCR engine and bind the LLM post‑processor
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=None)
```

**Dlaczego używać post‑procesora?** Surowy OCR często zawiera nieprawidłowe podziały linii, błędnie wykryte znaki interpunkcyjne lub zbędne symbole. LLM może przekształcić wynik w poprawne zdania, skorygować pisownię i nawet domyślić się brakujących słów – w praktyce zamienia surowy zrzut w dopracowaną prozę.

---

## Krok 4 – Uruchom OCR na pliku obrazu

Po podłączeniu wszystkiego, czas przekazać obraz do silnika.

```python
# ----------------------------------------------------------------------
# Step 4: Load the image and run OCR
# ----------------------------------------------------------------------
input_image = ocr.Image.load(r"YOUR_DIRECTORY/handwritten_note.jpg")
raw_result = ocr_engine.recognize(input_image)   # Returns an OcrResult object
```

**Przypadek brzegowy:** Jeśli obraz jest duży (> 5 MP), warto go najpierw zmniejszyć, aby przyspieszyć przetwarzanie. SDK przyjmuje obiekt Pillow `Image`, więc możesz wstępnie przetworzyć go metodą `PIL.Image.thumbnail()` w razie potrzeby.

---

## Krok 5 – Niech AI wyczyści rozpoznany tekst i pokaż obie wersje

Na koniec wywołujemy wcześniej podłączony post‑procesor. Ten krok ilustruje kontrast między *przed* a *po* czyszczeniu.

```python
# ----------------------------------------------------------------------
# Step 5: Clean the OCR output using the LLM and display both results
# ----------------------------------------------------------------------
cleaned_result = ocr_engine.run_postprocessor(raw_result)

print("=== Before AI ===")
print(raw_result.text)

print("\n=== After AI ===")
print(cleaned_result.text)
```

### Oczekiwany wynik

```
=== Before AI ===
Th1s 1s a h@ndwr1tt3n n0te.  It c0nta1ns m1st@k3s, l1n3 br3aks, & sp3c!@l ch@r@ct3rs.

=== After AI ===
This is a handwritten note. It contains mistakes, line breaks, and special characters.
```

Zauważ, jak LLM:

- Naprawił typowe błędy OCR (`Th1s` → `This`).  
- Usunął zbędne symbole (`&` → `and`).  
- Znormalizował podziały linii do poprawnych zdań.

---

## 🎨 Przegląd wizualny (Workflow „Uruchom OCR na obrazie”)

![Run OCR on image workflow](run_ocr_on_image_workflow.png "Diagram showing the run OCR on image pipeline from model download to cleaned output")

Diagram powyżej podsumowuje cały pipeline: **pobranie modelu z Hugging Face → konfiguracja LLM → inicjalizacja AI → silnik OCR → post‑procesor AI → czysty tekst OCR**.

---

## Często zadawane pytania i pro tipy

### Co zrobić, jeśli nie mam GPU?

Ustaw `gpu_layers=0` w `AsposeAIModelConfig`. Model będzie działał w pełni na CPU, co jest wolniejsze, ale wciąż funkcjonalne. Możesz także przejść na mniejszy model (np. `Qwen/Qwen2.5-1.5B‑Instruct‑GGUF`), aby utrzymać rozsądny czas inferencji.

### Jak zmienić model później?

Po prostu zaktualizuj `hugging_face_repo_id` i ponownie uruchom `ocr_ai.initialize(model_config)`. SDK wykryje zmianę wersji, pobierze nowy model i zastąpi zbuforowane pliki.

### Czy mogę dostosować prompt post‑procesora?

Tak. Przekaż słownik do `custom_settings` z kluczem `prompt_template`. Przykład:

```python
custom_prompt = {
    "prompt_template": "Correct the following OCR text and keep line breaks:\n{ocr_text}"
}
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=custom_prompt)
```

### Czy powinienem zapisać wyczyszczony tekst do pliku?

Zdecydowanie. Po czyszczeniu możesz zapisać wynik do pliku `.txt` lub `.json` do dalszego przetwarzania:

```python
with open("cleaned_note.txt", "w", encoding="utf-8") as f:
    f.write(cleaned_result.text)
```

---

## Zakończenie

Pokazaliśmy, jak **uruchomić OCR na obrazach** przy użyciu Aspose OCR Cloud, automatycznie **pobrać model z Hugging Face**, precyzyjnie **skonfigurować ustawienia modelu LLM** i w końcu **wyczyścić tekst OCR** za pomocą potężnego post‑procesora LLM. Cały proces mieści się w jednym, łatwym do uruchomienia skrypcie Pythona i działa zarówno na maszynach z GPU, jak i wyłącznie na CPU.

Jeśli ten pipeline Ci odpowiada, rozważ eksperymenty z:

- **Różnymi LLM** – wypróbuj `meta-llama/Meta-Llama-3-8B‑Instruct‑GGUF` dla większego okna kontekstowego.  
- **Przetwarzaniem wsadowym** – iteruj po folderze obrazów i agreguj wyczyszczone wyniki do CSV.  
- **Niestandardowymi promptami** – dostosuj AI do swojej dziedziny (dokumenty prawne, notatki medyczne itp.).

Śmiało modyfikuj wartość `gpu_layers`, wymieniaj model lub podłącz własny prompt. Niebo jest granicą, a kod, który masz teraz, to dopiero start.

Miłego kodowania i niech Twoje wyniki OCR będą zawsze czyste! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}