---
category: general
date: 2026-05-25
description: एक न्यूनतम ASP.NET Core API के साथ छवि से टेक्स्ट निकालना सीखें। POST
  के माध्यम से छवि अपलोड करें, मल्टीपार्ट फ़ॉर्म डेटा पढ़ें और छवि पर OCR करें।
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: hi
og_description: एक न्यूनतम ASP.NET Core API का उपयोग करके छवि से टेक्स्ट निकालें।
  यह गाइड दिखाता है कि POST के माध्यम से छवि कैसे अपलोड करें, मल्टीपार्ट फ़ॉर्म डेटा
  पढ़ें, और छवि पर OCR कैसे करें।
og_title: ASP.NET Core में छवि से टेक्स्ट निकालें – चरण‑दर‑चरण
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  headline: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  type: TechArticle
- description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  name: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  steps:
  - name: Breaking Down the Logic
    text: '| Step | What Happens | Why It Matters | |------|--------------|----------------|
      | **ReadFormAsync** | Parses the incoming *multipart/form-data* request. | Without
      this, you can’t access the uploaded files. | | **form.Files["image"]** | Retrieves
      the file whose form‑field name is `image`. | Guarant'
  - name: 1. Large Files
    text: 'The default request body limit is 30 MB. For larger scans you might need
      to adjust:'
  - name: 2. Asynchronous OCR
    text: Some OCR libraries expose async methods (`RecognizeAsync`). If yours does,
      replace `ocr.Recognize(img)` with `await ocr.RecognizeAsync(img)` and mark the
      lambda as `async`.
  - name: 3. Security Considerations
    text: '- **Validate file size** before loading it into memory. - **Sanitize the
      filename** if you ever write it to disk. - **Rate‑limit** the endpoint to avoid
      denial‑of‑service attacks.'
  - name: 4. GPU Acceleration
    text: If you uncomment the `engine.GpuDevice = new GpuDevice(0);` line and your
      hardware supports CUDA or DirectML, you’ll see a noticeable speed boost, especially
      on high‑resolution images.
  type: HowTo
tags:
- ASP.NET Core
- OCR
- Minimal API
title: ASP.NET Core Minimal API में छवि से पाठ निकालें – पूर्ण मार्गदर्शिका
url: /hi/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract Text from Image in ASP.NET Core Minimal API – Complete Guide

क्या आपने कभी सोचा है कि **छवि से टेक्स्ट निकालना** बिना भारी फ्रेमवर्क के कैसे किया जाए? आप अकेले नहीं हैं। कई डेवलपर्स को तेज़ तरीका चाहिए जहाँ उपयोगकर्ता एक तस्वीर ड्रॉप कर सके और तुरंत कच्चे अक्षर प्राप्त कर सके, चाहे वह रसीद स्कैन करना हो, हाथ से लिखे नोट्स को डिजिटल बनाना हो, या सर्च इंडेक्स को पावर देना हो।

इस ट्यूटोरियल में हम एक छोटा ASP.NET Core Minimal API बनाएँगे जो **POST के माध्यम से इमेज अपलोड** करता है, *multipart/form‑data* पेलोड को पार्स करता है, और फिर **इमेज पर OCR** को एक singleton `OcrEngine` की मदद से चलाता है। अंत तक आपके पास एक पूरी तरह चलने योग्य एप्लिकेशन होगा जिसे आप किसी भी .NET 8 प्रोजेक्ट में डाल सकते हैं और तुरंत इमेज से टेक्स्ट निकालना शुरू कर सकते हैं।

## What You’ll Build

- एक मिनिमल वेब ऐप जो `/ocr` पर सुनता है।
- एक एंडपॉइंट जो `multipart/form-data` POST अनुरोध के साथ भेजी गई इमेज फ़ाइल को स्वीकार करता है।
- लॉजिक जो अपलोड की गई फ़ाइल को पढ़ता है, उसे OCR इंजन को देता है, और प्लेन‑टेक्स्ट परिणाम लौटाता है।
- वैकल्पिक GPU एक्सेलेरेशन स्निपेट (कमेंटेड) उन लोगों के लिए जिनके पास संगत कार्ड है।

**Prerequisites**  
- .NET 8 SDK (या बाद का संस्करण)।  
- C# और कमांड लाइन की बुनियादी जानकारी।  
- एक OCR लाइब्रेरी जो `OcrEngine` क्लास प्रदान करती है (सैंपल एक काल्पनिक NuGet पैकेज मानता है)।  

यदि आपके पास ये हैं, तो चलिए शुरू करते हैं।

