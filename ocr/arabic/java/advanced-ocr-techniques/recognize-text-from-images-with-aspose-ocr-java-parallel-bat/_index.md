---
category: general
date: 2026-05-31
description: التعرف على النص من الصور بسرعة باستخدام Aspose OCR Java. تعلم كيفية استخراج
  النص من ملفات PNG وتعيين لغة OCR للحصول على أفضل النتائج.
draft: false
keywords:
- recognize text from images
- extract text from png
- set OCR language
- Aspose OCR Java
- parallel OCR processing
language: ar
og_description: تعرّف على النص من الصور بكفاءة باستخدام Aspose OCR Java. يوضح هذا
  الدرس كيفية استخراج النص من ملفات PNG وتعيين لغة OCR للمعالجة الدفعية.
og_title: التعرف على النص من الصور – Aspose OCR Java دفعة متوازية
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: recognize text from images quickly using Aspose OCR Java. Learn how
    to extract text from png files and set OCR language for optimal results.
  headline: recognize text from images with Aspose OCR – Java Parallel Batch Guide
  type: TechArticle
- description: recognize text from images quickly using Aspose OCR Java. Learn how
    to extract text from png files and set OCR language for optimal results.
  name: recognize text from images with Aspose OCR – Java Parallel Batch Guide
  steps:
  - name: How It Works
    text: '- **Thread Count** – The processor creates a thread pool of the size you
      specify. On a quad‑core laptop, `4` is a sweet spot; increase it for servers
      with more cores. - **Language Setting** – By calling `setLanguage(OcrLanguage.FRENCH)`,
      we tell the OCR engine to bias its dictionary toward French ch'
  - name: 1️⃣ Missing or Corrupt Images
    text: If an image path is invalid, `OcrBatchProcessor` throws an `IOException`.
      Wrap the call in a try‑catch block, log the problematic file, and continue with
      the rest of the batch.
  - name: 2️⃣ Mixed Languages in One Batch
    text: 'When you have documents in multiple languages, you can either:'
  - name: 3️⃣ Memory Constraints
    text: Processing very large images (e.g., >10 MB) can inflate heap usage. Pre‑scale
      the images or increase the JVM’s `-Xmx` flag if you encounter `OutOfMemoryError`.
  - name: 4️⃣ Customizing OCR Settings
    text: 'Beyond language, you can tweak recognition speed vs. accuracy:'
  - name: LicenseUtil.java
    text: '```java import com.aspose.ocr.*;'
  - name: ImageProvider.java
    text: '```java import java.util.*;'
  - name: ParallelBatchDemo.java
    text: '```java import com.aspose.ocr.*; import java.util.*;'
  type: HowTo
tags:
- Java
- OCR
- Aspose
- Image Processing
title: التعرف على النص من الصور باستخدام Aspose OCR – دليل الدفعة المتوازية في Java
url: /ar/java/advanced-ocr-techniques/recognize-text-from-images-with-aspose-ocr-java-parallel-bat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصور – دليل Aspose OCR Java للمعالجة المتوازية

هل تساءلت يومًا كيف **تتعرف على النص من الصور** بطريقة لا تُجمد واجهة المستخدم؟ ربما لديك مجلد مليء بالمسحات، لقطات الشاشة، أو حتى مزيج من ملفات PNG و JPEG، وتحتاج النص بأسرع وقت. الخبر السار؟ مع Aspose OCR for Java يمكنك تشغيل دفعة متعددة الخيوط **تستخرج النص من png** (وباقي الصيغ) بينما تحتسي قهوتك.

في هذا الدليل سنستعرض مثالًا كاملًا وجاهزًا للتنفيذ يوضح كيفية **تعيين لغة OCR**، تشغيل أربعة عمال متوازين، وطباعة النتائج. في النهاية ستحصل على قالب قوي يمكنك إدراجه في أي مشروع Java—بدون إضافات غير ضرورية، فقط الشيفرة التي تحتاجها.

## ما ستتعلمه

- كيفية تطبيق ترخيص Aspose OCR حتى لا تواجه قيود النسخة التجريبية.  
- الخطوات الدقيقة لـ **التعرف على النص من الصور** بشكل متوازي، مما يزيد من الإنتاجية على الأجهزة متعددة النوى.  
- لماذا وكيفية **تعيين لغة OCR** (الفرنسية في المثال) للحصول على دقة أعلى.  
- طريقة عملية لـ **استخراج النص من png**، لكن نفس المنطق يعمل مع ملفات JPG، TIFF، BMP، إلخ.  

**المتطلبات المسبقة** – ستحتاج إلى Java 8 أو أحدث، Maven أو Gradle لجلب مكتبة Aspose OCR، وملف ترخيص Aspose OCR صالح (`Aspose.OCR.Java.lic`). لا حاجة لحيل خاصة في IDE؛ أي محرر يستطيع تجميع Java يكفي.

---

## الخطوة 1: إضافة تبعية Aspose OCR

