---
category: general
date: 2026-04-29
description: Aspose OCR स्ट्रीमिंग मोड का उपयोग करके TIFF फ़ाइलों को OCR करना सीखें।
  यह गाइड आपको टाइल्ड TIFF छवियों से टेक्स्ट टाइल्स को कुशलतापूर्वक निकालने का तरीका
  दिखाता है।
draft: false
keywords:
- how to ocr tiff
- extract text tiles
language: hi
og_description: Aspose OCR स्ट्रीमिंग का उपयोग करके TIFF को OCR कैसे करें। बड़े TIFF
  छवियों से पाठ टाइल्स निकालने के लिए चरण‑दर‑चरण कोड।
og_title: tiff को OCR कैसे करें – पूर्ण स्ट्रीमिंग गाइड
tags:
- OCR
- Java
- Aspose
- TIFF
title: TIFF को OCR कैसे करें – बड़े TIFF फ़ाइलों को स्ट्रीम करें और जावा में टेक्स्ट
  टाइल्स निकालें
url: /hi/java/advanced-ocr-techniques/how-to-ocr-tiff-stream-large-tiffs-and-extract-text-tiles-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to ocr tiff – बड़े TIFFs को स्ट्रीम करें और जावा में टेक्स्ट टाइल्स निकालें

क्या आपने कभी सोचा है कि **how to ocr tiff** फ़ाइलों को जो एक बार में मेमोरी में लोड करने के लिए बहुत बड़ी हैं, कैसे प्रोसेस किया जाए? आप अकेले नहीं हैं। कई डेवलपर्स को तब समस्या आती है जब उनके TIFF इमेज कई टाइल्स में विभाजित होते हैं, और सामान्य `ocrEngine.recognize()` कॉल बस फेल हो जाता है।  

अच्छी खबर? Aspose OCR का स्ट्रीमिंग मोड आपको प्रत्येक टाइल को अलग स्ट्रीम के रूप में फीड करने देता है, जिससे आप **extract text tiles** बिना हीप को ब्लो किए निकाल सकते हैं। इस ट्यूटोरियल में हम एक पूरी, रन‑टू‑रन जावा उदाहरण के माध्यम से चलेंगे, समझाएंगे कि हर लाइन क्यों महत्वपूर्ण है, और उन pitfalls को दिखाएंगे जिन्हें आपको बचना चाहिए।

> **What you’ll get:** एक runnable प्रोग्राम जो टाइल्ड TIFFs को ऑन‑द‑फ्लाई जोड़ता है, संयुक्त टेक्स्ट प्रिंट करता है, और दिखाता है कि कोड को अन्य भाषाओं या इमेज फ़ॉर्मैट्स के लिए कैसे अनुकूलित किया जाए।

---

## Prerequisites

- **Java 17** या उससे नया (कोड try‑with‑resources का उपयोग करता है, इसलिए JDK 8+ काम करता है, लेकिन JDK 17 वर्तमान LTS है)।
- **Aspose.OCR for Java** लाइब्रेरी (v23.10 या बाद का)। इसे Maven के माध्यम से जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- एक फ़ोल्डर जिसमें व्यक्तिगत TIFF टाइल्स हों (उदा., `tile_0.tif`, `tile_1.tif`, …)।  
- वैकल्पिक: IntelliJ IDEA या VS Code जैसा IDE – लेकिन एक साधारण टेक्स्ट एडिटर भी ठीक काम करेगा।

---

## Step 1 – Prepare the Tile Paths (Why It Matters)

OCR इंजन को कुछ भी करने से पहले यह जानना जरूरी है कि प्रत्येक इमेज पीस कहाँ स्थित है। डेमो के लिए पाथ हार्ड‑कोड करना ठीक है, लेकिन प्रोडक्शन में आप संभवतः किसी डायरेक्टरी को स्कैन करेंगे या मैनिफेस्ट फ़ाइल पढ़ेंगे।

```java
// Define the absolute or relative paths to each TIFF tile
String[] tilePaths = {
    "YOUR_DIRECTORY/tile_0.tif",
    "YOUR_DIRECTORY/tile_1.tif",
    "YOUR_DIRECTORY/tile_2.tif"
};
```

> **Pro tip:** टाइल्स को लेक्सिकल क्रम में रखें (0, 1, 2…) क्योंकि इंजन स्ट्रीम्स को उसी क्रम में फीड करने पर पहचानित टेक्स्ट को जोड़ता है।

---

