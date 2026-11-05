---
category: general
date: 2026-02-13
description: Aspose OCR का उपयोग करके रसीद को जल्दी पढ़ना और regex से राशि निकालना।
  OCR के साथ रसीद को चरण‑दर‑चरण प्रोसेस करना सीखें।
draft: false
keywords:
- how to read receipt
- extract amount using regex
- regex find total
- process receipt with ocr
language: hi
og_description: C# में Aspose OCR और regex का उपयोग करके रसीद कैसे पढ़ें। यह गाइड
  आपको दिखाता है कि OCR के साथ रसीद को कैसे प्रोसेस करें और कुल राशि निकालें।
og_title: C# में रसीद कैसे पढ़ें – पूर्ण OCR और रेगेक्स ट्यूटोरियल
tags:
- OCR
- C#
- Regex
- Aspose
title: C# में रसीद पढ़ने का तरीका – OCR + Regex गाइड
url: /hi/net/text-recognition/how-to-read-receipt-in-c-ocr-regex-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में रसीद पढ़ने का तरीका – OCR + Regex गाइड

क्या आपने कभी **रसीद पढ़ने** की प्रक्रिया को मैन्युअली टाइप किए बिना स्वचालित करने के बारे में सोचा है? कई छोटे‑व्यवसाय एप्लिकेशन्स में आपको रसीद की फोटो से कुल राशि निकालनी होती है, और इसे हाथ से करना ऑटोमेशन का उद्देश्य ही बिगाड़ देता है। अच्छी खबर? Aspose OCR के साथ आप इंजन को भारी काम करने दे सकते हैं, फिर एक साधा रेगुलर एक्सप्रेशन कुल राशि को ढूँढ लेगा। इस ट्यूटोरियल में हम **process receipt with OCR** को समझेंगे, regex का उपयोग करके राशि निकालेंगे, और तैयार‑टू‑यूज़ कुल मान प्राप्त करेंगे।

आप एक पूर्ण, चलने योग्य उदाहरण देखेंगे, समझेंगे कि रसीद भाषा मॉडल क्यों महत्वपूर्ण है, और विभिन्न मुद्रा चिह्नों या “Total” लेबल की अनुपस्थिति जैसे एज केस को कैसे संभालें। कोई बाहरी दस्तावेज़ आवश्यक नहीं—आपको जो चाहिए वह सब यहाँ है।

## आप क्या सीखेंगे

- Aspose OCR को रसीद‑विशिष्ट पहचान ( `Receipt` भाषा मॉडल स्वचालित रूप से इमेज को डि‑स्क्यू और डि‑नॉइज़ करता है) के लिए कैसे सेट‑अप करें।  
- एक रेगुलर एक्सप्रेशन लागू करना जो **extract amount using regex** पैटर्न के साथ अधिकांश US‑स्टाइल रसीदों के लिए काम करता है।  
- “TOTAL”, “Total:”, या “Grand Total – $12.34” जैसी सामान्य विविधताओं को कैसे संभालें।  
- परिणाम को सुरक्षित रूप से आउटपुट करना और जब पैटर्न न मिले तो क्या करें।  

**Prerequisites**: .NET 6+ (या .NET Framework 4.7+), एक वैध Aspose OCR लाइसेंस या ट्रायल, और स्थानीय रूप से सहेजी गई रसीद की इमेज। बस इतना ही—Aspose.OCR के अलावा कोई अतिरिक्त NuGet पैकेज नहीं चाहिए।

---

## Step 1 – Install Aspose OCR and Prepare the Project

### Why this matters

Aspose OCR एक purpose‑built **process receipt with OCR** मॉडल प्रदान करता है जो मुड़ी हुई कागज़ को सीधा कर सकता है और बैकग्राउंड नॉइज़ को अनदेखा करता है। सामान्य टेक्स्ट मॉडल का उपयोग करने से विशेषकर लो‑रिज़ॉल्यूशन स्कैन पर अधिक त्रुटियाँ होंगी।

### Code

```csharp
// Install the package via NuGet first:
//   dotnet add package Aspose.OCR
using Aspose.OCR;
using Aspose.OCR.Enums;
using System.Text.RegularExpressions;

// If you have a license file, load it now (optional but removes trial watermark)
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

> **Pro tip:** लाइसेंस फ़ाइल को अपने स्रोत नियंत्रण फ़ोल्डर के बाहर रखें ताकि आकस्मिक कमिट से बचा जा सके।

---

## Step 2 – Configure the OCR Engine for Receipt Recognition

### Why this matters

`Receipt` भाषा मॉडल में बिल्ट‑इन डि‑स्क्यू और डि‑नॉइज़ शामिल है, जो वास्तविक‑दुनिया की रसीदों (जो अक्सर मोड़ी या क्रीज़्ड होती हैं) पर सटीकता को काफी बढ़ाता है।

### Code

```csharp
// Step 2: Create and configure the OCR engine for receipt processing
var ocrEngine = new OcrEngine
{
    // Receipt model is optimized for invoices, grocery receipts, etc.
    Language = OcrLanguage.Receipt
};
```

---

## Step 3 – Recognize Text from the Receipt Image

### Why this matters

कोई भी regex लागू करने से पहले आपको कच्चा टेक्स्ट चाहिए। `RecognizeImage` मेथड एक `OcrResult` लौटाता है जिसमें पूरी स्ट्रिंग, confidence स्कोर, और अन्य जानकारी होती है, जिसे बाद में उपयोग किया जा सकता है।

### Code

```csharp
// Step 3: Recognize text from the receipt image
// Replace the path with the actual location of your receipt file.
string receiptPath = @"C:\Receipts\sample-receipt.jpg";

OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

// Quick sanity check – print the whole OCR output (helps debugging)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(receiptResult.Text);
Console.WriteLine("===================\n");
```

**Expected OCR output (example)**  
```
Walmart Supercenter
123 Main St.
Anytown, USA
Date: 02/12/2026
Item A   $3.45
Item B   $7.89
Subtotal $11.34
Tax      $0.91
Total:   $12.25
Thank you!
```

---

## Step 4 – Build a Regex to **Extract Amount Using Regex**

### Why this matters

रसीदों के फॉर्मेट अलग‑अलग होते हैं, लेकिन शब्द “Total” (या उसका कोई समान रूप) के बाद डॉलर राशि होना एक भरोसेमंद एंकर है। नीचे दिया गया पैटर्न वैकल्पिक स्पेसेस, कोलन, हाइफ़न, और वैकल्पिक `$` साइन को संभालता है।

### Code

```csharp
// Step 4: Use a regular expression to locate the total amount in the recognized text
string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
RegexOptions options = RegexOptions.IgnoreCase;

Match totalMatch = Regex.Match(receiptResult.Text, pattern, options);
```

**Explanation of the pattern**

| Part | Meaning |
|------|---------|
| `Total` | शब्द “Total” को (case‑insensitive) खोजता है। |
| `\s*[:\-]?` | किसी भी व्हाइटस्पेस के बाद वैकल्पिक कोलन या हाइफ़न की अनुमति देता है। |
| `\s*\$?` | वैकल्पिक व्हाइटस्पेस और वैकल्पिक डॉलर साइन। |
| `(\d+(\.\d{2})?)` | एक या अधिक अंकों को कैप्चर करता है, वैकल्पिक रूप से दशमलव और दो सेंट्स के साथ। |

---

## Step 5 – Output the Extracted Total or Handle Missing Data

### Why this matters

सबसे अच्छे OCR भी कभी‑कभी शब्द को मिस कर सकते हैं, खासकर धुंधली रसीदों पर। एक ग्रेसफ़ुल फॉलबैक प्रदान करने से क्रैश रोकते हैं और कस्टम लॉजिक (जैसे उपयोगकर्ता से पुष्टि माँगना) के लिए हुक मिलता है।

### Code

```csharp
// Step 5: Output the extracted total, or indicate it wasn't found
if (totalMatch.Success)
{
    string amount = totalMatch.Groups[1].Value;
    Console.WriteLine($"Total: ${amount}");
}
else
{
    Console.WriteLine("Total amount not found. Consider reviewing the OCR output manually.");
}
```

**Sample console output**

```
Total: $12.25
```

---

## Full Working Example – All Steps in One File

नीचे एक सिंगल, सेल्फ‑कंटेन्ड प्रोग्राम है जिसे आप कॉन्सोल प्रोजेक्ट में कॉपी‑पेस्ट कर सकते हैं। इसमें कमेंट्स, एरर हैंडलिंग, और वैकल्पिक लाइसेंस लोडिंग शामिल है।

```csharp
// ---------------------------------------------------------------
// How to Read Receipt in C# – OCR + Regex (Complete Example)
// ---------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Enums;
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 0️⃣ Optional: Load your Aspose OCR license (remove trial watermark)
        try
        {
            var license = new Aspose.OCR.License();
            license.SetLicense("Aspose.OCR.lic"); // path to .lic file
        }
        catch (Exception ex)
        {
            Console.WriteLine("License not found – running in trial mode.");
        }

        // 1️⃣ Configure the OCR engine for receipt processing
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Receipt // receipt model = de‑skew + de‑noise
        };

        // 2️⃣ Path to the receipt image (change to your file)
        string receiptPath = @"YOUR_DIRECTORY/receipt.jpg";

        // 3️⃣ Perform OCR
        OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

        // 4️⃣ Debug: show full OCR text (helps when regex fails)
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(receiptResult.Text);
        Console.WriteLine("===================\n");

        // 5️⃣ Regex to **extract amount using regex** (find the total)
        string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
        Match totalMatch = Regex.Match(receiptResult.Text, pattern,
                                        RegexOptions.IgnoreCase);

        // 6️⃣ Output
        if (totalMatch.Success)
        {
            string amount = totalMatch.Groups[1].Value;
            Console.WriteLine($"Total: ${amount}");
        }
        else
        {
            Console.WriteLine("Total amount not found. You might need to adjust the regex or improve image quality.");
        }
    }
}
```

**Running the program**

1. एक नया कॉन्सोल प्रोजेक्ट बनाएं (`dotnet new console -n ReceiptReader`)।  
2. Aspose.OCR NuGet पैकेज जोड़ें (`dotnet add package Aspose.OCR`)।  
3. `YOUR_DIRECTORY/receipt.jpg` को रसीद इमेज के वास्तविक पाथ से बदलें।  
4. बिल्ड और रन करें (`dotnet run`)।  

यदि सब कुछ सही रहा तो आपको OCR डम्प के बाद `Total: $xx.xx` दिखना चाहिए।

---

## Handling Edge Cases & Common Variations

### 1. Different Currency Symbols

यदि आप यूरो (€) या पाउंड (£) के साथ काम करते हैं, तो पैटर्न को इस प्रकार विस्तारित करें:

```csharp
string pattern = @"Total\s*[:\-]?\s*[$€£]?\s*(\d+(\.\d{2})?)";
```

### 2. Missing “Total” Label

कुछ रसीदों में केवल “Grand Total” दिखता है। वैकल्पिक जोड़ें:

```csharp
string pattern = @"(?:Total|Grand\s*Total)\s*[:\-]?\s*[$]?\s*(\d+(\.\d{2})?)";
```

### 3. Multiple Totals (e.g., “Subtotal” and “Total”)

यदि regex पहली occurrence को मैच करता है, तो आप **last** मैच चाहते हैं:

```csharp
MatchCollection matches = Regex.Matches(receiptResult.Text, pattern,
                                         RegexOptions.IgnoreCase);
