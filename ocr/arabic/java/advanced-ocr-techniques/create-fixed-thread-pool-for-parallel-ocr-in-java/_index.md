---
category: general
date: 2026-05-03
description: إنشاء مجموعة مؤشرات ثابتة في جافا لاستخراج النص من الصور بسرعة. تعلم
  كيفية تشغيل OCR، تحويل الصورة إلى نص، وتعزيز الأداء باستخدام معالجة OCR المتوازية.
draft: false
keywords:
- create fixed thread pool
- extract text from images
- how to run OCR
- convert image to text
- parallel OCR processing
language: ar
og_description: إنشاء مجموعة خيوط ثابتة في جافا لاستخراج النص من الصور بسرعة. تعلم
  كيفية تشغيل OCR، تحويل الصورة إلى نص، وتعزيز الأداء باستخدام معالجة OCR المتوازية.
og_title: إنشاء مجموعة خيوط ثابتة للمعالجة المتوازية للـ OCR في جافا
tags:
- Java
- OCR
- Multithreading
title: إنشاء مجموعة خيوط ثابتة للمعالجة المتوازية للـ OCR في جافا
url: /ar/java/advanced-ocr-techniques/create-fixed-thread-pool-for-parallel-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مجموعة خيوط ثابتة لمعالجة OCR المتوازية في جافا

هل احتجت يوماً إلى **إنشاء مجموعة خيوط ثابتة** لتسريع مهام OCR، لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك. في العديد من المشاريع التي تتعامل مع صور كثيرة، تكون نقطة الاختناق هي استدعاء OCR أحادي الخيط، والحل بسيط بشكل مفاجئ: إنشاء مجموعة من خيوط العاملين وتركها تعالج الملفات بشكل متوازي.  

في هذا الدرس ستتعلم كيف **استخراج النص من الصور** باستخدام Aspose OCR، وكيف **تشغيل OCR** بكفاءة، وكيف **تحويل الصورة إلى نص** دون استنزاف وحدة المعالجة المركزية. في النهاية ستحصل على برنامج جافا جاهز للتنفيذ يوضح **معالجة OCR المتوازية** على مجموعة من الصور النموذجية.

## ما ستبنيه

سنقوم بإنشاء تطبيق سطر أوامر صغير يقوم بـ:

* قراءة قائمة بمسارات الصور (PNG، JPG، TIFF، BMP).
* **إنشاء مجموعة خيوط ثابتة** بحجم يساوي عدد نوى المعالج.
* إرسال مهمة OCR لكل صورة.
* جمع النص المستخرج وعرضه في وحدة التحكم.
* إغلاق الـ executor بشكل نظيف.

بدون أدوات بناء خارجية، بدون أطر عمل معقدة—فقط جافا عادية ومكتبة Aspose OCR. إذا كان لديك Java 8+ وبيئة تطوير متكاملة جيدة، فأنت جاهز.

## المتطلبات المسبقة

* **مجموعة تطوير جافا (JDK) 8 أو أحدث** – الكود يستخدم الـ lambdas، لذا الإصدارات الأقدم لن تُترجم.
* **Aspose OCR for Java** – حمّل ملف الـ JAR من موقع Aspose أو أضفه عبر Maven (`com.aspose:aspose-ocr`).
* مجلد يحتوي على بعض صور الاختبار (الكود يشير إلى `YOUR_DIRECTORY`).  
* إلمام أساسي بتزامن جافا (سنشرح البقية).

> *نصيحة محترف:* إذا كنت تستخدم Maven، أضف الاعتماد إلى ملف `pom.xml` ودع IDE يتولى إدارة مسار الفئات.  

---

## الخطوة 1: إضافة الاستيرادات المطلوبة

