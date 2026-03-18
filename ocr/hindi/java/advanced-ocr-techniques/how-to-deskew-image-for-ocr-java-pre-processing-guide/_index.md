---
category: general
date: 2026-03-18
description: Aspose OCR Java का उपयोग करके छवि को जल्दी से डेस्क्यू कैसे करें। OCR
  के लिए छवि को पूर्व-प्रसंस्करण करना सीखें, स्कैन की गई छवि को साफ़ करें और कुछ ही
  चरणों में OCR की सटीकता बढ़ाएँ।
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- clean scanned image
- improve ocr accuracy
language: hi
og_description: Aspose OCR Java के साथ इमेज को डेस्क्यू कैसे करें, OCR के लिए इमेज
  को प्रीप्रोसेस करें, स्कैन की गई इमेज को साफ़ करें और OCR की सटीकता में सुधार करें।
og_title: OCR के लिए इमेज को डेस्क्यू कैसे करें – जावा गाइड
tags:
- OCR
- Java
- Image Processing
title: OCR के लिए इमेज को डेस्क्यू कैसे करें – जावा प्री‑प्रोसेसिंग गाइड
url: /hi/java/advanced-ocr-techniques/how-to-deskew-image-for-ocr-java-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR के लिए इमेज को डेस्क्यू कैसे करें – जावा प्री‑प्रोसेसिंग गाइड

क्या आपने कभी **इमेज को डेस्क्यू** करने के बारे में सोचा है जब स्कैनर से निकली फ़ाइलें अजीब कोण पर आती हैं? आप अकेले नहीं हैं—कई डेवलपर्स को यह समस्या आती है जब वे इमेज‑भारी दस्तावेज़ों से टेक्स्ट निकालने की कोशिश करते हैं। अच्छी खबर? कुछ ही लाइनों के जावा कोड और Aspose OCR के साथ आप इमेज को सीधा, शोर‑मुक्त और साफ़ टेक्स्ट निकाल सकते हैं बिना किसी परेशानी के।

इस ट्यूटोरियल में हम पूरी वर्कफ़्लो को देखेंगे: शोरयुक्त, घुमाई गई स्कैन को लोड करना, डेस्क्यू फ़िल्टर लागू करना, दृश्य शोर हटाना, और अंत में **इमेज से टेक्स्ट निकालना**। अंत तक आप जान जाएंगे **OCR के लिए इमेज को प्री‑प्रोसेस** कैसे करें, **स्कैन की गई इमेज को साफ़** करें, और किसी भी प्रोजेक्ट के लिए **OCR की सटीकता बढ़ाएँ** जो विश्वसनीय टेक्स्ट एक्सट्रैक्शन की जरूरत रखता है।

## What You’ll Need

- Java 17 (या कोई भी हालिया JDK) – कोड मानक भाषा सुविधाओं का उपयोग करता है।
- Aspose OCR for Java लाइब्रेरी (फ्री ट्रायल प्रयोग के लिए पर्याप्त है)।
- एक सैंपल इमेज जो शोरयुक्त और घुमाई हुई हो (जैसे `noisy-rotated.png`)।
- आपका पसंदीदा IDE (IntelliJ IDEA, Eclipse, VS Code…) – कोई भी जो जावा कम्पाइल कर सके।

कोई अतिरिक्त फ्रेमवर्क नहीं, कोई Maven/Gradle जादू नहीं; केवल नीचे दिखाए गए इम्पोर्ट स्टेटमेंट्स ही आवश्यक हैं।

---

## How to Deskew Image with Aspose OCR

