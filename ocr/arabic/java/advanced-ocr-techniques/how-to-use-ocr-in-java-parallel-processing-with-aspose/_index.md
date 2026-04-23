---
category: general
date: 2026-02-27
description: تعلم كيفية استخدام OCR في جافا لاستخراج نص الصورة من ملفات TIFF وPDF
  باستخدام المعالجة المتوازية لـ Aspose OCR. دليل سريع وبسيط.
draft: false
keywords:
- how to use ocr
- perform ocr on pdf
- extract text from tiff
- extract image text java
language: ar
og_description: تعلم كيفية استخدام OCR في جافا لاستخراج نص الصورة من ملفات TIFF وPDF
  باستخدام المعالجة المتوازية لـ Aspose OCR.
og_title: كيفية استخدام OCR في جافا – المعالجة المتوازية مع Aspose
tags:
- OCR
- Java
- Aspose
title: كيفية استخدام OCR في جافا – المعالجة المتوازية مع Aspose
url: /ar/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/
---

placeholders unchanged.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في Java – المعالجة المتوازية مع Aspose

هل تساءلت يومًا **how to use OCR** لاستخراج النص من مستند ممسوح ضوئيًا دون عناء؟ لست وحدك. يواجه المطورون دائمًا صعوبة عندما يحتاجون إلى قراءة النص من الصور—خاصة TIFFs و PDFs—مع الحفاظ على الأداء.

في هذا الدرس سنعرض لك حلاً كاملاً وجاهزًا للتنفيذ يـ **extracts image text in Java** باستخدام Aspose OCR، يُفعِّل المعالجة المتوازية، وحتى يتيح لك تحديد الحد الأقصى لعدد الخيوط. في النهاية ستحصل على فئة واحدة يمكنها **perform OCR on PDF** واستخراج النص من صور **TIFF** في جزء بسيط من الوقت الذي تستغرقه الطريقة أحادية الخيط.

> **ما ستحصل عليه**  
> * شرح واضح لأهمية OCR المتوازي.  
> * برنامج Java كامل (بدون استيرادات مفقودة).  
> * نصائح لضبط استخدام الخيوط ومعالجة المشكلات الشائعة.  

## المتطلبات المسبقة

- Java 8 أو أحدث (الكود يُترجم مع JDK 11 أيضًا).  
- مكتبة Aspose.OCR للـ Java – يمكنك الحصول على أحدث JAR من Maven Central (`com.aspose:aspose-ocr`).  
- ملف صورة (`.tif`, `.tiff`) أو PDF تريد معالجته.  
- كمية معتدلة من الذاكرة RAM—المعالجة المتوازية ستنشئ عدة خيوط، لكن Aspose فعال في استخدام الذاكرة.

إذا كان لديك ذلك، فلنبدأ.

![مخطط يوضح خط أنابيب OCR – كيفية استخدام OCR في Java مع المعالجة المتوازية](how-to-use-ocr-pipeline.png)

*نص بديل للصورة: مخطط مثال على كيفية استخدام OCR*

---

## الخطوة 1: إعداد مشروعك وإضافة Aspose OCR

### لماذا هذا مهم

قبل أن تتمكن من **perform OCR on PDF** أو أي صورة، يجب أن تكون المكتبة في مسار الفئة (classpath). بدونها سيُصدر المترجم استثناء `ClassNotFoundException` وستعلق عند الخطوة الثانية.

### كيفية القيام بذلك

If you’re using Maven, add the dependency:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the newest version -->
</dependency>
```

For Gradle:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **نصيحة احترافية:** حافظ على توافق رقم الإصدار مع ملاحظات إصدار Aspose؛ الإصدارات الأحدث غالبًا ما تتضمن تحسينات في الأداء للمعالجة المتوازية.

---

## الخطوة 2: إنشاء محرك OCR وتمكين المعالجة المتوازية

### لماذا هذا مهم

بشكل افتراضي يعمل Aspose OCR على خيط واحد. عندما تزوده بملف PDF متعدد الصفحات أو دفعة من ملفات TIFF، سيعالج المحرك كل صفحة تلو الأخرى—ببطء وغير فعال. تمكين المعالجة المتوازية يسمح للمعالج بمعالجة عدة صفحات في آن واحد، مما يقلل زمن التنفيذ بشكل كبير.

### الكود

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Path to the input file (TIFF or PDF)
        String inputPath = "YOUR_DIRECTORY/input.tif";

        // 2️⃣ Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Turn on parallel processing – this is the core of how to use OCR efficiently
        ocrEngine.getConfig().setUseParallelProcessing(true);

        // 4️⃣ (Optional) Limit threads – you can cap it to the number of cores you have
        // ocrEngine.getConfig().setMaxThreads(Runtime.getRuntime().availableProcessors());

        // 5️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.processImage(inputPath);

        // 6️⃣ Output the recognised text
        System.out.println(ocrResult.getText());
    }
}
```

