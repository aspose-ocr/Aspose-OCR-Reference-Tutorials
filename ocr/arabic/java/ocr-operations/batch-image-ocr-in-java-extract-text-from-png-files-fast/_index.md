---
category: general
date: 2026-02-14
description: 'التعرف الضوئي على الحروف للصور على دفعات بسهولة: تعلم كيفية استخراج
  النص من ملفات PNG باستخدام Aspose OCR مع المعالجة المتوازية في Java.'
draft: false
keywords:
- batch image OCR
- extract text from png
- parallel OCR Java
- Aspose OCR async
- OCR batch processing
language: ar
og_description: دورة تعليمية لمعالجة OCR للصور على دفعات تُظهر كيفية استخراج النص
  من ملفات PNG باستخدام واجهة Aspose OCR غير المتزامنة في Java.
og_title: التعرف الضوئي على الأحرف للصور دفعة واحدة في جافا – استخراج نص PNG سريع
tags:
- Java
- OCR
- Aspose
- Image Processing
title: التعرف الضوئي على الحروف للصور دفعةً في جافا – استخراج النص من ملفات PNG بسرعة
url: /ar/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/
---

.

Now translate headings and paragraphs.

Will produce Arabic text.

Be careful with markdown syntax.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف الضوئي على الحروف للصور دفعةً في جافا – استخراج النص من ملفات PNG بسرعة

هل احتجت يومًا إلى تشغيل **التعرف الضوئي على الحروف للصور دفعةً** على مجلد يحتوي على مسح PNG لكنك كنت قلقًا بشأن السرعة؟ لست وحدك. في العديد من المشاريع الواقعية—رقمنة الفواتير، أرشفة الكتب الممسوحة، أو معالجة الإيصالات—يجب على المطورين **استخراج النص من PNG** بسرعة وبشكل موثوق.  

الأخبار السارة؟ باستخدام واجهة Aspose OCR غير المتزامنة يمكنك إنشاء خط أنابيب OCR متوازي ببضع أسطر من جافا فقط. في هذا الدليل سنستعرض الحل الكامل القابل للتنفيذ، نشرح لماذا كل جزء مهم، ونظهر لك كيفية التحقق من النتائج. بنهاية القراءة ستحصل على برنامج مستقل يعالج دفعة كاملة من ملفات PNG بشكل متوازي، ويعطيك نصًا نظيفًا ومصححًا إملائيًا.

## ما ستتعلمه

- كيفية سرد ملفات PNG للمعالجة الدفعة  
- ضبط `OcrEngine` من Aspose للغة الإنجليزية وتصحيح الإملاء  
- تشغيل OCR بشكل غير متزامن باستخدام `processAsync` ومعالجة نتيجة `Future`  
- قراءة وعرض النص المعترف به لكل صورة  
- نصائح للتوسع، معالجة الأخطاء، وتحسين الأداء  

### المتطلبات المسبقة

- تثبيت Java 8 أو أحدث (الكود يستخدم حزمة `java.util.concurrent` القياسية)  
- رخصة Aspose OCR for Java أو تجربة مجانية (حملها من موقع Aspose)  
- مجلد يحتوي على بعض لقطات PNG أو صفحات ممسوحة تريد اختبارها  

الآن، لنبدأ.

## الخطوة 1 – جمع ملفات PNG الخاصة بك للدفعة

قبل أن يتمكن محرك OCR من القيام بأي عمل، يحتاج إلى معرفة الصور التي سيعالجها. أبسط طريقة هي بناء `List<String>` من مسارات الملفات المطلقة أو النسبية.

```java
// Step 1: Prepare a list of PNG files you want to run OCR on
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png",
        "YOUR_DIRECTORY/page4.png");
```

**لماذا هذا مهم:**  
إنشاء القائمة مسبقًا يسمح للمحرك بجدولة كل ملف بشكل مستقل، وهو أساس المعالجة الدفعة الحقيقية. إذا احتجت لاحقًا إلى مسح دليل ديناميكيًا، ما عليك سوى استبدال `Arrays.asList` الثابت بـ `Files.walk` stream.

## الخطوة 2 – تهيئة وضبط محرك Aspose OCR

