---
category: general
date: 2026-03-13
description: Hur man utför OCR i C# och extraherar text från en bild med OcrEngine.
  Lär dig att snabbt konvertera bild till text med en komplett steg‑för‑steg‑guide.
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- read text from picture
- how to extract text
language: sv
og_description: Hur utför man OCR i C#? Den här guiden visar hur du extraherar text
  från en bild, konverterar bild till text och läser text från en bild med OcrEngine.
og_title: Hur man utför OCR i C# – Extrahera text från en bild
tags:
- OCR
- C#
- Image Processing
title: Hur man utför OCR i C# – Extrahera text från bild
url: /sv/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man utför OCR i C# – Extrahera text från bild

Att utföra OCR i C# är en vanlig fråga för utvecklare som behöver **läsa text från bild**-filer. I den här guiden går vi igenom hur du extraherar text från en bild med hjälp av `OcrEngine`-biblioteket, och omvandlar bilder till sökbara strängar med bara några rader kod.  

Om du någonsin har stirrat på en skannad faktura, en handskriven lapp eller en skärmdump och undrat *“hur extraherar jag text?”*, så är du på rätt plats. Vi kommer också att beröra konvertering av bild till text för batch‑behandling, så att du kan automatisera hela arbetsflödet.

---

## Vad du behöver

- **.NET 6.0 eller senare** (API‑et vi använder fungerar med .NET Standard 2.0+)
- **OcrEngine** NuGet‑paketet (eller något kompatibelt OCR‑bibliotek som exponerar egenskaperna `Language`, `Image`, `Recognize` och `Text`)
- En exempelbildfil, t.ex. `hindi_page.jpg`, placerad i en mapp som du kan referera till från koden
- En grundläggande förståelse för C#‑syntax – inga avancerade knep krävs

Det är allt. Inga externa tjänster, inga API‑nycklar, bara ett lokalt bibliotek som gör det tunga arbetet.

---

## Steg‑för‑steg‑implementering

Nedan delar vi upp processen i logiska delar. Varje avsnitt har en tydlig rubrik, ett kort kodexempel och en förklaring av **varför** steget är viktigt – inte bara **vad** det gör.

### Så utför du OCR – Grundsteg

1. **Create** en OCR‑motorinstans
2. **Select** språket du vill känna igen
3. **Load** bilden som innehåller texten
4. **Run** igenkänningsalgoritmen
5. **Read** den extraherade texten

Det är skelettet; avsnitten som följer fyller i detaljerna.

---

### Extrahera text från bild – Skapa motorn

Först behöver vi ett objekt som vet hur man kommunicerar med OCR‑motorn.

