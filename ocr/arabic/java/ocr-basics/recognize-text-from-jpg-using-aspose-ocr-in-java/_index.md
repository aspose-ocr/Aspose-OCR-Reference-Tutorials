---
category: general
date: 2026-06-22
description: التعرف على النص من ملف JPG في جافا باستخدام Aspose OCR – تعلم كيفية تحميل
  الصورة للتعرف الضوئي على الأحرف، استخراج النص من الصورة، وتحويل الصورة إلى نص بسرعة.
draft: false
keywords:
- recognize text from jpg
- extract text from image
- convert image to text
- read scanned document
- load image for ocr
language: ar
og_description: التعرف على النص من ملف JPG في جافا – دليل خطوة بخطوة لتحميل الصورة
  للتعرف الضوئي على الأحرف، استخراج النص من الصورة، وتحويل الصورة إلى نص.
og_title: التعرف على النص من ملف JPG باستخدام Aspose OCR في Java
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: recognize text from jpg in Java with Aspose OCR – learn how to load
    image for OCR, extract text from image, and convert image to text quickly.
  headline: recognize text from jpg using Aspose OCR in Java
  type: TechArticle
- description: recognize text from jpg in Java with Aspose OCR – learn how to load
    image for OCR, extract text from image, and convert image to text quickly.
  name: recognize text from jpg using Aspose OCR in Java
  steps:
  - name: Prerequisites (the bare minimum)
    text: '- Java Development Kit (JDK) 8 or newer installed. - Maven or Gradle (we’ll
      use Maven in the example, but the same JAR works with Gradle). - A JPEG image
      you want to test with (named `sample.jpg` for simplicity). - An Aspose OCR license
      (the free evaluation works fine for this demo).'
  - name: Why each line matters
    text: 1. **`OcrEngine engine = new OcrEngine();`** – Instantiates the engine.
      Think of it as turning on the scanner. 2. **`engine.setImage(...)`** – This
      is where we **load image for OCR**. The method accepts an `ImageStream`, which
      can come from a file, a byte array, or even a network stream. 3. **`engin
  - name: From a byte array (e.g., when the image is stored in a database)
    text: '```java byte[] imageBytes = Files.readAllBytes(Paths.get("YOUR_DIRECTORY/sample.jpg"));
      engine.setImage(ImageStream.fromByteArray(imageBytes)); ```'
  - name: Directly from a URL (useful for web services)
    text: '```java URL imageUrl = new URL("https://example.com/sample.jpg"); engine.setImage(ImageStream.fromUrl(imageUrl));
      ```'
  type: HowTo
tags:
- Java
- Aspose OCR
- Image Processing
title: التعرف على النص من ملف JPG باستخدام Aspose OCR في Java
url: /ar/java/ocr-basics/recognize-text-from-jpg-using-aspose-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من JPG باستخدام Aspose OCR في Java – دليل شامل

هل احتجت يومًا إلى **التعرف على النص من JPG** لكنك لم تكن متأكدًا أي مكتبة تجعل العملية سهلة؟ لست وحدك. سواء كنت تقوم برقمنة فواتير قديمة، أو استخراج بيانات من نماذج ممسوحة، أو مجرد فضول حول تحويل الصور إلى سلاسل قابلة للبحث، يوضح هذا الدليل بالضبط كيفية **تحميل الصورة للتعرف الضوئي**، **استخراج النص من الصورة**، و**تحويل الصورة إلى نص** باستخدام Aspose OCR في Java.

في الدقائق القليلة القادمة سننشئ برنامج Java صغير، نمرره صورة JPEG، ونراقب المحرك يخرج نصًا عاديًا. لا حيل سطر أوامر غامضة، لا خدمات خارجية—فقط شفرة نظيفة تُنفّذ محليًا يمكنك تشغيلها في أي بيئة تدعم Java.

## ما ستحصل عليه

- مشروع Java يعمل على **التعرف على النص من ملفات JPG**.
- فهم كل خطوة: تثبيت المكتبة، تحميل الصورة، تشغيل محرك OCR، ومعالجة النتيجة.
- نصائح لقراءة المستندات الممسوحة التي تحتوي على لغات متعددة أو صور منخفضة الجودة.
- أساس يمكنك توسيعه إلى PDFs، PNGs، أو حتى تدفقات كاميرا في الوقت الحقيقي.

### المتطلبات المسبقة (الحد الأدنى)

- Java Development Kit (JDK) 8 أو أحدث مثبت.
- Maven أو Gradle (سنستخدم Maven في المثال، لكن نفس الـ JAR يعمل مع Gradle).
- صورة JPEG تريد اختبارها (اسمها `sample.jpg` للتبسيط).
- رخصة Aspose OCR (التقييم المجاني يكفي لهذا العرض).

إذا كان أي من ذلك غير مألوف لك، لا تقلق—سأوجهك إلى الأوامر الدقيقة التي تحتاجها.

---

## التعرف على النص من JPG – إعداد Aspose OCR

أولًا: نحتاج مكتبة Aspose OCR في مسار الفئة (classpath). أسهل طريقة هي إضافة تبعية Maven إلى ملف `pom.xml`.

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check the latest version on Maven Central -->
</dependency>
```

