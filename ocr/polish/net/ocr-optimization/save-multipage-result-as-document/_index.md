---
date: 2025-12-30
description: Dowiedz się, jak konwertować obrazy na PDF w C# przy użyciu Aspose.OCR,
  zapisywać wyniki OCR wielostronicowe jako dokumenty oraz wyodrębniać tekst z obrazów
  w C#.
linktitle: Convert Images to PDF C# – Save Multipage OCR Result
second_title: Aspose.OCR .NET API
title: Konwertuj obrazy na PDF C# – Zapisz wynik OCR wielostronicowy
url: /pl/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwertuj obrazy do PDF C# – Zapisz wynik OCR wielostronicowy

## Wprowadzenie

W tym samouczku dowiesz się, jak **convert images to PDF C#** przy użyciu Aspose.OCR dla .NET i zapisać wynikowy wielostronicowy wynik OCR jako dokument. Niezależnie od tego, czy potrzebujesz **convert scanned images to PDF** do archiwizacji, czy **extract text from images C#** do przetwarzania danych, ten przewodnik przeprowadzi Cię przez każdy krok — wraz z rzeczywistymi przykładami i wskazówkami najlepszych praktyk.

## Szybkie odpowiedzi
- **Co obejmuje ten samouczek?** Konwertowanie wielu obrazów do PDF/Docx/Txt/Pdf/Xlsx przy użyciu Aspose.OCR w C#.
- **Jakie formaty są obsługiwane?** Docx, Text, Pdf i Xlsx (można także bezpośrednio wyjść PDF).
- **Czy potrzebna jest licencja?** Darmowa wersja próbna działa w ocenie; stała licencja jest wymagana w produkcji.
- **Jakie wersje .NET są kompatybilne?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
- **Czy mogę wyodrębnić tekst podczas konwersji?** Tak — użyj wyników OCR, aby pobrać tekst przed zapisem.

## Co to jest „convert images to PDF C#”?

Konwertowanie obrazów do PDF w C# oznacza programowe pobranie jednego lub kilku plików bitmap (PNG, JPEG, TIFF itp.) i wygenerowanie dokumentu PDF, który zachowuje układ wizualny, jednocześnie opcjonalnie osadzając przeszukiwalny tekst za pomocą OCR. Aspose.OCR sprawia, że proces ten jest prosty i wysoce konfigurowalny.

## Dlaczego używać Aspose.OCR do tego zadania?

- **Wysoka dokładność** silnika OCR, który działa z wieloma językami.
- **Obsługa wielu stron** – obsługa partii obrazów w jednym wywołaniu.
- **Bezpośredni zapis** do popularnych formatów biurowych bez dodatkowych kroków konwersji.
- **Pełna integracja z .NET** – brak natywnych zależności lub zewnętrznych narzędzi.

## Wymagania wstępne

