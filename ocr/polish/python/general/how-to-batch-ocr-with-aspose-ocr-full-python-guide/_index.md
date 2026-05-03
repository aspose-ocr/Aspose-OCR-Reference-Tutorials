---
category: general
date: 2026-05-03
description: Jak przetwarzać obrazy metodą OCR w trybie wsadowym przy użyciu Aspose
  OCR i AI sprawdzania pisowni. Dowiedz się, jak wyodrębniać tekst z obrazów, stosować
  sprawdzanie pisowni, korzystać z darmowych zasobów AI i korygować błędy OCR.
draft: false
keywords:
- how to batch ocr
- extract text from images
- free ai resources
- apply spell check
- correct ocr errors
language: pl
og_description: Jak przetwarzać obrazy OCR wsadowo przy użyciu Aspose OCR i AI sprawdzania
  pisowni. Postępuj zgodnie z przewodnikiem krok po kroku, aby wyodrębnić tekst z
  obrazów, zastosować sprawdzanie pisowni, korzystać z darmowych zasobów AI i poprawić
  błędy OCR.
og_title: Jak wykonywać OCR wsadowo przy użyciu Aspose OCR – Kompletny samouczek w
  Pythonie
tags:
- OCR
- Python
- AI
- Aspose
title: Jak przeprowadzić wsadowe OCR przy użyciu Aspose OCR – Pełny przewodnik w Pythonie
url: /pl/python/general/how-to-batch-ocr-with-aspose-ocr-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonywać OCR wsadowo przy użyciu Aspose OCR – Pełny przewodnik w Pythonie

Zastanawiałeś się kiedyś **jak wykonywać OCR wsadowo** na całym folderze zeskanowanych PDF‑ów lub zdjęć, nie pisząc osobnego skryptu dla każdego pliku? Nie jesteś sam. W wielu rzeczywistych pipeline’ach będziesz musiał **wyodrębniać tekst z obrazów**, usuwać błędy ortograficzne i w końcu zwolnić wszelkie zasoby AI, które przydzieliłeś. Ten tutorial pokazuje dokładnie, jak to zrobić przy użyciu Aspose OCR, lekkiego post‑procesora AI oraz kilku linijek Pythona.

Przejdziemy przez inicjalizację silnika OCR, podłączenie korektora ortograficznego AI, iterację po katalogu zdjęć oraz sprzątanie modelu po zakończeniu. Po zakończeniu będziesz mieć gotowy do uruchomienia skrypt, który automatycznie **koryguje błędy OCR** i zwalnia **darmowe zasoby AI**, aby Twój GPU był zadowolony.

## Czego będziesz potrzebować

- Python 3.9+ (kod używa podpowiedzi typów, ale działa na wcześniejszych wersjach 3.x)
- Pakiet `asposeocr` (`pip install asposeocr`) – zapewnia silnik OCR.
- Dostęp do modelu Hugging Face `bartowski/Qwen2.5-3B-Instruct-GGUF` (pobierany automatycznie).
- GPU z przynajmniej kilkoma GB VRAM (skrypt ustawia `gpu_layers = 30`, możesz zmniejszyć, jeśli potrzebne).

Brak zewnętrznych usług, brak płatnych API – wszystko działa lokalnie.

---

## Krok 1: Konfiguracja silnika OCR – **Jak wykonywać OCR wsadowo** efektywnie

Zanim będziemy mogli przetworzyć tysiąc obrazów, potrzebujemy solidnego silnika OCR. Aspose OCR pozwala wybrać język i tryb rozpoznawania w jednym wywołaniu.

```python
# Step 1: Initialize the OCR engine for English plain‑text output
def init_ocr() -> aocr.OcrEngine:
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English          # English language pack
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Returns raw string, no layout
    return ocr_engine
```

**Dlaczego to ważne:** Ustawienie `recognize_mode` na `Plain` utrzymuje wyjście lekkie, co jest idealne, gdy planujesz później uruchomić sprawdzanie pisowni. Jeśli potrzebujesz informacji o układzie, przełączyłbyś się na `Layout`, ale to dodaje narzut, którego prawdopodobnie nie chcesz w zadaniu wsadowym.

> **Pro tip:** Jeśli masz do czynienia ze skanami wielojęzycznymi, możesz przekazać listę taką jak `ocr_engine.language = [aocr.Language.English, aocr.Language.Spanish]`.

