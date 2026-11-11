---
category: general
date: 2026-03-18
description: Darmowe zasoby AI pozwalają wyodrębniać tekst z obrazów PNG przy użyciu
  Aspose OCR w Pythonie. Dowiedz się, jak pobrać model z Hugging Face i oczyścić wyniki.
draft: false
keywords:
- free ai resources
- how to extract text
- download hugging face model
- recognize text from png
- aspose ocr python
language: pl
og_description: Darmowe zasoby AI pozwalają wyodrębniać tekst z obrazów PNG przy użyciu
  Aspose OCR w Pythonie. Dowiedz się, jak pobrać model z Hugging Face i oczyścić wyniki.
og_title: 'Darmowe zasoby AI: OCR tekstu z PNG przy użyciu Aspose Python'
tags:
- OCR
- Python
- AI
title: 'Darmowe zasoby AI: OCR tekstu z PNG przy użyciu Aspose Python'
url: /pl/python/general/free-ai-resources-ocr-text-from-png-using-aspose-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Darmowe zasoby AI: Tekst OCR z PNG przy użyciu Aspose Python

Zastanawiałeś się kiedyś, jak wyodrębnić tekst z pliku PNG bez płacenia za usługę w chmurze? **Darmowe zasoby AI** umożliwiają to, a przy użyciu Aspose OCR Python możesz zrobić to lokalnie w kilku linijkach. W tym przewodniku przeprowadzimy Cię przez cały proces — rozpoznanie tekstu z PNG, pobranie modelu z Hugging Face i zwolnienie zasobów AI po zakończeniu.

Omówimy wszystko, co musisz wiedzieć: wymagane pakiety, kod krok po kroku, dlaczego każdy element jest ważny oraz kilka wskazówek, których nie znajdziesz w oficjalnej dokumentacji. Po zakończeniu będziesz mieć gotowy do uruchomienia skrypt, który zamieni dowolny obraz na czysty, sprawdzony pod kątem pisowni tekst.

## Co będziesz potrzebować

- **Python 3.9+** – kod używa podpowiedzi typów, ale działa również na wcześniejszych wersjach 3.x.  
- **Aspose.OCR for Python** (`pip install aspose-ocr`) – podstawowy silnik OCR.  
- **Internet access** przy pierwszym uruchomieniu skryptu – pobiera model z Hugging Face.  
- **GPU** (opcjonalnie) – ustawimy `gpu_layers=20`, aby model działał szybciej, jeśli masz CUDA.

Brak płatnej subskrypcji, brak ukrytych opłat — tylko darmowe zasoby AI, które kontrolujesz sam.

---

![Ilustracja darmowych zasobów AI pokazująca laptop przetwarzający obraz PNG](/images/free-ai-resources.png "Darmowe zasoby AI")

## Darmowe zasoby AI: użycie Aspose OCR Python

Ta sekcja pokazuje przepływ na wysokim poziomie. Pomyśl o tym jak o przepisie: ładujesz obraz, prosisz Aspose o rozpoznanie surowych znaków, przekazujesz te znaki modelowi AI, który je oczyszcza, a następnie zwalniasz zasoby. **Głównym celem** jest pokazanie, jak wyodrębnić tekst z PNG, zachowując wszystko lokalnie.

### Krok 1: Jak wyodrębnić tekst z obrazu PNG

Aspose OCR zajmuje się ciężką pracą konwersji piksel‑do‑znaku. Metoda `recognize()` zwraca zwykły tekst, który często jest zaszumiony (brak spacji, błędne litery). Poniżej znajduje się minimalny kod, aby uzyskać ten surowy wynik.

```python
import aspose.ocr as ocr

# Load the image you want to process
ocr_engine = ocr.OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/input.png")

# Run OCR – this is where we recognize text from PNG
raw_text = ocr_engine.recognize()          # plain text output
print("🔎 Raw OCR output:")
print(raw_text)
```

**Dlaczego to jest ważne:**  
- `load_image` obsługuje PNG, JPEG, TIFF i wiele innych formatów — więc „rozpoznanie tekstu z PNG” to tylko jeden przypadek użycia.  
- Surowy ciąg często zawiera błędy ortograficzne, przerwane podziały linii i zbędne symbole; dlatego potrzebny jest post‑processor.

#### Szybka wskazówka
Jeśli Twój PNG zawiera dużo szumu, wywołaj `ocr_engine.preprocess_image()` przed `recognize()`. Może to zwiększyć dokładność bez dodatkowych kosztów.

### Krok 2: Pobranie modelu Hugging Face do post‑przetwarzania AI

Aspose udostępnia cienką warstwę wokół dowolnego modelu Hugging Face. W naszym przykładzie pobieramy **Qwen/Qwen2.5-3B-Instruct‑GGUF** z kwantyzacją int8 — mały rozmiar, który nadal zapewnia solidne sprawdzanie pisowni i korektę gramatyki.

```python
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",   # small footprint, ideal for free AI resources
    gpu_layers=20                       # use GPU if available, otherwise fall back to CPU
)

# The model is downloaded automatically on first run
ai_helper = AsposeAI(model_cfg)

# Enable the built‑in spell‑check post‑processor
ai_helper.set_post_processor("spellcheck")
print("✅ Model downloaded and post‑processor configured.")
```

