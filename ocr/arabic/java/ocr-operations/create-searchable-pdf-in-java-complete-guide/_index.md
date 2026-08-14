---
category: general
date: 2026-07-05
description: إنشاء ملف PDF قابل للبحث في Java باستخدام Aspose OCR. تعلم كيفية ضغط
  الصور في PDF، وتحويل الصورة الممسوحة ضوئياً إلى PDF، وتعطيل تضمين الخطوط في PDF
  للحصول على ملفات أصغر.
draft: false
keywords:
- create searchable pdf
- compress images in pdf
- convert scanned image to pdf
- disable font embedding pdf
language: ar
og_description: إنشاء PDF قابل للبحث في Java باستخدام Aspose OCR. يوضح هذا الدرس كيفية
  ضغط الصور في PDF، وتحويل الصورة الممسوحة ضوئياً إلى PDF، وتعطيل تضمين الخطوط في
  PDF.
og_title: إنشاء ملف PDF قابل للبحث في جافا – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF in Java using Aspose OCR. Learn how to compress
    images in PDF, convert scanned image to PDF, and disable font embedding PDF for
    smaller files.
  headline: Create Searchable PDF in Java – Complete Guide
  type: TechArticle
tags:
- Java
- OCR
- PDF
title: إنشاء ملف PDF قابل للبحث في جافا – دليل كامل
url: /ar/java/ocr-operations/create-searchable-pdf-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث في Java – دليل كامل

هل احتجت يومًا إلى **create searchable PDF** من مستند ممسوح ضوئيًا لكن شعرت بالحيرة حيال كيفية القيام بذلك؟ لست وحدك. في العديد من المشاريع، تحويل ملف TIFF أو JPEG إلى PDF يمكنك فعلاً البحث فيه هو ميزة *ضرورية*، خاصة عندما تريد أيضًا **compress images in PDF** للحفاظ على حجم الملفات ضمن نطاق معقول.  

في هذا الدرس سنستعرض مثالًا عمليًا باستخدام Aspose OCR for Java. بنهاية الدرس ستعرف بالضبط كيفية **convert scanned image to PDF**، وضبط إعداد **compress images in PDF**، وحتى **disable font embedding PDF** لتقليل بعض الكيلوبايتات الإضافية. لا إطالة—حل كامل وقابل للتنفيذ يمكنك إدراجه في قاعدة الشيفرة الخاصة بك اليوم.

## ما ستتعلمه

- إعداد محرك Aspose OCR في مشروع Java.  
- إجراء OCR على ملف TIFF (أو أي صورة نقطية).  
- تهيئة `PdfSaveOptions` لتطبيق **compress images in PDF** و **disable font embedding PDF**.  
- حفظ النتيجة كـ **searchable PDF** يمكنك فهرستها أو البحث فيها فورًا.  

**Prerequisites**  
- Java 8 أو أحدث مثبت.  
- Maven أو Gradle لإدارة الاعتمادات (سنظهر مقتطف Maven).  
- ملف صورة ممسوحة ضوئيًا (TIFF، PNG، أو JPEG) جاهز للمعالجة.  

إذا كان لديك هذه المتطلبات، لنبدأ.

![Create searchable PDF workflow – Java OCR to PDF conversion](/images/create-searchable-pdf-workflow.png "Diagram showing the steps to create searchable PDF with Aspose OCR")

## الخطوة 1: إضافة اعتماد Aspose OCR

أولاً، استورد مكتبة Aspose OCR إلى مشروعك. باستخدام Maven، أضف التالي إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

إذا كنت تفضل Gradle، فالبديل هو:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **نصيحة احترافية:** راقب ملاحظات إصدارات Aspose؛ فالإصدارات الأحدث غالبًا ما تجلب تحسينات في الأداء لدقة OCR.

## الخطوة 2: تهيئة محرك OCR

إنشاء محرك OCR بسيط مثل إنشاء كائن `OcrEngine`. سيتولى هذا الكائن كل شيء من تحميل الصورة إلى استخراج النص.

