---
category: general
date: 2026-04-26
description: C# के साथ PNG फ़ाइलों से तेज़ी से टेक्स्ट निकालें। जानें कैसे छवियों
  को टेक्स्ट में बदलें, PNG फ़ाइलें पढ़ें, छवियों के माध्यम से लूप करें और मिनटों
  में बैच OCR छवियों को प्रोसेस करें।
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: hi
og_description: C# के साथ PNG फ़ाइलों से तेज़ी से टेक्स्ट निकालें। यह गाइड दिखाता
  है कि कैसे छवियों को टेक्स्ट में बदलें, PNG फ़ाइलें पढ़ें, छवियों के माध्यम से लूप
  करें और बैच OCR छवियों को प्रोसेस करें।
og_title: PNG से टेक्स्ट निकालें – पूर्ण C# बैच OCR ट्यूटोरियल
tags:
- C#
- OCR
- Aspose
title: PNG से टेक्स्ट निकालें – पूर्ण C# बैच OCR ट्यूटोरियल
url: /hi/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG से टेक्स्ट निकालें – पूर्ण C# बैच OCR ट्यूटोरियल

क्या आपको कभी **PNG से टेक्स्ट निकालने** की ज़रूरत पड़ी है लेकिन आप नहीं जानते थे कि कहाँ से शुरू करें? आप अकेले नहीं हैं—कई डेवलपर्स को पहली बार स्क्रीनशॉट्स के फ़ोल्डर पर OCR करने की कोशिश में यही समस्या आती है। अच्छी खबर यह है कि कुछ ही C# और Aspose OCR की लाइनों के साथ आप इमेजेज़ को टेक्स्ट में बदल सकते हैं, PNG फ़ाइलें पढ़ सकते हैं, इमेजेज़ के माध्यम से लूप कर सकते हैं, और सब कुछ एक साथ बैच‑प्रोसेस कर सकते हैं।  

इस ट्यूटोरियल में हम एक तैयार‑चलाने‑योग्य कंसोल ऐप के माध्यम से यह सब करेंगे। अंत तक आपके पास एक स्व‑समाहित समाधान होगा जो किसी डायरेक्टरी में हर PNG से टेक्स्ट निकालता है और प्रत्येक इमेज के बगल में एक समान `.txt` फ़ाइल रखता है। कोई अतिरिक्त स्क्रिप्ट नहीं, कोई मैन्युअल कॉपी‑पेस्ट नहीं—सिर्फ शुद्ध कोड।

## आपको क्या चाहिए

- **.NET 6 SDK** (या कोई भी नया .NET संस्करण)। यह मुफ्त है, तेज़ है, और हर जगह काम करता है।
- **Aspose.OCR for .NET** (NuGet पैकेज)। लाइब्रेरी में GPU एक्सेलेरेशन शामिल है यदि आपके पास संगत GPU है, लेकिन यह स्वचालित रूप से CPU पर भी फ़ॉल्बैक करता है।
- एक फ़ोल्डर जिसमें कुछ **PNG इमेजेज़** हों जिन्हें आप प्रोसेस करना चाहते हैं।  
- एक टेक्स्ट एडिटर या IDE—Visual Studio, VS Code, Rider—जैसा भी आपको पसंद हो।

बस इतना ही। यदि आपके पास ये सब हैं, तो आप शुरू करने के लिए तैयार हैं।

