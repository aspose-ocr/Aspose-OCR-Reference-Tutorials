---
category: general
date: 2026-10-11
description: जावा में PNG इमेज पर OCR कैसे करें, इमेज से टेक्स्ट निकालें और एक सरल
  OcrEngine उदाहरण के साथ इमेज को टेक्स्ट में बदलना सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: hi
lastmod: 2026-10-11
og_description: जावा में PNG इमेज पर OCR कैसे करें, इमेज से टेक्स्ट निकालें और एक
  संक्षिप्त, तैयार‑चलाने योग्य उदाहरण का उपयोग करके इमेज को टेक्स्ट में बदलें।
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: जावा में PNG इमेज पर OCR कैसे करें – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  headline: How to perform OCR on a PNG image in Java
  type: TechArticle
- description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  name: How to perform OCR on a PNG image in Java
  steps:
  - name: 4.1 Handling low‑resolution PNGs
    text: 'Tesseract performs best on images with at least 300 DPI. If your source
      PNG is smaller, upscale it before OCR:'
  - name: 4.2 Extracting non‑English text
    text: 'To **extract text from image** that contains other languages, download
      the appropriate `.traineddata` files and set the language code:'
  - name: 4.3 Batch processing multiple PNGs
    text: 'If you need to **recognize text from PNG** files in a folder, iterate over
      the directory:'
  - name: 4.4 Dealing with OCR errors
    text: 'Typical OCR mistakes include misreading `0` (zero) as `O` or `1` as `l`.
      Post‑processing with regular expressions can clean the result:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Text Extraction
title: जावा में PNG इमेज पर OCR कैसे करें
url: /hi/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java में PNG इमेज पर OCR कैसे करें

यदि आपको किसी इमेज फ़ाइल पर **perform OCR** करने की आवश्यकता है, तो Java में **how to perform OCR** सीखना कई ऑटोमेशन कार्यों के लिए आवश्यक है। चाहे आप रसीदों को डिजिटाइज़ कर रहे हों, स्कैन किए गए दस्तावेज़ों को इंडेक्स कर रहे हों, या एक सर्चेबल फोटो आर्काइव बना रहे हों, **extract text from image** फ़ाइलों से टेक्स्ट निकालने की क्षमता अनगिनत मैनुअल घंटे बचाती है।

यह ट्यूटोरियल आपको एक पूर्ण, चलाने योग्य समाधान दिखाता है जो PNG लोड करता है, OCR इंजन चलाता है, और **recognize text from PNG** फ़ाइलों को पढ़ता है। आप यह भी देखेंगे कि **convert image to text** कैसे किया जाता है और सामान्य समस्याओं जैसे कम‑रिज़ॉल्यूशन इनपुट या गैर‑ASCII अक्षरों को कैसे संभाला जाए।

## आप क्या हासिल करेंगे

* **load image java** कोड जो डिस्क से PNG पढ़ता है,
* एक हल्का OCR इंजन इनिशियलाइज़ करें,
* **extract text from image** और परिणाम को कंसोल पर प्रिंट करें,
* समाधान को अन्य इमेज फ़ॉर्मैट्स या बैच प्रोसेसिंग के लिए अनुकूलित करें।

कोई बाहरी सेवाएँ आवश्यक नहीं हैं—केवल एक एकल ओपन‑सोर्स OCR लाइब्रेरी (Tess4J) और Java SE रनटाइम।

---

## आवश्यकताएँ

* Java 17 या नया (कोड JDK 17 के साथ कंपाइल होता है)।
* डिपेंडेंसी मैनेजमेंट के लिए Maven या Gradle।
* कमांड लाइन और अपनी पसंद के IDE की बुनियादी जानकारी।
* `tess4j` लाइब्रेरी (Tesseract के लिए Java रैपर)। निम्नलिखित Maven डिपेंडेंसी जोड़ें:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

यदि आप Gradle का उपयोग करते हैं, तो समकक्ष है:

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

