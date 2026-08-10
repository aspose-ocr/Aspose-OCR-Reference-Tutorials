---
category: general
date: 2026-02-14
description: Aspose OCR Java में GPU को सक्षम करके छवि से तेज़ी से टेक्स्ट निकालना
  कैसे करें। TIFF को टेक्स्ट में बदलना, GPU डिवाइस ID सेट करना, और TIFF फ़ाइलों से
  टेक्स्ट पढ़ना सीखें।
draft: false
keywords:
- how to enable gpu
- extract text from image
- convert tiff to text
- set gpu device id
- read text from tiff
language: hi
og_description: कैसे Aspose OCR Java में GPU सक्षम करके छवि से तेज़ी से टेक्स्ट निकाला
  जाए। इस गाइड का पालन करके TIFF को टेक्स्ट में बदलें, GPU डिवाइस आईडी सेट करें, और
  TIFF से टेक्स्ट पढ़ें।
og_title: GPU को OCR के लिए कैसे सक्षम करें – TIFF से टेक्स्ट निकालें
tags:
- OCR
- Java
- GPU acceleration
title: GPU को OCR के लिए कैसे सक्षम करें और TIFF से टेक्स्ट निकालें
url: /hi/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-and-extract-text-from-tiff/
---

"# GPU को OCR के लिए सक्षम करना और TIFF से टेक्स्ट निकालना". Keep same heading level.

Paragraph: "Ever wondered **how to enable GPU** when performing OCR on large TIFF files? ..." translate.

Will keep bold formatting.

Proceed.

Make sure to keep markdown links unchanged (none present). Code block placeholders remain.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GPU को OCR के लिए सक्षम करना और TIFF से टेक्स्ट निकालना

क्या आपने कभी बड़े TIFF फ़ाइलों पर OCR करते समय **GPU को कैसे सक्षम किया जाए** के बारे में सोचा है? आप अकेले नहीं हैं—डेवलपर्स लगातार अतिरिक्त गति की तलाश में रहते हैं, ख़ासकर जब स्रोत इमेज कई मेगाबाइट्स वाला TIFF हो। अच्छी ख़बर? Aspose OCR for Java के साथ आप एक स्विच फ़्लिप कर सकते हैं, सही GPU को पॉइंट कर सकते हैं, और इंजन को इमेज के माध्यम से दौड़ते देख सकते हैं।

इस ट्यूटोरियल में हम पूरी वर्कफ़्लो को कवर करेंगे: TIFF लोड करना, GPU एक्सेलेरेशन को ऑन करना, वैकल्पिक रूप से एक विशेष GPU डिवाइस चुनना, OCR चलाना, और अंत में **इमेज से टेक्स्ट निकालना**। अंत तक आप कुछ लाइनों के कोड से **TIFF को टेक्स्ट में बदलना** सीख जाएंगे, और यह भी देखेंगे कि **TIFF फ़ाइलों से टेक्स्ट कैसे पढ़ें** किसी भी सपोर्टेड प्लेटफ़ॉर्म पर।

## आपको क्या चाहिए

- Java 17 या नया (कोड Java 8+ के साथ भी काम करता है)
- Aspose OCR for Java 23.10 (या लिखते समय उपलब्ध नवीनतम संस्करण)
- नवीनतम ड्राइवर के साथ CUDA‑संगत GPU
- एक सैंपल मल्टी‑पेज TIFF (हम इसे `sample_large.tif` कहेंगे)

कोई Maven जादू नहीं? कोई समस्या नहीं—बस JAR को अपने क्लासपाथ में डालें और आप तैयार हैं।

![GPU को सक्षम करने का ट्यूटोरियल](gpu-ocr.png)

*Image alt text: Java में OCR के लिए GPU को सक्षम करने का ट्यूटोरियल*

## चरण 1: OCR के लिए TIFF इमेज लोड करें

