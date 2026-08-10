---
category: general
date: 2026-05-06
description: Utwórz przeszukiwalny PDF z obrazu przy użyciu Aspose OCR w Javie. Dowiedz
  się, jak konwertować obraz na PDF, włączyć korektę pisowni i używać GPU OCR dla
  szybkich wyników.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- enable spell correction
- use ocr gpu
- process image ocr
language: pl
og_description: Utwórz przeszukiwalny PDF z obrazu przy użyciu Aspose OCR w Javie.
  Ten przewodnik pokazuje, jak przekonwertować obraz na PDF, włączyć korektę pisowni
  i używać OCR GPU.
og_title: Utwórz przeszukiwalny PDF z obrazu przy użyciu Java OCR
tags:
- OCR
- Java
- PDF
title: Utwórz przeszukiwalny PDF z obrazu przy użyciu Java OCR
url: /pl/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie przeszukiwalnego PDF z obrazu przy użyciu Java OCR

Czy kiedykolwiek potrzebowałeś **utworzyć przeszukiwalny PDF** ze zeskanowanego obrazu, ale nie wiedziałeś od czego zacząć? Nie jesteś sam — większość programistów napotyka ten problem, gdy po raz pierwszy zajmuje się PDF‑ami opartymi na obrazach. Na szczęście, dzięki Aspose OCR for Java możesz **konwertować obraz na PDF**, przekształcić tekst w wybieralną treść i nawet dodać korektę pisowni, aby uzyskać dopracowany rezultat.

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który pokazuje, jak **używać OCR GPU**, gdy jest dostępny, jak **efektywnie przetwarzać OCR obrazu**, oraz dlaczego włączenie korekty pisowni ma znaczenie dla późniejszych wyszukiwań. Po zakończeniu będziesz mieć jednopunktowy sposób generowania przeszukiwalnego PDF, który możesz udostępnić użytkownikom lub archiwizować w celu spełnienia wymogów.

> **Pro tip:** Jeśli uruchamiasz program na maszynie bez GPU, kod automatycznie przełącza się na CPU, więc nie musisz nic zmieniać.

---

## Czego będziesz potrzebować

- **Java 8+** (kod kompiluje się z JDK 8 i nowszymi)
- Biblioteka **Aspose OCR for Java** (pobierz najnowszy JAR ze strony Aspose)
- **Obraz wejściowy** (JPEG, PNG, TIFF itp.), który chcesz przekształcić w przeszukiwalny PDF
- (Opcjonalnie) **GPU** z obsługą CUDA, jeśli chcesz najszybsze rozpoznawanie

Bez dodatkowych frameworków, bez magii Maven/Gradle — wystarczy pojedynczy JAR w classpath i możesz zaczynać.

---

## Krok 1: Inicjalizacja silnika OCR – serce procesu  

Najpierw tworzymy instancję `OcrEngine` i wskazujemy plik źródłowy. Ten obiekt jest „kołowrotkiem”, który odczyta obraz, uruchomi sieć neuronową i zwróci nam tekst.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to convert
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

*Dlaczego to ważne:* Inicjalizacja silnika raz i ponowne jego użycie eliminuje konieczność wielokrotnego ładowania bibliotek natywnych — mały zysk wydajności, który rośnie przy przetwarzaniu dziesiątek plików jednocześnie.

---

## Krok 2: Wybór urządzenia przetwarzającego – użyj OCR GPU, gdy to możliwe  

Jeśli Twoja stacja robocza ma kompatybilne GPU, możesz poinstruować Aspose, aby wykonał ciężkie obliczenia na nim. W przeciwnym razie silnik automatycznie przełącza się na CPU.

```java
        // Prefer GPU; fall back to CPU if no compatible device is found
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);
```

*Jaka jest korzyść?* Przyspieszenie dzięki GPU może skrócić czas przetwarzania każdej strony o kilka sekund, szczególnie przy skanach wysokiej rozdzielczości. Mechanizm awaryjny zapewnia, że ten sam kod działa wszędzie, dlatego zalecamy **use OCR GPU** jako domyślne ustawienie.

---

## Krok 3: Przyspiesz skanowanie – wykorzystaj wszystkie rdzenie CPU  

Nawet gdy GPU jest zajęte, otaczające kroki wstępnego przetwarzania mogą być równolegle wykonywane. Ustawienie liczby wątków na liczbę dostępnych procesorów daje silnikowi szansę na jednoczesne przetwarzanie wielu fragmentów.

```java
        // Use all logical cores for preprocessing and language detection
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());
```

*Uwaga:* Na laptopie z 4‑rdzeniowym procesorem uruchomi się cztery wątki; na stacji roboczej z 16 rdzeniami uzyskasz pełną korzyść. Pamiętaj jednak, że więcej wątków oznacza większe zużycie pamięci.

---

## Krok 4: Oczyszczenie obrazu – filtry wstępnego przetwarzania  

Rozmyta lub zaszumiona skan może generować śmieciowy tekst. Dodanie kilku wbudowanych filtrów znacząco podnosi dokładność.

```java
        // Deskew the image so text lines are horizontal
        ocrEngine.getPreprocessing().add(new DeskewFilter());

        // Remove speckles and background noise
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());
```

*Dlaczego te filtry?* `DeskewFilter` koryguje rotację, która często pojawia się, gdy dokument jest podawany do skanera pod kątem. `NoiseRemovalFilter` usuwa przypadkowe piksele, które w przeciwnym razie byłyby interpretowane jako znaki. To tak, jakby dać silnikowi OCR czysty arkusz papieru do odczytania.

