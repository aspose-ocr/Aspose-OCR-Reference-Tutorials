---
category: general
date: 2026-03-23
description: Skapa sökbar PDF från bild med Aspose OCR. Lär dig hur du konverterar
  TIFF till PDF med hög kompression och känner igen bildtext på några minuter.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- high compression pdf
- recognize image text
- searchable pdf from image
language: sv
og_description: Skapa sökbar PDF från bild med Aspose OCR. Denna handledning visar
  hur du konverterar TIFF till PDF, lägger till ett sökbart textlager och använder
  hög komprimering.
og_title: Skapa sökbar PDF från bild – Komplett C#‑guide
tags:
- Aspose OCR
- C#
- PDF generation
title: Skapa sökbar PDF från bild – Komplett C#-guide
url: /sv/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa sökbar PDF från bild – Komplett C#-guide

Har du någonsin behövt **create searchable pdf** från ett skannat dokument men varit osäker på var du ska börja? Du är inte ensam—många utvecklare stöter på samma problem när de omvandlar TIFF-skanningar till sökbara PDF:er. De goda nyheterna? Med Aspose OCR kan du **convert tiff to pdf**, lägga ett dolt textlager ovanpå och till och med minska filstorleken med **high compression pdf**‑alternativ, allt i några få rader C#.

I den här handledningen går vi igenom hela processen: från att installera rätt NuGet‑paket, ladda en TIFF‑bild, känna igen dess text och slutligen exportera en sökbar PDF. När du är klar har du en körbar konsolapp som **recognize image text** och producerar en kompakt, sökbar PDF klar för indexering. Inga extra verktyg, inga manuella OCR‑steg—bara ren kod och lite förklaring.

## Förutsättningar och vad du behöver

- **.NET 6+** (or .NET Framework 4.6+). API:et fungerar på båda, men .NET 6 ger dig de senaste runtime‑förbättringarna.  
- **Visual Studio 2022** eller någon IDE du föredrar.  
- **Aspose.OCR** och **Aspose.OCR.Gpu** NuGet‑paket (GPU‑paketet är valfritt men snabbar upp igenkänning på stödjande hårdvara).  
- En exempel‑TIFF‑fil (t.ex. `invoice.tif`) placerad i en mapp du kontrollerar.  

Om du redan har dessa saker, toppen—hoppa över. Om inte, täcker installationssteget nedan allt.

## Steg 1: Installera Aspose OCR‑paket

För att börja, öppna din projektmapp i en terminal och kör:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Dessa kommandon hämtar både kärn‑OCR‑motorn och GPU‑accelerationsbiblioteket. Det senare är inte obligatoriskt; motorn kommer att falla tillbaka till CPU‑läge om den inte hittar ett kompatibelt GPU.

> **Pro tip:** När du riktar mot en produktionsmiljö, lås paketversionerna i din `csproj` för att undvika oväntade brytande förändringar.

## Steg 2: Ställ in projektets skelett

Skapa en ny konsolapp (om du inte redan har en):

```bash
dotnet new console -n PdfExportDemo
cd PdfExportDemo
```

Ersätt den automatiskt genererade `Program.cs` med den fullständiga koden som visas senare. Programmet kommer att:

1. Initiera en `OcrEngine` med GPU‑stöd.  
2. Ladda TIFF‑bilden.  
3. Köra OCR och avbryta elegant vid fel.  
4. Konfigurera **PdfExportOptions** för ett sökbart lager och **high compression**.  
5. Skriva utdatafilen.

## Steg 3: Skriv den kompletta koden (Fullt exempel)

Nedan är den *hela* källfilen. Kopiera‑klistra in den i `Program.cs`. Kommentarerna förklarar “varför” bakom varje rad, inte bara “vad”.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;

