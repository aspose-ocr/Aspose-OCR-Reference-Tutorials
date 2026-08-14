---
category: general
date: 2026-03-07
description: Lär dig hur du använder OCR i C# för att extrahera text från bildfiler.
  Denna guide visar offline‑OCR, konvertera bild till text och ladda bild för OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- convert image to text
- load image for ocr
language: sv
og_description: Hur man använder OCR i C# för att extrahera text från bilder offline.
  Steg‑för‑steg kod, tips och fullständig förklaring för att konvertera bild till
  text.
og_title: Hur man använder OCR i C# – Komplett offlineguide
tags:
- OCR
- C#
- Aspose
title: Hur man använder OCR i C# – Extrahera text från bilder offline
url: /sv/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-offline/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder OCR i C# – Extrahera text från bilder offline

Har du någonsin funderat **hur man använder OCR** i ett .NET‑projekt utan att skicka data till molnet? Du är inte ensam. Många utvecklare behöver *extrahera text från bild*‑filer på en säker arbetsstation, och de är rädda för att nätverkstrafik kan avslöja känslig information.  

Den goda nyheten? Med Aspose.OCR kan du känna igen text från PNG‑, JPEG‑ eller PDF‑filer helt offline. I den här handledningen går vi igenom hur du laddar en bild för OCR, konfigurerar motorn för offline‑läge och slutligen **konverterar bild till text** med bara några rader C#.

När du är klar med guiden kommer du att kunna:

* Installera Aspose.OCR‑paketet från NuGet.  
* Ställa in OCR‑motorn för offline‑bearbetning.  
* Ladda en bild för OCR och extrahera dess textinnehåll.  

Ingen extern tjänst, inga API‑nycklar – bara ren C#‑kod som körs på vilken Windows‑ eller Linux‑maskin som helst.

---

## Förutsättningar

Innan vi dyker ner, se till att du har:

* .NET 6.0 SDK eller senare (koden fungerar även med .NET Framework 4.7+).  
* Visual Studio 2022, VS Code eller någon editor som stödjer C#.  
* En kopia av **Aspose.OCR**‑biblioteket – du kan hämta det från NuGet (`Aspose.OCR`).  
* En OCR‑resursmapp (`Resources`) som följer med biblioteket (innehåller språkdatafiler).  
* En exempelbild (t.ex. `offline_test.png`) placerad i en känd katalog.

> **Pro tip:** Ha resursmappen bredvid din körbara fil; det förenklar `ResourcesPath`‑konfigurationen.

---

## Steg 1: Installera Aspose.OCR‑paketet från NuGet

Först lägger du till biblioteket i ditt projekt. Öppna en terminal i projektmappen och kör:

```bash
dotnet add package Aspose.OCR
```

Eller, om du föredrar Visual Studios UI, högerklicka **Dependencies → Manage NuGet Packages**, sök efter *Aspose.OCR* och klicka **Install**.

> Att installera paketet hämtar alla nödvändiga binärer, så du behöver inga extra DLL‑filer.

---

## Steg 2: Skapa och konfigurera OCR‑motorn (Hur man använder OCR – Offline‑läge)

Nu instansierar vi OCR‑motorn och talar om för den att arbeta **offline**. Detta säkerställer att ingen nätverkstrafik sker under igenkänning.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Switch the engine to offline mode – crucial for privacy‑first apps
ocrEngine.Settings.EngineMode = EngineMode.Offline;
```

**Varför offline?**  
När `EngineMode` är satt till `Online` kontaktar motorn Asposes moln för att ladda ner språkpaket i farten. I reglerade miljöer (finans, sjukvård) är sådan trafik ofta förbjuden. Genom att tvinga offline‑läge garanterar du att allt stannar på den lokala maskinen.

---

## Steg 3: Peka motorn mot OCR‑resursmappen

OCR‑motorn behöver språkdata (tränade modeller) för att känna igen tecken. Ange var dessa filer finns:

```csharp
// Replace with the absolute or relative path to your Resources folder
ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";
```

Om du är osäker på var mappen är, leta upp den under NuGet‑paketkatalogen (`%USERPROFILE%\.nuget\packages\aspose.ocr\*\resources`). Kopiera hela mappen till ditt projekt för enklare distribution.

---

## Steg 4: Ladda bilden för OCR (Load Image for OCR)

Du kan mata motorn med vilken stödjande bitmap som helst. Här laddar vi en PNG från disk:

```csharp
// Load the image you want to recognize – this is the “load image for OCR” step
ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");
```

**Tips:** Om du behöver bearbeta bilder från en ström (t.ex. uppladdad via ett API), använd `ImageStream.FromStream(yourStream)` istället.

---

## Steg 5: Kör igenkänningsprocessen och konvertera bild till text

När allt är på plats, trigga OCR. Metoden `Recognize()` gör det tunga arbetet, och den extraherade texten blir tillgänglig via egenskapen `Text`.

```csharp
// Perform OCR – this is where the engine reads the pixels and produces text
ocrEngine.Recognize();

