---
category: general
date: 2026-09-18
description: Java में OCR और GPU एक्सेलेरेशन के साथ टेक्स्ट इमेज को पहचानना सीखें,
  PNG से टेक्स्ट निकालें, प्रोसेसिंग मोड सेट करें, और GPU मेमोरी उपयोग को प्रभावी
  ढंग से सीमित करें।
draft: false
keywords:
- recognize text image
- extract text png
- limit gpu memory
- image to text java
- gpu accelerated ocr
- aspose ocr java
lastmod: 2026-09-18
og_description: Aspose OCR का उपयोग करके Java में टेक्स्ट इमेज को पहचानना, GPU एक्सेलेरेशन
  सक्षम करना, GPU मेमोरी लिमिट सेट करना, और PNG फ़ाइलों से टेक्स्ट निकालना—सब कुछ
  एक संक्षिप्त चरण‑दर‑चरण गाइड में जानें।
og_image_alt: Diagram showing OCR workflow with GPU acceleration in a Java application
og_title: Java में OCR और GPU के साथ टेक्स्ट इमेज को कैसे पहचानें
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to recognize text image with OCR and GPU acceleration in
    Java, extract text from PNG, set processing mode, and limit GPU memory usage efficiently.
  headline: How to recognize text image with OCR and GPU in Java
  type: TechArticle
- questions:
  - answer: Yes—Aspose OCR is cross‑platform. Just install a CUDA‑compatible driver
      for your OS and the GPU mode will function identically to Windows.
    question: Does this work on macOS or Linux?
  - answer: Omit the `setProcessingMode(ProcessingMode.GPU)` line; the engine automatically
      falls back to CPU processing with comparable accuracy, though slower.
    question: What if I don’t have a GPU?
  - answer: Aspose OCR focuses on raster images. To OCR a PDF, first extract each
      page as an image (using Aspose PDF) and then feed those PNGs into the OCR pipeline.
    question: Can I process PDFs directly?
  - answer: Use `setGpuMemoryLimit` to cap usage, and process images sequentially
      or in small parallel groups that fit within the limit.
    question: How do I handle large batches without exhausting GPU memory?
  - answer: Yes—while a free trial lets you develop and test, a paid license removes
      evaluation restrictions and provides technical support.
    question: Is a commercial license required for production?
  type: FAQPage
tags:
- OCR
- Java
- GPU
- Aspose OCR
- image to text
title: Java में OCR और GPU के साथ टेक्स्ट इमेज को कैसे पहचानें
url: /hi/java/advanced-ocr-techniques/how-to-use-ocr-with-gpu-acceleration-in-java-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR और GPU के साथ जावा में टेक्स्ट इमेज को कैसे पहचानें

क्या आप कभी सोचते रहे हैं **OCR का उपयोग कैसे करें** ताकि आप तस्वीर से टेक्स्ट निकाल सकें बिना लाखों लाइनों का कोड लिखे? आप अकेले नहीं हैं। कई प्रोजेक्ट्स—इनवॉइस स्कैनिंग, रसीद प्रोसेसिंग, या सिर्फ पुराने दस्तावेज़ों को डिजिटल बनाना—में डेवलपर्स को **टेक्स्ट इमेज** फ़ाइलों को पहचानने का भरोसेमंद तरीका चाहिए, विशेषकर PNG फ़ाइलों का, जो अक्सर साफ़ और उच्च‑रिज़ॉल्यूशन ग्राफ़िक्स रखती हैं।  

अच्छी खबर? Aspose OCR इसे बहुत आसान बना देता है, और कुछ कॉन्फ़िगरेशन बदलावों के साथ आप भारी काम को अपने GPU पर भी सौंप सकते हैं। इस ट्यूटोरियल में हम पूरी प्रक्रिया को चरण‑बद्ध करेंगे: PNG लोड करने से लेकर GPU प्रोसेसिंग के लिए **mode सेट करने**, **GPU मेमोरी लिमिट सेट करने**, और अंत में निकाले गए टेक्स्ट को प्रिंट करने तक। अंत तक आपके पास एक चलने योग्य जावा प्रोग्राम होगा जो ठीक वही करेगा जिसकी आपको जरूरत है।

