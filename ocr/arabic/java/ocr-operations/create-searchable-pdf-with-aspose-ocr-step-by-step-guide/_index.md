---
category: general
date: 2026-01-02
description: إنشاء ملف PDF قابل للبحث من ملف PDF يحتوي على صور ممسوحة ضوئياً باستخدام
  Aspose OCR. تعلّم كيفية تعيين لغة OCR، وإدراج طبقة نصية في ملف PDF، وتطبيق خيارات
  ضغط PDF عالية.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- high compression pdf
- embed text layer pdf
- set OCR language
language: ar
og_description: إنشاء ملف PDF قابل للبحث بسرعة. يوضح هذا الدليل كيفية تحويل ملف PDF
  الممسوح ضوئياً، وإدراج طبقة نصية، وتعيين لغة OCR، وتمكين ضغط عالي للملف PDF.
og_title: إنشاء ملف PDF قابل للبحث باستخدام Aspose OCR – دليل كامل
tags:
- Aspose OCR
- Java PDF
- Document Automation
title: إنشاء ملف PDF قابل للبحث باستخدام Aspose OCR – دليل خطوة بخطوة
url: /ar/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث – دليل برمجة كامل

هل احتجت يوماً إلى **إنشاء PDF قابل للبحث** من الصور الممسوحة ضوئياً لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك. في العديد من سير العمل التي تعتمد على الوثائق، يكون ملف PDF الذي يحتوي على صورة فقط dead‑end للبحث والفهرسة.  

الخبر السار هو أنه باستخدام Aspose OCR يمكنك **تحويل PDF صورة ممسوحة** إلى مستند قابل للبحث بالكامل في بضع أسطر من Java فقط. يشرح هذا الدليل كل خطوة — تهيئة محرك OCR، ضبط إعدادات PDF ذات الضغط العالي، تضمين طبقة نص مخفية، وحتى اختيار لغة OCR المناسبة.  

بنهاية هذا الدليل ستحصل على برنامج قابل للتنفيذ ينتج PDF قابل للبحث، وهو ملف يمكنك إدراجه في أي محرك بحث أو نظام إدارة مستندات دون أي مشاكل.

---

## إنشاء PDF قابل للبحث – نظرة عامة

قبل أن نغوص في الكود، دعونا نوضح ما يعنيه فعلاً “إنشاء PDF قابل للبحث”. يحتوي PDF القابل للبحث على طبقتين متوازيتين:

1. **الطبقة البصرية** – الصورة الممسوحة الأصلية (أو الصفحة المرسومة).  
2. **الطبقة النصية** – غير مرئية ولكنها أحرف قابلة للقراءة آليًا مستخرجة بواسطة OCR.  

عند فتح مثل هذا الـ PDF في Adobe Reader وتحديد النص، فإنك تتفاعل فعليًا مع طبقة النص المخفية، وليس الصورة. هذه المقاربة ذات الطبقتين هي ما يتيح وظيفة **embed text layer PDF**.

---

## تحويل PDF صورة ممسوحة باستخدام Aspose OCR

أول شيء تحتاجه هو صورة ممسوحة (PNG، JPEG، TIFF) تريد تحويلها إلى PDF. يمكن لـ Aspose OCR قراءة تلك الصورة، تشغيل OCR، وتسليم النتيجة إلى كاتب PDF.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Step 2: Configure PDF save options to embed a searchable text layer
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // enable searchable PDF
        pdfSaveOptions.setCompressionLevel(9);        // optional: high compression

        // Step 3: Perform OCR on the scanned image and save the result as a searchable PDF
        ocrEngine.recognizeImageAndSave(
                "YOUR_DIRECTORY/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,                // set OCR language
                "YOUR_DIRECTORY/output.pdf",                // output PDF file
                pdfSaveOptions);                            // options defined above

        // Step 4: Indicate that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

**لماذا هذا يعمل:**  
- `setCreateSearchablePdf(true)` يخبر Aspose بإنشاء طبقة النص المخفية، مما يلبي متطلب **embed text layer pdf**.  
- `setCompressionLevel(9)` يدفع الملف إلى نطاق **high compression pdf**، مما يقلص الحجم النهائي دون التضحية بدقة OCR.  
- معامل `RecognitionLanguage.ENGLISH` يوضح كيفية **set OCR language**؛ يمكنك استبداله بالفرنسية أو الألمانية، إلخ، حسب مادة المصدر.

---

## إعدادات PDF ذات الضغط العالي

يمكن أن تتضخم ملفات PDF الممسوحة الكبيرة بسرعة لتصل إلى مئات الميغابايت. تقدم Aspose واجهة برمجة تطبيقات ضغط بسيطة تعمل على مستوى PDF. طريقة `setCompressionLevel` تقبل قيمًا من 0 (بدون ضغط) إلى 9 (أقصى ضغط).

```java
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.setCompressionLevel(9); // 9 = strongest compression
```

