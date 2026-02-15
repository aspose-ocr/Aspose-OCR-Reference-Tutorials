---
category: general
date: 2026-02-14
description: Läs in bildfil och extrahera text från kvitto med Aspose OCR GPU-motor.
  Lär dig att ange maximalt GPU-minne, konfigurera GPU-minnet och köra OCR på bilden
  effektivt.
draft: false
keywords:
- load image file
- extract text from receipt
- set max gpu memory
- run OCR on image
- configure gpu memory
language: sv
og_description: Läs in bildfil och extrahera text från kvitto med Aspose OCR GPU-motorn.
  Denna guide visar hur du ställer in maximalt GPU-minne och kör OCR på bilden i C#.
og_title: Läs in bildfil & extrahera kvittotext med GPU‑OCR i C#
tags:
- C#
- OCR
- Aspose
- GPU
title: Läs in bildfil & extrahera kvittotext med GPU-OCR i C#
url: /sv/net/ocr-configuration/load-image-file-extract-receipt-text-with-gpu-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ladda bildfil & extrahera kvittotext med GPU OCR i C#

Har du någonsin behövt **load image file** och hämta exakt text från ett kvitto men känt dig fast vid OCR‑steget? Du är inte ensam. I många verkliga appar—utgiftsspårare, lagersystem eller till och med enkla kvitto‑skannings‑botar—kan förmågan att snabbt läsa en kvittobild vara en spelväxlare.  

Den goda nyheten? Med Aspose.OCR:s GPU‑accelererade motor kan du **load image file**, **set max GPU memory**, och **run OCR on image** i några få snygga rader C#. Nedan går vi igenom hela processen, från att konfigurera GPU:n till att skriva ut den extraherade ren‑texten.

## Vad du kommer att lära dig

* **Load image file** från disk med Aspose’s `ImageStream`.
* **Configure GPU memory** så att motorn aldrig använder mer RAM än du tillåter.
* **Run OCR on image** och hämta varje tecken på ett kvitto.
* Hantera vanliga fallgropar—som out‑of‑memory‑fel eller suddiga skanningar.
* Verifiera resultatet och justera inställningarna för bättre noggrannhet.

Inga externa tjänster, inga kryptiska knep—bara ren C#‑kod som du kan slänga in i vilket .NET 6+‑projekt som helst.

---

## Förutsättningar

Innan vi dyker ner, se till att du har:

* .NET 6 SDK eller senare installerat.
* En giltig Aspose.OCR‑licens (eller så kan du använda gratis utvärderingsläge).
* `Aspose.OCR` och `Aspose.OCR.Gpu` NuGet‑paket tillagda till ditt projekt.
* En exempelkvittobild (`receipt.png`) redo på disken.

Om något av detta låter obekant, pausa ett ögonblick och installera paketen:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Det är allt—inga extra inhemska bibliotek behövs eftersom GPU‑stöd är inbyggt direkt i NuGet‑paketet.

---

## Ladda bildfil och förbered GPU‑motor

Det första du måste göra är att **load image file** till en `ImageStream`. Detta objekt abstraherar bort filsystemdetaljer och ger OCR‑motorn en ren, in‑memory‑representation.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Step 1️⃣: Initialize the GPU‑accelerated engine.
var gpuEngine = new GpuEngine
{
    // Step 2️⃣: Set a safety net for GPU RAM usage.
    // Here we limit the engine to 1024 MB (1 GB). Adjust as needed.
    MaxDeviceMemory = 1024 // MB
};

// Step 3️⃣: Load the receipt image from disk.
var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

