---
category: general
date: 2026-09-13
description: Aspose OCR का उपयोग करके C# में स्कैन किए गए पृष्ठ को PDF में बदलना सीखें।
  यह गाइड प्रीप्रोसेसिंग, कोरियन टेक्स्ट पहचान, और सर्चेबल PDF बनाने को दर्शाता है।
keywords:
- scanned page to pdf
- preprocess image for OCR
- generate pdf with text
- convert image to searchable pdf
- gpu accelerated OCR
- recognize Korean text image
lastmod: 2026-09-13
og_description: Aspose OCR के साथ C# में स्कैन किए गए पृष्ठ को PDF में बदलना सीखें।
  यह ट्यूटोरियल इमेज प्रीप्रोसेसिंग, कोरियन टेक्स्ट के लिए GPU‑accelerated OCR, और
  मिनटों में सर्चेबल PDF जनरेट करने को कवर करता है।
og_image_alt: Screenshot of C# console app converting a scanned Korean page to searchable
  PDF using Aspose OCR
og_title: C# में OCR के साथ स्कैन किए गए पृष्ठ को PDF में कैसे बदलें
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  headline: How to turn a scanned page to PDF in C# with OCR
  type: TechArticle
- description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  name: How to turn a scanned page to PDF in C# with OCR
  steps:
  - name: Initialise the OCR engine with GPU support.
    text: Initialise the OCR engine with GPU support.
  - name: Add **preprocess image for OCR** filters such as deskew and denoise.
    text: Add **preprocess image for OCR** filters such as deskew and denoise.
  - name: Download and load the Korean language model (handled automatically).
    text: Download and load the Korean language model (handled automatically).
  - name: Run the OCR on the image.
    text: Run the OCR on the image.
  - name: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
    text: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
  - name: (Optional) Serialize the OCR output to JSON for downstream pipelines.
    text: (Optional) Serialize the OCR output to JSON for downstream pipelines.
  - name: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
    text: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
  - name: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
    text: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
  - name: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
    text: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
  type: HowTo
- questions:
  - answer: 'The exporter embeds the original bitmap at its native resolution. If
      size is a concern, downscale the image *before* recognition:'
    question: My PDF is huge compared to the original image.
  - answer: Verify that the image path is correct and that the file is not corrupted.
      Also, make sure the GPU driver is up‑to‑date; older drivers can cause silent
      failures.
    question: The OCR returns empty strings.
  - answer: Absolutely. Wrap steps 4‑6 in a `foreach (var file in Directory.GetFiles("Resources",
      "*.jpg"))` loop and change the output PDF path accordingly.
    question: Can I process multiple pages in a loop?
  type: FAQPage
tags:
- scanned page to pdf
- OCR
- Aspose
- C#
title: C# में OCR के साथ स्कैन किए गए पृष्ठ को PDF में कैसे बदलें
url: /hi/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# स्कैन किए गए पृष्ठ को C# में OCR के साथ PDF में कैसे बदलें

यदि आपको **स्कैन किए गए पृष्ठ को PDF** में बदलते समय टेक्स्ट को खोज योग्य रखना है, तो आप सही जगह पर हैं। यह ट्यूटोरियल Aspose OCR का उपयोग करके **preprocess image for OCR**, **recognize Korean text image**, और अंत में **create searchable PDF image** करने की प्रक्रिया को दिखाता है – सभी एक साधारण C# कंसोल एप्लिकेशन से।

## त्वरित उत्तर
- **OCR को संभालने वाली लाइब्रेरी कौन सी है?** Aspose.OCR for .NET  
- **क्या मैं GPU का उपयोग कर सकता हूँ?** हाँ – तेज़ प्रोसेसिंग के लिए GPU एक्सेलेरेशन सक्षम करें, जिससे गति 2× तक बढ़ सकती है  
- **क्या मुझे कोरियन भाषा पैक चाहिए?** यह पहली बार उपयोग पर स्वचालित रूप से डाउनलोड हो जाता है  
- **क्या आउटपुट खोज योग्य होगा?** उत्पन्न PDF में एक अदृश्य टेक्स्ट लेयर होता है  
- **कौन से .NET संस्करण समर्थित हैं?** .NET 6.0 और बाद के (जिसमें .NET Core और .NET Framework शामिल हैं)