**شرح السطور الرئيسية**

- `setUseParallelProcessing(true)`: يخبر Aspose بتقسيم عبء العمل عبر نوى المعالج المتاحة.  
- `setMaxThreads(...)`: يمكنك تقييد مجموعة الخيوط إذا كنت على خادم مشترك أو تريد ترك مساحة للخدمات الأخرى.  
- `processImage(inputPath)`: يعمل مع ملفات الصور ومستندات PDF، لذا فإن نفس الاستدعاء **performs OCR on PDF** وعلى TIFF على حد سواء.

---

## الخطوة 3: معالجة أنواع الإدخال المختلفة – PDF مقابل TIFF

### لماذا هذا مهم

على الرغم من أن `processImage` تقبل سلسلة مسار، إلا أن المعالجة الداخلية تختلف. غالبًا ما تحتوي ملفات PDF على عدة صفحات، كل واحدة تصبح مهمة OCR منفصلة. يمكن أن تكون ملفات TIFF صفحة واحدة أو متعددة؛ Aspose يعامل كل إطار كصفحة.

### ما الذي يجب الانتباه إليه

| الإدخال | المشكلة الشائعة | الحل الموصى به |
|------|----------------|-----------------|
| PDF | قد تستنزف ملفات PDF الكبيرة الذاكرة إذا تم تحميل جميع الصفحات في آن واحد. | استخدم `ocrEngine.getConfig().setMemoryOptimization(true);` (متوفر في الإصدارات الأحدث). |
| TIFF متعدد الصفحات | بعض ملفات TIFF القديمة تستخدم ضغطًا غير مدعوم. | حوّلها إلى تنسيق مدعوم أولاً، أو استخدم المساعد `TiffImage` من Aspose. |

فيما يلي مقتطف سريع يوضح كيفية اكتشاف نوع الملف وتسجيل رسالة ودية:

```java
import java.nio.file.*;

String ext = Files.probeContentType(Paths.get(inputPath)).toLowerCase();
if (ext.contains("pdf")) {
    System.out.println("Processing a PDF – expect multiple pages.");
} else if (ext.contains("tiff") || ext.contains("tif")) {
    System.out.println("Processing a TIFF image.");
} else {
    System.out.println("Unsupported file type. This demo works with PDF and TIFF.");
}
```

---

## الخطوة 4: التحقق من الناتج – ماذا يجب أن ترى؟

عند انتهاء البرنامج، سترى النص المستخرج الخام يُطبع على وحدة التحكم. لفاتورة ممسوحة بسيطة، قد يبدو الناتج كالتالي:

```
Invoice #12345
Date: 02/15/2026
Total Amount: $1,250.00
Thank you for your business!
```

إذا واجه OCR صعوبة مع صفحة معينة، يضيف Aspose سطرًا بديلًا مثل `[Unrecognizable]`. يمكنك تصفية هذه السطور لاحقًا إذا كنت بحاجة إلى بيانات نظيفة.

**تحقق سريع من الصحة**

```java
if (ocrResult.getText().trim().isEmpty()) {
    System.err.println("No text detected – verify the image quality or try a different language.");
}
```

---

## الخطوة 5: تحسين الأداء – متى تعديل عدد الخيوط

### لماذا هذا مهم

المزيد من الخيوط لا يعني دائمًا نتائج أسرع. على لابتوب بأربعة نوى، تشغيل 8 خيوط قد يسبب عبء تبديل السياق. وعلى العكس، على خادم بـ32 نواة قد ترغب في استغلال القوة الكاملة.

### كيفية العثور على النقطة المثالية

