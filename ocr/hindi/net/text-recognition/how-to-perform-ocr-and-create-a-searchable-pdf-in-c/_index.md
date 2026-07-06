---
category: general
date: 2026-02-14
description: सीखें कि कैसे TIFF या इमेज पर OCR करें और OCR का उपयोग करके PDF को सर्चेबल
  PDF में बदलें—स्टेप‑बाय‑स्टेप C# गाइड।
draft: false
keywords:
- how to perform OCR
- convert pdf using OCR
- make searchable pdf
- tiff to searchable pdf
- searchable pdf from image
language: hi
og_description: जाने कैसे इमेज पर OCR करें, OCR का उपयोग करके PDF को कनवर्ट करें,
  और Aspose OCR के साथ एक सर्चेबल PDF बनाएं, एक संक्षिप्त C# ट्यूटोरियल में।
og_title: C# में OCR कैसे करें और खोज योग्य PDF बनाएं
tags:
- OCR
- C#
- Aspose
- PDF conversion
title: C# में OCR कैसे करें और खोज योग्य PDF बनाएं
url: /hi/net/text-recognition/how-to-perform-ocr-and-create-a-searchable-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में OCR कैसे करें और सर्चेबल PDF बनाएं

क्या आपको कभी स्कैन किए गए दस्तावेज़ पर **perform OCR** करने की ज़रूरत पड़ी है लेकिन यह नहीं पता था कि परिणाम को सर्चेबल PDF में कैसे बदला जाए? आप अकेले नहीं हैं—कई डेवलपर्स को लेगेसी TIFF आर्काइव या केवल‑इमेज PDFs से निपटते समय यही समस्या आती है। अच्छी खबर? कुछ ही पंक्तियों के C# कोड और Aspose.OCR लाइब्रेरी के साथ, आप एक TIFF या किसी भी इमेज को कुछ सेकंड में पूरी तरह सर्चेबल PDF में बदल सकते हैं।

इस ट्यूटोरियल में हम वह सब कुछ कवर करेंगे जो आपको जानना आवश्यक है: लाइब्रेरी को इंस्टॉल करने से लेकर, मल्टी‑पेज TIFF लोड करने, और `RecognizeToPdf` को कॉल करने तक, ताकि आप **convert PDF using OCR** और **make searchable PDF** फ़ाइलें बना सकें जिन्हें आपके उपयोगकर्ता वास्तव में सर्च कर सकें। अंत तक, आपके पास एक तैयार‑चलाने‑योग्य कंसोल ऐप होगा जो इमेज स्रोत से सर्चेबल PDF उत्पन्न करता है।

## आवश्यकताएँ

- **.NET 6.0** या बाद का संस्करण (कोड .NET Framework 4.7+ पर भी काम करता है)।
- एक वैध **Aspose.OCR** लाइसेंस या अस्थायी इवैल्यूएशन की (फ़्री ट्रायल परीक्षण के लिए पर्याप्त है)।
- Visual Studio 2022 (या कोई भी एडिटर जो आप पसंद करते हैं) के साथ **NuGet** पैकेज मैनेजर।
- `input.tif` नाम की इनपुट फ़ाइल को उस फ़ोल्डर में रखें जिसे आप नियंत्रित करते हैं—मल्टी‑पेज TIFFs तुरंत काम करेंगे।

> **Pro tip:** यदि आप Windows पर हैं, तो TIFF को संकलित `.exe` के समान फ़ोल्डर में कॉपी करें ताकि पाथ‑से जुड़ी समस्याओं से बचा जा सके।

## चरण 1: Aspose.OCR NuGet पैकेज इंस्टॉल करें

टर्मिनल में अपने प्रोजेक्ट फ़ोल्डर को खोलें और चलाएँ:

```bash
dotnet add package Aspose.OCR
```

## चरण 2: एक न्यूनतम कंसोल एप्लिकेशन बनाएं