// Grab the result – now you have “convert image to text” completed
string extractedText = ocrEngine.Text;
```

---

## Steg 6: Skriv ut den extraherade texten

Till sist visar vi resultatet. I en konsolapp kan du helt enkelt skriva till konsolen, men i ett web‑API returnerar du strängen som JSON.

```csharp
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(extractedText);
```

När programmet körs bör det skriva ut textinnehållet i `offline_test.png`. Till exempel, om bilden innehåller frasen *“Hello, World!”*, kommer du att se:

```
=== OCR Result ===
Hello, World!
```

---

## Fullt fungerande exempel

Nedan är det kompletta, körklara programmet. Kopiera‑klistra in det i ett nytt konsolprojekt (`dotnet new console`) och justera sökvägarna så att de matchar din miljö.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // Step 2: Set offline mode – no network traffic
        // -------------------------------------------------
        ocrEngine.Settings.EngineMode = EngineMode.Offline;

        // -------------------------------------------------
        // Step 3: Provide path to OCR resource files
        // -------------------------------------------------
        ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";

        // -------------------------------------------------
        // Step 4: Load the image you want to recognize
        // -------------------------------------------------
        ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");

        // -------------------------------------------------
        // Step 5: Run recognition and extract text
        // -------------------------------------------------
        ocrEngine.Recognize();
        string extractedText = ocrEngine.Text;

        // -------------------------------------------------
        // Step 6: Show the result
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);
    }
}
```

> **Förväntad output:** Konsolen skriver exakt den text som finns i PNG‑filen. Om bilden är suddig kan resultatet innehålla felaktigt igenkända tecken – se felsökningsavsnittet nedan.

---

## Vanliga fallgropar & tips (Recognize Text from PNG Efficiently)

| Problem | Varför det händer | Hur du åtgärdar |
|---------|-------------------|-----------------|
| **Tomt resultat** | `ResourcesPath` pekar på fel mapp eller språkfiler saknas. | Kontrollera att mappen innehåller `eng.traineddata` (eller andra språkfiler) och dubbelkolla söksträngen. |
| **Skräptecken** | Bildens upplösning är för låg eller bilden är inte binäriserad. | Förbehandla bilden (öka DPI, applicera `ImageProcessor` för att skärpa). |
| **Prestandaproblem** | Stora bilder bearbetas i full upplösning. | Ändra storlek på bilden till max 2000 px i bredd innan du skickar den till OCR. |
| **Ej stödformat** | Använder en BMP med ett ovanligt pixelformat. | Konvertera bilden till PNG eller JPEG först (`System.Drawing.Image.Save`). |

**Pro tip:** Om du behöver känna igen flera språk, sätt `ocrEngine.Settings.Language = Language.English | Language.French;` innan du anropar `Recognize()`.

---

## Vanliga frågor

**Q: Kan jag använda den här koden på Linux?**  
Absolut. Aspose.OCR är plattformsoberoende; se bara till att de inhemska biblioteken finns (de levereras med NuGet‑paketet).  

**Q: Vad gör jag om jag inte har en Resources‑mapp?**  
Du kan ladda ner de fria språkpaketen från Asposes webbplats eller extrahera dem från NuGet‑paketet (`.../aspose.ocr/<version>/resources`).  

**Q: Finns det ett sätt att få konfidenspoäng?**  
Ja. Efter `Recognize()` kan du inspektera `ocrEngine.RecognizedWords` – varje ord innehåller en `Confidence`‑egenskap.

---

## Slutsats

Vi har gått igenom **hur man använder OCR** i C# för att *extrahera text från bild*‑filer helt offline. Genom att installera Aspose.OCR, konfigurera `EngineMode.Offline`, peka på resurserna, ladda en bild och anropa `Recognize()` kan du på ett pålitligt sätt **konvertera bild till text** utan att någonsin röra internet.  

Ta koden ovan, byt ut dina egna bildsökvägar och börja bygga funktioner som sökbara PDF‑filer, automatisering av datainmatning eller tillgänglighetsverktyg. Nästa steg kan vara att utforska **recognize text from PNG** i bulk, eller integrera motorn i ett ASP.NET Core‑API för att leverera OCR‑resultat till front‑end‑applikationer.

Lycka till med kodandet, och experimentera gärna – OCR är förvånansvärt förlåtande när motorn väl är korrekt konfigurerad!

--- 

![Diagram som visar offline OCR‑arbetsflöde – hur man använder OCR i en säker miljö](https://example.com/ocr-workflow.png "hur man använder OCR‑diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}