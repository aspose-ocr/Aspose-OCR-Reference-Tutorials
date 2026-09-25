---
category: general
date: 2026-01-15
description: Konvertera bild till JSON med Aspose OCR i C#. Lär dig hur du extraherar
  text från en bild, får JSON‑omslutningsrutor och känner igen kvittobilder.
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: sv
og_description: Konvertera bild till JSON med Aspose OCR i C#. Steg‑för‑steg‑guide
  för att extrahera text från bild, känna igen kvittobild och få JSON‑omslutningsrutor.
og_title: Konvertera bild till JSON med Aspose OCR C#-guide
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: Konvertera bild till JSON med Aspose OCR C#-guide
url: /sv/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertera bild till JSON med Aspose OCR C#-guide

Har du någonsin behövt **convert image to JSON** men varit osäker på vilket bibliotek som kan ge dig både råtexten och de exakta ordkoordinaterna? Du är inte ensam. Många utvecklare stöter på detta problem när de försöker extrahera text från bildfiler—särskilt kvitton—och samtidigt behöver en maskinläsbar JSON‑payload för efterföljande bearbetning.

I den här handledningen går vi igenom ett komplett **Aspose OCR C# example** som visar hur du extraherar text från en bild, känner igen en kvittobild och genererar **JSON bounding boxes** för varje ord. I slutet har du en färdig‑att‑köra konsolapp som skriver ut en snyggt formaterad JSON‑sträng som du kan skicka till vilket API, databas eller analys‑pipeline som helst.

> **Vad du får med dig**  
> • Ett fullt fungerande C#‑projekt som **converts image to JSON**  
> • Insikt i varför vi aktiverar `IncludeBoundingBoxes` (det är nyckeln till `json bounding boxes`)  
> • Tips för att hantera olika bildformat och språk  

Låt oss komma igång.

---

## Vad du behöver

- **.NET 6.0 SDK** (eller någon senare version) – koden riktar sig mot .NET 6 men fungerar även på .NET Framework 4.7+.  
- **Aspose.OCR for .NET** NuGet‑paket – du kan hämta det via `dotnet add package Aspose.OCR`.  
- En exempel‑kvitto‑bild (`receipt.jpg`) placerad i en mapp som du kan referera till från ditt projekt.  
- Visual Studio 2022, VS Code eller någon annan IDE du föredrar.

Inga andra externa tjänster krävs; allt körs lokalt.

---

## Konvertera bild till JSON – Översikt

Kärnidén är enkel: ladda en bild, be Aspose OCR att känna igen engelska (eller något annat stödjert språk), be den inkludera bounding boxes och slutligen begära resultatet i **JSON**‑format. Biblioteket sköter allt det tunga arbetet—OCR, layoutanalys och JSON‑serialisering.

Här är ett hög‑nivå‑diagram över flödet (föreställ dig en liten bild):

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

Det där lilla diagrammet fångar hela pipeline‑processen som vi kommer att implementera.

---

## Steg 1: Skapa projektet och installera Aspose OCR

Först, skapa ett nytt konsolprojekt och hämta Aspose OCR‑paketet.

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **Proffstips:** Om du använder Visual Studio, högerklicka på projektet → *Manage NuGet Packages* → sök efter **Aspose.OCR** och installera den senaste stabila versionen (för närvarande 23.12).

---

## Steg 2: Ladda bilden du vill känna igen

Vi kommer att använda metoden `OcrImage.FromFile` för att läsa kvittobilden. Se till att sökvägen pekar på en riktig fil; annars får du ett `FileNotFoundException`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

Om din bild ligger bredvid `.csproj`‑filen kan du helt enkelt använda `"receipt.jpg"`.

---

## Steg 3: Konfigurera OCR‑alternativ för JSON‑bounding boxes

