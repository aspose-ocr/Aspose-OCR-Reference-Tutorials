---
category: general
date: 2026-04-11
description: Lär dig hur du inaktiverar OCR i Aspose OCR för C# för att köra offline,
  extrahera text från en bild utan internet och korrekt ladda bilden för OCR.
draft: false
keywords:
- how to disable OCR
- extract text from image
- load image for OCR
- offline OCR C#
- Aspose OCR resources
language: sv
og_description: Hur du inaktiverar OCR i Aspose OCR för C# och kör offline, extraherar
  text från en bild utan att behöva internet, och enkelt laddar bild för OCR.
og_title: Hur man inaktiverar OCR i C# – Offline Aspose OCR‑guide
tags:
- C#
- OCR
- Aspose
- Offline Processing
title: Hur du inaktiverar OCR i C# – Offline Aspose OCR‑guide
url: /sv/net/ocr-configuration/how-to-disable-ocr-in-c-offline-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man inaktiverar OCR i C# – Offline Aspose OCR‑guide

Har du någonsin funderat **hur man inaktiverar OCR** när du behöver en riktigt offline‑lösning? Kanske bygger du en säker skrivbordsapp som inte kan förlita sig på en nätverksanslutning, eller så vill du bara undvika oväntade nedladdningar. Oavsett är den goda nyheten att Aspose OCR låter dig stänga av sin automatiska resurshämtning, peka den mot en lokal mapp och hålla allt på‑premises. I den här handledningen får du också se hur du **extraherar text från bild**‑filer och korrekt **laddar bild för OCR** utan några problem.

Vi går igenom ett komplett, färdigt exempel som visar varje steg – från att initiera motorn till att skriva ut den igenkända japanska texten. Inga externa dokument, ingen gömd magi; bara ren C#‑kod som du kan klistra in i ditt projekt idag. När du är klar vet du varför det är viktigt att inaktivera den automatiska nedladdningsfunktionen, hur du anger sökvägen till resurserna och vilka fallgropar du bör hålla utkik efter.

## Förutsättningar

- .NET 6.0 (eller någon nyare .NET‑version) installerad på din maskin.  
- Aspose.OCR för .NET NuGet‑paket (`Install-Package Aspose.OCR`).  
- En mapp som redan innehåller de språkresurser du behöver (t.ex. den japanska modellen).  
- En bildfil (`japan_doc.png`) som du vill köra OCR på.  

Om du saknar språkpaketen, hämta dem en gång från Aspose‑portalen, packa upp dem i en mapp som `AsposeOCRResources`, så är du klar. Inga ytterligare nedladdningar sker när du har inaktiverat den automatiska nedladdningsfunktionen.

![Hur man inaktiverar OCR offline](/images/how-to-disable-ocr.png "illustration av hur man inaktiverar OCR")

## Steg 1 – Skapa OCR‑motorn

Det första du gör är att instansiera `OcrEngine`. Tänk på detta objekt som hjärnan som kommer att läsa din bild.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Varför detta är viktigt:** Utan en motor kan du inte konfigurera någonting. Objektet innehåller alla inställningar, inklusive den avgörande flaggan som talar om för biblioteket huruvida det får nå internet.

## Steg 2 – Inaktivera automatisk resurshämtning

Som standard försöker Aspose OCR hämta saknade språkfiler i farten. För att hålla allt offline, sätt `AutoDownloadResources`‑växeln till `false`.

```csharp
        // Step 2: Disable automatic resource download to work offline
        ocrEngine.Settings.AutoDownloadResources = false;
```

> **Proffstips:** Att stänga av detta garanterar inte bara integritet utan snabbar också upp den första igenkänningskörningen eftersom motorn inte slösar tid på att leta efter uppdateringar.

## Steg 3 – Peka på din lokala resursermapp

Berätta nu för motorn var de för‑nedladdade språkpaketen finns. Detta är den sökväg du satte upp i förutsättningarna.

```csharp
        // Step 3: Point the engine to the folder containing pre‑downloaded resources
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";
```