## आवश्यकताएँ

- **.NET 6.0 या बाद का** – .NET Core, .NET Framework, और .NET 5/6+ पर काम करता है  
- **Aspose.OCR for .NET** NuGet पैकेज (`Aspose.OCR`) – ट्रायल कुंजियाँ Aspose साइट पर मुफ्त हैं  
- कोरियन अक्षरों वाली एक नमूना छवि, उदाहरण के लिए `korean_book_page.jpg`  
- आपका पसंदीदा IDE (Visual Studio 2022, VS Code, Rider, आदि)

> **Pro tip:** छवियों को `Resources/` फ़ोल्डर में रखें ताकि पाथ विभिन्न मशीनों में सुसंगत रहें।

## प्रक्रिया का अवलोकन

1. GPU समर्थन के साथ OCR इंजन को प्रारंभ करें।  
2. **preprocess image for OCR** फ़िल्टर जैसे deskew और denoise जोड़ें।  
3. कोरियन भाषा मॉडल डाउनलोड और लोड करें (स्वचालित रूप से संभाला जाता है)।  
4. छवि पर OCR चलाएँ।  
5. परिणाम को **SearchablePdfExporter** के साथ निर्यात करें ताकि **create searchable PDF image** बन सके।  
6. (वैकल्पिक) OCR आउटपुट को JSON में सीरियलाइज़ करें ताकि डाउनस्ट्रीम पाइपलाइन में उपयोग हो सके।

नीचे हम प्रत्येक चरण का विस्तार से वर्णन करेंगे, यह बताएँगे कि *क्यों* यह महत्वपूर्ण है, और आपको वह सटीक कोड देंगे जिसे आप कॉपी‑पेस्ट कर सकते हैं।

## स्कैन किए गए पृष्ठ को PDF में बदलने की प्रक्रिया कैसे काम करती है?

`OcrEngine` Aspose.OCR में मुख्य क्लास है जो छवियों पर ऑप्टिकल कैरेक्टर रिकग्निशन करता है।  
`SearchablePdfExporter` एक PDF बनाता है जिसमें मूल छवि और खोज के लिए एक अदृश्य टेक्स्ट लेयर होता है।  
`RecognitionResult` OCR इंजन द्वारा लौटाए गए टेक्स्ट और कॉन्फिडेंस डेटा को रखता है।

अपनी छवि को `new OcrEngine()` से लोड करें और `engine.Recognize("korean_book_page.jpg")` को कॉल करें, फिर `RecognitionResult` को `SearchablePdfExporter.Export` में पास करें। यह दो‑चरणीय प्रक्रिया बिटमैप पढ़ती है, यूनिकोड टेक्स्ट निकालती है, और दोनों को एक ही PDF में एम्बेड करती है जहाँ टेक्स्ट लेयर अदृश्य लेकिन खोज योग्य होती है। GPU एक्सेलेरेशन पहचान समय को लगभग आधा कर देता है, जबकि deskew और denoise फ़िल्टर शोरयुक्त स्कैन पर सटीकता को 15 % तक बढ़ाते हैं।

## इमेज को PDF में बदलें – पूर्ण कार्यप्रवाह

निम्नलिखित स्निपेट *पूर्ण* प्रोग्राम है। एक नया कंसोल प्रोजेक्ट बनाएं (`dotnet new console -n OcrPdfDemo`) और ऑटो‑जेनरेटेड `Program.cs` को प्लेसहोल्डर में दिखाए गए कोड से बदलें।

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### यह क्यों काम करता है

