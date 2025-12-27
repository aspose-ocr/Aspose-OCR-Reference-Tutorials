---
date: 2025-12-27
description: Lär dig hur du använder Aspose.OCR för .NET för att extrahera text från
  en bild, känna igen text i bilder och konvertera en bild till PDF .NET i olika dokumentformat.
linktitle: Save Result as Document in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Konvertera bild till PDF .NET – Spara resultatet som dokument i OCR‑bildigenkänning
url: /sv/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertera bild till PDF .NET – Spara resultat som dokument i OCR‑bildigenkänning

## Introduction

Välkommen till den spännande världen av optisk teckenigenkänning (OCR) med Aspose.OCR för .NET! I den här handledningen kommer du att lära dig hur du **konverterar bild till PDF .NET**, extraherar text från bild och sparar OCR‑utdata i sökbara dokumentformat som PDF, DOCX, TXT och Excel. Oavsett om du behöver skapa en sökbar PDF eller exportera OCR‑resultat till Excel, så guidar stegen nedan dig snabbt och effektivt genom processen.

## Quick Answers
- **What does “image to pdf .net” mean?** It refers to converting image files into PDF documents using .NET libraries, in this case Aspose.OCR.  
- **Which formats can I export OCR results to?** DOCX, TXT, PDF, and XLSX are supported out‑of‑the‑box.  
- **Do I need a license for production use?** Yes, a commercial license is required for production; a free trial is available for evaluation.  
- **Can I extract searchable text from the PDF?** Absolutely – the PDF generated is an **ocr to searchable pdf** that you can index.  
- **What .NET versions are supported?** Aspose.OCR works with .NET Framework 4.5+, .NET Core 3.1+, and .NET 5/6+.  

## What is “image to pdf .net”?
“Image to PDF .NET” är processen att ta rasterbilder (PNG, JPEG, TIFF, etc.) och programmässigt omvandla dem till PDF‑filer med ett .NET‑bibliotek. Aspose.OCR konverterar inte bara bilden utan utför även OCR, så att du kan **känna igen text i bilder** och bädda in den texten i den resulterande PDF‑filen, vilket gör den sökbar.

## Why use Aspose.OCR for this task?
- **High accuracy** – advanced OCR engine that handles multiple languages and fonts.  
- **One‑step conversion** – you can both recognize text and save it directly to PDF, DOCX, TXT, or Excel without extra post‑processing.  
- **No external dependencies** – pure .NET library, no native binaries required.  
- **Flexibility** – easily switch output format to create a document from OCR or export OCR to Excel for data analysis.

## Prerequisites

Innan vi ger oss in på denna OCR‑resa, se till att du har följande förutsättningar på plats:

- Aspose.OCR för .NET. Säkerställ att du har Aspose.OCR‑biblioteket installerat. Du kan ladda ner det [here](https://releases.aspose.com/ocr/net/).

- Document Directory: Have a designated directory for your documents, and update the `dataDir` variable in the provided code accordingly.

## Import Namespaces

Börja med att importera de nödvändiga namnutrymmena. Dessa är byggstenarna som ger din kod OCR‑funktionalitet.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Now, let's break down the example into multiple steps:

## How to Convert Image to PDF .NET Using Aspose.OCR

### Step 1: Initialize Aspose.OCR

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Detta steg förbereder genom att initiera Aspose.OCR‑API‑t.

### Step 2: Recognize Image

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

Här använder vi Aspose.OCR för att **känna igen text i den angivna bilden** (byt ut `"sample.png"` mot din bildfil). Detta är där operationen **extract text from image** sker.

### Step 3: Save Result in Different Formats

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

Anpassa detta steg efter dina behov. Aspose.OCR låter dig **spara den igenkända texten i olika dokumentformat såsom DOCX, TXT, PDF och XLSX**, vilket effektivt **creates a document from OCR** eller **exports OCR to Excel**.

### Step 4: Display Success Message

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

Ett enkelt bekräftelsemeddelande som visar att processen slutfördes utan problem.

Genom att följa dessa steg har du framgångsrikt utnyttjat kraften i Aspose.OCR för .NET för att känna igen text i bilder och spara resultaten i olika dokumentformat, inklusive en **ocr to searchable pdf**.

## Common Issues and Solutions
- **Image not recognized** – Ensure the image has sufficient resolution (at least 300 dpi) and is in a supported format (PNG, JPEG, TIFF).  
- **Incorrect language detection** – Pass a `RecognitionSettings` object with the appropriate `Language` property set (e.g., `Language = Language.English`).  
- **Output file not created** – Verify that `dataDir` points to a valid, writable folder and that the file names are unique.

## Frequently Asked Questions

**Q: Is Aspose.OCR compatible with different image formats?**  
A: Yes, Aspose.OCR supports a wide range of image formats, ensuring flexibility in your OCR tasks.

**Q: Can I customize recognition settings for better accuracy?**  
A: Absolutely! Aspose.OCR provides recognition settings to fine‑tune the OCR process according to your specific requirements.

**Q: Is there a free trial available?**  
A: Yes, you can get started with a free trial [here](https://releases.aspose.com/).

**Q: How can I get temporary licenses for Aspose.OCR?**  
A: Temporary licenses can be obtained [here](https://purchase.aspose.com/temporary-license/).

**Q: Where can I seek help or connect with the community?**  
A: Join the Aspose.OCR community at [Aspose Forum](https://forum.aspose.com/c/ocr/16) for support and discussions.

## Conclusion

Sammanfattningsvis öppnar Aspose.OCR för .NET upp en värld av möjligheter för **image to pdf .net**‑konverteringar, textutvinning och dokumentgenerering. Oavsett om du extraherar data, skapar sökbara PDF‑filer eller exporterar OCR‑resultat till Excel, förenklar Aspose.OCR processen med sitt intuitiva API och robusta funktionsuppsättning.

---

**Last Updated:** 2025-12-27  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}