Magin sker när vi aktiverar `OutputFormat = OutputFormat.Json` **och** `IncludeBoundingBoxes = true`. Det förra talar om för Aspose att serialisera resultatet som JSON, medan det senare lägger till `x`, `y`, `width` och `height` för varje ord—precis vad du behöver för `json bounding boxes`.

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

Du kan också justera `ocrOptions.Dpi` eller `ocrOptions.Language` om du behöver högre upplösning eller ett annat språk.

---

## Steg 4: Utför igenkänning – Extrahera text från bild

Nu anropar vi `Recognize`. Metoden returnerar ett `OcrResult`‑objekt som innehåller JSON‑strängen, råtexten och mer.

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

Om du behöver hantera andra språk, ersätt `Language.English` med `Language.Spanish`, `Language.French` osv. Aspose stöder över 30 språk direkt.

---

## Steg 5: Skriv ut resultatet – Din JSON‑payload

Till sist skriver vi ut JSON‑en till konsolen. I en riktig app skulle du troligen skriva den till en fil eller skicka den till en tjänst.

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

När du kör programmet bör det producera ett JSON‑dokument liknande kodsnutten nedan.

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

Lägg märke till hur varje ord nu har sin **JSON bounding box**—perfekt för att mata in i ett UI‑lager eller en efterföljande parser.

---

## Fullt fungerande exempel

Nedan är det kompletta, kopiera‑och‑klistra‑klara programmet. Inga dolda delar, inga externa anrop—bara ren C#.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **Se upp för:**  
> • **Filvägsfel** – dubbelkolla bildens plats.  
> • **Saknat NuGet‑paket** – säkerställ att `Aspose.OCR` är refererat.  
> • **Ej stödda bildformat** – håll dig till JPEG, PNG, BMP eller TIFF för bästa resultat.

---

## Vanliga frågor & edge‑cases

### Kan jag konvertera en **PDF‑sida** till JSON istället för en JPEG?

Ja. Konvertera PDF‑sidan till en bild först (t.ex. med `Aspose.PDF`), och mata sedan in den bilden i samma OCR‑pipeline. JSON‑utdata blir identisk eftersom OCR‑steget bara bryr sig om rasterdata.

### Vad händer om kvittot är suddigt?

Öka DPI‑värdet i `ocrOptions`. Till exempel:

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

Högre DPI kan öka minnesanvändningen, så balansera kvalitet mot prestanda.

### Jag behöver **flera språk** på samma kvitto (t.ex. engelska + spanska).

Du kan skicka en array med språk:

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

Aspose kommer att försöka känna igen varje språk i den angivna ordningen.

### Hur skriver jag JSON till en fil?

Byt helt enkelt ut `Console.WriteLine`‑raden mot:

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

Nu har du en bestående fil som du kan skicka till andra tjänster.

---

## Visuell sammanfattning

![convert image to json example](convert-image-to-json.png "convert image to json example")

*Skärmbilden visar konsolutdata av JSON‑payloaden efter att demon har körts.*

---

## Slutsats

Vi har just visat hur du **convert image to JSON** med Aspose OCR i C#. Genom att konfigurera `OutputFormat` och `IncludeBoundingBoxes` kan du **extract text from image**, **recognize receipt image** och få precisa **JSON bounding boxes** för varje ord. Den kompletta, körbara koden finns i kodsnutten ovan, så du kan klistra in den i vilket .NET‑projekt som helst just nu.

Vad blir nästa steg? Prova att mata in JSON i en front‑end‑visare som markerar varje ord, eller skicka data till en maskininlärningsmodell som klassificerar rader på kvitton. Du kan också experimentera med andra språk, högre DPI‑inställningar eller batch‑bearbeta flera bilder i en slinga.

Om du stöter på problem, kom ihåg tipsen om filvägar, DPI och språk‑arrayer. Känn dig fri att lämna en kommentar eller öppna ett ärende i GitHub‑repot du skapar för detta demo. Lycka till med kodandet, och njut av att omvandla bilder till strukturerad JSON!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}