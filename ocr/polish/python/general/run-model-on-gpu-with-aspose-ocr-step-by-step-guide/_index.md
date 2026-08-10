---
category: general
date: 2026-03-26
description: Uruchom model na GPU przy użyciu Aspose OCR. Dowiedz się, jak pobrać
  repozytorium Hugging Face, ustawić warstwy GPU, zaimportować Aspose OCR i w ciągu
  kilku minut załadować model Qwen2.5.
draft: false
keywords:
- run model on gpu
- download hugging face repo
- import aspose ocr
- set gpu layers
- load qwen2.5 model
language: pl
og_description: Uruchom model na GPU z Aspose OCR. Ten samouczek pokazuje, jak pobrać
  repozytorium Hugging Face, ustawić warstwy GPU, zaimportować Aspose OCR i wczytać
  model Qwen2.5.
og_title: Uruchom model na GPU z Aspose OCR – Kompletny przewodnik
tags:
- Aspose OCR
- GPU acceleration
- Hugging Face
- Python AI
title: Uruchom model na GPU z Aspose OCR – Przewodnik krok po kroku
url: /pl/python/general/run-model-on-gpu-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uruchom model na GPU z Aspose OCR – Pełny samouczek

Zastanawiałeś się kiedyś, jak **uruchomić model na GPU** bez walki z niskopoziomowym kodem CUDA? Nie jesteś sam. Wielu programistów napotyka problem, gdy muszą przyspieszyć duży model językowy, ale wciąż chcą prostoty biblioteki wysokiego poziomu. Dobra wiadomość? Aspose OCR dostarcza łatwy w użyciu silnik AI, który może pobrać model bezpośrednio z Hugging Face, go kwantyzować i przenieść pierwszą tuzin warstw na Twój GPU — wszystko w kilku linijkach Pythona.

W tym przewodniku przejdziemy przez cały proces: **pobranie repozytorium Hugging Face**, **import Aspose OCR**, konfigurację **warstw GPU**, a na końcu **załadowanie modelu Qwen2.5**. Po zakończeniu będziesz mieć gotowy silnik OCR działający już na karcie graficznej i zrozumiesz, dlaczego każde ustawienie ma znaczenie.

## Czego będziesz potrzebować

- Python 3.9 lub nowszy (kod używa podpowiedzi typów i f‑stringów)
- GPU kompatybilny z CUDA (opcjonalny, ale zalecany dla wydajności)
- Dostęp do Internetu, aby pobrać model z Hugging Face
- Pakiet `asposeocr` (`pip install asposeocr`)  

Nie są wymagane żadne inne zewnętrzne zależności — Aspose OCR zajmuje się ciężką pracą za Ciebie.

## Krok 1: Pobierz repozytorium Hugging Face i zaimportuj Aspose OCR

Pierwszą rzeczą, którą musisz zrobić, jest upewnienie się, że pliki modelu są dostępne lokalnie. `AsposeAIModelConfig` z Aspose OCR może automatycznie pobrać repozytorium z Hugging Face, więc nie musisz ręcznie klonować niczego.

```python
# Step 1: Import the Aspose OCR package
import asposeocr as ocr
from asposeocr import AsposeAI, AsposeAIModelConfig
```

**Dlaczego to ważne:** Importowanie pakietu daje dostęp do klasy `AsposeAI`, która opakowuje podstawowy model transformer. Obiekt `AsposeAIModelConfig` to miejsce, w którym określasz *gdzie* pobrać model i *jak* go traktować (np. kwantyzacja, przydział GPU).

> **Pro tip:** Jeśli pracujesz za proxy korporacyjnym, ustaw zmienną środowiskową `HTTPS_PROXY` przed uruchomieniem skryptu — Aspose OCR respektuje standardowe ustawienia proxy w Pythonie.

## Krok 2: Ustaw warstwy GPU dla optymalnej wydajności

Uruchamianie modelu na GPU nie jest prostym przełącznikiem „włącz/wyłącz”. Możesz zdecydować, ile wczesnych warstw transformera ma pozostać na GPU, a reszta ma wrócić do CPU. To hybrydowe podejście jest przydatne, gdy pamięć GPU jest ograniczona.

```python
# Step 2: Define the model configuration
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # automatically pull repo if missing
    hugging_face_repo_id="bartowski/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # int8 reduces memory footprint
    gpu_layers=20                                   # first 20 layers run on GPU
)
```

**Dlaczego 20 warstw?** Model Qwen2.5‑3B ma 32 bloki transformera. Przydzielenie pierwszych 20 do GPU zapewnia solidny przyrost prędkości, jednocześnie utrzymując zużycie pamięci pod kontrolą na karcie 12 GB. Śmiało dostosuj `gpu_layers` do swojego sprzętu — ustawienie `0` wymusza wyłącznie CPU, a `32` próbuje zmieścić wszystko na GPU (co może spowodować OOM na słabszych kartach).

## Krok 3: Utwórz silnik AI i załaduj model Qwen2.5

Teraz tworzymy silnik i przekazujemy mu skonfigurowany wcześniej obiekt. Jawne wywołanie `initialize` jest opcjonalne — Aspose OCR zainicjalizuje się leniwie przy pierwszym użyciu — ale wywołanie go od razu czyni sprawdzenie gotowości jaśniejszym.

```python
# Step 3: Create and initialize the AI engine with the configuration
ocr_engine = AsposeAI()
ocr_engine.initialize(model_config)   # explicit call for clarity
```

