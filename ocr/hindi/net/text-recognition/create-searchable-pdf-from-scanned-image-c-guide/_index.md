---
category: general
date: 2026-04-26
description: Aspose OCR का उपयोग करके C# में स्कैन की गई छवि से खोज योग्य PDF बनाएं।
  सीखें कि स्कैन की गई छवि को कैसे बदलें, टेक्स्ट निकालें, और जल्दी से खोज योग्य PDF
  जनरेट करें।
draft: false
keywords:
- create searchable pdf
- convert scanned image
- extract text from image
- how to ocr document
- convert tiff to pdf
language: hi
og_description: Aspose OCR का उपयोग करके स्कैन की गई छवि से खोज योग्य PDF बनाएं। परिवर्तन,
  टेक्स्ट निकालने और खोज योग्य PDF उत्पन्न करने के लिए चरण‑दर‑चरण C# कोड।
og_title: स्कैन की गई छवि से खोज योग्य PDF बनाएं – C# गाइड
tags:
- Aspose OCR
- C#
- PDF
- OCR
title: स्कैन की गई छवि से खोज योग्य PDF बनाएं – C# गाइड
url: /hi/net/text-recognition/create-searchable-pdf-from-scanned-image-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# स्कैन किए गए इमेज से सर्चेबल PDF बनाएं – C# गाइड

क्या आपको कभी कागज़ी अनुबंधों, रसीदों, या पुराने अभिलेखों से **searchable PDF** फ़ाइलें बनानी पड़ी हैं? आप अकेले नहीं हैं—अधिकांश डेवलपर्स इस समस्या का सामना करते हैं जब क्लाइंट एक ढेर सारा TIFF स्कैन देता है और अंतिम डिलिवरेबल के रूप में सर्चेबल PDF की अपेक्षा करता है।  

इस ट्यूटोरियल में हम आपको बिल्कुल दिखाएंगे **how to OCR a document** और स्कैन की गई इमेज को **searchable PDF** में बदलेंगे Aspose OCR for .NET के साथ। अंत तक आप **convert scanned image** फ़ाइलें, **extract text from image** डेटा, और यहाँ तक कि मल्टी‑पेज TIFF को भी आसानी से हैंडल कर पाएँगे।  

## आपको क्या चाहिए

* .NET 6.0 या बाद का संस्करण (API .NET Core, .NET Framework, और .NET 5+ के साथ काम करता है)।  
* एक वैध Aspose OCR लाइसेंस या आप एवाल्यूएशन वाटरमार्क से संतुष्ट हैं।  
* `Aspose.OCR` NuGet पैकेज इंस्टॉल किया हुआ (`dotnet add package Aspose.OCR`)।  
* एक सैंपल TIFF फ़ाइल (जैसे `contract_scan.tif`) जिसे आप सर्चेबल PDF में बदलना चाहते हैं।  

बस इतना ही—कोई अतिरिक्त लाइब्रेरी नहीं, कोई जटिल कॉन्फ़िगरेशन नहीं। तैयार हैं? चलिए शुरू करते हैं।

![Create searchable PDF example](create-searchable-pdf.png "create searchable pdf example")

## चरण 1 – OCR इंजन को इनिशियलाइज़ करें (Create Searchable PDF)