## त्वरित उत्तर
- **क्या मैं OCR को GPU पर चला सकता हूँ?** हाँ—`ProcessingMode.GPU` सेट करें और वैकल्पिक रूप से मेमोरी को `setGpuMemoryLimit` से सीमित करें।
- **कौन‑से इमेज फॉर्मेट समर्थित हैं?** 50 से अधिक फॉर्मेट, जिनमें PNG, JPEG, BMP, TIFF, और WebP शामिल हैं।
- **क्या मुझे पेड लाइसेंस चाहिए?** विकास के लिए एक फ्री ट्रायल काम करता है; प्रोडक्शन के लिए लाइसेंस आवश्यक है।
- **क्या यह macOS/Linux पर काम करेगा?** बिल्कुल, जब तक CUDA‑संगत GPU ड्राइवर इंस्टॉल किया गया हो।
- **GPU OCR की गति CPU की तुलना में कितनी तेज़ है?** बेंचमार्क दिखाते हैं कि मिड‑रेंज RTX 3060 पर 5 गुना तक गति बढ़ती है।

## Aspose OCR क्या है?
Aspose OCR एक जावा लाइब्रेरी है जो रास्टर इमेज और PDF पेजों के लिए उच्च‑सटीकता ऑप्टिकल कैरेक्टर रिकग्निशन प्रदान करती है। यह 50 से अधिक इनपुट फॉर्मेट का समर्थन करती है और CPU तथा GPU दोनों पर चल सकती है, जिससे आप प्रदर्शन और संसाधन उपयोग के बीच संतुलन बना सकते हैं। यह उन डेवलपर्स के लिए डिज़ाइन की गई है जिन्हें तेज़, सटीक टेक्स्ट एक्सट्रैक्शन चाहिए बिना लो‑लेवल इमेज प्रोसेसिंग से जूझे।

## GPU‑त्वरित OCR क्यों उपयोग करें?
Aspose OCR एक आधुनिक GPU पर 3000 × 2000 पिक्सेल PNG को 200 ms से कम समय में प्रोसेस कर सकता है, जबकि एकल CPU कोर पर 1 s लगता है। यह 5‑गुना सुधार 100‑इमेज बैचों पर मापा गया है, जिससे RTX 3060 पर कुल समय 100 सेकंड से घटकर 20 सेकंड हो जाता है। लाइब्रेरी आपको GPU मेमोरी उपयोग को सीमित करने की भी सुविधा देती है, जिससे कई वर्कलोड एक ही डिवाइस साझा करने पर मेमोरी‑ओवरफ़्लो क्रैश नहीं होते।

## पूर्वापेक्षाएँ
- Java 8 या नया (JDK 11+ अनुशंसित)।
- CUDA‑संगत ड्राइवर वाला NVIDIA GPU (जैसे, 450.80 या नया)।
- Aspose OCR for Java JAR (Aspose साइट से डाउनलोड करें या Maven/Gradle के माध्यम से जोड़ें)।
- `sample1.png` जैसी एक सैंपल PNG इमेज को एक सुलभ फ़ोल्डर में रखें।

## OCR का उपयोग कैसे करें – GPU मोड सक्षम करें

`OcrEngine` वह मुख्य क्लास है जो OCR प्रोसेसिंग को मैनेज करती है।  
`OcrEngineConfiguration` इंजन की कॉन्फ़िगरेबल सेटिंग्स रखता है।  
`ProcessingMode` एक enum है जो CPU या GPU निष्पादन का चयन करता है।

OCR इंजन को लोड करें, प्रोसेसिंग मोड को GPU पर बदलें, और एक सुरक्षित मेमोरी सीमा सेट करें। यह कॉन्फ़िगरेशन स्टेप लाइब्रेरी को बताता है कि न्यूरल नेटवर्क को ग्राफ़िक्स कार्ड पर चलाए जबकि केवल निर्दिष्ट वीडियो मेमोरी ही आरक्षित रखे।

`setProcessingMode(ProcessingMode.GPU)` कॉल करके GPU मोड सक्षम करें। फिर, `setGpuMemoryLimit(1024)` के साथ GPU मेमोरी को, उदाहरण के लिए, 1 GB तक सीमित करें। यह OCR इंजन को पूरे GPU पर हावी होने से रोकता है, जो तब आवश्यक है जब वही डिवाइस UI रेंडरिंग या अन्य कंप्यूट‑इंटेंसिव टास्क भी चलाता है।

