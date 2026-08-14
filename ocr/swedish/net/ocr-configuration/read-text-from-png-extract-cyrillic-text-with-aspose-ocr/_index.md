---
category: general
date: 2026-03-07
description: Lär dig hur du läser text från PNG och extraherar kyrillisk text med
  Aspose OCR, konverterar bilden till text och laddar ner det kyrilliska språkpaketet.
draft: false
keywords:
- read text from png
- extract cyrillic text
- convert image to text
- load image for ocr
- download cyrillic language pack
language: sv
og_description: Lär dig hur du läser text från png, extraherar kyrillisk text och
  konverterar bild till text med Aspose OCR i C#.
og_title: läsa text från png – extrahera kyrillisk text med Aspose OCR
tags:
- Aspose OCR
- C#
- Image Processing
title: Läsa text från PNG – extrahera kyrillisk text med Aspose OCR
url: /sv/net/ocr-configuration/read-text-from-png-extract-cyrillic-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# läs text från png – extrahera kyrillisk text med Aspose OCR

Behöver du **läsa text från png**‑filer och hämta ut kyrilliska tecken? I den här guiden visar vi hur du läser text från png med Aspose OCR, extraherar kyrillisk text och **konverterar bild till text** med bara några rader C#.

Om du någonsin har stirrat på en skärmdump av en rysk faktura och undrat hur du får orden till en sökbar sträng, så har du kommit rätt. Vi går också igenom hur du **laddar ner det kyrilliska språkpaketet** automatiskt, så att du slipper leta efter extra filer.

## Vad du kommer att uppnå

När du är klar med den här tutorialen kan du:

* **Ladda en bild för OCR** direkt från disk eller en ström.  
* Ställa in motorn på **kyrilliskt språk** utan manuella nedladdningar.  
* Köra igenkänning och **extrahera kyrillisk text** från en PNG‑fil.  
* Se den igenkända texten skriven till konsolen – ett rent, rentextresultat som du kan mata in i databaser, sökindex eller någon annan arbetsflöde.

Ingen extern tjänst, inga molnnycklar, bara Aspose OCR‑NuGet‑paketet och några rader C#.

## Förutsättningar

* .NET 6.0 eller senare (koden fungerar på .NET Core, .NET Framework och .NET 5+).  
* Visual Studio 2022 eller någon annan editor du föredrar.  
* Aspose.OCR‑NuGet‑paketet (`dotnet add package Aspose.OCR`).  
* En PNG‑bild som innehåller kyrilliska tecken – till exempel `cyrillic_sample.png` placerad i en mapp som heter `YOUR_DIRECTORY`.

> **Proffstips:** Om du använder Visual Studio, högerklicka på projektet → **Manage NuGet Packages** → sök “Aspose.OCR” och installera den senaste stabila versionen.

---

## Steg 1 – Installera Aspose OCR och skapa motorn

Först behöver vi en OCR‑motorsinstans. Klassen `OcrEngine` är ingångspunkten för alla operationer.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Create an OCR engine – this object holds all settings and results
var ocrEngine = new OcrEngine();
```

> **Varför detta är viktigt:** Motorn kapslar in språkpaket, bilddata och igenkänningsalternativ. Att instansiera den en gång och återanvända den för flera bilder kan förbättra prestandan.

---

## Steg 2 – **ladda bild för ocr** och ange språket

Nu talar vi om för motorn vilken bild som ska bearbetas och vilket språk som ska sökas efter. Att sätta `Language.Cyrillic` laddar automatiskt ner det behövliga språkpaketet första gången den körs.

```csharp
// 1️⃣ Load the PNG that contains Cyrillic text
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_sample.png");

// 2️⃣ Tell Aspose we want to read Cyrillic characters
ocrEngine.Settings.Language = Language.Cyrillic;   // downloads pack if missing
```

> **Edge case:** Om din PNG är stor (över 5 MB) kan du vilja ändra storlek på den först för att snabba upp igenkänningen. `Image`‑egenskapen accepterar också en `Stream`, så du kan ladda från minne, en webb‑request eller en Azure‑Blob utan att röra filsystemet.

---

## Steg 3 – **konvertera bild till text** med ett enda anrop

Igenkänning är så enkelt som att anropa `Recognize()`. Efter detta anrop innehåller `Text`‑egenskapen den extraherade strängen.

```csharp
// Run the OCR engine – this does the heavy lifting
ocrEngine.Recognize();