> **Vad kan gå fel?** Om sökvägen är fel eller den nödvändiga språkfilen saknas, kastar motorn ett `ResourceNotFoundException`. Dubbelkolla mappnamnet och att den japanska modellen (`jpn.traineddata`) finns där.

## Steg 4 – Välj den lokala språkmodellen

Välj det språk du faktiskt har på disken. I vårt exempel använder vi japanska, men du kan byta `Language.Japanese` mot vilket annat språk du har laddat ner.

```csharp
        // Step 4: Select the language model that is available locally
        ocrEngine.Settings.Language = Language.Japanese;
```

> **Edge case:** Vissa språk kräver extra ordböcker (t.ex. kinesiska). Se till att dessa hjälpfiler också finns i samma resursermapp.

## Steg 5 – Ladda bilden för OCR

Här **laddar vi bild för OCR**. Metoden `ImageStream.FromFile` läser filen till en ström som Aspose kan bearbeta.

```csharp
        // Step 5: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/japan_doc.png");
```

> **Tips:** Stödda format inkluderar PNG, JPEG, BMP och TIFF. Om du behöver hantera PDF‑filer, konvertera varje sida till en bild först.

## Steg 6 – Kör igenkänningsprocessen

Nu läser motorn faktiskt pixlarna och försöker omvandla dem till text.

```csharp
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **Varför detta steg kan vara långsamt:** OCR är CPU‑intensivt, särskilt för högupplösta bilder. Om prestanda är ett problem, överväg att skala ner bilden innan igenkänning.

## Steg 7 – Skriv ut den extraherade texten

Till sist **extraherar vi text från bild** och skriver ut den i konsolen.

```csharp
        // Step 7: Output the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

När du kör programmet bör de japanska tecknen som fanns i `japan_doc.png` visas. Om allt är korrekt konfigurerat ser du ett rent block med Unicode‑text i din konsol.

### Förväntad utdata

```
これはサンプルの日本語テキストです。
```

(Din faktiska utdata beror på innehållet i bilden.)

## Vanliga fallgropar & hur du undviker dem  

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| **Saknad språkfil** | `AutoDownloadResources` är falskt, så motorn kan inte hämta den. | Verifiera att `ResourcesPath` pekar på mappen som innehåller `jpn.traineddata`. |
| **Felaktig bildsökväg** | `ImageStream.FromFile` kastar `FileNotFoundException`. | Använd absoluta sökvägar eller säkerställ att arbetskatalogen är korrekt. |
| **Ej stödd bildformat** | Aspose läser bara vissa format. | Konvertera din bild till PNG eller JPEG innan du anropar `FromFile`. |
| **Minnesbrist på stora bilder** | OCR laddar hela bilden i minnet. | Ändra storlek eller dela upp bilden, eller öka processens minnesgräns. |

## Utöka exemplet  

- **Batch‑bearbetning:** Loopa igenom en katalog med bilder, anropa samma igenkänningskod och skriv varje resultat till en separat `.txt`‑fil.  
- **Olika språk:** Byt `Language.Japanese` mot `Language.English` (eller något annat) efter att du placerat motsvarande resursfiler.  
- **Anpassad förbehandling:** Använd Aspose.Imaging för att räta upp eller förbättra kontrasten innan OCR för bättre noggrannhet.

## Slutsats  

Du vet nu **hur man inaktiverar OCR** i Aspose OCR för C# och kör den helt offline. Genom att sätta `AutoDownloadResources` till `false`, peka motorn mot en lokal resursermapp och korrekt **ladda bild för OCR**, kan du på ett pålitligt sätt **extrahera text från bild** utan att nå internet. Detta tillvägagångssätt är idealiskt för säkra miljöer, CI‑pipelines eller alla scenarier där nätverksåtkomst är begränsad.

Redo för nästa steg? Prova att bearbeta en hel mapp med skannade PDF‑filer, experimentera med olika språkpaket, eller integrera OCR‑resultatet i en sökbar databas. Den offline‑konfiguration du byggt idag är en solid grund för alla on‑premises dokument‑bearbetningsarbetsflöden.

Lycka till med kodandet, och lämna gärna en kommentar om du stöter på några problem!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}