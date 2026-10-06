---
category: general
date: 2026-02-19
description: إنشاء ملف PDF قابل للبحث من صورة JPG باستخدام Aspose OCR في Java. تحويل
  JPG إلى PDF والتعرف على النص من الصورة بسرعة.
draft: false
keywords:
- create searchable pdf
- image to searchable pdf
- recognize text from image
- extract text from jpg
- convert jpg to pdf
language: ar
og_description: إنشاء ملف PDF قابل للبحث من صورة JPG باستخدام Aspose OCR. تعلم كيفية
  تحويل JPG إلى PDF والتعرف على النص من الصورة في Java.
og_title: إنشاء ملف PDF قابل للبحث من JPG – دليل Java OCR
tags:
- aspose-ocr
- java
- pdf
- ocr
title: إنشاء ملف PDF قابل للبحث من JPG – دليل جافا لتحويل الصورة إلى PDF قابل للبحث
url: /ar/java/ocr-operations/create-searchable-pdf-from-jpg-image-to-searchable-pdf-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث من JPG – دليل Java لتحويل الصورة إلى PDF قابل للبحث

هل احتجت يوماً إلى **إنشاء PDF قابل للبحث** من صورة ممسوحة ضوئياً لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك—العديد من المطورين يواجهون نفس المشكلة عندما يكون لديهم ملف JPG يحتاج إلى أن يكون قابلًا للبحث. الخبر السار هو أنه باستخدام Aspose OCR for Java يمكنك تحويل تلك الصورة إلى PDF قابل للبحث بالكامل ببضع أسطر من الشيفرة.

في هذا الدرس سنستعرض العملية بالكامل: تحميل JPG، التعرف على النص، وحفظ النتيجة كملف PDF قابل للبحث. في النهاية ستعرف كيف **تحول jpg إلى pdf**، كيف **استخراج النص من jpg**، ولماذا يعتبر هذا النهج أكثر موثوقية غالبًا من محاولة OCR للـ PDF بعد إنشائه.

## ما ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي على جهازك:

* **Java Development Kit (JDK) 8 أو أحدث** – يستخدم الكود واجهات برمجة تطبيقات Java القياسية.  
* مكتبة **Aspose OCR for Java** – يمكنك الحصول عليها من Maven Central أو تحميل ملف JAR من موقع Aspose.  
* **ملف JPG تجريبي** يحتوي على نص قابل للقراءة (مثل فاتورة ممسوحة أو لقطة شاشة لوثيقة).

لا توجد أطر عمل إضافية مطلوبة؛ المثال يعمل مع مشروع Java عادي.

## الخطوة 1 – إعداد المشروع وإضافة Aspose OCR

أولاً، أنشئ مشروع Maven جديد (أو مجرد مجلد يحتوي على ملف JAR في مسار الـ classpath). إذا كنت تستخدم Maven، أضف هذا الاعتماد إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

> **نصيحة احترافية:** تحقق دائمًا من أحدث نسخة في مستودع Aspose Maven؛ الإصدارات الأحدث تتضمن تحسينات في الأداء وإصلاحات للأخطاء.

بعد حل الاعتماد، أنت جاهز لكتابة كود Java الذي سي **ينشئ PDF قابل للبحث**.

## الخطوة 2 – تحميل الصورة (image to searchable pdf)

الخطوة الفعلية الأولى هي توجيه محرك OCR إلى صورة المصدر. هنا يبدأ التحويل من **image to searchable pdf** فعليًا.

```java
import com.aspose.ocr.*;

public class SearchablePdfExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the JPG you want to turn into a searchable PDF
        // Replace "YOUR_DIRECTORY/input.jpg" with the actual path to your file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

> **لماذا هذا مهم:** `setImage` يخبر Aspose أي صورة bitmap يجب تحليلها. إذا قدمت صورة منخفضة الدقة، سيتأثر جودة OCR، لذا تأكد من أن JPG بدقة لا تقل عن 300 dpi للحصول على أفضل النتائج.

## الخطوة 3 – التعرف على النص من الصورة

الآن بعد أن يعرف المحرك أي صورة سيعمل عليها، يمكننا أن نطلب منه **التعرف على النص من الصورة**. تقوم Aspose OCR بالمعالجة الثقيلة في الخلفية، بما في ذلك اكتشاف اللغة، تجزئة الأحرف، وتقييم الثقة.

```java
        // Perform OCR and directly output a searchable PDF
        ocrEngine.recognize()
                 .save("YOUR_DIRECTORY/output-searchable.pdf", OcrOutputFormat.SEARCHABLE_PDF);
