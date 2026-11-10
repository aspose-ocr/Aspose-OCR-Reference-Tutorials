---
category: general
date: 2026-06-16
description: تعرف على النص في الصورة بسرعة باستخدام Aspose OCR في Java. تعلم كيفية
  تعيين جهاز GPU، استخراج النص من ملف JPG، وقراءة صورة النص باستخدام تسريع GPU.
draft: false
keywords:
- recognize text image
- set gpu device
- extract text jpg
- how to recognize text
- read text picture
language: ar
og_description: التعرف على نص الصورة باستخدام Aspose OCR في Java. يوضح هذا الدليل
  كيفية ضبط جهاز GPU، استخراج النص من ملف JPG، وقراءة صورة النص بكفاءة.
og_title: التعرف على نص الصورة في جافا باستخدام Aspose OCR + GPU
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text image quickly with Aspose OCR in Java. Learn how to
    set gpu device, extract text jpg, and read text picture using GPU acceleration.
  headline: recognize text image in Java using Aspose OCR + GPU
  type: TechArticle
tags:
- OCR
- Java
- Aspose
- GPU
title: التعرف على نص الصورة في جافا باستخدام Aspose OCR + GPU
url: /ar/java/advanced-ocr-techniques/recognize-text-image-in-java-using-aspose-ocr-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص في صورة باستخدام Aspose OCR + GPU في جافا

هل تساءلت يومًا كيف يمكنك التعرف على النص في صورة داخل تطبيق جافا دون أن تُثقل وحدة المعالجة المركزية؟ لست وحدك—المطورون يسعون باستمرار إلى خطوط أنابيب OCR أسرع وأكثر موثوقية. في هذا الدرس سنستعرض حلًا كاملاً مدعومًا بـ GPU يتيح لك استخراج النص من صورة JPG في لحظات.

سنبدأ بإعداد Aspose OCR، ثم تمكين تسريع GPU، وأخيرًا سنوضح لك كيفية قراءة ملفات صور النص، طباعة النتائج، ومعالجة الأخطاء المحتملة. بنهاية الدرس ستعرف **كيفية التعرف على النص** في أي صورة، سواء كانت فاتورة ممسوحة أو لقطة شاشة عادية.

## ما الذي ستحتاجه

- **Java 17** (أو أي JDK حديث) – الشيفرة تعمل على جميع بيئات التشغيل الحديثة.  
- **Aspose.OCR for Java** – متاح عبر Maven Central.  
- **GPU** يدعم CUDA (اختياري لكن يُنصح به للسرعة).  
- صورة JPEG تجريبية (مثلاً `sample.jpg`) تريد معالجتها.  

لا توجد مكتبات طرف ثالث أخرى مطلوبة؛ كل ما تحتاجه مدمج مع Aspose OCR.

## الخطوة 1: إضافة Aspose OCR إلى مشروعك

إذا كنت تستخدم Maven، أضف الاعتماد التالي إلى ملف `pom.xml`. يمكن لمستخدمي Gradle نسخ سطر `implementation` المكافئ.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

> **نصيحة احترافية:** نسخة التقييم المجانية تضيف علامة مائية صغيرة. للإنتاج، احصل على ترخيص من بوابة Aspose واستخدم  
> `License license = new License(); license.setLicense("Aspose.OCR.lic");` قبل أي عملية OCR.

## الخطوة 2: تحميل الصورة التي تريد معالجتها

أول خطوة عندما تريد **التعرف على النص في صورة** هي إمداد محرك OCR بالصورة. توفر Aspose كائن `ImageStream` يسهل القراءة من مسار ملف، أو `InputStream`، أو حتى مصفوفة بايت.

```java
import com.aspose.ocr.*;

public class GpuOcrExample {
    public static void main(String[] args) throws Exception {
        // Load the image – replace the path with your own picture
        OcrEngine engine = new OcrEngine();
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

لاحظ أننا حافظنا على بساطة الشيفرة؛ استدعاء `setImage` يقبل أي تنسيق نقطي تدعمه Aspose، بما في ذلك JPEG و PNG و BMP.

## الخطوة 3: تمكين تسريع GPU (set gpu device)

الآن يأتي الجزء الذي يميز هذا الدليل: سنقوم **بتعيين جهاز GPU** لجعل محرك OCR يعمل على بطاقة الرسوميات بدلاً من المعالج. هذا يمكن أن يقلل الثواني من زمن المعالجة، خاصةً للصور عالية الدقة.

```java
        // Enable GPU acceleration – this is where the magic happens
        engine.getRecognitionSettings().setUseGpu(true);

        // Optional: pick a specific GPU if you have more than one
        // engine.getRecognitionSettings().setGpuDeviceId(0);