आपको Tesseract डेटा फ़ाइलें (`.traineddata`) भी चाहिए। आधिकारिक रिपॉज़िटरी से अंग्रेज़ी डेटा पैक डाउनलोड करें और इसे प्रोजेक्ट रूट में `tessdata` नामक फ़ोल्डर में रखें।

## चरण 1: Java में इमेज लोड करें

स्टैंडर्ड `ImageIO` क्लास के साथ PNG लोड करना सरल है। नीचे दिया गया कोड **load image java** को एक सुरक्षित, एक्सेप्शन‑अवेयर तरीके से दर्शाता है:

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Reads a PNG file from the given path and returns a BufferedImage.
 *
 * @param path absolute or relative path to the PNG file
 * @return BufferedImage representation of the file
 * @throws Exception if the file cannot be read or is not a PNG
 */
private static BufferedImage loadPng(String path) throws Exception {
    File imgFile = new File(path);
    if (!imgFile.exists()) {
        throw new IllegalArgumentException("File not found: " + path);
    }
    BufferedImage img = ImageIO.read(imgFile);
    if (img == null) {
        throw new IllegalArgumentException("Unsupported image format or corrupt file: " + path);
    }
    return img;
}
```

**Why this matters:** `ImageIO.read` स्वचालित रूप से इमेज फ़ॉर्मैट का पता लगाता है, लेकिन हम स्पष्ट रूप से `null` की जाँच करते हैं ताकि PNG के भ्रष्ट होने पर चुपचाप विफलता से बचा जा सके। यह पैटर्न OCR के लिए **load image java** करते समय एक सर्वोत्तम प्रैक्टिस है।

## चरण 2: OCR इंजन को इनिशियलाइज़ करें

Tess4J नेटिव Tesseract बाइनरी को रैप करता है, एक सरल Java API प्रदान करता है। निम्नलिखित मेथड एक `Tesseract` इंस्टेंस बनाता है, इसे `tessdata` फ़ोल्डर की ओर इंगित करता है, और भाषा को अंग्रेज़ी पर सेट करता है:

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;

/**
 * Configures and returns a ready‑to‑use Tesseract instance.
 *
 * @return configured ITesseract object
 */
private static ITesseract createOcrEngine() {
    ITesseract tesseract = new Tesseract();
    // Path to the folder that contains .traineddata files
    tesseract.setDatapath("tessdata");
    // Language code – "eng" for English; you can add more languages later
    tesseract.setLanguage("eng");
    // Optional: increase OCR accuracy for PNGs with low DPI
    tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
    return tesseract;
}
```

**Why we do this:** इंजन को एक बार इनिशियलाइज़ करके कई इमेज के लिए पुन: उपयोग करने से स्टार्टअप ओवरहेड कम होता है। `setOcrEngineMode` कॉल डिफ़ॉल्ट मोड चुनती है, जो अधिकांश PNG के लिए अच्छा काम करता है। यदि आप शोरयुक्त स्कैन का सामना करते हैं, तो आप अन्य मोड्स (जैसे `OEM_LSTM_ONLY`) के साथ प्रयोग कर सकते हैं।

## चरण 3: OCR करें और **recognize text from PNG**

अब हम इमेज लोडर और OCR इंजन को मिलाते हैं। नीचे दिया गया मेथड `BufferedImage` पर OCR चलाता है और निकाली गई स्ट्रिंग लौटाता है:

```java
/**
 * Runs OCR on the supplied image and returns the recognized text.
 *
 * @param image BufferedImage containing the PNG to process
 * @param tesseract configured OCR engine
 * @return plain‑text result of OCR
 * @throws Exception if OCR fails
 */
private static String extractText(BufferedImage image, ITesseract tesseract) throws Exception {
    // Tess4J can directly accept a BufferedImage
    return tesseract.doOCR(image);
}
```

**पूरा चलाने योग्य उदाहरण**