सबसे पहले: आपको एक `OcrEngine` इंस्टेंस चाहिए। यह ऑब्जेक्ट वह कार्यकर्ता है जो बिटमैप पढ़ता है, अक्षरों की पहचान करता है, और आपको टेक्स्ट वापस देता है।  

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine which language to look for – Latin works for most English documents
ocrEngine.Language = Language.Latin;
```

**भाषा क्यों सेट करें?**  
यदि आप इसे डिफ़ॉल्ट पर छोड़ देते हैं, तो Aspose सभी भाषा पैक्स को ट्राई करेगा, जिससे गति धीमी हो जाएगी। `Language.Latin` निर्दिष्ट करने से इंजन लैटिन अल्फ़ाबेट पर फोकस करता है, जिससे गति बढ़ती है और अंग्रेज़ी‑भाषा के अनुबंधों के लिए अधिक सटीक परिणाम मिलते हैं।  

## चरण 2 – अपनी स्कैन की हुई इमेज लोड करें (Convert Scanned Image)

अब हम इंजन को वह इमेज देते हैं जिसे हम प्रोसेस करना चाहते हैं। Aspose फ़ाइल पाथ, स्ट्रीम, या यहाँ तक कि `byte[]` को पढ़ सकता है। सरलता के लिए हम `ImageStream.FromFile` का उपयोग करेंगे।  

```csharp
// Load the TIFF (or any supported image format)
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\contract_scan.tif");
```

यदि आपको बाद में **convert TIFF to PDF** की आवश्यकता पड़े, तो ध्यान रखें कि मल्टी‑पेज TIFF स्वचालित रूप से हैंडल हो जाते हैं—प्रत्येक फ्रेम एक अलग PDF पेज बन जाता है।  

## चरण 3 – OCR चलाएँ और टेक्स्ट प्राप्त करें (Extract Text From Image)

OCR चलाना उतना ही आसान है जितना `Recognize` को कॉल करना। इंजन एक `RecognitionResult` लौटाएगा जिसमें प्लेन टेक्स्ट, कॉन्फिडेंस स्कोर, और लेआउट जानकारी होगी।  

```csharp
// Perform the OCR operation
RecognitionResult result = ocrEngine.Recognize();

// The raw text is available via the Text property
string extractedText = result.Text;

// Quick sanity check – print the first 200 characters
Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**Pro tip:** यदि आपको केवल टेक्स्ट चाहिए (PDF नहीं), तो आप यहाँ रुक सकते हैं और `extractedText` को `.txt` फ़ाइल में लिख सकते हैं। लेकिन अधिकांश समय हमारा लक्ष्य एक सर्चेबल PDF है, इसलिए हम आगे बढ़ेंगे।  

## चरण 4 – सर्चेबल PDF के रूप में सेव करें (Create Searchable PDF)

Aspose अंतिम चरण को बहुत आसान बनाता है: बस `Save` को `SaveFormat.PdfSearchable` के साथ कॉल करें। लाइब्रेरी एक्सट्रैक्टेड टेक्स्ट को एक अदृश्य लेयर के रूप में एम्बेड करती है जबकि मूल इमेज की उपस्थिति को बरकरार रखती है।  

```csharp
// Save the result as a searchable PDF
ocrEngine.Save(@"C:\Docs\contract_searchable.pdf", SaveFormat.PdfSearchable);
```

जब आप किसी भी PDF व्यूअर में `contract_searchable.pdf` खोलते हैं, तो आप टेक्स्ट को सेलेक्ट, कॉपी, और सर्च कर पाएँगे—बिल्कुल वही जो क्लाइंट “searchable PDF” से उम्मीद करता है।  

## मल्टी‑पेज TIFFs को हैंडल करना (Convert Tiff to PDF)

यदि आपकी स्रोत फ़ाइल में कई पेज हैं, तो Aspose प्रत्येक फ्रेम को स्वचालित रूप से एक अलग पेज के रूप में लेगा। अतिरिक्त लूप की जरूरत नहीं। हालांकि, आप प्रत्येक पेज के लिए DPI या इमेज क्वालिटी को नियंत्रित करना चाह सकते हैं:

```csharp
// Optional: tweak image processing settings before OCR
ocrEngine.ImageProcessingOptions.Dpi = 300; // higher DPI improves accuracy
ocrEngine.ImageProcessingOptions.Compression = ImageCompression.Jpeg;
```

इन विकल्पों को सेट करने के बाद, प्रत्येक फ्रेम के लिए **Step 2** दोहराएँ, या बस `ImageStream.FromFile` को मल्टी‑पेज TIFF की ओर इंगित करें और Aspose को बाकी काम करने दें।  

## सामान्य समस्याएँ और उनके समाधान

