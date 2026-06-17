---
category: general
date: 2026-02-17
description: تعلم كيفية استخدام مجموعة خيوط ثابتة في جافا لاستخراج النص من صور PNG
  باستخدام معالجة OCR المتوازية وإغلاق خدمة التنفيذ بشكل صحيح.
draft: false
keywords:
- fixed thread pool java
- extract text from png
- parallel ocr processing
- convert scanned pages text
- shut down executor service
language: ar
og_description: اكتشف كيف يمكن لتجمع خيوط ثابت في جافا استخراج النص من صور PNG بشكل
  متوازي، وتحويل نص الصفحات الممسوحة ضوئياً، وإغلاق خدمة التنفيذ بأمان.
og_title: مجموعة خيوط ثابتة جافا – OCR متوازي لملف PNG
tags:
- java
- ocr
- multithreading
- aspose
title: مجموعة خيوط ثابتة في جافا – OCR متوازي لملفات PNG
url: /ar/java/advanced-ocr-techniques/fixed-thread-pool-java-parallel-ocr-for-png/
---

careful to keep markdown formatting exactly, including spaces.

Let's construct final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# fixed thread pool java – OCR متوازي لملفات PNG

هل تساءلت يومًا كيف تُسرّع OCR لمجموعة من ملفات PNG باستخدام **fixed thread pool java**؟ في هذا الدرس سنستعرض **extract text from PNG** للصور بشكل متوازي، **convert scanned pages text** إلى سلاسل قابلة للتحرير، وسنقوم بأمان **shut down executor service** بمجرد انتهاء العمل.

إذا كنت قد حدقت يومًا في حلقة أحادية الخيط تستغرق دقائق، فأنت تعرف الإحباط من الانتظار حتى تنتهي كل صفحة قبل أن تبدأ التالية. الخبر السار؟ ببضع أسطر من Java و Aspose OCR يمكنك استغلال قوة جميع نوى المعالج، وتحويل تلك الصفحات الممسوحة إلى نص قابل للبحث، والحفاظ على استجابة تطبيقك.

فيما يلي مثال كامل جاهز للتنفيذ، بالإضافة إلى شرح لماذا كل جزء مهم، الأخطاء الشائعة، ونصائح يمكنك تطبيقها على أي مكتبة OCR.

---

## ما ستحتاجه

- **Java 17** (أو أي JDK حديث) – يستخدم الكود بنية `var` الحديثة بشكل محدود، لكنه يعمل على الإصدارات القديمة أيضًا.  
- **Aspose.OCR for Java** المكتبة – يمكنك الحصول عليها من Maven Central أو تنزيل نسخة تجريبية من Aspose.  
- مجموعة من ملفات **PNG** التي تريد معالجتها – فكر في إيصالات مسح ضوئي، صفحات كتب، أو لقطات شاشة.  
- إلمام أساسي بـ Java concurrency – ليس ضروريًا، لكنه مفيد.  

هذا كل شيء. لا خدمات خارجية، لا Docker، فقط Java عادي وقليل من سحر تعدد الخيوط.

## الخطوة 1: إضافة تبعية Aspose OCR والترخيص (اختياري)

أولاً، تأكد من أن ملف JAR الخاص بـ Aspose OCR موجود في classpath. إذا كنت تستخدم Maven، أضف:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

إذا لم يكن لديك ترخيص، ستعمل المكتبة في وضع التقييم؛ الكود يعمل بنفس الطريقة. لتحميل ترخيص (مستحسن للإنتاج)، ضع `Aspose.OCR.lic` في مجلد الموارد واستخدم:

