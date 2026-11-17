---
category: general
date: 2026-11-17
description: تعلم كيفية تنفيذ تقنية التعرف الضوئي على الأحرف (OCR) على صورة باستخدام
  جافا واستخراج النص من الصور عبر مثال شفرة بسيط. يتضمن نصائح لقراءة الصور في جافا.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: ar
lastmod: 2026-11-17
og_description: كيفية تنفيذ OCR على صورة في جافا واستخراج النص بسرعة. اتبع هذا الدليل
  لقراءة الصورة في جافا وتحويل الصورة إلى نص مع مثال جاهز للتنفيذ.
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: كيفية تنفيذ OCR على صورة في جافا – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: كيفية تنفيذ OCR على صورة في جافا – دليل خطوة بخطوة
url: /ar/java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR على صورة في Java – دليل خطوة بخطوة

إذا كنت بحاجة إلى **how to perform OCR** على صورة، يوضح لك هذا الدرس حلاً كاملاً قابلاً للتنفيذ في Java. سترى كيفية قراءة ملف صورة، وتكوين محرك OCR، واستخراج النص الذي يتعرف عليه المحرك.

العمل مع المستندات الممسوحة ضوئياً، والإيصالات، أو لقطات الشاشة غالبًا ما يتطلب تحويل المحتوى البصري إلى نص قابل للبحث. يوجهك هذا الدليل عبر كل خطوة، من تحميل الصورة إلى طباعة النص المستخرج، كما يغطي المشكلات الشائعة مثل صيغ الملفات غير المدعومة والنتائج الفارغة.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من أن لديك:

* Java Development Kit (JDK) 8 أو أحدث مثبت.
* أداة بناء (Maven أو Gradle) لجلب مكتبة OCR.
* ملف صورة (JPEG, PNG, BMP) تريد معالجته.

يستخدم الكود **OCR library from the `com.asprise.ocr` package** لأنه يتطلب JAR واحد فقط ويعمل على جميع الأنظمة الأساسية الرئيسية. استبدله بموفر آخر (Tesseract, Google Vision, إلخ) عن طريق تبديل عبارات الاستيراد وكود تهيئة المحرك.

## الخطوة 1: إضافة تبعية OCR

إذا كنت تستخدم Maven، أضف التبعية التالية إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

لـ Gradle، ضع هذا السطر في `build.gradle`:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

هذه الأسطر تضمن أن كود **read image Java** يمكن أن يُترجم وأن محرك OCR متاح أثناء التشغيل.

## الخطوة 2: قراءة الصورة باستخدام Java

قراءة ملف صورة هي الخطوة الملموسة الأولى في أي سير عمل **extract text image**. فئة `ImageIO` المدمجة في Java تتعامل مع معظم الصيغ الشائعة.

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**لماذا هذا مهم:** `ImageIO.read` تُعيد `null` للصيغ غير المدعومة أو الملفات الفاسدة. الطريقة أعلاه تسجل المشكلة وتُعيد `null` حتى يتمكن الخطوة التالية من التعامل معها برشاقة.

## الخطوة 3: إنشاء وتكوين محرك OCR

يجب أن يعرف محرك OCR أي لغة يجب التعرف عليها. ضبط اللغة يحسن الدقة بشكل كبير، خاصةً للوثائق غير الإنجليزية.

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**لماذا هذا مهم:** تشغيل المحرك عملية ثقيلة نسبيًا، لذا يجب إنشاؤه مرة واحدة وإعادة استخدامه لعدة صور إذا كان تطبيقك يعالج دفعات.

## الخطوة 4: تنفيذ OCR وتحويل الصورة إلى نص

الآن بعد تحميل الصورة واستعداد المحرك، يمكنك تشغيل خطوة التعرف. هذه هي جوهر **how to perform OCR**.

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**معالجة الحالات الحدية:** إذا كانت الصورة `null`، تُعيد الطريقة سلسلة فارغة بدلاً من رمي `NullPointerException`. هذا يجعل الكود المحيط أكثر صلابة عند التعامل مع ملفات يزودها المستخدم.

## الخطوة 5: عرض النص المستخرج

أخيرًا، اطبع النتيجة على وحدة التحكم أو مرّرها إلى مكوّن آخر (مثل قاعدة بيانات أو عنصر واجهة مستخدم).

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

عند تشغيل البرنامج باستخدام `java OcrDemo sample.jpg`، تُظهر وحدة التحكم الأحرف التي تم التعرف عليها. هذا يكمل دورة **convert image to text**.

### النتيجة المتوقعة

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

إذا لم تحتوي الصورة على أحرف قابلة للقراءة، يطبع البرنامج `(no text detected)`.

## الاختلافات الشائعة وكيفية التكيف معها

| التنوع | ما الذي يتغير | متى يستخدم |
|-----------|--------------|-------------|
| **لغة مختلفة** | استبدل `"eng"` بـ `"spa"` للإسبانية، `"fra"` للفرنسية، إلخ. | المستندات المكتوبة بلغة غير الإنجليزية |
| **معالجة دفعات** | كرر عبر قائمة مسارات الملفات، وأعد استخدام نفس كائن `Ocr`. | مجموعات كبيرة من الصفحات الممسوحة |
| **دقة أعلى** | استخدم `Ocr.SPEED_SLOW` أو فعّل `ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")` للمسحات الرقمية فقط. | عندما تكون جودة OCR حرجة (مثل أرقام الفواتير) |
| **بديل Tesseract** | بدّل الاستيراد إلى `net.sourceforge.tess4j.Tesseract` وعدّل كود التهيئة. | المشاريع التي تعتمد بالفعل على Tesseract |

## نصائح احترافية

* **Resize large images** قبل إمدادها إلى المحرك؛ سرعة OCR تتناسب مع عدد البكسلات.
* **Pre‑process** الصورة (تحويل إلى تدرج الرمادي، تعزيز التباين) باستخدام مكتبات مثل OpenCV إذا كان المصدر مشوشًا.
* **Cache the OCR engine** إذا كنت تستدعيه مرات متعددة في فترة قصيرة—بدء وإيقاف المحرك يستهلك موارد.
* **Validate the result** باستخدام تعبيرات منتظمة عندما تتوقع تنسيقًا محددًا (مثل التواريخ، أرقام الهواتف).

## الخلاصة

أنت الآن تعرف **how to perform OCR** على صورة في Java، من قراءة الملف إلى عرض النص المستخرج. غطى الدرس تقنيات **read image Java**, **extract text image**, **convert image to text**, و**image to text java**، وقدّم نصائح عملية للسيناريوهات الواقعية.

من هنا يمكنك:

* دمج خطوة OCR في خدمة ويب تستقبل ملفات مرفوعة.
* دمج الناتج مع فهرس بحث لتوفير بحث نص كامل عبر المستندات الممسوحة.
* استكشاف خيارات OCR المتقدمة مثل الدعم متعدد اللغات أو مجموعات الأحرف المخصصة.

برمجة سعيدة، واستمتع بتحويل الصور إلى نص قابل للبحث!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية استخدام OCR في Java – استخراج النص من الصورة مع تصحيح إملائي](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [تحويل الصورة إلى نص في Java باستخدام Aspose OCR – دليل كامل](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [كيفية تمكين GPU لـ OCR في Java – استخراج النص من الصورة](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}