**Co się dzieje pod maską?**  
1. Aspose OCR kontaktuje się z Hugging Face, pobiera plik GGUF (jeśli nie jest w pamięci podręcznej).  
2. Plik jest konwertowany do formatu zrozumiałego przez wewnętrzny runtime.  
3. Pierwsze `gpu_layers` bloki są przenoszone do pamięci CUDA; reszta pozostaje na CPU.  
4. Silnik oznacza się jako *zainicjalizowany*, co możesz sprawdzić metodą `is_initialized()`.

## Krok 4: Zweryfikuj, że model jest gotowy do działania na GPU

Krótka kontrola sanityzująca chroni przed niejasnymi błędami w czasie działania. Metoda `is_initialized()` zwraca wartość Boolean, pozwalając potwierdzić, że pobranie, konwersja i przydział GPU zakończyły się sukcesem.

```python
# Step 4: Confirm that the engine is ready
print("AI ready:", ocr_engine.is_initialized())
```

Gdy wszystko pójdzie gładko, powinieneś zobaczyć:

```
AI ready: True
```

Jeśli otrzymasz `False`, sprawdź, czy sterowniki CUDA są aktualne i czy GPU ma wystarczająco wolnej pamięci dla 20 warstw, które zażądałeś.

## Opcjonalnie: Uruchom szybkie wnioskowanie OCR, aby zobaczyć GPU w akcji

Choć głównym celem tego samouczka jest załadowanie modelu, większość czytelników wkrótce zechce faktycznie wykonać OCR. Oto minimalny przykład, który przetwarza lokalny obraz (`sample.png`) i wypisuje wykryty tekst.

```python
# Optional: Perform a single OCR inference
image_path = "sample.png"
result = ocr_engine.recognize_image(image_path)

print("Detected text:")
print(result.text)
```

**Dlaczego uruchomić to teraz?** Ponieważ pierwsze wnioskowanie często wyzwala JIT‑kompilację kerneli CUDA. Jeśli zmierzysz wywołanie przy pomocy `time.perf_counter()`, zauważysz, że drugi przebieg jest dramatycznie szybszy — wyraźny znak, że model naprawdę działa na GPU.

## Typowe pułapki i jak je naprawić

| Objaw | Prawdopodobna przyczyna | Rozwiązanie |
|-------|--------------------------|-------------|
| `RuntimeError: CUDA out of memory` | `gpu_layers` ustawione zbyt wysoko dla Twojej karty | Zmniejsz `gpu_layers` (np. do 12) lub przełącz się na kwantyzację `int8` (już zastosowaną). |
| `OSError: Unable to download repository` | Brak internetu lub blokada proxy | Ustaw zmienne środowiskowe `HTTPS_PROXY`/`HTTP_PROXY` lub pobierz plik GGUF ręcznie i wskaż `hugging_face_repo_id` na lokalną ścieżkę. |
| `AttributeError: 'AsposeAI' object has no attribute 'recognize_image'` | Używasz starszej wersji `asposeocr` | Zaktualizuj pakiet poleceniem `pip install --upgrade asposeocr`. |
| `False` z `is_initialized()` | Niekompatybilność sterownika CUDA | Sprawdź, czy `nvidia-smi` pokazuje wersję sterownika zgodną z Twoim zestawem narzędzi CUDA. |

## Wizualne podsumowanie

![Run model on GPU diagram](run-model-on-gpu.png "Diagram pokazujący pobieranie modelu, przydział warstw GPU i przepływ wnioskowania")

*Alt text:* *diagram uruchamiania modelu na GPU ilustrujący pobieranie repozytorium Hugging Face, ustawianie warstw GPU oraz wykonywanie modelu Qwen2.5 przy użyciu Aspose OCR.*

## Podsumowanie – Co osiągnęliśmy

- **Zaimportowaliśmy Aspose OCR** oraz jego klasy pomocnicze AI.  
- **Automatycznie pobraliśmy repozytorium Hugging Face**, dzięki `allow_auto_download`.  
- **Ustawiliśmy warstwy GPU** (`gpu_layers=20`), aby przenieść najbardziej obciążające części obliczeniowe na kartę graficzną.  
- **Załadowaliśmy model Qwen2.5‑3B‑Instruct** z kwantyzacją int8, znacząco zmniejszając zużycie pamięci.  
- **Zweryfikowaliśmy**, że silnik jest gotowy (`is_initialized()` zwraca `True`).  

Wszystko to odbyło się w mniej niż 30 linijkach Pythona — bez potrzeby pisania własnych kerneli CUDA.

## Kolejne kroki i powiązane tematy

1. **Eksperymentuj z różnymi kwantyzacjami** (`float16`, `bfloat16`), aby zobaczyć kompromis między prędkością a dokładnością.  
2. **Skaluj do większych modeli** (np. Qwen2.5‑7B), dostosowując `gpu_layers` i upewniając się, że masz wystarczająco VRAM.  
3. **Przetwarzanie wsadowe OCR**: przekaż listę ścieżek do obrazów do `ocr_engine.recognize_images()` w celu zwiększenia przepustowości.  
4. **Integracja z FastAPI** w celu udostępnienia endpointu REST, który wykonuje OCR na przychodzących plikach — idealne rozwiązanie dla mikroserwisów.  

Jeśli interesuje Cię bardziej zaawansowane tunowanie GPU, zajrzyj do oficjalnego przewodnika wydajności Aspose OCR lub dokumentacji CUDA Toolkit, gdzie znajdziesz zmienne środowiskowe takie jak `CUDA_VISIBLE_DEVICES`.

---

*Miłego kodowania! Jeśli ten samouczek pomógł Ci uruchomić model na GPU, daj znać w komentarzach lub podziel się własnymi modyfikacjami. Im więcej eksperymentujemy razem, tym szybciej społeczność się uczy.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}