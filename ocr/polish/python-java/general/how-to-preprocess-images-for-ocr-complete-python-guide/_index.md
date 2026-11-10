---
category: general
date: 2026-06-06
description: Jak przygotować obrazy do OCR przy użyciu Pythona. Dowiedz się, jak binaryzować
  obraz metodą Otsu, jak prostować zeskanowane dokumenty oraz jak poprawić dokładność
  OCR dla tekstu niemieckiego.
draft: false
keywords:
- how to preprocess images for OCR
- binarize image using otsu
- how to deskew scanned documents
- how to improve OCR accuracy
- extract text from german image
language: pl
og_description: Jak przygotować obrazy do OCR w Pythonie. Ten tutorial pokazuje, jak
  binaryzować obraz przy użyciu metody Otsu, jak prostować zeskanowane dokumenty oraz
  jak poprawić dokładność OCR dla obrazów w języku niemieckim.
og_title: Jak przygotować obrazy do OCR – Kompletny przewodnik w Pythonie
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  headline: How to Preprocess Images for OCR – Complete Python Guide
  type: TechArticle
- description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  name: How to Preprocess Images for OCR – Complete Python Guide
  steps:
  - name: How to Deskew Scanned Documents
    text: The `deskew` call above is the concrete answer to **how to deskew scanned
      documents**. Internally it estimates the dominant text line angle via Hough
      transform and rotates the image back. If your documents are rotated more than
      5°, bump `max_angle` up, but beware of over‑rotation artifacts.
  - name: Binarize Image Using Otsu
    text: The `binarize(method="otsu")` line directly answers the query **binarize
      image using otsu**. Otsu’s algorithm computes a threshold that minimizes intra‑class
      variance, which is perfect for documents with bimodal histograms (dark text
      vs. light background).
  - name: Expected Output
    text: 'Assuming the sample scan contains the sentence “Die schnelle braune Füchsin
      springt über den faulen Hund.” you should see something like:'
  type: HowTo
tags:
- OCR
- image preprocessing
- Python
- German language
title: Jak przygotować obrazy do OCR – Kompletny przewodnik w Pythonie
url: /pl/python-java/general/how-to-preprocess-images-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak przetwarzać obrazy pod OCR – Kompletny przewodnik w Pythonie

Zastanawiałeś się kiedyś **jak przetwarzać obrazy pod OCR**, aby tekst był krystalicznie czysty? Nie jesteś jedyny. Skanowane dokumenty — szczególnie zaszumione niemieckie strony — mogą być koszmarem dla każdego silnika OCR. Dobra wiadomość? Kilka sprytnych kroków przetwarzania może zamienić rozmyty, zaszpunowany skan w czysty, czytelny dla maszyny obraz.

W tym samouczku przeprowadzimy praktyczny przykład, który pokazuje **jak przetwarzać obrazy pod OCR** przy użyciu Pythona. Nauczysz się **binarizować obraz metodą Otsu**, **jak prostować zeskanowane dokumenty**, oraz ogólnie **jak poprawić dokładność OCR**, gdy potrzebujesz **wyodrębnić tekst z niemieckich plików obrazów**. Bez zbędnych wstępów, tylko działający skrypt, który możesz skopiować‑wkleić już dziś.

## Czego będziesz potrzebować

- **Python 3.9+** (dowolna nowsza wersja)
- Biblioteka OCR udostępniająca klasę `OcrEngine` – w demonstracji przyjmiemy ogólny pakiet `ocr`. Zainstaluj go poleceniem `pip install ocr-lib`.
- Zaszumiony skan niemiecki (`noisy_german_scan.tif`), który chcesz przetestować.
- Podstawowa znajomość funkcji w Pythonie (jeśli już pisałeś `def`, jesteś gotowy).

> **Pro tip:** Jeśli używasz innego SDK OCR (np. Tesseract przez `pytesseract`), koncepcje pozostają takie same — wystarczy dostosować nazwy metod.

## Przegląd rozwiązania

1. **Utwórz instancję silnika OCR.**  
2. **Ustaw język rozpoznawania na niemiecki.**  
3. **Zbuduj własny pipeline przetwarzania**, który obejmuje prostowanie, odszumianie, binarizację (Otsu) i rozciąganie kontrastu.  
4. **Dołącz pipeline do silnika**, aby każde zdjęcie przechodziło przez niego automatycznie.  
5. **Uruchom OCR** na zaszumionym niemieckim skanie.  
6. **Wypisz wyodrębniony tekst**, aby zweryfikować wynik.

