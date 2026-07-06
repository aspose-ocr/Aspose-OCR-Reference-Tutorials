---
category: general
date: 2026-04-26
description: كيفية تنفيذ OCR دفعيًا باستخدام Java و Aspose OCR – التعرف على النص من
  الصور، استخراج النص من PNG، واستخدام جميع نوى المعالج للمعالجة المتوازية للـ OCR.
draft: false
keywords:
- how to batch OCR
- recognize text from images
- extract text from PNG
- use all CPU cores
- parallel OCR processing
language: ar
og_description: كيفية تنفيذ OCR دفعيًا في جافا. تعلم كيفية التعرف على النص من الصور،
  استخراج النص من ملفات PNG، واستخدام جميع نوى المعالج للمعالجة السريعة المتوازية
  للـ OCR.
og_title: كيفية تنفيذ OCR دفعيًا في جافا – دليل المعالجة المتوازية
tags:
- OCR
- Java
- Aspose
- Performance
title: كيفية تنفيذ OCR دفعيًا في جافا باستخدام المعالجة المتوازية
url: /ar/java/advanced-ocr-techniques/how-to-batch-ocr-in-java-with-parallel-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR دفعيًا في جافا – دليل شامل

هل تساءلت يومًا **كيف تقوم بعمل OCR دفعيًا** عندما يكون لديك العشرات من لقطات PNG التي تواجهك؟ لست وحدك. يواجه معظم المطورين عقبة بمجرد أن يعمل عرض الـsingle‑image وتبدأ عبء العمل الحقيقي—مئات الملفات—في إبطاء المعالج.  

في هذا الدرس سنستعرض حلًا عمليًا من البداية إلى النهاية **يتعرف على النص من الصور**، يستخرج محتوى كل ملف PNG، و**يستخدم جميع نوى المعالج** لتسريع العملية. في النهاية ستحصل على فئة Java قابلة لإعادة الاستخدام تقوم بمعالجة مجلد من الصور بشكل متوازي، مما يمنحك سرعة محرك متعدد الخيوط دون عناء إدارة مجموعات الخيوط بنفسك.

> **ما ستحصل عليه:** برنامج Java قابل للتنفيذ بالكامل (Aspose OCR)، شروحات خطوة بخطوة، نصائح للحالات الخاصة، ومعاينة للمخرجات المتوقعة في وحدة التحكم.

---

## المتطلبات المسبقة

- **Java 17** (أو أي JDK حديث) مثبت ومُعَدّ `JAVA_HOME`.  
- **Aspose OCR for Java** مكتبة (الإصدار 23.10 أو أحدث). يمكنك الحصول عليها من Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- مجلد يحتوي على عدد قليل من **صور PNG** التي تريد معالجتها.  
- إلمام أساسي بصياغة Java—لا حاجة لأي شيء معقد.

إذا كان أي من ذلك غير مألوف لك، توقف هنا وقم بإعدادها؛ باقي الدليل يفترض أنها جاهزة.

## الخطوة 1 – إنشاء محرك OCR أحادي الخيط (الخط الأساسي)

أولًا: إنشاء كائن `OcrEngine`. هذا الكائن يقوم بالعمل الشاق—تحميل الصورة، تشغيل الشبكة العصبية، وإرجاع النص العادي.

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **لماذا هذا مهم:** إعادة استخدام نفس المحرك عبر ملفات متعددة يتجنب عبء تحميل نماذج اللغة بشكل متكرر، وهو ما يمكن أن يبطئ الأداء عندما تقوم بـ **معالجة دفعية**.

## الخطوة 2 – تمكين المعالجة المتوازية باستخدام جميع الأنوية المتاحة

الآن نخبر Aspose OCR بتوزيع العمل عبر كل معالج منطقي توفره أجهزتك. الدالة `Runtime.getRuntime().availableProcessors()` تُعيد هذا العدد، سواء كان لديك لابتوب بأربعة أنوية أو خادم بـ 32 نواة.

