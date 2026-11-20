---
category: general
date: 2026-10-11
description: تعلم كيفية إجراء التعرف الضوئي على الأحرف (OCR) على صورة PNG في جافا،
  استخراج النص من الصورة وتحويل الصورة إلى نص باستخدام مثال بسيط لـ OcrEngine.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: ar
lastmod: 2026-10-11
og_description: كيفية إجراء التعرف الضوئي على الأحرف (OCR) على صورة PNG في جافا، استخراج
  النص من الصورة وتحويل الصورة إلى نص باستخدام مثال مختصر وجاهز للتنفيذ.
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: كيفية إجراء OCR على صورة PNG في جافا – دليل شامل
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
title: كيفية إجراء OCR على صورة PNG في جافا
url: /ar/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إجراء OCR على صورة PNG في Java

إذا كنت بحاجة إلى **perform OCR** على ملف صورة، فإن تعلم **how to perform OCR** في Java أمر أساسي للعديد من مهام الأتمتة. سواء كنت تقوم برقمنة الإيصالات، أو فهرسة المستندات الممسوحة ضوئياً، أو بناء أرشيف صور قابل للبحث، فإن القدرة على **extract text from image** توفر ساعات لا تحصى من العمل اليدوي.

يظهر لك هذا البرنامج التعليمي حلاً كاملاً وقابلاً للتنفيذ يقوم بتحميل صورة PNG، وتشغيل محرك OCR، و**recognize text from PNG**. ستتعرف أيضًا على كيفية **convert image to text** ومعالجة المشكلات الشائعة مثل الإدخال منخفض الدقة أو الأحرف غير ASCII.

## ما ستحققه

* **load image java** كود يقرأ PNG من القرص،
* تهيئة محرك OCR خفيف الوزن،
* **extract text from image** وطباعة النتيجة إلى وحدة التحكم،
* تعديل الحل لتعامل مع صيغ صور أخرى أو المعالجة الدفعية.

لا تتطلب خدمات خارجية—فقط مكتبة OCR مفتوحة المصدر واحدة (Tess4J) وبيئة تشغيل Java SE.

---

## المتطلبات المسبقة

* Java 17 أو أحدث (الكود يُجمع باستخدام JDK 17).
* Maven أو Gradle لإدارة التبعيات.
* إلمام أساسي بسطر الأوامر وIDE التي تختارها.
* مكتبة `tess4j` (غلاف Java لـ Tesseract). أضف تبعية Maven التالية:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

إذا كنت تستخدم Gradle، فإن المكافئ هو:

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

تحتاج أيضًا إلى ملفات بيانات Tesseract (`.traineddata`). قم بتنزيل حزمة البيانات الإنجليزية من المستودع الرسمي وضعها في مجلد باسم `tessdata` في جذر المشروع.

---

## الخطوة 1: تحميل الصورة في Java

تحميل PNG سهل باستخدام الفئة القياسية `ImageIO`. يوضح الكود أدناه **load image java** بطريقة آمنة ومراعية للاستثناءات:

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

**لماذا هذا مهم:** `ImageIO.read` يكتشف تنسيق الصورة تلقائيًا، لكننا نتحقق صراحةً من `null` لتجنب الفشل الصامت عندما تكون PNG تالفة. هذا النمط هو أفضل ممارسة عندما تقوم **load image java** لـ OCR.

---

## الخطوة 2: تهيئة محرك OCR

Tess4J يلتف حول الثنائي الأصلي لـ Tesseract، ويعرض واجهة برمجة تطبيقات Java بسيطة. الطريقة التالية تنشئ كائن `Tesseract`، وتوجهه إلى مجلد `tessdata`، وتضبط اللغة إلى الإنجليزية:

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

**لماذا نفعل ذلك:** تهيئة المحرك مرة واحدة وإعادة استخدامه لعدة صور يقلل من عبء بدء التشغيل. استدعاء `setOcrEngineMode` يختار الوضع الافتراضي، والذي يعمل جيدًا لمعظم PNGs. إذا واجهت مسحات ضوضائية، يمكنك تجربة أوضاع أخرى (مثل `OEM_LSTM_ONLY`).

---

## الخطوة 3: تنفيذ OCR و**recognize text from PNG**

الآن نجمع محمل الصورة ومحرك OCR. الطريقة أدناه تنفذ OCR على `BufferedImage` وتعيد السلسلة المستخرجة:

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

**مثال كامل قابل للتنفيذ**

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

**الناتج المتوقع**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

ستظهر وحدة التحكم الأحرف الدقيقة التي استخرجها المحرك من `sample.png`. إذا كانت PNG تحتوي على كلمة واحدة فقط، فسيكون الناتج تلك الكلمة متبوعة بسطر جديد.

---

## الخطوة 4: التغييرات الشائعة وحالات الحافة

### 4.1 معالجة PNG منخفض الدقة

يعمل Tesseract بأفضل أداء على الصور التي لا تقل عن 300 DPI. إذا كانت PNG المصدر أصغر، قم بتكبيرها قبل OCR:

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

طبق `upscale(image, 2)` قبل استدعاء `extractText` لتحسين الدقة.

### 4.2 استخراج نص غير إنجليزي

لـ **extract text from image** التي تحتوي على لغات أخرى، قم بتنزيل ملفات `.traineddata` المناسبة واضبط رمز اللغة:

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 المعالجة الدفعية لعدة PNGs

إذا كنت بحاجة إلى **recognize text from PNG** في مجلد، قم بالتكرار عبر الدليل:

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 التعامل مع أخطاء OCR

الأخطاء الشائعة في OCR تشمل قراءة `0` (صفر) كـ `O` أو `1` كـ `l`. يمكن للمعالجة اللاحقة باستخدام التعبيرات النمطية تنظيف النتيجة:

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

---

## نصائح احترافية للحصول على OCR موثوق في Java

| النصيحة | السبب |
|-----|--------|
| **استخدم PNG غير مضغوط** | قد تشوش عيوب الضغط في JPEG على المحرك. |
| **قص الحدود البيضاء** | المسافات البيضاء الزائدة تزيد من وقت المعالجة وقد تتسبب في إيجابيات كاذبة. |
| **اضبط `tesseract.setPageSegMode(ITesseract.PSM_AUTO)`** فقط عندما يكون التخطيط غير معروف؛ وإلا اختر وضعًا محددًا (مثل `PSM_SINGLE_BLOCK`). |
| **خزن كائن `ITesseract` في الذاكرة** |

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شاملة من الكود مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية قراءة النص من صورة في Java باستخدام Aspose OCR – دليل كامل](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [كيفية استخدام OCR في Java – التعرف على النص من الصورة بسرعة](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [OCR للصور دفعيًا في Java – استخراج النص من ملفات PNG بسرعة](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}