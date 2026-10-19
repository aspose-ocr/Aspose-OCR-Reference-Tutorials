---
category: general
date: 2026-04-01
description: Dowiedz się, jak szybko rozpoznawać tekst z plików PNG, ustawiając identyfikator
  urządzenia GPU i włączając przyspieszenie GPU w Aspose OCR. Przewodnik krok po kroku
  w C#.
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: pl
og_description: Rozpoznawaj tekst z plików PNG szybko, ustawiając identyfikator urządzenia
  GPU. Skorzystaj z tego pełnego przewodnika C#, aby włączyć przyspieszenie GPU w
  Aspose OCR.
og_title: Rozpoznawanie tekstu z PNG – przyspieszony GPU poradnik Aspose OCR
tags:
- C#
- OCR
- GPU
- Aspose
title: Rozpoznawanie tekstu z PNG przy użyciu Aspose OCR – przyspieszona GPU demonstracja
  wsadowa
url: /pl/net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznawanie tekstu z png – Pełny samouczek wsadowy przyspieszony GPU w C#

Czy kiedykolwiek potrzebowałeś **rozpoznawać tekst z png** obrazów, ale proces okazał się wyjątkowo wolny? Nie jesteś sam. Większość programistów zaczyna od prostego wywołania OCR, a potem patrzy na konsolę, która porusza się jak ślimak, gdy folder zawiera dziesiątki zrzutów ekranu.  

Dobre wieści? Aspose OCR może przenieść ciężką pracę na Twoją kartę graficzną, a przy kilku linijkach kodu możesz **set gpu device id**, aby wybrać dokładnie ten GPU, którego chcesz używać. W tym przewodniku przejdziemy przez kompletny, gotowy do uruchomienia przykład, który pobiera wszystkie PNG z folderu, włącza przyspieszenie GPU, wybiera pierwszy GPU i wypisuje liczbę znaków dla każdego pliku.

Pod koniec będziesz mieć samodzielny program, który możesz wrzucić do dowolnego projektu .NET, i zrozumiesz, dlaczego włączenie GPU ma znaczenie, jak radzić sobie z przypadkami brzegowymi oraz co dostroić, aby uzyskać jeszcze lepszą wydajność.

## Czego będziesz potrzebować

- **.NET 6.0** lub nowszy (kod kompiluje się także z .NET Core).  
- Pakiet NuGet **Aspose.OCR** – zainstaluj go poleceniem `dotnet add package Aspose.OCR`.  
- Maszyna z kompatybilnym z CUDA GPU (zwykle NVIDIA) oraz odpowiednim sterownikiem.  
- Folder pełen **PNG** obrazów, które chcesz przetworzyć.  

Jeśli którykolwiek z tych elementów jest Ci nieznany, nie panikuj. Poniższe kroki zawierają dokładne polecenia, których potrzebujesz, a także omówimy, co zrobić, gdy GPU nie jest dostępny.

## Krok 1: Inicjalizacja silnika OCR i włączenie przyspieszenia GPU  

Pierwszą rzeczą, którą musisz zrobić, jest utworzenie instancji `OcrEngine` i włączenie obsługi GPU. Ten znacznik mówi Aspose, aby używał natywnych bibliotek CUDA pod maską.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**Dlaczego to ważne:** Bez `UseGpuAcceleration` każdy obraz jest przetwarzany na CPU, co może być o rzędy wielkości wolniejsze, szczególnie przy wysokiej rozdzielczości PNG. Włączenie tego flagi przygotowuje silnik również do przyjęcia konkretnego urządzenia GPU później.

## Krok 2: Ustawienie identyfikatora urządzenia GPU (opcjonalne, ale zalecane)  

Jeśli Twoja stacja robocza ma więcej niż jeden GPU, możesz zdecydować, którego użyć. Identyfikatory urządzeń zaczynają się od **0**, więc `0` wybiera pierwszy GPU, `1` drugi i tak dalej.

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**Pro tip:** Działając na współdzielonym serwerze, jawne ustawienie identyfikatora GPU może zapobiec przejmowaniu zasobów przez Twoje zadanie z innych procesów. Jeśli pominiesz tę linię, Aspose wybierze domyślne urządzenie, co zazwyczaj wystarcza w konfiguracji z jednym GPU.

## Krok 3: Zebranie wszystkich plików PNG z folderu wsadowego  

Następnie musimy zlokalizować każdy PNG, który ma zostać poddany OCR. Metoda `Directory.GetFiles` wykona ciężką pracę.

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**Przypadek brzegowy:** Jeśli folder jest pusty, `imageFiles` będzie pustą tablicą. Poradzimy sobie z tym później, wyświetlając przyjazny komunikat.

