---
category: general
date: 2026-08-12
description: التعرف على النص من الصورة باستخدام محرك OCR بلغة Java. تعلّم كيفية استخراج
  النص من الصورة، تحسين دقة OCR، ومعالجة الصورة مسبقًا للـ OCR على ملفات PNG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- how to extract text from image
- how to improve OCR accuracy
- how to preprocess image for OCR
- perform OCR on PNG
language: ar
lastmod: 2026-08-12
og_description: التعرف على النص من الصورة باستخدام جافا. يوضح هذا الدرس كيفية استخراج
  النص من الصورة، تحسين دقة OCR، وإجراء OCR على ملفات PNG باستخدام المعالجة المتعددة
  الخيوط ووحدة معالجة الرسومات.
og_image_alt: Diagram showing Java OCR engine recognizing text from image
og_title: التعرف على النص من الصورة في جافا – دليل OCR خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: recognize text from image using Java OCR engine. Learn how to extract
    text from image, improve OCR accuracy, and preprocess image for OCR on PNG files.
  headline: recognize text from image in Java – complete OCR guide
  type: TechArticle
- description: recognize text from image using Java OCR engine. Learn how to extract
    text from image, improve OCR accuracy, and preprocess image for OCR on PNG files.
  name: recognize text from image in Java – complete OCR guide
  steps:
  - name: Explanation of each step
    text: '| Step | Why it matters | How it helps you **recognize text from image**
      | |------|----------------|-----------------------------------------------|
      | 1️⃣ Create the OCR engine | Instantiates the core component that drives all
      subsequent operations. | Provides the entry point for all OCR actions. | '
  - name: Expected output
    text: 'If `sample-image.png` contains the sentence “Hello, world! 123”, the console
      will display something similar to:'
  - name: 1. Binarization with Otsu’s method
    text: '```java import java.awt.image.BufferedImage; import com.example.image.Binarizer;
      // hypothetical helper class'
  - name: 2. Scaling to 300 dpi
    text: '```java import com.example.image.Resizer;'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: التعرف على النص من الصورة في جافا – دليل OCR الكامل
url: /ar/java/advanced-ocr-techniques/recognize-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من صورة في Java – دليل OCR كامل

إذا كنت بحاجة إلى **التعرف على النص من صورة** في تطبيق Java، فإن هذا الدرس يوضح لك بالضبط كيفية القيام بذلك. بنهاية الدليل ستتمكن من استخراج النص من ملفات الصور، تحسين دقة OCR، وتشغيل OCR على ملفات PNG مع دعم المعالجة المتعددة النوى وGPU.

العديد من المطورين يتساءلون **كيف يمكن استخراج النص من صورة** دون كتابة شبكة عصبية مخصصة. الحل هو استخدام محرك OCR مثبت، ضبطه للسرعة والدقة، وتطبيق خطوات ما قبل المعالجة المناسبة. الأقسام التالية تقودك خلال كل متطلب، بحيث يمكنك نسخ الكود مباشرةً إلى مشروعك.

## ما ستتعلمه

* إعداد محرك OCR في Java.
* تمكين المعالجة المتعددة الخيوط وتسريع GPU الاختياري.
* إضافة حزم اللغات للإنجليزية والإسبانية.
* تطبيق فلاتر ما قبل معالجة الصورة لتعزيز جودة التعرف.
* تفعيل مصحح الإملاء المدمج للحصول على مخرجات أنظف.
* إجراء OCR على ملفات PNG وطباعة النص المُتعرف عليه.

لا توجد خدمات خارجية مطلوبة—كل شيء يعمل محليًا، مما يجعله مثاليًا للتطبيقات غير المتصلة أو الحساسة للخصوصية.

## المتطلبات المسبقة

* Java 17 أو أحدث (الكود يستخدم بناء `var` الحديث لكن يمكن إرجاعه إلى إصدارات أقدم).
* مكتبة OCR توفر الفئات `OcrEngine`، `Language`، و`EngineOptions` (مثل **GroupDocs.Parser**، **Aspose.OCR**، أو أي SDK متوافق).
* Maven أو Gradle لإدارة التبعيات.
* صورة PNG تجريبية (`sample-image.png`) موجودة في `YOUR_DIRECTORY`.

> **نصيحة احترافية:** إذا كنت تخطط لمعالجة آلاف الصور، خصص ذاكرة RAM كافية لمخزن GPU وتعطيل مصحح الإملاء فقط عندما تحتاج إلى مخرجات OCR خام.