सबसे पहले आपको एक `OcrEngine` इंस्टेंस और एक स्रोत इमेज चाहिए। Aspose OCR लगभग सभी रास्टर फ़ॉर्मेट पढ़ सकता है, लेकिन स्कैन किए गए दस्तावेज़ों के लिए TIFF आम है।

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the TIFF file – this is where we "read text from TIFF"
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample_large.tif"));
```

> **क्यों महत्वपूर्ण है:** `setImage` कॉल फ़ाइल को `ImageStream` में रैप करता है, जिससे इंजन मल्टी‑पेज TIFF को मैन्युअल रूप से विभाजित किए बिना संभाल सकता है। यदि फ़ाइल नहीं मिलती, तो आपको स्पष्ट `FileNotFoundException` मिलेगा—इसलिए पाथ दोबारा जांचें।

## चरण 2: GPU एक्सेलेरेशन सक्षम करें

अब जादू शुरू होता है। GPU को ऑन करना सिर्फ एक बूलियन फ़्लैग है, लेकिन यह प्रोसेसिंग टाइम को सेकंड या यहाँ तक कि मिनटों तक घटा सकता है।

```java
        // Enable GPU acceleration (requires a supported driver)
        ocrEngine.getEngineOptions().setUseGpu(true);
```

> **प्रो टिप:** यदि आपके मशीन में कई GPUs हैं, तो डिफ़ॉल्ट रूप से आमतौर पर पहला (डिवाइस 0) चुना जाता है। आप Aspose को स्वचालित रूप से सबसे अच्छा डिवाइस चुनने दे सकते हैं, लेकिन इसे स्पष्ट रूप से सेट करने से मल्टी‑GPU वर्कस्टेशन पर आश्चर्य कम होते हैं।

## चरण 3: GPU डिवाइस ID सेट करें (वैकल्पिक)

कभी‑कभी आपको पता होता है कि कौन सा GPU उपयोग करना है—शायद दूसरा कार्ड AI वर्कलोड के लिए समर्पित है। यही वह जगह है जहाँ `setGpuDeviceId` काम आता है।

```java
        // Optional: select the GPU device (0 = first device, 1 = second, etc.)
        ocrEngine.getEngineOptions().setGpuDeviceId(0);
```

> **एज केस:** यदि आप एक अमान्य ID पास करते हैं, तो इंजन `IllegalArgumentException` फेंकेगा। एक त्वरित `System.out.println(ocrEngine.getEngineOptions().getAvailableGpuDevices())` आपके लिए उपलब्ध IDs की सूची दिखा सकता है।

## चरण 4: इमेज प्रोसेस करें और **इमेज से टेक्स्ट निकालें**

इंजन कॉन्फ़िगर हो जाने के बाद, OCR चलाने का समय है। परिणाम ऑब्जेक्ट आपको कच्चा स्ट्रिंग देता है, साथ ही यदि चाहें तो कॉन्फिडेंस स्कोर भी।

```java
        // Perform OCR – this is where we "convert TIFF to text"
        OcrResult ocrResult = ocrEngine.process();

        // Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

### अपेक्षित आउटपुट

यदि TIFF में वाक्य “Hello, World!” है, तो आपको कुछ इस तरह दिखना चाहिए:

```
Recognized text:
Hello, World!
```

इंजन लाइन ब्रेक, विराम चिह्न, और बुनियादी लेआउट डिटेक्शन को संभालता है। अधिक ग्रैन्युलर कंट्रोल (जैसे पेज‑वाइज़ टेक्स्ट निकालना) के लिए `ocrResult.getPages()` देखें।

## चरण 5: आउटपुट सत्यापित करें और सामान्य समस्याओं को संभालें

### GPU क्यों उपयोग नहीं हो रहा हो सकता है?

