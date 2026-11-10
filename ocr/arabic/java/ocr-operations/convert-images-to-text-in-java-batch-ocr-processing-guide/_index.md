---
category: general
date: 2026-08-28
description: تعلم كيفية استخراج النص من صور png في Java باستخدام Aspose OCR. يغطي
  هذا الدليل معالجة OCR الدفعي، قراءة الصور من مجلد، وتصفية الملفات حسب الامتداد.
draft: false
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
lastmod: 2026-08-28
og_description: تعلم كيفية استخراج النص من صور png في Java باستخدام Aspose OCR. يغطي
  هذا الدليل معالجة OCR الدفعي، قراءة الصور من مجلد، وتصفية الملفات حسب الامتداد.
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: كيفية استخراج النص من png في Java – دليل OCR الدفعي
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Learn how to extract text from png images in Java using Aspose OCR.
    This tutorial covers batch OCR processing, reading images from a folder, and filtering
    files by extension.
  headline: How to extract text from png in Java – batch OCR guide
  type: TechArticle
- questions:
  - answer: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP,
      and GIF—so just add the desired extensions to the filter in the directory‑walk
      step.
    question: Can I process PDFs or TIFFs as well?
  - answer: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`
      (or any supported language). The language packs are bundled with the library,
      so no extra download is required.
    question: What if I need a language other than English, such as Spanish?
  - answer: Yes. `Files.walk` traverses the entire tree recursively, so every nested
      PNG/J
    question: My folder contains sub‑folders—will they be scanned?
  - answer: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This
      tells the engine to read the image in chunks, dramatically reducing peak memory
      usage.
    question: How do I handle extremely large images that exceed 200 MB?
  - answer: Yes. When constructing `ParallelRecognizer`, pass the desired maximum
      thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine,
      4)`).
    question: Is there a way to limit the number of concurrent OCR threads?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: كيفية استخراج النص من png في Java – دليل OCR الدفعي
url: /ar/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخراج النص من png في Java – دليل OCR الدفعي

إذا كنت قد احتجت يومًا إلى **extract text from png** ولكنك لم تكن متأكدًا من كيفية توسيع العملية إلى ما بعد عدد قليل من الصور، فأنت في المكان الصحيح. يبدأ العديد من المطورين باستدعاء OCR لصورة واحدة بسرعة ويواجهون جدران أداء عندما ينمو المجلد إلى عشرات أو مئات الملفات. باستخدام Aspose OCR for Java يمكنك إنشاء خط أنابيب OCR دفعي قوي يمشي عبر دليل، يفلتر فقط أنواع الصور التي تهمك، ينفذ التعرف بشكل متوازي، ويعيد النتائج بنفس ترتيب ملفات المصدر. بنهاية هذا الدليل ستحصل على مقتطف Java جاهز للإسقاط يتعامل مع **batch OCR processing** بشكل موثوق وفعال.

