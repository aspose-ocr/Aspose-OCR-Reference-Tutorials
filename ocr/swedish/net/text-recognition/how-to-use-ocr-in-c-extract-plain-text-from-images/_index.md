---
category: general
date: 2026-04-06
description: Hur man använder OCR i C# för att extrahera ren text från JPG‑bilder,
  inklusive kyrilliska tecken. Lär dig att ladda bild för OCR, känna igen text i jpg
  och få pålitliga resultat.
draft: false
keywords:
- how to use OCR
- extract plain text
- extract cyrillic text
- recognize text jpg
- load image for OCR
language: sv
og_description: Hur man använder OCR i C# för att extrahera vanlig text från JPG-filer.
  Denna guide visar hur man laddar bild för OCR, känner igen text i jpg och hanterar
  kyrillisk text.
og_title: Hur man använder OCR i C# – Extrahera ren text från bilder
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Hur man använder OCR i C# – Extrahera vanlig text från bilder
url: /sv/net/text-recognition/how-to-use-ocr-in-c-extract-plain-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder OCR i C# – Extrahera vanlig text från bilder

Har du någonsin undrat **hur man använder OCR** i ett .NET‑projekt utan att kämpa med inhemska bibliotek? Kanske har du en mapp med skannade kvitton, ett fåtal skärmdumpar med kyrilliska bildtexter, eller så behöver du bara dra ut texten ur en JPEG för snabb analys. Den goda nyheten är att Aspose OCR gör hela processen till en barnlek.

I den här handledningen går vi igenom ett komplett, körbart exempel som visar **hur man använder OCR** för att **extrahera vanlig text** från en JPEG‑bild, hur man **laddar bild för OCR**, och till och med hur man **extraherar kyrillisk text** när källspråket inte är latin. I slutet har du en liten konsolapp som skriver ut den igenkända texten direkt i konsolen – inga extra filer, inga mystiska bieffekter.

> **Vad du får**  
> * En steg‑för‑steg‑guide som du kan kopiera‑klistra in i Visual Studio.  
> * Förklaringar till *varför* varje rad är viktig, inte bara *vad* den gör.  
> * Tips för att hantera stora bilder, flera språk och vanliga fallgropar.

## Förutsättningar

Innan vi dyker ner, se till att du har:

* .NET 6 SDK eller senare (koden fungerar även med .NET Core och .NET Framework).  
* Visual Studio 2022 (eller någon annan editor du föredrar).  
* Internetåtkomst första gången du kör exemplet – Aspose OCR laddar ner språkpaket vid behov.  

Om du saknar Aspose OCR NuGet‑paketet täcker vi det i första steget.

## Steg 1 – Installera Aspose OCR via NuGet (och varför det är viktigt)

Steget **ladda bild för OCR** kan inte ske förrän biblioteket finns på plats. Att använda NuGet garanterar att du får de senaste, säkerhetsuppdaterade binärerna och automatiskt drar in eventuella beroenden.

```bash
dotnet add package Aspose.OCR
```

*Varför detta är viktigt*: Aspose OCR levereras med en liten kärn‑DLL och hämtar språkdatan endast när du begär den. Det håller din app lättviktig och undviker att paketera megabyte av oanvända språkfiler.

## Steg 2 – Initiera OCR‑motorn (hjärtat i **hur man använder OCR**)

Att skapa en `OcrEngine`‑instans är den första riktiga kodraden som betyder något för **hur man använder OCR**. Motorn är som standard i “on‑demand”-läge, vilket betyder att den laddar ner språkpaketet första gången du begär ett specifikt språk.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Step 2: Create the engine – it will fetch language data when needed.
var ocrEngine = new OcrEngine();
```

> **Proffstips**: Om du befinner dig bakom en företagsproxy, sätt `OcrEngine.Proxy` innan det första igenkänningsanropet så att nedladdningen lyckas.

## Steg 3 – Välj språk – **Extrahera kyrillisk text** när det behövs

Aspose OCR stödjer dussintals skript. För att **extrahera kyrillisk text**, sätt helt enkelt `Language`‑egenskapen till `OcrLanguage.Cyrillic`. Första gången den här raden körs hämtas kyrilliska modulen (≈ 5 MB) från Asposes CDN.

```csharp
// Step 3: Tell the engine which language to look for.
// This will automatically download the Cyrillic language pack on first use.
ocrEngine.Language = OcrLanguage.Cyrillic;
```

Om din bild bara innehåller latinska tecken kan du ersätta `Cyrillic` med `English`. Samma mönster fungerar för alla stödjade språk.

## Steg 4 – **Ladda bild för OCR** – Från disk eller ström

Nu **laddar vi bild för OCR**. Klassen `System.Drawing.Image` hanterar de flesta vanliga format (JPG, PNG, BMP). Om du kör på en icke‑Windows‑plattform, överväg `ImageSharp` istället, men för den här handledningen räcker den inbyggda typen.

```csharp
using System.Drawing;

