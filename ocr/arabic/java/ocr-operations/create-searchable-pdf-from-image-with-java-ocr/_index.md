---
category: general
date: 2026-04-26
description: إنشاء ملف PDF قابل للبحث من صورة باستخدام Aspose OCR في Java. تعلم كيفية
  تحويل الصورة إلى PDF، واستخدام OCR لتحويل الصورة إلى PDF، واستخراج النص من الصورة
  بسرعة.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- extract text from image
- how to set language
language: ar
og_description: إنشاء ملف PDF قابل للبحث من صورة باستخدام Aspose OCR. يوضح هذا الدليل
  كيفية تحويل الصورة إلى PDF، واستخدام OCR لتحويل الصورة إلى PDF، واستخراج النص من
  الصورة.
og_title: إنشاء ملف PDF قابل للبحث من صورة باستخدام Java OCR
tags:
- Java
- OCR
- PDF
title: إنشاء PDF قابل للبحث من صورة باستخدام Java OCR
url: /ar/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء ملف PDF قابل للبحث من صورة باستخدام Java OCR

هل احتجت يومًا إلى **إنشاء ملف PDF قابل للبحث** من فاتورة ممسوحة ضوئيًا لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك—العديد من المطورين يواجهون هذه العقبة عندما يرغبون في ملف PDF يمكن البحث فيه فعليًا. الخبر السار؟ باستخدام Aspose OCR for Java يمكنك **تحويل الصورة إلى PDF**، تشغيل OCR في الوقت الفعلي، والحصول على ملف قابل للبحث مرتب في بضع أسطر من الشيفرة فقط.

في هذا الدرس سنستعرض العملية بالكامل: تحميل الصورة، إخبار المحرك باللغة المتوقعة، تنفيذ OCR، وأخيرًا حفظ **PDF قابل للبحث**. في النهاية ستعرف أيضًا كيفية **استخراج النص من الصورة** يدويًا، تعديل إعدادات اللغة، ومعالجة بعض الحالات الخاصة الشائعة. لا خدمات خارجية، لا أدوات سطر أوامر غامضة—فقط Java نقي.

## ما ستحتاجه

- Java 17 أو أحدث (واجهة البرمجة تعمل مع الإصدارات الأقدم أيضًا، لكن 17 هو الخيار المثالي).  
- مكتبة Aspose OCR for Java – يمكنك الحصول على أحدث JAR من Maven Central (`com.aspose:aspose-ocr:23.10`).  
- ملف صورة يحتوي على نص قابل للقراءة (PNG، JPG، أو TIFF).  
- قليل من الصبر في بيئة التطوير—IntelliJ IDEA أو VS Code يكفيان.

إذا كان لديك كل ذلك، رائع! إذا لم يكن، فإن مقتطف Maven أدناه سيجعلك جاهزًا للعمل:

```xml
<!-- Add to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

الآن بعد أن تم إعداد الأساس، دعنا نغوص في الشيفرة.

## الخطوة 1: تهيئة محرك OCR – قلب **إنشاء PDF قابل للبحث**

قبل حدوث أي تحويل، يجب إنشاء كائن `OcrEngine`. فكر فيه كالعقل الذي سيقرأ البكسلات ويحولها إلى أحرف.

```java
import com.aspose.ocr.*;

public class PdfExportDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

*لماذا هذا مهم:* يحتفظ المحرك بجميع إعدادات التعرف (اللغة، وضع الدقة، إلخ). إنشاءه مرة واحدة وإعادة استخدامه عبر صور متعددة أكثر كفاءة من إنشاء محرك جديد لكل ملف.

## الخطوة 2: **كيفية ضبط اللغة** – تحسين الدقة للفرنسية أو الألمانية أو أي نص

إذا كنت تعرف لغة المستند الأصلي، أخبر محرك OCR. هذا يسرّع المعالجة ويقلل الأخطاء.

```java
        // Step 2: (Optional) Specify the language to improve text extraction
        ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.FRENCH);
```

يمكنك استبدال `OcrLanguage.FRENCH` بـ `ENGLISH` أو `SPANISH` أو `GERMAN`، إلخ. إذا لم تكن متأكدًا، احذف السطر ودع Aspose يحدد اللغة تلقائيًا—لكن توقع انخفاضًا طفيفًا في الدقة.

## الخطوة 3: تحميل الصورة التي تريد **تحويل الصورة إلى PDF**

```java
        // Step 3: Load the image that contains the text to be recognized
        ocrEngine.setImage("YOUR_DIRECTORY/french_invoice.png");
```

طريقة `setImage` تقبل مسار ملف، `InputStream`، أو حتى كائن `java.awt.Image`. إذا كان لديك مصفوفة بايت (مثلاً من رفع ويب)، غلفها في `ByteArrayInputStream` ومررها مباشرة.

## الخطوة 4: تنفيذ OCR و **ocr image to pdf** في استدعاء واحد

Aspose يجعل هذه الخطوة سهلة: `recognizeToPdf` تشغل محرك التعرف وتكتب PDF قابل للبحث في خطوة واحدة.

```java
        // Step 4: Recognize the text and save it as a searchable PDF
        ocrEngine.recognizeToPdf("YOUR_DIRECTORY/french_invoice_searchable.pdf");
```

خلف الكواليس، المكتبة تنشئ طبقة نصية غير مرئية تتطابق مع الصورة الأصلية. عند فتح الملف الناتج في Adobe Reader، ستتمكن من كتابة كلمة في صندوق البحث والقفز فورًا إلى الموقع المطابق.

