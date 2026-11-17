---
category: general
date: 2026-03-18
description: كيفية تصحيح انحراف الصورة بسرعة باستخدام Aspose OCR Java. تعلم كيفية
  تمهيد الصورة للتعرف الضوئي على الأحرف، وتنظيف الصورة الممسوحة ضوئياً، وتحسين دقة
  التعرف الضوئي على الأحرف في بضع خطوات فقط.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- clean scanned image
- improve ocr accuracy
language: ar
og_description: كيفية تصحيح ميل الصورة باستخدام Aspose OCR Java، ومعالجة الصورة مسبقًا
  للتعرف الضوئي على الأحرف، وتنظيف الصورة الممسوحة ضوئيًا وتحسين دقة التعرف الضوئي
  على الأحرف.
og_title: كيفية تصحيح إمالة الصورة للتعرف الضوئي على الحروف – دليل جافا
tags:
- OCR
- Java
- Image Processing
title: كيفية تصحيح انحراف الصورة للتعرف الضوئي على الأحرف – دليل المعالجة المسبقة
  بلغة جافا
url: /ar/java/advanced-ocr-techniques/how-to-deskew-image-for-ocr-java-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصحيح إمالة الصورة للتعرف الضوئي على الحروف (OCR) – دليل ما قبل المعالجة بجافا

هل تساءلت يومًا **كيف تصحح إمالة الصورة** التي تخرج من الماسح الضوئي بزاوية غريبة؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عندما يحاولون استخراج النص من المستندات التي تحتوي على الكثير من الصور. الخبر السار؟ ببضع أسطر من جافا ومكتبة Aspose OCR يمكنك تسوية الصورة، إزالة الضوضاء، واستخراج نص نظيف دون عناء.

في هذا الدرس سنستعرض سير العمل بالكامل: تحميل مسح ضوضائي ومائل، تطبيق مرشح تصحيح الإمالة، إزالة الفوضى البصرية، وأخيرًا **استخراج النص من الصورة**. في النهاية ستعرف كيف **تُعِد الصورة للـ OCR**، **تنظف ملفات الصور الممسوحة**، و**تحسّن دقة الـ OCR** لأي مشروع يحتاج إلى استخراج نص موثوق.

## ما ستحتاجه

- Java 17 (أو أي JDK حديث) – يستخدم الكود ميزات اللغة القياسية.
- مكتبة Aspose OCR لجافا (الإصدار التجريبي المجاني يكفي للتجربة).
- صورة نموذجية تحتوي على ضوضاء وإمالة (مثال: `noisy-rotated.png`).
- بيئتك المفضلة للتطوير (IntelliJ IDEA، Eclipse، VS Code…) – أي شيء يمكنه تجميع جافا.

لا حاجة لإطارات عمل إضافية، ولا حاجة لسحر Maven/Gradle؛ جمل الاستيراد الوحيدة هي تلك المعروضة أدناه.

---

## كيفية تصحيح إمالة الصورة باستخدام Aspose OCR

