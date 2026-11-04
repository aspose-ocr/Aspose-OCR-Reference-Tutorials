---
category: general
date: 2026-02-09
description: تعلم كيفية تنفيذ التعرف الضوئي على الحروف (OCR) على دفعات في Java باستخدام
  Aspose OCR. استخراج النص من الصور، والتعرف على النص من ملفات PNG وJPG وTIFF في مكالمة
  واحدة.
draft: false
keywords:
- how to batch ocr
- extract text from images
- recognize text from png
- recognize text from jpg
- recognize text from tiff
language: ar
og_description: تعلّم كيفية تنفيذ OCR دفعيًا في جافا. يوضح لك هذا الدليل كيفية استخراج
  النص من صور PNG و JPG و TIFF باستخدام Aspose OCR مع أمثلة شفرة واضحة.
og_title: كيفية تنفيذ التعرف الضوئي على الحروف (OCR) على دفعات في جافا – استخراج النص
  من الصور بكفاءة
tags:
- OCR
- Java
- Aspose
title: كيفية تنفيذ التعرف الضوئي على الحروف على دفعات في جافا – دليل شامل لاستخراج
  النص من الصور
url: /ar/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيف تقوم بعملية OCR دفعةً في Java – دليل كامل لاستخراج النص من الصور

هل تساءلت يومًا **كيف تقوم بعملية OCR دفعةً** لعدد من الصور دون كتابة حلقة لكل ملف؟ لست وحدك. في العديد من المشاريع الواقعية ستحصل على مجلد مليء بالمسحات—إيصالات PNG، لقطات شاشة JPG، أو حتى ملفات TIFF متعددة الصفحات—وتحتاج إلى النص بسرعة.  

الخبر السار هو أن Aspose OCR يتيح لك فعل ذلك بالضبط: استدعاء طريقة واحدة تتعرف على النص من ملفات PNG وJPG وTIFF جميعًا مرة واحدة. في هذا الدرس سنستعرض العملية بالكامل، من إعداد المشروع إلى طباعة النتائج، حتى تتمكن من بدء استخراج النص من الصور اليوم.

## ما يغطيه هذا الدرس

* **كيف تقوم بعملية OCR دفعةً** باستخدام `OcrBatchProcessor` من Aspose.
* طرق **استخراج النص من الصور** بمختلف الصيغ (PNG، JPG، TIFF).
* نصائح للتحكم في التوازي للحفاظ على استجابة تطبيقك.
* برنامج Java كامل قابل للتنفيذ يمكنك نسخه ولصقه وتشغيله فورًا.

لا تحتاج إلى خبرة سابقة مع Aspose—فقط تثبيت Java أساسي وIDE من اختيارك. في النهاية، ستحصل على أساس قوي للتعرف على النص من ملفات PNG وJPG وTIFF بالجملة.

---

![مخطط يوضح كيفية تنفيذ OCR دفعةً لعدة ملفات صورة](/images/batch-ocr-diagram.png "كيفية تنفيذ OCR دفعةً")

*نص بديل للصورة: مخطط يوضح كيفية تنفيذ OCR دفعةً لعدة ملفات صورة معالجة معًا.*

## المتطلبات المسبقة

| المتطلب | لماذا هو مهم |
|-------------|----------------|
| Java 17 أو أحدث | Aspose OCR يستهدف JVM الحديثة. |
| Maven أو Gradle | يبسط إضافة مكتبة Aspose OCR. |
| معرفة أساسية بـ Java | ضرورية لفهم تدفق الكود. |
| مجموعة من الصور التجريبية (`.png`، `.jpg`، `.tif`) | لرؤية عملية الاستخراج عمليًا. |

إذا كان لديك هذه المتطلبات بالفعل، رائع—لنبدأ.

## الخطوة 1: إضافة Aspose OCR إلى مشروعك

أول شيء تحتاجه هو ملف JAR الخاص بـ Aspose OCR. إذا كنت تستخدم Maven، أضف ما يلي إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

