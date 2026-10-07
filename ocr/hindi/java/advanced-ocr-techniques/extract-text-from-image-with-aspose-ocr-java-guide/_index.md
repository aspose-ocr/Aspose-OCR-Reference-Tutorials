---
category: general
date: 2026-02-14
description: Aspose OCR का उपयोग करके जावा में छवि से टेक्स्ट निकालें। सटीक परिणामों
  के लिए रुचि के क्षेत्रों के साथ फ़ॉर्म फ़ील्ड्स से टेक्स्ट निकालना सीखें।
draft: false
keywords:
- extract text from image
- extract text from form
language: hi
og_description: Aspose OCR का उपयोग करके जावा में छवि से टेक्स्ट निकालें। यह ट्यूटोरियल
  दिखाता है कि कैसे फॉर्म फ़ील्ड्स से रुचि के क्षेत्रों के माध्यम से टेक्स्ट निकाला
  जाए।
og_title: Aspose OCR के साथ छवि से टेक्स्ट निकालें – जावा गाइड
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Aspose OCR के साथ छवि से पाठ निकालें – जावा गाइड
url: /hi/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज से टेक्स्ट निकालें Aspose OCR – Java गाइड

क्या आपको कभी **इमेज से टेक्स्ट निकालने** की ज़रूरत पड़ी है लेकिन पूरे चित्र को पार्स करने, CPU साइकिल बर्बाद करने और शोरयुक्त परिणाम मिलने पर थक गए हैं? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया के ऐप्स—जैसे इनवॉइस स्कैनर, पासपोर्ट रीडर, या डेटा‑एंट्री फ़ॉर्म—में आपको केवल कुछ फ़ील्ड्स की परवाह होती है, पूरे कैनवास की नहीं।  

अच्छी खबर यह है कि Aspose OCR आपको **इमेज से टेक्स्ट निकालने** *और* विशिष्ट फ़ॉर्म क्षेत्रों से बहुभुज (polygon) परिभाषित करके निकालने की सुविधा देता है। इस ट्यूटोरियल में आप देखेंगे कि Java का उपयोग करके **फ़ॉर्म से टेक्स्ट निकालना** कैसे किया जाता है, यह तरीका क्यों महत्वपूर्ण है, और जब चीज़ें उलट‑पुलट हों तो क्या समायोजित करना चाहिए।  

नीचे हम लाइब्रेरी सेटअप से लेकर जटिल एज केसों को संभालने तक सब कुछ कवर करेंगे, ताकि अंत तक आपके पास एक तैयार‑चलाने‑योग्य स्निपेट हो जो केवल आवश्यक डेटा को निकालता है।

## आपको क्या चाहिए

- Java 17 (या कोई भी नया JDK) – नए संस्करणों में बेहतर Unicode समर्थन होता है।  
- Aspose.OCR for Java 23.10 (या पढ़ने के समय उपलब्ध नवीनतम संस्करण)।  
- `form.png` नाम की एक सैंपल इमेज जिसमें स्पष्ट रूप से परिभाषित फ़ील्ड्स हों।  
- एक IDE या साधा टेक्स्ट एडिटर—IntelliJ IDEA, VS Code, या यहाँ तक कि Notepad भी चलेगा।  

कोर डेमो के लिए कोई Maven/Gradle जादू नहीं चाहिए; बस Aspose OCR JAR को अपने क्लासपाथ में जोड़ें.

---

## चरण 1 – OCR इंजन को इनिशियलाइज़ करें और अपनी इमेज लोड करें

