---
category: general
date: 2026-06-22
description: Rozpoznawaj tekst z plików PNG przy użyciu Aspose OCR w Pythonie. Naucz
  się przetwarzać obrazy OCR w trybie wsadowym i ustaw warstwy GPU dla szybkiego przetwarzania.
draft: false
keywords:
- recognize text from png
- batch ocr images
- set gpu layers
- Aspose OCR Python
- GPU acceleration OCR
language: pl
og_description: Rozpoznawaj tekst z plików PNG przy użyciu Aspose OCR w Pythonie.
  Ten przewodnik pokazuje, jak przetwarzać obrazy OCR w partiach i ustawiać warstwy
  GPU dla zwiększenia szybkości.
og_title: Rozpoznawanie tekstu z PNG – krok po kroku samouczek Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  headline: recognize text from png – Complete Guide with Aspose OCR & AI
  type: TechArticle
- description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  name: recognize text from png – Complete Guide with Aspose OCR & AI
  steps:
  - name: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
    text: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
  - name: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
    text: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
  - name: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
    text: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
  - name: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
    text: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
  type: HowTo
tags:
- OCR
- Python
- AsposeAI
title: Rozpoznawanie tekstu z PNG – Kompletny przewodnik z Aspose OCR i AI
url: /pl/python/general/recognize-text-from-png-complete-guide-with-aspose-ocr-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznawanie tekstu z png – pełny poradnik Aspose OCR i AI

Kiedykolwiek potrzebowałeś **rozpoznawać tekst z plików png**, ale utknąłeś w szczegółach konfiguracji? Nie jesteś sam. Niezależnie od tego, czy digitalizujesz paragony, skanujesz formularze, czy zamieniasz zrzuty ekranu w przeszukiwalny tekst, opanowanie batch OCR images w Pythonie może zaoszczędzić godziny pracy.  

W tym przewodniku przeprowadzimy Cię przez gotowy do uruchomienia przykład, który nie tylko **rozpoznaje tekst z png**, ale także pokazuje, jak **ustawić warstwy GPU** dla zauważalnego przyspieszenia. Po zakończeniu będziesz mieć samodzielny skrypt, jasne wyjaśnienie każdego kroku oraz kilka praktycznych wskazówek, które możesz skopiować i wkleić do własnych projektów.

## Co obejmuje ten tutorial

- Instalacja pakietów Aspose OCR i Aspose AI dla Pythona  
- Konfiguracja modelu AI z automatycznym pobraniem z Hugging Face  
- Tworzenie małego post‑processora, który naprawia najczęstsze literówki OCR  
- Uruchomienie pętli **batch OCR images** na całym folderze PNG‑ów  
- Użycie opcji **set GPU layers** w celu wykorzystania karty graficznej  
- Bezpieczne zwalnianie zasobów po przetworzeniu  

Bez zewnętrznych usług, bez ukrytej magii — po prostu czysty kod Pythona, który możesz wrzucić do pliku `.py` i uruchomić.

![Diagram of recognize text from png workflow](workflow.png){alt="diagram przepływu rozpoznawania tekstu z png"}

## Wymagania wstępne

| Wymaganie | Dlaczego jest ważne |
|-----------|---------------------|
| Python 3.8+ | Koła Aspose AI są przeznaczone dla nowoczesnych interpreterów |
| Kompatybilna z CUDA karta GPU (opcjonalnie) | Potrzebna, jeśli chcesz **ustawić warstwy GPU** dla przyspieszenia |
| Dostęp do Internetu przy pierwszym uruchomieniu | Model zostanie automatycznie pobrany z Hugging Face |
| Zainstalowany `pip` | Do pobrania pakietów Aspose |

Jeśli już masz te elementy, świetnie — możesz od razu zaczynać. Jeśli nie, poniższe kroki instalacyjne poprowadzą Cię przez brakujące elementy.

---

## Krok 1: Zainstaluj pakiety Aspose OCR i Aspose AI

Najpierw pobierz biblioteki z PyPI. Poniższe polecenie pobiera zarówno silnik OCR, jak i pomocnika AI jednocześnie.

```bash
pip install aspose-ocr aspose-ai
```

*Wskazówka:* Użyj wirtualnego środowiska (`python -m venv .venv`), aby pakiety były odizolowane od globalnej instalacji Pythona.

---