- **GPU एक्सेलेरेशन** CPU‑केवल मोड की तुलना में पहचान समय को लगभग आधा कर देता है।  
- **Deskew** और **Denoise** क्लासिक *preprocess image for OCR* तकनीकें हैं; ये सामान्य स्कैनिंग दोषों को सुधारते हैं जो अन्यथा इंजन को अक्षर मिस करने का कारण बनते हैं।  
- **Language model loading** **recognize Korean text image** के लिए आवश्यक है – कोरियन मॉडल के बिना इंजन सामान्य लैटिन अल्फाबेट पर लौट आएगा और बकवास आउटपुट देगा।  
- **SearchablePdfExporter** मूल बिटमैप और एक अदृश्य टेक्स्ट ओवरले को बंडल करता है, जिससे आपको **create searchable pdf image** परिणाम मिलता है जिसे आप किसी भी PDF व्यूअर में इंडेक्स कर सकते हैं।

## यह क्यों काम करता है

- **GPU एक्सेलेरेशन** CPU‑केवल मोड की तुलना में पहचान समय को लगभग आधा कर देता है।  
- **Deskew** और **Denoise** क्लासिक *preprocess image for OCR* तकनीकें हैं; ये सामान्य स्कैनिंग दोषों को सुधारते हैं जो अन्यथा इंजन को अक्षर मिस करने का कारण बनते हैं।  
- **Language model loading** **recognize Korean text image** के लिए आवश्यक है – कोरियन मॉडल के बिना इंजन सामान्य लैटिन अल्फाबेट पर लौट आएगा और बकवास आउटपुट देगा।  
- **SearchablePdfExporter** मूल बिटमैप और एक अदृश्य टेक्स्ट ओवरले को बंडल करता है, जिससे आपको **create searchable pdf image** परिणाम मिलता है जिसे आप किसी भी PDF व्यूअर में इंडेक्स कर सकते हैं।

## OCR के लिए इमेज प्रीप्रोसेस – टिप्स और ट्रिक्स

`DeskewFilter` स्कैन किए गए पृष्ठों की घूर्णन को सुधारता है।  
`ContrastFilter` OCR सटीकता सुधारने के लिए इमेज कंट्रास्ट को समायोजित करता है।  
`BinarizationFilter` थ्रेशोल्ड के आधार पर इमेज को ब्लैक‑एंड‑व्हाइट में बदलता है, जिससे बैकग्राउंड शोर कम होता है।  
`OrientationFilter` मिश्रित पोर्ट्रेट/लैंडस्केप पृष्ठों का पता लगाता और सुधारता है।  

| समस्या | अतिरिक्त फ़िल्टर | कैसे जोड़ें |
|-------|-------------------|------------|
| कम कंट्रास्ट | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| भारी बैकग्राउंड शोर | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| मिश्रित अभिविन्यास (पोर्ट्रेट और लैंडस्केप) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Note:** बहुत अधिक फ़िल्टर जोड़ने से प्रोसेसिंग धीमी हो सकती है। स्केल अप करने से पहले प्रत्येक परिवर्तन को एक पृष्ठ पर परीक्षण करें।

## कोरियन टेक्स्ट इमेज को पहचानें – सामान्य समस्याएँ

कोरियन लिपियों में हंगुल अक्षर होते हैं जो दृश्य रूप से घने होते हैं। यदि आप गड़बड़ आउटपुट देखते हैं:

1. **सुनिश्चित करें कि भाषा मॉडल पूरी तरह से डाउनलोड हो गया है** – कंसोल में “Downloading Korean model…” जैसा संदेश देखें।  
2. यदि आपके स्कैन 12° से अधिक घुमा हुए हैं तो `DeskewFilter` में `MaxAngle` बढ़ाएँ।  
3. `ocrEngine.GpuMemoryLimit = 2048;` सेट करके GPU मेमोरी बढ़ाएँ (मान MB में)।  

`LanguageModel.Korean` OCR के लिए कोरियन भाषा डेटा लोड करता है, जिससे सटीक हंगुल पहचान संभव होती है।  

