---
description: Lär dig hur du sparar OCR‑resultat med Aspose.OCR för .NET – konvertera
  bild till PDF, extrahera text från PNG och spara den igenkända texten som DOCX,
  TXT, PDF eller XLSX.
linktitle: How to Save OCR Result as Document
second_title: Aspose.OCR .NET API
title: Hur man sparar OCR‑resultat som dokument
url: /sv/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så sparar du OCR-resultat som dokument

## Introduktion

I den här handledningen kommer du att upptäcka **hur man sparar OCR**-utdata med Aspose.OCR för .NET. Vi går igenom att känna igen text i en bild och sedan konvertera den texten till populära dokumentformat som DOCX, TXT, PDF och XLSX. I slutet kommer du att kunna automatisera extraktionen av data från bilder och lagra dem som sökbara, redigerbara filer—perfekt för arkivering, rapportering eller vidare bearbetning.

## Snabba svar
- **Vad betyder “how to save ocr”?** Det avser att spara den text som har identifierats från en bild i ett filformat som DOCX, PDF osv.  
- **Vilka format kan jag exportera till?** DOCX, TXT, PDF och XLSX stöds direkt.  
- **Behöver jag en licens?** En gratis provversion fungerar för utvärdering; en kommersiell licens krävs för produktionsanvändning.  
- **Kan jag konvertera bild till PDF direkt?** Ja—spara OCR-resultatet som PDF för att få ett sökbart PDF‑dokument.  
- **Stöds PNG?** Absolut; du kan **extrahera text från PNG**‑bilder med samma API.

## Vad är OCR och varför spara resultat som dokument?

Optisk teckenigenkänning (OCR) omvandlar tryckt eller handskriven text i bilder till maskinläsbara strängar. Att spara dessa strängar som dokument låter dig:

* Skapa sökbara PDF‑filer för efterlevnad.  
* Fyll i kalkylblad (XLSX) för dataanalys.  
* Generera redigerbara rapporter (DOCX).  
* Arkivera ren‑text‑loggar (TXT) för snabb sökning.

## Förutsättningar

Innan vi börjar, se till att du har:

- Aspose.OCR för .NET installerat. Du kan ladda ner det **[here](https://releases.aspose.com/ocr/net/)**.  
- En mapp på din dator som kommer att innehålla källbilderna och utdata‑dokumenten. Uppdatera variabeln `dataDir` i koden så att den pekar på denna mapp.

## Importera namnrymder

Vi behöver några .NET‑namnrymder för att komma åt fil‑I/O och Aspose OCR‑klasserna.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

### Steg 1: Initiera Aspose.OCR

Ange sökvägen till din arbetskatalog och skapa en instans av OCR‑motorn.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Steg 2: Känn igen bild

Skicka bildfilen (t.ex. en PNG) till igenkännaren. Det är här vi **känner igen textbilder** och omvandlar dem till ett `RecognitionResult`.

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### Steg 3: Spara resultat i olika format

Nu exporterar vi den igenkända texten. Välj det format som passar ditt arbetsflöde—oavsett om du behöver **konvertera bild till PDF**, **extrahera text från PNG**, eller generera ett kalkylblad.

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

### Steg 4: Visa framgångsmeddelande

Ett enkelt konsolmeddelande bekräftar att processen slutfördes utan fel.

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

## Vanliga fallgropar & tips

- **Filvägar:** Använd alltid absoluta sökvägar eller se till att `dataDir` slutar med en sökvägsseparator (`\` eller `/`).  
- **Bildkvalitet:** Högupplösta bilder förbättrar noggrannheten; överväg förbehandling (räta upp, brusreducering) för bättre resultat.  
- **Licensläge:** I utvärderingsläge kan utdata innehålla ett vattenmärke; tillämpa en giltig licens för att ta bort det.

## Vanliga frågor

**Q1. Är Aspose.OCR kompatibel med olika bildformat?**  
A1: Ja, Aspose.OCR stöder ett brett spektrum av bildformat, vilket säkerställer flexibilitet i dina OCR‑uppgifter.

**Q2: Kan jag anpassa igenkänningsinställningar för bättre noggrannhet?**  
A2: Absolut! Aspose.OCR tillhandahåller `RecognitionSettings` för att finjustera OCR‑processen enligt dina specifika krav.

**Q3: Finns det en gratis provversion tillgänglig?**  
A3: Ja, du kan komma igång med en gratis provversion **[here](https://releases.aspose.com/)**.

**Q4: Hur kan jag få en tillfällig licens för Aspose.OCR?**  
A4: Tillfälliga licenser kan erhållas **[here](https://purchase.aspose.com/temporary-license/)**.

**Q5: Var kan jag få hjälp eller ansluta till communityn?**  
A5: Gå med i Aspose.OCR‑communityn på **[Aspose Forum](https://forum.aspose.com/c/ocr/16)** för support och diskussioner.

---

**Senast uppdaterad:** 2026-02-12  
**Testat med:** Aspose.OCR 24.11 för .NET  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}