इंजन को सबसे पहले एक बिटमैप चाहिए जिस पर वह काम कर सके। हम इसे `form.png` की ओर इंगित करेंगे, जो स्रोत फ़ाइल के समान फ़ोल्डर में स्थित है.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the source image – replace the path if your file lives elsewhere
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));
```

*यह क्यों महत्वपूर्ण है:*  
एक नया `OcrEngine` बनाना आपको एक साफ़ शुरुआत देता है, जिससे कोई भी बचा हुआ सेटिंग आपके रन को प्रभावित नहीं करता। इमेज को पहले लोड करने से यह भी सत्यापित होता है कि फ़ाइल मौजूद है, इसलिए बाद में समय बर्बाद करने से पहले आपको एक उपयोगी एक्सेप्शन मिल जाता है।

> **Pro tip:** यदि आपकी इमेज बहुत बड़ी है (5 MB से अधिक), तो पहले उसका आकार बदलने पर विचार करें। Aspose OCR उन इमेजों पर तेज़ काम करता है जिनकी किसी भी दिशा में 2000 px से कम हो।

---

## चरण 2 – उन फ़ील्ड्स के लिए बहुभुज (Polygons) परिभाषित करें जिन्हें आप पढ़ना चाहते हैं

एक *Region of Interest* (ROI) बस एक बहुभुज है जो इंजन को बताता है कि कहाँ देखना है। नीचे हम दो आयत बनाते हैं—एक “First Name” के लिए और दूसरा “Date of Birth” के लिए। अपने फ़ॉर्म के अनुसार निर्देशांक समायोजित करें.

```java
        // Polygon for the first field (e.g., First Name)
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},   // X‑coordinates
                new int[]{100, 100, 150, 150}, // Y‑coordinates
                4);

        // Polygon for the second field (e.g., Date of Birth)
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);
```

*आयतों के बजाय बहुभुज क्यों?*  
बहुभुज आपको विकृत या गैर‑आयताकार बॉक्स को संभालने की लचीलापन देते हैं—जो प्रिंटेड फ़ॉर्म को स्कैन करते समय आम है जब वे पूरी तरह से संरेखित नहीं होते।

---

## चरण 3 – Aspose OCR को केवल उन क्षेत्रों पर फोकस करने को कहें

अब हम बहुभुजों को इंजन से बाइंड करते हैं। `setRegionsOfInterest` मेथड एक सूची स्वीकार करता है, इसलिए आप जितने चाहें फ़ील्ड्स जोड़ सकते हैं.

```java
        // Limit OCR to the defined regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));
```

*आंतरिक रूप से क्या होता है?*  
Aspose OCR प्रत्येक बहुभुज को एक अलग बिटमैप में क्रॉप करता है, उसकी पहचान एल्गोरिद्म चलाता है, और फिर परिणामों को जोड़ता है। यह आसपास के ग्राफ़िक्स से होने वाले फॉल्स पॉज़िटिव को काफी घटा देता है।

---

## चरण 4 – OCR प्रक्रिया चलाएँ

सब कुछ कॉन्फ़िगर हो जाने पर, हम OCR को शुरू करते हैं। `process()` कॉल एक `OcrResult` ऑब्जेक्ट लौटाता है जिसमें निकाला गया टेक्स्ट और कॉन्फिडेंस स्कोर होते हैं.

```java
        // Execute OCR on the selected ROIs
        OcrResult ocrResult = ocrEngine.process();
```

यदि आपको प्रति‑फ़ील्ड कॉन्फिडेंस चाहिए, तो आप `ocrResult.getRegions()` देख सकते हैं—प्रत्येक क्षेत्र अपना स्कोर रखता है। अधिकांश सरल फ़ॉर्मों के लिए, कुल मिलाकर टेक्स्ट पर्याप्त है।

---

## चरण 5 – निकाले गए टेक्स्ट को प्रदर्शित (या स्टोर) करें

अंत में, हम परिणाम को कंसोल पर प्रिंट करते हैं। वास्तविक एप्लिकेशन में आप इसे डेटाबेस, JSON फ़ाइल में लिख सकते हैं, या API के माध्यम से भेज सकते हैं.

```java
        // Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**अपेक्षित आउटपुट (उदाहरण):**

```
=== Extracted Text ===
John Doe
12/04/1990
```

दोनों पंक्तियाँ उन दो बहुभुजों से मेल खाती हैं जिन्हें हमने परिभाषित किया था। यदि आपको अतिरिक्त व्हाइटस्पेस दिखे, तो उसे `String.trim()` से ट्रिम करें।

---

## कई फ़ील्ड्स वाले फ़ॉर्म से टेक्स्ट निकालने का तरीका

जब फ़ॉर्म में दर्जनों इनपुट होते हैं, तो मैन्युअल रूप से कोऑर्डिनेट टाइप करना थकाऊ हो जाता है। यहाँ एक तेज़ पैटर्न है जिसे आप अपना सकते हैं:

1. **एक CSV बनाएं** जिसमें प्रत्येक पंक्ति `fieldName, x1, y1, x2, y2, x3, y3, x4, y4` रखती हो।  
2. **रनटाइम पर CSV लोड करें**, प्रत्येक लाइन पर लूप करें, एक `Polygon` बनाएं, और उसे ROI सूची में जोड़ें।  

