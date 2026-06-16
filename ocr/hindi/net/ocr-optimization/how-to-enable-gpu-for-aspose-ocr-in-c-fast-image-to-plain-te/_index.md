---
category: general
date: 2026-02-24
description: Aspose OCR C# उदाहरण में GPU को कैसे सक्षम करें – छवि को जल्दी से साधारण
  टेक्स्ट में बदलें। इसमें GPU डिवाइस ID सेट करना और छवि का टेक्स्ट पढ़ने के लिए C#
  गाइड शामिल है।
draft: false
keywords:
- how to enable gpu
- image to plain text
- aspose ocr example
- set gpu device id
- read image text c#
language: hi
og_description: Aspose OCR C# उदाहरण में GPU को कैसे सक्षम करें। GPU डिवाइस आईडी सेट
  करना और C# में छवि का टेक्स्ट प्रभावी रूप से पढ़ना सीखें।
og_title: C# में Aspose OCR के लिए GPU कैसे सक्षम करें – तेज़ इमेज से साधारण टेक्स्ट
tags:
- Aspose OCR
- C#
- GPU acceleration
title: C# में Aspose OCR के लिए GPU कैसे सक्षम करें – तेज़ इमेज से साधारण टेक्स्ट
url: /hi/net/ocr-optimization/how-to-enable-gpu-for-aspose-ocr-in-c-fast-image-to-plain-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR में GPU कैसे सक्षम करें C# – तेज़ इमेज से प्लेन टेक्स्ट

क्या आप कभी सोचते रहे हैं **GPU को कैसे सक्षम करें** जब आप Aspose OCR का उपयोग करके तस्वीर को संपादन योग्य टेक्स्ट में बदलते हैं? आप अकेले नहीं हैं—कई डेवलपर्स बड़े इनवॉइस या स्कैन किए गए कॉन्ट्रैक्ट्स को प्रोसेस करते समय प्रदर्शन की दीवार से टकराते हैं। अच्छी खबर? एक इमेज को प्लेन टेक्स्ट में बदलना बहुत तेज़ हो सकता है जब आप अपने ग्राफ़िक्स कार्ड का उपयोग करते हैं।

इस गाइड में हम एक पूर्ण **Aspose OCR उदाहरण** के माध्यम से दिखाएंगे कि GPU को कैसे सक्षम करें, GPU डिवाइस ID सेट करें, और **C# शैली में इमेज टेक्स्ट पढ़ें**। अंत तक आपके पास एक चलाने योग्य प्रोग्राम होगा जो किसी भी समर्थित इमेज से टेक्स्ट निकालता है, वह भी CPU‑only तरीके की तुलना में बहुत कम समय में।

## आपको क्या चाहिए

