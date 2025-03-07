---
title: Zapisz wynik jako dokument w rozpoznawaniu obrazu OCR
linktitle: Zapisz wynik jako dokument w rozpoznawaniu obrazu OCR
second_title: Aspose.OCR .NET API
description: Odblokuj potencjał Aspose.OCR dla .NET. Z łatwością rozpoznaj tekst na obrazach i zapisuj wyniki w różnych formatach dokumentów.
weight: 10
url: /pl/net/ocr-settings/save-result-as-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zapisz wynik jako dokument w rozpoznawaniu obrazu OCR

## Wstęp

Witamy w ekscytującym świecie optycznego rozpoznawania znaków (OCR) z Aspose.OCR dla .NET! W tym obszernym samouczku zagłębimy się w zawiłości używania Aspose.OCR do rozpoznawania tekstu na obrazach i pokażemy, jak zapisywać wyniki w różnych formatach dokumentów.

## Warunki wstępne

Zanim rozpoczniemy przygodę z OCR, upewnij się, że spełniasz następujące wymagania wstępne:

-  Aspose.OCR dla .NET. Upewnij się, że masz zainstalowaną bibliotekę Aspose.OCR. Możesz go pobrać[Tutaj](https://releases.aspose.com/ocr/net/).

-  Katalog dokumentów: Przygotuj wyznaczony katalog na swoje dokumenty i aktualizuj go`dataDir` odpowiednio zmienna w dostarczonym kodzie.

## Importuj przestrzenie nazw

Rozpocznij od zaimportowania niezbędnych przestrzeni nazw. Są to elementy składowe, które wyposażą Twój kod w funkcje OCR.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Podzielmy teraz przykład na kilka kroków:

## Krok 1: Zainicjuj Aspose.OCR

```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";

// Zainicjuj instancję AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Ten krok przygotowuje etap poprzez inicjowanie interfejsu API Aspose.OCR.

## Krok 2: Rozpoznaj obraz

```csharp
// Rozpoznaj obraz
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

W tym przypadku używamy Aspose.OCR do rozpoznawania tekstu w określonym obrazie (zamień „sample.png” na plik obrazu).

## Krok 3: Zapisz wynik w różnych formatach

```csharp
// Zapisz wynik w preferowanym formacie
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

Dostosuj ten krok do swoich potrzeb. Aspose.OCR umożliwia zapisanie rozpoznanego tekstu w różnych formatach dokumentów, takich jak DOCX, TXT, PDF i XLSX.

## Krok 4: Wyświetl komunikat o powodzeniu

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

Prosty komunikat potwierdzający informujący, że proces zakończył się bez żadnych problemów.

Wykonując te kroki, z powodzeniem wykorzystałeś moc Aspose.OCR dla .NET w rozpoznawaniu tekstu w obrazach i zapisywaniu wyników w różnych formatach dokumentów.

## Wniosek

Podsumowując, Aspose.OCR dla .NET otwiera świat możliwości rozpoznawania tekstu w obrazach. Niezależnie od tego, czy wyodrębniasz dane, czy tworzysz dokumenty z możliwością przeszukiwania, Aspose.OCR upraszcza proces dzięki intuicyjnemu interfejsowi API.

## Często zadawane pytania

### Pytanie 1. Czy Aspose.OCR jest kompatybilny z różnymi formatami obrazów?

Odpowiedź 1: Tak, Aspose.OCR obsługuje szeroką gamę formatów obrazów, zapewniając elastyczność w zadaniach OCR.

### P2: Czy mogę dostosować ustawienia rozpoznawania, aby uzyskać większą dokładność?

A2: Absolutnie! Aspose.OCR zapewnia ustawienia rozpoznawania, aby dostroić proces OCR zgodnie z Twoimi konkretnymi wymaganiami.

### P3: Czy dostępny jest bezpłatny okres próbny?

 Odpowiedź 3: Tak, możesz rozpocząć korzystanie z bezpłatnego okresu próbnego[Tutaj](https://releases.aspose.com/).

### P4: Jak mogę uzyskać tymczasowe licencje na Aspose.OCR?

 A4: Można uzyskać licencje tymczasowe[Tutaj](https://purchase.aspose.com/temporary-license/).

### P5: Gdzie mogę szukać pomocy lub nawiązać kontakt ze społecznością?

 A5: Dołącz do społeczności Aspose.OCR pod adresem[Forum Aspose](https://forum.aspose.com/c/ocr/16) za wsparcie i dyskusję.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
