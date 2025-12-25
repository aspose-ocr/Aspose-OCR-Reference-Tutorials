---
date: 2025-12-25
description: Popraw dokładność OCR dzięki Aspose OCR dla .NET, wykorzystując sprawdzanie
  pisowni i obsługę języków, aby korygować błędy ortograficzne oraz dostosowywać słowniki
  do rozpoznawania tekstu bezbłędnie.
linktitle: Improve OCR Accuracy with Spell Checking in Images
second_title: Aspose.OCR .NET API
title: Popraw dokładność OCR dzięki sprawdzaniu pisowni na obrazach
url: /pl/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Popraw dokładność OCR za pomocą sprawdzania pisowni na obrazach

## Wprowadzenie

Kiedy pracujesz z rozpoznawaniem znaków optycznych (OCR), ostatecznym celem jest **poprawić dokładność OCR**, aby wyodrębniony tekst idealnie odpowiadał oryginalnemu obrazowi. Błędnie napisane słowa są częstym źródłem błędów, szczególnie gdy źródłowy obraz jest zaszumiony lub zawiera nietypowe czcionki. Aspose.OCR dla .NET oferuje wbudowane możliwości sprawdzania pisowni, które nie tylko korygują te błędy, ale także pozwalają rozszerzyć silnik o własne słowniki. W tym samouczku dowiesz się, jak używać sprawdzania pisowni, aby zwiększyć wyniki OCR, zobaczysz efekty przed i po oraz odkryjesz, jak dostosować proces korekcji do konkretnych potrzeb językowych.

## Szybkie odpowiedzi
- **Co robi sprawdzanie pisowni dla OCR?** Automatycznie wykrywa błędnie napisane słowa w wyniku OCR i zastępuje je najbardziej prawdopodobnymi poprawnymi alternatywami.  
- **Która biblioteka udostępnia tę funkcję?** Aspose.OCR dla .NET zawiera gotowe do użycia API sprawdzania pisowni.  
- **Czy potrzebuję połączenia z internetem?** Nie, silnik sprawdzania pisowni działa w pełni offline.  
- **Czy mogę dodać własną terminologię?** Tak, możesz dostarczyć własny słownik użytkownika, aby obsłużyć słowa specyficzne dla domeny.  
- **Jakie języki są obsługiwane?** Zobacz sekcję „aspose ocr language support” po szczegóły.

## Czym jest sprawdzanie pisowni w OCR?

Sprawdzanie pisowni analizuje surowy tekst zwrócony przez silnik OCR, identyfikuje tokeny, które nie pasują do znanych słów w wybranym słowniku językowym, i sugeruje lub stosuje poprawki. Ten krok jest niezbędny do **poprawy dokładności OCR**, szczególnie przy przetwarzaniu zeskanowanych dokumentów, paragonów czy formularzy, gdzie OCR może błędnie interpretować znaki.

## Dlaczego używać wsparcia językowego Aspose OCR?

Aspose.OCR dostarcza rozbudowane pakiety językowe i umożliwia podłączanie dodatkowych słowników. Wykorzystanie **aspose ocr language support** pozwala obsługiwać dokumenty wielojęzyczne bez pisania własnych parserów oraz daje dostęp do reguł specyficznych dla języka, które dodatkowo podnoszą jakość rozpoznawania.

## Wymagania wstępne

Zanim przejdziemy do magii sprawdzania pisowni, upewnij się, że masz spełnione następujące wymagania:

- Biblioteka Aspose.OCR dla .NET: Pobierz i zainstaluj bibliotekę Aspose.OCR ze [strony wydania](https://releases.aspose.com/ocr/net/).

- Katalog dokumentów: Upewnij się, że masz wyznaczony katalog dla swoich dokumentów. Zastąp `"Your Document Directory"` w fragmentach kodu rzeczywistą ścieżką.

## Importowanie przestrzeni nazw

Zacznijmy od zaimportowania niezbędnych przestrzeni nazw w Twoim projekcie .NET:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Krok 1: Inicjalizacja Aspose.OCR

Zainicjuj instancję Aspose.OCR, aby rozpocząć proces rozpoznawania.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Krok 2: Rozpoznawanie obrazu

Następnie rozpoznaj tekst na obrazie przy użyciu Aspose.OCR. Oto fragment kodu demonstrujący ten proces:

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Krok 3: Przed korektą

Pobierz wynik OCR przed korektą, aby porównać go z wersją po poprawce.

```csharp
// Get result
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Krok 4: Po korekcie

Zastosuj sprawdzanie pisowni, aby uzyskać skorygowany wynik. Poniższy fragment kodu ilustruje ten krok:

```csharp
// Get corrected result
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Krok 5: Błędnie napisane słowa i sugestie

Uzyskaj listę błędnie napisanych słów wraz z proponowanymi poprawkami, używając następującego kodu:

```csharp
// Get list of misspelled words with suggestions
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

## Krok 6: Korekta tekstu użytkownika

Skoryguj konkretny tekst podany przez użytkownika przy użyciu biblioteki Aspose.OCR:

```csharp
// Correct user text
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Krok 7: Korekta przy użyciu słownika użytkownika

Zwiększ skuteczność korekty, włączając własny słownik użytkownika:

```csharp
// Get corrected result with user dictionary
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Częste problemy i rozwiązania

| Problem | Dlaczego się pojawia | Jak naprawić |
|---------|----------------------|--------------|
| Brak zwróconych sugestii | Pakiet językowy nie został załadowany lub tekst jest zbyt krótki. | Upewnij się, że `RecognitionSettings(Language.Eng)` odpowiada językowi obrazu źródłowego i że wynik OCR zawiera wystarczającą liczbę znaków. |
| Słownik niestandardowy nie został zastosowany | Nieprawidłowa ścieżka lub format pliku. | Sprawdź, czy `dictionary.txt` istnieje w podanej lokalizacji i czy używa jednego słowa w linii. |
| Sprawdzanie pisowni spowalnia przetwarzanie dużych dokumentów | Przetwarzanie każdego słowa osobno generuje dodatkowy narzut. | Przetwarzaj strony w partiach lub zwiększ przydział pamięci, jeśli działasz na .NET Core. |

## Najczęściej zadawane pytania

### P1: Czy mogę używać Aspose.OCR dla języków innych niż angielski?

Tak, Aspose.OCR obsługuje wiele języków. Dostosuj ustawienia językowe odpowiednio.

### P2: Jak zintegrować Aspose.OCR z moim projektem .NET?

Zobacz [dokumentację](https://reference.aspose.com/ocr/net/) po szczegółowe kroki integracji.

### P3: Czy dostępna jest wersja próbna Aspose.OCR?

Tak, możesz wypróbować funkcje za pomocą [darmowej wersji próbnej](https://releases.aspose.com/).

### P4: Czy mogę przesłać własny słownik do sprawdzania pisowni?

Oczywiście! Samouczek pokazuje, jak zwiększyć skuteczność korekcji przy użyciu słownika dostarczonego przez użytkownika.

### P5: Gdzie mogę uzyskać wsparcie dla Aspose.OCR?

Odwiedź [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) po wsparcie społeczności i wskazówki.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Ostatnia aktualizacja:** 2025-12-25  
**Testowane z:** Aspose.OCR dla .NET najnowsza wersja  
**Autor:** Aspose