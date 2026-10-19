---
category: general
date: 2026-03-26
description: Jak wsadowe OCR w C# ułatwia wyodrębnianie tekstu z plików PNG. Skorzystaj
  z tego krok po kroku tutorialu C# OCR do wsadowego wyodrębniania tekstu przy użyciu
  Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- c# ocr tutorial
- how to create OCR
- batch text extraction
language: pl
og_description: Jak wykonywać OCR wsadowo w C# pozwala na szybkie wyodrębnianie tekstu
  z plików PNG. Ten przewodnik przeprowadzi Cię przez kompletny samouczek OCR w C#
  z wsadowym wyodrębnianiem tekstu.
og_title: Jak wykonać wsadowe OCR w C# – wyodrębnić tekst z PNG
tags:
- OCR
- C#
- Aspose
title: Jak wykonywać OCR wsadowo w C# – Wyodrębnić tekst z PNG
url: /pl/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonywać OCR wsadowo w C# – Ekstrahowanie tekstu z PNG

Zastanawiałeś się kiedyś **jak wykonywać OCR wsadowo** na stosie zrzutów ekranu bez pisania osobnego programu dla każdego pliku? Nie jesteś sam. W wielu projektach kończymy z dziesiątkami plików PNG, z których trzeba wyodrębnić tekst, a robienie tego jeden po drugim jest uciążliwe.  

Dobra wiadomość? Z Aspose OCR możesz uruchomić małą aplikację konsolową w C#, która przetwarza wszystkie te obrazy równolegle, zapewniając szybkie **wsadowe wyodrębnianie tekstu** i czysty zestaw wyników. W tym przewodniku przeprowadzimy Cię przez pełny **c# ocr tutorial**, wyjaśnimy, dlaczego każdy element ma znaczenie, i pokażemy dokładnie, jak wygląda wyjściowy rezultat.

Do końca tego artykułu będziesz w stanie:

* Załadować listę plików PNG (lub dowolnego obsługiwanego obrazu) jednorazowo.  
* Skonfigurować współdzielony `OcrEngine`, aby ustawienia były spójne w całym wsadzie.  
* Uruchomić kolejkę rozpoznawania z maksymalnie czterema równoległymi pracownikami.  
* Pobrać rozpoznany tekst dla każdej strony i wydrukować go w konsoli.

Bez magii, po prostu solidny kod, który możesz dziś wstawić do swojego rozwiązania.

## Czego będziesz potrzebować

* .NET 6 SDK (lub dowolna nowsza wersja .NET).  
* Ważna licencja Aspose OCR lub tymczasowy klucz ewaluacyjny.  
* Folder zawierający pliki PNG, które chcesz przetworzyć.  
* Visual Studio 2022 lub Twój ulubiony edytor.

To wszystko — żadnych dodatkowych pakietów NuGet poza `Aspose.OCR` i standardowym `System.Collections.Generic`.

## Jak wykonywać OCR wsadowo – Konfiguracja projektu

Na początek, utwórz nowy projekt konsolowy i dodaj bibliotekę Aspose OCR.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