`OcrEngine` من Aspose قابل للتكوين بدرجة عالية. هنا نضبط اللغة إلى الإنجليزية ونفعل تصحيح الإملاء—خياران يحسنان جودة النص المستخرج بشكل كبير، خاصةً من مسحات PNG الضوضائية.

```java
// Step 2: Create and configure the OCR engine
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getEngineOptions()
         .setLanguage(OcrLanguage.ENGLISH)          // English language model
         .setSpellCorrectionEnabled(true);          // Enable spell‑checking
```

**لماذا هذه الإعدادات:**  
- **اختيار اللغة** يخبر المحرك بمجموعة الأحرف والقاموس الذي سيستخدمه، مما يقلل من الأخطاء غير الصحيحة.  
- **تصحيح الإملاء** يلتقط الأخطاء الشائعة في OCR (مثل “1” مقابل “l”) دون الحاجة إلى معالجة لاحقة للنتيجة.

> **نصيحة احترافية:** إذا كانت صورك تحتوي على لغات متعددة، يمكنك تمرير قائمة مثل `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.FRENCH)`.

## الخطوة 3 – إطلاق المعالجة الدفعة غير المتزامنة

العمل الشاق يحدث في `processAsync`. تُعيد هذه الدالة `Future<List<OcrResult>>`، مما يسمح للخيط الرئيسي بالاستمرار في أداء مهام أخرى بينما يعمل OCR في الخلفية.

```java
// Step 3: Start asynchronous processing of the image batch
Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

// (Optional) Do something useful while OCR runs, e.g., log progress, load UI, etc.
System.out.println("OCR started – you can perform other tasks now...");
```

**لماذا غير متزامن:**  
تشغيل OCR بشكل تسلسلي يمكن أن يكون بطيئًا جدًا—كل ملف PNG قد يستغرق ثانية أو أكثر. عبر تفويض العمل إلى مجموعة خيوط، تستغل نوى المعالج المتعددة وتقلل زمن التنفيذ الكلي بشكل كبير.

## الخطوة 4 – استرجاع النتائج عندما تكون جاهزة

عندما تكون مستعدًا لاستهلاك المخرجات، ما عليك سوى استدعاء `get()` على كائن `Future`. هذا الاستدعاء يحجب التنفيذ فقط حتى ينتهي OCR، ثم يُعيد لك قائمة من كائنات `OcrResult` بنفس ترتيب القائمة المدخلة.

```java
// Step 4: Wait for all results and retrieve them
List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion
```

**معالجة المهلات:**  
إذا أردت تجنب الحجب غير المحدود، استخدم `ocrFuture.get(60, TimeUnit.SECONDS)` وامسك `TimeoutException` لتنفيذ خطة احتياطية.

## الخطوة 5 – عرض النص المعترف به لكل PNG

الآن بعد أن حصلت على النتائج، قم بالتكرار فوقها واطبع النص المستخرج جنبًا إلى جنب مع اسم الملف الأصلي. هنا تقوم أخيرًا **باستخراج النص من PNG**.

```java
// Step 5: Show the OCR output for each image
for (int i = 0; i < ocrResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(ocrResults.get(i).getText());
    System.out.println("---");
}
```

**مثال على المخرجات المتوقعة**

```
File: YOUR_DIRECTORY/page1.png
Invoice #12345
Date: 2024‑03‑01
Total: $1,250.00
---
File: YOUR_DIRECTORY/page2.png
...
```

إذا لم يتمكن محرك OCR من التعرف على صفحة، فإن `getText()` المقابل سيُعيد سلسلة فارغة—من الجيد دائمًا التحقق من ذلك في كود الإنتاج.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ الذي يجمع كل الأجزاء معًا. انسخه والصقه في ملف باسم `ParallelOcrDemo.java`، استبدل `YOUR_DIRECTORY` بمسار مجلد PNG الخاص بك، ثم نفّذ `javac ParallelOcrDemo.java && java ParallelOcrDemo`.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Prepare a list of image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png",
                "YOUR_DIRECTORY/page4.png");

        // Step 2: Create and configure the OCR engine (set language and enable spell‑checking)
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineOptions()
                 .setLanguage(OcrLanguage.ENGLISH)
                 .setSpellCorrectionEnabled(true);

        // Step 3: Start asynchronous processing of the image batch
        Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

        // (Optional) Perform other work here while OCR runs in the background...
        System.out.println("OCR processing started in background...");

        // Step 4: Wait for all results and retrieve them
        List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion

        // Step 5: Display the recognized text for each file
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

