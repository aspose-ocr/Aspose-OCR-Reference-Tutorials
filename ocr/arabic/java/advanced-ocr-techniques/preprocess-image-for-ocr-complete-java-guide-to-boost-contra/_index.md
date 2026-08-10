---
category: general
date: 2026-02-17
description: معالجة الصورة مسبقًا للتعرف الضوئي على الحروف باستخدام Aspose OCR في
  جافا. تعلم كيفية تعزيز تباين الصورة، وضبط مستوى التباين، والتعرف على النص من الصورة
  في دقائق قليلة.
draft: false
keywords:
- preprocess image for ocr
- boost image contrast
- recognize text from image
- extract text using OCR
- set contrast level
language: ar
og_description: معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف باستخدام Aspose OCR
  Java. يوضح هذا الدليل كيفية تعزيز تباين الصورة، ضبط مستوى التباين، والتعرف بسرعة
  على النص من الصورة.
og_title: معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف – درس جافا لتعزيز التباين
  واستخراج النص
tags:
- Java
- OCR
- Image Processing
title: معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف – دليل جافا الكامل لتعزيز التباين
  واستخراج النص
url: /ar/java/advanced-ocr-techniques/preprocess-image-for-ocr-complete-java-guide-to-boost-contra/
---

Now ensure all markdown formatting preserved.

Check for any missing translation of bullet points, etc.

Now produce final output with all content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# معالجة الصورة للتعرف الضوئي على الأحرف – دليل Java كامل

هل احتجت يومًا إلى **preprocess image for OCR** لكن لم تكن متأكدًا من الإعدادات التي تُحدث فرقًا فعليًا؟ لست وحدك. معظم المطورين يرسلون صورة إلى محرك OCR ويأملون حدوث السحر، فقط للحصول على مخرجات مشوشة. في هذا البرنامج التعليمي سنستعرض مثالًا عمليًا من البداية إلى النهاية يقوم **boosts image contrast**، ويضبط **contrast level**، وأخيرًا **recognizes text from image** باستخدام Aspose OCR for Java.

بحلول الوقت الذي تنتهي فيه، ستحصل على مقتطف شفرة قابل لإعادة الاستخدام يقوم **extracts text using OCR** بشكل موثوق، حتى على المسحات الضوضائية. لا حيل مخفية، فقط خطوات واضحة والمنطق وراء كل خطوة.

## ما ستحتاجه

- Java 17 أو أحدث (الكود يُترجم مع أي JDK حديث)
- مكتبة Aspose OCR for Java (حمّلها من الموقع الرسمي لـ Aspose)
- ملف ترخيص Aspose OCR صالح (`Aspose.OCR.lic`)
- صورة الإدخال (`input.jpg`) التي تريد قراءتها
- بيئة تطوير مفضلة أو إعداد سطر أوامر بسيط

إذا كان لديك هذه بالفعل، عظيم—لنغص مباشرةً.

## الخطوة 1: تحميل ترخيص Aspose OCR (الإعداد الأساسي)