1. Zainstaluj Aspose.OCR dla .NET. Możesz pobrać go [tutaj](https://releases.aspose.com/ocr/net/).
2. Uzyskaj darmową wersję próbną lub zakupioną licencję – wersję próbną znajdziesz [tutaj](https://releases.aspose.com/), a zakup [tutaj](https://purchase.aspose.com/buy).
3. Przejrzyj oficjalną [dokumentację](https://reference.aspose.com/ocr/net/), aby zapoznać się z interfejsem API.
4. Dołącz do społeczności na [forum wsparcia](https://forum.aspose.com/c/ocr/16), aby uzyskać pomoc w razie problemów.

Teraz, gdy wszystko jest gotowe, rozpocznijmy kodowanie.

## Importowanie przestrzeni nazw

Rozpocznij od dodania wymaganych przestrzeni nazw do pliku C#:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

Te importy zapewniają dostęp do kolekcji, obsługi plików, LINQ oraz klas Aspose OCR.

## Krok 1: Ustaw katalog dokumentów

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

Zastąp `"Your Document Directory"` absolutną lub względną ścieżką, w której znajdują się Twoje obrazy źródłowe i gdzie chcesz zapisać pliki wyjściowe.

## Krok 2: Zainicjalizuj Aspose.OCR

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Utworzenie obiektu `AsposeOcr` zapewnia dostęp do wszystkich operacji OCR, w tym przepływu pracy **convert images to PDF C#**.

## Krok 3: Rozpoznaj obrazy

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

Metoda `RecognizeMultipleImages` przetwarza każdy plik na liście i zwraca kolekcję `RecognitionResult`. Możesz podać dowolną liczbę obrazów, co jest idealne w scenariuszach **convert scanned images to PDF**.

## Krok 4: Zapisz wyniki w preferowanych formatach

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

Wybierz format, który najlepiej pasuje do Twojego dalszego przepływu pracy:

- **Docx** – edytowalny dokument Word z przeszukiwalnym tekstem.
- **Text** – wyodrębnianie zwykłego tekstu do szybkiego przetwarzania danych (**extract text from images C#**).
- **Pdf** – klasyczny wynik PDF, idealny do archiwizacji.
- **Xlsx** – reprezentacja arkusza kalkulacyjnego dla danych tabelarycznych.

## Typowe przypadki użycia

- **Cyfrowe archiwizowanie:** Konwertuj zeskanowane papierowe umowy na przeszukiwalne pliki PDF.
- **Automatyzacja wprowadzania danych:** Wyodrębnij tekst z paragonów lub faktur i wprowadź go do bazy danych.
- **Przetwarzanie wsadowe:** Obsłuż tysiące obrazów w jednym zadaniu przy minimalnym kodzie.

## Rozwiązywanie problemów i wskazówki

- **Duże zestawy obrazów:** Przetwarzaj obrazy w mniejszych partiach, aby uniknąć skoków pamięci.
- **Jakość obrazu:** Upewnij się, że obrazy mają co najmniej 300 dpi dla optymalnej dokładności OCR.
- **Błędy licencji:** Sprawdź, czy plik licencji jest poprawnie załadowany przed wywołaniem metod OCR.

## Najczęściej zadawane pytania (oryginalne)

### P1: Czy dostępna jest tymczasowa licencja do celów testowych?
A1: Tak, możesz uzyskać tymczasową licencję [tutaj](https://purchase.aspose.com/temporary-license/) do testowania Aspose.OCR.

### P2: Czy mogę rozpoznawać tekst z obrazów w różnych formatach?
A2: Oczywiście! Aspose.OCR obsługuje różne formaty obrazów, zapewniając elastyczność w zadaniach OCR.

### P3: Czy istnieją ograniczenia liczby obrazów do rozpoznania?
A3: Liczba obrazów, które możesz przetworzyć, zależy od Twojej licencji. Sprawdź dokumentację po szczegóły.

### P4: Jak mogę obsłużyć błędy podczas rozpoznawania OCR?
A4: Odwołaj się do dokumentacji w celu uzyskania najlepszych praktyk obsługi błędów lub poproś o pomoc na forum wsparcia.

### P5: Czy Aspose.OCR obsługuje języki inne niż angielski?
A5: Tak, Aspose.OCR obsługuje wiele języków. Zapoznaj się z dokumentacją, aby uzyskać szczegóły dotyczące obsługi języków.

## Dodatkowe najczęściej zadawane pytania

**P:** Czy mogę konwertować obrazy do PDF C# bez użycia OCR?  
**O:** Tak, możesz użyć Aspose.PDF lub innych bibliotek do czystej konwersji obrazu na PDF, ale OCR dodaje przeszukiwalny tekst.

**P:** Jak wyodrębnić tekst z obrazów C# po konwersji?  
**O:** Lista `result` zwrócona przez `RecognizeMultipleImages` zawiera właściwości `Text`, które możesz zapisać do pliku `.txt` lub przetworzyć bezpośrednio.

**P:** Czy można ustawić własne marginesy strony lub orientację?  
**O:** Podczas zapisywania do PDF lub Docx możesz zmodyfikować układ dokumentu za pomocą API Aspose.Words lub Aspose.PDF przed wywołaniem `SaveMultipageDocument`.

**P:** Co się stanie, jeśli obraz nie może zostać odczytany?  
**O:** Silnik OCR zwróci pusty `RecognitionResult` dla tej strony; możesz sprawdzić `result[i].Text` pod kątem wartości null lub pustych ciągów i odpowiednio obsłużyć.

**P:** Czy API obsługuje wdrożenia w chmurze?  
**O:** Tak, biblioteka działa na dowolnym środowisku .NET, w tym Azure Functions i AWS Lambda, pod warunkiem spełnienia wymagań wersji środowiska.

---

**Last Updated:** 2025-12-30  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}