## Krok 2: Utwórz i skonfiguruj instancję Aspose AI

Komponent AI napędza „inteligentny” tryb silnika OCR. skierujemy go na model `Qwen/Qwen2.5-3B-Instruct-GGUF`, poprosimy o automatyczne pobranie w razie braku oraz **ustawimy warstwy GPU** na 30 (wartość możesz dostosować później).

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Initialize the AI wrapper
ai = AsposeAI()

# Build a model configuration
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",                     # Grab the model automatically
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # Smaller footprint, still accurate
    directory_model_path="YOUR_DIRECTORY/ai_models", # Where the model will live
    gpu_layers=30                                   # <-- set gpu layers for GPU acceleration
)

# Apply the configuration and spin up the model
ai.initialize(model_cfg)
```

**Dlaczego to ważne:**  
- `allow_auto_download` eliminuje ręczny krok pobierania ~2 GB modelu.  
- `gpu_layers=30` mówi podległemu transformerowi, aby pierwsze 30 warstw uruchomił na GPU, co znacząco skraca czas inferencji przy dostępnej karcie.  
- Kwantyzacja `int8` utrzymuje niskie zużycie pamięci bez dużej utraty dokładności.

---

## Krok 3: Zdefiniuj prosty post‑processor do czyszczenia błędów OCR

OCR nie jest doskonały — szczególnie przy niskiej rozdzielczości PNG‑ów. Szybkim rozwiązaniem jest zamiana znaków, które są często mylnie odczytywane. Poniższa funkcja zamienia „0” na „o” i „1” na „l”, co jest częstym wzorcem w zeskanowanych fakturach.

```python
def fix_common_errors(text, **_):
    """
    Post‑processor that corrects typical OCR mis‑recognitions.
    Feel free to extend this with regexes or custom dictionaries.
    """
    return text.replace("0", "o").replace("1", "l")
```

Podłączymy ją do instancji AI w następnym kroku, aby każdy wynik rozpoznawania przechodził automatycznie przez tę funkcję.

---

## Krok 4: Połącz post‑processor i silnik OCR

Teraz łączymy wszystko: silnik OCR, model AI oraz post‑processor.

```python
import ocr  # Aspose OCR module

# Attach the post‑processor
ai.set_post_processor(fix_common_errors, {})

# Spin up the OCR engine and bind the AI
engine = ocr.OcrEngine()
engine.set_ai(ai)
```

**Co się dzieje pod maską?**  
`OcrEngine` deleguje ciężką pracę na skonfigurowany model AI. Po zwróceniu surowego tekstu Aspose wywołuje `fix_common_errors`, aby uporządkować wynik przed jego wyświetleniem.

---

## Krok 5: Batch OCR Images – przetwarzaj każdy PNG w folderze

Oto serce tutorialu: pętla, która przechodzi po katalogu, ładuje każdy plik `.png`, wykonuje OCR i wypisuje wyczyszczony wynik. Ten wzorzec jest kanoniczny dla efektywnego **batch OCR images**.

```python
from pathlib import Path

# Replace with the folder that holds your PNG files
image_folder = Path("YOUR_DIRECTORY")

# Iterate over every PNG file in the folder
for img_path in image_folder.glob("*.png"):
    # Load the image into the engine
    engine.load_image(str(img_path))

    # Perform recognition
    result = engine.recognize()

    # Output the filename and the extracted text
    print(f"[{img_path.name}] → {result.text}")
```

**Oczekiwany wynik** (przykład dla paragonu):

```
[receipt_001.png] → Total amount: $23.45
[receipt_002.png] → Item: Coffee, Price: $3.50
```

Jeśli masz dziesiątki lub setki plików, pętla obsłuży je kolejno, ponownie używając tej samej instancji AI, aby uniknąć kosztów ponownego ładowania modelu.

---

## Krok 6: Czyszczenie – zwolnij zasoby i usuń silnik

Po zakończeniu warto zwolnić pamięć GPU oraz inne zasoby natywne. Aspose udostępnia do tego wyraźne metody.

```python
# Release the AI model and any GPU buffers
ai.free_resources()