قبل أن يقوم محرك OCR بأي شيء، يحتاج إلى معرفة أنك مرخص. وإلا ستواجه علامة مائية تجريبية.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {

        // Load the Aspose OCR license – this disables the evaluation limits
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Why this matters:** بدون ترخيص صحيح، يعمل المحرك في وضع التقييم، مما قد يقتطع النتائج أو يضيف علامات مائية. ضبط الترخيص مبكرًا يضمن أيضًا أن أي خيارات ما قبل المعالجة اللاحقة تُطبق في وضع كامل الميزات.

## الخطوة 2: تهيئة محرك OCR

إنشاء نسخة من `OcrEngine` يمنحك الوصول إلى كل من خطوط التعرف وخطوط ما قبل المعالجة.

```java
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Pro tip:** احتفظ بالمحرك ككائن واحد (singleton) إذا كنت تخطط لمعالجة العديد من الصور على دفعة؛ فهو يخزن الموارد الداخلية ويُسرّع الاستدعاءات اللاحقة.

## الخطوة 3: ضبط ما قبل المعالجة – تصحيح الميل (Deskew)، إزالة الضوضاء (Denoise)، وتعزيز التباين

هنا حيث نقوم **preprocess image for OCR**. الثلاثة إعدادات التي سنضبطها هي:

1. **Deskew** – يصحح الدورانات الطفيفة.
2. **Denoise** – يزيل البقع التي تُربك تجزئة الأحرف.
3. **Contrast enhancement** – يجعل النص الداكن يبرز مقابل الخلفية.

```java
        // Access preprocessing settings
        PreprocessingSettings preprocessing = ocrEngine.getPreprocessing();

        // Enable automatic deskew (helps with scanned pages that are a few degrees off)
        preprocessing.setDeskew(true);
        preprocessing.setDeskewAngleTolerance(0.1); // tolerance in degrees

        // Turn on denoising – median works well for salt‑and‑pepper noise
        preprocessing.setDenoise(true);
        preprocessing.setDenoiseMode(DenoiseMode.MEDIAN); // alternatives: GAUSSIAN

        // Boost contrast – this is the “boost image contrast” step
        preprocessing.setContrastEnhance(true);
        preprocessing.setContrastLevel(1.3f); // 1.0 = no change, >1.0 = stronger contrast
```

### لماذا تعديل مستوى التباين؟

زيادة مستوى التباين يمدد هيستوجرام الصورة، مما يجعل البكسلات الداكنة أكثر ظلامًا والبكسلات الفاتحة أكثر إشراقًا. عمليًا، **contrast level** بقيمة `1.3f` غالبًا ما يعطي أفضل توازن للمستندات المطبوعة، بينما القيمة فوق `1.5f` قد تُفرط في إظهار الخطوط الرفيعة. لا تتردد في التجربة؛ الإعداد غير مكلف للتغيير ويمكنه تحسين معدل نجاح **recognize text from image** بشكل كبير.

## الخطوة 4: تحضير صورة الإدخال

فئة `OcrInput` تُجرد التعامل مع الملفات. يمكنك إضافة صور متعددة إذا كنت تحتاج إلى معالجة دفعة.

```java
        // Prepare the image for OCR – you can add more files to the same OcrInput
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.jpg");
```

**Edge case:** إذا كانت صورتك بتنسيق غير قياسي (مثلاً TIFF مع صفحات متعددة)، يمكنك تحميل كل صفحة على حدة أو تحويلها إلى PNG/JPEG أولاً.

## الخطوة 5: تنفيذ التعرف

الآن يقوم المحرك بتشغيل خط أنابيب ما قبل المعالجة الذي قمنا بضبطه، ثم يُسلم الصورة المنقاة إلى خوارزمية OCR الأساسية.

```java
        // Run OCR – this returns a result object containing the extracted text
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**What’s happening under the hood?** أولًا يطبق Aspose OCR تحويل الـ deskew، ثم يشغل مرشح الـ denoise، وأخيرًا يضبط التباين قبل تمرير الصورة إلى المُعرّف القائم على الشبكة العصبية. الترتيب مقصود؛ تغييره قد يؤدي إلى نتائج غير مثالية.

## الخطوة 6: إخراج النص المُعترف به

أخيرًا، نطبع السلسلة المستخرجة إلى وحدة التحكم. في تطبيق حقيقي قد تكتبها إلى ملف أو تُرسلها عبر الشبكة.

```java
        // Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

### النتيجة المتوقعة

إذا كانت `input.jpg` تحتوي على العبارة “Hello World!”، يجب أن تُظهر وحدة التحكم:

```
Hello World!
```

إذا كان الإخراج مشوشًا، تحقق مرة أخرى من قيم ما قبل المعالجة—خاصةً **contrast level** و **denoise mode**—وحاول تنسيق صورة مختلف.

## إضافي: تصور الصورة ما قبل المعالجة (اختياري)

أحيانًا تريد رؤية ما يراه المحرك بعد الـ deskew، والـ denoise، وتعزيز التباين. يتيح لك Aspose OCR تصدير الصورة المتوسطة (bitmap):

```java
        // Export the pre‑processed image for debugging
        BufferedImage processed = preprocessing.getProcessedImage();
        ImageIO.write(processed, "png", new File("processed.png"));
```

افتح `processed.png` جنبًا إلى جنب مع الأصل؛ ستلاحظ أفقًا أكثر استقامة ونصًا أكثر وضوحًا. هذه الخطوة مفيدة عندما تحاول استكشاف سبب فشل مسح معين.

![مثال على معالجة الصورة للتعرف الضوئي على الأحرف](/images/ocr-preprocess-example.png "معالجة الصورة للتعرف الضوئي على الأحرف – قبل وبعد تعزيز التباين")

*الصورة أعلاه توضح كيف أن تعزيز التباين وإزالة الضوضاء يحول مسحًا ضبابيًا إلى صورة نظيفة جاهزة للتعرف الضوئي على الأحرف.*

## الأخطاء الشائعة وكيفية تجنّبها

| المشكلة | سبب حدوثها | الحل |
|---------|----------------|-----|
| **Over‑contrasting** (`setContrastLevel` too high) | الخلفية الفاتحة تصبح بيضاء، مما يمحو الأحرف الخفيفة | حافظ على المستوى بين 1.1 و 1.4 لمعظم النصوص المطبوعة |
| **Deskew tolerance too low** | تبقى الدورانات الصغيرة غير مصححة | ارفع `setDeskewAngleTolerance` إلى 0.2 أو 0.3 للكتب الممسوحة |
| **Using GAUSSIAN denoise on binary images** | يطمس الحواف، مما يدمج الأحرف | استخدم `DenoiseMode.MEDIAN` للمسحات بالأبيض والأسود |
| **Missing license** | يعود المحرك إلى وضع التجربة، مما يقتطع المخرجات | تحقق من مسار `Aspose.OCR.lic` وأن الملف قابل للقراءة |

## الخطوات التالية: تجاوز المعالجة الأساسية

الآن بعد أن يمكنك **preprocess image for OCR** و **extract text using OCR**، فكر في هذه الإضافات:

- **Language packs** – حمّل قواميس لغات محددة لتحسين الدقة للنص غير الإنجليزي.
- **Region‑of‑interest (ROI) cropping** – ركّز على جزء من الصورة إذا كنت تحتاج فقط إلى جزء من الصفحة.
- **Batch processing** – كرّر عبر مجلد من الصور، مع إعادة استخدام نفس نسخة `OcrEngine` للسرعة.
- **Integrate with PDF** – اجمع Aspose OCR مع Aspose PDF لتحويل ملفات PDF الممسوحة إلى PDF قابل للبحث في خط أنابيب واحد.

كل من هذه المواضيع يدمج بطبيعية كلماتنا المفتاحية الثانوية: ستستمر في **boost image contrast**، **set contrast level**، وستستمر في **recognize text from image** عبر العديد من السيناريوهات.

## الخلاصة

لقد غطينا كل ما تحتاجه لـ **preprocess image for OCR** باستخدام Aspose OCR for Java: تحميل الترخيص، ضبط الـ deskew، والـ denoise، وتعزيز التباين، تمرير الصورة، وأخيرًا **recognize text from image**. مع المثال الكامل القابل للتنفيذ أعلاه، يمكنك الآن **extract text using OCR** على أي صورة مُعدّة بشكل مناسب.

جرّب الشفرة، عدّل **contrast level**، وشاهد الدقة ترتفع. عندما تكون جاهزًا، استكشف نماذج مخصصة للغات أو خطوط دفعات لتحويل هذا العرض التجريبي لصورة واحدة إلى حل جاهز للإنتاج.

*برمجة سعيدة، ولتكن مسحاتك دائمًا واضحة!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}