## الخطوة 5: التحقق من النتيجة – كيف يبدو الناتج؟

```java
        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF generated.");
    }
}
```

شغّل البرنامج، ثم افتح `french_invoice_searchable.pdf`. جرّب البحث عن كلمة تعرف أنها موجودة في الفاتورة (مثلاً “Total”). إذا تم تمييز الكلمة في المكان الصحيح، فقد نجحت في **إنشاء PDF قابل للبحث**.  
![مثال على إنشاء PDF قابل للبحث](example.png)<!-- alt text includes primary keyword -->

### النتيجة المتوقعة

```
Searchable PDF generated.
```

وملف PDF موجود في `YOUR_DIRECTORY` يمكنك مشاركته أو فهرسته أو أرشفته.

## الخطوة 6: استخراج النص الخام من الصورة (اختياري)

أحيانًا تحتاج النص الصافي لمعالجة إضافية—ربما لإدخاله في قاعدة بيانات أو تشغيل تحليل مشاعر. Aspose يتيح لك سحب النص المعترف به مباشرة:

```java
        // Optional: Get the extracted text as a String
        String extractedText = ocrEngine.getText();
        System.out.println("Extracted text:");
        System.out.println(extractedText);
```

هذا المقتطف يوضح **استخراج النص من الصورة** دون إنشاء PDF. مفيد عندما يهمك المحتوى فقط، وليس التخطيط البصري.

## معالجة صفحات أو صور متعددة

ماذا لو كان مصدر البيانات ملف TIFF متعدد الصفحات أو مجلد من JPEGs؟ يمكنك التكرار على الملفات واستدعاء `recognizeToPdf` لكل منها، ثم دمج ملفات PDF باستخدام Aspose PDF أو أي مكتبة أخرى. إليك نمط سريع:

```java
import java.io.File;
import com.aspose.pdf.*;

public class MultiPageDemo {
    public static void main(String[] args) throws Exception {
        OcrEngine engine = new OcrEngine();
        File folder = new File("YOUR_DIRECTORY/images");
        Document finalDoc = new Document();

        for (File img : folder.listFiles((d, n) -> n.matches(".*\\.(png|jpg|tif)"))) {
            engine.setImage(img.getAbsolutePath());
            // Save each page as a temporary PDF
            String tempPdf = img.getName() + ".pdf";
            engine.recognizeToPdf(tempPdf);
            // Append to final document
            Document pageDoc = new Document(tempPdf);
            finalDoc.getPages().add(pageDoc.getPages().get_Item(1));
        }
        finalDoc.save("YOUR_DIRECTORY/combined_searchable.pdf");
        System.out.println("All pages merged into searchable PDF.");
    }
}
```

**نصيحة احترافية:** احذف ملفات PDF المؤقتة بعد الدمج للحفاظ على نظافة مساحة العمل.

## الأخطاء الشائعة وكيفية تجنّبها

- **صور منخفضة الدقة:** تنخفض دقة OCR بشكل كبير تحت 150 dpi. قم بزيادة الدقة أو اطلب مسحًا بدقة أعلى إذا أمكن.  
- **صفحات مائلة:** الصورة المدورة قد تربك المحرك. استخدم `ocrEngine.getImagePreprocessingSettings().setDeskew(true)` لتصحيح الميل الخفيف تلقائيًا.  
- **لغة غير مدعومة:** تأكد من أن اللغة التي ضبطتها مدرجة في رخصة Aspose OCR؛ وإلا سيتراجع المحرك إلى الإنجليزية.  
- **ملفات كبيرة:** معالجة TIFF بحجم 30 MB قد تستهلك ذاكرة كبيرة. فكر في تقسيمه إلى أجزاء أصغر أو زيادة حجم heap للـ JVM (`-Xmx2g`).

## الخطوات التالية – إلى أين تتجه الآن

بعد أن أتقنت أساسيات **إنشاء PDF قابل للبحث**، قد ترغب في استكشاف:

- **تحويل دفعي:** دمج نمط الصفحات المتعددة مع جدولة لمعالجة المسحات الواردة كل ليلة.  
- **إدخال بيانات التعريف:** استخدم Aspose PDF لإضافة عنوان، مؤلف، أو وسوم مخصصة إلى PDF القابل للبحث.  
- **التوقيعات الرقمية:** أمان PDF بشهادة بعد OCR، لضمان الامتثال للوثائق القانونية.  

كل هذه الإضافات لا تزال تعتمد على المفاهيم الأساسية التي غطيناها: تهيئة محرك OCR، ضبط اللغة اختياريًا، تحميل الصورة، واستدعاء `recognizeToPdf`.

---

### TL;DR

استعرضنا مثالًا كاملًا وقابلًا للتنفيذ يوضح كيفية **إنشاء ملف PDF قابل للبحث** من صورة باستخدام Aspose OCR for Java. تشمل الخطوات تهيئة المحرك، ضبط اللغة (الإجابة على سؤال “كيفية ضبط اللغة”)، تحميل الصورة، تنفيذ OCR، حفظ PDF قابل للبحث، واستخراج النص الصافي اختياريًا. كما تناولنا معالجة صفحات متعددة، الأخطاء الشائعة، وأفكار لأتمتة إضافية.

جرّبه مع إيصالاتك، عقودك، أو ملاحظاتك المكتوبة يدويًا—حوّل تلك الصور الثابتة إلى مستندات قابلة للبحث بالكامل في ثوانٍ. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}