यदि आपके पास अभी तक नहीं है तो एक नया कंसोल प्रोजेक्ट बनाएं:

```bash
dotnet new console -n OcrSearchablePdfDemo
cd OcrSearchablePdfDemo
```

ऑटो‑जनरेटेड `Program.cs` को **Step 3** में दिखाए गए पूर्ण कोड से बदलें। प्रोग्राम करेगा:

1. OCR इंजन को इंस्टैंशिएट करेगा।
2. स्रोत इमेज (या मल्टी‑पेज TIFF) लोड करेगा।
3. OCR चलाएगा और आउटपुट को सीधे सर्चेबल PDF में लिखेगा।
4. उपयोगकर्ता को प्रक्रिया सफल होने की सूचना देगा।

## चरण 3: पूर्ण कार्यशील कोड – इमेज से सर्चेबल PDF तक

नीचे **पूरा** स्रोत फ़ाइल दिया गया है। इसे `Program.cs` में कॉपी‑पेस्ट करें। टिप्पणियों में उन गैर‑स्पष्ट भागों की व्याख्या की गई है।

```csharp
using System;
using Aspose.OCR;          // Core OCR namespace
using Aspose.OCR.Image;   // Provides ImageStream helpers

namespace OcrSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialise the OCR engine.
            // -------------------------------------------------
            // The Engine class is the entry point for all OCR operations.
            // You can optionally pass a license object here if you have one.
            var ocrEngine = new Engine();

            // -------------------------------------------------
            // 2️⃣ Load the source image.
            // -------------------------------------------------
            // ImageStream.FromFile supports TIFF, PDF, JPEG, PNG, etc.
            // For multi‑page TIFFs the stream automatically contains all pages.
            string inputPath = "YOUR_DIRECTORY/input.tif";
            var imageStream = ImageStream.FromFile(inputPath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR and write a searchable PDF.
            // -------------------------------------------------
            // RecognizeToPdf does the heavy lifting:
            // • It runs the OCR engine on every page.
            // • It embeds the extracted text as an invisible layer.
            // • The visual appearance of the original image is preserved.
            string outputPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.RecognizeToPdf(imageStream, outputPath);

            // -------------------------------------------------
            // 4️⃣ Inform the user.
            // -------------------------------------------------
            Console.WriteLine("Searchable PDF created at: " + outputPath);
        }
    }
}
```

**आपको क्या दिखेगा:** प्रोग्राम चलाने के बाद, लक्ष्य फ़ोल्डर में `searchable.pdf` नाम की फ़ाइल बनती है। इसे Adobe Reader या किसी भी PDF व्यूअर में खोलें और मूल TIFF में मौजूद किसी शब्द को खोजने की कोशिश करें। टेक्स्ट तुरंत मिलना चाहिए, जिससे यह साबित होता है कि आपने इमेज से सफलतापूर्वक **made searchable PDF** किया है।

### एप्लिकेशन चलाना

```bash
dotnet run
```

यदि सब कुछ सही तरीके से सेट है तो आपको मिलेगा:

```
Searchable PDF created at: YOUR_DIRECTORY/searchable.pdf
```

PDF खोलें, `Ctrl+F` दबाएँ, स्रोत से कोई शब्द टाइप करें, और देखें कि हाइलाइट सही स्थान पर कूदता है।

## चरण 4: सामान्य विविधताएँ और किनारे के मामले

### नियमित PDF (केवल‑इमेज) को सर्चेबल PDF में बदलना

यदि आपका स्रोत PDF स्कैन की गई इमेजेज़ रखता है न कि टेक्स्ट, तो आप वही विधि उपयोग कर सकते हैं—सिर्फ `ImageStream` स्रोत को बदलें:

```csharp
var pdfStream = ImageStream.FromFile("YOUR_DIRECTORY/input.pdf");
ocrEngine.RecognizeToPdf(pdfStream, "YOUR_DIRECTORY/searchable_from_pdf.pdf");
```

