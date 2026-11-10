---
category: general
date: 2026-07-05
description: تحويل الصورة إلى نص باستخدام Java و Aspose OCR. تعلّم كيفية استخراج النص
  من عمليات المسح، ملفات TIFF، وتدفقات البيانات بسرعة وموثوقية.
draft: false
keywords:
- convert image to text
- extract text from scan
- extract text from tif
- recognize text from stream
- how to ocr stream
language: ar
og_description: تحويل الصورة إلى نص باستخدام Aspose OCR في Java. يوضح هذا الدليل كيفية
  استخراج النص من المسح الضوئي، ملفات TIFF، وتدفقات البيانات، ويغطي كل خطوة من الإعداد
  إلى الإخراج.
og_title: تحويل الصورة إلى نص في جافا – دليل Aspose OCR الكامل
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert image to text with Java using Aspose OCR. Learn how to extract
    text from scan, TIFF files, and streams quickly and reliably.
  headline: Convert Image to Text in Java Using Aspose OCR – Full Guide
  type: TechArticle
tags:
- Java
- OCR
- Aspose
title: تحويل الصورة إلى نص في جافا باستخدام Aspose OCR – دليل كامل
url: /ar/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل الصورة إلى نص في جافا باستخدام Aspose OCR – دليل كامل

هل تساءلت يومًا كيف **تحويل الصورة إلى نص** دون الخوض في حيل معالجة الصور منخفضة المستوى؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى استخراج النص من ملفات المسح أو مستندات TIFF الكبيرة، خاصةً عندما يكون المصدر من تدفق بيانات بدلاً من مسار ملف بسيط.  

في هذا الدرس سنستعرض حلًا عمليًا من البداية إلى النهاية ي **يستخرج النص من صور المسح**، ويتعامل مع **استخراج النص من ملفات tif**، ويظهر لك بالضبط **كيفية إجراء OCR على التدفق** باستخدام مكتبة Aspose OCR لجافا. في النهاية ستحصل على مقطع شفرة قابل لإعادة الاستخدام يطبع النص المعترف به مباشرةً إلى وحدة التحكم.

## ما ستحتاجه

- **Java Development Kit (JDK) 8 أو أحدث** – يعمل الكود على أي JDK حديث.
- **Maven أو Gradle** (أداة البناء المفضلة لديك) لجلب تبعية Aspose OCR.
- ملف صورة – ويفضل أن يكون **TIFF** متعدد الصفحات (`large_image.tif`) تريد اختباره.
- قدر معقول من الصبر (أمزح فقط – الخطوات سريعة جدًا).

إذا كان أي من ذلك غير مألوف لك، لا تقلق. سنغطي إعداد Maven في الخطوة الأولى، والبقية هي جافا بحتة.

## الخطوة 1: إضافة Aspose OCR إلى مشروعك

العقبة الأولى هي الحصول على محرك OCR في مسار الفئات الخاص بك. تنشر Aspose مكتباتها على Maven Central، لذا يمكنك إضافة تبعية واحدة.

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Use the latest stable version -->
    </dependency>
</dependencies>
```

> **نصيحة احترافية:** إذا كنت تستخدم Gradle، فإن المكافئ هو  
> `implementation 'com.aspose:aspose-ocr:23.9'`.  
> هذه الإضافة الصغيرة تمنحك الوصول إلى `OcrEngine` و `RecognitionResult` وكل الأعمال الثقيلة تحت الغطاء.

## الخطوة 2: تهيئة محرك OCR

الآن بعد أن أصبحت المكتبة جاهزة، يمكننا إنشاء نسخة من `OcrEngine`. فكر في المحرك كالعقل الذي سي **يتعرف على النص من التدفق**.

```java
import com.aspose.ocr.OcrEngine;

// ...

// Step 2: Initialize the OCR engine – this is where the magic starts.
OcrEngine engine = new OcrEngine();
```

لماذا ننشئ المحرك مرة واحدة؟ إعادة استخدام نفس كائن `OcrEngine` لعدة صور يقلل من الحمل الزائد ويحسن الأداء، خاصةً عند معالجة دفعة من الصفحات الممسوحة.

## الخطوة 3: فتح الصورة كتيار بيانات

معظم السيناريوهات الواقعية تتضمن قراءة الصور من موقع شبكة، قاعدة بيانات، أو ملف تم تحميله – جميعها تظهر كتيارات بيانات. إليك كيفية **التعرف على النص من التدفق** دون الحاجة إلى لمس نظام الملفات مباشرةً.

```java
import java.io.FileInputStream;
import java.io.InputStream;

// ...

// Step 3: Load the image (a TIFF in this case) as an InputStream.
try (InputStream imageStream = new FileInputStream("YOUR_DIRECTORY/large_image.tif")) {
    // The try‑with‑resources block ensures the stream closes automatically.
```

إذا كان المصدر `ByteArrayInputStream` أو `InputStream` من طلب servlet، استبدل ببساطة مُنشئ `FileInputStream` – يبقى باقي الكود كما هو.

## الخطوة 4: تنفيذ OCR واستخراج النص

مع وجود التيار في اليد، نستدعي `engine.recognizeImage`. تُعيد هذه الطريقة كائن `RecognitionResult` الذي يحتوي على السلسلة المستخرجة.

```java
import com.aspose.ocr.RecognitionResult;

// ...

    // Step 4: Recognize text from the image stream
    RecognitionResult ocrResult = engine.recognizeImage(imageStream);

    // Step 5: Print the extracted text to the console
    System.out.println("=== OCR Output ===");
    System.out.println(ocrResult.getText());
}
```

لاحظ كيف أن استدعاء `recognizeImage` يقوم بكل الأعمال الثقيلة: فهو يفك تشفير TIFF، يشغل محرك OCR، ويعيد النص العادي. هذا هو جوهر وظيفة **تحويل الصورة إلى نص**.

## الخطوة 5: معالجة ملفات TIFF متعددة الصفحات (اختياري)

إذا كان ملف TIFF يحتوي على عدة صفحات، سيقوم Aspose OCR بدمج النص من كل صفحة تلقائيًا. ومع ذلك، قد ترغب في فصل الصفحات لسهولة القراءة. إليك تعديلًا سريعًا:

```java
String fullText = ocrResult.getText();
String[] pages = fullText.split("\\f"); // Form feed character denotes page break