```

إذا كان لديك عدة بطاقات GPU، ألغِ التعليق عن سطر `setGpuDeviceId` واستبدل `0` بالفهرس الخاص بالجهاز الذي تفضله. سيعود Aspose تلقائيًا إلى المعالج إذا لم يُعثر على GPU متوافق، لذا لا داعي للقلق بشأن الأعطال.

## الخطوة 4: تنفيذ OCR – كيفية التعرف على النص

مع تحميل الصورة وتفعيل GPU، يمكننا أخيرًا **كيفية التعرف على النص** في الصورة. طريقة `recognize()` تشغل كامل الخطوات—المعالجة المسبقة، التجزئة، تصنيف الأحرف، والمعالجة اللاحقة.

```java
        // Execute the OCR process
        OcrResult result = engine.recognize();
```

الكائن `OcrResult` المرتجع يحتوي على السلسلة النصية الخام، درجات الثقة، وحتى إطارات الحدود إذا احتجت معلومات التخطيط لاحقًا.

## الخطوة 5: إخراج النص المُتعرف عليه – استخراج نص jpg / قراءة صورة نصية

لنقم **باستخراج نص jpg** و**قراءة صورة نصية** ببساطة عن طريق طباعة النتيجة إلى وحدة التحكم. في تطبيق واقعي قد تكتب النتيجة إلى قاعدة بيانات أو ملف.

```java
        // Show the recognized text in the console
        System.out.println("Recognized text:");
        System.out.println(result.getText());
    }
}
```

عند تشغيل البرنامج، يجب أن ترى شيئًا مشابهًا لـ:

```
Recognized text:
Invoice #12345
Date: 2026-06-15
Total: $1,250.00
```

إذا كانت الصورة تحتوي على ضوضاء، يمكنك تعديل إعدادات المعالجة المسبقة في Aspose (التباين، التثبيت الثنائي، إلخ)—لكن الإعدادات الافتراضية تعمل مع معظم ملفات JPG النظيفة.

## مثال كامل يعمل

بجمع كل ما سبق، إليك الفئة الكاملة الجاهزة للتنفيذ:

```java
import com.aspose.ocr.*;

public class GpuOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the image to be processed
        OcrEngine engine = new OcrEngine();
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Step 2: Enable GPU acceleration for faster recognition
        engine.getRecognitionSettings().setUseGpu(true);
        // Optional: specify a GPU device index if multiple GPUs are present
        // engine.getRecognitionSettings().setGpuDeviceId(0);

        // Step 3: Perform OCR on the loaded image
        OcrResult result = engine.recognize();

        // Step 4: Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(result.getText());
    }
}
```

> **الناتج المتوقع:** تُطبع وحدة التحكم النص الدقيق الموجود في `sample.jpg`. إذا كانت الصورة صورة لإيصال، سترى كل سطر كسلسلة منفصلة، مع الحفاظ على فواصل الأسطر.

## الحالات الخاصة والمشكلات الشائعة

| الحالة | ما يجب مراقبته | الحل المقترح |
|-----------|-------------------|---------------|
| **عدة بطاقات GPU** | قد لا تكون البطاقة الافتراضية هي الأقوى. | استخدم `setGpuDeviceId` لاستهداف البطاقة عالية الأداء. |
| **نفاد الذاكرة على صور كبيرة** | الصور JPG ذات الدقة العالية قد تستنزف ذاكرة GPU. | قلل حجم الصورة أولًا (`engine.getPreprocessingSettings().setResizeFactor(0.5)`). |
| **ثقة منخفضة** | قد تُخطئ بعض الأحرف إذا كانت الصورة غير واضحة. | فعّل `engine.getRecognitionSettings().setUseLanguageModel(true)` لتصحيح السياق. |
| **تنسيق صورة غير مدعوم** | يدعم Aspose OCR العديد من الصيغ، لكن ليس بيانات RAW للمستشعر. | حوّل الملف إلى JPEG أو PNG قبل إرساله إلى المحرك. |

معالجة هذه السيناريوهات تضمن بقاء سير عمل **التعرف على النص في صورة** ثابتًا عبر بيئات مختلفة.

## نصائح احترافية لتسريع OCR وتحسين جودته

- **المعالجة الدفعية:** أعد استخدام كائن `OcrEngine` واحد للعديد من الصور؛ يبقى سياق GPU نشطًا، مما يوفر وقت التهيئة.  
- **سلامة الخيوط:** يجب أن يمتلك كل خيط كائن `OcrEngine` خاص به؛ الفئة غير آمنة للاستخدام المتعدد الخيوط.  
- **الترخيص مبكرًا:** حمّل ترخيص Aspose عند بدء التطبيق لتجنب علامة التقييم.  
- **التسجيل:** فعّل `engine.getLogSettings().setEnableLogging(true)` إذا احتجت لتتبع سبب فشل صورة معينة.

## الخلاصة

لقد أظهرنا لك كيفية **التعرف على النص في صورة** باستخدام Aspose OCR مع تسريع GPU في جافا. باتباع الخطوات—إضافة المكتبة، تحميل JPEG، **تعيين جهاز GPU**، تشغيل محرك OCR، وأخيرًا **استخراج نص jpg** أو **قراءة صورة نصية**—يمكنك تحويل أي صورة إلى نص بسهولة.

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي استعرضناها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}