# Dispose of the OCR engine to close native handles
engine.dispose()
```

Pominięcie tego kroku może pozostawić nieużywaną pamięć GPU, co może spowodować błędy „out‑of‑memory” przy następnym uruchomieniu skryptu.

---

## Bonus: Dostosowywanie warstw GPU do różnych konfiguracji sprzętowych

Wartość `gpu_layers`, którą ustawiłeś wcześniej, jest dobrym kompromisem dla wielu nowoczesnych GPU, ale możesz ją dostosować:

| Pamięć GPU (GB) | Zalecane `gpu_layers` |
|-----------------|-----------------------|
| ≤ 4 GB          | 10‑15                 |
| 6‑8 GB          | 20‑30                 |
| ≥ 12 GB         | 35‑45 (lub więcej)    |

Jeśli przekroczysz pamięć GPU, silnik automatycznie przełączy pozostałe warstwy na CPU, więc nie nastąpi awaria — jedynie spowolnienie. Eksperymentuj i monitoruj zużycie przy pomocy `nvidia‑smi`.

---

## Typowe pułapki i jak ich unikać

1. **Pobieranie modelu nie powiodło się** – Upewnij się, że środowisko ma dostęp do `https://huggingface.co`. W firmowym środowisku może być potrzebna konfiguracja proxy (`https_proxy` zmienna środowiskowa).  
2. **GPU nie wykryte** – Sprawdź, czy biblioteka `torch` (zainstalowana jako zależność) widzi GPU: `import torch; print(torch.cuda.is_available())`. Jeśli zwróci `False`, zainstaluj koło PyTorch kompatybilne z CUDA.  
3. **Nieprawidłowa ścieżka do obrazu** – `Path.glob("*.png")` jest wrażliwe na wielkość liter w Linuksie. Użyj `*.PNG` lub `*.png` odpowiednio, albo dodaj `pathlib.Path(...).rglob("*.[pP][nN][gG]")` dla bezpieczeństwa.  
4. **Post‑processor nadmiernie koryguje** – Prosta zamiana może zamienić prawdziwe „0” na „o”. Przetestuj na reprezentatywnej próbce i dostosuj logikę w razie potrzeby.

---

## Pełny działający przykład (gotowy do kopiowania)

```python
# recognize_text_from_png_batch.py
# -------------------------------------------------
# Author: Your Name
# Date:   2026‑06‑22
# -------------------------------------------------
from pathlib import Path
import ocr                      # Aspose OCR module
from aspose_ai import AsposeAI, AsposeAIModelConfig

# ----- Step 1: AI configuration -----
ai = AsposeAI()
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    directory_model_path="YOUR_DIRECTORY/ai_models",
    gpu_layers=30               # <-- set gpu layers
)
ai.initialize(model_cfg)

# ----- Step 2: Post‑processor -----
def fix_common_errors(text, **_):
    """Replace typical OCR mis‑reads."""
    return text.replace("0", "o").replace("1", "l")

ai.set_post_processor(fix_common_errors, {})

# ----- Step 3: OCR engine -----
engine = ocr.OcrEngine()
engine.set_ai(ai)

# ----- Step 4: Batch processing -----
image_folder = Path("YOUR_DIRECTORY")
for img_path in image_folder.glob("*.png"):
    engine.load_image(str(img_path))
    result = engine.recognize()
    print(f"[{img_path.name}] → {result.text}")

# ----- Step 5: Cleanup -----
ai.free_resources()
engine.dispose()
```

Uruchom go poleceniem:

```bash
python recognize_text_from_png_batch.py
```

Powinieneś zobaczyć nazwę każdego pliku PNG oraz wyodrębniony tekst, dokładnie tak jak pokazano wcześniej.

---

## Zakończenie

Przeszliśmy razem kompletny, gotowy do produkcji przepływ pracy, aby **rozpoznawać tekst z png** przy użyciu Aspose OCR i Aspose AI w Pythonie. Pakując kroki w przejrzysty skrypt, możesz bez trudu **batch OCR images**, a dzięki opcji `set gpu layers` uzyskać przyspieszenie.

## Co warto nauczyć się dalej?

Poniższe tutoriale obejmują tematy blisko powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne przykłady kodu oraz szczegółowe wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i eksplorować alternatywne podejścia w własnych projektach.

- [Jak przetwarzać obrazy OCR w partiach przy użyciu List w Aspose.OCR dla .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Wyodrębnianie tekstu z obrazów przy użyciu operacji OCR na folderach](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Jak wykonać OCR tekstu obrazu z wyborem języka przy użyciu Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}