> **نصيحة محترف:** إذا كنت تستخدم Gradle، فالمكافئ هو `implementation 'com.aspose:aspose-ocr:23.9'`.  

بعد أن ينتهي Maven من التحميل، ستكون جاهزًا لـ **تحميل الصورة للتعرف الضوئي** في شفرة Java الخاصة بك.

---

## استخراج النص من الصورة – كتابة الفئة الأساسية في Java

فيما يلي فئة قابلة للتنفيذ بالكامل تُدعى `SimpleOcr`. تتبع نفس التدفق الموجود في العينة الأصلية، مع بعض الحمايات والتعليقات لتوضيح المنطق.

```java
import com.aspose.ocr.*;

public class SimpleOcr {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance – this is the heart of the process.
        OcrEngine engine = new OcrEngine();

        // Step 2: Load the image to be recognized.
        // Replace "YOUR_DIRECTORY/sample.jpg" with the real path to your JPEG.
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Optional: tweak language or recognition mode if you know the source.
        // engine.setLanguage(OcrLanguage.English);
        // engine.setRecognitionMode(OcrRecognitionMode.Text);

        // Step 3: Perform the OCR operation.
        OcrResult result = engine.recognize();

        // Step 4: Retrieve and display the recognized plain‑text.
        System.out.println("=== OCR Output ===");
        System.out.println(result.getText());
    }
}
```

### لماذا كل سطر مهم

1. **`OcrEngine engine = new OcrEngine();`** – ينشئ المحرك. فكّر فيه كتشغيل الماسح الضوئي.
2. **`engine.setImage(...)`** – هنا **نحمّل الصورة للتعرف الضوئي**. الطريقة تقبل `ImageStream`، ويمكن أن يأتي من ملف، مصفوفة بايت، أو حتى تدفق شبكة.
3. **`engine.recognize();`** – يطلق العملية الثقيلة. تحت الغطاء، Aspose يطبق ما قبل المعالجة، التجزئة، وتصنيف الأحرف.
4. **`result.getText();`** – يُعيد `String` نصًا عاديًا. لا XML، لا PDF—فقط الأحرف التي يمكنك توجيهها إلى قاعدة بيانات أو فهرس بحث.

الترجمة والتشغيل:

```bash
mvn compile exec:java -Dexec.mainClass=SimpleOcr
```

ستظهر لك نتيجة مشابهة لـ:

```
=== OCR Output ===
Invoice #12345
Date: 2026-06-01
Total: $1,234.56
```

إذا كان الإخراج مشوشًا، سنغطي لاحقًا حيل **قراءة المستند الممسوح**.

---

## تحويل الصورة إلى نص – تحسين الدقة

الإعدادات الافتراضية تعمل مع JPEGs نظيفة وعالية الدقة، لكن المسحات الواقعية غالبًا ما تعاني من ضوضاء، ميل، أو خطوط غير مألوفة. إليك ثلاث تعديلات يمكنك إجراؤها دون تعديل الكود الأساسي:

| الإعداد | ما يفعله | متى تستخدمه |
|---------|----------|--------------|
| `engine.setLanguage(OcrLanguage.English);` | يجبر المحرك على النظر فقط إلى الحروف الإنجليزية، مما يقلل الإيجابيات الزائفة. | صورتك تحتوي لغة واحدة فقط. |
| `engine.setPreprocessingOptions(OcrPreprocessingOptions.AutoRotate);` | يدور الصورة تلقائيًا إذا اكتشف ميلًا. | مستندات ممسوحة ليست أفقية تمامًا. |
| `engine.setResolution(300);` | يرفع دقة الصورة إلى 300 dpi قبل التعرف. | JPEGs منخفضة الدقة (مثل لقطات الشاشة). |

أضف أيًا من هذه الأسطر بعد تحميل الصورة وقبل `recognize()`. مثال:

```java
engine.setResolution(300);
engine.setPreprocessingOptions(OcrPreprocessingOptions.AutoRotate);
engine.setLanguage(OcrLanguage.English);
```

هذه التعديلات تحسّن خطوة **تحويل الصورة إلى نص**، خاصةً عندما *تقرأ مستندًا ممسوحًا* تم حفظه أولًا كـ JPEG.

---

## تحميل الصورة للتعرف الضوئي – التعامل مع مصادر الإدخال المختلفة

حتى الآن أظهرنا تحميلًا بسيطًا من ملف. Aspose OCR، مع ذلك، مرن بما يكفي لقبول تدفقات من الذاكرة، URLs، أو حتى موارد Android. إليك بديلان شائعان:

### من مصفوفة بايت (مثلاً عندما تكون الصورة مخزنة في قاعدة بيانات)

```java
byte[] imageBytes = Files.readAllBytes(Paths.get("YOUR_DIRECTORY/sample.jpg"));
engine.setImage(ImageStream.fromByteArray(imageBytes));
```

### مباشرةً من URL (مفيد للخدمات الويب)

```java
URL imageUrl = new URL("https://example.com/sample.jpg");
engine.setImage(ImageStream.fromUrl(imageUrl));
```

كلا النهجين يلبّيان متطلبات **تحميل الصورة للتعرف الضوئي**، مما يتيح لك دمج OCR في نقاط نهاية REST أو وظائف دفعية دون الحاجة إلى نظام ملفات.

---

## قراءة المستند الممسوح – التعامل مع ملفات متعددة الصفحات أو منخفضة الجودة

المستند الممسوح نادرًا ما يكون صورة واحدة مثالية. إليك كيف يمكنك توسيع المثال البسيط:

1. **التكرار عبر الصفحات** – إذا كان لديك TIFF متعدد الصفحات، استخدم `ImageStream.fromFile("multi.tif")` واستدعِ `engine.recognize()` لكل فهرس صفحة.
2. **تطبيق التثنيم** – للمسحات المتناثرة، استدعِ `engine.setBinarizationMethod(OcrBinarizationMethod.Otsu);` قبل التعرف.
3. **تمكين المدقق الإملائي** – Aspose يمكنه معالجة النتائج بقاموس مدمج: `engine.setUseSpellChecker(true);`.

هذه التقنيات تُحدث الفارق بين مجموعة من الأحرف العشوائية ونص نظيف قابل للبحث.

---

## مثال كامل من البداية إلى النهاية – من إعداد Maven إلى مخرجات وحدة التحكم

فيما يلي تخطيط المشروع الكامل يمكنك نسخه ولصقه في دليل جديد.

```
my-ocr-project/
├─ pom.xml
└─ src/
   └─ main/
      └─ java/
         └─ SimpleOcr.java
```

**pom.xml**

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-demo</artifactId>
    <version>1.0.0</version>
    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-ocr</artifactId>
            <version>23.9</version>
        </dependency>
    </dependencies>
</project>
```

**SimpleOcr.java** – (نفس المقتطف السابق، مع تعديلات اختيارية)



## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [التعرف على نص الصورة باستخدام Aspose OCR – دليل Java OCR كامل](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [كيفية التعرف الضوئي على نص الصورة مع اللغة باستخدام Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [استخراج النص من صورة Java باستخدام وضع اكتشاف المناطق في Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}