for (int i = 0; i < pages.length; i++) {
    System.out.println("--- Page " + (i + 1) + " ---");
    System.out.println(pages[i].trim());
}
```

هذا المقتطف **يستخرج النص من المستندات الممسوحة** صفحةً بصفحة، مما يمنحك تحكمًا دقيقًا في الناتج.

## مثال كامل يعمل

بجمع كل شيء معًا، إليك فئة كاملة جاهزة للتنفيذ يمكنك نسخها إلى بيئة التطوير المتكاملة الخاصة بك.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;
import java.io.FileInputStream;
import java.io.InputStream;

public class StreamOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2: Open the image file as a stream
        try (InputStream imageStream = new FileInputStream("YOUR_DIRECTORY/large_image.tif")) {

            // Step 3: Recognize text from the image stream
            RecognitionResult ocrResult = engine.recognizeImage(imageStream);

            // Step 4: Print the extracted text
            System.out.println("=== OCR Output ===");
            System.out.println(ocrResult.getText());

            // Optional: Separate pages if it's a multi‑page TIFF
            String[] pages = ocrResult.getText().split("\\f");
            for (int i = 0; i < pages.length; i++) {
                System.out.println("--- Page " + (i + 1) + " ---");
                System.out.println(pages[i].trim());
            }
        }
    }
}
```

**الناتج المتوقع** (مقتطع للاختصار):

```
=== OCR Output ===
This is the first line of the scanned document.
Another line follows...
--- Page 1 ---
This is the first line of the scanned document.
...
```

إذا كانت الصورة غير واضحة أو اللغة ليست الإنجليزية، يمكنك تعديل `engine.setLanguage` أو ضبط خيارات ما قبل المعالجة – لكن سير العمل الأساسي يظل كما هو.

## الأخطاء الشائعة وكيفية تجنبها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| `NullPointerException` على `ocrResult.getText()` | المحرك غير مهيأ أو تم إغلاق تدفق الصورة مبكرًا | تأكد من إنشاء `OcrEngine` **قبل** فتح التيار وابقِ التيار مفتوحًا حتى بعد عودة `recognizeImage`. |
| حروف مشوهة | دقة DPI للصورة منخفضة جدًا (أقل من 300) | استخدم مصدرًا بدقة أعلى أو فعّل تحسين الصورة في Aspose (`engine.getImagePreprocessingOptions().setDpi(300)`). |
| لا يوجد ناتج لملف TIFF متعدد الصفحات | النتيجة لم تُقسم بشكل صحيح | استخدم `\\f` (تغذية النموذج) كما هو موضح أعلاه لفصل الصفحات. |
| `OutOfMemoryError` على ملفات ضخمة | تحميل الملف بالكامل إلى الذاكرة | عالج TIFF صفحةً بصفحة باستخدام `engine.recognizeImage(pageStream)` داخل حلقة. |

## إضافي: تحويل النتيجة إلى ملف نصي

إذا كنت بحاجة إلى **تحويل الصورة إلى نص** وتخزينه للاستخدام لاحقًا، فقط أضف بضع أسطر:

```java
import java.nio.file.Files;
import java.nio.file.Paths;

// ...

String outputPath = "output.txt";
Files.write(Paths.get(outputPath), ocrResult.getText().getBytes());
System.out.println("Text saved to " + outputPath);
```

الآن لديك نسخة دائمة من مخرجات OCR، مثالية للمعالجة اللاحقة أو الفهرسة.

## الخلاصة

لقد تعلمت الآن كيفية **تحويل الصورة إلى نص** في جافا باستخدام Aspose OCR، مع تغطية كل شيء من ملفات **استخراج النص من المسح** إلى صور **استخراج النص من tif**، وإتقان تقنيات **التعرف على النص من التدفق**. المثال الكامل يوضح الخطوات الدقيقة التي تحتاجها لتشغيلها اليوم، وتظهر المقاطع الاختيارية كيفية معالجة المستندات متعددة الصفحات أو حفظ النتائج على القرص.

ما التالي؟ جرّب إمداد محرك OCR بملفات PDF، جرب إعدادات اللغة، أو دمج الناتج في فهرس بحث. النمط نفسه يعمل مع بيانات **كيفية إجراء OCR على التدفق** القادمة من تحميلات الويب، التخزين السحابي، أو حتى طابور رسائل.

هل لديك أسئلة أو صورة صعبة ترفض التعاون؟ اترك تعليقًا أدناه، وبرمجة سعيدة! 

![مخطط يوضح التدفق من ملف الصورة → InputStream → OcrEngine → ناتج النص – تحويل الصورة إلى نص](https://example.com/convert-image-to-text-diagram.png "مخطط تدفق تحويل الصورة إلى نص")

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية استخراج النص من TIFF باستخدام Aspose.OCR لجافا](/ocr/english/java/ocr-operations/recognize-tiff/)
- [تحويل الصورة إلى نص في جافا باستخدام Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [كيفية إجراء OCR لنص الصورة مع اللغة باستخدام Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}