## Step 1: Set Up the Project and Add the OCR Package

पहले, एक नया वेब प्रोजेक्ट बनाइए और OCR लाइब्रेरी जोड़िए।

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **Pro tip:** अपनी डिपेंडेंसीज़ को अपडेटेड रखें। नए वर्ज़न अक्सर परफ़ॉर्मेंस सुधार लाते हैं, विशेषकर GPU‑accelerated inference के लिए।

## Step 2: Register a Singleton OCR Engine (Primary Service)

हम चाहते हैं कि पूरे ऐप के लिए एक ही `OcrEngine` इंस्टेंस रहे—प्रत्येक अनुरोध पर नया इंजन बनाने की ज़रूरत नहीं। इसे बिल्डर की सर्विस कंटेनर में रजिस्टर करें।

```csharp
using Awesome.Ocr;               // <-- the OCR library namespace
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using System.Drawing;            // System.Drawing.Common for Image handling

var builder = WebApplication.CreateBuilder(args);

// Register a singleton OCR engine (English language)
// Uncomment the GPU line if you have a compatible GPU and the library supports it.
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU acceleration
    return engine;
});
```

**Why a singleton?**  
OCR इंजन बनाना महंगा हो सकता है—जैसे न्यूरल‑नेटवर्क वज़न को मेमोरी में लोड करना। वही इंस्टेंस दोबारा उपयोग करके हम CPU साइकिल और RAM दोनों बचाते हैं, जिससे हर `/ocr` कॉल के लिए तेज़ रिस्पॉन्स टाइम मिलता है।

## Step 3: Build the Application

अब हम `WebApplication` ऑब्जेक्ट को वास्तविक रूप देते हैं।

```csharp
var app = builder.Build();
```

यह लाइन लगभग जादुई लगती है, लेकिन अंदर से यह रूटिंग, मिडलवेयर, और DI कंटेनर को कॉन्फ़िगर करती है जिसे हमने अभी सेट किया था।

## Step 4: Define the POST Endpoint – “Upload Image via POST”

यहाँ ट्यूटोरियल का मुख्य भाग है: एक एंडपॉइंट जो **POST के माध्यम से इमेज अपलोड** करता है, multipart पेलोड पढ़ता है, और डेटा को OCR इंजन को देता है।

```csharp
app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    // Step 5: Read multipart form data and extract the uploaded image
    var form = await request.ReadFormAsync();               // <-- read multipart/form-data
    var file = form.Files["image"];                         // expects a field named "image"

    if (file is null || file.Length == 0)
    {
        return Results.BadRequest("No image file provided.");
    }

    // Guard against unsupported content types
    if (!file.ContentType.StartsWith("image/"))
    {
        return Results.BadRequest("Uploaded file is not an image.");
    }

    // Load the image into a System.Drawing.Image
    using var img = Image.FromStream(file.OpenReadStream());

    // Step 6: Perform OCR on the image
    string text = ocr.Recognize(img);                       // <-- perform OCR on image

    // Step 7: Return the extracted text as plain‑text
    return Results.Text(text);
});
```

### Breaking Down the Logic

| चरण | क्या होता है | क्यों महत्वपूर्ण है |
|------|--------------|-------------------|
| **ReadFormAsync** | इनकमिंग *multipart/form-data* अनुरोध को पार्स करता है। | इसके बिना आप अपलोड की गई फ़ाइलों तक पहुँच नहीं सकते। |
| **form.Files["image"]** | उस फ़ाइल को प्राप्त करता है जिसका फ़ॉर्म‑फ़ील्ड नाम `image` है। | कॉलर्स के लिए एक पूर्वनिर्धारित कॉन्ट्रैक्ट सुनिश्चित करता है। |
| **Content‑type check** | फ़ाइल का इमेज होना सत्यापित करता है (जैसे `image/png`)। | OCR इंजन को नॉन‑इमेज डेटा पर फेल होने से रोकता है। |
| **Image.FromStream** | रॉ स्ट्रीम को `System.Drawing.Image` में बदलता है। | OCR लाइब्रेरी को `Image` ऑब्जेक्ट चाहिए, न कि रॉ बाइट ऐरे। |
| **ocr.Recognize(img)** | OCR इंजन को **इमेज से टेक्स्ट कैसे पहचानें** को कॉल करता है। | यह मुख्य **इमेज पर OCR** स्टेप है। |
| **Results.Text** | प्लेन‑टेक्स्ट रिस्पॉन्स वापस भेजता है। | डाउनस्ट्रीम सर्विसेज के लिए एक सरल, उपयोगी फ़ॉर्मेट। |