![C# बैच OCR का उपयोग करके PNG से टेक्स्ट निकालें](image.png "PNG से टेक्स्ट निकालने का डेमो स्क्रीनशॉट")

*छवि वैकल्पिक पाठ: “C# बैच OCR का उपयोग करके PNG से टेक्स्ट निकालें”*

## चरण 1 – प्रोजेक्ट सेट अप करें और Aspose.OCR इंस्टॉल करें

पहले, एक नया कंसोल प्रोजेक्ट बनाएं और Aspose OCR पैकेज को जोड़ें।

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

हम कंसोल ऐप क्यों उपयोग करते हैं? यह बैच जॉब्स के लिए सबसे सरल होस्ट है, और आप इसे कमांड लाइन से चला सकते हैं या टास्क रनर के साथ शेड्यूल कर सकते हैं। यदि बाद में आपको UI चाहिए, तो आप कोर लॉजिक को एक क्लास लाइब्रेरी में ले जा सकते हैं।

## चरण 2 – GPU‑एक्सेलेरेटेड OCR इंजन (या CPU फ़ॉलबैक) को इनिशियलाइज़ करें

Aspose एक `GpuOcrEngine` प्रदान करता है जो स्वचालित रूप से समर्थित GPU का पता लगाता है। यदि कोई नहीं मिलता, तो यह सामान्य CPU इंजन पर वापस आ जाता है—कोई अतिरिक्त कोड नहीं चाहिए।

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create the OCR engine – GPU if available, otherwise CPU
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;   // Latin covers most Western alphabets

        // The rest of the code lives in a separate method for clarity
        ProcessFolder(ocrEngine, @"C:\MyPngFolder");
    }

    // …
}
```

**Pro tip:** यदि आप GPU के बिना हेडलेस सर्वर पर हैं, तो आप `GpuOcrEngine` को `OcrEngine` से बदल सकते हैं और कोड बिल्कुल वही व्यवहार करेगा।

## चरण 3 – लक्ष्य डायरेक्टरी में इमेजेज़ पर लूप करें

हमें **इमेजेज़ पर लूप** करना है और केवल PNG फ़ाइलें चुननी हैं। `Directory.GetFiles` मेथड यह काम करता है, और हम खाली फ़ोल्डर की स्थिति को भी संभालेंगे।

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    if (!Directory.Exists(folderPath))
    {
        Console.WriteLine($"❌ Folder not found: {folderPath}");
        return;
    }

    // Grab every *.png file – this is the “read png files” part
    string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

    if (pngFiles.Length == 0)
    {
        Console.WriteLine("⚠️ No PNG files found. Make sure the folder contains .png images.");
        return;
    }

    foreach (var pngPath in pngFiles)
    {
        Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
        ExtractAndSave(engine, pngPath);
    }
}
```

ध्यान दें `SearchOption.TopDirectoryOnly` के उपयोग पर। यदि बाद में आपको सब‑फ़ोल्डर्स में रीकर्स करना है, तो बस `AllDirectories` में बदल दें। यह छोटा बदलाव आपको पूरे ट्री में **इमेजेज़ को टेक्स्ट में बदलने** की अनुमति देता है, एक ही लाइन में।

## चरण 4 – OCR करें और परिणाम सहेजें

अब **बैच OCR इमेजेज़** वर्कफ़्लो का मुख्य भाग आता है। हम प्रत्येक PNG को लोड करते हैं, `Recognize()` चलाते हैं, और निकाले गए स्ट्रिंग को उसी बेस नाम वाली `.txt` फ़ाइल में लिखते हैं।

```csharp
static void ExtractAndSave(OcrEngine engine, string imagePath)
{
    try
    {
        // Load the PNG into the engine
        engine.Image = ImageStream.FromFile(imagePath);

        // Run recognition – this returns a RecognitionResult object
        RecognitionResult result = engine.Recognize();

        // Build the output path (same name, .txt extension)
        string txtPath = Path.ChangeExtension(imagePath, ".txt");

        // Write the OCR text to disk
        File.WriteAllText(txtPath, result.Text);

        Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        // Edge case: corrupted PNG or unsupported format
        Console.WriteLine($"❗ Error processing {Path.GetFileName(imagePath)}: {ex.Message}");
    }
}
```

**try/catch में क्यों रखें?** वास्तविक दुनिया की इमेज बैच में अक्सर कोई टूटी फ़ाइल या असामान्य कलर प्रोफ़ाइल वाली PNG मिलती है। एक्सेप्शन को पकड़ने से पूरी रन क्रैश नहीं होती और आप बाकी फ़ाइलों को प्रोसेस करना जारी रख सकते हैं।

## चरण 5 – एप्लिकेशन चलाएँ और आउटपुट सत्यापित करें

ऐप को बिल्ड और लॉन्च करें:

```bash
dotnet run
```