بعض النصائح:

- **استخدم صيغ الصور غير الضائعة** (PNG) للمسحات التي تحتوي على نص كثيف؛ JPEG أفضل للصور الفوتوغرافية.  
- **فعّل تقليل الخطوط** إذا قمت بتضمين خطوط مخصصة—يقوم Aspose بذلك تلقائيًا عند إنشاء PDF قابل للبحث.  
- **اختبر حجم الناتج** بعد كل تعديل؛ أحيانًا يعطي ضغط المستوى 8 تقليلًا بنسبة 10 % في الحجم مع فقدان جودة ضئيل مقارنة بالمستوى 9.

---

## تضمين طبقة النص في PDF للبحث

إذا تخطيت استدعاء `setCreateSearchablePdf(true)`، سيظهر الملف الناتج جيدًا لكنك لن تتمكن من البحث في محتوياته. يتم إنشاء طبقة النص المخفية عن طريق ربط كل حرف مُعترف به بموقعه على الصفحة.

```java
pdfSaveOptions.setCreateSearchablePdf(true);
```

**ما يجب الانتباه إليه:**  

- **مستندات متعددة اللغات** – قد تحتاج إلى تشغيل OCR مرتين، مرة لكل لغة، ثم دمج طبقات النص.  
- **تخطيطات معقدة** (جداول، متعددة الأعمدة) – يقوم Aspose بعمل جيد، لكن تحقق من الناتج باستخدام عارض PDF يُظهر النص المخفي (مثل وضع “Edit PDF” في Adobe Acrobat).

---

## ضبط لغة OCR للتعرف الدقيق

تعتمد دقة محرك OCR على اللغة التي تخبره بتوقعها. يأتي Aspose بمجموعة من اللغات المدمجة، ويمكنك أيضًا إضافة حزم لغات مخصصة.

```java
ocrEngine.recognizeImageAndSave(
        "input.png",
        RecognitionLanguage.ENGLISH, // change to RecognitionLanguage.FRENCH, etc.
        "output.pdf",
        pdfSaveOptions);
```

**متى تغير اللغة:**  

- المستندات تحتوي على **نصوص غير لاتينية** (سيريلية، عربية) – انتقل إلى `RecognitionLanguage` المناسب.  
- صفحات متعددة اللغات – يمكنك استدعاء `recognizeImageAndSave` مرتين، كل مرة بلغة مختلفة، ثم دمج ملفات PDF.

---

## تشغيل المثال الكامل

فيما يلي البرنامج الكامل الجاهز للتنفيذ. استبدل مسارات العناصر النائبة بمواقع الملفات الفعلية، وتأكد من وجود ملف JAR الخاص بـ Aspose OCR في مسار الفئات الخاص بك، ثم نفّذ.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Configure PDF save options
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // embed text layer PDF
        pdfSaveOptions.setCompressionLevel(9);        // high compression PDF

        // Perform OCR and save searchable PDF
        ocrEngine.recognizeImageAndSave(
                "C:/scans/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,          // set OCR language
                "C:/output/searchable.pdf",           // output PDF
                pdfSaveOptions);                      // options defined above

        System.out.println("Searchable PDF created.");
    }
}
```

**المخرجات المتوقعة:** عند تشغيل البرنامج، يطبع الطرفية:

```
Searchable PDF created.
```

افتح `searchable.pdf` في أي عارض PDF، حاول تحديد النص، وسترى الطبقة المخفية تعمل. لقد نجحت في **إنشاء PDF قابل للبحث** من صورة ممسوحة.

---

![مثال إنشاء PDF قابل للبحث](image-placeholder.png "مثال إنشاء PDF قابل للبحث")

*لقطة الشاشة أعلاه (عنصر نائب) عادةً ما تُظهر عارض PDF مع نص قابل للتحديد فوق صفحة ممسوحة.*

---

## الخلاصة

لقد غطينا كل ما تحتاجه لإنشاء ملفات **PDF قابل للبحث** باستخدام Aspose OCR:

- تهيئة محرك OCR.  
- **تحويل PDF صورة ممسوحة** عن طريق تمرير PNG/JPEG إلى `recognizeImageAndSave`.  
- استخدم `setCreateSearchablePdf(true)` لـ **embed text layer PDF**.  
- طبّق `setCompressionLevel(9)` للحصول على **high compression PDF** يظل خفيفًا.  
- اختر `RecognitionLanguage` المناسب لـ **set OCR language** لتحقيق أقصى دقة.

من هنا يمكنك تجربة المعالجة الدفعية، لغات مختلفة، أو حتى دمج صفحات ممسوحة متعددة في PDF قابل للبحث واحد. النمط نفسه يعمل مع لغات أخرى مثل الإسبانية أو اليابانية—فقط استبدل تعداد `RecognitionLanguage`.

لا تتردد في ترك تعليق إذا واجهت أي صعوبات، وبرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}