أولاً، تأكد من أن ملف Aspose OCR JAR موجود في مسار الفئة (classpath). إذا كنت تستخدم Maven، أضف:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

لـ Gradle:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

> **نصيحة احترافية:** راقب ملاحظات إصدارات Aspose؛ فهي غالبًا ما تضيف حزم لغات أو تحسينات أداء يمكن أن توفر ثوانٍ في تشغيل الدفعات.

## الخطوة 2: تطبيق ترخيص Aspose OCR

بدون ترخيص، تعمل المكتبة في وضع التجربة وستضيف علامات مائية إلى الناتج. حمّل ملف الترخيص مرة واحدة، ويفضل عند بدء تشغيل التطبيق.

```java
import com.aspose.ocr.*;

public class LicenseUtil {
    /** Loads the Aspose OCR license from the given path. */
    public static void applyLicense(String licensePath) throws Exception {
        License license = new License();
        license.setLicense(licensePath);
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

استدعاء `LicenseUtil.applyLicense("Aspose.OCR.Java.lic")` يضمن أن كل استدعاء لاحق لـ **التعرف على النص من الصور** يعمل بدون قيود.

## الخطوة 3: إعداد قائمة الصور

يمكنك تزويد معالج الدفعة بأي مجموعة من مسارات الملفات. أدناه نوضح **استخراج النص من png** إلى جانب ملفات JPEG و TIFF—فقط استبدل المسارات بالدليل الخاص بك.

```java
import java.util.*;

public class ImageProvider {
    /** Returns a list of absolute image paths to be processed. */
    public static List<String> getImagePaths() {
        return Arrays.asList(
            "YOUR_DIRECTORY/doc1.png",   // PNG – our primary example
            "YOUR_DIRECTORY/doc2.jpg",
            "YOUR_DIRECTORY/doc3.tif"
        );
    }
}
```

> **لماذا قائمة؟** يتوقع `OcrBatchProcessor` أن تكون من نوع `List<String>` حتى يتمكن من تقسيم العمل عبر الخيوط تلقائيًا.

## الخطوة 4: تكوين وتشغيل معالج الدفعة المتوازي

الآن يأتي جوهر الدليل: إنشاء `OcrBatchProcessor`، وتحديد عدد الخيوط التي يجب تشغيلها، و **تعيين لغة OCR** إلى الفرنسية (يمكن تغييرها إلى `OcrLanguage.ENGLISH` أو أي لغة مدعومة حسب الحاجة).

```java
import com.aspose.ocr.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply the license
        LicenseUtil.applyLicense("Aspose.OCR.Java.lic");

        // 2️⃣ Gather image files
        List<String> imagePaths = ImageProvider.getImagePaths();

        // 3️⃣ Create and configure the batch processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor();
        batchProcessor.setThreadCount(4);                 // 4 parallel workers
        batchProcessor.setLanguage(OcrLanguage.FRENCH);   // set OCR language

        // 4️⃣ Run OCR on the entire batch – this is where we **recognize text from images**
        List<OcrResult> ocrResults = batchProcessor.recognize(imagePaths);

        // 5️⃣ Output the recognized text for each file
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imagePaths.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

### كيف يعمل

- **عدد الخيوط** – ينشئ المعالج مجموعة خيوط بالحجم الذي تحدده. على لابتوب رباعي النواة، `4` هو الخيار المثالي؛ يمكنك زيادة العدد للخوادم ذات النوى الأكثر.  
- **إعداد اللغة** – باستدعاء `setLanguage(OcrLanguage.FRENCH)`، نخبر محرك OCR بأن يفضّل القاموس الفرنسي، مما يحسن الدقة بشكل كبير للوثائق غير الإنجليزية.  
- **التعرف على الدفعة** – تقوم طريقة `recognize` داخليًا بالتكرار على القائمة المقدمة، وتوزيع العمل، وتعيد `List<OcrResult>` مع الحفاظ على الترتيب الأصلي. هذه هي أبسط طريقة لـ **التعرف على النص من الصور** دون كتابة كود إدارة الخيوط الخاص بك.

## الخطوة 5: التحقق من المخرجات

عند تشغيل البرنامج، يجب أن ترى شيئًا مشابهًا لـ:

```
File: YOUR_DIRECTORY/doc1.png
Bonjour le monde! Ceci est un test d'OCR.
---
File: YOUR_DIRECTORY/doc2.jpg
Hello world! This is an OCR test.
---
File: YOUR_DIRECTORY/doc3.tif
¡Hola mundo! Prueba de OCR.
---
```

إذا كان الملف الفرنسي (`doc1.png`) يحتوي على نص فرنسي، فإن خطوة **تعيين لغة OCR** ستساعد في التقاط الأحرف المشكّلة بشكل صحيح. بالنسبة لملفات PNG، يوضح هذا طريقة نظيفة لـ **استخراج النص من png** مع معالجة الصيغ الأخرى في نفس الدفعة.

---

## معالجة الحالات الشائعة

