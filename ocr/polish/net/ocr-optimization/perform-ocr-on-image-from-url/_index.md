---
title: Wykonaj OCR na obrazie z adresu URL w Rozpoznawaniu obrazu OCR
linktitle: Wykonaj OCR na obrazie z adresu URL w Rozpoznawaniu obrazu OCR
second_title: Aspose.OCR .NET API
description: Poznaj bezproblemową integrację OCR z Aspose.OCR dla .NET. Precyzyjne rozpoznawanie tekstu na obrazach.
weight: 10
url: /pl/net/ocr-optimization/perform-ocr-on-image-from-url/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wykonaj OCR na obrazie z adresu URL w Rozpoznawaniu obrazu OCR

## Wstęp

dziedzinie optycznego rozpoznawania znaków (OCR) Aspose.OCR dla .NET wyróżnia się jako potężne narzędzie, które umożliwia programistom precyzyjne wyodrębnianie treści tekstowych z obrazów. Jeśli chcesz zintegrować funkcje OCR z aplikacją .NET i bez wysiłku rozpoznawać tekst, ten przewodnik krok po kroku przeprowadzi Cię przez proces wykonywania OCR na obrazie z adresu URL.

## Warunki wstępne

Przed przystąpieniem do samouczka upewnij się, że spełnione są następujące wymagania wstępne:

-  Aspose.OCR dla .NET: Upewnij się, że biblioteka Aspose.OCR jest zintegrowana z projektem .NET. Można go pobrać z[strona wydania](https://releases.aspose.com/ocr/net/).

- Środowisko programistyczne: Skonfiguruj działające środowisko programistyczne .NET na swoim komputerze.

## Importuj przestrzenie nazw

W swoim projekcie .NET uwzględnij niezbędne przestrzenie nazw, aby uzyskać dostęp do funkcjonalności Aspose.OCR. Dodaj następujący fragment kodu do swojego projektu:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
```

## Krok 1: Skonfiguruj katalog dokumentów

 Rozpocznij od określenia katalogu, w którym przechowywane są dokumenty. Zastępować`"Your Document Directory"` z rzeczywistą ścieżką do dokumentów.

```csharp
string dataDir = "Your Document Directory";
```

## Krok 2: Uzyskaj obraz do rozpoznania

Podaj adres URL obrazu, na którym chcesz wykonać OCR. Upewnij się, że obraz jest publicznie dostępny.

```csharp
string uri = "https://qph.fs.quoracdn.net/main-qimg-0ff82d0dc3543dcd3b06028f5476c2e4";
```

## Krok 3: Zainicjuj AsposeOcr

Utwórz instancję klasy AsposeOcr, aby uzyskać dostęp do funkcji OCR.

```csharp
AsposeOcr api = new AsposeOcr();
```

## Krok 4: Rozpoznaj obraz

Skorzystaj z biblioteki Aspose.OCR, aby rozpoznać tekst z określonego adresu URL obrazu. Dostosuj ustawienia rozpoznawania w oparciu o swoje wymagania.

```csharp
RecognitionResult result = api.RecognizeImageFromUri(uri, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    RecognitionAreas = new List<Rectangle>()
    {
        new Rectangle(1,3,390,70),
        new Rectangle(1,72,390,70)
    }
});
```

## Krok 5: Wydrukuj wynik

Wyświetl wynik rozpoznania, w tym rozpoznany tekst, obszary i wszelkie ostrzeżenia.

```csharp
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
```

## Krok 6: Wykonaj i zweryfikuj

Uruchom aplikację i jeśli wszystko jest poprawnie skonfigurowane, powinieneś zobaczyć, że proces OCR został pomyślnie wykonany.

```csharp
Console.WriteLine("PerformOCROnImageFromUrl executed successfully");
```

## Wniosek

Dzięki Aspose.OCR dla .NET integracja funkcji OCR z aplikacjami .NET staje się płynnym doświadczeniem. Ten samouczek poprowadził Cię przez proces wykonywania OCR na obrazie z adresu URL, zapewniając podstawy do wykorzystania możliwości rozpoznawania tekstu w swoich projektach.

## Często zadawane pytania

### P1: Czy Aspose.OCR nadaje się do obsługi wielu języków?

Odpowiedź 1: Tak, Aspose.OCR obsługuje rozpoznawanie tekstu w różnych językach, dzięki czemu jest wszechstronny w zastosowaniach międzynarodowych.

### P2: Czy mogę używać Aspose.OCR zarówno do rozpoznawania tekstu jednowierszowego, jak i wielowierszowego?

A2: Absolutnie! Aspose.OCR zapewnia elastyczność rozpoznawania zarówno tekstu jednowierszowego, jak i wielowierszowego, dostosowując się do konkretnego przypadku użycia.

### P3: Czy dostępne są jakieś opcje licencjonowania dla Aspose.OCR?

 Odpowiedź 3: Tak, możesz zapoznać się z opcjami licencjonowania i dokonać zakupów na stronie[Sklep Aspose](https://purchase.aspose.com/buy).

### P4: Czy dostępna jest bezpłatna wersja próbna Aspose.OCR?

 Odpowiedź 4: Tak, możesz wypróbować Aspose.OCR za darmo, odwiedzając stronę[strona z wydaniami](https://releases.aspose.com/).

### P5: Gdzie mogę znaleźć wsparcie lub dyskusje społeczności związane z Aspose.OCR?

 A5: Odwiedź[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) za wsparcie i współpracę ze społecznością.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