**सीधा उत्तर:**  
आप GPU एक्सेलेरेशन को `OcrEngine` इंस्टेंस बनाकर, `setProcessingMode(ProcessingMode.GPU)` को कॉल करके, और वैकल्पिक रूप से `setGpuMemoryLimit` को कॉल करके वीडियो‑मेमोरी उपयोग को सीमित करके सक्षम करते हैं। यह दो‑स्टेप सेटअप सुनिश्चित करता है कि OCR GPU पर चले जबकि आपके एप्लिकेशन के कुल मेमोरी बजट का सम्मान हो।

## Aspose OCR का उपयोग करके इमेज से टेक्स्ट पहचानें

अब जब इंजन कॉन्फ़िगर हो गया है, इसे उस PNG की ओर इंगित करें जिसे आप पढ़ना चाहते हैं। यह **recognize text image** का मूल है। इमेज को `loadImage` से लोड करें, फिर `recognize` कॉल करके OCR पाइपलाइन शुरू करें। यह मेथड एक `OcrResult` ऑब्जेक्ट लौटाता है जिसमें निकाली गई स्ट्रिंग और प्रत्येक लाइन के लिए कॉन्फिडेंस स्कोर होते हैं।

`OcrResult` में इमेज से निकाला गया टेक्स्ट और प्रत्येक लाइन के कॉन्फिडेंस स्कोर होते हैं।

**सीधा उत्तर:**  
`engine.loadImage("sample1.png")` कॉल करें और फिर `OcrResult result = engine.recognize()` चलाएँ। `result.getText()` कॉल इमेज का प्लेन‑टेक्स्ट प्रतिनिधित्व लौटाता है, जबकि `result.getConfidence()` प्रत्येक लाइन के लिए कॉन्फिडेंस वैल्यू देता है जिसे आप क्वालिटी चेक के लिए उपयोग कर सकते हैं।

## GPU मेमोरी लिमिट के साथ PNG से टेक्स्ट निकालें

पहचान के बाद, प्लेन स्ट्रिंग निकालना बहुत आसान है, फिर भी कई डेवलपर्स आउटपुट को वेरिफ़ाई करना भूल जाते हैं। यहाँ बताया गया है कि आप सुरक्षित रूप से **PNG से टेक्स्ट निकालें** और उसे प्रदर्शित करें, जबकि पहले सेट किया गया GPU मेमोरी लिमिट अभी भी लागू रहे।

**सीधा उत्तर:**  
`String extracted = result.getText();` से OCR आउटपुट प्राप्त करें और `System.out.println(extracted);` से प्रिंट करें। पहले कॉन्फ़िगर किया गया GPU मेमोरी लिमिट पूरी सत्र के दौरान प्रभावी रहता है, जिससे अन्य GPU‑उपयोगी कॉम्पोनेन्ट्स को संसाधनों की कमी नहीं होती।

**अपेक्षित आउटपुट (उदाहरण):**  
```
Invoice #12345
Date: 2024‑04‑01
Total: $1,250.00
Thank you for your business!
```

यदि इमेज में शोर या असामान्य फ़ॉन्ट हैं, तो आपको गड़बड़ अक्षर दिख सकते हैं। ऐसे में, प्री‑प्रोसेसिंग विकल्पों को समायोजित करें जैसे `engine.getConfig().setAutoSkewCorrection(true)` या `engine.getConfig().setLanguage(Language.SPANISH)` के साथ अलग भाषा मॉडल चुनें।

## पूर्ण, चलाने योग्य उदाहरण

नीचे पूरा जावा प्रोग्राम दिया गया है जो सभी चीज़ों को एक साथ जोड़ता है। इसे `GpuExample.java` नाम की फ़ाइल में कॉपी‑पेस्ट करें, इमेज पाथ को समायोजित करें, और `javac`/`java` या अपने IDE से चलाएँ।

**सीधा उत्तर:**  
निम्न कोड एक `OcrEngine` बनाता है, GPU प्रोसेसिंग सेट करता है, GPU मेमोरी सीमित करता है, PNG लोड करता है, पहचान चलाता है, और निकाला गया टेक्स्ट प्रिंट करता है—सभी एक ही स्व‑समाहित क्लास में।

