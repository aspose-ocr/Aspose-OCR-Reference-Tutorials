---
category: general
date: 2026-04-26
description: Jak przeprowadzić OCR na zeskanowanym formularzu, nauczyć się wstępnie
  przetwarzać obraz, aby zredukować szumy, i szybko wyodrębnić tekst z obrazu.
draft: false
keywords:
- how to run OCR
- how to preprocess image
- extract text from image
- how to extract text
- how to reduce noise
language: pl
og_description: Jak uruchomić OCR na zeskanowanych dokumentach, wstępnie przetworzyć
  obrazy, zredukować szumy i efektywnie wyodrębnić tekst.
og_title: Jak uruchomić OCR i przetwarzać obrazy – szybki przewodnik
tags:
- OCR
- image processing
- Python
title: Jak uruchomić OCR i przetwarzać obrazy – wyodrębnić tekst ze skanowanych formularzy
url: /pl/python-java/general/how-to-run-ocr-and-preprocess-images-extract-text-from-scann/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak uruchomić OCR – Kompletny przewodnik po wyodrębnianiu tekstu z obrazów

Zastanawiałeś się kiedyś **jak uruchomić OCR** na niechlujnym zeskanowanym formularzu i uzyskać czysty, przeszukiwalny tekst? Nie jesteś jedyny. W wielu rzeczywistych projektach surowy obraz jest pełen plamek, nierównego oświetlenia i innych niedoskonałości, które powodują, że domyślne OCR się potyka.  

Dobra wiadomość? Dzięki kilku linijkom Pythona i inteligentnemu potokowi wstępnego przetwarzania możesz znacząco zwiększyć dokładność rozpoznawania, **zredukować szumy**, i wyciągnąć dokładnie te słowa, których potrzebujesz. W tym samouczku przeprowadzimy Cię przez każdy krok — od wczytania obrazu po wypisanie końcowego ciągu znaków — tak abyś otrzymał gotowy fragment kodu, który możesz dostosować do faktur, paragonów lub dowolnego zeskanowanego dokumentu.

## Co zbudujesz

- Instancję `OcrEngine`, która komunikuje się z bazową biblioteką OCR.  
- Łańcuch wstępnego przetwarzania, który **binaryzuje** obraz i stosuje **median blur**, aby wygładzić plamki.  
- Proste wywołanie `process()`, które zwraca obiekt udostępniający `text`, wyodrębniony ciąg znaków.  

Na koniec będziesz mieć samodzielny skrypt, który możesz uruchomić na dowolnym pliku obrazu i od razu zobaczyć wyodrębniony tekst w konsoli.

## Wymagania wstępne

- Python 3.9+ (użyta składnia odpowiada najnowszemu stabilnemu wydaniu).  
- Fikcyjny pakiet `aocr` – traktuj go jako cienką nakładkę na Tesseract lub dowolny nowoczesny silnik OCR. Zainstaluj go poleceniem `pip install aocr`.  
- Zeskanowany obraz (`scanned_form.jpg`) umieszczony w folderze, do którego możesz odwołać się w kodzie.  

Jeśli używasz prawdziwej biblioteki OCR, takiej jak `pytesseract`, możesz zamienić `OcrEngine` na odpowiednią klasę — wszystko inne pozostaje bez zmian.

![](how-to-run-ocr-example.png "przykład uruchamiania OCR pokazujący zeskanowany formularz i wyodrębniony tekst")

*Alt text: jak uruchomić OCR na zeskanowanym dokumencie i wyświetlić wyodrębniony tekst.*

---

## Krok 1: Jak uruchomić OCR – Inicjalizacja silnika

