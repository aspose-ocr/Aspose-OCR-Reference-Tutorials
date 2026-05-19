---
category: general
date: 2026-03-07
description: حمّل صورة للتعرف الضوئي على الأحرف (OCR) في جافا بسرعة. تعلّم كيفية ضبط
  محرك OCR، وتحديد منطقة الاهتمام (ROI)، واستخراج النص – يتضمن مثالًا كاملاً للكود
  ونصائح حول كيفية ضبط OCR.
draft: false
keywords:
- load image for OCR
- how to set OCR
- OCR region of interest
- Java OCR example
- image processing Java
language: ar
og_description: حمّل صورة للتعرف الضوئي على الأحرف في جافا وتعلم كيفية ضبط محرك التعرف
  الضوئي على الأحرف. يشرح لك هذا الدليل كيفية التعامل مع منطقة الاهتمام (ROI)، والتدوير،
  والكود الكامل.
og_title: تحميل الصورة للتعرف الضوئي على الأحرف في جافا – دليل برمجة شامل
tags:
- OCR
- Java
- Image Processing
title: تحميل صورة للتعرف الضوئي على الأحرف في جافا – دليل خطوة بخطوة
url: /ar/java/ocr-operations/load-image-for-ocr-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحميل صورة للتعرف الضوئي على الحروف في جافا – دليل برمجة كامل

هل احتجت يوماً إلى **تحميل صورة للتعرف الضوئي على الحروف** لكن لم تكن متأكدًا من الاستدعاءات التي يجب استخدامها؟ لست وحدك—معظم المطورين يواجهون هذه المشكلة عندما تصل الصورة الأولى ويظهر محرك التعرف الضوئي على الحروف مشوشًا. الخبر السار هو أن الحل بسيط جدًا بمجرد معرفة الخطوات الصحيحة.

في هذا الدرس سنوضح لك **كيفية ضبط إعدادات التعرف الضوئي على الحروف**، وتعريف منطقة الاهتمام (ROI)، وأخيرًا استخراج النص من تلك القطعة من الصورة. في النهاية ستحصل على برنامج جافا قابل للتنفيذ يقوم بتحميل صورة للتعرف الضوئي على الحروف، يدورها تلقائيًا إذا لزم الأمر، ويطبع النص المستخرج—كل ذلك دون أي تعقيدات غير واضحة.

## ما ستحتاجه

- Java 17 أو أحدث (يستخدم الكود كلمة المفتاح `var` للتقليل، لكن يمكنك الرجوع إلى إصدار أقدم إذا اضطررت).  
- مجموعة تطوير برمجيات (SDK) للتعرف الضوئي على الحروف توفر الفئات `OcrEngine`، `OcrResult`، و `ImageInputStream` — فكر في مكتبات مثل **Tesseract‑Java**، **ABBYY**، أو حل مملوك.  
- صورة نموذجية (`multi_page_form.png`) تحتوي على النص الذي تريد قراءته.  
- بيئة تطوير متكاملة (IDE) بسيطة (IntelliJ IDEA، Eclipse، VS Code) — أي منها يناسبك.

لا يتطلب المنطق الأساسي أي تعقيدات Maven أو Gradle؛ فقط أضف ملف JAR الخاص بالتعرف الضوئي إلى مسار الفئات (classpath) وستكون جاهزًا للانطلاق.

## الخطوة 1: إعداد محرك التعرف الضوئي – كيفية ضبط التعرف الضوئي بشكل صحيح

قبل أن تتمكن من **تحميل صورة للتعرف الضوئي على الحروف**، تحتاج إلى نسخة من المحرك تعرف ما يجب البحث عنه. معظم مجموعات SDK تكشف عن كائن إعدادات؛ هنا تخبر المحرك بتمكين تدوير النص تلقائيًا داخل منطقة الاهتمام.

```java
import com.example.ocr.OcrEngine;   // Replace with your actual package
import com.example.ocr.OcrConfig;

public class OcrSetup {
    public static OcrEngine createEngine() {
        OcrEngine engine = new OcrEngine();

        // Enable automatic rotation handling within the region of interest
        engine.getConfig().setAutoRotateWithinRegion(true);

        // You can also tweak language, confidence thresholds, etc.
        // engine.getConfig().setLanguage("eng");
        // engine.getConfig().setMinConfidence(0.75);

        return engine;
    }
}
```