```java
        // Step 2: Enable parallel processing by using all available logical processors
        ocrEngine.getRecognitionSettings()
                 .setNumberOfThreads(Runtime.getRuntime().availableProcessors());
```

> **نصيحة احترافية:** على معالج يدعم الـ hyper‑threading سترى عدد الأنوية مضاعفًا، لكن المكتبة تقيد مجموعة الخيوط بذكاء، لذا لا تحتاج إلى ضبطها يدويًا.

## الخطوة 3 – جمع الصور التي تريد معالجتها

تحديد مصفوفة صغيرة يدوياً يعمل للعرض التجريبي، لكن في مهمة دفعية واقعية ربما ستقوم بمسح دليل. أدناه نعرض كلا النهجين.

```java
        // Step 3a: Define a static list (quick demo)
        String[] imageFiles = {
            "YOUR_DIRECTORY/image1.png",
            "YOUR_DIRECTORY/image2.png",
            "YOUR_DIRECTORY/image3.png"
        };

        // Step 3b: Or, dynamically load every PNG in a folder
        // File folder = new File("YOUR_DIRECTORY");
        // String[] imageFiles = folder.list((dir, name) -> name.toLowerCase().endsWith(".png"));
```

> **لماذا قد تحتاج هذا:** إذا كنت بحاجة إلى **استخراج النص من ملفات PNG** التي تصل عبر خط أنابيب التحميل، فإن النسخة الديناميكية تلتقط الملفات الجديدة تلقائيًا دون تعديل الكود.

## الخطوة 4 – تشغيل OCR على كل صورة باستخدام نفس المحرك

الحلقة أدناه تعيين الصورة الحالية، تشغيل `recognize()`، وطباعة النتيجة. بما أننا فعلنا المعالجة المتعددة الخيوط مسبقًا، قد يتم تشغيل كل استدعاء على خيط عامل منفصل في الخلفية.

```java
        // Step 4: Recognize text from each image (reusing the same engine instance)
        for (String imagePath : imageFiles) {
            ocrEngine.setImage(imagePath);
            String recognizedText = ocrEngine.recognize().getText();
            System.out.println("Result for " + imagePath + ":\n" + recognizedText);
        }
    }
}
```

### الإخراج المتوقع في وحدة التحكم

```
Result for YOUR_DIRECTORY/image1.png:
Welcome to the OCR demo.
Result for YOUR_DIRECTORY/image2.png:
Invoice #12345
Total: $567.89
Result for YOUR_DIRECTORY/image3.png:
© 2026 MyCompany. All rights reserved.
```

إذا كانت الصور تحتوي على نصوص غير لاتينية أو لقطات شاشة منخفضة الدقة، قد ترى أحرفًا مشوشة—قم بضبط إعدادات DPI أو تقليل الضوضاء للمحرك وفقًا لذلك (انظر قسم “التعديلات المتقدمة” أدناه).

## التعديلات المتقدمة – ضبط دقيق للدفعات الواقعية

| الحالة | الإعداد المقترح | مقتطف الكود |
|-----------|-------------------|--------------|
| صور PNG منخفضة الدقة | زيادة `setResolution` | `ocrEngine.getRecognitionSettings().setResolution(300);` |
| مستندات متعددة اللغات | إضافة حزم اللغة | `ocrEngine.getRecognitionSettings().addLanguage(OcrLanguage.Spanish);` |
| دفعات كبيرة جدًا (أكثر من 10k ملف) | تدفق الملفات بدلاً من تحميل جميع الأسماء مرة واحدة | Use `Files.walk(Paths.get("YOUR_DIRECTORY"))` with a filter. |
| قيود الذاكرة | إلغاء تخصيص المحرك بعد كل N ملف | `if (counter % 500 == 0) ocrEngine.dispose();` |