Po zakończeniu przywracania, otwórz **Program.cs** (lub utwórz nowy plik) i dodaj standardowe dyrektywy `using`:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
```

Ta prosta struktura daje nam dostęp do `OcrEngine`, `RecognitionQueue` oraz klas pomocniczych, których będziemy potrzebować później.

## Ekstrahowanie tekstu z PNG – Przygotowanie listy obrazów

Teraz musimy powiedzieć programowi, **które PNG** mają zostać przetworzone przez OCR. Najprostszy sposób to zbudowanie `List<string>` przechowującej absolutne lub względne ścieżki.

```csharp
// Step 1: Define the image files to be processed
var imagePaths = new List<string>
{
    @"YOUR_DIRECTORY/page1.png",
    @"YOUR_DIRECTORY/page2.png",
    @"YOUR_DIRECTORY/page3.png",
    @"YOUR_DIRECTORY/page4.png"
};
```

Zastąp `YOUR_DIRECTORY` rzeczywistą ścieżką do folderu. Jeśli masz dynamiczny zestaw, możesz także użyć `Directory.GetFiles(@\"YOUR_DIRECTORY\", \"*.png\")` i wprowadzić wynik do listy. Kluczowe jest to, że **ekstrahowanie tekstu z PNG** to po prostu podanie właściwych nazw plików do kolejki.

![Diagram przepływu OCR wsadowego](https://example.com/placeholder.png "Diagram ilustrujący, jak wykonać OCR wsadowo na kolekcji plików PNG")

*Tekst alternatywny obrazu: diagram przepływu OCR wsadowego*

## Samouczek C# OCR – Konfiguracja kolejki rozpoznawania

Serce operacji wsadowej to `RecognitionQueue`. Wyobraź sobie ją jako taśmę produkcyjną, która przekazuje każdy obraz do współdzielonego `OcrEngine`. Dzięki współdzieleniu silnika utrzymujemy niskie zużycie pamięci i zapewniamy identyczne ustawienia dla każdej strony.

```csharp
// Step 2: Create a recognition queue with shared OCR engine and parallelism
var recognitionQueue = new RecognitionQueue
{
    MaxDegreeOfParallelism = 4,          // run up to 4 images at the same time
    Engine = new OcrEngine()            // shared configuration for all images
};
```

Dlaczego ustawić `MaxDegreeOfParallelism` na 4? Na typowym laptopie z czterordzeniowym procesorem zapewnia to najlepszą przepustowość bez obciążania systemu operacyjnego. Jeśli uruchamiasz na serwerze z większą liczbą rdzeni, zwiększ tę wartość odpowiednio.

### Wskazówka pro

Jeśli potrzebujesz własnych pakietów językowych, ustawień DPI lub przycinania regionu zainteresowania, zrób to **jednorazowo** na współdzielonym `Engine` przed dodaniem jakichkolwiek obrazów do kolejki. Na przykład:

```csharp
recognitionQueue.Engine.Language = Language.English;
recognitionQueue.Engine.Dpi = 300;
```

Wszystkie kolejne rozpoznania dziedziczą te opcje automatycznie — to istota **tworzenia pipeline OCR**, które pozostają spójne.

## Wsadowe wyodrębnianie tekstu – Dodawanie obrazów do kolejki i uruchamianie kolejki

Po przygotowaniu kolejki, następnym krokiem jest dodanie każdego obrazu do niej. Metoda `Enqueue` przyjmuje instancję `OcrImage`, którą tworzymy ze ścieżki pliku.

```csharp
// Step 3: Enqueue each image for OCR processing
foreach (var path in imagePaths)
    recognitionQueue.Enqueue(OcrImage.FromFile(path));
```

Gdy wszystkie pliki zostaną dodane do kolejki, uruchamiamy przetwarzanie:

```csharp
// Step 4: Run the queue and collect OCR results
List<OcrResult> ocrResults = recognitionQueue.ExecuteAll();
```

`ExecuteAll` blokuje aż wszystkie obrazy zakończą przetwarzanie, a następnie zwraca listę, w której każdy element odpowiada kolejności wejściowej. To gwarantuje, że wynik strony 1 znajduje się pod indeksem 0, strony 2 pod indeksem 1 itd. — przydatne, gdy trzeba odwzorować wyniki na pliki źródłowe.

## Jak tworzyć OCR – Wyświetlanie wyników

Na koniec wydrukujmy rozpoznany tekst w konsoli. To właśnie tutaj naprawdę zobaczysz **wsadowe wyodrębnianie tekstu** w działaniu.

```csharp
// Step 5: Output the recognized text for each page
for (int i = 0; i < ocrResults.Count; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

Po uruchomieniu programu (`dotnet run`) powinieneś zobaczyć coś podobnego do:

```
--- Page 1 ---
Welcome to the quarterly report.
--- Page 2 ---
Revenue increased by 12% YoY.
--- Page 3 ---
All figures are provisional.
--- Page 4 ---
Contact finance@example.com for details.
```

Jeśli którykolwiek obraz się nie powiedzie (np. uszkodzony plik), odpowiadający `OcrResult` będzie miał pustą właściwość `Text`, a możesz sprawdzić `ocrResults[i].Exception` w celu diagnostyki.

## Jak tworzyć OCR – Wskazówki, przypadki brzegowe i najlepsze praktyki

### Obsługa dużych partii

Przetwarzanie setek plików PNG może nadal zużywać pamięć, jeśli utrzymujesz wszystkie obiekty `OcrResult` w pamięci. W takich przypadkach strumieniuj wyjście do pliku lub bazy danych, gdy tylko pojawi się każdy wynik:

```csharp
recognitionQueue.OnResultReady += (sender, args) =>
{
    File.AppendAllText("OcrOutput.txt",
        $"--- {args.Image.Path} ---{Environment.NewLine}{args.Result.Text}{Environment.NewLine}");
};
```

### Obsługa formatów innych niż PNG

Aspose OCR obsługuje również JPEG, BMP i TIFF od razu. Wystarczy zmienić rozszerzenie pliku na liście lub użyć wyszukiwania z wieloznacznikiem. Te same kroki **c# ocr tutorial** mają zastosowanie — nie są potrzebne zmiany w kodzie.

### Pomijanie pustych stron

Jeśli masz zeskanowane PDF-y, które czasami zawierają puste strony, możesz przefiltrować wyniki:

```csharp
if (!string.IsNullOrWhiteSpace(result.Text))
    // process non‑empty text
```

### Rozważania licencyjne

Wersja ewaluacyjna znakowanie każdej strony znak wodny. W zastosowaniach produkcyjnych upewnij się, że osadzasz plik licencji na początku `Main`:

```csharp
License lic = new License();
lic.SetLicense("Aspose.OCR.lic");
```

### Dostosowywanie równoległości

`MaxDegreeOfParallelism` domyślnie jest ustawione na `Environment.ProcessorCount`. Jeśli zauważysz wysokie zużycie CPU lub presję pamięci, obniż wartość. Odwrotnie, na maszynie wirtualnej w chmurze z wieloma rdzeniami, podnieś ją, aby w pełni wykorzystać sprzęt.

## Podsumowanie

Masz teraz kompletną **rozwiązanie do wsadowego OCR** w C#, które może **ekstrahować tekst z plików PNG**, uruchamiać je równolegle i dostarczać czyste, uporządkowane wyniki. Dzięki współdzieleniu jednego `OcrEngine` nauczyłeś się **tworzyć pipeline OCR**, które są zarówno oszczędne pod względem pamięci, jak i łatwe w utrzymaniu. Ten **c# ocr tutorial** pokazuje również, jak skalować do **wsadowego wyodrębniania tekstu** dla setek obrazów przy użyciu kilku dodatkowych linii.

---

### Co dalej?

* Spróbuj dodać wykrywanie języka (`Engine.Language = Language.AutoDetect`).  
* Eksperymentuj z formatami wyjściowymi — zapisz wyniki do JSON lub CSV dla dalszej analizy.  
* Połącz to wsadowe OCR z krokiem konwersji PDF‑na‑obraz, aby przetwarzać całe zeskanowane dokumenty.

Śmiało dostosowuj równoległość, wymieniaj własne źródła obrazów lub podłącz wyniki do indeksu wyszukiwania. Nie ma ograniczeń, gdy opanujesz **wsadowe OCR** w C#.

Miłego kodowania, niech Twoje uruchomienia OCR będą szybkie i wolne od błędów!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}