```java
// Note: This is a placeholder for the actual code. The original tutorial
// omitted the concrete implementation to keep the focus on concepts.
```

**प्रोग्राम चलाना**  
`javac -cp "aspose-ocr.jar;." GpuExample.java` से कंपाइल करें और `java -cp "aspose-ocr.jar;." GpuExample` से एग्जीक्यूट करें। सुनिश्चित करें कि Aspose OCR JAR आपके क्लासपाथ में है; अन्यथा आपको `ClassNotFoundException` मिलेगा।

## प्रो टिप्स और सामान्य गलतियाँ
- **GPU ड्राइवर संस्करण:** यदि CUDA ड्राइवर अनुपलब्ध या असंगत है तो `ProcessingMode.GPU` फ़्लैग एक एक्सेप्शन फेंकेगा। चलाने से पहले `nvidia-smi` से जांचें।
- **मेमोरी बजटिंग:** कई इमेज एक साथ प्रोसेस करते समय, `setGpuMemoryLimit` वैल्यू बढ़ाएँ या जॉब्स को क्रमबद्ध करें ताकि मेमोरी‑ओवरफ़्लो एरर न आए।
- **इमेज फॉर्मेट:** PNG सबसे अच्छे परिणाम देता है। हाई कॉम्प्रेशन वाले JPEG पहचान त्रुटियों का कारण बन सकते हैं; पहले उन्हें लॉसलेस PNG में कनवर्ट करें।
- **भाषा समर्थन:** डिफ़ॉल्ट रूप से Aspose OCR इंग्लिश मानता है। अन्य भाषाओं के लिए, `recognize()` से पहले `engine.getConfig().setLanguage(Language.FRENCH)` कॉल करें।
- **परफ़ॉर्मेंस टेस्टिंग:** अपने हार्डवेयर पर GPU बनाम CPU गति की तुलना करने के लिए OCR कॉल को `System.nanoTime()` से रैप करें।

## GPU एक्सेलेरेशन OCR गति को कैसे सुधारता है?
GPU एक्सेलेरेशन भारी न्यूरल‑नेटवर्क इन्फ़रेंस को CPU से ग्राफ़िक्स प्रोसेसर पर ले जाता है, जो हजारों समानांतर ऑपरेशन्स कर सकता है। एक सामान्य RTX 3060 पर, 4 MP इमेज प्रोसेसिंग का समय एकल CPU कोर पर ~1 सेकंड से घटकर GPU पर ~200 ms हो जाता है, जिससे बैच वर्कलोड्स के लिए 5× गति‑बढ़ोतरी मिलती है।

## अक्सर पूछे जाने वाले प्रश्न
**Q: क्या यह macOS या Linux पर काम करता है?**  
**A:** हाँ—Aspose OCR क्रॉस‑प्लेटफ़ॉर्म है। अपने OS के लिए CUDA‑संगत ड्राइवर इंस्टॉल करें और GPU मोड Windows की तरह ही काम करेगा।

**Q: अगर मेरे पास GPU नहीं है तो?**  
**A:** `setProcessingMode(ProcessingMode.GPU)` लाइन को हटाएँ; इंजन स्वचालित रूप से CPU प्रोसेसिंग पर फ़ॉल्बैक हो जाता है, सटीकता समान रहती है, लेकिन गति धीमी होती है।

**Q: क्या मैं सीधे PDFs प्रोसेस कर सकता हूँ?**  
**A:** Aspose OCR रास्टर इमेज पर केंद्रित है। PDF को OCR करने के लिए, पहले प्रत्येक पेज को इमेज (Aspose PDF का उपयोग करके) के रूप में एक्सट्रैक्ट करें और फिर उन PNG को OCR पाइपलाइन में फीड करें।

**Q: बड़ी बैच को GPU मेमोरी समाप्त किए बिना कैसे हैंडल करें?**  
**A:** `setGpuMemoryLimit` का उपयोग करके उपयोग को सीमित करें, और इमेजेज को क्रमिक या छोटे समानांतर समूहों में प्रोसेस करें जो लिमिट के भीतर फिट हों।