![jak przetwarzać obrazy pod OCR przykład](image.png "jak przetwarzać obrazy pod OCR przykład")

## Krok 1: Utwórz instancję silnika OCR

Na początek — bez silnika nic się nie dzieje. Obiekt `OcrEngine` jest punktem wejścia, który koordynuje wszystkie późniejsze operacje.

```python
# Step 1: Initialize the OCR engine
from ocr import OcrEngine, Language

ocr_engine = OcrEngine()
```

*Dlaczego to ważne:* Inicjalizacja silnika konfiguruje zasoby wewnętrzne (takie jak modele językowe) i daje czystą bazę do podłączenia własnego pipeline’u później.

## Krok 2: Ustaw język rozpoznawania na niemiecki

Dokładność OCR jest silnie zależna od języka. Informując silnik, że ma oczekiwać języka niemieckiego, aktywujesz odpowiedni zestaw znaków i model językowy.

```python
# Step 2: Tell the engine we’re working with German text
ocr_engine.set_recognition_language(Language.GERMAN)
```

Jeśli pominiesz ten krok, silnik może domyślnie używać angielskiego, co spowoduje błędne rozpoznawanie umlautów (ä, ö, ü) oraz znaku ß — typowe pułapki przy pracy z niemieckimi skanami.

## Krok 3: Zbuduj własny pipeline przetwarzania

To serce **jak przetwarzać obrazy pod OCR**. Połączymy cztery transformacje:

| Transformacja | Co robi | Dlaczego pomaga |
|----------------|--------------|--------------|
| **Deskew** | Obraca obraz z powrotem do poziomu (maks 5°) | Skanowane dokumenty rzadko są idealnie wyrównane; prostowanie usuwa pochylenie, które myli segmentację znaków. |
| **Denoise** | Redukuje losowe plamki (siła 0.7) | Szum tworzy fałszywe krawędzie, które silnik OCR może zinterpretować jako znaki. |
| **Binarize (Otsu)** | Konwertuje do czerni‑i‑bieli metodą Otsu | Czysty obraz binarny zapewnia silnikowi wyraźny kontrast między pierwszym planem (tekst) a tłem. |
| **Contrast Stretch** | Rozciąga zakres dynamiczny | Poprawia czytelność słabych kresek, szczególnie w starych dokumentach. |

```python
# Step 3: Assemble the preprocessing pipeline
preprocessing_pipeline = (
    ocr_engine.preprocessing()
               .deskew(max_angle=5)          # auto‑deskew up to 5°
               .denoise(strength=0.7)       # medium denoise
               .binarize(method="otsu")      # **binarize image using Otsu**
               .contrast(stretch=True)      # auto contrast stretch
)

# Explanation:
# - `deskew` corrects rotation; 5° is a safe ceiling for most scans.
# - `denoise` with 0.7 balances smoothing without erasing thin characters.
# - `binarize` with method "otsu" automatically selects the optimal threshold.
# - `contrast` stretch brightens faint ink while keeping dark ink dark.
```

### Jak prostować zeskanowane dokumenty

Wywołanie `deskew` powyżej jest konkretną odpowiedzią na **jak prostować zeskanowane dokumenty**. Wewnątrz szacuje dominujący kąt linii tekstu za pomocą transformacji Hougha i obraca obraz z powrotem. Jeśli Twoje dokumenty są obrócone o więcej niż 5°, zwiększ `max_angle`, ale uważaj na artefakty nadmiernego obracania.

### Binarnizuj obraz metodą Otsu

Linia `binarize(method="otsu")` bezpośrednio odpowiada na pytanie **binarizować obraz metodą Otsu**. Algorytm Otsu oblicza próg minimalizujący wariancję wewnątrz klas, co jest idealne dla dokumentów z dwumodalnym histogramem (ciemny tekst vs. jasne tło).

## Krok 4: Dołącz pipeline do silnika

Teraz informujemy silnik OCR, aby uruchamiał każdy przychodzący obraz przez właśnie zbudowany pipeline.

```python
# Step 4: Register the custom pipeline
ocr_engine.set_preprocessing(preprocessing_pipeline)
```

*Dlaczego to ważne:* Bez rejestracji silnik przetworzyłby surowy skan, ignorując wszystkie przygotowane czyszczenia. Ten krok zapewnia **jak poprawić dokładność OCR** poprzez konsekwentne stosowanie tego samego przetwarzania.