## التعرف على النص من صورة باستخدام محرك OCR في Java

فيما يلي برنامج Java كامل وقابل للتنفيذ يتبع الخطوات الثمانية الموضحة في المقتطف الأصلي. يتضمن الاستيرادات، طريقة `main`، وتعليقات داخلية تشرح هدف كل سطر.

```java
// File: OcrDemo.java
import com.example.ocr.OcrEngine;            // Replace with your OCR library's package
import com.example.ocr.Language;
import com.example.ocr.EngineOptions;
import com.example.ocr.ImagePreprocessingOptions;

public class OcrDemo {

    public static void main(String[] args) {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable multi‑core processing for faster throughput
        ocrEngine.getEngineOptions().setUseMultiThreading(true);

        // Step 3: (Optional) Turn on GPU acceleration if a compatible GPU is present
        ocrEngine.getEngineOptions().setUseGpu(true);

        // Step 4: Add the languages you want to recognize (English and Spanish)
        ocrEngine.getLanguage().add(Language.English);
        ocrEngine.getLanguage().add(Language.Spanish);

        // Step 5: Apply common image‑preprocessing filters to improve OCR accuracy
        ImagePreprocessingOptions imgOpts = ocrEngine.getImagePreprocessingOptions();
        imgOpts.setRotate(true);   // Auto‑rotate based on EXIF orientation
        imgOpts.setDeskew(true);   // Straighten skewed text lines
        imgOpts.setDenoise(true);  // Reduce background noise

        // Step 6: Enable the built‑in spell corrector for cleaner output
        ocrEngine.getEngineOptions().setUseSpellCorrector(true);

        // Step 7: Perform OCR on the target PNG image
        // This demonstrates how to perform OCR on PNG files efficiently.
        String imagePath = "YOUR_DIRECTORY/sample-image.png";
        String ocrResult = ocrEngine.recognizeImage(imagePath);

        // Step 8: Output the recognized text
        System.out.println("=== OCR Result ===");
        System.out.println(ocrResult);
    }
}
```

### شرح كل خطوة

| الخطوة | لماذا يهم | كيف يساعدك **التعرف على النص من صورة** |
|--------|-----------|----------------------------------------|
| 1️⃣ إنشاء محرك OCR | ينشئ المكوّن الأساسي الذي يدير جميع العمليات اللاحقة. | يوفر نقطة الدخول لجميع عمليات OCR. |
| 2️⃣ تمكين المعالجة المتعددة النوى | المعالجات الحديثة لديها نوى متعددة؛ الاستفادة منها يقلل من إجمالي زمن المعالجة. | يسرّع وظائف الدُفعات عندما **تجري OCR على ملفات PNG** بشكل متوازي. |
| 3️⃣ تفعيل تسريع GPU (اختياري) | تتفوق وحدات GPU في عمليات البكسل المتوازية، خاصةً للصور الكبيرة. | يمكن أن يقلل زمن التعرف حتى 70 % على الأجهزة المدعومة. |
| 4️⃣ إضافة حزم اللغات | تعتمد دقة OCR على نماذج اللغة؛ تحديد اللغات المطلوبة فقط يقلل الإيجابيات الزائفة. | يحسّن فرص التعرف الصحيح على الأحرف عندما **تستخرج النص من صورة** في سيناريوهات متعددة اللغات. |
| 5️⃣ معالجة ما قبل الصورة | التدوير، تصحيح الميل، وإزالة الضوضاء تصحّح مشاكل المسح الشائعة. | يُحسّن **دقة OCR** مباشرةً عبر تقديم صورة bitmap أنظف للمحرك. |
| 6️⃣ مصحح الإملاء | خطوة ما بعد المعالجة التي تُصحح الأخطاء الإملائية الشائعة في OCR. | يُنتج مخرجات أكثر قابلية للقراءة دون تنظيف يدوي. |
| 7️⃣ إجراء OCR على PNG | طريقة `recognizeImage` تقرأ الملف، تطبق المعالجة المسبقة، وتنفّذ خط أنابيب التعرف. | تُظهر **إجراء OCR على PNG** مع معالجة الخصائص الخاصة بالتنسيق (مثل الضغط غير الفاقد). |
| 8️⃣ طباعة النتيجة | توفر لك تغذية راجعة فورية للتحقق من النجاح. | تسمح لك بالتأكد من أن النص تم **التعرف عليه من الصورة** بشكل صحيح. |

### النتيجة المتوقعة