أول شيء يجب معالجته هو ميل الصورة. إذا لم تكن أسطر النص أفقية، سيقرأ محرك الـ OCR الأحرف بشكل خاطئ. يقوم `DeskewFilter` بالعمل الشاق.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;
import com.aspose.ocr.preprocess.DeskewFilter;
import com.aspose.ocr.preprocess.DenoiseFilter;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the raw scanned image
        Image scannedImage = Image.load("YOUR_DIRECTORY/noisy-rotated.png");

        // Step 3: Correct the image orientation (deskew)
        DeskewFilter deskewFilter = new DeskewFilter();
        scannedImage = deskewFilter.apply(scannedImage);

        // Step 4: Reduce visual noise (denoise)
        DenoiseFilter denoiseFilter = new DenoiseFilter();
        scannedImage = denoiseFilter.apply(scannedImage);

        // Step 5: Perform OCR on the cleaned image
        String recognizedText = ocrEngine.recognize(scannedImage);

        // Step 6: Output the extracted text
        System.out.println(recognizedText);
    }
}
```

> **لماذا هذا مهم:** يقوم `DeskewFilter` بتحليل هندسة الصورة، يقدّر زاوية الدوران، ويعيد تدوير البت ماب إلى أفق مستوي. بدون هذه الخطوة، معظم محركات الـ OCR تتعامل مع الأحرف المائلة كرموز مختلفة تمامًا، مما يضع جهودك في **تحسين دقة الـ OCR** في دوامة لا نهائية.  
> **نصيحة احترافية:** إذا كنت تتعامل مع مستندات قد تكون مقلوبة، فعّل علم `setAutoRotate` على `DeskewFilter` (متاح في إصدارات Aspose الأحدث). يقوم تلقائيًا بقلب الصورة 180° عند الحاجة.

![مخطط يوضح قبل وبعد الدوران – كيفية تصحيح إمالة الصورة](https://example.com/deskew-diagram.png "مثال على كيفية تصحيح إمالة الصورة")

*نص بديل للصورة: مثال على كيفية تصحيح إمالة الصورة*

---

## إعداد الصورة للـ OCR – إزالة الضوضاء والتنظيف

بعد أن تصبح الصورة مستقيمة، التحدي التالي هو الضوضاء البصرية—البقع، عيوب الضغط، أو الأنماط الخلفية الخفيفة التي تربك محرك الـ OCR. يقوم `DenoiseFilter` بتطبيق خوارزمية تنعيم دقيقة تحافظ على الحواف (الأحرف) بينما تمحو الحبيبات.

```java
// Step 4 (continued): Reduce visual noise (denoise)
DenoiseFilter denoiseFilter = new DenoiseFilter();
scannedImage = denoiseFilter.apply(scannedImage);
```

### متى تعديل إعدادات إزالة الضوضاء

- **مسحات داكنة جدًا:** زيادة قوة الفلتر (`denoiseFilter.setStrength(2)`) لإزالة ظلال الخلفية.
- **خطوط دقيقة:** خفض القوة لتجنب تشويش الزوائد الصغيرة.
- **مستندات ملونة:** تحويلها إلى تدرج الرمادي أولاً (`scannedImage = scannedImage.toGrayscale();`)—محرك الـ OCR يعمل بأفضل شكل على الصور أحادية القناة.

هذه التعديلات جزء من ممارسات **تنظيف الصور الممسوحة** المثلى؛ bitmap أنظف يترجم مباشرة إلى درجات ثقة أعلى من محرك الـ OCR.

---

## استخراج النص من الصورة – تشغيل محرك الـ OCR

الآن بعد أن أصبحت الصورة مستقيمة وخالية من الضوضاء، حان الوقت **لاستخراج النص من الصورة**. تتولى فئة `OcrEngine` كل شيء في الخلفية: التجزئة، تصنيف الأحرف، ونمذجة اللغة.

```java
// Step 5: Perform OCR on the cleaned image
String recognizedText = ocrEngine.recognize(scannedImage);
System.out.println(recognizedText);
```

#### النتيجة المتوقعة

إذا كان ملف المصدر يحتوي على السطر “**Invoice # 12345**”، يجب أن يطبع الطرفية شيئًا مشابهًا لـ:

```
Invoice # 12345
Date: 2026-03-18
Total: $1,250.00
```

إذا كان الناتج مشوشًا، تحقق مرة أخرى من الخطوات السابقة—خاصةً تصحيح الإمالة. حتى ميل قدره درجة واحدة يمكن أن يفسد الأرقام والرموز.

---

## الأخطاء الشائعة ونصائح **تحسين دقة الـ OCR**

| المشكلة | لماذا يؤثر على الدقة | الحل السريع |
|---------|----------------------|-------------|
| **دوران متبقي** | يتوقع الـ OCR خطوط أساس أفقية. | تحقق باستخدام `deskewFilter.getAngle()` وسجّل القيمة. |
| **إزالة ضوضاء مفرطة** | يمحو الخطوط الرفيعة، محولًا “i” إلى “l”. | استخدم `setStrength(0.5)` للخطوط الحساسة. |
| **تنسيق صورة غير صحيح** | ضغط JPEG يضيف عيوبًا. | يفضل PNG أو TIFF للتخزين بدون فقد. |
| **لغة غير صحيحة** | المحرك يفرض الإنجليزية افتراضيًا؛ الأحرف الأبجدية الأخرى تحتاج إلى تعيين صريح. | `ocrEngine.setLanguage(OcrEngine.Language.Spanish);` |
| **دقة DPI منخفضة (≤150)** | ليس هناك بيانات بكسل كافية لتجزئة موثوقة. | أعد التحويل إلى 300 DPI قبل المعالجة (`scannedImage = scannedImage.resample(300);`). |

### إضافي: المعالجة الدفعية

إذا كان لديك مجلد من المسحات، غلف العرض التجريبي داخل حلقة:

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.endsWith(".png"))) {
    Image img = Image.load(file.getAbsolutePath());
    img = new DeskewFilter().apply(img);
    img = new DenoiseFilter().apply(img);
    String text = ocrEngine.recognize(img);
    System.out.println("=== " + file.getName() + " ===");
    System.out.println(text);
}
```

هذا النمط يتيح لك **إعداد الصورة للـ OCR** على نطاق واسع، مع الحفاظ على نظافة قاعدة الشيفرة وتوقع الأداء.

---

## ملخص وخطوات مستقبلية

لقد غطينا **كيفية تصحيح إمالة الصورة**، **إعداد الصورة للـ OCR**، وأخيرًا **استخراج النص من الصورة** باستخدام Aspose OCR Java. من خلال تسوية المسح، تنظيف الضوضاء، وإمداد المحرك بصورة bitmap نقية، ستحقق **تحسين دقة الـ OCR** بشكل ملحوظ في جميع الحالات.

ما الخطوة التالية؟ فكر في هذه الإضافات:

- **اكتشاف اللغة** – غيّر `ocrEngine.setLanguage` بناءً على النص المكتشف.  
- **إخراج PDF** – أدخل النص المعترف به إلى مولد PDF لإنشاء مستندات قابلة للبحث.  
- **معالجة ما بعد التعلم الآلي** – نفّذ تدقيق إملائي أو قواميس مخصصة على نتيجة الـ OCR.

جرّب هذه الأفكار، واختبر قوّات الفلاتر المختلفة، وستحصل قريبًا على خط أنابيب قوي لأي مشروع رقمنة مستندات.

*برمجة سعيدة! إذا واجهت أي مشكلة، اترك تعليقًا أدناه—سأساعدك في ضبط معلمات تصحيح الإمالة وإزالة الضوضاء.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}