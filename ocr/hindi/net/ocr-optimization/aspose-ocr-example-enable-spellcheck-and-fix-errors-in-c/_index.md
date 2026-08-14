---
category: general
date: 2026-03-07
description: Aspose OCR उदाहरण जो दिखाता है कि स्पेलचेक कैसे सक्षम करें, कस्टम शब्दकोश
  जोड़ें, इमेज OCR लोड करें और OCR त्रुटियों को जल्दी ठीक करें।
draft: false
keywords:
- aspose ocr example
- how to enable spellcheck
- how to add dictionary
- load image ocr
- how to fix ocr errors
language: hi
og_description: Aspose OCR उदाहरण जो आपको वर्तनी जाँच सक्षम करने, एक कस्टम शब्दकोश
  जोड़ने, OCR के लिए छवि लोड करने और सामान्य OCR त्रुटियों को ठीक करने के चरणों से
  परिचित कराता है।
og_title: Aspose OCR उदाहरण – वर्तनी जाँच सक्षम करें और त्रुटियों को ठीक करें
tags:
- Aspose
- OCR
- C#
- SpellCheck
title: Aspose OCR उदाहरण – C# में स्पेलचेक सक्षम करें और त्रुटियों को ठीक करें
url: /hi/net/ocr-optimization/aspose-ocr-example-enable-spellcheck-and-fix-errors-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR उदाहरण – स्पेलचेक सक्षम करें और C# में त्रुटियों को ठीक करें

क्या आपको कभी ऐसा **Aspose OCR example** चाहिए था जो केवल छवि से टेक्स्ट पढ़ता ही नहीं, बल्कि उन परेशान करने वाले वर्तनी त्रुटियों को भी साफ़ करता हो? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स में कच्चा OCR आउटपुट टाइपो से भरा होता है, विशेषकर जब स्रोत छवि में कम कंट्रास्ट वाले फ़ॉन्ट या हाथ से लिखे नोट्स हों।  

अच्छी खबर? Aspose.OCR के साथ आप **spellcheck सक्षम कर** सकते हैं, अपना शब्दकोश जोड़ सकते हैं, और कुछ ही कोड लाइनों में एक परिष्कृत स्ट्रिंग प्राप्त कर सकते हैं। नीचे आप बिल्कुल देखेंगे **spellcheck कैसे सक्षम करें**, **शब्दकोश कैसे जोड़ें**, और **छवि OCR कैसे लोड करें** ताकि आप अंततः **OCR त्रुटियों को ठीक** कर सकें बिना सिर दर्द के।  

इस ट्यूटोरियल में हम सब कुछ कवर करेंगे—NuGet इंस्टॉलेशन से लेकर एक पूर्ण, चलाने योग्य प्रोग्राम जो सुधरा हुआ टेक्स्ट प्रिंट करता है। अंत तक आपके पास एक ठोस **Aspose OCR example** होगा जिसे आप सीधे किसी भी .NET प्रोजेक्ट में डाल सकते हैं।

## आवश्यकताएँ

- .NET 6.0 SDK या बाद वाला (कोड .NET Core और .NET Framework के साथ भी काम करता है)
- Visual Studio 2022 या कोई भी C#‑compatible IDE
- `typed_text.png` नामक इमेज फ़ाइल जिसमें स्पष्ट, टाइप किया गया अंग्रेज़ी टेक्स्ट हो
- Aspose.OCR NuGet पैकेज को प्राप्त करने के लिए इंटरनेट एक्सेस

कोई अन्य थर्ड‑पार्टी लाइब्रेरी आवश्यक नहीं है.

---

## चरण 1 – Aspose.OCR NuGet पैकेज इंस्टॉल करें (Load Image OCR)

कोड लिखने से पहले, हमें उस लाइब्रेरी की आवश्यकता है जो OCR इंजन को शक्ति देती है।

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** यदि आप Visual Studio का उपयोग कर रहे हैं, तो प्रोजेक्ट पर राइट‑क्लिक करें → *Manage NuGet Packages* → **Aspose.OCR** खोजें और *Install* पर क्लिक करें।  

पैकेज को इंस्टॉल करने से आपको `OcrEngine`, `ImageStream`, और बिल्ट‑इन spell‑checking यूटिलिटीज़ तक पहुंच मिलती है जिन्हें हम बाद में उपयोग करेंगे। पैकेज स्थापित होने के बाद, आप **load image OCR** करने के लिए तैयार हैं।

## चरण 2 – OCR इंजन इंस्टेंस बनाएं

