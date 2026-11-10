---
category: general
date: 2026-09-18
description: تعلم كيفية استخراج النص من الصور في Java باستخدام Aspose OCR. عالج ملفات
  PNG و JPG و TIFF دفعيًا بكفاءة في مكالمة واحدة.
keywords:
- extract text from images
- convert images to text
- how to batch ocr
- extract text from png
- extract text from jpg
- extract text from tiff
lastmod: 2026-09-18
og_description: اتقن كيفية استخراج النص من الصور في Java باستخدام OCR الدفعي. استخدم
  Aspose OCR لتحويل ملفات PNG و JPG و TIFF في مكالمة واحدة.
og_image_alt: Diagram showing multiple image files processed together for batch OCR
og_title: استخراج النص من الصور في Java – دليل OCR الدفعي
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to extract text from images in Java using Aspose OCR. Batch
    process PNG, JPG, and TIFF files efficiently in a single call.
  headline: How to extract text from images in Java by batch OCR
  type: TechArticle
- questions:
  - answer: Yes, Aspose OCR is pure Java and requires no UI components, so it works
      perfectly on headless environments.
    question: Can I run this on a headless server?
  - answer: A commercial license is needed for production deployments; a free trial
      is available for evaluation.
    question: Is a license required for production use?
  - answer: Any OS that can run Java 17+, including Windows, Linux, and macOS.
    question: Which operating systems are supported?
  - answer: Over 60 languages are supported out of the box, ranging from English and
      Spanish to Arabic and Chinese.
    question: How many languages can Aspose OCR recognise?
  - answer: Individual image files up to 200 MB are supported; larger files should
      be split before processing.
    question: What is the maximum file size Aspose OCR can handle?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: كيفية استخراج النص من الصور في Java باستخدام OCR الدفعي
url: /ar/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخراج النص من الصور في Java باستخدام OCR الدفعي

إذا كنت تحتاج إلى **استخراج النص من الصور** بسرعة ودون كتابة حلقة لكل ملف، فإن OCR الدفعي هو الجواب. في العديد من المشاريع الواقعية تستلم مجلدًا مليئًا بالمسحات—إيصالات PNG، لقطات شاشة JPG، أو ملفات TIFF متعددة الصفحات—ويجب تحويلها إلى نص قابل للبحث. يتيح لك Aspose OCR القيام بذلك تمامًا باستدعاء طريقة واحدة تعالج ملفات PNG و JPG و TIFF معًا، مما يوفر وقت التطوير ودورات CPU.

## إجابات سريعة
- **ما الذي يفعله OCR الدفعي؟** يقوم بمعالجة ملفات صور متعددة في طلب واحد، ويعيد النص لكل ملف.
- **ما الصيغ المدعومة؟** يتم التعامل مع PNG و JPG/JPEG و TIFF متعدد الصفحات مباشرةً.
- **هل أحتاج إلى مكتبة أصلية منفصلة؟** لا، يحتوي ملف JAR الخاص بـ Aspose OCR على كل ما تحتاجه.
- **هل يمكنني التحكم في عدد الخيوط التي تعمل؟** نعم، استخدم `setMaxParallelism` على معالج الدفعات.
- **ما نسخة Java المطلوبة؟** Java 17 أو أحدث.

## ما هو Aspose OCR؟
Aspose OCR هو مكتبة Java تتعرف على النص المطبوع والمكتوب يدويًا في ملفات الصور دون تبعيات خارجية. تدعم أكثر من 60 لغة ويمكنها معالجة ما يصل إلى 100 صورة لكل دفعة، مما يجعلها مثالية للرقمنة الضخمة للوثائق.

## ما يغطيه هذا الدرس
حمّل قائمة بمسارات الصور، أنشئ `OcrBatchProcessor`، اضبط التوازي، نفّذ استدعاء `recognize` واحد، واطبع السلاسل المستخرجة. في النهاية ستحصل على برنامج Java جاهز للتشغيل يستخرج النص من ملفات PNG و JPG و TIFF بالجملة.

- **كيفية تنفيذ OCR دفعي** باستخدام `OcrBatchProcessor` الخاص بـ Aspose.
- طرق **استخراج النص من الصور** بصيغ مختلفة (PNG، JPG، TIFF).
- نصائح للتحكم في التوازي للحفاظ على استجابة التطبيق.
- برنامج Java كامل وقابل للتنفيذ يمكنك نسخه ولصقه وتشغيله فورًا.

لا تحتاج إلى خبرة سابقة مع Aspose — فقط تثبيت Java أساسي وبيئة تطوير IDE تختارها. في النهاية ستحصل على أساس قوي للتعرف على النص من ملفات PNG و JPG و TIFF بالجملة.

