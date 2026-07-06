---
category: general
date: 2026-02-19
description: تعلم كيفية تصحيح انحراف الصورة وإزالة الضوضاء من أجل OCR. يوضح هذا الدليل
  كيفية التعرف على صورة النص، وتصحيح دوران الصورة، ومعالجة صورة OCR مسبقًا باستخدام
  Aspose OCR.
draft: false
keywords:
- how to deskew image
- recognize text image
- how to remove noise
- correct image rotation
- preprocess image ocr
language: ar
og_description: كيفية تصحيح انحراف الصورة وإزالة الضوضاء لتتمكن من التعرف على النص
  في الصورة بسرعة. اتبع هذا الدليل لتصحيح دوران الصورة ومعالجة الصورة مسبقًا لتقنية
  OCR باستخدام Aspose.
og_title: كيفية تصحيح إمالة الصورة – دليل شامل لمعالجة ما قبل التعرف الضوئي على الأحرف
tags:
- OCR
- Java
- Image Processing
title: كيفية تصحيح إمالة الصورة — دليل خطوة بخطوة لمعالجة ما قبل التعرف الضوئي على
  الأحرف (OCR)
url: /ar/java/ocr-operations/how-to-deskew-image-step-by-step-ocr-pre-processing-guide/
---

is. It appears bold. We'll keep the bold phrase unchanged. Similarly "recognize text image". Keep those.

Proceed.

Will translate accordingly.

Let's craft Arabic text.

Be careful with RTL: just Arabic text.

Now bullet list.

Ok.

Now produce final.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصحيح ميلان الصورة — دورة شاملة لمعالجة ما قبل OCR

هل تساءلت يوماً **how to deskew image** قبل تمرير الملفات إلى محرك OCR؟ ربما قمت بمسح مجموعة من الإيصالات، وتبدو الصفحات وكأنها مائلة قليلاً، أو أن المسح مليء بنقاط عشوائية. هذه مشكلة شائعة—الصور المائلة والضوضائية تجعل التعرف على النص يتعثر.  

الخبر السار؟ يمكنك تعديل (تصحيح دوران الصورة) وإزالة الضوضاء (how to remove noise) ببضع أسطر من Java باستخدام Aspose.OCR. في هذا الدليل سنستعرض التدفق الكامل: من تحميل صورة PNG ملوثة ومائلة، تطبيق تصحيح الميلان + إزالة الضوضاء بالمتوسط، وصولاً إلى **recognize text image** وطباعة النتيجة. في النهاية ستحصل على مقتطف يمكن إعادة استخدامه في أي مشروع Java.

## ما ستحتاجه

- **Java 17** أو أحدث (الكود يتوافق مع الإصدارات الأقدم، لكن 17 هو الأنسب).  
- **Aspose.OCR for Java** – يمكنك الحصول على أحدث JAR من Maven Central (`com.aspose:aspose-ocr`).  
- ملف صورة مائل ومشوَّش (مثال: `noisy-rotated.png`).  
- بيئة تطوير متوسطة (IntelliJ، Eclipse، أو حتى VS Code).  

لا تحتاج إلى أدوات بناء معقدة؛ تشغيل بسيط بـ `javac` + `java` يكفي.

---

## الخطوة 1 – إنشاء كائن محرك OCR  

أول ما تقوم به هو إنشاء `OcrEngine`. فكر فيه كالعقل الذي سيقرأ الأحرف لاحقاً.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **نصيحة احترافية:** احتفظ بالمحرك ككائن Singleton إذا كنت تعالج العديد من الصور؛ فهو يعيد استخدام الذاكرة الداخلية ويسرّع العملية.

## الخطوة 2 – تفعيل تصحيح الميلان وإزالة الضوضاء بالمتوسط (How to Remove Noise)

الآن نخبر المحرك بـ **correct image rotation** و **how to remove noise**. كلا الفلترين اختياريان، لكن معاً يحسّنان الدقة بشكل كبير.

```java
        // Turn on preprocessing filters
        ocrEngine.getPreprocessing().setDeskew(true);          // fixes rotation
        ocrEngine.getPreprocessing().setMedianDenoise(true);   // smooths out speckles
```

لماذا إزالة الضوضاء بالمتوسط؟ لأنها تحافظ على الحواف (الخطوط التي تحدد الأحرف) بينما تمسح البكسلات المنعزلة—بالضبط ما تحتاجه للحصول على OCR نظيف.

## الخطوة 3 – تحميل الصورة التي تريد معالجتها  

هنا نوجه المحرك إلى الملف الذي يحتاج إلى تنظيف. `ImageStream.fromFile` يقرأ PNG إلى الذاكرة.