**لماذا هذا مهم:** تشغيل `setAutoRotateWithinRegion` يوفر عليك الكثير من معالجة ما بعد التعرف. تخيل نموذجًا ممسوحًا حيث يميل المستخدم الصفحة بضع درجات—بدون هذا الإعداد سيقرأ محرك التعرف نصًا غير مفهوم. تمكينه *كيفية ضبط التعرف الضوئي* يضمن المتانة مباشرةً من الصندوق.

## الخطوة 2: تحميل صورة للتعرف الضوئي – إمداد المحرك

الآن بعد أن أصبح المحرك جاهزًا، نقوم فعليًا بـ **تحميل صورة للتعرف الضوئي على الحروف**. فئة `ImageInputStream` تُجردك من التعامل مع الملفات وتسمح لمجموعة SDK للتعرف الضوئي باستهلاك التدفق مباشرةً.

```java
import com.example.ocr.ImageInputStream;
import java.nio.file.Paths;

public class ImageLoader {
    public static ImageInputStream load(String path) throws Exception {
        // Validate the file exists and is readable
        if (!java.nio.file.Files.isReadable(Paths.get(path))) {
            throw new IllegalArgumentException("Cannot read image at: " + path);
        }

        // Create the stream – most SDKs accept a simple file path, but a stream is more flexible
        return new ImageInputStream(path);
    }
}
```

**نصيحة:** إذا كنت تتعامل مع ملفات PDF متعددة الصفحات، تسمح العديد من مكتبات التعرف الضوئي بتمرير فهرس الصفحة إلى مُنشئ التدفق. بهذه الطريقة يمكنك التكرار عبر الصفحات دون خطوات تحويل إضافية.

## الخطوة 3: تعريف منطقة الاهتمام (ROI)

مسح الصورة بالكامل قد يكون مضيعة للموارد، خاصةً مع النماذج الكبيرة. بتضييق التركيز إلى مستطيل، تسرّع المعالجة وتزيد الدقة.

```java
import java.awt.Rectangle;

public class RoiHelper {
    public static Rectangle defineRoi() {
        // x, y, width, height – adjust these numbers to match your form layout
        int x = 120;
        int y = 350;
        int width = 800;
        int height = 200;

        return new Rectangle(x, y, width, height);
    }
}
```

**حالة حافة:** إذا امتدت منطقة الاهتمام خارج حدود الصورة، فإن معظم المحركات ستطرح استثناءً. فحص سريع للمنطق (مثل مقارنة `x + width` مع `image.getWidth()`) يمكن أن يمنع الأعطال.

## الخطوة 4: تشغيل التعرف الضوئي على منطقة الاهتمام

مع وجود المحرك، الصورة، ومنطقة الاهتمام جاهزة، حان الوقت لـ **تحميل صورة للتعرف الضوئي على الحروف** وتحديد النص فعليًا.

```java
import com.example.ocr.OcrResult;

public class OcrRunner {
    public static OcrResult run(OcrEngine engine,
                                ImageInputStream image,
                                Rectangle roi) throws Exception {
        // The recognize method returns both text and confidence data
        return engine.recognize(image, roi);
    }
}
```

إذا احتجت إلى درجة الثقة لكل كلمة، عادةً ما توفر `OcrResult` مجموعة `getWords()` حيث يحتوي كل عنصر على طريقة `getConfidence()`. تصفية الكلمات ذات الثقة المنخفضة قد تكون مفيدة للتحقق اللاحق.

## الخطوة 5: استخراج النص والتحقق من النتيجة

أخيرًا، نطبع السلسلة المستخرجة. في تطبيق حقيقي قد تكتبها إلى قاعدة بيانات أو تمررها إلى محلل، لكن طباعة النص على وحدة التحكم كافية للعرض.

```java
public class RoiOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create and configure the OCR engine
        OcrEngine ocrEngine = OcrSetup.createEngine();

        // Step 2: Load the image you want to process
        ImageInputStream imageStream = ImageLoader.load("YOUR_DIRECTORY/multi_page_form.png");

        // Step 3: Define where to look – the ROI
        Rectangle regionOfInterest = RoiHelper.defineRoi();

        // Step 4: Run OCR limited to that region
        OcrResult ocrResult = OcrRunner.run(ocrEngine, imageStream, regionOfInterest);

        // Step 5: Show the result
        System.out.println("ROI text:");
        System.out.println(ocrResult.getText());
    }
}
```

