---
category: general
date: 2026-04-01
description: Hur man konverterar OCR‑utdata till JSON och XML i C# – lär dig extrahera
  text från bild och skriva JSON‑fil i C# med Aspose.OCR.
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: sv
og_description: Hur man konverterar OCR‑resultat till strukturerade JSON‑ och XML‑filer
  med C#. Steg‑för‑steg‑guide för att extrahera text från bild och skriva JSON‑fil
  i C#.
og_title: Hur man konverterar OCR till JSON & XML i C# – Skriv JSON‑fil
tags:
- OCR
- C#
- Aspose
title: Hur man konverterar OCR till JSON och XML i C# – Skriva JSON-fil
url: /sv/net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så konverterar du OCR till JSON & XML i C# – Skriv JSON-fil

**Hur du konverterar OCR**‑resultat till något du faktiskt kan använda är en fråga som många utvecklare ställer. I den här guiden visar vi hur du extraherar text från en bild, omvandlar OCR‑utdata till snyggt formaterad JSON och XML, och sedan skriver dessa filer till disk med C#.

Om du någonsin har stirrat på en rå OCR‑sträng och tänkt, “Det måste finnas ett bättre sätt att lagra detta,” så är du på rätt plats. När du är klar har du ett komplett, körbart program som inte bara **extraherar text från bild**‑filer utan också vet hur man **skrivs JSON-fil C#** och **skrivs XML-fil C#** utan att svettas.

## Vad du behöver

- **.NET 6.0** eller senare (koden fungerar även med .NET Framework 4.6+).  
- **Aspose.OCR** NuGet‑paket – installera det med `dotnet add package Aspose.OCR`.  
- En bild som innehåller text (t.ex. `invoice.png`).  
- Valfri IDE – Visual Studio, Rider eller VS Code duger.

> **Proffstips:** Håll dina bildfiler i en dedikerad mapp (t.ex. `Resources/`) så att sökvägarna förblir prydliga.

## Steg 1: Ställ in OCR-motorn – Så konverterar du OCR

Först skapar vi en `OcrEngine`‑instans och talar om för den vilket språk den ska leta efter. I de flesta fall räcker engelska, men du kan byta `Language.English` mot vilket stödjande språk som helst.

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine for English text
        var ocrEngine = new OcrEngine { Language = Language.English };
```

> **Varför detta är viktigt:** Att initiera motorn med rätt språk förbättrar noggrannheten avsevärt, särskilt för icke‑latinska skript.

## Steg 2: Känn igen text – Extrahera text från bild

Nu matar vi bilden till motorn. Metoden `Recognize` returnerar ett `OcrResult`‑objekt som innehåller den råa texten samt positionsdata.

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

Om bilden inte kan hittas kastar `Recognize` ett `FileNotFoundException`. För att hålla demon enkel antar vi att sökvägen är korrekt, men i produktion bör du omsluta detta i ett try‑catch‑block.

## Steg 3: Konvertera resultatet till JSON – Skriv JSON-fil C#

Aspose.OCR gör serialisering till en barnlek. Metoden `ToJson` accepterar en `indent`‑flagga för att producera vackert indenterad output, vilket är perfekt när du planerar att öppna filen i en textredigerare.

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### Förväntat JSON-exempel

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑31\nTotal: $250.00",
  "Regions": [
    {
      "Bounds": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Text": "Invoice #12345"
    }
    // … more regions …
  ]
}
```

> **Hur du extraherar text:** `Text`‑egenskapen ger dig den rena strängen som du kan skicka till andra tjänster (sökindex, databaser osv.).

## Steg 4: Spara JSON – Skriv JSON-fil C# (Fortsättning)

När JSON‑strängen är klar skriver vi den helt enkelt till en fil med `File.WriteAllText`. Detta säkerställer UTF‑8‑kodning som standard.

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

Nu har du en `invoice.json` som ligger bredvid din bild, redo för vidare bearbetning.

## Steg 5: Konvertera resultatet till XML – Skriv XML-fil C#

Om du föredrar XML för äldre system gör `ToXml` det tunga arbetet. Precis som `ToJson` stödjer den också vacker indentering.

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### Förväntat XML-exempel

```xml
<OcrResult>
  <Text>Invoice #12345
Date: 2024-03-31
Total: $250.00</Text>
  <Regions>
    <Region>
      <Bounds X="10" Y="20" Width="200" Height="30" />
      <Text>Invoice #12345</Text>
    </Region>
    <!-- … more regions … -->
  </Regions>
</OcrResult>
```

## Steg 6: Spara XML – Skriv XML-fil C# (Fortsättning)

Att spara XML är identiskt med JSON‑steget; peka bara på en `.xml`‑filändelse.

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### Fullt fungerande exempel

Sätter vi ihop allt får du hela programmet som du kan kopiera‑klistra in i en konsolapp:

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Initialise OCR engine for English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Recognise text from image
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");

        // Convert to JSON and save
        string jsonOutput = ocrResult.ToJson(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);

        // Convert to XML and save
        string xmlOutput = ocrResult.ToXml(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

Kör programmet så hittar du två nya filer—`invoice.json` och `invoice.xml`—precis där du angav dem. Öppna dem för att verifiera att strukturen matchar exemplen ovan.

## Vanliga frågor & kantfall

| Fråga | Svar |
|----------|--------|
| **Vad händer om bilden innehåller flera språk?** | Skapa separata `OcrEngine`‑instanser för varje språk eller använd `Language.Multi` om det stöds. |
| **Kan jag styra utdataformatet (t.ex. exkludera regiondata)?** | Ja. Både `ToJson` och `ToXml` accepterar valfria parametrar för att filtrera fält; se Aspose.OCR‑dokumentationen för `ExportOptions`. |
| **Hur hanterar jag stora PDF-filer med många sidor?** | Bearbeta varje sida individuellt, samla resultaten och serialisera sedan en gång. |
| **Är utdata UTF‑8‑säker?** | Absolut—Aspose.OCR använder Unicode internt, och `File.WriteAllText` skriver UTF‑8 som standard. |
| **Vad gäller prestanda?** | OCR är CPU‑intensivt. För batchjobb överväg att parallellisera över kärnor eller använda Asposes moln‑API. |

## Slutsats

Du vet nu **hur du konverterar OCR**‑resultat till både JSON och XML med C#. Genom att följa stegen ovan kan du **extrahera text från bild**, sedan **skriva JSON-fil C#** och **skriva XML-fil C#** med bara några få rader kod. Detta tillvägagångssätt är snabbt, pålitligt och fungerar med alla bildtyper som Aspose.OCR stödjer.

Redo för nästa utmaning? Prova att mata in the

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}