```java
import java.awt.image.BufferedImage;
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.TesseractException;

public class OcrDemo {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the PNG file
            BufferedImage image = loadPng("sample.png");

            // 2️⃣ Create and configure the OCR engine
            ITesseract ocrEngine = createOcrEngine();

            // 3️⃣ Recognize text from PNG
            String recognizedText = extractText(image, ocrEngine);

            // 4️⃣ Display the result – this is the **convert image to text** step
            System.out.println("=== OCR RESULT ===");
            System.out.println(recognizedText);
        } catch (Exception e) {
            System.err.println("Error during OCR processing:");
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps -----
    // loadPng, createOcrEngine, extractText (copy-pasted here for completeness)
    // ... (methods omitted for brevity; see the sections above) ...
}
```

**अपेक्षित आउटपुट**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

कंसोल `sample.png` से इंजन द्वारा निकाले गए सटीक अक्षर दिखाएगा। यदि PNG में केवल एक शब्द है, तो आउटपुट वह शब्द होगा जिसके बाद एक नई लाइन आएगी।

## चरण 4: सामान्य विविधताएँ और किनारे के केस

### 4.1 कम‑रिज़ॉल्यूशन PNG को संभालना

Tesseract कम से कम 300 DPI वाली इमेज पर सबसे अच्छा काम करता है। यदि आपका स्रोत PNG छोटा है, तो OCR से पहले इसे अपस्केल करें:

```java
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.RenderingHints;

private static BufferedImage upscale(BufferedImage src, int scaleFactor) {
    int width = src.getWidth() * scaleFactor;
    int height = src.getHeight() * scaleFactor;
    Image tmp = src.getScaledInstance(width, height, Image.SCALE_SMOOTH);
    BufferedImage resized = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
    Graphics2D g2d = resized.createGraphics();
    g2d.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                         RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g2d.drawImage(tmp, 0, 0, null);
    g2d.dispose();
    return resized;
}
```

`extractText` को कॉल करने से पहले `upscale(image, 2)` लागू करें ताकि सटीकता बढ़े।

### 4.2 गैर‑अंग्रेज़ी टेक्स्ट निकालना

अन्य भाषाओं वाले इमेज से **extract text from image** करने के लिए, उपयुक्त `.traineddata` फ़ाइलें डाउनलोड करें और भाषा कोड सेट करें:

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 कई PNGs की बैच प्रोसेसिंग

यदि आपको फ़ोल्डर में **recognize text from PNG** फ़ाइलों को प्रोसेस करना है, तो डायरेक्टरी पर इटररेट करें:

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 OCR त्रुटियों से निपटना

आम OCR गलतियों में `0` (शून्य) को `O` या `1` को `l` पढ़ना शामिल है। रेगुलर एक्सप्रेशन्स के साथ पोस्ट‑प्रोसेसिंग परिणाम को साफ़ कर सकती है:

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

## Java में विश्वसनीय OCR के लिए प्रो टिप्स

| टिप | कारण |
|-----|--------|
| **Lossless PNG का उपयोग करें** | JPEG में कम्प्रेशन आर्टिफैक्ट्स इंजन को भ्रमित कर सकते हैं। |
| **सफ़ेद बॉर्डर ट्रिम करें** | अनावश्यक व्हाइटस्पेस प्रोसेसिंग टाइम बढ़ाता है और फॉल्स पॉज़िटिव्स का कारण बन सकता है। |
| **`tesseract.setPageSegMode(ITesseract.PSM_AUTO)` सेट करें** केवल तब जब लेआउट अज्ञात हो; अन्यथा एक विशिष्ट मोड चुनें (जैसे `PSM_SINGLE_BLOCK`). |
| **`ITesseract` इंस्टेंस को कैश करें** |

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर करने में मदद करती हैं।

- [Java में Aspose OCR का उपयोग करके इमेज से टेक्स्ट पढ़ना – पूर्ण गाइड](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Java में OCR का उपयोग कैसे करें – इमेज से तेज़ी से टेक्स्ट पहचानें](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [Java में बैच इमेज OCR – PNG फ़ाइलों से तेज़ी से टेक्स्ट निकालें](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}