---

![مخطط يوضح كيفية تنفيذ OCR دفعي لملفات صور متعددة](/images/batch-ocr-diagram.png "how to batch ocr")

*نص بديل للصورة: مخطط يوضح كيفية تنفيذ OCR دفعي يظهر معالجة ملفات صور متعددة معًا.*

## المتطلبات المسبقة

| المتطلب | لماذا يهم |
|-------------|----------------|
| Java 17 أو أحدث | Aspose OCR يستهدف JVMs الحديثة. |
| Maven أو Gradle | يبسط إضافة مكتبة Aspose OCR. |
| معرفة أساسية بـ Java | مطلوبة لفهم تدفق الكود. |
| مجموعة من صور العينة (`.png`، `.jpg`، `.tif`) | لرؤية عملية الاستخراج عمليًا. |

إذا كان لديك هذه بالفعل، رائع—لنبدأ.

## الخطوة 1: إضافة Aspose OCR إلى مشروعك

أول شيء تحتاجه هو ملف JAR الخاص بـ Aspose OCR. مع Maven، ضع هذا في ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

إذا كنت تفضّل Gradle، فإن المكافئ هو:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

إضافة الاعتماد يجلب كل ما يلزم لـ **استخراج النص من png**، **استخراج النص من jpg**، و **استخراج النص من tiff**. لا تحتاج إلى مكتبات أصلية إضافية.

## الخطوة 2: تعريف ملفات الصور التي تريد معالجتها

الآن سنخبر محرك OCR بالملفات التي يجب معالجتها. هنا يبرز **كيفية تنفيذ OCR دفعي** حقًا—فقط مرّر قائمة بالمسارات ودع المكتبة تقوم بالعمل الشاق.

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

## الخطوة 3: إنشاء معالج الدفعات وضبط التوازي

Aspose OCR يأتي مع `OcrBatchProcessor`، الذي يمكنه تشغيل عدة عمليات التعرف بالتوازي. التحكم في عدد الخيوط يمنع تطبيقك من استهلاك CPU عندما يكون لديك العشرات من الصور.

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

لماذا نحد من التوازي؟ إذا شغّلت الكثير من الخيوط على حاسوب محمول متوسط، قد تلاحظ بطءً بدلاً من تسريع. ضبط `setMaxParallelism` يتيح لك موازنة السرعة والاستقرار.

## الخطوة 4: تشغيل استدعاء OCR الدفعي

هذا هو جوهر **كيفية تنفيذ OCR دفعي**: استدعاء `recognize` واحد يُعيد قائمة من كائنات `RecognitionResult`، واحدة لكل صورة.  
`recognize` يعالج الصور المقدمة ويعيد قائمة من كائنات `RecognitionResult`، كل منها يحتوي على النص المستخرج.

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

الطريقة تحجب التنفيذ حتى تُعالج كل صورة، ثم تُعيد لك النص. إذا كنت تحتاج سلوكًا غير محجوب، يمكنك تغليف ذلك في `CompletableFuture`، لكن بالنسبة لمعظم السكريبتات يبقى الاستدعاء المتزامن منظمًا.

## الخطوة 5: طباعة النص المستخرج

أخيرًا، كرّر عبر النتائج واعرض السلاسل المعترف بها. هذا يوضح أننا نجحنا في **استخراج النص من الصور** بصيغ مختلفة.  
`RecognitionResult` يحتوي على ناتج OCR لصورة واحدة، بما في ذلك النص المستخرج ودرجة الثقة.

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

إذا لم يتمكن محرك OCR من قراءة ملف، فإن طريقة `getText()` تُعيد سلسلة فارغة، لذا يمكنك إضافة فحص بسيط لتسجيل التحذيرات.

## مثال كامل يعمل

بجمع كل شيء معًا، إليك الفئة الكاملة القابلة للتشغيل في Java. انسخها إلى ملف باسم `BatchOcrTutorial.java`، عدّل مسارات الصور، وشغّل `javac && java`.

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

شغّله، وسترى وحدة التحكم تطبع النص المستخرج لكل ملف PNG و JPG و TIFF—بالضبط ما تحتاجه عندما تكون **كيفية تنفيذ OCR دفعي** هي السؤال في ذهنك.

## أسئلة شائعة وحالات حافة

### ماذا لو كان لدي أكثر من ثلاث صور؟

فقط أضف المزيد من الإدخالات إلى قائمة `imageFiles`. سيقسم معالج الدفعات العمل تلقائيًا عبر الخيوط التي قمت بضبطها باستخدام `setMaxParallelism`.