أولاً، استورد الفئات التي نحتاجها. هذا ليس مجرد قالب؛ كل استيراد يخبر JVM أين يجد محرك OCR، أدوات معالجة الصور، وأدوات التزامن التي تسمح لنا **بإنشاء مجموعة خيوط ثابتة**.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;
```

* `com.aspose.ocr.*` – واجهة برمجة تطبيقات OCR الأساسية.  
* `java.util.*` – مجموعات لتخزين مسارات الصور والنتائج.  
* `java.util.concurrent.*` – حزمة التزامن التي تحتوي على `ExecutorService` و `Future`.

---

## الخطوة 2: تعريف الصور التي سيتم معالجتها

بعد ذلك، نُدرج الملفات التي نريد **استخراج النص من الصور**. استخدام `Arrays.asList` يبقي الكود مختصرًا ويسمح لك بتبديل الدليل الخاص بك دون تعديل باقي المنطق.

```java
List<String> imagePaths = Arrays.asList(
        "YOUR_DIRECTORY/image1.png",
        "YOUR_DIRECTORY/image2.jpg",
        "YOUR_DIRECTORY/image3.tif",
        "YOUR_DIRECTORY/image4.bmp"
);
```

لا تتردد في إضافة المزيد من الإدخالات؛ مجموعة الخيوط ستتوسع تلقائيًا بناءً على عدد نوى المعالج المتاحة لديك.

---

## الخطوة 3: **إنشاء مجموعة خيوط ثابتة** مطابقة لعدد نوى المعالج

هذا هو جوهر الدرس. نطلب من وقت التشغيل معرفة عدد النوى المتاحة ونطلب من مصنع `Executors` أن يمنحنا مجموعة بحجم ذلك العدد بالضبط. لماذا ثابتة؟ لأن عددًا متوقعًا من الخيوط يمنع “انفجار الخيوط” الذي قد يحرم نظام التشغيل من الموارد.

```java
int coreCount = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(coreCount);
```

* `availableProcessors()` تُعيد عدد النوى المنطقية (بما فيها الـ hyper‑threads).  
* `newFixedThreadPool(coreCount)` يضمن أننا لا نتجاوز قدرة المعالج، وهو الطريقة الأكثر أمانًا لـ **تشغيل OCR** بشكل متوازي.

---

## الخطوة 4: إرسال مهمة OCR لكل صورة

الآن نحول كل مسار ملف إلى كائن قابل للنداء (`callable`) يقوم **بتشغيل OCR**، يتعرف على النص، ويعيد النتيجة. لاحظ أننا ننشئ `OcrEngine` جديد داخل الـ lambda—هذا يمنع مشاركة حالة المحرك غير الآمنة بين الخيوط.

```java
List<Future<String>> ocrResults = new ArrayList<>();
for (String path : imagePaths) {
    ocrResults.add(executor.submit(() -> {
        OcrEngine engine = new OcrEngine();          // fresh engine per task
        engine.setImage(ImageStream.fromFile(path));
        engine.getLanguage().setEnglish(true);
        return engine.recognize() ? engine.getText()
                                   : "Failed: " + path;
    }));
}
```

* كل استدعاء `submit` يسلّم الـ lambda إلى المجموعة، التي تُجدوله على خيط خامل.  
* كائنات `Future<String>` تتيح لنا استرجاع النص المستخرج لاحقًا، مع الحفاظ على الترتيب إذا احتجت ذلك.

---

## الخطوة 5: استرجاع وعرض النص المستخرج

بعد أن تُضاف جميع المهام إلى القائمة، نمر ببساطة على قائمة الـ `Future`، مستدعين `get()` للانتظار حتى ينتهي كل عمل OCR. هنا يصبح خطوة **تحويل الصورة إلى نص** واضحة لك: استدعاء `engine.getText()` يُعيد السلسلة النصية الخام.

```java
for (Future<String> result : ocrResults) {
    System.out.println("OCR result:\n" + result.get());
}
```

نموذج الإخراج في وحدة التحكم يكون كالتالي:

```
OCR result:
Hello world!
OCR result:
Invoice #12345
Date: 2026‑04‑30
...
```

إذا فشل ملف ما (مثلاً كان معطوبًا)، ستظهر سطر يبدأ بـ `Failed:` متبوعًا بالمسار—مفيد لتصحيح الأخطاء بسرعة.

---

## الخطوة 6: تنظيف خدمة الـ Executor

لا تنسَ إغلاق المجموعة؛ وإلا قد يبقى الـ JVM قيد التشغيل معتقدًا أن هناك عملًا مستمرًا. إغلاقٍ منظم يسمح لأي مهمة جارية بالانتهاء قبل انتهاء العملية.

```java
executor.shutdown();
```

يمكنك أيضًا استدعاء `awaitTermination` إذا أردت فرض مهلة زمنية، لكن بالنسبة لمعظم الأدوات سطر الأوامر يكفي `shutdown()` العادي.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ. انسخه إلى ملف باسم `ParallelOcrTutorial.java`، عدّل مسارات الصور، ثم شغّله باستخدام `javac` + `java` كالمعتاد.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Define the images to be processed
        List<String> imagePaths = Arrays.asList(
                "YOUR_DIRECTORY/image1.png",
                "YOUR_DIRECTORY/image2.jpg",
                "YOUR_DIRECTORY/image3.tif",
                "YOUR_DIRECTORY/image4.bmp"
        );

        // Step 3: Create a fixed‑size thread pool matching the CPU cores
        int coreCount = Runtime.getRuntime().availableProcessors();
        ExecutorService executor = Executors.newFixedThreadPool(coreCount);

        // Step 4: Submit an OCR task for each image
        List<Future<String>> ocrResults = new ArrayList<>();
        for (String path : imagePaths) {
            ocrResults.add(executor.submit(() -> {
                OcrEngine engine = new OcrEngine();          // fresh engine per task
                engine.setImage(ImageStream.fromFile(path));
                engine.getLanguage().setEnglish(true);
                return engine.recognize() ? engine.getText()
                                           : "Failed: " + path;
            }));
        }

        // Step 5: Retrieve and display the recognized text
        for (Future<String> result : ocrResults) {
            System.out.println("OCR result:\n" + result.get());
        }

        // Step 6: Clean up the executor service
        executor.shutdown();
    }
}
```

**النتيجة المتوقعة:** طباعة المحتوى النصي لكل صورة في وحدة التحكم، بنفس ترتيب قائمة `imagePaths`. إذا تعذّر معالجة أي صورة، ستظهر إشعار فشل بدلاً من سطر فارغ.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو كان لدي عدد صور أكبر من عدد الخيوط؟

ستقوم مجموعة الخيوط الثابتة تلقائيًا بصفّ المهام الزائدة. بمجرد أن ينتهي خيط من مهمة OCR الحالية، يلتقط المهمة التالية. سلوك الصفّ هذا هو جوهر **معالجة OCR المتوازية**—تحصل على أقصى إنتاجية دون إغراق المعالج.

### هل يمكنني تغيير اللغة؟

بالطبع. استبدل `engine.getLanguage().setEnglish(true);` بالعلامة اللغوية المناسبة، مثل `setFrench(true)` أو فعّل عدة لغات باستدعاء عدة setters قبل `recognize()`.

### كيف أتعامل مع الصور الكبيرة جدًا؟

الملفات الضخمة قد تستهلك الكثير من الذاكرة لكل خيط. إذا لاحظت `OutOfMemoryError`، فكر في تقليل حجم الصورة قبل تمريرها إلى المحرك، أو زِد حجم الـ heap باستخدام `-Xmx`. خيار آخر هو استخدام **مجموعة خيوط مخزنة** (`cached thread pool`) ( 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}