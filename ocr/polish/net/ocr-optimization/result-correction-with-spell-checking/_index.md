---
date: 2026-04-23
description: Popraw dokładność OCR za pomocą Aspose OCR dla .NET, wykorzystując sprawdzanie
  pisowni, obsługę pakietów językowych OCR oraz własne słowniki, aby zwiększyć jakość
  OCR w zeskanowanych dokumentach.
keywords:
- improve ocr accuracy
- ocr language pack
- process scanned documents
- boost ocr quality
- ocr spell checking
linktitle: Popraw dokładność OCR dzięki sprawdzaniu pisowni na obrazach
second_title: Aspose.OCR .NET API
title: Popraw dokładność OCR dzięki sprawdzaniu pisowni na obrazach
url: /pl/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Popraw dokładność OCR za pomocą sprawdzania pisowni na obrazach

Kiedy pracujesz z rozpoznawaniem znaków optycznych (OCR), ostatecznym celem jest **poprawa dokładności OCR**, aby wyodrębniony tekst idealnie odpowiadał oryginalnemu obrazowi. Błędnie napisane słowa, zaszumione tła i nietypowe czcionki to częste winowajcy, które pogarszają wynik. Łącząc wbudowany silnik sprawdzania pisowni Aspose.OCR z rozbudowanym pakietem językowym OCR, możesz znacząco **zwiększyć jakość OCR** dla każdego zeskanowanego dokumentu.

## Jak poprawić dokładność OCR za pomocą sprawdzania pisowni

W tej sekcji przeprowadzimy Cię przez cały przepływ pracy — od wczytania obrazu, przez zastosowanie sprawdzania pisowni, aż po dopracowanie wyniku przy użyciu własnego słownika użytkownika. Zobaczysz rzeczywiste przykłady przed i po, dowiesz się, dlaczego jest to ważne przy przetwarzaniu zeskanowanych dokumentów, oraz odkryjesz wskazówki, jak maksymalnie wykorzystać funkcję sprawdzania pisowni w OCR.

## Szybkie odpowiedzi
- **Co robi sprawdzanie pisowni dla OCR?** Automatycznie wykrywa błędnie napisane słowa w wyniku OCR i zastępuje je najbardziej prawdopodobnymi poprawnymi alternatywami.  
- **Która biblioteka udostępnia tę funkcję?** Aspose.OCR dla .NET zawiera gotowe do użycia API sprawdzania pisowni.  
- **Czy potrzebuję połączenia z internetem?** Nie, silnik sprawdzania pisowni działa w pełni offline.  
- **Czy mogę dodać własną terminologię?** Tak, możesz dostarczyć własny słownik użytkownika, aby obsłużyć słowa specyficzne dla danej dziedziny.  
- **Jakie języki są obsługiwane?** Zobacz sekcję „aspose ocr language support” po szczegóły.

## Czym jest sprawdzanie pisowni w OCR?

Sprawdzanie pisowni analizuje surowy tekst zwrócony przez silnik OCR, identyfikuje tokeny, które nie pasują do znanych słów w wybranym słowniku językowym, i sugeruje lub stosuje poprawki. Ten krok jest niezbędny do **poprawy dokładności OCR**, szczególnie przy przetwarzaniu zeskanowanych dokumentów, paragonów lub formularzy, w których OCR może błędnie interpretować znaki.

## Dlaczego warto używać pakietu językowego Aspose OCR?

Aspose.OCR dostarcza rozbudowane pakiety językowe i umożliwia podłączanie dodatkowych słowników. Wykorzystanie **aspose ocr language support** oznacza, że możesz obsługiwać dokumenty wielojęzyczne bez pisania własnych parserów oraz uzyskasz dostęp do reguł specyficznych dla języka, które dodatkowo poprawiają jakość rozpoznawania.

## Wymagania wstępne

Zanim zagłębimy się w magię sprawdzania pisowni, upewnij się, że masz spełnione następujące wymagania:

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

Zainicjalizuj instancję Aspose.OCR, aby rozpocząć proces OCR.

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

Pobierz wynik OCR przed korektą, aby porównać go z wersją po korekcie.

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

Uzyskaj listę błędnie napisanych słów wraz z sugerowanymi poprawkami, używając poniższego kodu:

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

## Krok 6: Poprawianie tekstu użytkownika

Popraw konkretny tekst dostarczony przez użytkownika przy użyciu biblioteki Aspose.OCR:

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

## Wskazówki, jak zwiększyć jakość OCR

- **Wybierz odpowiedni pakiet językowy OCR**, który pasuje do dokumentu źródłowego. Użycie `Language.Eng` w dokumencie francuskim znacznie obniży dokładność.  
- **Wstępnie przetwarzaj obrazy** (prostowanie, usuwanie szumów, zwiększanie kontrastu) przed przekazaniem ich do silnika OCR; czystsze obrazy generują mniej błędów pisowni.  
- **Utrzymuj zwięzły słownik użytkownika** — jedno słowo na linię — aby sprawdzarka pisowni mogła szybko znaleźć niestandardowe terminy bez spowalniania dużych partii.  
- **Przetwarzaj strony w partiach** przy obsłudze wielostronicowych plików PDF; zmniejsza to zużycie pamięci i przyspiesza fazę sprawdzania pisowni.

## Typowe problemy i rozwiązania

| Problem | Dlaczego się pojawia | Jak naprawić |
|---------|----------------------|--------------|
| Brak zwróconych sugestii | Pakiet językowy nie jest załadowany lub tekst jest zbyt krótki. | Upewnij się, że `RecognitionSettings(Language.Eng)` odpowiada językowi obrazu źródłowego i że wynik OCR zawiera wystarczającą liczbę znaków. |
| Niestandardowy słownik nie został zastosowany | Nieprawidłowa ścieżka lub format pliku. | Sprawdź, czy `dictionary.txt` istnieje w podanej lokalizacji i używa jednego słowa na linię. |
| Sprawdzarka pisowni spowalnia duże dokumenty | Przetwarzanie każdego słowa osobno generuje dodatkowy narzut. | Przetwarzaj strony w partiach lub zwiększ przydział pamięci, jeśli uruchamiasz na .NET Core. |

## Najczęściej zadawane pytania

### P1: Czy mogę używać Aspose.OCR dla języków innych niż angielski?

O1: Tak, Aspose.OCR obsługuje wiele języków. Dostosuj odpowiednio ustawienia języka.

### P2: Jak zintegrować Aspose.OCR z moim projektem .NET?

O2: Odwołaj się do [dokumentacji](https://reference.aspose.com/ocr/net/) po szczegółowe kroki integracji.

### P3: Czy dostępna jest wersja próbna Aspose.OCR?

O3: Tak, możesz przetestować funkcje za pomocą [bezpłatnej wersji próbnej](https://releases.aspose.com/).

### P4: Czy mogę wgrać własny słownik do sprawdzania pisowni?

O4: Absolutnie! Samouczek pokazuje, jak zwiększyć skuteczność korekty przy użyciu słownika dostarczonego przez użytkownika.

### P5: Gdzie mogę uzyskać wsparcie dla Aspose.OCR?

O5: Odwiedź [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) po wsparcie społeczności i wskazówki.

---

**Ostatnia aktualizacja:** 2026-04-23  
**Testowano z:** Aspose.OCR for .NET latest version  
**Autor:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}