```java
import com.aspose.ocr.OcrEngine;

// ...

// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

لماذا نحتاج إلى محرك مخصص؟ تقوم Aspose بفصل العمليات الثقيلة (معالجة الصور مسبقًا، نماذج اللغات) عن باقي تطبيقك، بحيث يمكنك إعادة استخدام نفس `engine` عبر ملفات متعددة دون إعادة تهيئة الموارد الثقيلة.

## الخطوة 3: إجراء OCR على الصورة الممسوحة

الآن نمرّر للـ engine ملفًا ممسوحًا. تُعيد الدالة `recognizeImage` كائنًا من نوع `RecognitionResult` يحتوي على النص المستخرج ومعلومات التخطيط.

```java
import com.aspose.ocr.RecognitionResult;

// ...

// Step 3: Perform OCR on the source image
String sourcePath = "YOUR_DIRECTORY/document_scan.tif"; // could be .png or .jpg too
RecognitionResult result = engine.recognizeImage(sourcePath);
```

> **ماذا لو لم تكن الصورة بصيغة TIFF؟**  
> يكتشف Aspose OCR تلقائيًا صيغ الصور النقطية الشائعة، لذا يمكنك توجيهه إلى JPEG أو PNG أو BMP دون تعديل الشيفرة.

## الخطوة 4: تهيئة خيارات حفظ PDF (ضغط الصور وتعطيل تضمين الخطوط)

هنا تتألق الكلمات المفتاحية الثانوية. سنخبر Aspose بـ **compress images in PDF** و **disable font embedding PDF**. كلا الإعدادين يقللان من حجم الملف النهائي—مفيد عندما تقوم بشحن عشرات المستندات.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

// ...

// Step 4: Set up PDF save options
PdfSaveOptions pdfOpts = new PdfSaveOptions();

// Reduce PDF size by compressing images
pdfOpts.setCompressImages(true);
pdfOpts.setImageQuality(80); // 0‑100, 80 is a good balance

// Prevent fonts from being embedded – saves a few KB per page
pdfOpts.setEmbedFonts(false);
```

**لماذا ضغط الصور؟**  
الصفحات الممسوحة عادةً ما تكون عالية الدقة؛ ضغطها إلى جودة 80 % يمكن أن يقلص ملف PDF مكوّن من 10 صفحات من 12 ميغابايت إلى أقل من 3 ميغابايت دون فقدان بصري ملحوظ.

**لماذا تعطيل تضمين الخطوط؟**  
إذا كان محرك OCR يستخدم خطوط نظام قياسية (مثل Arial أو Times New Roman)، فإن تضمينها يكون غير ضروري. إيقافه يقلل حجم الملف أكثر، خاصةً في الدفعات الكبيرة.

## الخطوة 5: حفظ نتيجة OCR كـ PDF قابل للبحث

الخطوة الأخيرة تجمع كل شيء معًا: الصورة الأصلية، طبقة النص المستخرجة، وإعدادات PDF التي ضبطناها للتو.

```java
// Step 5: Save the OCR result as a searchable PDF
String outputPath = "YOUR_DIRECTORY/document.pdf";
engine.saveAsSearchablePdf(outputPath, pdfOpts);

System.out.println("Searchable PDF created at: " + outputPath);
```

عند فتح `document.pdf` في Adobe Reader أو أي عارض حديث، سترى الصورة الممسوحة الأصلية **بالإضافة إلى** طبقة نص غير مرئية. كتابة كلمة في صندوق البحث ستُبرز التطابقات—تمامًا ما تعد به “create searchable pdf”.

### النتيجة المتوقعة

تشغيل البرنامج مع ملف TIFF صالح ينتج شيئًا مشابهًا لـ:

```
Searchable PDF created at: YOUR_DIRECTORY/document.pdf
```