```java
int cores = Runtime.getRuntime().availableProcessors();
System.out.println("Available processors: " + cores);

// Experiment: set max threads to half the cores first
ocrEngine.getConfig().setMaxThreads(Math.max(1, cores / 2));
```

شغّل البرنامج بإعدادات مختلفة وقم بقياس الوقت:

```java
long start = System.nanoTime();
ocrEngine.processImage(inputPath);
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed time (ms): " + elapsed / 1_000_000);
```

سجّل الأوقات، اختر الإعداد الذي يمنحك أعلى معدل نقل، وثبّته للإنتاج.

---

## الخطوة 6: توسيع العرض – معالجة دفعات متعددة من الملفات

إذا كنت بحاجة إلى **extract image text java** من مجلد كامل، غلف المنطق الأساسي في حلقة:

```java
Path folder = Paths.get("YOUR_DIRECTORY");
try (DirectoryStream<Path> stream = Files.newDirectoryStream(folder, "*.{tif,tiff,pdf}")) {
    for (Path file : stream) {
        System.out.println("\n--- Processing: " + file.getFileName() + " ---");
        OcrResult result = ocrEngine.processImage(file.toString());
        // Save or further process result.getText()
    }
}
```

هذا النمط يتوسع بشكل جيد لأن المحرك بالفعل يعالج صفحات كل ملف بشكل متوازي. الحلقة الخارجية تعمل تسلسليًا، لكن يمكنك أيضًا إرسال كل ملف إلى `ExecutorService` إذا كنت تحتاج إلى استغلال حقل CPU كبير.

---

## المشكلات الشائعة وكيفية تجنبها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| `OutOfMemoryError` | تحميل عدد كبير من الصفحات في آن واحد (خاصة مع ملفات PDF الضخمة). | فعّل تحسين الذاكرة (`setMemoryOptimization(true)`) أو عالج ملفات PDF صفحةً بصفحة باستخدام `processPage`. |
| أحرف مشوهة | تكوين لغة/ترميز غير صحيح. | استدعِ `ocrEngine.getConfig().setLanguage(OcrLanguage.English);` أو تعداد اللغة المناسب. |
| أداء بطيء رغم تفعيل المعالجة المتوازية | نظام التشغيل يحد من إنشاء الخيوط أو JVM يعمل بذاكرة heap منخفضة. | زد علم `-Xmx` للذاكرة، وتحقق من حدود الخيوط في نظام التشغيل (`ulimit -u`). |
| ناتج فارغ | دقة صورة الإدخال أقل من 300 dpi. | قم بزيادة دقة الصورة قبل OCR أو استخدم ماسحًا يخرج بدقة أعلى. |

---

## ملخص – ما تم تغطيته

- **How to use OCR** في Java مع `OcrEngine` من Aspose.  
- تمكين **parallel processing** لتسريع **perform OCR on PDF** و **extract text from TIFF**.  
- ضبط عدد الخيوط لتحقيق الأداء الأمثل.  
- معالجة الحالات الخاصة مثل PDFs الكبيرة، TIFF متعددة الصفحات، وإعدادات اللغة.  
- توسيع عرض الملف الواحد إلى معالج دفعات للمهام الواقعية.

---

## الخطوات التالية

الآن بعد أن أتقنت الأساسيات، فكر في استكشاف المواضيع ذات الصلة التالية:

- **Extract image text java** من ملاحظات مكتوبة بخط اليد (فعّل `setHandwritingRecognition(true)`).  
- دمج ناتج OCR مع Apache Tika لاستخراج البيانات الوصفية.  
- تخزين النتائج في Elasticsearch لأرشفة المستندات القابلة للبحث.  
- استخدام OCR من Aspose مع لغات أخرى مثل Python أو .NET—المبادئ تبقى نفسها.

لا تتردد في تجربة حدود خيوط مختلفة، صيغ صور، وحزم لغات. كلما جربت أكثر، كلما فهمت أفضل التوازنات بين السرعة والدقة.

---

### برمجة سعيدة!

إذا واجهت أي مشاكل أو كان لديك أفكار لتحسين إضافي، اترك تعليقًا أدناه. أنا دائمًا مستعد للنقاش حول حيل OCR—بدون عناء، فقط كود.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}