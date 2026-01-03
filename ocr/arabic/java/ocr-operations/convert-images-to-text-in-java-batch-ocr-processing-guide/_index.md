---
category: general
date: 2026-01-02
description: تحويل الصور إلى نص باستخدام Java و Aspose OCR. إتقان معالجة OCR الدفعية،
  قراءة الصور من المجلد، وتصفية الملفات حسب الامتداد.
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: ar
og_description: تحويل الصور إلى نص بسرعة باستخدام Java. يغطي هذا الدرس معالجة OCR
  على دفعات، قراءة الصور من مجلد، وتصفية الملفات حسب الامتداد.
og_title: تحويل الصور إلى نص في جافا – دليل شامل لتقنية OCR الدفعي
tags:
- OCR
- Java
- Aspose
title: تحويل الصور إلى نص في جافا – دليل معالجة OCR على دفعات
url: /ar/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل الصور إلى نص في جافا – دليل معالجة OCR الدفعي

هل احتجت يومًا إلى **تحويل الصور إلى نص** لكن لم تكن متأكدًا من كيفية التعامل مع العشرات من الملفات في آنٍ واحد؟ لست وحدك—المطورون يواجهون باستمرار صعوبة استخراج البيانات من PNGs و JPGs والمسحات الأخرى. الخبر السار؟ مع Aspose OCR يمكنك إنشاء خط أنابيب معالجة OCR دفعي في دقائق، قراءة الصور من بنية المجلدات، وحتى تصفية الملفات حسب الامتداد بحيث تعمل فقط على ما يهمك.

في هذا الدرس سنبني برنامج جافا مستقل يتجول في دليل، يلتقط كل ملف `.png` أو `.jpg`، يرسل كل صورة إلى Aspose OCR بصورة غير متزامنة، ويطبع النص المستخرج بالترتيب الأصلي. بنهاية الدرس ستحصل على مقتطف قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع يحتاج إلى **تحويل الصور إلى نص** على نطاق واسع.

---