```java
        // Load the noisy‑rotated image
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/noisy-rotated.png"));
```

إذا كانت صورتك موجودة على خادم بعيد، ما عليك سوى تمرير `InputStream` بدلاً من ذلك—Aspose يتعامل مع ذلك بسلاسة.

## الخطوة 4 – تشغيل OCR والتقاط النص المُستخرج  

مع تفعيل المعالجة المسبقة، يقرأ المحرك الآن الصورة المصححة. استدعاء `recognize()` يُعيد كائن `RecognitionResult` يحتوي على السلسلة المستخرجة.

```java
        // Perform OCR – the engine automatically applies deskew & denoise first
        String recognizedText = ocrEngine.recognize().getText();

        // Show the output
        System.out.println("=== Recognized Text ===");
        System.out.println(recognizedText);
    }
}
```

سترى نصاً نظيفاً وقابلاً للقراءة في وحدة التحكم، حتى وإن كانت الصورة الأصلية مائلة ومشوشة.

## الخطوة 5 – التحقق من النتيجة (ما المتوقع)

عند نجاح العملية، ستظهر في وحدة التحكم نتيجة مشابهة لـ:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑02‑15
Total: $1,234.56
```

إذا ظل الإخراج يحتوي على أحرف غير مفهومة، تحقق من التالي:

- دقة الصورة (≥ 300 dpi هي المثالية).  
- صحة مسار الملف.  
- ما إذا كانت فلاتر إضافية (مثل `setContrastStretch`) قد تساعد.

---

## اختياري: تأكيد بصري باستخدام صورة مثال  

في الأسفل معاينة صغيرة لإيصال مائل ومشوَّش. لاحظ الميل—الكود سيصححه لك.

![مثال على تصحيح الميلان للصورة](deskew-demo.png "how to deskew image")

*نص بديل: مثال على تصحيح الميلان للصورة – قبل وبعد المعالجة.*

---

## الأسئلة المتكررة

### هل يعمل هذا مع ملفات PDF أم فقط PNG/JPEG؟  
Aspose.OCR يمكنه قراءة ملفات PDF مباشرة؛ فقط استبدل `ImageStream.fromFile` بـ `ImageStream.fromPdf`. نفس خيارات المعالجة المسبقة تُطبق، لذا ستحصل على **how to deskew image** و **how to remove noise**.

### ماذا لو أردت الحفاظ على الاتجاه الأصلي للصور لخطوات لاحقة؟  
يمكنك استنساخ الصورة قبل المعالجة:

```java
Image original = ocrEngine.getImage().clone();
ocrEngine.getPreprocessing().apply(); // modifies the internal copy
// Use original later if needed
```

### هل يمكنني تغيير زاوية تصحيح الميلان يدوياً؟  
نعم—`setDeskewAngle(double degrees)` يتيح لك تجاوز الخوارزمية التلقائية. مفيد عندما تفشل الكشف التلقائي عند دوران شديد.

### كيف يختلف إزالة الضوضاء بالمتوسط عن تمويه Gaussian؟  
فلاتر المتوسط تستبدل كل بكسل بمتوسط جيرانه، مما يحافظ على الحواف. تمويه Gaussian يُنعم كل شيء، وقد يطمس خطوط الأحرف—لذا المتوسط هو الخيار الأكثر أماناً لـ OCR.

---

## الخلاصة  

في هذا الدرس غطينا **how to deskew image**، وأظهرنا **how to remove noise**، وبيّنّا لك كيفية **recognize text image** باستخدام المعالجة المدمجة في Aspose OCR. عبر تفعيل `setDeskew(true)` و `setMedianDenoise(true)`، تقوم تلقائياً بـ **correct image rotation** وتنظيف البقع، محوّلاً مسحاً فوضوياً إلى نص نظيف.  

لا تتردد في التجربة: جرّب استراتيجيات إزالة ضوضاء مختلفة، عالج ملفات PDF، أو ربط عدة صور في حلقة. النمط نفسه—المحرك → المعالجة المسبقة → التعرف—ينطبق على أي سيناريو، مما يجعله أساساً متيناً لأي خط أنابيب OCR.

**الخطوات التالية** التي قد تستكشفها:

- **المعالجة الدفعية** – تكرار عبر مجلد من الصور وكتابة كل نتيجة إلى ملف `.txt`.  
- **حزم اللغات** – تحميل قاموس لغة محددة لزيادة الدقة للنص غير الإنجليزي.  
- **فلاتر متقدمة** – مثل `setContrastStretch` أو `setBinarization` للمسحات ذات التباين المنخفض.  

هل لديك أسئلة أخرى؟ اترك تعليقاً، ونتمنى لك برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}