```java
List<Polygon> rois = new ArrayList<>();
try (BufferedReader br = new BufferedReader(new FileReader("fields.csv"))) {
    String line;
    while ((line = br.readLine()) != null) {
        String[] parts = line.split(",");
        int[] xs = { Integer.parseInt(parts[1]), Integer.parseInt(parts[3]),
                    Integer.parseInt(parts[5]), Integer.parseInt(parts[7]) };
        int[] ys = { Integer.parseInt(parts[2]), Integer.parseInt(parts[4]),
                    Integer.parseInt(parts[6]), Integer.parseInt(parts[8]) };
        rois.add(new Polygon(xs, ys, 4));
    }
}
ocrEngine.getEngineOptions().setRegionsOfInterest(rois);
```

*क्यों bother?*  
ROI जेनरेशन को ऑटोमेट करने से आप एक ही Java कोड को कई फ़ॉर्म लेआउट्स में पुन: उपयोग कर सकते हैं, जिससे आपका प्रोजेक्ट DRY (Don’t Repeat Yourself) रहता है।

---

## एज केस और टिप्स जिनके बारे में आप नहीं सोच सकते

- **Rotated scans:** यदि पूरी इमेज घुमी हुई है, तो `ocrEngine.getEngineOptions().setRotateAngle(degrees)` कॉल करें।  
- **Low contrast:** पढ़ने योग्यता बढ़ाने के लिए `ocrEngine.getEngineOptions().setContrast(1.5f)` सेट करें।  
- **Non‑Latin scripts:** भाषा बदलने के लिए `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.Spanish)` (या कोई भी समर्थित भाषा) का उपयोग करें।  
- **Partial OCR failures:** हमेशा `ocrResult.getConfidence()` जांचें; यदि यह 80 % से नीचे गिरता है, तो उपयोगकर्ता को मैन्युअल वेरिफिकेशन के लिए प्रॉम्प्ट करने पर विचार करें।  

---

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा प्रोग्राम है, जिसे कंपाइल और रन करने के लिए तैयार है। `YOUR_DIRECTORY` को उस फ़ोल्डर से बदलें जहाँ `form.png` स्थित है.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Step 1 – Initialize engine and load image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));

        // Step 2 – Define polygons for each form field
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},
                new int[]{100, 100, 150, 150},
                4);
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);

        // Step 3 – Limit OCR to those regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));

        // Step 4 – Run OCR
        OcrResult ocrResult = ocrEngine.process();

        // Step 5 – Show the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

कम्पाइल करें:

```bash
javac -cp "aspose-ocr-23.10.jar" MultiRoiDemo.java
java -cp ".:aspose-ocr-23.10.jar" MultiRoiDemo
```

आपको दो पंक्तियों का टेक्स्ट दिखना चाहिए जो परिभाषित ROI से संबंधित हैं।

---

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या यह PDFs के साथ काम करता है?**  
A: सीधे नहीं। प्रत्येक PDF पेज को पहले इमेज में बदलें (जैसे, Aspose PDF का उपयोग करके) और फिर इमेज को OCR इंजन में फीड करें।

**Q: अगर मेरे फ़ॉर्म में चेकबॉक्स हैं तो?**  
A: OCR बूलियन स्टेट्स नहीं पढ़ सकता, लेकिन आप चेकबॉक्स क्षेत्र को ROI के रूप में ले सकते हैं और पिक्सेल डेंसिटी जांच कर टिक का अनुमान लगा सकते हैं।

**Q: क्या मैं मल्टी‑पेज फ़ॉर्म से एक बार में टेक्स्ट निकाल सकता हूँ?**  
A: प्रत्येक पेज इमेज पर लूप करें, वही ROI सूची पुन: उपयोग करें, और परिणामों को जोड़ें।

---

## निष्कर्ष

हमने Aspose OCR का उपयोग करके **इमेज से टेक्स्ट निकालने** के लिए एक पूर्ण, एंड‑टू‑एंड समाधान को चरण‑दर‑चरण देखा, और दिखाया कि वही तकनीक आपको **फ़ॉर्म से टेक्स्ट निकालने** में सटीकता के साथ मदद करती है। बहुभुज परिभाषित करके, इंजन के फोकस को सीमित करके, और सामान्य समस्याओं को संभालकर, आप पूरे चित्र को प्रोसेस किए बिना तेज़, साफ़ डेटा प्राप्त करते हैं।  

अगले कदम के लिए तैयार हैं? इस OCR आउटपुट को JSON पेलोड में जोड़ने की कोशिश करें, या वैलिडेशन के लिए इसे मशीन‑लर्निंग मॉडल में फीड करें। संभावनाएँ असीमित हैं, और अब आप 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}