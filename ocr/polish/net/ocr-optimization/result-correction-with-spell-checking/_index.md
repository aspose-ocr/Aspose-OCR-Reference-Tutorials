---
title: Korekta wyników poprzez sprawdzanie pisowni w rozpoznawaniu obrazu OCR
linktitle: Korekta wyników poprzez sprawdzanie pisowni w rozpoznawaniu obrazu OCR
second_title: Aspose.OCR .NET API
description: Zwiększ dokładność OCR dzięki Aspose.OCR dla .NET. Poprawiaj pisownię, dostosowuj słowniki i bezproblemowo rozpoznawaj tekst bez błędów.
weight: 13
url: /pl/net/ocr-optimization/result-correction-with-spell-checking/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Korekta wyników poprzez sprawdzanie pisowni w rozpoznawaniu obrazu OCR

## Wstęp

dziedzinie optycznego rozpoznawania znaków (OCR) uzyskanie dokładnych wyników ma kluczowe znaczenie dla wydobycia znaczących informacji z obrazów. Częstym wyzwaniem jest radzenie sobie z błędnie napisanymi słowami w procesie rozpoznawania. Na szczęście Aspose.OCR dla .NET zapewnia potężne rozwiązanie poprawiające wyniki OCR poprzez sprawdzanie pisowni.

Ten samouczek poprowadzi Cię przez proces poprawiania wyników poprzez sprawdzanie pisowni przy użyciu Aspose.OCR dla .NET. Na koniec będziesz mieć możliwość poprawy dokładności tekstu pochodzącego z OCR, zapewniając bardziej dopracowany i wolny od błędów wynik.

## Warunki wstępne

Zanim zagłębimy się w magię sprawdzania pisowni, upewnij się, że spełniasz następujące wymagania wstępne:

-  Biblioteka Aspose.OCR dla .NET: Pobierz i zainstaluj bibliotekę Aspose.OCR z[strona wydania](https://releases.aspose.com/ocr/net/).

- Katalog dokumentów: Upewnij się, że masz wyznaczony katalog na swoje dokumenty. Zastąp „Twój katalog dokumentów” we fragmentach kodu rzeczywistą ścieżką.

## Importuj przestrzenie nazw

Zacznijmy od zaimportowania niezbędnych przestrzeni nazw do Twojego projektu .NET:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Krok 1: Zainicjuj Aspose.OCR

Zainicjuj instancję Aspose.OCR, aby rozpocząć proces OCR.

```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";

// Zainicjuj instancję AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Krok 2: Rozpoznaj obraz

Następnie rozpoznaj tekst na obrazie za pomocą Aspose.OCR. Oto fragment demonstrujący ten proces:

```csharp
// Rozpoznaj obraz
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Krok 3: Przed korektą

Pobierz wynik OCR przed korektą, aby porównać go z poprawioną wersją.

```csharp
// Uzyskaj wynik
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Krok 4: Po korekcie

Zastosuj sprawdzanie pisowni, aby uzyskać poprawiony wynik. Poniższy fragment kodu ilustruje ten krok:

```csharp
// Uzyskaj poprawiony wynik
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Krok 5: Błędnie napisane słowa i sugestie

Uzyskaj listę błędnie napisanych słów wraz z sugerowanymi poprawkami, korzystając z następującego kodu:

```csharp
// Uzyskaj listę błędnie napisanych słów z sugestiami
List<SpellCheckError> errorsList = result.GetSpellCheckErrorList(SpellCheckLanguage.Eng);
foreach (var word in errorsList)
{
	Console.Write("Word:" + word.Word);
	Console.Write(" StartPosition:" + word.StartPosition);
	Console.WriteLine(" Length:" + word.Length);
	Console.WriteLine("SuggestedWords:");
	foreach (var suggest in word.SuggestedWords)
	{
		Console.Write(suggest.Word + " ");
	}
	Console.WriteLine();
}
```

## Krok 6: Popraw tekst użytkownika

Popraw konkretny tekst dostarczony przez użytkownika, korzystając z biblioteki Aspose.OCR:

```csharp
// Popraw tekst użytkownika
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Krok 7: Korekta za pomocą słownika użytkownika

Jeszcze bardziej ulepsz korekcję, włączając niestandardowy słownik użytkownika:

```csharp
// Uzyskaj poprawiony wynik za pomocą słownika użytkownika
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Wniosek

Gratulacje! Udało Ci się nawigować po możliwościach sprawdzania pisowni Aspose.OCR dla .NET. Ta funkcja umożliwia udoskonalenie wyników OCR, zapewniając dokładność i eliminując błędy.

## Często zadawane pytania

### P1: Czy mogę używać Aspose.OCR w językach innych niż angielski?

O1: Tak, Aspose.OCR obsługuje wiele języków. Dostosuj odpowiednio ustawienia języka.

### P2: Jak zintegrować Aspose.OCR z moim projektem .NET?

 Odpowiedź 2: Patrz[dokumentacja](https://reference.aspose.com/ocr/net/) szczegółowe kroki integracji.

### P3: Czy dostępna jest wersja próbna Aspose.OCR?

 Odpowiedź 3: Tak, możesz eksplorować funkcje za pomocą[bezpłatna wersja próbna](https://releases.aspose.com/).

### P4: Czy mogę przesłać niestandardowy słownik do sprawdzania pisowni?

A4: Absolutnie! W samouczku pokazano, jak ulepszyć korektę za pomocą słownika dostarczonego przez użytkownika.

### P5: Gdzie mogę szukać wsparcia dla Aspose.OCR?

 A5: Odwiedź[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) o wsparcie i wskazówki społeczności.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
