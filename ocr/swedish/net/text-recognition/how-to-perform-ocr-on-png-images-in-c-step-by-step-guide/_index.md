---
category: general
date: 2026-03-29
description: Hur man utför OCR i C# och läser text från PNG‑filer. Lär dig att extrahera
  rysk text, läsa text från PNG och hur man extraherar text med Aspose OCR.
draft: false
keywords:
- how to perform ocr
- read text from png
- how to extract text
- extract russian text
- c# ocr tutorial
language: sv
og_description: Hur man utför OCR i C# med Aspose OCR. Denna guide visar hur man läser
  text från png, extraherar rysk text och implementerar en komplett C# OCR‑lösning.
og_title: Hur man utför OCR i C# – Fullständig PNG‑textutvinning
tags:
- OCR
- C#
- Aspose
title: Hur man utför OCR på PNG‑bilder i C# – Steg‑för‑steg‑guide
url: /sv/net/text-recognition/how-to-perform-ocr-on-png-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man utför OCR på PNG‑bilder i C# – Komplett handledning

Har du någonsin behövt **utföra OCR** på en skärmdump eller ett skannat dokument men varit osäker på var du ska börja i C#? Du är inte ensam. Utvecklare frågar ständigt, “Hur läser jag text från PNG‑filer utan att skicka dem till en extern tjänst?” Den goda nyheten är att med Aspose.OCR kan du **extrahera rysk text**, **läsa text från png**, och få en ren sträng tillbaka på bara några rader kod.

I den här handledningen går vi igenom allt du behöver: installera biblioteket, välja rätt språkmodell, köra igenkänningen och hantera vanliga fallgropar. I slutet kommer du att kunna **hur man extraherar text** från vilken PNG‑bild som helst, oavsett om det är engelska, ryska eller något av de 70+ språk som Aspose stödjer. Inga onödiga detaljer, bara ett praktiskt, körbart exempel som du kan klistra in i en konsolapp direkt.

---

## Vad du kommer att lära dig

- Installera och referera Aspose.OCR NuGet‑paketet.
- Initiera OCR‑motorn i dess standard auto‑download‑läge.
- Konfigurera motorn för att **extrahera rysk text** med den kyrilliska språkmodellen.
- Kör OCR på en lokal PNG‑fil och visa resultatet.
- Tips för att felsöka saknade språkfiler och förbättra noggrannheten.

**Förutsättningar**: .NET 6+ (eller .NET Framework 4.7.2+), Visual Studio 2022 eller VS Code, och en internetanslutning för första körningen (språkmodellen laddas ner automatiskt).

---

## Steg 1 – Installera Aspose.OCR‑paketet

För att komma igång, lägg till Aspose.OCR‑biblioteket i ditt projekt. Öppna en terminal i projektmappen och kör:

```bash
dotnet add package Aspose.OCR
```

Eller, om du föredrar Visual Studio‑gränssnittet, högerklicka på **Dependencies → Manage NuGet Packages**, sök efter **Aspose.OCR**, och klicka på **Install**.

> **Proffstips**: Paketet är bara några megabyte, och språkmodellerna hämtas vid behov, så du inte fyller upp din app med onödiga filer.

---

## Steg 2 – Initiera OCR‑motorn (Primärt nyckelord i handling)

Att skapa motorn är enkelt. Konstruktorn aktiverar automatiskt *auto‑download‑läge*, vilket betyder att första gången du begär ett språk som inte finns lokalt, så hämtar Aspose det åt dig.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine – it will download missing models automatically.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Choose the language model – Russian Cyrillic (downloads if missing).
        ocrEngine.Language = Language.RussianCyrillic;

        // 3️⃣ Run OCR on the PNG image.
        var ocrResult = ocrEngine.RecognizeImage("sample_russian.png");

        // 4️⃣ Output the recognized text.
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Varför detta är viktigt**: Genom att använda standard‑auto‑download‑läget undviker du manuell filhantering. Om du senare behöver **läsa text från png** på ett annat språk, ändra bara `Language.RussianCyrillic` till rätt enum‑värde.

---

## Steg 3 – Förbered din PNG‑bild

Se till att bilden du vill bearbeta är åtkomlig vid körning. Placera `sample_russian.png` i samma mapp som den kompilerade `.exe`, eller använd en absolut sökväg om du föredrar. Bilden bör vara en tydlig skanning eller skärmdump; OCR‑noggrannheten sjunker dramatiskt på suddiga eller kraftigt komprimerade PNG‑filer.

**Vanligt specialfall**: Om PNG‑filen innehåller flera språk kan du sätta `ocrEngine.Language = Language.Multilingual;` så att motorn automatiskt upptäcker varje block.

---

## Steg 4 – Kör applikationen och verifiera resultatet

Kompilera och kör programmet:

```bash
dotnet run
```

Du bör se den extraherade ryska texten skrivas ut i konsolen, något i stil med:

```
Привет, мир! Это пример текста на русском языке.
```

Om du får en tom sträng, dubbelkolla:

1. Att filvägen är korrekt.  
2. Att bilden inte är helt vit eller helt svart.  
3. Att språkmodellen har laddats ner framgångsrikt (titta efter en `Aspose.OCR`‑mapp under din användarprofil).

---

## Steg 5 – Avancerade justeringar för bättre noggrannhet

Även om standardinställningarna fungerar för de flesta fall, kan du vilja finjustera motorn:

| Inställning | Vad den gör | När den ska användas |
|------------|-------------|----------------------|
| `ocrEngine.PreprocessOptions.Deskew = true;` | Korrigerar lätt rotation | Skannade dokument som inte är perfekt inriktade |
| `ocrEngine.PreprocessOptions.RemoveNoise = true;` | Filtrerar bort bakgrundsspetter | Lågt kvalitativa PNG‑filer från mobilkameror |
| `ocrEngine.RecognitionOptions.CharWhitelist = "0123456789";` | Begränsar tecken till siffror | Extrahera siffror från fakturor |

Lägg till någon av dessa innan du anropar `RecognizeImage`:

```csharp
ocrEngine.PreprocessOptions.Deskew = true;
ocrEngine.PreprocessOptions.RemoveNoise = true;
```

---

## Steg 6 – Exportera resultat till en fil (valfritt)

Om du behöver **hur man extraherar text** till en fil för senare bearbetning, skriv helt enkelt resultatet till disk:

```csharp
System.IO.File.WriteAllText("ocr_output.txt", ocrResult.Text);
Console.WriteLine("OCR output saved to ocr_output.txt");
```

Nu har du en bestående kopia som kan matas in i en databas, ett sökindex eller en översättningsmotor.

---

## Vanliga frågor

**Q: Fungerar detta med andra bildformat som JPEG eller BMP?**  
A: Absolut. `RecognizeImage` accepterar alla format som stöds av .NET:s `System.Drawing`‑bibliotek, inklusive JPEG, BMP och TIFF.

**Q: Vad händer om jag behöver extrahera engelsk text i samma körning?**  
A: Skapa en andra `OcrEngine`‑instans med `Language.English` eller byt språkegenskapen mellan anrop.

**Q: Kan jag köra OCR i ett webb‑API utan att blockera huvudtråden?**  
A: Ja. Wrappa igenkänningsanropet i `Task.Run` eller använd den asynkrona överlagringen `RecognizeImageAsync` (tillgänglig i nyare Aspose‑versioner).

**Q: Finns det en gräns för storleken på PNG‑filen?**  
A: Biblioteket kan hantera stora bilder, men minnesanvändningen ökar med upplösningen. Om du får `OutOfMemoryException`, överväg att skala ner bilden först.

---

## Fullt fungerande exempel (Klar att kopiera‑klistra in)

Nedan är det kompletta programmet som du kan klistra in i ett nytt konsolprojekt (`dotnet new console`) och köra omedelbart efter att ha installerat NuGet‑paketet.

```csharp
// File: Program.cs
using System;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize OCR engine – auto‑download enabled.
            var ocrEngine = new OcrEngine();

            // Choose Russian Cyrillic language model.
            ocrEngine.Language = Language.RussianCyrillic;

            // Optional: improve accuracy for skewed or noisy images.
            ocrEngine.PreprocessOptions.Deskew = true;
            ocrEngine.PreprocessOptions.RemoveNoise = true;

            // Path to the PNG file you want to read.
            string imagePath = "sample_russian.png";

            // Perform OCR.
            OcrResult result = ocrEngine.RecognizeImage(imagePath);

            // Output the recognized text.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(result.Text);

            // Save to a text file for later use.
            System.IO.File.WriteAllText("ocr_output.txt", result.Text);
            Console.WriteLine("Result saved to ocr_output.txt");
        }
    }
}
```

**Förväntad konsolutdata** (förutsatt att exemplet innehåller frasen “Привет, мир!”):

```
=== OCR Result ===
Привет, мир! Это пример текста на русском языке.
Result saved to ocr_output.txt
```

---

## Slutsats

Vi har gått igenom **hur man utför OCR** på PNG‑bilder med C#, från installation av Aspose.OCR till anpassning av förbehandlingsalternativ och export av resultat. Du vet nu hur man **läser text från png**, **hur man extraherar text** på olika språk, och specifikt **extraherar rysk text** med minimal kod.

Redo för nästa utmaning? Prova att mata OCR‑utdata i ett språkdetekteringsbibliotek, eller kombinera det med Azure Cognitive Services för översättning. Himlen är gränsen när du kombinerar en pålitlig OCR‑motor med C#‑s kraftfulla ekosystem.

Om du fann denna **c# ocr tutorial** hjälpsam, ge den ett stjärnmärke, dela den med kollegor, eller lämna en kommentar med dina egna tips. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}