- **ड्राइवर असंगति:** GPU ड्राइवर Aspose द्वारा सुझाए गए न्यूनतम संस्करण से कम नहीं होना चाहिए (रिलीज़ नोट्स देखें)।
- **अपर्याप्त मेमोरी:** बहुत बड़ी इमेजेज GPU VRAM से अधिक हो सकती हैं। ऐसे में इंजन स्वचालित रूप से CPU पर फ़ॉल बैक हो जाता है—कंसोल में एक वार्निंग देखें।
- **असमर्थित हार्डवेयर:** इंटीग्रेटेड ग्राफिक्स अक्सर आवश्यक कंप्यूट कैपेबिलिटी नहीं रखते।

### प्रोग्रामेटिक रूप से CPU पर फ़ॉल बैक करना

```java
if (!ocrEngine.getEngineOptions().isGpuAvailable()) {
    System.out.println("GPU not available – switching to CPU.");
    ocrEngine.getEngineOptions().setUseGpu(false);
}
```

### लूप में TIFF से टेक्स्ट पढ़ना

यदि आपके पास TIFF फ़ाइलों से भरा फ़ोल्डर है, तो आप इस तरह इटररेट कर सकते हैं:

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".tif"))) {
    ocrEngine.setImage(ImageStream.fromFile(file.getAbsolutePath()));
    OcrResult result = ocrEngine.process();
    System.out.println("File: " + file.getName());
    System.out.println(result.getText());
}
```

यह स्निपेट दिखाता है कि **TIFF फ़ाइलों से टेक्स्ट पढ़ना** बैच में कैसे किया जाए, जबकि अभी भी GPU एक्सेलेरेशन का लाभ मिल रहा हो।

## अक्सर पूछे जाने वाले प्रश्न (FAQ)

**प्रश्न: क्या यह Linux पर काम करता है?**  
उत्तर: बिल्कुल—Aspose OCR क्रॉस‑प्लेटफ़ॉर्म है। बस सुनिश्चित करें कि CUDA टूलकिट और ड्राइवर इंस्टॉल हों।

**प्रश्न: अगर मेरे पास GPU नहीं है तो क्या करें?**  
उत्तर: `setUseGpu(false)` सेट करें या कॉल को ही छोड़ दें। इंजन डिफ़ॉल्ट रूप से CPU उपयोग करेगा।

**प्रश्न: क्या मैं अन्य फ़ॉर्मेट से भी टेक्स्ट निकाल सकता हूँ?**  
उत्तर: हाँ, वही `setImage` मेथड JPEG, PNG, BMP, और यहाँ तक कि PDF स्ट्रीम को भी स्वीकार करता है।

**प्रश्न: कम‑रिज़ॉल्यूशन TIFF पर OCR की सटीकता कितनी है?**  
उत्तर: 300 dpi से नीचे सटीकता घटती है। इंजन को फीड करने से पहले इमेज को बाइनराइज़ेशन, डेस्क्यू जैसे प्री‑प्रोसेसिंग करें।

## निष्कर्ष

अब आप जानते हैं **GPU को कैसे सक्षम करें** Aspose OCR Java में, **GPU डिवाइस ID कैसे सेट करें**, और सबसे महत्वपूर्ण, **इमेज फ़ाइलों से टेक्स्ट कैसे निकालें**, विशेष रूप से **TIFF को टेक्स्ट में बदलना** और **TIFF से टेक्स्ट पढ़ना** प्रभावी ढंग से। एक फ़्लैग टॉगल करके और वैकल्पिक रूप से डिवाइस चुनकर आप बिना किसी OCR लॉजिक को बदले बड़े प्रदर्शन लाभ प्राप्त कर सकते हैं।

अगला कदम तैयार है? इन पर प्रयोग करें:

- **सैकड़ों TIFFs की बैच प्रोसेसिंग** समानांतर थ्रेड्स में।
- **कस्टम लैंग्वेज पैक्स** ताकि विशेष दस्तावेज़ों पर पहचान बेहतर हो।
- **एक्सट्रैक्टेड स्ट्रिंग पर पोस्ट‑प्रोसेसिंग** रेगेक्स के साथ फ़ॉर्मेटिंग साफ़ करने के लिए।

यदि कोई समस्या आती है तो टिप्पणी छोड़ें, और कोडिंग का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}