// At this point the image is ready for OCR.
```

**Varför detta är viktigt:**  
*Loading the image file* via `ImageStream.FromFile` garanterar att motorn ser exakt pixeldata, bevarar DPI och färgdjup. Att hoppa över detta steg eller mata in en korrupt ström kommer få OCR att missa tecken eller kasta undantag.

> **Pro tip:** Om du hanterar användar‑uppladdade filer, omge `FromFile`‑anropet med ett try‑catch‑block och validera filstorleken först. Stora bilder kan spränga GPU‑minnet om du inte har **configured GPU memory** korrekt.

---

## Ställ in max GPU‑minne för optimal prestanda

GPU‑resurser är värdefulla, särskilt på delade servrar eller bärbara med begränsad VRAM. `MaxDeviceMemory`‑egenskapen talar om för Aspose hur mycket av GPU‑minnet den säkert kan allokera.

```csharp
// Example: Restrict to 512 MB for low‑end GPUs.
gpuEngine.MaxDeviceMemory = 512; // MB
```

När du **set max GPU memory**, kommer motorn automatiskt att falla tillbaka till CPU‑bearbetning om den inte kan uppfylla begäran—vilket förhindrar krascher. Detta är det säkraste sättet att **configure GPU memory** utan att hårdkoda enhetsspecifika gränser.

**När du ska justera:**  
* Om du märker `OutOfMemoryException` under tung batch‑bearbetning, sänk gränsen.  
* Om dina kvitton är högupplösta (300 DPI+), höj den till 2 GB för att behålla hög hastighet.

---

## Kör OCR på bild för att extrahera text från kvitto

Nu blir det roligt—verkligen **run OCR on image** och hämta kvittots text. `Recognize`‑metoden returnerar ett `OcrResult`‑objekt som innehåller en `Text`‑egenskap med ren‑text‑utdata.

```csharp
// Step 4️⃣: Perform OCR.
OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

// Step 5️⃣: Output the extracted text.
Console.WriteLine("=== Receipt Text ===");
Console.WriteLine(ocrResult.Text);
```

Konsolen kommer att visa något liknande:

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

**Varför detta fungerar:**  
GPU‑motorn kör en deep‑learning‑modell som tränats på en mängd olika dokumentlayouter. Genom att mata in en ren, korrekt laddad bild ger du modellen den bästa chansen att **extract text from receipt** exakt.

---

## Verifiera resultatet och vanliga fallgropar

Även med en kraftfull motor är OCR inte magi. Här är några saker att hålla utkik efter:

| Problem | Orsak | Lösning |
|-------|-------|-----|
| Garbled characters | Low contrast or blurred image | Pre‑process with Aspose’s `ImageProcessor` to increase contrast |
| Missing lines | Image cropped too tightly | Ensure the receipt fits fully within the image bounds |
| Out‑of‑memory errors | `MaxDeviceMemory` too low for image size | Increase `MaxDeviceMemory` or downscale the image first |
| Wrong language | Receipt contains non‑English text | Set `gpuEngine.Language = OcrLanguage.Spanish;` (or appropriate) |

Om du stöter på någon av dessa, är en snabb lösning att ändra storlek på bilden till under 2000 px på den längsta sidan—det minskar GPU‑belastningen kraftigt utan att offra läsbarheten för de flesta kvitton.

---

## Fullt fungerande exempel (klar att kopiera‑klistra in)

Nedan är hela programmet, redo att kompileras. Ersätt filsökvägen med din egen kvittoplats.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

class ReceiptOcrDemo
{
    static void Main()
    {
        // 1️⃣ Create GPU‑accelerated engine with a safe memory cap.
        var gpuEngine = new GpuEngine
        {
            MaxDeviceMemory = 1024 // MB – adjust for your hardware
        };

        // 2️⃣ Load the receipt image from disk.
        //    Make sure the path points to a valid PNG/JPEG file.
        var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

        // 3️⃣ Run OCR – this will automatically use the GPU if available.
        OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

        // 4️⃣ Print the extracted text.
        Console.WriteLine("=== Receipt Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Förväntad konsolutmatning** (ditt kvitto kommer naturligtvis att skilja sig):

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

Kör programmet med `dotnet run`. Om du ser texten skrivas ut, grattis—du har framgångsrikt **load image file**, **set max GPU memory**, och **run OCR on image** för att **extract text from receipt**.

---

## Vanliga frågor

**Q: Fungerar detta på maskiner utan dedikerad GPU?**  
A: Ja. Aspose.OCR faller elegant tillbaka till CPU‑läge om ingen kompatibel GPU upptäcks. Du kommer fortfarande kunna **load image file** och **run OCR on image**, bara lite långsammare.

**Q: Kan jag bearbeta flera kvitton i en batch?**  
A: Absolut. Omge igenkänningskoden med en `foreach`‑loop, men kom ihåg att återanvända samma `GpuEngine`‑instans—det undviker att återinitiera GPU‑resurser för varje fil.

**Q: Vad händer om mitt kvitto är på ett annat språk än engelska?**  
A: Ställ in språket innan du anropar `Recognize`:

```csharp
gpuEngine.Language = OcrLanguage.French;
```

---

## Nästa steg & relaterade ämnen

Nu när du behärskar grunderna, överväg att utforska:

* **Fine‑tuning OCR accuracy** – experimentera med `gpuEngine.RecognitionOptions` såsom `EnableDeskew` eller `ContrastEnhancement`.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}