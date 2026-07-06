---
category: general
date: 2026-03-26
description: Känn igen text från png och extrahera kvittodata med Aspose OCR i C#.
  Konvertera bilden till JSON‑L och bearbeta kvittot med OCR i ett komplett exempel.
draft: false
keywords:
- recognize text from png
- extract text from receipt
- convert image to jsonl
- process receipt with ocr
- aspose ocr example c#
language: sv
og_description: igenkänn text från png och omvandla kvitton till JSON‑L med Aspose
  OCR i C#. Fullständig steg‑för‑steg‑kod och tips.
og_title: Känn igen text från PNG – Aspose OCR C#‑guide
tags:
- Aspose OCR
- C#
- JSONL
- Receipt Processing
title: Känn igen text från png – Aspose OCR C# JSON‑L handledning
url: /sv/net/text-recognition/recognize-text-from-png-aspose-ocr-c-json-l-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# igenkänna text från png – Fullständig Aspose OCR C#‑guide

Har du någonsin behövt **igenkänna text från png**‑filer men varit osäker på vilket bibliotek som ger rena, rad‑för‑rad‑resultat? Du är inte ensam. I många småföretagsappar lagras kvittot som en PNG‑bild, och att dra ut belopp, datum eller handlarens namn är ett dagligt smärtpunktsproblem.  

Den goda nyheten? Med några rader C# och **Aspose OCR**‑biblioteket kan du **extract text from receipt**, sedan **convert image to jsonl** för efterföljande analys. I den här handledningen går vi igenom hela pipeline—laddar en PNG, kör OCR och skriver varje rad till en JSON‑L‑fil—så att du kan **process receipt with OCR** direkt.

Vi täcker allt du behöver: nödvändiga NuGet‑paket, ett komplett körbart program, förklaringar till varför varje steg är viktigt, och ett antal praktiska tips du kommer att uppskatta när kvittona blir röriga. Ingen extern dokumentation behövs; bara kopiera‑klistra, kör och anpassa.

---

## Vad du kommer att lära dig

- Hur du **recognize text from png** med `Aspose.OCR`.
- Hur du **extract text from receipt**‑radobjekt och fånga förtroendescore.
- Hur du **convert image to jsonl** så att varje OCR‑rad blir ett separat JSON‑objekt.
- Hur du **process receipt with OCR** end‑to‑end, hanterar kantfall som tomma bilder eller lågt förtroende.
- Tips för att felsöka vanliga OCR‑problem och förbättra noggrannheten.

### Förutsättningar

- .NET 6.0 eller senare (koden fungerar även med .NET Core och .NET Framework).
- Visual Studio 2022 eller någon annan IDE du föredrar.
- En giltig Aspose OCR‑licens (du kan börja med en gratis temporär licens från Aspose.com).
- Ett exempel‑kvitto sparat som `receipt.png` i en mapp du har kontroll över.

---

## Steg 1: Recognize text from png med Aspose OCR

Det första vi behöver är en initierad `OcrEngine`. Detta objekt innehåller OCR‑motorinställningarna (språk, detekteringsläge osv.). Som standard använder den engelska och autodetekterar sidlayouten, vilket fungerar bra för de flesta kvitton.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is where Aspose loads its models.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG image that contains the receipt.
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // Run OCR and get the result object.
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);
```

**Varför detta är viktigt:**  
`OcrEngine` är den tunga komponenten; att skapa den en gång och återanvända den för många bilder minskar minnesanvändningen. Om du behöver ett annat språk (t.ex. spanska kvitton) kan du sätta `ocrEngine.Language = OcrLanguage.Spanish;` innan du anropar `Recognize`.

---

## Steg 2: Extract text from receipt‑rader

`OcrResult` innehåller en samling som heter `Lines`. Varje rad innehåller den råa texten och ett förtroendescore (0‑100). Att plocka ut dessa ger dig fin kontroll—du kan kasta lågt‑förtroende‑rader eller flagga dem för manuell granskning.

```csharp
        // Prepare to write each line as a JSON‑L record.
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";

        using (StreamWriter jsonLineWriter = new StreamWriter(jsonlPath))
        {
            foreach (var line in ocrResult.Lines)
            {
                // Build a simple JSON object for the line.
                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                jsonLineWriter.WriteLine(json);
            }
        }

        Console.WriteLine("JSON‑L file written to " + jsonlPath);
    }

    // Helper to escape quotes and backslashes in JSON strings.
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Varför vi escape:ar JSON:**  
Kvitton kan innehålla citattecken (`"`) eller bakstreck (`\`) som skulle bryta en naiv JSON‑sträng. Metoden `EscapeJson` garanterar en giltig JSON‑rad.

**Hur utdata ser ut:**  

```
{"text":"Store XYZ","confidence":98.5}
{"text":"Date: 2024-07-15","confidence":97.2}
{"text":"Total $23.45","confidence":99.1}
```

Varje rad är en separat post, perfekt för att strömma in i ett datalake eller mata en maskininlärningsmodell.

---

## Steg 3: Convert image to JSONL – hantera kantfall

När du bearbetar en batch av kvitton kan några bilder vara tomma, korrupta eller ha extremt låga förtroendescore. Låt oss göra pipelinen lite mer robust.

```csharp
        // After OCR, check if any lines were detected.
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("Warning: No text detected. Verify the image path and quality.");
            return;
        }

        // Optional: filter out lines with confidence below a threshold.
        const double minConfidence = 80.0;
        foreach (var line in ocrResult.Lines)
        {
            if (line.Confidence < minConfidence)
                continue; // skip noisy line
            // write as before...
        }
