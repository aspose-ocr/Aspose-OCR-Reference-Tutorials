---
category: general
date: 2026-03-05
description: Hur man använder OCR i C# för att extrahera text från en bild. Lär dig
  att konvertera bild till text, läsa koreanska tecken och snabbt ladda bild för OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert image to text
- read korean characters
- load image for OCR
language: sv
og_description: Hur man använder OCR i C# och omedelbart extraherar text från en bild.
  Denna guide visar hur man konverterar bild till text, läser koreanska tecken och
  laddar bild för OCR.
og_title: Hur man använder OCR i C# – Extrahera text från bild
tags:
- OCR
- C#
- Aspose
title: Hur man använder OCR i C# – Extrahera text från bild
url: /sv/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder OCR i C# – Extrahera text från bild

Har du någonsin funderat **hur man använder OCR** när du har en skärmdump full av koreansk text och du behöver den rena strängen tillbaka? Du är inte den enda som kliar sig i huvudet över detta. I den här handledningen går vi igenom ett komplett, färdigt exempel som **extraherar text från bild**, **konverterar bild till text**, och till och med visar hur du **läser koreanska tecken** med Aspose.OCR.

Vi kommer också att täcka det ofta förbisedda steget **ladda bild för OCR** så att du inte får en “fil ej hittad”-överraskning senare. När du är klar har du ett självständigt program som du kan släppa in i vilket .NET‑projekt som helst.

## Vad du behöver

- .NET 6+ (eller .NET Framework 4.7.2 och senare) – koden fungerar på båda.
- Aspose.OCR för .NET – du kan hämta en gratis provversion från Aspose‑webbplatsen.
- En exempelbild (`korean_doc.png`) som innehåller koreansk text.
- Din favorit‑IDE (Visual Studio, Rider, VS Code – vad du än föredrar).

Inga andra tredjepartsbibliotek krävs.

## Steg 1: Skapa projektet och lägg till Aspose.OCR

Först, skapa en ny konsolapp:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Lägg sedan till Aspose.OCR‑NuGet‑paketet:

```bash
dotnet add package Aspose.OCR
```

> **Proffstips:** Om du har en licensfil, placera den i projektets rot; annars fungerar gratisprovversionen men lägger till ett vattenmärke i resultatet.

## Steg 2: Hur man använder OCR – Initiera motorn

Nu skriver vi C#‑koden. Det första du gör när du **hur man använder OCR** är att instansiera `OcrEngine`. Detta objekt är bibliotekets hjärta; det innehåller alla inställningar du kommer att behöva senare.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: apply your license to remove trial limitations
            // Replace the path with the actual location of your .lic file
            ocrEngine.SetLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Varför detta är viktigt:** Utan en korrekt motorinstans kan du inte ange språk, ladda bilder eller hämta resultat. Motorn hanterar också interna resurser, så att skapa den en gång och återanvända den är mer effektivt än att upprepade gånger konstruera nya objekt.

## Steg 3: Välj språk – Läs koreanska tecken

Nästa rad talar om för motorn vilket språk den ska leta efter. Eftersom vårt mål är att **läsa koreanska tecken**, sätter vi `OcrLanguage.Korean`. Du kan byta ut detta mot Arabiska, Thai, Gujarati osv., beroende på ditt användningsfall.

```csharp
            // Step 3: Tell the engine which language to recognize
            ocrEngine.Language = OcrLanguage.Korean; // alternatives: Arabic, Thai, Gujarati, etc.
```

**Varför det är viktigt:** Språkval förbättrar noggrannheten dramatiskt. OCR‑motorn använder språk‑specifika ordböcker och teckenmodeller; om du matar in fel språk kan du få förvrängd utskrift.

## Steg 4: Ladda bild för OCR – Konvertera bild till text

Innan motorn kan göra något arbete måste du **ladda bild för OCR**. Metoden `ImageStream.FromFile` läser filen till ett format som motorn förstår.

```csharp
            // Step 4: Load the image that contains the text
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/korean_doc.png");
```

Om bilden ligger i en annan mapp, justera bara sökvägen. Kom ihåg att sätta filens *Build Action* till “Copy if newer” så att den körbara filen kan hitta den vid körning.