Zanim silnik będzie mógł cokolwiek odczytać, musimy utworzyć jego instancję. Traktuj `OcrEngine` jako mózg, który później będzie interpretował dane wizualne.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()
```

> **Dlaczego to ważne:** Inicjalizacja silnika ustawia wewnętrzne modele, ładuje pakiety językowe i przygotowuje środowisko uruchomieniowe. Pominięcie tego kroku zazwyczaj skutkuje błędem `NoneType`, gdy później wywołasz `process()`.

---

## Krok 2: Jak wstępnie przetworzyć obraz – Wczytaj swój zeskanowany formularz

Teraz, gdy mózg jest gotowy, podajemy mu obraz. Obraz może być w dowolnym formacie obsługiwanym przez `aocr.Image`.

```python
# Step 2: Load the image you want to recognize
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/scanned_form.jpg")
```

> **Porada:** Używaj ścieżek bezwzględnych podczas rozwoju, aby uniknąć niespodzianek „plik nie znaleziony”, gdy skrypt uruchamia się z innego katalogu roboczego.

---

## Krok 3: Jak zredukować szumy – Zastosuj binaryzację i median blur

Surowe skany często zawierają przypadkowe kropki, nierówne tło lub słabe cienie. Dwa klasyczne triki — **binaryzacja** i **median blur** — oczyszczają obraz bez utraty krawędzi definiujących znaki.

```python
# Step 3: Pre‑process the image to improve recognition accuracy
# • Binarize converts the image to black‑and‑white using a threshold
# • Median blur reduces noise while preserving edges
ocr_engine.image = ocr_engine.image.apply_filters(
    aocr.ImageFilters.binarize(threshold=180),
    aocr.ImageFilters.median_blur(radius=2)
)
```

### Zagłębienie się

- **Binaryzacja**: Wartość `threshold=180` mówi algorytmowi: „Wszystko jaśniejsze niż 180 staje się białe; wszystko inne czarne.” Dostosuj tę liczbę, jeśli Twój skan jest zbyt ciemny lub zbyt jasny.  
- **Median Blur**: Promień `2` oznacza, że filtr patrzy na okno 5×5 pikseli i zastępuje środkowy piksel medianą. To wygładza pojedyncze plamki, zachowując jednocześnie kreski liter.

> **Przypadek brzegowy:** Jeśli Twój dokument ma kolorowe podświetlenia, prosty próg binarny może je usunąć. W takim scenariuszu rozważ użycie `aocr.ImageFilters.adaptive_threshold()` — dostosowuje on progowanie lokalnie w całym obrazie.

---

## Krok 4: Jak wyodrębnić tekst – Uruchom proces OCR

Mając czysty obraz, w końcu pozwalamy silnikowi wykonać swoją magię.

```python
# Step 4: Run the OCR process on the prepared image
ocr_result = ocr_engine.process()
```

> **Co dzieje się pod maską?** Silnik uruchamia sieć neuronową (lub starszy matcher wzorców) na macierzy pikseli, tłumaczy każdy rozpoznany glif na znaki Unicode i układa je w linie oraz akapity.

---

## Krok 5: Jak wyodrębnić tekst – Wypisz wynik

Obiekt `ocr_result` udostępnia wygodny atrybut `text`. Zobaczmy, co otrzymaliśmy.

```python
# Step 5: Print the extracted text
print(ocr_result.text)
```

### Oczekiwany wynik

Jeśli zeskanowany formularz zawiera:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Powinieneś zobaczyć coś podobnego:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Zauważ, jak krok wstępnego przetwarzania usunął przypadkowe kropki, które wcześniej zamieniły „Amount” w „Am0unt”. To moc **redukcji szumów** przed OCR.

---

## Częste problemy i jak je naprawić

| Objaw | Prawdopodobna przyczyna | Szybka naprawa |
|-------|--------------------------|----------------|
| Zniekształcone znaki (np. “@#%”) | Obraz zbyt ciemny lub zbyt jasny | Dostosuj `threshold` w `binarize()`; wypróbuj `adaptive_threshold`. |
| Brakujące słowa | Nadal obecne szumy | Zwiększ `radius` w `median_blur` lub dodaj filtr `gaussian_blur`. |
| Nieprawidłowy język (np. angielskie litery zamieniają się na chińskie) | Załadowany niewłaściwy pakiet językowy | Przekaż `language="eng"` przy tworzeniu `OcrEngine()`, jeśli biblioteka to obsługuje. |
| Wolne przetwarzanie dużych plików | Wysoka rozdzielczość | Zmniejsz rozmiar obrazu najpierw: `aocr.ImageFilters.resize(width=1200)` przed binaryzacją. |

---

## Dalsze kroki – Następne etapy i powiązane tematy

- **Przetwarzanie wsadowe**: Zawijaj powyższą logikę w pętlę, aby automatycznie obsługiwać dziesiątki plików.  
- **Strukturalny wynik**: Użyj wyrażeń regularnych na `ocr_result.text`, aby wyciągnąć pola takie jak daty czy kwoty.  
- **Alternatywne biblioteki**: Zamień `aocr` na `pytesseract` — kod zmienia się tylko w kroku inicjalizacji silnika.  
- **Jak wstępnie przetworzyć obraz dla PDF‑ów**: Konwertuj każdą stronę PDF na obraz, a następnie zastosuj ten sam potok.  

Te rozszerzenia pozwalają skalować rozwiązanie od pojedynczego formularza do przedsiębiorstwa‑poziomu potoku ingestującego dokumenty.

---

## Zakończenie

Omówiliśmy **jak uruchomić OCR** od początku do końca, pokazaliśmy **jak wstępnie przetworzyć obraz**, aby **zredukować szumy**, oraz zademonstrowaliśmy **jak wyodrębnić tekst z obrazu** przy użyciu czystego, powtarzalnego skryptu. Najważniejsze wnioski? Kilka prostych filtrów — binaryzacja i median blur — może przekształcić zaszumiony skan w wiarygodne źródło danych, oszczędzając godziny ręcznego czyszczenia.  

Wypróbuj skrypt na własnych dokumentach, dostosuj progi i obserwuj, jak rośnie dokładność. Gdy będziesz gotowy, zbadaj przetwarzanie wsadowe lub zintegrować wynik z bazą danych, aby uzyskać przeszukiwalne archiwa. Szczęśliwego kodowania i niech Twój OCR zawsze będzie precyzyjny!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}