---

## Krok 2: Inicjalizacja post‑procesora AI – **Zastosuj sprawdzanie pisowni** do wyniku OCR

Aspose AI dostarcza wbudowany post‑procesor, który może uruchomić dowolny model. Tutaj pobieramy kwantyzowany model Qwen 2.5 z Hugging Face i podłączamy procedurę sprawdzania pisowni.

```python
# Step 2: Configure and start the AI post‑processor
def init_ai() -> aocr.ai.AsposeAI:
    model_cfg = AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 30          # Adjust based on your GPU memory
    ai_processor = AsposeAI()
    ai_processor.initialize(model_cfg)

    # Attach the built‑in spell‑check post‑processor
    ai_processor.set_post_processor(ai_processor.postprocessor_spell_check, {})
    return ai_processor
```

**Dlaczego to ważne:** Model jest kwantyzowany (`q4_k_m`), co znacznie zmniejsza zużycie pamięci, jednocześnie zapewniając przyzwoite rozumienie języka. Wywołując `set_post_processor`, informujemy Aspose AI, aby automatycznie wykonywał krok **apply spell check** na dowolnym ciągu, który mu przekażemy.

> **Uwaga:** Jeśli Twój GPU nie radzi sobie z 30 warstwami, zmniejsz liczbę do 15 lub nawet 5 – skrypt nadal będzie działał, tylko nieco wolniej.

---

## Krok 3: Uruchom OCR i **koryguj błędy OCR** na pojedynczym obrazie

Teraz, gdy silnik OCR i korektor ortograficzny AI są gotowe, łączymy je. Ta funkcja wczytuje obraz, wyodrębnia surowy tekst, a następnie uruchamia post‑procesor AI, aby go oczyścić.

```python
# Step 3: OCR an image and run the spell‑check post‑processor
def ocr_and_correct(image_path: str,
                    ocr_engine: aocr.OcrEngine,
                    ai_processor: aocr.ai.AsposeAI) -> str:
    image = aocr.Image.load(image_path)               # Load any supported format
    raw_text = ocr_engine.recognize(image)           # Plain string from OCR
    corrected_text = ai_processor.run_postprocessor(raw_text)
    return corrected_text
```

**Dlaczego to ważne:** Bezpośrednie podanie surowego ciągu OCR do modelu AI daje nam etap **correct OCR errors** bez pisania jakichkolwiek wyrażeń regularnych czy własnych słowników. Model rozumie kontekst, więc może naprawić „recieve” → „receive” i jeszcze subtelniejsze błędy.

---

## Krok 4: **Wyodrębniaj tekst z obrazów** masowo – prawdziwa pętla wsadowa

Tutaj magia **jak wykonywać OCR wsadowo** błyszczy. Iterujemy po katalogu, pomijamy nieobsługiwane pliki i zapisujemy każde poprawione wyjście do pliku `.txt`.

```python
# Step 4: Process an entire folder of images
if __name__ == "__main__":
    # Initialize once – reuse for every file
    ocr_engine = init_ocr()
    ai_processor = init_ai()

    input_dir = "YOUR_DIRECTORY/input_images"
    output_dir = "YOUR_DIRECTORY/output_text"
    os.makedirs(output_dir, exist_ok=True)

    for file_name in os.listdir(input_dir):
        # Only handle common image extensions
        if not file_name.lower().endswith(('.png', '.jpg', '.jpeg', '.tif', '.tiff')):
            continue

        image_path = os.path.join(input_dir, file_name)
        corrected = ocr_and_correct(image_path, ocr_engine, ai_processor)

        txt_path = os.path.join(output_dir,
                                os.path.splitext(file_name)[0] + ".txt")
        with open(txt_path, "w", encoding="utf-8") as txt_file:
            txt_file.write(corrected)

        print(f"Processed {file_name}")

    # Step 5: Release **free AI resources** after the batch finishes
    ai_processor.free_resources()
```

### Oczekiwany wynik

Dla obrazu zawierającego zdanie *„The quick brown fox jumps over the lazzy dog.”* zobaczysz plik tekstowy z:

```
The quick brown fox jumps over the lazy dog.
```

Zauważ, że podwójne „z” zostało automatycznie skorygowane – to działanie AI spell‑check.