```java
// Load the Aspose OCR license (optional)
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

> **نصيحة احترافية:** احتفظ بملف الترخيص خارج نظام التحكم بالإصدار لتجنب كشفه عن طريق الخطأ.

## الخطوة 2: إنشاء كائن `OcrEngine` آمن للخيوط

كائن `OcrEngine` الخاص بـ Aspose OCR آمن للخيوط طالما تعيد استخدام نفس المثيل عبر المهام. إن إنشاؤه مرة واحدة يوفر الذاكرة ويتجنب عبء إعادة تهيئة المحرك لكل صورة.

```java
// One shared OcrEngine for all threads
OcrEngine ocrEngine = new OcrEngine();
```

لماذا إعادة الاستخدام؟ فكر في المحرك كعامل ثقيل الوزن يحمل نماذج اللغة في الذاكرة. إنشاء محرك جديد لكل صورة سيكون كاستئجار متخصص جديد لكل مهمة صغيرة – مكلف وغير ضروري.

## الخطوة 3: إعداد Fixed Thread Pool في Java

الآن يأتي نجم العرض: **fixed thread pool java**. سنحدد حجمه بناءً على عدد المعالجات المنطقية بحيث يحصل كل نواة على عمل دون تجاوز السعة.

```java
// Determine available processors and create a fixed pool
int threadCount = Runtime.getRuntime().availableProcessors();
ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);
```

استخدام مجموعة *ثابتة* (بدلاً من المؤقتة) يمنحك استخدام موارد متوقع ويمنع الارتفاعات المخيفة للـ “out‑of‑memory” عندما تصل مئات الصور دفعة واحدة.

## الخطوة 4: سرد ملفات PNG التي تريد معالجتها (Extract Text from PNG)

اجمع مسارات الصور التي تريد تطبيق OCR عليها. في مشروع حقيقي قد تقوم بمسح دليل أو القراءة من قاعدة بيانات؛ هنا سنكتب بعض الأمثلة يدويًا.

```java
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png"
);
```

> **ملاحظة:** امتداد الملف **png** مهم لأن Aspose OCR يكتشف الصيغة تلقائيًا، لكن يمكنك أيضًا إمداده بملفات JPEG أو TIFF.

## الخطوة 5: تقديم مهام OCR – معالجة OCR متوازية

كل صورة تتحول إلى callable يُعيد النص المُعترف به. لأن `OcrEngine` مشترك، نحتاج فقط لتمرير مسار الملف إلى المهمة.

```java
List<Future<String>> ocrFutures = new ArrayList<>();

for (String imagePath : imageFiles) {
    ocrFutures.add(threadPool.submit(() -> {
        // Prepare input for this image
        OcrInput input = new OcrInput();
        input.add(imagePath);

        // Perform OCR using the shared engine
        OcrResult result = ocrEngine.recognize(input);

        // Return the plain text
        return result.getText();
    }));
}
```

لماذا نغلفها في `Future`؟ يتيح لنا إطلاق جميع الوظائف فورًا، ثم جمع النتائج لاحقًا بالترتيب الذي تم تقديمها به – مثالي للحفاظ على ترتيب الصفحات عند **convert scanned pages text** مرة أخرى إلى مستند.

## الخطوة 6: استرجاع النتائج وعرضها (Convert Scanned Pages Text)

الآن ننتظر كل `Future` لتنتهي ونطبع الناتج. استدعاء `get()` يحجب فقط حتى يكتمل المهمة المحددة، وليس كل المجموعة.

```java
for (Future<String> future : ocrFutures) {
    System.out.println("----");
    System.out.println(future.get()); // prints OCR result for one PNG
}
```

مخرجات وحدة التحكم النموذجية تبدو هكذا:

```
----
The quick brown fox jumps over the lazy dog.
----
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----
Page 3 content goes here…
```

إذا كنت تفضل كتابة النتائج إلى ملفات، استبدل `System.out.println` بـ `Files.writeString`.

## الخطوة 7: إغلاق Executor Service بشكل نظيف

عند انتهاء جميع المهام، من الضروري **shut down executor service**؛ وإلا قد يبقى JVM يحتفظ بخيوط غير daemon نشطة، مما يمنع الخروج السلس.

```java
threadPool.shutdown();               // No new tasks accepted
if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
    threadPool.shutdownNow();        // Force shutdown after timeout
}
```

نمط `awaitTermination` يمنح المجموعة فرصة لإنهاء العمل الجاري قبل أن نجبرها على الإغلاق. تجاهل هذه الخطوة هو مصدر شائع لتسرب الذاكرة في التطبيقات طويلة التشغيل.

## مثال كامل يعمل

بجمع كل ذلك معًا، إليك البرنامج الكامل الذي يمكنك نسخه ولصقه في `ParallelBatchDemo.java` وتشغيله:

```java
import com.aspose.ocr.*;

import java.util.*;
import java.util.concurrent.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license (optional)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // 2️⃣ Shared, thread‑safe OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Fixed thread pool java – one thread per core
        int threadCount = Runtime.getRuntime().availableProcessors();
        ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);

        // 4️⃣ Files to process – extract text from png
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png"
        );

        // 5️⃣ Submit tasks – parallel OCR processing
        List<Future<String>> ocrFutures = new ArrayList<>();
        for (String imagePath : imageFiles) {
            ocrFutures.add(threadPool.submit(() -> {
                OcrInput input = new OcrInput();
                input.add(imagePath);
                OcrResult result = ocrEngine.recognize(input);
                return result.getText();
            }));
        }

        // 6️⃣ Retrieve and print – convert scanned pages text
        for (Future<String> future : ocrFutures) {
            System.out.println("----");
            System.out.println(future.get());
        }

        // 7️⃣ Shut down executor service cleanly
        threadPool.shutdown();
        if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
            threadPool.shutdownNow();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}