إذا كنت تفضّل Gradle، فالمكافئ هو:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

إضافة الاعتماد يجلب كل ما يلزم لـ **recognize text from png**، **recognize text from jpg**، و**recognize text from tiff**. لا تحتاج إلى مكتبات أصلية إضافية.

## الخطوة 2: تعريف ملفات الصور التي تريد معالجتها

الآن سنخبر محرك OCR بأي ملفات يتعامل معها. هنا يبرز **how to batch OCR**—فقط مرّر قائمة بالمسارات ودع المكتبة تتولى العمل الشاق.

```java
import java.util.Arrays;
import java.util.List;

// Step 2: List your image files (PNG, JPG, TIFF)
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/img1.png",   // PNG file – recognize text from png
        "YOUR_DIRECTORY/img2.jpg",   // JPG file – recognize text from jpg
        "YOUR_DIRECTORY/img3.tif");  // TIFF file – recognize text from tiff
```

> **نصيحة احترافية:** احرص على أن تكون مسارات الملفات مطلقة أو استخدم `Paths.get(...)` لتجنب المفاجآت على أنظمة تشغيل مختلفة.

## الخطوة 3: إنشاء معالج الدفعة وضبط التوازي

Aspose OCR يأتي مع `OcrBatchProcessor`، الذي يمكنه تشغيل عدة عمليات التعرف بالتوازي. التحكم في عدد الخيوط يمنع تطبيقك من استهلاك كل موارد الـ CPU عندما يكون لديك عشرات الصور.

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

لماذا نحدّ من التوازي؟ إذا شغلت عددًا كبيرًا من الخيوط على حاسوب محمول متوسط، قد تلاحظ بطءً بدلاً من تسريع. ضبط `setMaxParallelism` يتيح لك موازنة السرعة والاستقرار.

## الخطوة 4: تشغيل استدعاء OCR الدفعي

هذا هو جوهر **how to batch OCR**: استدعاء `recognize` واحد يُعيد قائمة من كائنات `RecognitionResult`، واحدة لكل صورة.

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

الطريقة تحجب التنفيذ حتى تُعالج كل صورة، ثم تُعيد لك النص. إذا كنت تحتاج سلوكًا غير محجوب، يمكنك تغليف هذا في `CompletableFuture`، لكن بالنسبة لمعظم السكريبتات يكفي الاستدعاء المتزامن للحفاظ على نظافة الكود.

## الخطوة 5: طباعة النص المستخرج

أخيرًا، قم بالتكرار على النتائج وعرض السلاسل التي تم التعرف عليها. هذا يوضح أننا نجحنا في **extract text from images** بمختلف الصيغ.

```java
// Step 5: Output the recognized text for each file
for (int i = 0; i < recognitionResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(recognitionResults.get(i).getText());
    System.out.println("---");
}
```

### النتيجة المتوقعة

```
File: YOUR_DIRECTORY/img1.png
The quick brown fox jumps over the lazy dog.
---
File: YOUR_DIRECTORY/img2.jpg
Invoice #12345
Total: $567.89
---
File: YOUR_DIRECTORY/img3.tif
Page 1 of 3
Report generated on 2026-02-09
---
```

إذا لم يتمكن محرك OCR من قراءة ملف ما، فإن طريقة `getText()` تُعيد سلسلة فارغة، لذا يمكنك إضافة فحص بسيط لتسجيل التحذيرات.

## مثال كامل يعمل

بجمع كل ما سبق، إليك الفئة Java الكاملة الجاهزة للتنفيذ. انسخها إلى ملف باسم `BatchOcrTutorial.java`، عدّل مسارات الصور، ثم شغّل `javac && java`.