**Dlaczego pobieramy model:**  
- Model dodaje rozumienie kontekstowe, którego brakuje czystemu OCR.  
- Korzystanie z **darmowego zasobu AI**, takiego jak otwarto‑źródłowy model GGUF, oznacza, że omijasz kosztowne API.  
- Kwantyzacja `int8` zmniejsza zużycie RAM do poniżej 4 GB, co jest przyjazne dla większości laptopów.

#### Pro wskazówka
Jeśli używasz maszyny tylko z CPU, ustaw `gpu_layers=0`. Kod nadal będzie działał; po prostu nie będzie tak szybki.

### Krok 3: Zastosowanie post‑procesora do oczyszczenia wyniku OCR

Teraz podajemy surowy ciąg do modelu AI. Metoda `run_postprocessor()` zwraca oczyszczoną wersję — błędy ortograficzne są naprawiane, brakujące spacje dodawane, a tekst staje się gotowy do dalszych zadań.

```python
# Clean the OCR result with the AI post‑processor
cleaned_text = ai_helper.run_postprocessor(raw_text)

print("\n✨ Cleaned OCR output:")
print(cleaned_text)
```

**Co zobaczysz:**  
- „Ths is a smple txt” → „This is a simple text”  
- „2023/09/01” pozostaje niezmienione, ponieważ model szanuje liczby.

### Krok 4: Zwolnienie darmowych zasobów AI po zakończeniu

Po zakończeniu wywołaj `free_resources()`, aby zwolnić model z pamięci i zamknąć wszelki kontekst GPU. Zapomnienie tego kroku może pozostawić niezwolnioną pamięć GPU, co jest częstym problemem dla programistów nowych w inferencji AI.

```python
# Free up memory and GPU resources
ai_helper.free_resources()
print("\n🧹 Resources released – your free AI resources are back to idle.")
```

### Typowe pułapki i przypadki brzegowe

| Problem | Dlaczego się pojawia | Rozwiązanie |
|------|----------------|-----|
| **Zawieszanie się pobierania modelu** | Przekroczenie limitu czasu sieci lub zapora blokuje CDN Hugging Face. | Użyj VPN lub pobierz model ręcznie (`git lfs pull`) i wskaż `AsposeAIModelConfig` na lokalną ścieżkę. |
| **GPU brak pamięci** | `gpu_layers` jest zbyt wysokie dla Twojej karty. | Zmniejsz `gpu_layers` do 10 lub ustaw na 0 dla wyłącznie CPU. |
| **Zbędne znaki** | PNG zawiera przezroczyste tło, które myli OCR. | Wykonaj wstępne przetwarzanie za pomocą `ocr_engine.preprocess_image()` lub najpierw skonwertuj PNG do BMP. |
| **Sprawdzanie pisowni usuwa terminy specyficzne dla domeny** | Wbudowany post‑processor nie zna Twojego żargonu. | Podaj własny słownik za pomocą `ai_helper.set_custom_vocab(["MyProduct", "XYZ123"])`. |

### Pełny działający przykład

Łącząc wszystko razem, oto pojedynczy skrypt, który możesz skopiować i uruchomić. Zakłada, że masz zainstalowany `aspose-ocr` oraz PNG pod nazwą `input.png`.

```python
import aspose.ocr as ocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

def main():
    # -------------------------------------------------
    # Step 1: Load image and run OCR (recognize text from PNG)
    # -------------------------------------------------
    engine = ocr.OcrEngine()
    engine.load_image("input.png")
    raw = engine.recognize()
    print("🔎 Raw OCR output:")
    print(raw)

    # -------------------------------------------------
    # Step 2: Download and configure the Hugging Face model
    # -------------------------------------------------
    cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20
    )
    ai = AsposeAI(cfg)
    ai.set_post_processor("spellcheck")
    print("\n✅ Model ready for post‑processing.")

    # -------------------------------------------------
    # Step 3: Clean the OCR result
    # -------------------------------------------------
    cleaned = ai.run_postprocessor(raw)
    print("\n✨ Cleaned OCR output:")
    print(cleaned)

    # -------------------------------------------------
    # Step 4: Release free AI resources
    # -------------------------------------------------
    ai.free_resources()
    print("\n🧹 All resources freed.")

if __name__ == "__main__":
    main()
```

**Oczekiwany wynik (przykład):**

```
🔎 Raw OCR output:
Ths is a smple txt frm a png img.

✅ Model ready for post‑processing.

✨ Cleaned OCR output:
This is a simple text from a PNG image.

🧹 All resources freed.
```

Zauważ, jak fraza „recognize text from PNG” staje się całkowicie czytelna po przetworzeniu przez AI post‑processor.

## Kolejne kroki: Rozszerzanie potoku

- **Przetwarzanie wsadowe:** Przejdź przez folder z PNG, zbieraj wyniki w pliku CSV.  
- **Niestandardowe post‑procesory:** Zamień `"spellcheck"` na `"summarize"`, aby uzyskać jednowierszowe podsumowanie każdego obrazu.  
- **Integracja z FastAPI:** Udostępnij endpoint OCR jako mikro‑serwis, nadal używając wyłącznie darmowych zasobów AI.  

Jeśli jesteś ciekawy, **jak wyodrębnić tekst** z PDF‑ów zamiast PNG

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}