افتح ملف PDF، اضغط `Ctrl+F`، اكتب كلمة تظهر في الصفحة الممسوحة، وستلاحظ القفز إلى الموضع الصحيح. هذا هو علامة نجاح سير عمل **create searchable pdf**.

## المشكلات الشائعة وكيفية تجنبها

| المشكلة | سبب حدوثها | الحل |
|-------|----------------|-----|
| **Blank PDF** | `PdfSaveOptions` لم يتم تمريره إلى `saveAsSearchablePdf`. | تأكد من استدعاء الدالة التي تقبل `PdfSaveOptions`. |
| **Garbage characters** | لم يتم تعيين لغة OCR (الافتراضية هي الإنجليزية). | استخدم `engine.getLanguage().setLanguage(OcrLanguage.FRENCH);` قبل `recognizeImage`. |
| **Huge file size** | `setCompressImages(false)` أو `setEmbedFonts(true)`. | احتفظ بالعلامتين كما هو موضح أعلاه. |
| **Image distortion** | `setImageQuality` تم ضبطه منخفضًا جدًا (<50). | التزم بالقيمة بين 70‑90 لتحقيق توازن جيد. |

## توسيع المثال

الآن بعد أن يمكنك **convert scanned image to PDF** والتحكم في الحجم، قد ترغب في:

- **Batch process** مجلد من المسحات باستخدام حلقة بسيطة `for(File f : folder.listFiles())`.  
- إضافة **watermarks** باستخدام Aspose PDF (`PdfDocument.addWatermarkText`).  
- تصدير نص OCR إلى ملف **plain .txt** لأغراض الفهرسة (`result.getText().writeToFile("doc.txt")`).  

جميع هذه الإضافات تعيد استخدام نفس كائن `OcrEngine`، مما يحافظ على انخفاض استهلاك الذاكرة.

## الكود الكامل الجاهز للتنفيذ

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Perform OCR on the source image
        String source = "YOUR_DIRECTORY/document_scan.tif";
        RecognitionResult result = engine.recognizeImage(source);

        // Step 3: Configure PDF save options (compress images & disable fonts)
        PdfSaveOptions pdfOpts = new PdfSaveOptions();
        pdfOpts.setCompressImages(true);      // Reduce PDF size by compressing images
        pdfOpts.setImageQuality(80);          // Image quality (0‑100)
        pdfOpts.setEmbedFonts(false);         // Do not embed fonts to keep file size small

        // Step 4: Save the OCR result as a searchable PDF
        String output = "YOUR_DIRECTORY/document.pdf";
        engine.saveAsSearchablePdf(output, pdfOpts);

        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF created at: " + output);
    }
}
```

انسخ‑الصق هذا في بيئة التطوير المتكاملة (IDE) الخاصة بك، استبدل `YOUR_DIRECTORY` بمسار فعلي، ثم شغّله. إذا تم إعداد كل شيء بشكل صحيح، ستحصل على **searchable PDF** خفيف الوزن بفضل ضغط الصور وتعطيل تضمين الخطوط.

## الخاتمة

لقد غطينا الآن كل ما تحتاجه لإنشاء ملفات **create searchable pdf** في Java باستخدام Aspose OCR. بدءًا من تهيئة المحرك، إجراء OCR، تعديل **compress images in pdf** و **disable font embedding pdf**، وصولاً إلى حفظ المستند القابل للبحث—تم شرح كل خطوة مع *السبب* وراءها.  

هل أنت مستعد للتحدي التالي؟ جرّب إضافة حزم لغات OCR، معالجة دفعات من المجلدات بالكامل، أو إضافة طبقات إلى ملفات PDF مع التعليقات التوضيحية. الأساسيات التي تعلمتها الآن ستجعل هذه الإضافات سهلة.  

هل لديك أسئلة أو ترغب في مشاركة حيلك الخاصة؟ اترك تعليقًا أدناه، وبرمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [التعرف على نص PDF – عمليات OCR باستخدام Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [التعرف على مستندات PDF باستخدام OCR في Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [كيفية OCR لملفات PDF في .NET باستخدام Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}