**Dlaczego to ważne:** Tworząc obiekty OCR i AI **jednorazowo** i ponownie ich używając, unikamy narzutu ładowania modelu dla każdego pliku. To najefektywniejszy sposób na **jak wykonywać OCR wsadowo** w skali.

---

## Krok 5: Sprzątanie – **Zwolnij zasoby AI** prawidłowo

Gdy skończysz, wywołanie `free_resources()` zwalnia pamięć GPU, konteksty CUDA oraz wszelkie tymczasowe pliki utworzone przez model.

```python
# Step 5: Explicitly free GPU and model memory
ai_processor.free_resources()
```

Pominięcie tego kroku może pozostawić wiszące alokacje GPU, co może spowodować awarię kolejnych procesów Pythona lub zająć VRAM. Traktuj to jako część „wyłączenia świateł” w zadaniu wsadowym.

---

## Typowe problemy i dodatkowe wskazówki

| Issue | What to Look For | Fix |
|-------|------------------|-----|
| **Błędy braku pamięci** | GPU wyczerpuje się po kilku dziesiątkach obrazów | Zredukuj `gpu_layers` lub przełącz na CPU (`model_cfg.gpu_layers = 0`). |
| **Brak pakietu językowego** | OCR zwraca puste ciągi | Upewnij się, że wersja `asposeocr` zawiera dane języka angielskiego; w razie potrzeby reinstaluj. |
| **Pliki nie będące obrazami** | Skrypt wyłącza się przy przypadkowym pliku `.pdf` | Warunek `if not file_name.lower().endswith(...)` już je pomija. |
| **Sprawdzanie pisowni nie zastosowane** | Wyjście wygląda identycznie jak surowy OCR | Sprawdź, czy `ai_processor.set_post_processor` został wywołany przed pętlą. |
| **Powolna prędkość wsadowa** | Trwa >5 sekund na obraz | Włącz `model_cfg.allow_auto_download = "false"` po pierwszym uruchomieniu, aby model nie był pobierany ponownie przy każdym uruchomieniu. |

**Pro tip:** Jeśli potrzebujesz **wyodrębniać tekst z obrazów** w języku innym niż angielski, po prostu zmień `ocr_engine.language` na odpowiedni enum (np. `aocr.Language.French`). Ten sam post‑procesor AI nadal zastosuje sprawdzanie pisowni, ale możesz chcieć model specyficzny dla języka, aby uzyskać najlepsze wyniki.

---

## Podsumowanie i kolejne kroki

Omówiliśmy cały pipeline dla **jak wykonywać OCR wsadowo**:

1. **Initialize** silnik OCR zwracający czysty tekst dla języka angielskiego.  
2. **Configure** model AI do sprawdzania pisowni i powiąż go jako post‑procesor.  
3. **Run** OCR na każdym obrazie i pozwól AI **korygować błędy OCR** automatycznie.  
4. **Loop** po katalogu, aby **wyodrębniać tekst z obrazów** masowo.  
5. **Free AI resources** po zakończeniu zadania.

Z tego miejsca możesz:

- Przekierować poprawiony tekst do dalszego pipeline’u NLP (analiza sentymentu, ekstrakcja encji, itp.).
- Zamienić post‑procesor sprawdzania pisowni na własny streszczacz, wywołując `ai_processor.set_post_processor(your_custom_func, {})`.
- Zrównoleglić pętlę folderu przy użyciu `concurrent.futures.ThreadPoolExecutor`, jeśli Twój GPU może obsłużyć wiele strumieni.

---

## Końcowe przemyślenia

Wykonywanie OCR wsadowo nie musi być uciążliwe. Korzystając z Aspose OCR razem z lekkim modelem AI, otrzymujesz **kompleksowe rozwiązanie**, które **wyodrębnia tekst z obrazów**, **stosuje sprawdzanie pisowni**, **koryguje błędy OCR** i **czysto zwalnia zasoby AI**. Wypróbuj skrypt na folderze testowym, dostosuj liczbę warstw GPU do swojego sprzętu i będziesz mieć gotowy do produkcji pipeline w kilka minut.

Masz pytania dotyczące dostosowywania modelu, obsługi PDF‑ów lub integracji tego w usłudze webowej? zostaw komentarz poniżej lub napisz do mnie na GitHubie. Szczęśliwego kodowania i niech Twój OCR będzie zawsze precyzyjny!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}