## Step 5: Run the API

अंत में, वेब सर्वर को स्टार्ट करें।

```csharp
app.Run();
```

जब आप `dotnet run` चलाते हैं, API `http://localhost:5000` (या आपकी चुनी हुई पोर्ट) पर सुनना शुरू कर देगा। आप इसे `curl` से टेस्ट कर सकते हैं:

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**Expected output:** कंसोल में पहचाने गए अक्षर प्रिंट होंगे, उदाहरण के तौर पर:

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

यदि इमेज धुंधली है या भाषा समर्थित नहीं है, तो OCR इंजन खाली स्ट्रिंग या एरर मैसेज लौटाएगा—प्रोडक्शन कोड में इन केसों को हैंडल करें।

## Edge Cases & Best Practices

### 1. Large Files

डिफ़ॉल्ट रिक्वेस्ट बॉडी लिमिट 30 MB है। बड़े स्कैन के लिए आपको इसे समायोजित करना पड़ सकता है:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. Asynchronous OCR

कुछ OCR लाइब्रेरी async मेथड (`RecognizeAsync`) प्रदान करती हैं। यदि आपका ऐसा है, तो `ocr.Recognize(img)` को `await ocr.RecognizeAsync(img)` से बदलें और लैम्ब्डा को `async` मार्क करें।

### 3. Security Considerations

- **फ़ाइल साइज वैलिडेट** करें इससे पहले कि उसे मेमोरी में लोड करें।  
- **फ़ाइलनाम को सैनिटाइज़** करें यदि आप उसे डिस्क पर लिखते हैं।  
- **रेट‑लिमिट** लागू करें ताकि डिनायल‑ऑफ़‑सर्विस अटैक से बचा जा सके।

### 4. GPU Acceleration

यदि आप `engine.GpuDevice = new GpuDevice(0);` लाइन को अनकमेंट करते हैं और आपका हार्डवेयर CUDA या DirectML सपोर्ट करता है, तो आप तेज़ प्रोसेसिंग देखेंगे, विशेषकर हाई‑रेज़ोल्यूशन इमेज पर।

## Full Working Example

नीचे पूरा `Program.cs` दिया गया है जिसे आप एक नए Minimal API प्रोजेक्ट में कॉपी‑पेस्ट कर सकते हैं।

```csharp
using Awesome.Ocr;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Http.Features;
using System.Drawing;

var builder = WebApplication.CreateBuilder(args);

// Optional: increase multipart limit for big images
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});

// Register the OCR engine as a singleton
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU if available
    return engine;
});

var app = builder.Build();

app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    var form = await request.ReadFormAsync();
    var file = form.Files["image"];

    if (file is null || file.Length == 0)
        return Results.BadRequest("No image file provided.");

    if (!file.ContentType.StartsWith("image/"))
        return Results.BadRequest("Uploaded file is not an image.");

    using var img = Image.FromStream(file.OpenReadStream());

    // Core OCR operation
    string text = ocr.Recognize(img);

    return Results.Text(text);
});

app.Run();
```

सेव करें, `dotnet run` चलाएँ, और आप **इमेज से टेक्स्ट निकालने** के लिए तैयार हैं।

## Conclusion

हमने ASP.NET Core Minimal API का उपयोग करके इमेज से टेक्स्ट निकालने के लिए **पूरा, एंड‑टू‑एंड समाधान** पर काम किया। प्रोजेक्ट सेटअप से लेकर **singleton OCR इंजन रजिस्टर** करने, **POST के माध्यम से इमेज अपलोड** करने, **multipart फ़ॉर्म डेटा पढ़ने**, और अंत में **इमेज पर OCR** करके साफ़ प्लेन‑टेक्स्ट लौटाने तक का सफ़र तय किया।

अब आप कर सकते हैं:

- रिचर रिस्पॉन्स के लिए JSON रैपर जोड़ें।  
- निकाले गए टेक्स्ट को स्टोर करने के लिए डेटाबेस इंटीग्रेट करें।  
- कई भाषाओं (`OcrLanguage.Spanish` आदि) को सपोर्ट करने के लिए विस्तार करें।  

यह पैटर्न आसानी से स्केल करता है—इसे किसी बड़े माइक्रोसर्विस में डालें या API गेटवे के पीछे एक्सपोज़ करें।

PDF हैंडलिंग, बैच प्रोसेसिंग, या GPU ट्यूनिंग के बारे में सवाल हैं? कमेंट करें, और हैप्पी कोडिंग!

## Related Tutorials

- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}