सबसे पहले हमें इमेज के झुकाव को ठीक करना है। यदि टेक्स्ट लाइन्स क्षैतिज नहीं हैं, तो OCR इंजन अक्षरों को गलत पढ़ेगा। `DeskewFilter` इस काम को संभालता है।

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;
import com.aspose.ocr.preprocess.DeskewFilter;
import com.aspose.ocr.preprocess.DenoiseFilter;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the raw scanned image
        Image scannedImage = Image.load("YOUR_DIRECTORY/noisy-rotated.png");

        // Step 3: Correct the image orientation (deskew)
        DeskewFilter deskewFilter = new DeskewFilter();
        scannedImage = deskewFilter.apply(scannedImage);

        // Step 4: Reduce visual noise (denoise)
        DenoiseFilter denoiseFilter = new DenoiseFilter();
        scannedImage = denoiseFilter.apply(scannedImage);

        // Step 5: Perform OCR on the cleaned image
        String recognizedText = ocrEngine.recognize(scannedImage);

        // Step 6: Output the extracted text
        System.out.println(recognizedText);
    }
}
```

> **Why this matters:** `DeskewFilter` इमेज की ज्योमेट्री का विश्लेषण करता है, घुमाव का कोण अनुमानित करता है, और बिटमैप को फिर से क्षैतिज कर देता है। इस चरण के बिना अधिकांश OCR इंजन तिरछे अक्षरों को पूरी तरह अलग ग्लिफ़ मानते हैं, जिससे आपका **improve OCR accuracy** प्रयास नीचे गिर जाता है।

> **Pro tip:** यदि आप ऐसे दस्तावेज़ों से निपट रहे हैं जो उल्टे हो सकते हैं, तो `DeskewFilter` पर `setAutoRotate` फ़्लैग सक्षम करें (नए Aspose रिलीज़ में उपलब्ध)। यह आवश्यकता पड़ने पर स्वचालित रूप से 180° घुमा देता है।

![इमेज को डेस्क्यू करने से पहले और बाद का डायग्राम – कैसे इमेज को डेस्क्यू करें](https://example.com/deskew-diagram.png "इमेज को डेस्क्यू करने का उदाहरण")

*Image alt text: इमेज को डेस्क्यू करने का उदाहरण*

---

## Preprocess Image for OCR – Denoising and Cleaning

एक बार इमेज सीधी हो जाने के बाद, अगला बाधा है दृश्य शोर—वे बिंदु, कम्प्रेशन आर्टिफैक्ट्स, या हल्के बैकग्राउंड पैटर्न जो OCR इंजन को भ्रमित करते हैं। `DenoiseFilter` एक सूक्ष्म स्मूदिंग एल्गोरिद्म लागू करता है जो किनारों (अक्षर) को संरक्षित रखते हुए ग्रेन को हटाता है।

```java
// Step 4 (continued): Reduce visual noise (denoise)
DenoiseFilter denoiseFilter = new DenoiseFilter();
scannedImage = denoiseFilter.apply(scannedImage);
```

### When to Adjust Denoising Settings

- **बहुत डार्क स्कैन:** बैकग्राउंड शैडोज़ को हटाने के लिए फ़िल्टर की स्ट्रेंथ बढ़ाएँ (`denoiseFilter.setStrength(2)`)।
- **फाइन‑प्रिंट फ़ॉन्ट्स:** बहुत अधिक ब्लरिंग से बचने के लिए स्ट्रेंथ कम रखें।
- **रंगीन दस्तावेज़:** पहले ग्रेस्केल में बदलें (`scannedImage = scannedImage.toGrayscale();`)—OCR इंजन सिंगल‑चैनल इमेज पर बेहतर काम करता है।

ये समायोजन **clean scanned image** की बेस्ट प्रैक्टिस का हिस्सा हैं; एक साफ़ बिटमैप सीधे OCR इंजन के उच्च कॉन्फिडेंस स्कोर में बदल जाता है।

---

## Extract Text from Image – Running the OCR Engine

अब जब चित्र सीधा और शांत है, तो **इमेज से टेक्स्ट निकालने** का समय है। `OcrEngine` क्लास सब कुछ बैकग्राउंड में संभालता है: सेगमेंटेशन, कैरेक्टर क्लासिफिकेशन, और लैंग्वेज मॉडलिंग।

```java
// Step 5: Perform OCR on the cleaned image
String recognizedText = ocrEngine.recognize(scannedImage);
System.out.println(recognizedText);
```

#### Expected Output

यदि आपके स्रोत फ़ाइल में लाइन “**Invoice # 12345**” है, तो कंसोल कुछ इस तरह प्रिंट करेगा:

```
Invoice # 12345
Date: 2026-03-18
Total: $1,250.00
```

यदि आउटपुट गड़बड़ दिखे, तो पिछले चरणों—विशेषकर डेस्क्यूइंग—को दोबारा जांचें। सिर्फ 1‑डिग्री का झुकाव भी नंबरों और सिंबल्स को बिगाड़ सकता है।

---

## Common Pitfalls & Tips to **Improve OCR Accuracy**

| Issue | Why it hurts accuracy | Quick fix |
|-------|----------------------|-----------|
| **शेष घुमाव** | OCR क्षैतिज बेसलाइन की अपेक्षा करता है। | `deskewFilter.getAngle()` से जांचें और मान लॉग करें। |
| **अधिक‑डेनॉइज़िंग** | पतली स्ट्रोक ब्लर हो जाती हैं, “i” को “l” बना देती हैं। | नाज़ुक फ़ॉन्ट्स के लिए `setStrength(0.5)` उपयोग करें। |
| **गलत इमेज फ़ॉर्मेट** | JPEG कम्प्रेशन आर्टिफैक्ट्स जोड़ता है। | लॉसलेस स्टोरेज के लिए PNG या TIFF पसंद करें। |
| **गलत भाषा** | इंजन डिफ़ॉल्ट रूप से अंग्रेज़ी मानता है; अन्य लिपियों के लिए स्पष्ट सेटिंग चाहिए। | `ocrEngine.setLanguage(OcrEngine.Language.Spanish);` |
| **कम DPI (≤150)** | विश्वसनीय सेगमेंटेशन के लिए पर्याप्त पिक्सेल डेटा नहीं। | प्रोसेसिंग से पहले 300 DPI पर री‑सैंपल करें (`scannedImage = scannedImage.resample(300);`). |

### Bonus: Batch Processing

यदि आपके पास स्कैन की फ़ोल्डर है, तो डेमो को लूप में रैप करें:

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.endsWith(".png"))) {
    Image img = Image.load(file.getAbsolutePath());
    img = new DeskewFilter().apply(img);
    img = new DenoiseFilter().apply(img);
    String text = ocrEngine.recognize(img);
    System.out.println("=== " + file.getName() + " ===");
    System.out.println(text);
}
```

