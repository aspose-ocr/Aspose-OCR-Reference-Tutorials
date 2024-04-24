---
title: Przygotuj prostokąty w rozpoznawaniu obrazu OCR
linktitle: Przygotuj prostokąty w rozpoznawaniu obrazu OCR
second_title: Aspose.OCR .NET API
description: Odblokuj potencjał Aspose.OCR dla .NET dzięki naszemu obszernemu przewodnikowi. Dowiedz się krok po kroku jak przygotować prostokąty do rozpoznawania obrazu. Ulepsz swoje aplikacje .NET dzięki płynnej integracji OCR.
type: docs
weight: 11
url: /pl/net/ocr-optimization/prepare-rectangles/
---
## Wstęp

W stale rozwijającym się środowisku technologicznym optyczne rozpoznawanie znaków (OCR) odgrywa kluczową rolę w przekształcaniu obrazów w tekst nadający się do odczytu maszynowego. Aspose.OCR dla .NET wyróżnia się jako solidne rozwiązanie dla programistów poszukujących bezproblemowej integracji możliwości OCR z aplikacjami .NET. W tym obszernym przewodniku omówimy proces przygotowywania prostokątów w rozpoznawaniu obrazów OCR przy użyciu Aspose.OCR dla .NET.

## Warunki wstępne

Zanim przejdziesz do samouczka, upewnij się, że spełniasz następujące wymagania wstępne:

- Praktyczna wiedza na temat programowania .NET.
-  Zainstalowana biblioteka Aspose.OCR dla .NET. Możesz go pobrać[Tutaj](https://releases.aspose.com/ocr/net/).
- Podstawowa znajomość koncepcji rozpoznawania obrazu.

## Importuj przestrzenie nazw

Zacznijmy od zaimportowania niezbędnych przestrzeni nazw, aby rozpocząć naszą przygodę z OCR:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Krok 1: Skonfiguruj katalog dokumentów

 Rozpocznij od określenia katalogu, w którym przechowywane są dokumenty. Zastępować`"Your Document Directory"` z rzeczywistą ścieżką do dokumentów.

```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";

// Zainicjuj instancję AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Krok 2: Rozpoznaj obraz z wieloma prostokątami

tym kroku pokażemy, jak rozpoznać tekst z obrazu za pomocą wielu prostokątów. Wykonaj następujące podetapy:

### 2.1 Zdefiniuj prostokąty

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### 2.2 Wykonaj rozpoznawanie OCR

```csharp
// pierwszy przypadek
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Wyświetl rozpoznany tekst
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## Krok 3: Rozpoznaj obraz za pomocą ustawień rozpoznawania

W tym kroku zaprezentujemy alternatywną metodę wykorzystującą RecognitionSettings do rozpoznawania obrazu:

### 3.1 Zdefiniuj ustawienia rozpoznawania

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### 3.2 Wyświetl rozpoznany tekst

```csharp
// Wyświetl rozpoznany tekst
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Wniosek

Gratulacje! Pomyślnie przeszedłeś proces przygotowania prostokątów w rozpoznawaniu obrazu OCR przy użyciu Aspose.OCR dla .NET. Ten przewodnik umożliwia bezproblemową integrację OCR z aplikacjami .NET, zwiększając ich możliwości rozpoznawania tekstu.

### Często zadawane pytania

### P1: Czy mogę używać Aspose.OCR dla .NET z innymi frameworkami .NET?

O1: Tak, Aspose.OCR dla .NET jest kompatybilny z różnymi frameworkami .NET.

### P2: Czy dostępna jest bezpłatna wersja próbna Aspose.OCR dla .NET?

 A2: Absolutnie! Możesz uzyskać dostęp do bezpłatnego okresu próbnego[Tutaj](https://releases.aspose.com/).

### P3: Jak uzyskać wsparcie dla Aspose.OCR dla .NET?

 A3: Odwiedź[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) za dedykowane wsparcie.

### P4: Czy mogę uzyskać tymczasową licencję do celów testowych?

 Odpowiedź 4: Tak, możesz nabyć licencję tymczasową[Tutaj](https://purchase.aspose.com/temporary-license/).

### P5: Gdzie mogę znaleźć dokumentację Aspose.OCR dla .NET?

 Odpowiedź 5: Dokumentacja jest dostępna[Tutaj](https://reference.aspose.com/ocr/net/).