यह **convert pdf using OCR** परिदृश्य को अतिरिक्त कोड के बिना पूरा करता है।

### बड़े मल्टी‑पेज दस्तावेज़ों को संभालना

कुछ सौ पृष्ठों से अधिक वाले दस्तावेज़ों के लिए, विचार करें:

- **मेमोरी लिमिट बढ़ाना** (`Engine.MemoryLimit = 2_000; // MB`)।
- **चंक्स में प्रोसेस करना**: पृष्ठों का एक उपसमुच्चय लोड करें, मध्यवर्ती PDFs लिखें, फिर उन्हें PDF लाइब्रेरी (जैसे Aspose.PDF) से मर्ज करें।

### अंग्रेज़ी के अलावा अन्य भाषाओं को संभालना

Aspose.OCR बॉक्स से बाहर कई भाषाओं को सपोर्ट करता है। पहचान से पहले भाषा सेट करें:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

यदि आपको गैर‑लैटिन स्क्रिप्ट में **tiff to searchable pdf** चाहिए, तो सुनिश्चित करें कि उपयुक्त भाषा पैक इंस्टॉल हो।

### यदि आउटपुट PDF खाली है तो क्या करें?

- जाँचें कि इनपुट फ़ाइल भ्रष्ट नहीं है।
- सुनिश्चित करें कि OCR इंजन के पास वैध लाइसेंस है—इवैल्यूएशन मोड पेज लिमिट लगा सकता है।
- जांचें कि इमेज रेज़ोल्यूशन कम से कम 300 dpi है; कम रेज़ोल्यूशन से पहचान खराब हो सकती है।

## चरण 5: परिणाम को प्रोग्रामेटिकली सत्यापित करना (वैकल्पिक)

कभी‑कभी आप यह पुष्टि करना चाहते हैं कि PDF में वास्तव में टेक्स्ट लेयर है। आप Aspose.PDF का उपयोग करके टेक्स्ट निकाल सकते हैं:

```csharp
using Aspose.Pdf;

var pdfDoc = new Document("YOUR_DIRECTORY/searchable.pdf");
string extracted = pdfDoc.Pages[1].ExtractText();
Console.WriteLine("First page text snippet: " + extracted.Substring(0, 100));
```

यदि `extracted` खाली नहीं है, तो आपने सफलतापूर्वक **made searchable pdf** किया है।

## निष्कर्ष

हमने **how to perform OCR** को TIFF (या किसी भी इमेज) पर कवर किया और सहजता से **convert PDF using OCR** करके एक **searchable PDF** बनाया जो मूल दस्तावेज़ की तरह व्यवहार करता है। मुख्य कदम हैं:

1. Aspose.OCR इंस्टॉल करें।  
2. `Engine` को इनिशियलाइज़ करें।  
3. `ImageStream` के माध्यम से इमेज लोड करें।  
4. `RecognizeToPdf` को कॉल करें।  

इसके बाद आप भाषा सेटिंग्स, बड़े बैच प्रोसेसिंग के साथ प्रयोग कर सकते हैं, या आउटपुट को अन्य PDF मैनिपुलेशन कार्यों के साथ संयोजित कर सकते हैं। वही पैटर्न **tiff to searchable pdf**, **searchable pdf from image**, और स्कैन किए गए PDFs पर भी काम करता है।

अगली चुनौती के लिए तैयार हैं? OCR को वेब API में एम्बेड करने की कोशिश करें ताकि उपयोगकर्ता स्कैन अपलोड कर सकें और तुरंत सर्चेबल PDFs प्राप्त कर सकें, या `OcrEngine` की उन्नत सेटिंग्स का उपयोग करके हस्तलिखित नोट्स पर OCR का अन्वेषण करें। संभावनाएँ असीमित हैं—कोडिंग का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}