class PdfExport
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Initialise OCR engine with GPU acceleration.
        //    GpuMode.Enabled tells Aspose to use the GPU if one is present.
        //    If no compatible GPU exists, the engine automatically falls back
        //    to CPU mode—no extra code required.
        // ------------------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine(GpuMode.Enabled))
        {
            // ------------------------------------------------------------
            // 2️⃣ Load the source image.
            //    ImageStream.FromFile supports many formats; here we use TIFF.
            // ------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\invoice.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // ------------------------------------------------------------
            // 3️⃣ Perform OCR recognition.
            //    Recognize() returns false if the engine cannot read the image.
            //    Exiting early prevents us from creating an empty PDF.
            // ------------------------------------------------------------
            if (!ocrEngine.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return;
            }

            // ------------------------------------------------------------
            // 4️⃣ Configure PDF export options.
            //    IncludeTextLayer = true adds an invisible, searchable text layer.
            //    CompressionLevel = High reduces file size dramatically.
            // ------------------------------------------------------------
            PdfExportOptions pdfExportOptions = new PdfExportOptions
            {
                IncludeTextLayer = true,
                CompressionLevel = PdfCompression.High
            };

            // ------------------------------------------------------------
            // 5️⃣ Save the searchable PDF.
            //    The output will be a compact, searchable PDF ready for indexing.
            // ------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\invoice.pdf";
            ocrEngine.Save(outputPath, pdfExportOptions);
            Console.WriteLine($"Searchable PDF saved to: {outputPath}");
        }
    }
}
```

### Varför detta fungerar

- **GPU acceleration** kan minska igenkänningstiden från sekunder till millisekunder på moderna kort—praktiskt för massbearbetning.  
- **IncludeTextLayer** bäddar in den OCR‑genererade texten osynligt, vilket låter PDF‑visare söka i dokumentet utan att ändra dess visuella utseende.  
- **High compression** använder Flate (ZIP)‑komprimering på bildströmmen, vilket är förlustfritt men minskar filstorleken dramatiskt—idealiskt för arkivering av tusentals fakturor.

## Steg 4: Kör applikationen och verifiera resultatet

Öppna en terminal i projektmappen och kör:

```bash
dotnet run
```

Om allt är korrekt konfigurerat kommer du att se:

```
Searchable PDF saved to: YOUR_DIRECTORY\invoice.pdf
```

Öppna `invoice.pdf` i någon PDF‑läsare (Adobe Acrobat, Edge eller till och med en webbläsare). Försök söka efter ett ord du vet finns i den ursprungliga TIFF‑filen—t.ex. “Total”. Visaren bör markera ordet även om det är en del av bilden. Det är kännetecknet för en **searchable pdf**.

### Förväntad filstorlek

En typisk skannad faktura (≈300 KB TIFF) krymper ofta till **~80 KB** efter att ha applicerat `PdfCompression.High`. Den exakta storleken beror på bildens komplexitet, men du kommer att märka en tydlig minskning.

## Steg 5: Vanliga variationer och kantfall

| Situation | What to Adjust | Why |
|-----------|----------------|-----|
| **Ingen GPU tillgänglig** | Ändra `new OcrEngine(GpuMode.Enabled)` till `new OcrEngine(GpuMode.Disabled)` | Förhindrar att motorn försöker initiera GPU, vilket kan orsaka en kort fördröjning. |
| **Flera sidor (multi‑page TIFF)** | Sätt `ocrEngine.Image = ImageStream.FromFile("multi.tif", PageRange.All);` | Laddar alla ramar; Aspose kommer att bearbeta varje sida och generera en multi‑page PDF. |
| **Behöver OCR‑språk annat än engelska** | `ocrEngine.Language = Language.French;` (eller något annat stödjande språk) | Förbättrar noggrannheten för icke‑engelska dokument. |
| **Vill ha ett synligt textlager istället för dolt lager** | `pdfExportOptions.IncludeTextLayer = false;` och lägg manuellt till `TextFragment`‑objekt. | Användbart när du vill att OCR‑texten ska visas som markerbar text ovanpå bilden. |
| **Ultralätta PDF:er** | Kombinera `PdfCompression.High` med `ImageResolution = 150` DPI före igenkänning. | Lägre DPI minskar bilddata, vilket ytterligare minskar PDF‑storleken på bekostnad av visuell kvalitet. |

> **Note:** Test alltid kantfall på ett litet prov innan du skalar till produktion. OCR‑noggrannheten kan variera med bildkvalitet, brus och språk.

## Steg 6: Tips för produktionsklara implementationer

1. **Error Logging** – Ersätt `Console.WriteLine` med ett korrekt loggningsramverk (Serilog, NLog) för enklare diagnostik.  
2. **Batch Processing** – Packa in kärnlogiken i en metod som accepterar in‑/utdata‑sökvägar, och iterera sedan över en katalog med TIFF‑filer.  
3. **Async I/O** – Även om Aspose OCR själv är synkron, kan inläsning och sparande av filer vara asynkrona för att hålla UI‑trådar responsiva.  
4. **Security** – Om du exponerar denna funktion via ett webb‑API, validera filvägar och begränsa filstorlekar för att förhindra missbruk.  
5. **Version Pinning** – Använd exakta versionsnummer (`<PackageReference Include="Aspose.OCR" Version="23.12.0" />`) för att garantera konsekvent beteende över byggen.

## Slutsats

Vi har precis byggt en **complete, end‑to‑end solution** som **create searchable pdf**‑filer från skannade bilder, **convert tiff to pdf**, och gör det med **high compression pdf**‑inställningar medan **recognize image text** noggrant. Den resulterande **searchable pdf from image** är lättviktig, sökbar och klar för efterföljande arbetsflöden såsom indexering, arkivering eller e‑discovery.

Har du en massa fakturor? Koppla in metoden i en loop, peka på en mapp, och låt Aspose OCR göra det tunga lyftet. Vill du experimentera med olika komprimeringsnivåer eller språkpaket? Koden är tillräckligt modulär för att byta dessa alternativ på sekunder.

---

*Ready to level up?* Prova att lägga till ett vattenmärke, bädda in metadata, eller till och med sammanfoga flera OCR‑bearbetade PDF:er. Aspose‑sviten erbjuder många tillägg—utforska dokumentationen och håll momentumet igång. Lycka till med kodningen!

![Skapa sökbar PDF från bild exempel skärmbild](https://example.com/images/create-searchable-pdf.png "exempel på skapa sökbar pdf")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}