```java
import com.aspose.ocr.*;
import java.util.Arrays;
import java.util.List;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {

        // Step 1: Define the image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/img1.png",
                "YOUR_DIRECTORY/img2.jpg",
                "YOUR_DIRECTORY/img3.tif");

        // Step 2: Create the batch OCR processor and optionally limit parallelism
        OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();
        ocrProcessor.setMaxParallelism(4); // limit to 4 concurrent threads

        // Step 3: Perform OCR on all images in a single batch call
        List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);

        // Step 4: Output the recognized text for each file
        for (int i = 0; i < recognitionResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(recognitionResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

شغّله، وسترى وحدة التحكم تطبع النص المستخرج لكل ملف PNG، JPG، وTIFF—تمامًا ما تحتاجه عندما تكون **how to batch OCR** هي السؤال الذي يدور ببالك.

## أسئلة شائعة وحالات خاصة

### ماذا لو كان لدي أكثر من ثلاث صور؟

فقط أضف المزيد إلى قائمة `imageFiles`. سيقوم معالج الدفعة تلقائيًا بتقسيم العمل عبر الخيوط التي ضبطتها باستخدام `setMaxParallelism`.

### صوري موجودة في مجلد فرعي—هل يجب أن أدرج كل واحدة يدويًا؟

يمكنك جمع جميع الملفات ذات الامتداد المحدد برمجيًا:

```java
try (Stream<Path> paths = Files.walk(Paths.get("YOUR_DIRECTORY"))) {
    List<String> imageFiles = paths
        .filter(Files::isRegularFile)
        .filter(p -> p.toString().matches(".*\\.(png|jpg|tif|tiff)$"))
        .map(Path::toString)
        .collect(Collectors.toList());
}
```

هذا يجعل الكود مرنًا ولا يزال يحترم **how to batch OCR**.

### كيف أتعامل مع النتائج ذات الثقة المنخفضة؟

توفر `RecognitionResult` طريقة `getConfidence()`. يمكنك تصفية النتائج التي تقل عن عتبة معينة وإعادة المحاولة بإعدادات DPI أعلى:

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### هل يدعم Aspose OCR لغات أخرى؟

نعم—فقط استدعِ `ocrProcessor.setLanguage(OcrLanguage.Spanish)` (أو أي قيمة من القيم المدعومة) قبل استدعاء `recognize`. هذا يوسع الفائدة لتشمل أكثر من الإنجليزية، مما يجعل **extract text from images** متعدد اللغات فعليًا.

## نصائح للأداء

* **حجم الدفعة مهم** – الدفعات الأكبر تقلل من الحمل الزائد، لكن القوائم الكبيرة جدًا قد تستهلك ذاكرة أكثر. جرّب بين 50–200 صورة لكل دفعة.
* **التوازي** – على معالج رباعي النوى، عادةً ما يعطي `setMaxParallelism(4)` أفضل معدل نقل. عدّل حسب عبء عمل الخادم الخاص بك.
* **معالجة ما قبل OCR** – تحويل الصور إلى تدرج رمادي أو زيادة التباين قبل OCR يمكن أن يحسن الدقة، خاصةً للماسحات الضوضائية.

## الخلاصة

أنت الآن تعرف **how to batch OCR** في Java باستخدام Aspose OCR، وكيفية **extract text from images** بمختلف الصيغ، ولماذا التحكم في التوازي مهم. يوضح المثال الكامل كيفية التعرف على النص من ملفات PNG، JPG، وTIFF في استدعاء واحد فعال.

هل أنت مستعد للخطوة التالية؟ جرّب إمداد مخرجات OCR إلى فهرس بحث، قاعدة بيانات، أو حتى ملخص ذكي بالذكاء الاصطناعي. يمكنك أيضًا تجربة إدخال PDF (Aspose OCR يدعمه) أو دمج هذا مع مكتبات معالجة الصور مثل OpenCV للحصول على دقة أعلى.

برمجة سعيدة، وتذكر—batch OCR لا يجب أن يكون صداعًا. بالأدوات الصحيحة والنمط الواضح، ستحول أكوام الصور إلى نص قابل للبحث في لمح البصر.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}