> **Vanligt fallgropp:** Att ange en sökväg med bakåtsnedstreck (`\`) i en strängliteral utan att escapea dem ger ett kompileringsfel. Använd antingen dubbla bakåtsnedstreck (`\\`) eller en verbatim‑sträng (`@"C:\path\file.png"`).

## Steg 5: Utför OCR – Extrahera text från bild

Nu sker det tunga arbetet. Anropet `Recognize()` kör OCR‑algoritmen, och egenskapen `Text` ger dig den råa strängen.

```csharp
            // Step 5: Run OCR and get the recognized text
            string recognizedText = ocrEngine.Recognize().Text;
```

Vid detta steg har du **extraherat text från bild** och effektivt **konverterat bild till text**. Resultatet kan innehålla radbrytningar om den ursprungliga layouten hade dem.

## Steg 6: Visa resultatet – Verifiera utskriften

Till sist, skriv ut resultatet till konsolen så att du kan verifiera att det fungerade.

```csharp
            // Step 6: Output the result to the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

Kör programmet:

```bash
dotnet run
```

### Förväntad utskrift

```
=== Recognized Text ===
안녕하세요. 이것은 OCR 테스트 문서입니다.
```

Om du ser koreanska tecken som liknar bilden, grattis – du har bemästrat **hur man använder OCR** med Aspose.OCR!

![how to use OCR example diagram](image.png)

*Bildtext: hur man använder OCR‑exempeldiagram som visar flödet från att ladda en bild till att skriva ut erkänd text.*

## Edge Cases & Variationer

### 1. Hantera flera sidor

Om du behöver **extrahera text från bild**‑filer som innehåller flera sidor (t.ex. en multi‑sidig TIFF), loopa över varje sida och anropa `Recognize()` för varje `ImageStream`‑instans.

### 2. Hantera lågkvalitativa skanningar

Lågre lösningsbilder kan försämra noggrannheten. Innan du anropar `Recognize()` kan du förbättra bilden med Asposes förbehandlingsverktyg:

```csharp
ocrEngine.Image = ImageProcessing.Preprocess(ocrEngine.Image, ImageProcessingOptions.Deskew);
```

### 3. Byta språk i farten

Anta att du har ett dokument med blandade språk. Du kan ändra `ocrEngine.Language` mellan igenkänningar:

```csharp
ocrEngine.Language = OcrLanguage.English;
string english = ocrEngine.Recognize().Text;

ocrEngine.Language = OcrLanguage.Korean;
string korean = ocrEngine.Recognize().Text;
```

### 4. Spara resultatet till en fil

Om du föredrar att **konvertera bild till text** och lagra den, skriv bara strängen till en `.txt`‑fil:

```csharp
System.IO.File.WriteAllText("output.txt", recognizedText);
```

## Vanliga frågor

- **Behöver jag en licens för att köra den här koden?**  
  Nej. Gratisprovet fungerar bra för experiment, men lägger till ett vattenmärke i resultatet. En köpt licens tar bort vattenmärket och låser upp full prestanda.

- **Kan jag använda detta på Linux?**  
  Absolut. Aspose.OCR är plattformsoberoende; se bara till att du har de nödvändiga inhemska beroendena (libgdiplus för .NET Core på Linux).

- **Vad händer om min bild är i en ström istället för en fil?**  
  Använd `ImageStream.FromStream(yourStream)` – API‑et accepterar vilken `System.IO.Stream` som helst.

## Slutsats

Vi har steg för steg gått igenom **hur man använder OCR** i C# för att **extrahera text från bild**, **konvertera bild till text**, och **läsa koreanska tecken** samtidigt som vi korrekt **laddar bild för OCR**. Det kompletta, körbara exemplet ovan bör fungera direkt, och de extra tipsen ger dig en färdplan för mer avancerade scenarier.

Redo för nästa utmaning? Prova att byta till ett annat språk, bearbeta PDF‑filer sida för sida, eller integrera OCR‑anropet i ett webb‑API så att användare kan ladda upp bilder och få omedelbara textextraktioner. Möjligheterna är oändliga, och nu har du en solid grund att bygga vidare på.

Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}