- .NET 6.0 या बाद का संस्करण (API .NET Core और .NET Framework दोनों के साथ काम करता है)
- नवीनतम ड्राइवर स्थापित CUDA‑संगत GPU
- Aspose.OCR for .NET लाइसेंस (या एक फ्री ट्रायल, जो विकास के लिए काम करता है)
- Visual Studio 2022 (या कोई भी C# एडिटर जो आप पसंद करते हैं)

`Aspose.OCR` के अलावा कोई अतिरिक्त NuGet पैकेज आवश्यक नहीं है—सिर्फ लाइब्रेरी ही काफी है।

---

## चरण 1 – Aspose OCR NuGet पैकेज स्थापित करें

सबसे पहले, आधिकारिक Aspose OCR लाइब्रेरी को अपने प्रोजेक्ट में जोड़ें। Package Manager Console खोलें और चलाएँ:

```powershell
Install-Package Aspose.OCR
```

यह `Aspose.OCR.dll` और उसकी सभी डिपेंडेंसीज़ को जोड़ देगा। यदि आप GUI पसंद करते हैं, तो अपने प्रोजेक्ट पर राइट‑क्लिक → **Manage NuGet Packages** → *Aspose.OCR* खोजें और **Install** पर क्लिक करें।  

*Pro tip:* इंस्टॉल होने के बाद, Solution Explorer में **Dependencies** के तहत `Aspose.OCR` फ़ोल्डर दिखाई देना चाहिए।

## चरण 2 – एक साधारण Console App का ढांचा बनाएं

हम एक छोटा console app बनाएँगे जो पूरी प्रक्रिया को दर्शाता है। नया प्रोजेक्ट बनाएँ:

```bash
dotnet new console -n GpuOcrDemo
cd GpuOcrDemo
```

जेनरेटेड `Program.cs` को नीचे दिखाए गए पूर्ण कोड से बदलें। यह ढांचा हमें एक साफ़ एंट्री पॉइंट देता है और OCR लॉजिक पर ध्यान केंद्रित करने में मदद करता है।

## चरण 3 – GPU को कैसे सक्षम करें और GPU डिवाइस ID सेट करें

अब मुख्य भाग: **GPU को कैसे सक्षम करें** Aspose OCR में। लाइब्रेरी एक `OcrSettings` ऑब्जेक्ट प्रदान करती है जहाँ आप `UseGpu` को टॉगल कर सकते हैं और वैकल्पिक रूप से `GpuDeviceId` के माध्यम से विशिष्ट CUDA डिवाइस चुन सकते हैं। नीचे वही स्निपेट है जिसे आप अपने प्रोग्राम में एम्बेड करेंगे:

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration – this is the crucial “how to enable gpu” step
        ocrEngine.Settings = new OcrSettings()
        {
            UseGpu = true,          // Turn on GPU processing
            GpuDeviceId = 0         // Optional: select the first CUDA‑compatible device
        };

        // 3️⃣ Recognise text from an image (any supported format)
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/large_invoice.png");

        // 4️⃣ Output the plain‑text result to the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

### GPU क्यों सक्षम करें?

GPU को सक्षम करने से भारी काम—पिक्सेल प्री‑प्रोसेसिंग, कैरेक्टर सेगमेंटेशन, और न्यूरल नेटवर्क इनफ़रेंस—ग्राफ़िक्स कार्ड को सौंप दिया जाता है। एक मध्यम GTX 1650 पर, आप CPU‑only मोड की तुलना में **2‑3× गति वृद्धि** देख सकते हैं, विशेषकर हाई‑रिज़ॉल्यूशन दस्तावेज़ों के साथ।

### डिवाइस ID चुनना

यदि आपके मशीन में कई GPU हैं, तो `GpuDeviceId` आपको एक विशिष्ट डिवाइस टार्गेट करने की अनुमति देता है। `0` पहला डिवाइस चुनता है; `1` दूसरा, आदि। उपलब्ध ID को आप NVIDIA के `nvidia-smi` टूल से या Aspose के `GpuInfo` क्लास को क्वेरी करके (यहाँ संक्षिप्तता के लिए नहीं दिखाया गया) पता कर सकते हैं।

## चरण 4 – पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा, तैयार‑चलाने‑योग्य प्रोग्राम है। इसे `Program.cs` में पेस्ट करें, इमेज पाथ को अपने डिस्क पर मौजूद वास्तविक फ़ाइल से बदलें, और **F5** दबाएँ।

```csharp
// Program.cs – Complete Aspose OCR GPU example
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Validate the input argument (optional but handy)
            if (args.Length == 0)
            {
                Console.WriteLine("Usage: dotnet run <image_path>");
                return;
            }

            string imagePath = args[0];

            // Initialise the OCR engine
            var ocrEngine = new OcrEngine();

            // -------------------- How to Enable GPU --------------------
            // Turn on GPU acceleration and optionally pick a device
            ocrEngine.Settings = new OcrSettings()
            {
                UseGpu = true,          // Enables GPU processing
                GpuDeviceId = 0         // Selects the first CUDA‑compatible GPU
            };
            // ---------------------------------------------------------

            try
            {
                // Recognise the image – this is the “image to plain text” core
                var ocrResult = ocrEngine.RecognizeImage(imagePath);

                // Display the extracted text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Graceful error handling – helpful when the GPU is unavailable
                Console.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

### अपेक्षित आउटपुट

यदि प्रदान की गई इमेज में लाइन *“Invoice #12345 – Total $1,250.00”* मौजूद है, तो कंसोल प्रिंट करेगा:

```
=== Extracted Text ===
Invoice #12345 – Total $1,250.00
```

परिणाम प्लेन टेक्स्ट होगा, जिसे आगे प्रोसेस किया जा सकता है (जैसे डेटाबेस में डालना या नेचुरल‑लैंग्वेज पार्सर को फीड करना)।

## चरण 5 – GPU उपयोग की पुष्टि करें (वैकल्पिक)

यह सुनिश्चित करने के लिए कि GPU वास्तव में उपयोग हो रहा है, प्रोग्राम चलाते समय अपना GPU मॉनिटरिंग टूल (जैसे **NVIDIA‑Smi** या **GPU‑Z**) खोलें। चयनित डिवाइस के कंप्यूट उपयोग में स्पाइक दिखना चाहिए। यदि केवल CPU एक्टिविटी दिख रही है, तो दोबारा जांचें:

- GPU ड्राइवर अपडेटेड है।
- `UseGpu` फ़्लैग `true` पर सेट है।
- आपका इमेज फ़ॉर्मेट समर्थित है (PNG, JPEG, TIFF, आदि)।

## सामान्य समस्याएँ और उनके समाधान

| समस्या | क्यों होता है | त्वरित समाधान |
|-------|----------------|-----------|
| **GPU नहीं पहचाना गया** | पुराना ड्राइवर या गायब CUDA रनटाइम | नवीनतम NVIDIA ड्राइवर और CUDA टूलकिट इंस्टॉल करें |
| **`Aspose.OCR` “GPU not supported” त्रुटि देता है** | गैर‑CUDA GPU पर चल रहा है (जैसे पुराना AMD) | `UseGpu = false` सेट करें या संगत GPU पर स्विच करें |
| **गलत इमेज पाथ** | रिलेटिव पाथ गलत फ़ोल्डर की ओर इशारा कर रहा है | एब्सोल्यूट पाथ उपयोग करें या पाथ को कमांड‑लाइन आर्ग्यूमेंट के रूप में पास करें |
| **लाइसेंस लागू नहीं हुआ** | एवाल्यूएशन मोड GPU उपयोग को सीमित कर सकता है | `License license = new License(); license.SetLicense("Aspose.OCR.lic");` के साथ लाइसेंस रजिस्टर करें |

## उदाहरण का विस्तार: GPU के साथ बैच प्रोसेसिंग

यदि आपको दर्जनों इनवॉइस प्रोसेस करने हैं, तो रिकग्निशन कॉल को लूप में रखें। क्योंकि GPU वार्म रहता है, बाद की इमेजेज **warm‑up caching** से लाभ उठाती हैं, जिससे प्रत्येक रन में और भी मिलिसेकंड बचते हैं।

```csharp
string[] files = Directory.GetFiles(@"C:\Invoices\", "*.png");
foreach (var file in files)
{
    var result = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Trim()}");
}
```

ध्यान रखें कि वही `OcrEngine` इंस्टेंस रखें—प्रति फ़ाइल नया इंजन बनाना GPU कॉन्टेक्स्ट को री‑इनिशियलाइज़ कर देगा और प्रदर्शन घटा देगा।

## निष्कर्ष

अब आपके पास एक ठोस, एंड‑टू‑एंड **Aspose OCR उदाहरण** है जो दिखाता है **GPU को कैसे सक्षम करें**, **GPU डिवाइस ID कैसे सेट करें**, और **C# शैली में इमेज टेक्स्ट कैसे पढ़ें**। `UseGpu` को टॉगल करके और सही डिवाइस पॉइंट करके आप एक धीमे CPU‑बाउंड OCR जॉब को हाई‑थ्रूपुट पाइपलाइन में बदल सकते हैं, जो बड़े इनवॉइस, रसीद या किसी भी स्कैन किए गए दस्तावेज़ को संभाल सके।

बिना झिझक प्रयोग करें: विभिन्न इमेज फ़ॉर्मेट आज़माएँ, मल्टी‑GPU सेटअप पर `GpuDeviceId` समायोजित करें, या PDF जेनरेशन के लिए अन्य Aspose लाइब्रेरीज़ के साथ मिलाएँ। GPU के साथ काम शुरू होते ही संभावनाएँ असीमित हैं।

<img src="gpu-ocr.png" alt="Aspose OCR के साथ GPU कैसे सक्षम करें C# – इमेज को तेज़ी से प्लेन टेक्स्ट में बदलें">

*कोडिंग का आनंद लें! यदि कोई समस्या आती है, तो नीचे टिप्पणी करें या गहराई से सीखने के लिए Aspose के आधिकारिक फ़ोरम देखें।*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}