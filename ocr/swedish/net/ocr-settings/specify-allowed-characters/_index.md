---
date: 2025-12-27
description: Lär dig hur du använder OCR‑bild‑till‑text‑konvertering med Aspose.OCR
  för .NET, specificerar tillåtna tecken och finjusterar OCR‑igenkänningsinställningar.
  Inkluderar kod för att känna igen siffror i en bild.
linktitle: 'ocr image to text: Specify Allowed Characters in OCR'
second_title: Aspose.OCR .NET API
title: 'ocr bild till text: ange tillåtna tecken i OCR'
url: /sv/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ocr image to text: Specificera tillåtna tecken i OCR

## Introduktion

I den ständigt föränderliga teknikvärlden har Optical Character Recognition (OCR) – eller **ocr image to text**‑konvertering – framträtt som ett transformerande verktyg som möjliggör för maskiner att förstå text från bilder. Aspose.OCR för .NET utmärker sig som en kraftfull lösning som erbjuder sömlös integration för utvecklare som söker robusta OCR‑funktioner i sina .NET‑applikationer.

## Snabba svar
- **Vad gör “Specify Allowed Characters”?** Det begränsar OCR‑utdata till en definierad uppsättning symboler, t.ex. endast siffror.  
- **Vilken metod extraherar en enskild textrad?** `RecognizeLine` returnerar den första raden den upptäcker.  
- **Kan jag ändra OCR‑igenkänningsinställningar i realtid?** Ja – använd `RecognitionSettings` för att justera alternativ som `AllowedCharacters`.  
- **Finns en provversion?** Absolut, ladda ner gratisprovet från Aspose‑sajten.  
- **Vilka .NET‑versioner stöds?** Alla moderna .NET Framework‑ och .NET Core/5/6‑versioner.

## Förutsättningar

Innan du dyker ner i handledningen, se till att du har följande förutsättningar på plats:

- En fungerande kunskap om .NET‑utveckling.  
- Aspose.OCR för .NET‑biblioteket. Du kan ladda ner det [här](https://releases.aspose.com/ocr/net/).  
- Bekantskap med Visual Studio eller någon annan föredragen .NET‑utvecklingsmiljö.

## Importera namnrymder

I ditt .NET‑projekt importerar du de nödvändiga namnrymderna för att effektivt utnyttja funktionerna i Aspose.OCR för .NET:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Now, let's break down the tutorial into a series of comprehensive steps:
## Steg 1: Specificera tillåtna tecken i ocr image to text

För att börja, ange sökvägen till din dokumentkatalog:

```csharp
string dataDir = "Your Document Directory";
```

## Steg 2: Initiera Aspose.OCR med tillåtna symboler (igenkänna siffror bild)

Skapa en instans av `AsposeOcr` och specificera de tillåtna symbolerna. I detta fall tillåter vi endast siffror (0‑9):

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

## Steg 3: Känn igen bild

Använd `AsposeOcr`‑instansen för att känna igen text från en bild:

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

## Steg 4: Visa igenkänd text

Skriv ut den igenkända texten till konsolen:

```csharp
Console.WriteLine(result);
```

## Steg 5: Andra fallet – Känn igen bild med specifika OCR‑igenkänningsinställningar

Initiera en annan `AsposeOcr`‑instans, den här gången med mer specifika inställningar som demonstrerar användning av **ocr recognition settings**:

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

## Steg 6: Visa igenkänd text för andra fallet

Skriv ut den igenkända texten från det andra fallet till konsolen:

```csharp
Console.WriteLine(result2.RecognitionText);
```

## Steg 7: Lyckad körning

Slutligen, bekräfta den lyckade körningen av **SpecifyAllowedCharacters**‑handledningen:

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Genom att följa dessa steg har du låst upp möjligheten att **specificera tillåtna tecken** i OCR‑bildigenkänning med Aspose.OCR för .NET, vilket möjliggör exakt **ocr image to text**‑konvertering för scenarier som endast innehåller siffror.

## Varför använda filtrering av tillåtna tecken?

- **Högre noggrannhet:** Att begränsa teckenuppsättningen minskar falska igenkännanden, särskilt i brusiga bilder.  
- **Prestandaförbättring:** OCR‑motorn hoppar över irrelevanta glyfer, vilket snabbar upp bearbetningen.  
- **Efterlevnad:** Tvingar datatyper (t.ex. fakturanummer, serienummer) redan i OCR‑steget.

## Vanliga fallgropar & tips

- **Fallgrop:** Att ange en tom sträng för tillåtna tecken inaktiverar filtreringen.  
  **Tips:** Skicka alltid en icke‑tom sträng eller använd `CharactersAllowedType`‑enum.  
- **Fallgrop:** Att använda `RecognizeLine` på flerradiga dokument kan leda till att data missas.  
  **Tips:** Byt till `RecognizeImage` med `RecognizeSingleLine = false` för fullsidig extraktion.  
- **Fallgrop:** Att glömma att kombinera katalogsökvägen korrekt kan orsaka `FileNotFoundException`.  
  **Tips:** Använd `Path.Combine(dataDir, "file.jpg")` för plattformsoberoende sökvägar.

## Vanliga frågor

**Q: Är Aspose.OCR för .NET lämplig för både nybörjare och erfarna utvecklare?**  
A: Absolut! API‑et är intuitivt för nybörjare samtidigt som det erbjuder avancerade inställningar för erfarna användare.

**Q: Kan jag använda Aspose.OCR för .NET för att känna igen tecken på flera språk?**  
A: Ja, Aspose.OCR stödjer ett brett spektrum av språk; du kan även kombinera språkpaket för flerspråkiga projekt.

**Q: Hur ofta uppdateras Aspose.OCR för .NET?**  
A: Uppdateringar släpps regelbundet för att hålla jämna steg med nya .NET‑releaser och OCR‑förbättringar. Kontrollera [dokumentationen](https://reference.aspose.com/ocr/net/) för den senaste versionen.

**Q: Finns en gratis provversion av Aspose.OCR för .NET?**  
A: Ja, du kan utforska funktionerna genom att ladda ner [gratisprovet](https://releases.aspose.com/).

**Q: Var kan jag söka hjälp eller ansluta till communityn för support?**  
A: Besök [Aspose.OCR‑forumet](https://forum.aspose.com/c/ocr/16) för att interagera med experter och andra utvecklare.

---

**Senast uppdaterad:** 2025-12-27  
**Testat med:** Aspose.OCR 24.11 för .NET  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}