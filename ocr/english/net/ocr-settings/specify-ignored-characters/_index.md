---
title: OCR Image Recognition Settings: Specify Ignored Characters
linktitle: OCR Image Recognition Settings: Specify Ignored Characters
second_title: Aspose.OCR .NET API
description: Learn how to configure OCR image recognition settings in Aspose.OCR for .NET, including specifying ignored characters for more accurate results.
weight: 14
url: /net/ocr-settings/specify-ignored-characters/
date: 2026-02-15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Image Recognition Settings: Specify Ignored Characters

## Introduction

In modern digital workflows, **ocr image recognition settings** are the key to turning noisy scans into clean, searchable text. Whether you’re processing invoices, passports, or multilingual documents, fine‑tuning these settings lets you exclude characters that would otherwise cause false positives. In this tutorial we’ll walk through how Aspose.OCR for .NET lets you configure the *IgnoredCharacters* option, giving you tighter control over the OCR output.

## Quick Answers
- **What does “IgnoredCharacters” do?** It tells the OCR engine to skip the listed characters during recognition.  
- **When should I use it?** Ideal for languages or templates where certain symbols never appear (e.g., a numeric form that never contains the letter “O”).  
- **Does it affect performance?** No noticeable impact; it simply filters results after recognition.  
- **Which version supports this?** All recent Aspose.OCR for .NET releases (tested with the latest 2026 build).  
- **Do I need a license?** A temporary or full license is required for production use.

## What Are OCR Image Recognition Settings?

OCR image recognition settings are a collection of parameters that influence how the engine interprets visual data. They include language selection, DPI handling, character whitelists/blacklists, and the *IgnoredCharacters* property we’ll focus on here. Adjusting these settings helps you achieve higher accuracy and reduces post‑processing cleanup.

## Why Specify Ignored Characters?

- **Reduce noise:** Prevents characters that are unlikely to appear from being mis‑detected.  
- **Speed up validation:** Less text to validate downstream.  
- **Improve multilingual handling:** Exclude characters from a language set that aren’t relevant to your document.  

## Prerequisites

Before diving into the code, ensure you have the following:

1. **Aspose.OCR Installation** – Download the library from the [download page](https://releases.aspose.com/ocr/net/).  
2. **Document Directory Setup** – Create a folder for your sample images and note its full path; you’ll update the `dataDir` variable accordingly.  
3. **Temporary License (Optional)** – If you’re evaluating, obtain a temporary license from [here](https://purchase.aspose.com/temporary-license/).

## Import Namespaces

To start, add the required namespaces to your C# file:

```csharp
using System.IO;

using Aspose.OCR;
using System;
```

## Step‑by‑Step Guide to Configure Ignored Characters

### Step 1: Set Up Your Document Directory

Define the folder that contains the images you want to process. Replace the placeholder with the actual path on your machine.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

### Step 2: Initialize Aspose.OCR

Create an instance of the OCR engine. This object will be used to apply the recognition settings.

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Step 3: Recognize Image with Ignored Characters

Pass a `RecognitionSettings` object that includes the `IgnoredCharacters` property. In this example we ignore the characters **a**, **b**, and **1**.

```csharp
// Recognize image with specified ignored characters
RecognitionResult result = api.RecognizeImage(dataDir + "SpanishOCR.bmp", new RecognitionSettings
{
    IgnoredCharacters = "ab1"
});
```

### Step 4: Display Recognized Text

Output the OCR result to the console. You’ll see the recognized text **without** the ignored characters.

```csharp
// Display the recognized text
Console.WriteLine(result.RecognitionText);
```

## Common Issues and Solutions

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| Ignored characters still appear | The characters are part of a larger glyph (e.g., “ß” contains “b”) | Use a more specific `IgnoredCharacters` list or enable language‑specific settings. |
| No output is returned | Wrong file path or unsupported image format | Verify `dataDir` and ensure the image is a supported format (BMP, PNG, JPEG). |
| License exception | Running without a valid license in a non‑trial build | Apply a temporary or purchased license before calling the API. |

## Frequently Asked Questions

**Q: Can I use Aspose.OCR for .NET in non‑commercial projects?**  
A: Yes, both commercial and non‑commercial projects are allowed. See the [licensing details](https://purchase.aspose.com/buy) for specifics.

**Q: Is there a free trial available?**  
A: Absolutely! You can download a free trial [here](https://releases.aspose.com/) and evaluate all features before purchasing.

**Q: How can I get support for Aspose.OCR?**  
A: Visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) to ask questions and receive help from the community and Aspose engineers.

**Q: What languages does Aspose.OCR support?**  
A: A wide range of languages is supported; consult the official documentation for the full list.

**Q: Can I purchase a temporary license for short‑term testing?**  
A: Yes, temporary licenses are available [here](https://purchase.aspose.com/temporary-license/) and are perfect for proof‑of‑concept projects.

## Conclusion

By mastering **ocr image recognition settings**—specifically the `IgnoredCharacters` option—you can dramatically improve the cleanliness of your OCR output. The steps above give you a ready‑to‑run example; from here you can explore additional settings like language selection, DPI scaling, and custom character whitelists. For deeper exploration, check the full [documentation](https://reference.aspose.com/ocr/net/).

---

**Last Updated:** 2026-02-15  
**Tested With:** Aspose.OCR 24.11 for .NET (latest 2026 build)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}