> **تذكر:** على الرغم من أننا **نستخدم جميع نوى المعالج**، إلا أن نظام التشغيل لا يزال يدير جدولة الخيوط. إذا لاحظت بطء جهازك، فكر في تقليل عدد الخيوط إلى `availableProcessors() - 1`.

## المشكلات الشائعة وكيفية تجنبها

1. **نفاد مقابض الملفات** – Java يحد عدد الملفات المفتوحة لكل عملية. أغلق كل صورة صراحة إذا واجهت أخطاء `Too many open files`:

   ```java
   ocrEngine.setImage(imagePath);
   String text = ocrEngine.recognize().getText();
   ocrEngine.getImage().close(); // releases the handle
   ```

2. **فواصل المسارات غير الصحيحة على Windows** – استخدم `File.separator` أو `Paths.get()` لتكون مستقلة عن النظام.

3. **استدعاءات رد فعل مخصصة غير آمنة للخيوط** – إذا أضفت مستمع تقدم، تأكد من أنه آمن للخيوط (مثلاً `AtomicInteger`).

## مثال كامل يعمل (جاهز للنسخ واللصق)

```java
import com.aspose.ocr.*;
import java.io.File;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable parallelism – use every logical CPU core
        ocrEngine.getRecognitionSettings()
                 .setNumberOfThreads(Runtime.getRuntime().availableProcessors());

        // 3️⃣ Locate PNG files (adjust the folder path)
        File folder = new File("YOUR_DIRECTORY");
        String[] imageFiles = folder.list((dir, name) ->
                name.toLowerCase().endsWith(".png"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG files found in the directory.");
            return;
        }

        // 4️⃣ Process each image – same engine, multi‑threaded under the hood
        for (String imageName : imageFiles) {
            String imagePath = folder.getAbsolutePath() + File.separator + imageName;
            ocrEngine.setImage(imagePath);
            String recognizedText = ocrEngine.recognize().getText();

            System.out.println("Result for " + imagePath + ":\n" + recognizedText);
            // Optional: free the image handle (good for huge batches)
            ocrEngine.getImage().close();
        }

        // Clean up
        ocrEngine.dispose();
    }
}
```

> **ما يفعله هذا:** يقوم بمسح `YOUR_DIRECTORY` للعثور على كل ملف `.png`، تشغيل OCR بشكل متوازي، طباعة كل نتيجة، وأخيرًا تحرير الموارد. يمكنك إضافة هذه الفئة إلى أي مشروع Maven، تشغيل `mvn exec:java`، وملاحظة زيادة السرعة مقارنةً بحلقة أحادية الخيط.

## الخاتمة

أصبح لديك الآن نمط قوي وجاهز للإنتاج لـ **كيفية تنفيذ OCR دفعيًا** في جافا. من خلال إعادة استخدام `OcrEngine` واحد، تمكين **معالجة OCR المتوازية**، والاستفادة من **جميع نوى المعالج**، يمكنك **التعرف على النص من الصور** في جزء بسيط من الوقت الذي تستغرقه حلقة بسيطة.

من هنا قد:

- ربط الناتج مع فهرس بحث (Elasticsearch) للبحث السريع.  
- دمجه مع محول PDF إلى PNG لـ **استخراج النص من PNG** المضمن في المستندات الممسوحة.  
- إضافة معالجة أخطاء ومنطق إعادة المحاولة لأقراص الشبكة غير المستقرة.

استمر في التجربة—استبدل JPEGs، عدل DPI، أو حتى قدم إطارات فيديو للتفريغ الفوري. الأفكار الأساسية تبقى كما هي، وعادةً ما تكون مكاسب الأداء ملحوظة.

برمجة سعيدة، ولتعمل خطوط OCR الخاصة بك بسرعة آلة القهوة! 🚀

![مخطط يوضح سير عمل OCR المتوازي – كيفية تنفيذ OCR دفعيًا عبر عدة نوى للمعالج]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}