// Grab the result; it’s plain Unicode text
string extractedText = ocrEngine.Text;
```

> **Vad händer under huven?** Aspose kör en neuronnäts‑baserad klassificerare tränad på miljontals kyrilliska tecken. Biblioteket abstraherar all den komplexiteten, så du får bara ren Unicode.

---

## Steg 4 – Skriv ut resultatet (eller skicka det vidare)

För demonstrationsändamål skriver vi ut texten till konsolen, men du kan lika lätt skriva den till en fil, en databas eller skicka den till ett sökindex.

```csharp
// Show the OCR result in the console
Console.WriteLine("=== Recognized Cyrillic Text ===");
Console.WriteLine(extractedText);
```

**Förväntad output** (förutsatt att `cyrillic_sample.png` innehåller frasen “Привет мир”):

```
=== Recognized Cyrillic Text ===
Привет мир
```

Om utskriften ser förvrängd ut, dubbelkolla att bilden är tydlig och att du har satt `Language.Cyrillic`. Motorn använder som standard engelska, vilket skulle behandla kyrilliska tecken som okända symboler.

---

## Steg 5 – Fullt körbart exempel

Sätter vi ihop allt får du ett självständigt program som du kan kopiera‑klistra in i ett nytt konsolprojekt.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // 2️⃣ Load the PNG and select Cyrillic language
        // -------------------------------------------------
        // Replace the path with the location of your PNG
        ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_sample.png");
        ocrEngine.Settings.Language = Language.Cyrillic; // auto‑downloads pack

        // -------------------------------------------------
        // 3️⃣ Perform recognition
        // -------------------------------------------------
        ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== Recognized Cyrillic Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

Spara filen som `Program.cs`, kör `dotnet run`, så bör du se den kyrilliska texten skrivas ut.

---

## Vanliga frågor & felsökning

| Fråga | Svar |
|----------|--------|
| **Vad händer om språkpaketet inte laddas ner?** | Säkerställ att maskinen har internetåtkomst. Paketet cachas i `%USERPROFILE%\.Aspose\OCR\Languages`. Att radera den mappen tvingar en ny nedladdning. |
| **Kan jag läsa andra språk än kyrilliska?** | Absolut – ersätt `Language.Cyrillic` med `Language.English`, `Language.Arabic` osv. Samma automat‑nedladdningslogik gäller. |
| **Min PNG är brusig – resultatet är dåligt. Vad kan jag göra?** | Förbehandla bilden: öka kontrast, konvertera till gråskala eller applicera ett medianfilter. Aspose OCR erbjuder också `Settings.ImagePreprocess`‑alternativ. |
| **Finns det ett sätt att få bounding‑boxar för varje ord?** | Ja, efter `Recognize()` kan du inspektera `ocrEngine.Regions` som returnerar rektanglar för varje upptäckt ord. |
| **Behöver jag en licens för produktionsbruk?** | Den fria utvärderingen fungerar för upp till 100 sidor. För kommersiella projekt köper du en licens – den tar bort vattenstämpeln och låser upp högpresterande batch‑bearbetning. |

---

## Nästa steg – utöka lösningen

* **Batch‑bearbetning:** Loopa igenom en mapp med PNG‑filer, samla alla texter i en CSV‑fil.  
* **Integration med Azure Cognitive Search:** Indexera de extraherade kyrilliska strängarna för snabb uppslagning.  
* **Kombinera med PDF‑konvertering:** Använd Aspose.PDF för att först konvertera skannade PDF‑filer till PNG, och kör sedan samma OCR‑flöde.  

Alla dessa scenarier återanvänder det grundmönster vi just gått igenom: **ladda bild för OCR → ange språk → igenkänn → använd texten**.

---

## Slutsats

Du vet nu hur du **läser text från png**, **extraherar kyrillisk text** och **konverterar bild till text** med Aspose OCR i C#. Nyckelstegen är att skapa motorn, ladda bilden, välja rätt språk (vilket automatiskt **laddar ner det kyrilliska språkpaketet**), och slutligen anropa `Recognize()`.

Prova med olika bilder, experimentera med `Settings`‑alternativen, och se dina applikationer bli sökbara, flerspråkiga och mycket smartare.  

Lycka till med kodandet, och lämna gärna en kommentar om du stöter på problem!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}