### النتيجة المتوقعة

بافتراض أن منطقة الاهتمام تحتوي على العبارة “Invoice #12345”، سترى شيئًا مشابهًا لـ:

```
ROI text:
Invoice #12345
Date: 2026-03-07
Total: $1,250.00
```

إذا لم يتمكن محرك التعرف الضوئي من العثور على أي نص، فإن `ocrResult.getText()` سيعيد سلسلة فارغة – إشارة جيدة لإعادة فحص إحداثيات منطقة الاهتمام أو جودة الصورة.

## معالجة المشكلات الشائعة

| المشكلة | السبب | الحل السريع |
|---------|-------|-------------|
| **مخرجات فارغة** | منطقة الاهتمام خارج حدود الصورة أو الصورة رمادية ذات تباين منخفض. | تحقق من الإحداثيات باستخدام محرر صور؛ زد التباين أو قم بالتحويل إلى ثنائي قبل التعرف. |
| **حروف غير مفهومة** | عدم معالجة التدوير، أو حزمة لغة غير صحيحة. | تأكد من تفعيل `setAutoRotateWithinRegion(true)`؛ حمّل نموذج اللغة المناسب (`engine.getConfig().setLanguage("eng")`). |
| **بطء الأداء** | معالجة الصورة بالكامل بدلاً من منطقة الاهتمام. | مرّر دائمًا كائن `Rectangle` لتحديد مساحة الفحص؛ فكر في تقليل حجم الصور الكبيرة أولاً. |
| **أخطاء نفاد الذاكرة** | تحميل صور ضخمة كبايتات خام. | استخدم واجهات البث (`ImageInputStream`) وإذا كان مدعومًا، اطلب معالجة مقسمة إلى مربعات. |

**نصيحة احترافية:** عند التعامل مع نماذج متعددة الصفحات، احط استدعاء التعرف الضوئي بحلقة تزيد فهرس الصفحة. تسمح معظم مجموعات SDK بإعادة استخدام نفس نسخة `OcrEngine`، مما يوفر وقت التهيئة.

## التعمق – ماذا لو احتجت إلى المزيد؟

- **معالجة دفعات:** اجمع قائمة مسارات الملفات، كرّر عبرها، وخزّن كل نتيجة تعرّف ضوئي في ملف CSV.  
- **منطقة اهتمام ديناميكية:** استخدم OpenCV لاكتشاف حقول النموذج تلقائيًا، ثم مرّر تلك الإحداثيات إلى خطوة التعرف الضوئي.  
- **معالجة لاحقة:** طبّق أنماط regex لتنظيف التواريخ، أرقام الفواتير، أو القيم النقدية المستخرجة من منطقة الاهتمام.  

جميع هذه الامتدادات تُبنى على النمط الأساسي الذي غطيناه للتو: **تحميل صورة للتعرف الضوئي على الحروف**، ضبط **كيفية ضبط التعرف الضوئي**، تعريف منطقة، تشغيل المحرك، ومعالجة النتيجة.

![لقطة شاشة تُظهر منطقة الاهتمام مميزة على نموذج – مثال تحميل صورة للتعرف الضوئي على الحروف](roi-screenshot.png "مثال تحميل صورة للتعرف الضوئي على الحروف")

*نص بديل للصورة: تحميل صورة للتعرف الضوئي على الحروف – منطقة اهتمام مميزة على نموذج عينة.*

## الخلاصة

أصبح لديك الآن مثال كامل وقابل للتنفيذ يوضح كيفية **تحميل صورة للتعرف الضوئي على الحروف** في جافا، وضبط **كيفية ضبط التعرف الضوئي** بشكل صحيح، واستخراج النص من منطقة محددة. الخطوات معيارية، لذا يمكنك استبدال مكتبة التعرف الضوئي أو تعديل منطقة الاهتمام دون الحاجة لإعادة كتابة الكود بالكامل.

في الخطوة التالية، جرّب تجربة صيغ صور مختلفة (TIFF، BMP) أو أضف خطوة ما قبل المعالجة باستخدام OpenCV لتحسين الدقة على المسحات الضوضائية. وإذا كنت مهتمًا بالتعامل مع صفحات متعددة، وسّع الحلقة في `RoiOcrExample` لتكرار فهارس الصفحات.

برمجة سعيدة، ونتمنى أن تكون نتائج التعرف الضوئي واضحة كالكريستال!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}