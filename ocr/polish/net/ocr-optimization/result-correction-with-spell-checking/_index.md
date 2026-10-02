---
date: 2026-04-29
description: Popraw dokładność OCR i dowiedz się, jak rozpoznawać tekst z obrazu przy
  użyciu Aspose OCR dla .NET, wykorzystując sprawdzanie pisowni i obsługę języków
  do korekty błędów oraz dostosowywania słowników.
keywords:
- improve ocr accuracy
- recognize text from image
- Aspose OCR spell checking
- custom OCR dictionary
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

Kiedy pracujesz z rozpoznawaniem znaków optycznych (OCR), ostatecznym celem jest **poprawa dokładności OCR**, aby wyodrębniony tekst idealnie odpowiadał oryginalnemu obrazowi. Błędnie napisane słowa są częstym źródłem błędów, szczególnie gdy obraz źródłowy jest zaszumiony lub zawiera nietypowe czcionki. Aspose.OCR dla .NET oferuje wbudowane funkcje sprawdzania pisowni, które nie tylko korygują te błędy, ale także pozwalają rozszerzyć silnik o własne słowniki. W tym samouczku dowiesz się, jak używać sprawdzania pisowni, aby zwiększyć wyniki OCR, zobaczysz efekty przed i po oraz odkryjesz, jak dostosować proces korekcji do konkretnych potrzeb językowych.

## Szybkie odpowiedzi
- **Co robi sprawdzanie pisowni dla OCR?** Automatycznie wykrywa błędnie napisane słowa w wyniku OCR i zastępuje je najbardziej prawdopodobnymi poprawnymi alternatywami.  
- **Która biblioteka zapewnia tę funkcję?** Aspose.OCR for .NET zawiera gotowe do użycia API sprawdzania pisowni.  
- **Czy potrzebuję połączenia z internetem?** Nie, silnik sprawdzania pisowni działa całkowicie offline.  
- **Czy mogę dodać własną terminologię?** Tak, możesz dostarczyć własny słownik użytkownika, aby obsługiwać słowa specyficzne dla domeny.  
- **Jak to pomaga mi rozpoznawać tekst z obrazu?** Poprzez korektę błędów wygenerowanych przez OCR, końcowy tekst staje się czysty i gotowy do dalszego przetwarzania.

## Czym jest sprawdzanie pisowni w OCR?
Sprawdzanie pisowni analizuje surowy tekst zwrócony przez silnik OCR, identyfikuje tokeny, które nie pasują do znanych słów w wybranym słowniku językowym, i sugeruje lub stosuje poprawki. Ten krok jest niezbędny dla **poprawy dokładności OCR**, szczególnie przy przetwarzaniu zeskanowanych dokumentów, paragonów czy formularzy, w których OCR może błędnie interpretować znaki.

## Dlaczego warto używać wsparcia językowego Aspose OCR?
Aspose.OCR ships with extensive language packs and allows you to plug in additional dictionaries. Leveraging **aspose ocr language support** means you can handle multilingual documents without writing custom parsers, and you gain access to language‑specific rules that further improve recognition quality.

## Kiedy poprawa dokładności OCR ma największe znaczenie?
- **Dokumenty prawne i zgodności** , w których pojedynczy błąd może zmienić znaczenie.  
- **Potoki ekstrakcji danych** , które przekazują wyniki OCR do analiz lub modeli AI.  
- **Aplikacje skierowane do klientów** takie jak mobilne skanery, które muszą natychmiast zwracać czytelny tekst.  

## Wymagania wstępne

Zanim zagłębimy się w magię sprawdzania pisowni, upewnij się, że masz spełnione następujące wymagania:

- Aspose.OCR for .NET Library: Pobierz i zainstaluj bibliotekę Aspose.OCR ze [strony wydania](https://releases.aspose.com/ocr/net/).
- Document Directory: Upewnij się, że masz wyznaczony katalog dla swoich dokumentów. Zastąp `"Your Document Directory"` w fragmentach kodu rzeczywistą ścieżką.

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

## Krok 6: Korekta tekstu użytkownika

Skoryguj konkretny tekst podany przez użytkownika przy użyciu biblioteki Aspose.OCR:

```csharp
// Correct user text
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Krok 7: Korekta przy użyciu słownika użytkownika

Ulepsz korektę, włączając własny słownik użytkownika:

```csharp
// Get corrected result with user dictionary
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Typowe problemy i rozwiązania
| Problem | Dlaczego się dzieje | Jak naprawić |
|-------|----------------|------------|
| Brak zwróconych sugestii | Pakiet językowy nie jest załadowany lub tekst jest zbyt krótki. | Upewnij się, że `RecognitionSettings(Language.Eng)` odpowiada językowi obrazu źródłowego i że wynik OCR zawiera wystarczającą liczbę znaków. |
| Niestandardowy słownik nie został zastosowany | Nieprawidłowa ścieżka lub format pliku. | Sprawdź, czy `dictionary.txt` istnieje w podanej lokalizacji i używa jednego słowa w linii. |
| Sprawdzanie pisowni spowalnia duże dokumenty | Przetwarzanie każdego słowa osobno zwiększa obciążenie. | Przetwarzaj strony w partiach lub zwiększ przydział pamięci, jeśli uruchamiasz na .NET Core. |

## Często zadawane pytania

**Q1: Czy mogę używać Aspose.OCR dla języków innych niż angielski?**  
A1: Tak, Aspose.OCR obsługuje wiele języków. Dostosuj odpowiednio ustawienia języka.

**Q2: Jak zintegrować Aspose.OCR z moim projektem .NET?**  
A2: Zapoznaj się z [dokumentacją](https://reference.aspose.com/ocr/net/) po szczegółowe kroki integracji.

**Q3: Czy dostępna jest wersja próbna Aspose.OCR?**  
A3: Tak, możesz przetestować funkcje za pomocą [bezpłatnej wersji próbnej](https://releases.aspose.com/).

**Q4: Czy mogę wgrać własny słownik do sprawdzania pisowni?**  
A4: Oczywiście! Tutorial pokazuje, jak ulepszyć korektę przy użyciu słownika dostarczonego przez użytkownika.

**Q5: Gdzie mogę uzyskać wsparcie dla Aspose.OCR?**  
A5: Odwiedź [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) aby uzyskać wsparcie społeczności i wskazówki.

---

**Ostatnia aktualizacja:** 2026-04-29  
**Testowano z:** Aspose.OCR for .NET latest version  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}