## Step 2 – Enable Streaming Mode on the OCR Engine (Primary Keyword)

अब हम `OcrEngine` इंस्टेंस बनाते हैं और स्ट्रीमिंग को ऑन करते हैं। यही **how to ocr tiff** बिना पूरी इमेज को RAM में लोड किए करने का मुख्य तरीका है।

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Activate streaming – essential for large or tiled TIFFs
ocrEngine.getProcessingSettings().setEnableStreaming(true);

// Set the language to English; change as needed (e.g., "fr", "de")
ocrEngine.getLanguageSettings().setLanguage("en");
```

**Why streaming?**  
जब `setEnableStreaming(true)` कॉल किया जाता है, तो इंजन प्रत्येक आने वाले `ImageStream` को पिछले वाले की निरंतरता मानता है। यह एक आंतरिक वर्चुअल कैनवास बनाता है, टाइल्स को वर्चुअली जोड़ता है, और अंत में एक बार OCR चलाता है। इससे “OutOfMemoryError” से बचा जा सकता है, जो कि अगर आप एक मल्टी‑गिगाबाइट TIFF को एक साथ लोड करने की कोशिश करेंगे तो उत्पन्न होता।

---

## Step 3 – Append Each Tile as an Input Stream (Secondary Keyword)

यह लूप हर टाइल को इंजन में फीड करता है। `try‑with‑resources` ब्लॉक फाइल हैंडल को तुरंत बंद कर देता है, जो कि दर्जनों फ़ाइलों के साथ काम करते समय बहुत महत्वपूर्ण है।

```java
for (String tilePath : tilePaths) {
    try (InputStream stream = new FileInputStream(tilePath)) {
        // Wrap the raw InputStream in Aspose's ImageStream wrapper
        ocrEngine.appendImage(ImageStream.fromStream(stream));
    } catch (IOException e) {
        // If a single tile fails, we log and continue – you might want to abort instead
        System.err.println("Failed to load tile: " + tilePath);
        e.printStackTrace();
    }
}
```

ध्यान दें कि **extract text tiles** वाक्यांश स्वाभाविक रूप से एम्बेड है: प्रत्येक इटरेशन *एक टाइल से* टेक्स्ट निकालता है और बढ़ते हुए रिज़ल्ट सेट में जोड़ता है।

---

## Step 4 – Run Recognition and Output the Combined Text (Primary Keyword)

सभी टाइल्स को क्यू करने के बाद, एक ही कॉल वर्चुअल इमेज पर OCR चलाता है। परिणाम में पूरा टेक्स्ट होता है, जैसे कि आपके पास एक ही बड़ा TIFF हो।

```java
// Perform OCR on the combined virtual image
OcrResult ocrResult = ocrEngine.recognize();

// Print the extracted text to the console
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Expected output** (मान लीजिए टाइल्स में “Hello World” वाक्यांश विभाजित है):

```
=== OCR Output ===
Hello World
```

यदि आपकी टाइल्स में अधिक लाइन्स हैं, तो वे उसी क्रम में दिखेंगी जैसा आपने उन्हें फीड किया था। आप `ocrResult.getText()` को फ़ाइल में भी लिख सकते हैं आगे की प्रोसेसिंग के लिए।

---

## Step 5 – Full, Runnable Example (All Steps in One Place)

नीचे पूरा प्रोग्राम है जिसे आप `StreamingExample.java` में कॉपी‑पेस्ट कर सकते हैं। इसमें सभी इम्पोर्ट्स, कमेंट्स और एरर हैंडलिंग शामिल है।