### 1️⃣ الصور المفقودة أو التالفة

إذا كان مسار الصورة غير صالح، يرمي `OcrBatchProcessor` استثناءً من نوع `IOException`. غلف الاستدعاء بكتلة try‑catch، سجّل الملف المسبب للمشكلة، واستمر في باقي الدفعة.

```java
try {
    List<OcrResult> results = batchProcessor.recognize(imagePaths);
} catch (IOException ex) {
    System.err.println("Failed to process: " + ex.getMessage());
}
```

### 2️⃣ لغات مختلطة في دفعة واحدة

عند وجود مستندات بعدة لغات، يمكنك إما:

- تشغيل دفعات منفصلة، كل واحدة مع `setLanguage` الخاصة بها.  
- أو ترك اللغة غير محددة (`OcrLanguage.AUTO_DETECT`) والسماح لـ Aspose بالتخمين، رغم أن الدقة قد تنخفض.

### 3️⃣ قيود الذاكرة

معالجة صور كبيرة جدًا (مثلاً >10 MB) قد تستهلك الذاكرة heap بشكل كبير. قلل حجم الصور مسبقًا أو زد قيمة علم `-Xmx` في JVM إذا واجهت `OutOfMemoryError`.

```bash
java -Xmx2g -cp yourapp.jar ParallelBatchDemo
```

### 4️⃣ تخصيص إعدادات OCR

إلى جانب اللغة، يمكنك تعديل سرعة التعرف مقابل الدقة:

```java
batchProcessor.setRecognitionMode(OcrRecognitionMode.ACCURATE); // default is BALANCED
```

اختيار `ACCURATE` أبطأ لكنه يعطي نتائج أفضل للمسحات الضوضائية.

---

## مثال كامل يعمل (جميع الملفات)

فيما يلي مجموعة الملفات المصدرية الكاملة التي تحتاجها. انسخها إلى مشروع Maven، عدّل مسار الترخيص ودليل الصور، ثم شغّل الأمر `mvn exec:java -Dexec.mainClass=ParallelBatchDemo`.

### LicenseUtil.java
```java
import com.aspose.ocr.*;

public class LicenseUtil {
    public static void applyLicense(String licensePath) throws Exception {
        License license = new License();
        license.setLicense(licensePath);
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

### ImageProvider.java
```java
import java.util.*;

public class ImageProvider {
    public static List<String> getImagePaths() {
        return Arrays.asList(
            "YOUR_DIRECTORY/doc1.png",
            "YOUR_DIRECTORY/doc2.jpg",
            "YOUR_DIRECTORY/doc3.tif"
        );
    }
}
```

### ParallelBatchDemo.java
```java
import com.aspose.ocr.*;
import java.util.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // Apply license
        LicenseUtil.applyLicense("Aspose.OCR.Java.lic");

        // Gather images
        List<String> imagePaths = ImageProvider.getImagePaths();

        // Configure batch processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor();
        batchProcessor.setThreadCount(4);                 // Parallelism
        batchProcessor.setLanguage(OcrLanguage.FRENCH);   // set OCR language

        // Recognize text from images
        List<OcrResult> ocrResults = batchProcessor.recognize(imagePaths);

        // Output results
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imagePaths.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

شغّله، وسترى النص المستخرج من كل ملف يُطبع على وحدة التحكم—ما تحتاجه بالضبط عند بناء أرشيفات قابلة للبحث، أتمتة إدخال البيانات، أو أدوات الوصول.

---

## الخلاصة

لقد استعرضنا للتو نمطًا كاملاً وجاهزًا للإنتاج لـ **التعرف على النص من الصور** باستخدام Aspose OCR for Java. من خلال تكوين معالج الدفعة، يمكنك **استخراج النص من png** (وباقي الصيغ) بشكل متوازي، وإمكانية **تعيين لغة OCR** تضمن حصولك على أعلى دقة ممكنة للعبء متعدد اللغات.

الخطوات التالية؟ جرّب تغيير اللغة إلى `OcrLanguage.SPANISH` أو جرب `OcrRecognitionMode.ACCURATE` للمسحات الصعبة. يمكنك أيضًا دمج النتائج في قاعدة بيانات، أو إطعامها إلى فهرس بحث، أو تمريرها إلى واجهة برمجة تطبيقات ترجمة.

هل لديك سيناريو صعب—مثل OCR على ملفات PDF أو على صور مخزنة في السحابة؟ هذه امتدادات طبيعية لما بنيناه اليوم. غص في التفاصيل، عدّل الإعدادات، ودع محرك OCR يقوم بالعمل الشاق.

برمجة سعيدة، ولتكن استخراج النصوص سريعًا ودقيقًا!

## ما الذي يجب أن تتعلمه بعد ذلك؟

- [استخراج نص الصور – أساسيات OCR مع Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [كيفية OCR نص الصورة مع اللغة باستخدام Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [التعرف على نص الصورة باستخدام Aspose OCR – دليل OCR كامل لـ Java](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}