इंजन बनाना किसी भी **Aspose OCR example** में पहला ठोस कदम है। `OcrEngine` को उस मस्तिष्क की तरह समझें जो बिटमैप का विश्लेषण करेगा और टेक्स्ट निकालेगा।

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Step 2: Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

`OcrEngine` कन्स्ट्रक्टर को किसी भी पैरामीटर की आवश्यकता नहीं होती, जिससे यह त्वरित प्रोटोटाइप के लिए साफ़ और सरल बन जाता है।

## चरण 3 – Spellcheck कैसे सक्षम करें (और यह क्यों महत्वपूर्ण है)

कच्चा OCR आउटपुट अक्सर “teh” जैसी गलत पहचानी गई शब्दों को शामिल करता है, जहाँ सही शब्द “the” होना चाहिए। बिल्ट‑इन spell‑checker को सक्षम करने से Aspose स्वचालित रूप से उन त्रुटियों को सबसे संभावित सही वर्तनी से बदल देता है।

```csharp
// Step 3: Turn on spell checking and set the language to English
ocrEngine.Settings.SpellCheck.Enabled = true;
ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;
```

> **Spellcheck क्यों सक्षम करें?**  
> - **सटीकता:** पोस्ट‑प्रोसेसिंग spell check प्रिंटेड दस्तावेज़ों के लिए कुल टेक्स्ट सटीकता को 10‑15 % तक बढ़ा सकता है।  
> - **उपयोगकर्ता अनुभव:** साफ़ टेक्स्ट का मतलब है कम डाउनस्ट्रीम सफ़ाई जब आप परिणाम को सर्च इंडेक्स या एनालिटिक्स पाइपलाइन में फीड करते हैं।

## चरण 4 – शब्दकोश कैसे जोड़ें (कस्टम शब्द)

कभी‑कभी डिफ़ॉल्ट शब्दकोश आपके ब्रांड नाम, प्रोडक्ट कोड, या डोमेन‑स्पेसिफिक जार्गन को नहीं जानता। यही वह जगह है जहाँ **how to add dictionary** काम आता है।

```csharp
// Step 4: Add custom words that the spell checker should accept
ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
{
    "AsposeOCR",   // our library name
    "OCRify",      // a fictional product
    "CSharpify"    // another custom term
});
```

आप एक एरे, लिस्ट, या यहाँ तक कि फ़ाइल से भी पढ़ सकते हैं यदि आपके पास बड़ा कस्टम शब्दावली है। अब spell‑checker उन एंट्रीज़ को वैध मान लेगा, जिससे गलत सुधारों से बचा जा सकेगा।

## चरण 5 – OCR के लिए इमेज लोड करें (Load Image OCR)

अब जब इंजन कॉन्फ़िगर हो गया है, हमें उसे उस चित्र की ओर इंगित करना है जिसे हम पढ़ना चाहते हैं। `ImageStream.FromFile` हेल्पर फ़ाइल‑रीडिंग विवरणों को एब्स्ट्रैक्ट करता है।

```csharp
// Step 5: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");
```

> **Tip:** यदि आपकी इमेज प्रोजेक्ट की सब‑फ़ोल्डर में स्थित है, तो उसकी *Copy to Output Directory* प्रॉपर्टी को *Copy always* पर सेट करें ताकि रनटाइम पर पाथ सही ढंग से रिजॉल्व हो।

## चरण 6 – पहचान चलाएँ और OCR त्रुटियों को ठीक करें

सब कुछ सेट होने पर, `Recognize()` को एक बार कॉल करने से OCR पाइपलाइन चलती है, spell‑checking लागू होती है, और साफ़ परिणाम `ocrEngine.Text` में संग्रहीत हो जाता है।

```csharp
// Step 6: Run OCR and let the spell checker clean the output
ocrEngine.Recognize();

// Step 7: Output the corrected text to the console
Console.WriteLine("Corrected text:");
Console.WriteLine(ocrEngine.Text);
```

### अपेक्षित आउटपुट

मान लीजिए `typed_text.png` में वाक्य `The quick brown fox jumps over teh lazy dog` है, तो कंसोल में यह प्रदर्शित होगा:

```
Corrected text:
The quick brown fox jumps over the lazy dog
```

ध्यान दें कि “teh” को स्वचालित रूप से “the” में सुधारा गया। यदि आपने “OCRify” को कस्टम शब्दकोश में जोड़ा होता और इमेज में वह शब्द होता, तो इंजन उसे बिना बदले रखता।