```java
import com.aspose.ocr.*;
import java.io.*;

public class StreamingExample {
    public static void main(String[] args) throws Exception {
        // ------------------------------------------------------------
        // Step 1: List the TIFF tile files
        // ------------------------------------------------------------
        String[] tilePaths = {
            "YOUR_DIRECTORY/tile_0.tif",
            "YOUR_DIRECTORY/tile_1.tif",
            "YOUR_DIRECTORY/tile_2.tif"
        };

        // ------------------------------------------------------------
        // Step 2: Set up the OCR engine in streaming mode
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getProcessingSettings().setEnableStreaming(true);
        ocrEngine.getLanguageSettings().setLanguage("en");

        // ------------------------------------------------------------
        // Step 3: Feed each tile as a separate stream
        // ------------------------------------------------------------
        for (String tilePath : tilePaths) {
            try (InputStream stream = new FileInputStream(tilePath)) {
                ocrEngine.appendImage(ImageStream.fromStream(stream));
            } catch (IOException e) {
                System.err.println("Unable to read tile: " + tilePath);
                e.printStackTrace();
                // Optionally: return; // abort on missing tile
            }
        }

        // ------------------------------------------------------------
        // Step 4: Recognize the combined image and display the text
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

सेव करें, कंपाइल करें, और रन करें:

```bash
javac -cp "path/to/aspose-ocr.jar" StreamingExample.java
java -cp ".:path/to/aspose-ocr.jar" StreamingExample
```

आपको कंसोल में कंकैटेनेटेड OCR टेक्स्ट प्रिंट होते हुए दिखेगा।

---

## Advanced Tips & Common Pitfalls (Why This Works)

| Issue | Why It Happens | How to Fix / Optimize |
|-------|----------------|-----------------------|
| **Out‑of‑memory errors** | पूरी‑साइज़ TIFF को `BufferedImage` में लोड करने से पूरी हीप खपत हो जाती है। | स्ट्रीमिंग मोड (`setEnableStreaming(true)`) उपयोग करें – इंजन कभी भी पूरी इमेज को मैटेरियलाइज़ नहीं करता। |
| **Tile order mismatch** | फ़ाइलें अल्फ़ाबेटिकली सॉर्ट होती हैं बनाम न्यूमेरिक क्रम (उदा., `tile_10.tif` `tile_2.tif` से पहले)। | नंबरों को ज़ीरो‑पैड करें (`tile_00.tif`, `tile_01.tif`) या प्रोग्रामेटिकली `Comparator` से सॉर्ट करें। |
| **Wrong language** | OCR डिफ़ॉल्ट रूप से अंग्रेज़ी में है; गैर‑अंग्रेज़ी टेक्स्ट गड़बड़ हो जाता है। | `ocrEngine.getLanguageSettings().setLanguage("fr")` (या कोई भी सपोर्टेड ISO कोड) कॉल करें। |
| **Partial failures** | एक करप्ट टाइल पूरी प्रक्रिया को रोक देती है। | प्रत्येक टाइल के लिए `IOException` को कैच करें, लॉग करें, और तय करें कि जारी रखें या एबॉर्ट करें। |
| **Performance bottleneck** | कई छोटे फ़ाइलों को पढ़ते समय डिस्क I/O प्रमुख बन जाता है। | टाइल्स को ZIP में बंडल करें और मेमोरी से स्ट्रीम करें, या तेज़ SSD उपयोग करें। |

---

## When to Use Streaming vs. Single‑Image OCR

- **Streaming** आदर्श है:
  - मल्टी‑पेज TIFFs या गिगापिक्सेल स्कैन के लिए।
  - जब मेमोरी सीमित हो (उदा., Docker कंटेनर, मोबाइल डिवाइस)।
  - ऐसे पाइपलाइन में जहाँ पहले से ही इमेज चंक्स मिलते हैं (उदा., कैमरा फ़ीड)।

- **Single‑image OCR** ठीक है:
  - छोटे PNG/JPEG फ़ाइलों (< 5 MB) के लिए।
  - एक‑बार स्कैन जहाँ सरलता प्रदर्शन से अधिक महत्वपूर्ण हो।

---

## Conclusion

अब आपके पास **how to ocr tiff** फ़ाइलों को Aspose OCR की स्ट्रीमिंग क्षमताओं का उपयोग करके प्रोसेस करने की ठोस समझ है, और आप **extract text tiles** को प्रभावी ढंग से निकाल सकते हैं। पूरी सॉल्यूशन—इंजन को इनिशियलाइज़ करना, स्ट्रीमिंग ऑन करना, प्रत्येक टाइल को जोड़ना, और अंत में वर्चुअल कैनवास को पहचानना—आपको प्रोडक्शन‑रेडी कोड के लिए “क्या”, “क्यों” और “कैसे” प्रदान करता है।

अगला कदम? `"en"` को किसी अन्य भाषा से बदलें, या विभिन्न इमेज फ़ॉर्मैट्स (`.png`, `.jpg`) के साथ प्रयोग करें। आप OCR रिज़ल्ट को सीधे सर्च इंडेक्स या PDF जेनरेटर में भी फीड कर सकते हैं। पैटर्न वही रहता है: स्ट्रीम, स्टिच, रेकग्नाइज़।

सैकड़ों टाइल्स को स्केल करने या एरर हैंडलिंग में मदद चाहिए? नीचे कमेंट करें, और हैप्पी कोडिंग!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}