![مثال تحويل الصور إلى نص](https://example.com/convert-images-to-text.png "لقطة شاشة لمخرجات وحدة التحكم في جافا تُظهر النص المحول من ملفات PNG")

## ما ستبنيه

- محرك `AsposeOCR` واحد مشترك بين الخيوط (فعّال وآمن للخطوط).  
- `ParallelRecognizer` يُجري مهام OCR بالتوازي، مثالي لـ **معالجة OCR الدفعي**.  
- منطق **يقرأ الصور من المجلد** باستخدام `java.nio.file.Files`.  
- مرشحات بسيطة **لاستخراج النص من PNG** مع الاستمرار في معالجة JPGs.  
- إغلاق نظيف لمجمع الخيوط الداخلي لتجنب تسرب الموارد.

### المتطلبات المسبقة

- Java 17 (أو أي نسخة LTS حديثة).  
- Maven أو Gradle لجلب مكتبة Aspose OCR.  
- مجلد مليء بصور PNG/JPG تريد معالجتها.  
- إلمام أساسي بـ Java streams—لا شيء معقد مطلوب.

> **نصيحة احترافية:** إذا لم يكن لديك ترخيص بعد، تقدم Aspose مفتاحًا مؤقتًا مجانيًا يمكنك استخدامه للاختبار.

---

## الخطوة 1 – إعداد المشروع وإضافة Aspose OCR

أولاً، أنشئ مشروع Maven جديد (أو Gradle، حسب رغبتك). أضف تبعية Aspose OCR إلى `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **لماذا هذا مهم:** إعلان التبعية مسبقًا يضمن أن المترجم يستطيع رؤية `AsposeOCR` و `ParallelRecognizer` والفئات ذات الصلة. كما يضمن أن نفس الإصدار يُستخدم على جميع الأجهزة، وهو أمر حاسم لـ **معالجة OCR الدفعي** القابلة لإعادة الإنتاج.

بعد انتهاء عملية البناء، قم بتحديث بيئة التطوير المتكاملة ويجب أن ترى حزم Aspose تحت `External Libraries`.

---

## الخطوة 2 – تحويل الصور إلى نص – تهيئة محرك OCR

نحتاج فقط إلى **محرك OCR واحد** طوال عملية التنفيذ. مشاركته بين الخيوط توفر الذاكرة وتسرّع العملية لأن المحرك يحمل حزم اللغات مرة واحدة فقط.

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

> **شرح:** `ParallelRecognizer` يلف المحرك في مجموعة خيوط. عندما تُرسل العديد من الملفات، يحصل كل منها على خيط عمل خاص به، مما يتيح التوازي الحقيقي على المعالجات متعددة النوى.

---

## الخطوة 3 – قراءة الصور من المجلد – استعراض شجرة الدليل

الآن نحتاج إلى **قراءة الصور من المجلد** وجمع كل ملفات PNG أو JPG. تجعلنا واجهة برمجة التطبيقات `Files.walk` نكتب ذلك في سطر واحد، لكننا سنضيف مرشحًا **لاستخراج النص من PNG** فقط عند الحاجة.

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

> **لماذا نُصفي هنا:** استخدام `filter` يتيح لنا **تصفية الملفات حسب الامتداد** مبكرًا، مما يقلل من عمليات الإدخال/الإخراج غير الضرورية لاحقًا. كما يبقي الكود مقروءًا—لا حاجة لتعبيرات regex معقدة.

---

## الخطوة 4 – معالجة OCR الدفعي – إرسال المهام بصورة غير متزامنة

مع قائمة الملفات جاهزة، نُرسل كل مسار إلى `ParallelRecognizer`. تُعيد طريقة `recognizeAsync` كائن `Future<OcrResult>` نحتفظ به لاسترجاعه لاحقًا.

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

> **ما الذي يحدث خلف الكواليس؟** كل استدعاء يضيف مهمة إلى خدمة التنفيذ الداخلية للمُعرّف. تُنفّذ المهام بالتوازي، لذا يمكن معالجة مجلد يحتوي على 100 صورة في جزء صغير من الوقت الذي تستغرقه حلقة أحادية الخيط.

---

## الخطوة 5 – استرجاع النتائج بالترتيب الأصلي – الحفاظ على تسلسل الملفات

نظرًا لأننا خزنّا الـ futures بنفس ترتيب `imagePaths`، يمكننا ببساطة التكرار على القائمة واستدعاء `get()`. يُحجب الاستدعاء فقط حتى تُنتهي المعالجة لتلك الصورة المحددة، مما يحافظ على الترتيب دون الحاجة إلى تتبع إضافي.

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

**عينة من مخرجات وحدة التحكم** (مقتطفة للاختصار):

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

> **معالجة الحالات الحدية:** إذا أطلقت صورة معينة استثناءً (ملف تالف، تنسيق غير مدعوم)، نلتقطه ونستمر في معالجة البقية—عادة أساسية لخطوط أنابيب **معالجة OCR الدفعي** الموثوقة.

---

## الخطوة 6 – التنظيف – إغلاق المُعرّف

لا تنسَ أبدًا إغلاق مجموعة الخيوط الداخلية؛ وإلا قد يبقى JVM معلقًا عند الإغلاق.

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

هذا كل شيء! سيقوم البرنامج الآن باستعراض أي دليل، تصفية ملفات PNG/JPG، تشغيل OCR بالتوازي، وطباعة النتائج.

---

## مثال كامل يعمل

فيما يلي الفئة الكاملة الجاهزة للنسخ واللصق. استبدل `"YOUR_DIRECTORY"` بمسار مجلد الصور الخاص بك وشغّله من بيئة التطوير المتكاملة أو سطر الأوامر.

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

شغّل الفئة، راقب وحدة التحكم وهي تملأ بالسلاسل المستخرجة، واحتفل بحقيقة أنك **قمت بتحويل الصور إلى نص** دون كتابة حلقة واحدة تحجب الإدخال/الإخراج.

---

## الأسئلة المتكررة (FAQs)

**س: هل يمكنني معالجة ملفات PDF أو TIFF أيضًا؟**  
ج: بالتأكيد. يدعم Aspose OCR العديد من الصيغ—فقط أضف امتدادات الملفات المناسبة إلى المرشح في الخطوة 2.

**س: ماذا لو احتجت لغة مختلفة، مثل الإسبانية؟**  
ج: غيّر `RecognitionLanguage.ENGLISH` إلى `RecognitionLanguage.SPANISH`. تأكد من تثبيت حزمة اللغة (تضمّن Aspose معظم اللغات الرئيسية بشكل افتراضي).

**س: مجلدي يحتوي على مجلدات فرعية—هل سيتم فحصها؟**  
ج: نعم. `Files.walk` يتجول في الشجرة بالكامل بشكل متكرر، لذا سيتم مسح كل ملف PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}