Match last = matches.Count > 0 ? matches[matches.Count - 1] : null;
```

### 4. Low‑Resolution Images

- स्कैन करते समय DPI बढ़ाएँ (`300 DPI` एक अच्छा पॉइंट है)।  
- इमेज को Aspose को फीड करने से पहले एक साधा ब्लर‑रिड्यूस फ़िल्टर से प्री‑प्रोसेस करें (इस गाइड के दायरे से बाहर, लेकिन एक्सप्लोर करने लायक है)।

---

## Pro Tips for Real‑World Projects

- **Cache the OCR result** यदि आपको कई फ़ील्ड (टैक्स, आइटम्स, आदि) निकालने हैं – OCR लागत केवल एक बार आएगी।  
- **Log the raw OCR text** को डेटाबेस में रखें; यह विवादित खर्चों के लिए एक मूल्यवान ऑडिट ट्रेल बन जाता है।  
- जब आप वेब API बना रहे हों, **run OCR in a background worker**; यह कुछ सौ मिलीसेकंड ले सकता है, जो असिंक्रोनस रूप में ठीक है लेकिन सिंक्रोनस रिक्वेस्ट में आदर्श नहीं।  
- **Validate the extracted amount** को बिज़नेस रूल्स के खिलाफ (जैसे amount > 0) जांचें, फिर ही स्टोर करें।

---

## Conclusion

हमने **how to read receipt** इमेजेज़ को C# में Aspose OCR के साथ कवर किया, फिर **extract amount using regex** करके कुल लाइन को भरोसेमंद रूप से पाया। `Receipt` भाषा मॉडल का उपयोग करके आपको डि‑स्क्यूड, डि‑नॉइज़्ड टेक्स्ट मिलता है, और एक संक्षिप्त रेगुलर एक्सप्रेशन अधिकांश फ़ॉर्मेटिंग क्विर्क्स को संभालता है। ऊपर दिया गया पूर्ण कोड स्निपेट किसी भी .NET कॉन्सोल या सर्विस प्रोजेक्ट में डालने के लिए तैयार है, और अतिरिक्त एज‑केस सुझाव आपको प्रोडक्शन उपयोग के लिए ठोस आधार देते हैं।

अगला कदम तैयार है? समाधान को individual line items निकालने, टैक्स ऑटो‑कैल्कुलेट करने, या expense‑tracking API के साथ इंटीग्रेट करने के लिए विस्तारित करें। और यदि कोई रसीद पैटर्न को तोड़ देती है, तो याद रखें कि **regex find total** अप्रोच सिर्फ एक शुरुआती बिंदु है—आप हमेशा अपने लोकल सेटिंग्स के अनुसार पैटर्न को ट्यून कर सकते हैं।

Happy coding, और आपकी रसीद‑प्रोसेसिंग तेज़, सटीक, और पूरी तरह ऑटोमेटेड रहे!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}