```

**Varför filtrera:**  
Kvitton tryckta på blekt papper kan ge stray‑tecken med lågt förtroende. Att släppa allt under 80 % tar vanligtvis bort brus samtidigt som den användbara datan behålls.

---

## Steg 4: Process receipt with OCR – end‑to‑end‑exempel

När vi sätter ihop allt, här är det **kompletta, körklara** programmet. Ersätt `YOUR_DIRECTORY` med mappen som innehåller din PNG‑fil.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load receipt PNG
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Perform OCR
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

        // 4️⃣ Verify we got something back
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("❗ No text found – check the image quality.");
            return;
        }

        // 5️⃣ Write each line to a JSON‑L file
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";
        using (StreamWriter writer = new StreamWriter(jsonlPath))
        {
            const double minConfidence = 80.0;
            foreach (var line in ocrResult.Lines)
            {
                if (line.Confidence < minConfidence) continue; // skip low‑confidence

                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                writer.WriteLine(json);
            }
        }

        Console.WriteLine($"✅ JSON‑L written to: {jsonlPath}");
    }

    // Helper to make JSON safe
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Köra koden:**  
1. Öppna en terminal i projektmappen.  
2. `dotnet add package Aspose.OCR` – installerar biblioteket.  
3. `dotnet run` – du bör se ett lyckat meddelande och en `receipt.jsonl`‑fil dyka upp.

**Förväntat resultat:** En rad‑avgränsad JSON‑fil där varje rad speglar en kvittorad, komplett med förtroendescore. Du kan nu skicka denna fil till Power BI, Elastic eller något annat analysverktyg som förstår JSON‑L.

---

## Vanliga fallgropar & Pro‑tips

| Problem | Varför det händer | Snabb lösning |
|-------|----------------|-----------|
| **Tomt resultat** | Fel bildsökväg eller filen är inte en PNG. | Dubbelkolla sökvägen, använd `File.Exists(imagePath)`. |
| **Skräptecken** | Låg DPI eller kraftigt komprimerad PNG. | Använd minst 300 dpi‑skanningar; undvik aggressiv JPEG‑kompression. |
| **För många lågt‑förtroende‑rader** | Kvitto tryckt på termiskt papper med blekning. | Höj `minConfidence`‑tröskeln eller förbehandla bilden (kontrast/tröskel). |
| **JSON‑parsfel** | Oescaped citattecken i kvittotexten. | Behåll `EscapeJson`‑hjälpen eller byt till `System.Text.Json` för robust serialisering. |

**Pro‑tips:** Om du behöver extrahera specifika fält (t.ex. totalbelopp) kan du köra ett enkelt regex på varje `line.Text` efter att du har JSON‑L‑filen. Detta håller OCR separerat från affärslogik och gör felsökning enklare.

---

## Utöka lösningen

- **Batch‑bearbetning:** Lägg `Main`‑logiken i en `foreach` över alla PNG‑filer i en katalog.
- **Flerspråkigt stöd:** Sätt `ocrEngine.Language = OcrLanguage.Spanish;` (eller något annat stödjert språk) innan `Recognize`.
- **Strukturerad utdata:** Istället för rad‑för‑rad JSON, bygg ett `Receipt`‑objekt med `Date`, `Merchant`, `Total`‑egenskaper och serialisera en gång.

Alla dessa varianter behåller fortfarande **convert image to jsonl** i kärnan, så du kan byta downstream‑konsumenten utan att röra OCR‑delen.

---

## Slutsats

Vi har just visat hur du **recognize text from png**‑filer med Aspose OCR, **extract text from receipt** och **convert image to jsonl** för enkel efterföljande bearbetning. Det fullständiga, självständiga C#‑programmet demonstrerar hela arbetsflödet—from att ladda en PNG, hantera kantfall, till att skriva en ren JSON‑L‑fil—så att du omedelbart kan **process receipt with OCR** i dina egna projekt.

Prova med några exempel‑kvitton, justera förtroendeträskeln, och du kommer se hur snabbt en bullrig hög av bilder blir strukturerad data redo för analys. När du känner dig bekväm, utforska batch‑bearbetning eller lägg till en liten ML‑modell för att automatiskt klassificera utgiftsslag.

Har du frågor eller har du hittat ett smart knep? Lämna en kommentar nedan—lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}