## Krok 4: Przetwarzanie każdego obrazu i wyświetlanie liczby rozpoznanych znaków  

Teraz główna pętla. Dla każdego PNG wywołujemy `Recognize`, a następnie wypisujemy nazwę pliku i długość wyodrębnionego tekstu.

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**Co zobaczysz:**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

Jeśli obraz nie zawiera tekstu, liczba będzie równa `0`. To całkowicie normalne dla zrzutów ekranu, które są wyłącznie graficzne.

## Krok 5: Uruchomienie programu i weryfikacja użycia GPU  

Skompiluj plik (`dotnet build`) i uruchom go (`dotnet run`). Gdy konsola przewija się, możesz otworzyć narzędzie monitorujące GPU (np. NVIDIA Smi), aby zobaczyć krótkie skoki wykorzystania GPU dla każdego obrazu. Jeśli nie widzisz żadnej aktywności, sprawdź ponownie:

1. Czy sterownik CUDA jest zainstalowany.  
2. Czy `UseGpuAcceleration` jest ustawione na `true`.  
3. Czy poprawny `GpuDeviceId` odpowiada fizycznemu GPU.

Jeśli GPU nie jest dostępny, Aspose automatycznie przełączy się na CPU, ale utracisz przewagę prędkości.

## Typowe warianty i wskazówki  

| Sytuacja | Co zmienić |
|-----------|------------|
| **Inny format obrazu** (np. JPEG) | Zmień wzorzec wyszukiwania na `*.jpg` lub `*.*`, a Aspose nadal rozpozna tekst. |
| **Rozmiar partii jest ogromny** (tysiące plików) | Przetwarzaj w partiach, aby uniknąć obciążenia pamięci: podziel `imageFiles` na mniejsze tablice. |
| **Potrzebny jest rzeczywisty tekst, a nie tylko długość** | Zamień `ocrResult.Text.Length` na `ocrResult.Text` w `WriteLine`. |
| **Uruchamianie na serwerze bez interfejsu graficznego** | Upewnij się, że serwer ma sterownik GPU; w przeciwnym razie ustaw `UseGpuAcceleration = false`, aby uniknąć niepotrzebnych błędów. |
| **Wiele GPU, chcesz równoważyć obciążenie** | W pętli `foreach` ustaw `ocrEngine.GpuDeviceId = i % gpuCount`, aby rotować urządzenia. |

## Oczekiwany wynik i weryfikacja  

Gdy wszystko działa, konsola wypisuje nazwę każdego pliku wraz z liczbą znaków, jak pokazano wcześniej. Aby podwójnie sprawdzić rzeczywisty wynik OCR, możesz tymczasowo wyświetlić tekst:

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

Pamiętaj tylko, aby usunąć lub zakomentować tę linię przy dużych partiach; drukowanie tysięcy linii może przytłoczyć Twój terminal.

## Pełny działający przykład (gotowy do kopiowania i wklejania)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

Zapisz to jako `GpuBatchDemo.cs`, uruchom `dotnet add package Aspose.OCR`, a następnie `dotnet run`. Powinieneś zobaczyć liczbę znaków pojawiającą się prawie natychmiast dla każdego PNG, dzięki przyspieszeniu GPU.

## Zakończenie  

Teraz wiesz, jak **rozpoznawać tekst z png** plików efektywnie, włączając przyspieszenie GPU i wyraźnie **set gpu device id** w Aspose OCR. Kompletny, gotowy do kopiowania program obsługuje wykrywanie folderu, sprawdzanie przypadków brzegowych i daje natychmiastową informację zwrotną o wydajności OCR.  

Co dalej? Spróbuj zamienić wywołanie `Recognize` na `ocrEngine.RecognizeAsync`, jeśli potrzebujesz przetwarzania asynchronicznego, lub poeksperymentuj z różnymi opcjami wstępnego przetwarzania obrazu (np. binaryzacja), które oferuje Aspose. Możesz także skierować wyniki OCR do bazy danych lub indeksu wyszukiwania, aby uzyskać rozwiązanie pełnotekstowego przeszukiwania.

Masz pytania dotyczące obsługi wielostronicowych PDF‑ów lub chcesz porównać Aspose OCR z Tesseract? Dodaj komentarz lub zapoznaj się z innymi naszymi samouczkami o **batch OCR C#**, **OCR performance tips** i **GPU‑driven image processing**. Szczęśliwego kodowania!  

![Wyjście konsoli pokazujące rozpoznane liczby znaków dla plików PNG – rozpoznawanie tekstu z png przy użyciu przyspieszenia GPU](image-placeholder.png "przykład wyjścia rozpoznawania tekstu z png")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}