// Step 4: Load the picture that holds the text.
using var image = Image.FromFile(@"C:\Images\cyrillic_sample.jpg");
```

> **Varför detta är viktigt**: Att ladda bilden inom ett `using`‑block garanterar att de okontrollerade GDI+‑resurserna frigörs omedelbart, vilket förhindrar minnesläckor i långkörande tjänster.

## Steg 5 – **Känn igen text JPG** – Kör OCR‑processen

Med motorn konfigurerad och bilden laddad, kan vi slutligen **känna igen text jpg**. Metoden `Recognize` returnerar ett `OcrResult` som innehåller den rena strängen, förtroendesiffror och till och med avgränsningsrutor om du behöver dem senare.

```csharp
// Step 5: Perform the recognition.
var ocrResult = ocrEngine.Recognize(image);
```

Om du vill finjustera noggrannheten kan du justera `ocrEngine.Config` (t.ex. aktivera `AutoRotate` eller sätta `TextOrientation`). För de flesta enkla scenarier fungerar standardinställningarna förvånansvärt bra.

## Steg 6 – **Extrahera vanlig text** – Visa resultatet

Den sista delen av **hur man använder OCR** är att hämta den igenkända strängen från `ocrResult` och göra något med den. Här skriver vi helt enkelt ut den till konsolen, vilket också demonstrerar hur man **extraherar vanlig text** från resultatobjektet.

```csharp
// Step 6: Output the plain text to the console.
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(ocrResult.Text);
```

### Förväntad utdata

Om `cyrillic_sample.jpg` innehåller frasen “Привет мир” (Hello world) bör du se:

```
=== Recognized Text ===
Привет мир
```

Om bilden är suddig eller texten för liten kan utdata innehålla fel; du kan inspektera `ocrResult.Confidence` för att avgöra om du ska försöka igen med en bild i högre upplösning.

## Fullt, körbart exempel

Nedan är hela programmet. Kopiera det till ett nytt Console App‑projekt (`dotnet new console`) och kör. Inga extra filer krävs förutom bilden du pekar på.

```csharp
// ---------------------------------------------------------------
// How to Use OCR in C# – Complete Example
// ---------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Install Aspose.OCR via NuGet first (dotnet add package Aspose.OCR)

        // 2️⃣ Initialize the OCR engine – on‑demand language download.
        var ocrEngine = new OcrEngine();

        // 3️⃣ Select Cyrillic to **extract Cyrillic text**.
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // 4️⃣ **Load image for OCR** – change the path to your own file.
        using var image = Image.FromFile(@"YOUR_DIRECTORY\cyrillic_sample.jpg");

        // 5️⃣ **Recognize text jpg** – run the engine.
        var ocrResult = ocrEngine.Recognize(image);

        // 6️⃣ **Extract plain text** – display it.
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Obs**: Ersätt `YOUR_DIRECTORY\cyrillic_sample.jpg` med den faktiska sökvägen till din JPEG‑fil.

## Vanliga frågor & kantfall

### Vad händer om jag behöver **känna igen text jpg** från en ström istället för en fil?

Du kan mata in en `MemoryStream` direkt:

```csharp
using var ms = new MemoryStream(File.ReadAllBytes("myImage.jpg"));
using var img = Image.FromStream(ms);
var result = ocrEngine.Recognize(img);
```

### Hur hanterar jag flera språk i samma bild?

Sätt `ocrEngine.Language` till `OcrLanguage.Multilingual`. Motorn försöker då automatiskt identifiera varje skript, vilket är praktiskt när ett kvitto blandar engelska och kyrilliska.

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

### Min bild är enorm (över 5 MP). Kommer motorn att krångla?

Stora bilder ökar minnesanvändningen och kan sakta ner igenkänningen. En snabb för‑skalning hjälper:

```csharp
var resized = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
var result = ocrEngine.Recognize(resized);
```

### Kan jag få förtroendesiffran för varje rad?

Ja – `ocrResult.Lines` innehåller `Confidence` per rad. Genom att loopa igenom dem kan du filtrera bort resultat med låg förtroendegrad.

```csharp
foreach (var line in ocrResult.Lines)
{
    if (line.Confidence > 0.8)
        Console.WriteLine(line.Text);
}
```

## Proffstips för produktionsklar OCR

* **Cacha språkpaket** – den första nedladdningen kan ta några sekunder; lagra filerna i en känd mapp och sätt `ocrEngine.LanguageDataPath` för att återanvända dem.  
* **Batch‑behandling** – återanvänd en enda `OcrEngine`‑instans för många bilder; att skapa en ny motor per fil ger onödig overhead.  
* **Felfångst** – omslut `Recognize`‑anropet med ett try‑catch‑block. Aspose kastar `OcrException` för korrupta bilder eller format som inte stöds.  
* **Loggning** – registrera `ocrResult.Confidence` så att du senare kan granska vilka sidor som behövde manuell kontroll.

## Slutsats

Vi har just gått igenom **hur man använder OCR** i C# för att **extrahera vanlig text** från en JPEG, demonstrerat stegen för att **ladda bild för OCR**, visat hur man **känner igen text jpg**, och till och med hämtat **kyrillisk text** ur bilden. Exemplet är fullt funktionellt, kräver bara ett NuGet‑paket och kan utökas för att hantera flerspråkiga dokument, batch‑jobb eller real‑tids‑skanning.

Redo för nästa utmaning? Prova att byta ut det kyrilliska språket mot arabiska, experimentera med flaggan `AutoRotate`, eller integrera resultatet i ett sökindex. Möjligheterna är oändliga.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}