यह पैटर्न आपको **OCR के लिए इमेज को प्री‑प्रोसेस** बड़े पैमाने पर करने देता है, कोडबेस को साफ़ रखता है और प्रदर्शन को पूर्वानुमेय बनाता है।

---

## Recap & Next Steps

हमने **इमेज को डेस्क्यू** करने, **OCR के लिए इमेज को प्री‑प्रोसेस** करने, और अंत में **इमेज से टेक्स्ट निकालने** को Aspose OCR जावा के साथ कवर किया। स्कैन को सीधा करके, शोर हटाकर, और एक शुद्ध बिटमैप को इंजन को फीड करके आप पूरे प्रोजेक्ट में **OCR की सटीकता बढ़ाएँ**गे।

अगला क्या? इन एक्सटेंशन पर विचार करें:

- **भाषा पहचान** – `ocrEngine.setLanguage` को डिटेक्टेड स्क्रिप्ट के आधार पर स्विच करें।
- **PDF आउटपुट** – पहचाने गए टेक्स्ट को सर्चेबल डॉक्यूमेंट के लिए PDF जेनरेटर में फीड करें।
- **मशीन‑लर्निंग पोस्ट‑प्रोसेसिंग** – OCR परिणाम पर स्पेल‑चेक या कस्टम डिक्शनरी चलाएँ।

इन विचारों को आज़माएँ, विभिन्न फ़िल्टर स्ट्रेंथ के साथ प्रयोग करें, और आप किसी भी दस्तावेज़‑डिजिटलीज़ेशन प्रोजेक्ट के लिए एक मजबूत पाइपलाइन बना लेंगे।

---

*हैप्पी कोडिंग! अगर कोई समस्या आती है, तो नीचे कमेंट करें—मैं आपको डेस्क्यू और डेनॉइज़ पैरामीटर को फाइन‑ट्यून करने में मदद करूंगा।*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}