| लक्षण | संभावित कारण | समाधान |
|---------|--------------|-----|
| टेक्स्ट गड़बड़ या गायब है | गलत भाषा सेट की गई | सही भाषा पैक सेट करें (उदाहरण के लिए `Language.German`)। |
| PDF बहुत बड़ा है (एक पेज स्कैन के लिए 10 MB) | डिफ़ॉल्ट इमेज कॉम्प्रेशन कम है | `ocrEngine.ImageProcessingOptions.Compression` को `Jpeg` सेट करें और एक उचित `Quality` मान (0‑100) निर्धारित करें। |
| OCR बहुत धीरे चलता है | `Auto` डिफ़ॉल्ट भाषा डिटेक्शन का उपयोग करना | स्पष्ट रूप से अपेक्षित भाषा सेट करें। |
| कोई सर्चेबल लेयर नहीं दिखती | `SaveFormat.Pdf` के साथ सेव किया गया, `PdfSearchable` के बजाय | `PdfSearchable` का उपयोग करें। |

## पूर्ण एंड‑टू‑एंड उदाहरण

सब कुछ मिलाकर, यहाँ एक तैयार‑चलाने योग्य कंसोल ऐप है जिसे आप Visual Studio में कॉपी‑पेस्ट कर सकते हैं:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.Latin,
                // Optional: improve accuracy for low‑resolution scans
                ImageProcessingOptions = { Dpi = 300, Compression = ImageCompression.Jpeg }
            };

            // 2️⃣ Load the scanned image (convert scanned image)
            string inputPath = @"C:\Docs\contract_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Run OCR and extract text (extract text from image)
            RecognitionResult result = ocrEngine.Recognize();
            Console.WriteLine("First 200 characters of extracted text:");
            Console.WriteLine(result.Text.Substring(0, Math.Min(200, result.Text.Length)));

            // 4️⃣ Save as searchable PDF (create searchable pdf)
            string outputPath = @"C:\Docs\contract_searchable.pdf";
            ocrEngine.Save(outputPath, SaveFormat.PdfSearchable);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**आपको क्या दिखेगा:**  
* एक कंसोल विंडो जो OCR किए गए टेक्स्ट का एक स्निपेट प्रिंट करेगी।  
* एक `contract_searchable.pdf` फ़ाइल जो आपके मूल TIFF के बगल में होगी। इसे खोलें, **Ctrl + F** दबाएँ, और मूल स्कैन में मौजूद किसी भी शब्द को सर्च करें—वोilà, यह काम करता है।  

## अगले कदम और संबंधित विषय

* **How to OCR document** बैच – ऊपर दिया कोड को `foreach` लूप में रखें और पूरी फ़ोल्डर प्रोसेस करें।  
* **Convert scanned image** फ़ॉर्मैट्स TIFF के अलावा (PNG, JPEG) – वही API काम करता है; बस फ़ाइल एक्सटेंशन बदलें।  
* **Extract text from image** आगे के विश्लेषण के लिए – `result.Text` को नेचुरल‑लैंग्वेज‑प्रोसेसिंग पाइपलाइन में फीड करें।  
* **Optimize PDF size** – `PdfSaveOptions` को एक्सप्लोर करें ताकि इमेज को और कॉम्प्रेस किया जा सके या फ़ॉन्ट्स को केवल ज़रूरत पड़ने पर एम्बेड किया जाए।  

इन विचारों के साथ प्रयोग करें, और आप जल्दी ही किसी भी “इस स्कैन को सर्चेबल PDF में बदलें” अनुरोध के लिए जाने‑माने व्यक्ति बन जाएंगे।  

---

### TL;DR

अब आप जानते हैं कि Aspose OCR in C# का उपयोग करके स्कैन की गई इमेज से **searchable PDF** फ़ाइलें कैसे बनाते हैं। प्रक्रिया है: इंजन को इनिशियलाइज़ करें, इमेज लोड करें, OCR चलाएँ, और `PdfSearchable` के साथ सेव करें। भाषा सेटिंग्स, DPI, और कॉम्प्रेशन को एडजस्ट करके एज केस को हैंडल करें, और आप **convert scanned image**, **extract text from image**, और यहाँ तक कि **convert TIFF to PDF** बड़े पैमाने पर करने के लिए तैयार हैं। कोडिंग का आनंद लें!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}