---
date: 2025-12-27
description: Utforska avancerat OCR-språkstöd och funktioner med Aspose.OCR för .NET.
  Effektivt, exakt och utvecklarvänligt.
linktitle: OCR Language Support – Ignored Characters in Image Recognition
second_title: Aspose.OCR .NET API
title: OCR-språkstöd – Ignorerade tecken i bildigenkänning
url: /sv/net/ocr-settings/specify-ignored-characters/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR-språkstöd: Ange ignorerade tecken i bildigenkänning

## Introduktion

OCR-språkstöd är en hörnsten i modern dokumentautomatisering och gör det möjligt för applikationer att läsa text från bilder över många alfabet och symboler. I den här handledningen lär du dig hur du får **Aspose.OCR for .NET** att ignorera specifika tecken under igenkänning – ett viktigt knep när du behöver renare resultat eller vill filtrera bort brus som sidnummer eller dekorativa symboler. I slutet av guiden har du ett färdigt kodexempel som demonstrerar funktionen från början till slut.

## Snabba svar
- **Vad betyder “ignorerade tecken”?** Tecken som OCR‑motorn hoppar över när den bygger resultatsträngen.  
- **Varför använda det?** Förbättrar noggrannheten när vissa symboler är irrelevanta för din affärslogik.  
- **Vilken API‑metod hanterar det?** `RecognitionSettings.IgnoredCharacters`.  
- **Kan jag kombinera det med språkpaket?** Ja – ignorerade tecken fungerar tillsammans med vilket språk du än laddar.  
- **Krävs en licens?** En tillfällig eller fullständig licens behövs för produktionsanvändning.

## Förutsättningar

Innan du dyker ner i den rika funktionaliteten som Aspose.OCR for .NET erbjuder, se till att du har följande förutsättningar på plats:

1. Aspose.OCR‑installation  

   Säkerställ att du har installerat Aspose.OCR for .NET framgångsrikt. Du hittar de nödvändiga filerna på [download page](https://releases.aspose.com/ocr/net/).

2. Dokumentkataloginställning  

   Skapa en dedikerad katalog för dina dokument. Detta är avgörande för att köra exemplen utan problem. Uppdatera variabeln `dataDir` i exemplen med sökvägen till din dokumentkatalog.

3. Tillfällig licens (valfritt)  

   Om du utforskar Aspose.OCR for .NET med en tillfällig licens, hämta den från [here](https://purchase.aspose.com/temporary-license/).

## Importera namnrymder

För att kickstarta din resa med Aspose.OCR for .NET behöver du importera de nödvändiga namnrymderna. Lägg till följande rader i din kod:

```csharp
using System.IO;

using Aspose.OCR;
using System;
```

## Varför ange ignorerade tecken?

I många verkliga scenarier – såsom bearbetning av fakturor, kvitton eller flerspråkiga formulär – kan du stöta på återkommande tecken som inte är en del av den meningsfulla datan (t.ex. bindestreck som avgränsare, sidnummer eller dekorativa symboler). Genom att tala om för OCR‑motorn att hoppa över dessa minskar du efterbearbetningsarbetet och förbättrar den övergripande tillförlitligheten i efterföljande analyser.

## Steg‑för‑steg‑guide

### Steg 1: Ställ in din dokumentkatalog

Börja med att ange katalogen där dina dokument lagras. Ersätt `"Your Document Directory"` med den faktiska sökvägen till dina dokument.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

### Steg 2: Initiera Aspose.OCR

Skapa en instans av OCR‑motorn. Detta objekt hanterar alla efterföljande igenkänningsanrop.

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Steg 3: Läs av bild med ignorerade tecken

Skicka bildfilen tillsammans med ett `RecognitionSettings`‑objekt som listar de tecken du vill ignorera. I det här exemplet ignorerar vi tecknen `a`, `b` och `1`.

```csharp
// Recognize image with specified ignored characters
RecognitionResult result = api.RecognizeImage(dataDir + "SpanishOCR.bmp", new RecognitionSettings
{
    IgnoredCharacters = "ab1"
});
```

### Steg 4: Visa igenkänd text

Till sist, skriv ut den rensade texten till konsolen eller någon annan mottagare du föredrar.

```csharp
// Display the recognized text
Console.WriteLine(result.RecognitionText);
```

## Vanliga problem & tips

- **Felaktig sökväg:** Säkerställ att `dataDir` avslutas med en sökvägsseparator (`\` eller `/`) som är lämplig för ditt operativsystem.  
- **Ej stödd språk:** OCR‑motorn måste ha språkpaketet för källbilden; annars kommer ignorerade tecken inte att tillämpas korrekt.  
- **Licensfel:** Om du får ett licensundantag, kontrollera att den tillfälliga licensfilen refereras korrekt i ditt projekt.

## Slutsats

Aspose.OCR for .NET ger utvecklare avancerade OCR‑möjligheter och förenklar processen att omvandla bilder till redigerbar och sökbar text. Genom att följa den här steg‑för‑steg‑guiden har du lärt dig hur du exkluderar oönskade tecken, vilket gör dina OCR‑pipelines renare och mer pålitliga. Utforska [documentation](https://reference.aspose.com/ocr/net/) för djupare insikter och upptäck hur Aspose.OCR kan lyfta dina OCR‑projekt.

## Vanliga frågor

### Q1: Kan jag använda Aspose.OCR för .NET i icke‑kommersiella projekt?

A1: Ja, Aspose.OCR for .NET kan användas både i kommersiella och icke‑kommersiella projekt. Se [licensing details](https://purchase.aspose.com/buy) för mer information.

### Q2: Finns det en gratis provperiod?

A2: Självklart! Du kan få en gratis provperiod [here](https://releases.aspose.com/) för att utforska funktionerna och fördelarna med Aspose.OCR for .NET innan du fattar ett beslut.

### Q3: Hur kan jag få support för Aspose.OCR?

A3: För frågor eller hjälp, besök [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) för att komma i kontakt med communityn och söka expertråd.

### Q4: Vilka språk stöder Aspose.OCR?

A4: Aspose.OCR stödjer ett brett spektrum av språk, vilket gör det till ett mångsidigt val för OCR‑uppgifter. Se dokumentationen för den kompletta listan.

### Q5: Kan jag köpa en tillfällig licens för Aspose.OCR?

A5: Ja, om du behöver en tillfällig licens kan du skaffa den [here](https://purchase.aspose.com/temporary-license/) för korttidsanvändning.

**Last Updated:** 2025-12-27  
**Tested With:** Aspose.OCR 23.12 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}