![مثال تحويل الصور إلى نص](https://example.com/convert-images-to-text.png "لقطة شاشة لمخرجات وحدة تحكم Java تُظهر النص المستخرج من ملفات PNG")

## إجابات سريعة
- **ما المكتبة التي تتعامل مع OCR؟** Aspose OCR for Java.
- **هل يمكنني معالجة PNG و JPG معًا؟** نعم – العينة تقوم بفلترة كلا الامتدادين.
- **هل محرك OCR آمن للخطوط المتعددة؟** مثيل `AsposeOCR` المشترك الواحد آمن للاستخدام المتزامن.
- **هل أحتاج إلى ترخيص للاختبار؟** مفتاح مؤقت مجاني متاح من Aspose.
- **هل سيتم فحص المجلدات الفرعية تلقائيًا؟** `Files.walk` يتجول في الشجرة بأكملها بشكل متكرر.

## ما هو استخراج النص من png؟

`extract text from png` يشير إلى عملية تطبيق التعرف الضوئي على الأحرف (OCR) على ملفات Portable Network Graphics بحيث تصبح الأحرف الظاهرة قابلة للبحث وسلاسل قابلة للتحرير. محرك Aspose OCR يقرأ بيانات البكسل، يحدد أشكال الحروف، ويعيد نص Unicode في استدعاء طريقة واحد.

## لماذا نستخدم Aspose OCR for Java؟

Aspose OCR يدعم **30+ لغة**، يعالج ما يصل إلى **500 صورة في الدقيقة** على خادم قياسي بثمانية أنوية، ويمكنه التعامل مع ملفات تصل إلى **200 MB** دون تحميل الصورة بالكامل في الذاكرة. هذه القدرات المرقمة تعني أنك تستطيع تشغيل وظائف دفعية واسعة النطاق على عتاد عادي دون مواجهة حدود الذاكرة.

## المتطلبات المسبقة
- Java 17 (أو أي نسخة LTS حديثة).
- Maven أو Gradle لإدارة التبعيات.
- دليل يحتوي على صور PNG/JPG ترغب في معالجتها.
- إلمام أساسي بـ Java streams وحزمة `java.nio.file`.
- (اختياري) مفتاح ترخيص مؤقت لـ Aspose OCR للتقييم.

> **نصيحة احترافية:** المفتاح المؤقت المجاني ينتهي صلاحيته بعد 30 يومًا، لكنه يمنحك وصولًا كاملًا إلى API للاختبار.

## كيف يحافظ خط أنابيب OCR الدفعي على الترتيب؟

`Future<OcrResult>` يمثل نتيجة OCR معلقة يمكن استرجاعها بمجرد انتهاء المعالجة. يحافظ خط الأنابيب على ترتيب الملفات الأصلي عن طريق تخزين كائنات `Future<OcrResult>` في قائمة تعكس ترتيب مجموعة `Path` المدخلة. عندما تتكرر على الـ futures وتستدعي `get()`، كل استدعاء يحجب فقط للصور المقابلة، لذا يتطابق تسلسل الإخراج مع تسلسل الإدخال دون الحاجة إلى منطق فرز إضافي.

## ما هو Aspose OCR for Java؟

`AsposeOCR` هو الفئة الأساسية لمكتبة Aspose OCR التي تغلف جميع حزم اللغات، إعدادات التعرف، والموارد الأصلية الداخلية. صُممت لتُنشأ مرة واحدة طوال عمر التطبيق وتُشارك بأمان عبر عدة خيوط. لأن تحميل بيانات اللغة يتم مرة واحدة فقط، فإن إعادة استخدام نفس المثيل يقلل من عبء التهيئة ويحسن معدل النقل للعمليات الدفعية.

## كيفية إعداد المشروع وإضافة Aspose OCR

أولاً، أنشئ مشروع Maven (أو Gradle) وأضف تبعية Aspose OCR إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **لماذا هذا مهم:** إعلان التبعية مسبقًا يضمن أن المترجم يستطيع رؤية `AsposeOCR`، `ParallelRecognizer`، والفئات ذات الصلة. كما يضمن أن نفس الإصدار يُستخدم عبر جميع الأجهزة، وهو أمر حاسم لمعالجة **batch OCR processing** القابلة لإعادة الإنتاج.

قم بتحديث IDE بعد إكمال البناء؛ يجب الآن أن ترى حزم Aspose تحت **External Libraries**.

## كيفية تهيئة محرك OCR – مشاركة مثيل واحد

`AsposeOCR` هو فئة محرك OCR الرئيسية التي توفرها مكتبة Aspose OCR. نحتاج فقط إلى **مثيل واحد** من محرك OCR لكامل التشغيل. مشاركة هذا المثيل عبر الخيوط توفر الذاكرة وتسرّع العملية لأن المحرك يحمل حزم اللغات مرة واحدة فقط.

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

`AsposeOCR` آمن للخطوط المتعددة، لذا يمكنك تمريره بأمان إلى `ParallelRecognizer` الذي سيدير مجموعة من خيوط العامل.

> **شرح:** `ParallelRecognizer` يلف المحرك في مجموعة خيوط. عندما تُرسل العديد من الملفات، يحصل كل منها على خيط عامل خاص به، مما يتيح التوازي الحقيقي على المعالجات متعددة الأنوية.

## كيفية قراءة الصور من المجلد – استعراض شجرة الدليل

`Files.walk` هي طريقة في Java NIO تتجول بشكل متكرر في شجرة الملفات وتعيد تدفقًا من كائنات `Path`. الآن نحتاج إلى **قراءة الصور من المجلد** وجمع كل PNG أو JPG. تجعلنا واجهة `Files.walk` نفعل ذلك بسطر واحد، لكننا سنضيف فلترًا لـ **extract text from png** فقط عند الحاجة.

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **لماذا نفلتر هنا:** استخدام `filter` يسمح لنا **بفلترة الملفات حسب الامتداد** مبكرًا، مما يقلل من عمليات الإدخال/الإخراج غير الضرورية لاحقًا. كما يبقي الكود مقروءًا—بدون حاجة إلى تعبيرات regex معقدة.

## كيفية تقديم وظائف OCR بشكل غير متزامن

`recognizeAsync` يرسل صورة إلى محرك OCR للمعالجة غير المتزامنة ويعيد `Future<OcrResult>` يمثل النتيجة المعلقة. مع قائمة الملفات جاهزة، ندفع كل مسار إلى `ParallelRecognizer`. طريقة `recognizeAsync` تعيد `Future<OcrResult>` التي نخزنها لاسترجاعها لاحقًا.

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **ما الذي يحدث خلف الكواليس؟** كل استدعاء يضيف مهمة إلى خدمة التنفيذ الداخلية للمعرف. تُنفذ المهام بشكل متوازي، لذا يمكن لمجلد يحتوي على 100 صورة أن يُعالج في جزء صغير من الوقت مقارنةً بحلقة أحادية الخيط.

## كيفية استرجاع النتائج مع الحفاظ على تسلسل الملفات

`Future<OcrResult>` يحمل نتيجة مهمة OCR غير المتزامنة ويوفر طريقة `get()` للحصول على النص المعترف به. لأننا خزنّا الـ futures بنفس ترتيب `imagePaths`، يمكننا ببساطة التكرار على القائمة واستدعاء `get()`. الاستدعاء يحجب فقط حتى تكتمل معالجة تلك الصورة المحددة، مما يحافظ على الترتيب دون حاجة إلى تتبع إضافي.

```java
for (int i = 0; i < futures.size(); i++) {
    try {
        OcrResult result = futures.get(i).get();
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println("Text: " + result.getText());
    } catch (Exception e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**عينة مخرجات وحدة التحكم** (مقتصرة للوجز):

```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **معالجة الحالات الحدية:** إذا أطلقت صورة معينة استثناءً (ملف تالف، تنسيق غير مدعوم)، نلتقطه ونستمر في معالجة البقية—عادة أساسية لخطوط **batch OCR processing** الموثوقة.

## كيفية تنظيف الموارد – إغلاق المعرف

`ParallelRecognizer.shutdown()` يوقف مجموعة الخيوط الداخلية، مما يضمن إكمال جميع مهام OCR قبل خروج التطبيق. لا تنسَ إغلاق مجموعة الخيوط الداخلية؛ وإلا قد يتعطل JVM عند الإغلاق.

```java
recognizer.shutdown();
```

هذا كل شيء! الآن البرنامج يتجول في أي دليل، يفلتر ملفات PNG/JPG، ينفذ OCR بشكل متوازي، ويطبع النتائج بالترتيب الأصلي.

---

## مثال كامل جاهز للتنفيذ (نسخ‑ولصق)

فيما يلي الفئة Java الكاملة الجاهزة للتشغيل. استبدل `"YOUR_DIRECTORY"` بمسار مجلد الصور الخاص بك وشغّله من IDE أو سطر الأوامر.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class BatchOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine (single shared instance)
        AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");

        // Create a parallel recognizer that uses a thread pool
        ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine,
                Runtime.getRuntime().availableProcessors());

        // Walk the directory and collect PNG/JPG files
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(Files::isRegularFile)
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        // Submit OCR jobs asynchronously
        List<Future<OcrResult>> futures = new ArrayList<>();
        for (Path imagePath : imagePaths) {
            futures.add(recognizer.recognizeAsync(imagePath));
        }

        // Retrieve results in the original order
        for (int i = 0; i < futures.size(); i++) {
            try {
                OcrResult result = futures.get(i).get();
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println("Text: " + result.getText());
            } catch (Exception e) {
                System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Clean up the recognizer's thread pool
        recognizer.shutdown();
    }
}
```

شغّل الفئة، راقب وحدة التحكم تمتلئ بالسلاسل المستخرجة، واحتفل بحقيقة أنك **converted images to text** دون كتابة حلقة واحدة تحجب على I/O.

---

## الأسئلة المتكررة (FAQs)

**س: هل يمكنني معالجة PDFs أو TIFFs أيضًا؟**  
ج: بالتأكيد. Aspose OCR يدعم أكثر من 30 تنسيقًا—بما في ذلك PDF، TIFF، BMP، و GIF—فما عليك سوى إضافة الامتدادات المطلوبة إلى الفلتر في خطوة استعراض الدليل.

**س: ماذا لو احتجت إلى لغة غير الإنجليزية، مثل الإسبانية؟**  
ج: غيّر `RecognitionLanguage.ENGLISH` إلى `RecognitionLanguage.SPANISH` (أو أي لغة مدعومة). حزم اللغات مدمجة مع المكتبة، لذا لا يلزم تحميل إضافي.

**س: مجلدي يحتوي على مجلدات فرعية—هل سيتم فحصها؟**  
ج: نعم. `Files.walk` يتجول في الشجرة بأكملها بشكل متكرر، لذا كل PNG/J

**س: كيف أتعامل مع صور ضخمة جدًا تتجاوز 200 MB؟**  
ج: فعّل وضع البث عن طريق استدعاء `ocrEngine.setUseStreaming(true)`. هذا يخبر المحرك بقراءة الصورة على دفعات، مما يقلل بشكل كبير من استهلاك الذاكرة القصوى.

**س: هل هناك طريقة لتحديد عدد خيوط OCR المتزامنة؟**  
ج: نعم. عند إنشاء `ParallelRecognizer`، مرّر عدد الخيوط الأقصى المطلوب كمعامل ثانٍ (مثال: `new ParallelRecognizer(ocrEngine, 4)`).

---

**آخر تحديث:** 2026-08-28  
**تم الاختبار مع:** Aspose OCR for Java 24.10  
**المؤلف:** Aspose  






```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

## دروس ذات صلة

- [تحويل الصور إلى نص في دليل معالجة OCR الدفعي بـ Java](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [قراءة النص من الصورة في Java – دليل Aspose OCR الكامل](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [استخراج النص من الصور باستخدام Aspose.OCR – الأحرف المسموح بها](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}