```csharp
using System;
using OcrLibrary;   // Replace with the actual namespace of your OCR package

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

*Varför detta är viktigt:* Att instansiera `OcrEngine` allokerar alla interna buffertar och laddar eventuella inhemska DLL‑filer som krävs för bildanalys. Att hoppa över detta steg skulle lämna dig utan en igenkännare att anropa senare.

> **Pro tip:** Om du planerar att bearbeta många bilder i rad, håll samma `ocrEngine`‑instans vid liv. Den återanvänder språkmodeller och snabbar upp efterföljande anrop.

---

### Konvertera bild till text – Välj språk

OCR‑noggrannheten beror starkt på språkmodellen du matar den med. För Hindi, Tamil eller något annat skript, ställ in `Language`‑egenskapen därefter.

```csharp
// Step 2: Select the language of the text to recognize (e.g., Hindi)
ocrEngine.Language = Language.Hindi;   // You can also use Language.Tamil, Language.English, etc.
```

*Varför detta är viktigt:* Motorn använder språk‑specifika teckenuppsättningar och statistiska modeller. Att ange fel språk ger ofta förvrängd output, särskilt för icke‑latinska skript.

> **Edge case:** Om du behöver flerspråkigt stöd, låter vissa bibliotek dig ange en reservlista, t.ex. `ocrEngine.Language = Language.Multilingual;`.

---

### Läs text från bild – Ladda källbilden

Nu pekar vi motorn på filen som innehåller den visuella texten.

```csharp
// Step 3: Load the image that contains the text
ocrEngine.Image = ImageStream.FromFile(@"C:\OCR\Samples\hindi_page.jpg");
```

*Varför detta är viktigt:* `ImageStream.FromFile` konverterar den råa filen till ett bitmap‑format som OCR‑kärnan kan förstå. Att ange en korrupt eller ej stödd format (som SVG) kommer att orsaka ett undantag.

> **Watch out:** Stora bilder kan förbruka mycket minne. Om du bearbetar högupplösta skanningar, överväg att skala ner med `Image.Resize` innan du skickar dem till motorn.

---

### Konvertera bild till text – Kör igenkänningen

Med motorn redo och bilden laddad, anropar vi slutligen OCR‑processen.

```csharp
// Step 4: Perform the OCR operation
ocrEngine.Recognize();
```

*Varför detta är viktigt:* `Recognize` triggar en serie interna steg – förbehandling, segmentering, teckenklassificering och efterbehandling. Anropet är blockande, vilket betyder att tråden väntar tills texten är klar.

> **Performance note:** På en vanlig stationär dator tar igenkänning av en 300 dpi‑sida < 1 sekund. På en server kan du vilja köra detta i en bakgrundsuppgift för att undvika UI‑frysningar.

---

### Så extraherar du text – Hämta resultatet

När igenkänningen är klar lagrar motorn den rena textutmatningen i `Text`‑egenskapen.

```csharp
// Step 5: Output the recognized text
Console.WriteLine(ocrEngine.Text);
```

*Varför detta är viktigt:* `Text`‑egenskapen ger dig en ren UTF‑8‑sträng som du kan skriva till en fil, mata in i en databas eller skicka till efterföljande NLP‑pipelines.

> **Expected output:** För exempel‑Hindi‑sidan kan du se något i stil med  
> `यह एक उदाहरण पाठ है जो OCR द्वारा पहचाना गया है।`  
> (Den exakta utmatningen beror på bildkvalitet och språkmodell.)

---

## Ytterligare överväganden för projekt i verkligheten

Nedan är några “what‑if”-scenarier du sannolikt stöter på när du försöker **extrahera text från bild** i produktion.

### Hantera flera bilder i en loop

Om du behöver **konvertera bild till text** för dussintals filer, slå in stegen i en `foreach`‑loop och återanvänd samma `ocrEngine`:

```csharp
string[] files = Directory.GetFiles(@"C:\OCR\Batch\", "*.jpg");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    ocrEngine.Recognize();
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), ocrEngine.Text);
}
```

### Hantera lågkvalitativa skanningar

- **Pre‑process** med binarisering (`Image.Binarize()`), brusreducering eller rakning.
- **Increase DPI** när du skannar (300 dpi är en säker baslinje).
- **Choose a language model** som stödjer skriptets ligaturer (t.ex. Devanagari för Hindi).

### Läsa text från bild på webben

När bilden kommer från en URL, ladda ner den till en minnesström först:

```csharp
using (HttpClient client = new())
{
    byte[] data = await client.GetByteArrayAsync(imageUrl);
    using var ms = new MemoryStream(data);
    ocrEngine.Image = ImageStream.FromStream(ms);
    ocrEngine.Recognize();
    Console.WriteLine(ocrEngine.Text);
}
```

### Trådsäkerhet och parallellism

De flesta OCR‑bibliotek är **not** trådsäkra ur lådan. Om du planerar att **read text from picture** samtidigt, starta separata `OcrEngine`‑instanser per tråd, eller använd en producent‑konsument‑kö för att serialisera åtkomst.

---

## Komplett fungerande exempel

När vi sätter ihop allt, här är en färdig att köra konsolapp som demonstrerar **how to perform OCR**, **extract text from image**, och **read text from picture** i ett sammanhängande program.

```csharp
using System;
using OcrLibrary;               // Adjust to your OCR library's namespace
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Choose the language (Hindi in this case)
        ocrEngine.Language = Language.Hindi;

        // Load the image file
        string imagePath = @"C:\OCR\Samples\hindi_page.jpg";
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }

        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // Run the recognition process
        ocrEngine.Recognize();

        // Output the extracted text
        string result = ocrEngine.Text;
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(result);

        // Optional: Save to a .txt file
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, result);
        Console.WriteLine($"Text saved to {txtPath}");
    }
}
```

**What you should see:** Konsolen skriver ut den Hindi‑mening som extraherats från `hindi_page.jpg`, följt av en bekräftelse på att textfilen skapades. Om bilden är ren, kommer utdata att vara praktiskt taget identisk med den ursprungliga tryckta texten.

---

## Slutsats

Du vet nu **how to perform OCR** i C# från början till slut, hur du **extract text from image**, **convert image to text**, och **read text from picture** med ett enkelt `OcrEngine`‑arbetsflöde. Det femstegs‑mönstret – create, set language, load, recognize, read – täcker de flesta användningsfall, och de extra tipsen hjälper dig att hantera batch‑jobb, lågkvalitativa skanningar och webbaserade källor.

Redo för nästa utmaning? Prova att byta språk till engelska, mata in en PDF‑sida renderad som en bild, eller kedja OCR‑utdata till en sök‑index‑pipeline. Himlen är gränsen när du har bemästrat grunderna i OCR i C#.

Har du frågor eller en knepig bild som inte samarbetar? Lämna en kommentar nedan, så felsöker vi tillsammans. Lycka till med kodandet!  

![how to perform OCR example](images/ocr-example.png "how to perform OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}