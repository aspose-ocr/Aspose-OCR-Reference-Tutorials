---
title: Specify Allowed Characters in OCR Image Recognition
linktitle: Specify Allowed Characters in OCR Image Recognition
second_title: Aspose.OCR .NET API
description: Unlock precise OCR in .NET with Aspose.OCR. Recognize text from images effortlessly. Download now for a transformative development experience.
type: docs
weight: 13
url: /net/ocr-settings/specify-allowed-characters/
---
## Introduction

In the ever-evolving landscape of technology, Optical Character Recognition (OCR) has emerged as a transformative tool, enabling machines to comprehend text from images. Aspose.OCR for .NET stands out as a powerful solution, providing seamless integration for developers seeking robust OCR capabilities in their .NET applications.

## Prerequisites

Before diving into the tutorial, ensure you have the following prerequisites in place:

- A working knowledge of .NET development.
- Aspose.OCR for .NET library. You can download it [here](https://releases.aspose.com/ocr/net/).
- Familiarity with Visual Studio or any other preferred .NET development environment.

## Import Namespaces

In your .NET project, import the necessary namespaces to leverage the functionalities of Aspose.OCR for .NET effectively:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Now, let's break down the tutorial into a series of comprehensive steps:

## Step 1: Specify Allowed Characters in OCR Image Recognition

To begin, set up the path to your document directory:

```csharp
string dataDir = "Your Document Directory";
```

## Step 2: Initialize Aspose.OCR with Allowed Symbols

Create an instance of AsposeOcr, specifying the allowed symbols. In this case, we're allowing digits (0-9):

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

## Step 3: Recognize Image

Utilize the AsposeOcr instance to recognize text from an image:

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

## Step 4: Display Recognized Text

Print the recognized text to the console:

```csharp
Console.WriteLine(result);
```

## Step 5: Second Case - Recognize Image with Specific Settings

Initialize another AsposeOcr instance, this time with more specific settings:

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

## Step 6: Display Second Case Recognized Text

Print the recognized text from the second case to the console:

```csharp
Console.WriteLine(result2.RecognitionText);
```

## Step 7: Successful Execution

Finally, confirm the successful execution of the SpecifyAllowedCharacters tutorial:

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

By following these steps, you've unlocked the capability to specify allowed characters in OCR image recognition using Aspose.OCR for .NET.

## Conclusion

Aspose.OCR for .NET empowers developers to seamlessly integrate OCR capabilities into their applications, opening doors to innovative solutions in various domains. Embrace the power of OCR and enhance your projects with accurate text recognition.

## FAQ's

### Q1: Is Aspose.OCR for .NET suitable for both beginners and experienced developers?

A1: Absolutely! Aspose.OCR for .NET caters to developers of all skill levels, providing intuitive functionalities for seamless integration.

### Q2: Can I use Aspose.OCR for .NET for recognizing characters in multiple languages?

A2: Yes, Aspose.OCR supports recognition in various languages, making it versatile for diverse applications.

### Q3: How often is Aspose.OCR for .NET updated?

A3: Updates are regularly released to ensure compatibility with the latest technologies and address any potential issues. Check the [documentation](https://reference.aspose.com/ocr/net/) for the latest information.

### Q4: Is there a free trial available for Aspose.OCR for .NET?

A4: Yes, you can explore the capabilities of Aspose.OCR by downloading the [free trial](https://releases.aspose.com/).

### Q5: Where can I seek assistance or connect with the community for support?

A5: Visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) to engage with the community and get expert assistance.