### تشغيل العرض التجريبي

1. **التجميع** – `javac -cp "aspose-ocr.jar" ParallelOcrDemo.java`  
2. **التنفيذ** – `java -cp ".:aspose-ocr.jar" ParallelOcrDemo`  

يجب أن ترى كل اسم ملف PNG متبوعًا بالنص المستخرج، مفصولًا بشرطات.  

> **ملاحظة:** إذا صادفت `LicenseException`، تأكد من تحميل رخصة Aspose قبل إنشاء المحرك:

```java
License lic = new License();
lic.setLicense("Aspose.OCR.Java.lic");
```

## التوسع – نصائح للـ OCR الدفعي في العالم الحقيقي

| الحالة | التوصية |
|-----------|----------------|
| **مئات ملفات PNG** | زيادة حجم مجموعة الخيوط عبر `ocrEngine.setThreadPoolSize(8)` (أو أكثر، بحسب عدد نوى المعالج). |
| **قيود الذاكرة** | معالجة الملفات على دفعات أصغر (مثلاً دفعات من 50) وإطلاق قائمة `OcrResult` بعد كل دفعة. |
| **جودة الصورة المتغيرة** | تفعيل `setPreprocessingOptions` لتدوير تلقائي، تصحيح الميل، أو تحسين التباين قبل التعرف. |
| **لغات متعددة** | استدعاء `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.SPANISH)` وإمكانية ضبط قاموس مخصص. |
| **معالجة الأخطاء** | احط `ocrFuture.get()` بكتلة try‑catch لـ `ExecutionException` لتسجيل الملفات الفاشلة دون إيقاف الدفعة بالكامل. |

هذه الاستراتيجيات تحافظ على خط أنابيب **التعرف الضوئي على الحروف للصور دفعةً** قويًا، حتى عندما يزداد حجم مجموعة الإدخال.

## الأسئلة المتكررة

**س: هل يعمل هذا مع ملفات JPEG أو TIFF؟**  
ج: بالتأكيد. طريقة `processAsync` تقبل أي تنسيق تدعمه Aspose OCR (PNG، JPEG، TIFF، BMP، إلخ). فقط غيّر امتدادات الملفات في قائمتك.

**س: ماذا لو أردت الحفاظ على التخطيط (جداول، أعمدة)؟**  
ج: توفر Aspose OCR طريقة `getLayoutResult()` التي تُعيد بيانات موضعية. يمكنك إعادة بناء الجداول بتحليل الصناديق المحيطة بكل كلمة.

**س: هل يمكن تشغيله على منصة بدون خادم؟**  
ج: نعم—ما عليك سوى حزم الـ JAR مع مكتبة Aspose ونشره على AWS Lambda أو Azure Functions أو Google Cloud Functions. تذكّر تخصيص ذاكرة الدالة بما يكفي لمجموعة خيوط OCR.

## الخلاصة

أصبح لديك الآن حل **التعرف الضوئي على الحروف للصور دفعةً** كامل ومستقل يُستخرج **النص من PNG** بكفاءة باستخدام واجهة Aspose OCR غير المتزامنة في جافا. غطى الدليل كل شيء من إعداد قائمة الملفات إلى ضبط اللغة وتصحيح الإملاء، وإطلاق المعالجة المتوازية، ومعالجة النتائج، وتوسيع الخط الأنابيب لأحمال الإنتاج.

هل أنت مستعد للخطوة التالية؟ جرّب تغيير اللغة إلى الفرنسية، جرب القواميس المخصصة، أو دمج المخرجات في فهرس ElasticSearch قابل للبحث. السماء هي الحد عندما تجمع بين OCR دفعي سريع وتزامن جافا الحديث.

برمجة سعيدة، ولتكن استخراج النصوص سريعًا ودقيقًا! 

![Diagram showing parallel OCR workers handling multiple PNG files](/images/batch-ocr-diagram.png){: .center alt="مخطط معالجة OCR المتوازي للملفات PNG"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}