ये समायोजन सीधे **recognize Korean text image** की सफलता को प्रभावित करते हैं।

## खोज योग्य PDF इमेज बनाएं – परिणाम की पुष्टि

प्रोग्राम समाप्त होने के बाद, `korean_page.pdf` को किसी भी PDF रीडर (Adobe Acrobat Reader, Foxit, यहाँ तक कि Chrome) में खोलें। आपको सक्षम होना चाहिए:

- **टेक्स्ट चुनें** अपने माउस से जैसे यह एक मूल PDF हो।  
- **खोजें** कोरियन शब्दों को बिल्ट‑इन सर्च बॉक्स का उपयोग करके।  

यदि टेक्स्ट लेयर खाली दिखे, तो दोबारा जांचें कि `Export` मेथड को सही इमेज पाथ मिला है और OCR परिणाम में `RecognitionResult.Text` खाली नहीं है।

## पूर्ण JSON आउटपुट – क्या अपेक्षित है

कंसोल एक सुगठित JSON पेलोड प्रिंट करता है। एक संक्षिप्त उदाहरण इस प्रकार दिखता है:

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

## समस्या निवारण और अक्सर पूछे जाने वाले प्रश्न

**Q: मेरा PDF मूल इमेज की तुलना में बहुत बड़ा है।**  
A: एक्सपोर्टर मूल बिटमैप को उसकी मूल रेज़ोल्यूशन पर एम्बेड करता है। यदि आकार समस्या है, तो पहचान से *पहले* इमेज को डाउनस्केल करें:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: OCR खाली स्ट्रिंग्स लौटाता है।**  
A: जांचें कि इमेज पाथ सही है और फ़ाइल भ्रष्ट नहीं है। साथ ही, सुनिश्चित करें कि GPU ड्राइवर अपडेटेड है; पुराने ड्राइवर साइलेंट फेल्योर का कारण बन सकते हैं।

**Q: क्या मैं लूप में कई पृष्ठों को प्रोसेस कर सकता हूँ?**  
A: बिल्कुल। चरण 4‑6 को `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` लूप में रखें और आउटपुट PDF पाथ को उसी अनुसार बदलें।

## निष्कर्ष

हमने अभी **इमेज को PDF में बदला** और खोज योग्य टेक्स्ट को संरक्षित किया, यह सब Aspose OCR की शक्तिशाली पाइपलाइन के कारण संभव हुआ। **preprocess image for OCR** करके आप सटीकता बढ़ाते हैं; **recognize Korean text image** करके आप जटिल लिपियों को संभालते हैं; और **create searchable pdf image** करके आपको एक पोर्टेबल, इंडेक्सेबल दस्तावेज़ मिलता है।

कोड को प्राप्त करें, इसे अपनी स्कैन पर लागू करें, और अतिरिक्त फ़िल्टर या भाषा मॉडल के साथ प्रयोग करें। वही पैटर्न चीनी, जापानी, या किसी भी लैटिन‑आधारित भाषा के लिए काम करता है—सिर्फ `LanguageModel.Korean` को उपयुक्त enum से बदलें।

और प्रश्न हैं? टिप्पणी छोड़ें, और कोडिंग का आनंद लें!

---

**अंतिम अपडेट:** 2026-09-13  
**परीक्षित संस्करण:** Aspose.OCR 24.11 for .NET  
**लेखक:** Aspose

## संबंधित ट्यूटोरियल

- [Aspose Ocr का उपयोग करके स्कैन फ़ाइलों से खोज योग्य PDF बनाएं](/ocr/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/)
- [OCR प्रीप्रोसेसिंग पाइपलाइन – इमेज से टेक्स्ट कैसे पहचानें](/ocr/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)
- [Aspose Ocr के साथ इमेज से टेक्स्ट पहचानें – पूर्ण C गाइड](/ocr/net/ocr-configuration/recognize-text-from-image-with-aspose-ocr-complete-c-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}