إذا كان `sample-image.png` يحتوي على الجملة “Hello, world! 123”، سيعرض الطرفية شيئًا مشابهًا لـ:

```
=== OCR Result ===
Hello, world! 123
```

قد يختلف الإخراج الدقيق قليلًا حسب جودة الصورة وإعدادات اللغة، لكن مصحح الإملاء عادةً ما يُصحح الأخطاء البسيطة مثل “Helli” → “Hello”.

## كيفية ما قبل معالجة الصورة لـ OCR – غوص أعمق

على الرغم من أن الكود أعلاه يستخدم المعالجة المدمجة للمحرك، يمكنك أيضًا تطبيق فلاتر مخصصة قبل تمرير الصورة إلى محرك OCR. إليك تقنيتين شائعتين:

### 1. التحويل إلى ثنائي باستخدام طريقة Otsu

```java
import java.awt.image.BufferedImage;
import com.example.image.Binarizer; // hypothetical helper class

BufferedImage original = ImageIO.read(new File(imagePath));
BufferedImage binary = Binarizer.otsuThreshold(original);
ocrEngine.recognizeImage(binary);
```

التحويل إلى ثنائي يحول الصورة إلى أبيض وأسود، وهو غالبًا ما **يحسن دقة OCR** للماسحات ذات التباين المنخفض.

### 2. التحجيم إلى 300 dpi

```java
import com.example.image.Resizer;

BufferedImage scaled = Resizer.scaleToDPI(original, 300);
ocrEngine.recognizeImage(scaled);
```

معظم محركات OCR تتوقع على الأقل 300 dpi للحصول على أفضل التعرف على الأحرف. التحجيم يمنع المحرك من قراءة الرموز الصغيرة بشكل خاطئ.

> **ملاحظة:** إذا فعّلت كلًا من المعالجة المسبقة المخصصة وخيارات المحرك المدمجة، سيطبق المحرك فلاتره *بعد* فلاترك. اختر الترتيب الذي يناسب خصائص صورتك الأفضل.

## كيفية استخراج النص من صورة – التعامل مع الحالات الطرفية

| الحالة | التعديل الموصى به |
|--------|-------------------|
| **خلفية صاخبة جدًا** | زيادة شدة `setDenoise(true)` أو تشغيل مرشح متوسط قبل OCR. |
| **ميل > 15°** | استخدم `setDeskew(true)` *وأضف* زاوية تدوير يدوية عبر `imgOpts.setRotateAngle(θ)`. |
| **لغات مختلطة (مثل الإنجليزية + الإسبانية)** | أضف كلتا حزمتي اللغة كما هو موضح في الخطوة 4؛ سيقوم المحرك بتبديل السياق تلقائيًا. |
| **ملفات PDF كبيرة تم تحويلها إلى PNG** | عالج كل صفحة كملف PNG منفصل وجمع النتائج؛ المعالجة المتعددة الخيوط (الخطوة 2) ستحافظ على انخفاض الوقت الإجمالي. |
| **GPU غير متوفر** | احتفظ بـ `setUseGpu(true)` لكن ضعها داخل try‑catch؛ سيعود المحرك إلى CPU دون تعطل. |

## إجراء OCR على PNG – مثال على المعالجة الدُفعية

عندما تحتاج إلى **إجراء OCR على PNG** عبر دليل كامل، حلقة بسيطة باستخدام نفس نسخة المحرك تعمل بشكل جيد:

```java
Path dir = Paths.get("YOUR_DIRECTORY");
try (Stream<Path> files = Files.list(dir)) {
    files.filter(p -> p.toString().endsWith(".png"))
         .forEach(p -> {
             String text = ocrEngine.recognizeImage(p.toString());
             System.out.println("File: " + p.getFileName());
             System.out.println(text);
             System.out.println("---");
         });
}
```

نظرًا لأن المحرك مُعد مسبقًا للمعالجة المتعددة النوى وGPU، يمكن لهذه الحلقة معالجة العشرات من الصور بشكل متوازي دون كتابة كود إضافي.

## مثال عملي كامل

بدمج كل ما سبق، إليك فئة مستقلة يمكنك نسخها ولصقها في بيئة التطوير IDE، إضافة تبعية Maven المناسبة، وتشغيلها فورًا:



## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية إجراء OCR لنص الصورة مع اللغة باستخدام Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [استخراج النص من صورة Java باستخدام وضع اكتشاف المناطق في Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [صورة إلى نص Java: تحويل الصورة إلى نص باستخدام Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}