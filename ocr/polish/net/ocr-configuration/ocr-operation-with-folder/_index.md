---
title: OCR Operacja z folderem w trybie rozpoznawania obrazu OCR
linktitle: OCR Operacja z folderem w trybie rozpoznawania obrazu OCR
second_title: Aspose.OCR .NET API
description: Odblokuj moc rozpoznawania obrazów OCR w .NET dzięki Aspose.OCR. Wyodrębnij tekst z obrazów bez wysiłku.
weight: 11
url: /pl/net/ocr-configuration/ocr-operation-with-folder/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Operacja z folderem w trybie rozpoznawania obrazu OCR

## Wstęp

Witamy w świecie optycznego rozpoznawania znaków (OCR) przy użyciu Aspose.OCR dla .NET! Jeśli chcesz płynnie wyodrębniać tekst z obrazów w aplikacjach .NET, jesteś we właściwym miejscu. Ten samouczek poprowadzi Cię przez proces rozpoznawania obrazów OCR z folderami, wykorzystując potężne możliwości Aspose.OCR.

## Warunki wstępne

Przed przystąpieniem do samouczka upewnij się, że spełniasz następujące wymagania wstępne:

- Praktyczna znajomość programowania w C# i .NET.
- Program Visual Studio zainstalowany na Twoim komputerze.
-  Biblioteka Aspose.OCR dla .NET, którą możesz pobrać[Tutaj](https://releases.aspose.com/ocr/net/).
- Podstawowa znajomość koncepcji OCR.

## Importuj przestrzenie nazw

W kodzie C# pamiętaj o zaimportowaniu przestrzeni nazw niezbędnych do korzystania z Aspose.OCR. Na początku skryptu umieść następujące informacje:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Krok 1: Ustaw katalog dokumentów

```csharp
// ExStart:1
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";
```

Upewnij się, że zastąpiłeś „Twój katalog dokumentów” rzeczywistą ścieżką, w której przechowywane są Twoje obrazy.

## Krok 2: Zainicjuj Aspose.OCR

```csharp
// Zainicjuj instancję AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Utwórz instancję klasy AsposeOcr, aby wykorzystać jej funkcjonalności.

## Krok 3: Określ ścieżkę obrazu

```csharp
//Ścieżka obrazu
string fullPath = dataDir + "OCR";
```

Połącz ścieżkę katalogu dokumentów z określonym folderem zawierającym obrazy.

## Krok 4: Rozpoznaj obrazy

```csharp
// Rozpoznaj obraz
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
    //domyślny lub niestandardowy
});
```

Użyj metody RecognizeMultipleImages, aby wykonać OCR na wielu obrazach w określonym folderze.

## Krok 5: Wydrukuj wyniki

```csharp
// Wydrukuj wynik
for (int i = 0; i < result.Length; i++)
{
    Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
```

Przejrzyj wyniki i wydrukuj rozpoznany tekst dla każdego obrazu.

## Krok 6: Wniosek

```csharp
// RozwińKoniec:1
Console.WriteLine("OCROperationWithFolder executed successfully");
```

Upewnij się, że skrypt został zakończony, co oznacza pomyślne wykonanie operacji OCR na folderach.

## Wniosek

Gratulacje! Pomyślnie nauczyłeś się, jak wdrożyć rozpoznawanie obrazów OCR w folderach przy użyciu Aspose.OCR dla .NET. To potężne narzędzie otwiera mnóstwo możliwości wyodrębniania tekstu z obrazów w aplikacjach .NET.

## Często zadawane pytania

### P1: Czy mogę używać Aspose.OCR dla .NET w projektach komercyjnych?

 O1: Tak, Aspose.OCR dla .NET jest produktem komercyjnym. Informacje dotyczące licencji można znaleźć na stronie[Tutaj](https://purchase.aspose.com/buy).

### Pytanie 2:. Czy dostępny jest bezpłatny okres próbny?

 Odpowiedź 2: Tak, możesz skorzystać z bezpłatnego okresu próbnego[Tutaj](https://releases.aspose.com/).

### P3: Gdzie mogę znaleźć dokumentację?

 A3: Dokumentacja jest dostępna[Tutaj](https://reference.aspose.com/ocr/net/).

### P4: Jak mogę uzyskać licencję tymczasową?

 A4: Można uzyskać licencje tymczasowe[Tutaj](https://purchase.aspose.com/temporary-license/).

### P5: Potrzebujesz wsparcia lub masz pytania?

 A5: Odwiedź[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) za wsparcie społeczności.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