### صوري في مجلد فرعي—هل يجب أن أدرج كل واحدة يدويًا؟

`Files.list` تُعيد تدفقًا مملوءًا ببطء لمسارات داخل دليل.

```java
try (Stream<Path> paths = Files.walk(Paths.get("YOUR_DIRECTORY"))) {
    List<String> imageFiles = paths
        .filter(Files::isRegularFile)
        .filter(p -> p.toString().matches(".*\\.(png|jpg|tif|tiff)$"))
        .map(Path::toString)
        .collect(Collectors.toList());
}
```

هذا يحافظ على مرونة الكود ولا يزال يحترم **كيفية تنفيذ OCR دفعي**.

### كيف أتعامل مع النتائج ذات الثقة المنخفضة؟

`getConfidence()` تُعيد قيمة عددية للثقة تشير إلى مدى احتمال صحة النص المعترف به.

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### هل يدعم Aspose OCR لغات أخرى؟

نعم—استدعِ `ocrProcessor.setLanguage(OcrLanguage.Spanish)` (أو أي تعداد مدعوم) قبل استدعاء `recognize`. هذا يوسع الفائدة إلى ما بعد الإنجليزية، مما يجعل **استخراج النص من الصور** متعدد اللغات حقًا.

## نصائح الأداء

* **حجم الدفعة مهم** – الدفعات الأكبر تقلل الحمل الزائد، لكن القوائم الكبيرة جدًا قد تستهلك المزيد من الذاكرة. اختبر بـ 50–200 صورة لكل دفعة.
* **التوازي** – على معالج رباعي النوى، `setMaxParallelism(4)` عادةً ما يعطي أفضل معدل نقل. اضبط بناءً على عبء عمل الخادم.
* **معالجة ما قبل الصورة** – تحويل الصور إلى تدرج الرمادي أو زيادة التباين قبل OCR يمكن أن يحسن الدقة، خاصةً للماسحات الضوضائية.

## الخلاصة

أنت الآن تعرف **كيفية تنفيذ OCR دفعي** في Java باستخدام Aspose OCR، وكيفية **استخراج النص من الصور** بصيغ مختلفة، ولماذا يهم التحكم في التوازي. مثال الكود الكامل يوضح التعرف على النص من ملفات PNG و JPG و TIFF في استدعاء واحد فعال.

هل أنت مستعد للخطوة التالية؟ ضع ناتج OCR في فهرس بحث، قاعدة بيانات، أو ملخص AI. يمكنك أيضًا تجربة إدخال PDF (يدعمها Aspose OCR) أو دمج ذلك مع مكتبات معالجة الصور مثل OpenCV للحصول على دقة أعلى.

برمجة سعيدة، وتذكر—OCR الدفعي لا يجب أن يكون صداعًا. مع الأدوات الصحيحة والنمط الواضح، ستحول أكوام الصور إلى نص قابل للبحث في وقت قصير.

## الأسئلة المتكررة

**س: هل يمكن تشغيل هذا على خادم بدون واجهة رسومية؟**  
ج: نعم، Aspose OCR هو Java نقي ولا يتطلب مكونات واجهة مستخدم، لذا يعمل بشكل مثالي في بيئات بدون واجهة.

**س: هل يلزم ترخيص للاستخدام في الإنتاج؟**  
ج: يلزم الحصول على ترخيص تجاري للنشر في بيئات الإنتاج؛ يتوفر نسخة تجريبية مجانية للتقييم.

**س: ما أنظمة التشغيل المدعومة؟**  
ج: أي نظام تشغيل يمكنه تشغيل Java 17+، بما في ذلك Windows و Linux و macOS.

**س: كم عدد اللغات التي يمكن لـ Aspose OCR التعرف عليها؟**  
ج: أكثر من 60 لغة مدعومة مباشرةً، من الإنجليزية والإسبانية إلى العربية والصينية.

**س: ما هو الحد الأقصى لحجم الملف الذي يمكن لـ Aspose OCR التعامل معه؟**  
ج: تدعم ملفات الصور الفردية حتى 200 ميغابايت؛ يجب تقسيم الملفات الأكبر قبل المعالجة.

---

**آخر تحديث:** 2026-09-18  
**تم الاختبار مع:** Aspose OCR 24.9 for Java  
**المؤلف:** Aspose

## دروس ذات صلة

- [استخراج النص من الصور – أساسيات OCR للـ Java](/ocr/java/ocr-basics/)
- [كيفية تنفيذ OCR دفعي في Java – دليل كامل لاستخراج النص من](/ocr/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/)
- [معالجة مسبقة لصورة OCR في Java لزيادة الدقة واستخراج النص](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}