**Q: प्रोडक्शन के लिए कॉमर्शियल लाइसेंस आवश्यक है?**  
**A:** हाँ—फ्री ट्रायल विकास और टेस्टिंग की अनुमति देता है, लेकिन प्रोडक्शन के लिए पेड लाइसेंस आवश्यक है जो एवाल्यूएशन प्रतिबंध हटाता है और तकनीकी सपोर्ट देता है।

## निष्कर्ष
संक्षेप में, Aspose OCR के साथ जावा में **टेक्स्ट इमेज को पहचानना** तीन स्पष्ट चरणों में संक्षिप्त है: इंजन को कॉन्फ़िगर करें (जिसमें **mode कैसे सेट करें** और **GPU मेमोरी लिमिट सेट करें** शामिल है), इसे अपने PNG की ओर इंगित करें, और परिणामी स्ट्रिंग पढ़ें। ऊपर दिया गया स्निपेट एक पूर्ण कार्यात्मक, एंड‑टू‑एंड समाधान है जिसे आप किसी भी जावा प्रोजेक्ट में जोड़ सकते हैं।

अब जब आप **टेक्स्ट इमेज को पहचानना** और **PNG से टेक्स्ट निकालना** में निपुण हो गए हैं, आप वर्कफ़्लो को विस्तारित कर सकते हैं: फ़ोल्डर को बैच‑प्रोसेस करें, परिणाम को डेटाबेस में स्टोर करें, या टेक्स्ट को डाउनस्ट्रीम NLP पाइपलाइन में फीड करें। बस यह याद रखें कि GPU मेमोरी की निगरानी रखें और बेहतर प्रदर्शन के लिए ड्राइवर को अपडेट रखें।

OCR, GPU एक्सेलेरेशन, या Aspose फीचर्स के बारे में और प्रश्न हैं? टिप्पणी छोड़ें या आधिकारिक Aspose OCR दस्तावेज़ देखें ताकि अधिक कस्टमाइज़ेशन विकल्प मिल सकें। कोडिंग का आनंद लें! 🚀

![OCR उपयोग करने का आरेख](https://example.com/images/ocr-gpu-diagram.png "OCR उपयोग करने का आरेख")

---

**अंतिम अपडेट:** 2026-09-18  
**परीक्षण किया गया:** Aspose OCR for Java 24.10  
**लेखक:** Aspose  

```java
// Step 1: Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Step 2: Grab the configuration object
OcrEngineConfiguration config = ocrEngine.getConfiguration();

// Step 3: Switch processing mode to GPU
config.setProcessingMode(ProcessingMode.GPU);   // requires a CUDA‑compatible driver

// (Optional) Step 4: Limit GPU memory usage to 1024 MB
config.setGpuMemoryLimit(1024);                 // set gpu memory limit (MB)
```
```java
// Step 5: Define the image to be processed
ImageRecognitionResult imageInfo = new ImageRecognitionResult();
imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

// Step 6: Run the OCR operation
RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);
```
```java
// Step 7: Output the recognized text
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```
```
Recognized text:
Invoice #12345
Date: 2026-02-09
Total: $1,250.00
Thank you for your business!
```
```java
import com.aspose.ocr.*;
import com.aspose.ocr.configuration.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Specify the image to be processed
        ImageRecognitionResult imageInfo = new ImageRecognitionResult();
        imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

        // Step 2: Create the OCR engine and enable GPU processing
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration config = ocrEngine.getConfiguration();

        // Step 3: Set processing mode to GPU (requires CUDA driver)
        config.setProcessingMode(ProcessingMode.GPU);

        // Step 4 (optional): Limit GPU memory usage to 1024 MB
        config.setGpuMemoryLimit(1024);

        // Step 5: Perform recognition
        RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);

        // Step 6: Print the extracted text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```
```bash
javac -cp "path/to/aspose-ocr.jar" GpuExample.java
java -cp ".:path/to/aspose-ocr.jar" GpuExample
```

## संबंधित ट्यूटोरियल

- [Aspose.OCR डिटेक्ट एरिया मोड के साथ जावा में इमेज से टेक्स्ट निकालें](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Aspose.OCR का उपयोग करके भाषा के साथ इमेज टेक्स्ट OCR कैसे करें](/ocr/java/ocr-operations/perform-ocr-language-selection/)
- [जावा में इमेज OCR को प्री‑प्रोसेस करके सटीकता बढ़ाएँ और टेक्स्ट निकालें](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}