---

## Krok 5: Włączenie inteligentnych funkcji – korekta pisowni i automatyczne wykrywanie języka  

Jeśli pracujesz z dokumentami wielojęzycznymi lub po prostu chcesz mieć mniej literówek, włącz wbudowany sprawdzacz pisowni i pozwól silnikowi odgadnąć język.

```java
        // Activate spell correction to fix common OCR mistakes
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Let the engine automatically detect the language of the input
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

*Kiedy to przydatne?* Załóżmy, że skan zawiera zarówno fragmenty po angielsku, jak i po hiszpańsku. Funkcja automatycznego wykrywania przełącza słowniki w locie, a korekta pisowni naprawia błędnie odczytane znaki, np. „0” zamiast „O”. Ten krok jest niezbędny, aby **przeszukiwalny PDF** zwracał prawidłowe wyniki.

---

## Krok 6: Zapis wyniku – konwersja obrazu na PDF i uczynienie go przeszukiwalnym  

Na koniec prosimy silnik o zapisanie PDF, w którym oryginalny obraz znajduje się pod niewidzialną warstwą tekstową. To klasyczny **convert image to PDF** workflow, ale PDF jest teraz przeszukiwalny.

```java
        // Generate a searchable PDF – the text layer sits behind the original image
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

Plik wyjściowy (`output-searchable.pdf`) można otworzyć w dowolnym przeglądarce PDF; będziesz mógł zaznaczać, kopiować i wyszukiwać tekst tak, jak w natywnym PDF. Nie potrzebujesz dodatkowych narzędzi.

---

## Pełny działający przykład – kopiuj‑i‑uruchom  

Poniżej znajduje się cały program, gotowy do kompilacji. Zamień `YOUR_DIRECTORY` na folder, w którym znajduje się `input.jpg`.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine and load the source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 2: Select the processing device (GPU if available, otherwise CPU)
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);

        // Step 3: Use all available CPU cores to speed up recognition
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 4: Add preprocessing filters to improve image quality
        ocrEngine.getPreprocessing().add(new DeskewFilter());
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());

        // Step 5: Enable spell correction and automatic language detection
        ocrEngine.getSettings().setEnableSpellCorrection(true);
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // Step 6: Perform OCR and save the result as a searchable PDF
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

**Oczekiwany wynik:** Po uruchomieniu programu w konsoli pojawi się linia *„Searchable PDF generated successfully.”* Otwierając `output-searchable.pdf` w Adobe Reader, możesz wpisać słowo z oryginalnego obrazu w polu wyszukiwania i natychmiast przeskoczyć do jego lokalizacji.

---

## Częste pytania i sytuacje brzegowe  

- **Co jeśli GPU nie zostanie wykryte?**  
  Wywołanie `setDeviceType(OcrDeviceType.GPU)` nie generuje wyjątku; jedynie instruuje silnik, aby najpierw spróbował użyć GPU. Jeśli się nie powiedzie, silnik cicho przełącza się na CPU.

- **Czy mogę przetwarzać wiele obrazów w jednym uruchomieniu?**  
  Tak. Umieść kod w pętli, zmieniaj nazwę pliku w każdej iteracji i ponownie używaj tej samej instancji `OcrEngine`, aby utrzymać niskie zużycie pamięci.

- **Mój PDF jest ogromny — jak go zmniejszyć?**  
  Po OCR możesz skorzystać z API optymalizacji PDF Aspose lub po prostu zmniejszyć rozdzielczość obrazu przed przekazaniem go silnikowi (`ImageStream.fromFile(...).setResolution(150)` dla 150 DPI).

- **Muszę zachować oryginalną rozdzielczość obrazu ze względu na wymogi prawne.**  
  Format `PDF_SEARCHABLE` zachowuje oryginalny bitmap dokładnie; niewidzialna warstwa tekstowa jest dodawana na wierzchu, nie zmieniając jakości wizualnej.

---

## Podsumowanie wizualne  

![przykład tworzenia przeszukiwalnego pdf](placeholder-image.png "przykład tworzenia przeszukiwalnego pdf")

*Tekst alternatywny:* *przykład tworzenia przeszukiwalnego pdf – silnik Java OCR przekształcający zeskanowany JPG w przeszukiwalny PDF.*

---

## Zakończenie  

Masz teraz **kompletną, end‑to‑end rozwiązanie** do przekształcania dowolnego obrazu w **przeszukiwalny PDF** przy użyciu Aspose OCR for Java. Dzięki **konwersji obrazu na PDF**, **włączeniu korekty pisowni** i **użyciu OCR GPU**, gdy to możliwe, uzyskasz szybkie, dokładne i przeszukiwalne wyniki działające na wszystkich platformach.

Co dalej? Wypróbuj:

- **Różne formaty wyjściowe** (`PDF`, `DOCX`, `HTML`), aby zobaczyć, jak zachowuje się warstwa tekstowa.
- **Własne słowniki**, jeśli przetwarzasz żargon specyficzny dla danej dziedziny.
- **Przetwarzanie wsadowe**, aby automatycznie obsłużyć tysiące skanów.

Śmiało modyfikuj liczbę wątków, zamieniaj filtry lub podłącz własny pipeline wstępnego przetwarzania. Podstawowy wzorzec pozostaje ten sam: ładowanie → wstępne przetwarzanie → konfiguracja → OCR → zapis.

Miłego kodowania i niech Twoje PDF‑y zawsze będą przeszukiwalne!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}