---

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा प्रोग्राम है जिसे आप नए कंसोल प्रोजेक्ट में डाल सकते हैं। इसमें ऊपर बताए सभी चरण शामिल हैं, साथ ही स्पष्टता के लिए कुछ टिप्पणियाँ भी हैं।

```csharp
// ---------------------------------------------------------------
// Aspose OCR Example – Enable Spellcheck and Fix Errors
// ---------------------------------------------------------------

using System;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable spell checking (how to enable spellcheck)
            ocrEngine.Settings.SpellCheck.Enabled = true;
            ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;

            // 3️⃣ Add custom words (how to add dictionary)
            ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
            {
                "AsposeOCR",
                "OCRify",
                "CSharpify"
            });

            // 4️⃣ Load the image (load image OCR)
            // Replace the path with the actual location of your image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");

            // 5️⃣ Run OCR – this also fixes common OCR errors (how to fix ocr errors)
            ocrEngine.Recognize();

            // 6️⃣ Show the corrected result
            Console.WriteLine("Corrected text:");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

`Program.cs` के रूप में सहेजें, `dotnet run` चलाएँ, और आपको कंसोल में सुधरा हुआ वाक्य प्रिंट होता दिखेगा।

---

## अक्सर पूछे जाने वाले प्रश्न एवं किनारे के मामलों

| Question | Answer |
|----------|--------|
| **यदि इमेज एक मल्टी‑पेज PDF है तो क्या होगा?** | Aspose.OCR PDF पेजों को इमेज के रूप में संभाल सकता है। `ocrEngine.Image = ImageStream.FromPdf("file.pdf", pageNumber: 1);` का उपयोग करें और पेजों के माध्यम से लूप करें। |
| **क्या मैं भाषा को अंग्रेज़ी के अलावा किसी अन्य में बदल सकता हूँ?** | बिल्कुल। `ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.French;` सेट करें (या कोई भी समर्थित भाषा)। |
| **मेरा कस्टम शब्दकोश बहुत बड़ा है—क्या यह प्रदर्शन को प्रभावित करेगा?** | हजारों शब्द जोड़ने से प्रारंभिक थोड़ा खर्च होता है, लेकिन लुकअप O(1) है क्योंकि पीछे एक hash‑set उपयोग किया जाता है। बड़े शब्दावली के लिए, एप्लिकेशन स्टार्ट पर एक बार लोड करने पर विचार करें। |
| **यदि OCR इंजन भ्रष्ट इमेज पर अपवाद फेंके तो क्या करें?** | `Recognize()` को try‑catch ब्लॉक में रैप करें और `ocrEngine.LastError` की जाँच करें। आप `ocrEngine.Image.Width` और `Height` से इमेज के आयामों को पहले से वैलिडेट भी कर सकते हैं। |
| **क्या उत्पादन उपयोग के लिए लाइसेंस की आवश्यकता है?** | फ़्री इवैल्यूएशन परीक्षण के लिए काम करता है, लेकिन एक कमर्शियल लाइसेंस इवैल्यूएशन वॉटरमार्क को हटाता है और पूरी परफ़ॉर्मेंस अनलॉक करता है। |

## निष्कर्ष

अब आपके पास एक **complete Aspose OCR example** है जो **spellcheck कैसे सक्षम करें**, **शब्दकोश कैसे जोड़ें**, **image OCR कैसे लोड करें**, और **OCR त्रुटियों को कैसे ठीक करें** को साफ़, प्रोडक्शन‑रेडी तरीके से दर्शाता है। spell‑checker को कॉन्फ़िगर करके और कस्टम शब्द सूची प्रदान करके, आप निकाले गए टेक्स्ट की गुणवत्ता को बहुत बढ़ा सकते हैं बिना कोई पोस्ट‑प्रोसेसिंग लॉजिक लिखे।

अगले कदम के लिए तैयार हैं? भाषा को स्पेनिश में बदलें, मल्टी‑पेज PDF फीड करें, या आउटपुट को सर्चेबल Azure Cognitive Search इंडेक्स में इंटीग्रेट करें। वही पैटर्न लागू होता है—सिर्फ भाषा फ़्लैग को समायोजित करें और शायद कस्टम शब्दकोश को विस्तारित करें।

यदि आपको यह गाइड उपयोगी लगा, तो इसे GitHub पर स्टार दें, टीम के साथ साझा करें, या नीचे टिप्पणी छोड़ें। कोडिंग का आनंद लें, और आपके OCR परिणाम हमेशा त्रुटि‑रहित रहें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}