## Krok 5: Rozpoznaj tekst z zaszumionego niemieckiego skanu

Czas połączyć wszystko. Przekazujemy silnikowi zaszumiony niemiecki obraz i pozwalamy mu wykonać ciężką pracę.

```python
# Step 5: Run OCR on the target file
image_path = "YOUR_DIRECTORY/noisy_german_scan.tif"
recognition_result = ocr_engine.recognize_image(image_path)
```

Jeśli interesuje Cię wydajność, możesz zmierzyć czas wywołania:

```python
import time
start = time.time()
result = ocr_engine.recognize_image(image_path)
print(f"OCR took {time.time() - start:.2f}s")
```

## Krok 6: Wyświetl rozpoznany tekst

Na koniec wypisujemy wyodrębniony ciąg znaków. To bezpośrednia odpowiedź na **wyodrębnić tekst z niemieckiego obrazu**.

```python
# Step 6: Display the OCR output
print("=== Recognized German Text ===")
print(recognition_result.text)
```

### Oczekiwany wynik

Zakładając, że przykładowy skan zawiera zdanie „Die schnelle braune Füchsin springt über den faulen Hund.”, powinieneś zobaczyć coś w stylu:

```
=== Recognized German Text ===
Die schnelle braune Füchsin springt über den faulen Hund.
```

Jeśli wynik nadal zawiera zniekształcone znaki, rozważ dostosowanie siły `denoise` lub zwiększenie `max_angle` przy prostowaniu.

## Częste pułapki i jak je rozwiązać

- **Brak modelu językowego:** Zapomnienie o `set_recognition_language(Language.GERMAN)` często skutkuje brakującymi umlautami. Sprawdź, czy wywołanie jest obecne.
- **Nadmierne odszumianie:** Siła powyżej 0.9 może wymazać cienkie kreski, zwłaszcza w starszych czcionkach. Trzymaj się zakresu 0.5‑0.7 w większości przypadków.
- **Nieprawidłowy format pliku:** Niektóre silniki OCR nie radzą sobie z wielostronicowymi TIFF‑ami. Jeśli masz dokument wielostronicowy, podziel go najpierw na pojedyncze pliki.
- **Kolejność pipeline’u:** Pokazana kolejność (prostowanie → odszumianie → binarizacja → kontrast) jest zamierzona. Binarizacja przed odszumianiem może utrwalić szum; zawsze najpierw odszumiaj.

## Rozszerzanie pipeline (Co dalej?)

Teraz, gdy masz solidną bazę, możesz rozważyć:

- **Dodanie otwarcia morfologicznego** w celu usunięcia drobnych plamek (`.morph_open(kernel=3)`).
- **Integrację modelu językowego** do korekcji po‑procesowej (`ocr_engine.apply_spellcheck()`).
- **Równoległe przetwarzanie wsadowe** dużych zbiorów danych przy użyciu `concurrent.futures`.

Wszystkie te rozszerzenia zachowują główną ideę **jak przetwarzać obrazy pod OCR**, jednocześnie podnosząc **jak poprawić dokładność OCR** jeszcze bardziej.

## Zakończenie

Omówiliśmy **jak przetwarzać obrazy pod OCR** od początku do końca: utworzyliśmy silnik, ustawiliśmy język niemiecki, zbudowaliśmy pipeline, który **binarizuje obraz metodą Otsu**, **jak prostować zeskanowane dokumenty**, i w końcu **wyodrębnić tekst z niemieckiego obrazu** z większą pewnością. Stosując sześć opisanych kroków, zauważysz wyraźny wzrost jakości rozpoznawania — koniec z niekończącymi się ręcznymi poprawkami.

Wypróbuj skrypt na własnych skanach, eksperymentuj z parametrami i pozwól wynikom przemówić. Masz pytania o konkretną technikę przetwarzania? Zostaw komentarz, a zagłębimy się razem.

Powodzenia w kodowaniu i niech Twój OCR będzie zawsze precyzyjny!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz szczegółowe wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Wyodrębnij tekst z obrazu C# z wyborem języka przy użyciu Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Jak ustawić wartość progu w rozpoznawaniu obrazu OCR](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Jak wykonać OCR obrazu – Przeprowadź OCR na obrazie w rozpoznawaniu obrazu OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}