आपको कंसोल लॉग कुछ इस तरह दिखना चाहिए:

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

किसी भी जनरेट की गई `.txt` फ़ाइल को खोलें—यहाँ आपका निकाला गया टेक्स्ट है। यदि फ़ाइल खाली है, तो इमेज की क्वालिटी दोबारा जांचें; OCR स्पष्ट, हाई‑कॉन्ट्रास्ट टेक्स्ट के साथ सबसे अच्छा काम करता है।

### त्वरित सत्यापन स्क्रिप्ट (वैकल्पिक)

यदि आप सुनिश्चित करना चाहते हैं कि हर PNG को एक मिलती‑जुलती टेक्स्ट फ़ाइल मिली है, तो यह छोटा PowerShell वन‑लाइनर चलाएँ:

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## सामान्य विविधताएँ और किनारे के मामलों

| Situation | What to Change |
|-----------|----------------|
| **गैर‑लैटिन भाषाएँ** (जैसे, Cyrillic) | Set `ocrEngine.Language = Language.Cyrillic;` |
| **बड़ी इमेज सेट (>10 000 फ़ाइलें)** | Use `Parallel.ForEach` to speed up processing, but watch GPU memory usage. |
| **मूल इमेज क्रम को बनाए रखना है** | Sort `pngFiles` before the `foreach` (`Array.Sort(pngFiles);`). |
| **GPU के बिना CI सर्वर पर चलाना** | Replace `GpuOcrEngine` with `OcrEngine` to avoid GPU initialization errors. |
| **आप केवल उन फ़ाइलों को प्रोसेस करना चाहते हैं जिनमें एक विशिष्ट कुंजी शब्द हो** | After `result.Text` is retrieved, check `result.Text.Contains("Invoice")` before writing the file. |

इन बदलावों से आप **इमेजेज़ को टेक्स्ट में बदलने** पाइपलाइन को लगभग किसी भी परिदृश्य के अनुसार अनुकूलित कर सकते हैं।

## पूर्ण स्रोत कोड (कॉपी‑पेस्ट तैयार)

```csharp
// ------------------------------------------------------------
// Extract Text from PNG – Batch OCR using Aspose.OCR (C#)
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine (GPU if possible)
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;

        // 2️⃣ Define the folder that holds your PNG files
        string targetFolder = @"C:\MyPngFolder";   // <-- change to your path

        // 3️⃣ Process every PNG in the folder
        ProcessFolder(ocrEngine, targetFolder);
    }

    static void ProcessFolder(OcrEngine engine, string folderPath)
    {
        if (!Directory.Exists(folderPath))
        {
            Console.WriteLine($"❌ Folder not found: {folderPath}");
            return;
        }

        string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

        if (pngFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No PNG files found.");
            return;
        }

        foreach (var pngPath in pngFiles)
        {
            Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
            ExtractAndSave(engine, pngPath);
        }
    }

    static void ExtractAndSave(OcrEngine engine, string imagePath)
    {
        try
        {
            engine.Image = ImageStream.FromFile(imagePath);
            RecognitionResult result = engine.Recognize();

            string txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, result.Text);

            Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❗ Error on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

इसे `Program.cs` के रूप में सेव करें, `dotnet run` चलाएँ, और जादू देखें।

## निष्कर्ष

अब आपके पास C# का उपयोग करके **PNG फ़ाइलों से टेक्स्ट निकालने का पूर्ण, प्रोडक्शन‑रेडी तरीका** है। ट्यूटोरियल ने सब कुछ कवर किया—प्रोजेक्ट सेट अप करने से लेकर GPU‑एक्सेलेरेटेड OCR इंजन को इनिशियलाइज़ करने, **इमेजेज़ पर लूप** करने, **बैच OCR इमेजेज़** करने और परिणाम को प्लेन टेक्स्ट के रूप में सहेजने तक।  

यदि आप अगले कदमों के बारे में जिज्ञासु हैं, तो कोशिश करें:

- **इमेजेज़ को टेक्स्ट में बदलें** अन्य फ़ॉर्मैट्स (JPG, BMP

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}