```

نداء `recognize()` يُعيد واجهة سلسة، مما يسمح بربط طريقة `save`. عند تحديد `OcrOutputFormat.SEARCHABLE_PDF`، تُدرج المكتبة طبقة نصية غير مرئية داخل الـ PDF مع الحفاظ على مظهر الصورة الأصلي.

> **حالة خاصة:** إذا كان JPG يحتوي على عدة صفحات (مثل TIFF متعدد الصفحات محفوظ كملفات JPG منفصلة)، ستحتاج إلى حلقة تمر على كل ملف ودمج ملفات PDF الناتجة لاحقًا. يمكن إعادة استخدام نفس محرك OCR لكل تكرار.

## الخطوة 4 – التحقق من النتيجة

بعد إكمال عملية الحفظ، رسالة بسيطة في وحدة التحكم تُخبرك بأن كل شيء تم بنجاح.

```java
        // Let the user know the PDF is ready
        System.out.println("Searchable PDF created.");
    }
}
```

عند فتح `output-searchable.pdf` في عارض مثل Adobe Acrobat، يجب أن تكون قادرًا على تحديد النص المخفي، نسخه، أو إجراء بحث—تمامًا ما تتوقعه من **PDF قابل للبحث**.

### النتيجة المتوقعة

تشغيل البرنامج يطبع:

```
Searchable PDF created.
```

وسيظهر الـ PDF المُولد JPG الأصلي مع إمكانية تحديد النص. إذا فتحت “Properties → Description → PDF Producer” في الـ PDF، سترى شيئًا مثل `Aspose.OCR for Java`.

## مثال كامل يعمل

فيما يلي الملف المصدر الكامل وجاهز للتنفيذ. انسخه‑الصقه في بيئة التطوير المتكاملة (IDE)، عدل مسارات الملفات، ثم شغّله.

```java
import com.aspose.ocr.*;

public class SearchablePdfExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image containing the text to be recognized
        // Make sure the path points to a real JPG on your disk
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 3: Recognize the text and directly save it as a searchable PDF
        ocrEngine.recognize()
                 .save("YOUR_DIRECTORY/output-searchable.pdf", OcrOutputFormat.SEARCHABLE_PDF);

        // Step 4: Notify that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

> **ماذا لو فشل الـ OCR؟**  
> * عادةً يحدث ذلك لأن الصورة مليئة بالضوضاء أو اللغة غير مدعومة مباشرة. يمكنك تحسين الدقة بمعالجة مسبقة للصورة (زيادة التباين، تصحيح الميل) أو بتحديد اللغة صراحةً باستخدام `ocrEngine.getLanguage().setLanguage(OcrLanguage.English);`.

## أسئلة شائعة ومشكلات محتملة

| السؤال | الإجابة |
|----------|--------|
| **هل يمكنني استخراج النص العادي بدلاً من PDF؟** | نعم. استخدم `ocrEngine.recognize().save("output.txt", OcrOutputFormat.TEXT);` |
| **ماذا لو احتجت لمعالجة PNG؟** | نفس الـ API يعمل؛ فقط غير امتداد الملف في `fromFile`. |
| **هل الـ PDF الناتج قابل للبحث فعلاً على جميع المشاهدين؟** | المشاهدات الحديثة (Adobe Reader, Foxit, Chrome) تحترم طبقة النص المخفي. الأدوات القديمة قد تتجاهلها. |
| **كيف يمكنني التحكم في حجم صفحة PDF؟** | Aspose OCR يستخدم أبعاد الصورة افتراضيًا. للحصول على حجم مخصص، أنشئ PDF يدويًا واطلق طبقة نص OCR فوقه—هذا سيناريو متقدم. |

## نصائح الأداء

* **المعالجة الدفعية:** أعد استخدام كائن `OcrEngine` واحد للعديد من الصور لتجنب تحميل المكتبة الأصلية المتكرر.  
* **سلامة الخيوط:** المحرك **ليس** آمنًا للاستخدام المتعدد الخيوط؛ أنشئ نسخة لكل خيط إذا كنت تُنفّذ عمليات متوازية.  
* **استهلاك الذاكرة:** الصور الكبيرة قد تستهلك الكثير من الذاكرة. إذا واجهت `OutOfMemoryError`، قلل أبعاد الصورة قبل تمريرها إلى المحرك.

## الخطوات التالية

الآن بعد أن عرفت كيف **تنشئ PDF قابل للبحث**، قد ترغب في استكشاف مهام ذات صلة:

* **تحويل jpg إلى pdf** بدون OCR (استخدم مكتبة Aspose PDF لإنشاء PDF بصورة عادية).  
* **استخراج النص من jpg** إلى ملف `.txt` للفهرسة.  
* **دمج عدة PDFs قابلة للبحث** في مستند واحد باستخدام `PdfFileEditor` من Aspose PDF.  

كل هذه تبني على الأساس نفسه الذي أعددته للتو.

---

### ملخص سريع

* قمنا **بإنشاء PDF قابل للبحث** من JPG باستخدام Aspose OCR for Java.  
* شمل العملية تحميل الصورة، التعرف على النص، وحفظه كـ PDF قابل للبحث.  
* لديك الآن نمط قابل لإعادة الاستخدام لـ **image to searchable PDF**، **recognize text from image**، **extract text from jpg**، و **convert jpg to pdf**.

جرّبه مع مستنداتك الخاصة، عدّل إعدادات اللغة إذا لزم الأمر، ودع OCR يتولى العمل الشاق. برمجة سعيدة!  

![إنشاء مثال PDF قابل للبحث](placeholder.png){alt="إنشاء مثال PDF قابل للبحث"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}