---
category: general
date: 2026-08-22
description: كيفية تمكين GPU في OCR باستخدام Java للتعرف على النص من الصورة بسرعة.
  تعلم استخراج النص من PNG، ضبط خيارات الصورة، والتعرف على النص بكفاءة باستخدام Aspose
  OCR.
draft: false
keywords:
- how to enable gpu
- recognize text image java
- aspose ocr java tutorial
- extract text from png
- set image options
lastmod: 2026-08-22
og_description: كيفية تمكين GPU في OCR باستخدام Java للتعرف على النص من الصورة بسرعة.
  يوضح هذا الدليل كيفية استخراج النص من PNG، ضبط خيارات الصورة، والتعرف على النص بكفاءة
  باستخدام Aspose OCR.
og_image_alt: Java OCR GPU example code snippet showing Aspose OCR usage
og_title: كيفية تمكين GPU لتقنية OCR في Java – استخراج النص بسرعة
schemas:
- author: Aspose
  dateModified: '2026-08-22'
  description: How to enable GPU in Java OCR to recognize text from image quickly.
    Learn to extract text from PNG, set image options, and recognize text efficiently
    using Aspose OCR.
  headline: How to Enable GPU for OCR in Java – Recognize Text from Image Fast
  type: TechArticle
- description: How to enable GPU in Java OCR to recognize text from image quickly.
    Learn to extract text from PNG, set image options, and recognize text efficiently
    using Aspose OCR.
  name: How to Enable GPU for OCR in Java – Recognize Text from Image Fast
  steps:
  - name: '**Low‑resolution scans (< 150 dpi).** Upscale first or ask the user for
      a higher‑resolution scan.'
    text: '**Low‑resolution scans (< 150 dpi).** Upscale first or ask the user for
      a higher‑resolution scan.'
  - name: '**Handwritten notes.** The default model focuses on printed text; you’d
      need a custom trained model for cursive.'
    text: '**Handwritten notes.** The default model focuses on printed text; you’d
      need a custom trained model for cursive.'
  - name: '**Multiple languages.** Pass a comma‑separated list to `RecognitionLanguage`,
      e.g., `RecognitionLanguage.ENGLISH_FRENCH`.'
    text: '**Multiple languages.** Pass a comma‑separated list to `RecognitionLanguage`,
      e.g., `RecognitionLanguage.ENGLISH_FRENCH`.'
  type: HowTo
- questions:
  - answer: Yes, the Aspose OCR trial includes full GPU support; you just need to
      enable it in code.
    question: Does the free trial support GPU acceleration?
  - answer: Aspose OCR can rasterize PDF pages internally, but for best performance
      convert to high‑resolution PNG first.
    question: Can I process PDFs directly without converting to images?
  - answer: CUDA 11.2 or newer is recommended; older versions may work but are not
      officially tested.
    question: What CUDA version is required?
  - answer: Validate file size and type before processing, and run the OCR in a sandboxed
      thread to mitigate risks.
    question: Is it safe to run OCR on untrusted user uploads?
  - answer: Set `ocrEngine.setDebugMode(true)`; the console will list the selected
      GPU device and memory statistics.
    question: How do I enable logging to verify GPU usage?
  type: FAQPage
tags:
- OCR
- Java
- GPU
title: كيفية تمكين GPU لتقنية OCR في Java – التعرف على النص من الصورة بسرعة
url: /ar/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين وحدة معالجة الرسومات (GPU) لتقنية OCR في جافا – التعرف على النص من الصورة بسرعة

## إجابات سريعة
- **ما هو أكبر تحسين في السرعة؟** حتى 5× أسرع على بطاقة RTX 2060 متوسطة مقارنةً بـ OCR على المعالج فقط.  
- **هل أحتاج إلى ترخيص خاص؟** ترخيص Aspose OCR القياسي يعمل مع GPU؛ فقط فعّل علامة GPU.  
- **ما نسخة جافا المطلوبة؟** يوصى بـ Java 17 أو أحدث للحصول على أداء مثالي.  
- **هل يمكن تشغيله داخل Docker؟** نعم – فقط أضف العلامة `--gpus all` وثبّت برامج تشغيل NVIDIA داخل الحاوية.  
- **هل الكود متوافق مع صيغ صور أخرى؟** نفس الـ API يعمل مع JPEG وTIFF وBMP وPNG دون أي تغييرات.

## ما ستحتاجه

تحتاج إلى جهاز يدعم وحدة معالجة الرسومات (GPU)، ومكتبة Aspose OCR لجافا، وبيئة تطوير Java 17 (أو أحدث). يتضمن الإعداد النموذجي بطاقة NVIDIA RTX 3060 أو أي بطاقة متوافقة مع CUDA، أحدث ملف JAR من Aspose OCR المتوفر في Maven Central، وعينة من فاتورة PNG للاختبار.

**الإجابة المباشرة (40‑70 كلمة):** لبَدْء العمل، يجب تثبيت Java 17، وإضافة تبعية Aspose OCR إلى مشروعك، والتحقق من أن JVM يمكنه رؤية جهاز CUDA واحد على الأقل، وتوفير صورة اختبار جاهزة. بمجرد استيفاء هذه المتطلبات، يمكنك تمكين GPU في محرك OCR والبدء في معالجة الصور بسرعة GPU.

- **Java 17** (أو أحدث) – الكود يُترجم مع الإصدارات السابقة لكن 17 يوفر أفضل دعم للـ API.  
- **Aspose OCR لجافا** – احصل على أحدث ملف JAR من موقع Aspose أو Maven Central.  
- **GPU متوافق مع CUDA** – مثل NVIDIA RTX 3060 أو RTX 2070 أو أي بطاقة حديثة مع برامج تشغيل مناسبة.  
- **صورة اختبار** – فاتورة PNG ذات حجم كبير مناسبة لقياس الأداء.

> **نصيحة احترافية:** على الحواسيب المحمولة التي تحتوي على رسومات مدمجة ومنفصلة، اجبر JVM على استخدام وحدة معالجة الرسومات المنفصلة عبر لوحة تحكم التعريف؛ وإلا سيعود المكتبة صامتًا إلى المعالج.

![مثال على تمكين GPU](image.png "مثال على تمكين GPU")
[مثال على تمكين GPU](image.png "مثال على تمكين GPU")

*نص بديل: مثال على تمكين GPU يُظهر مقتطف كود جافا.*

## الخطوة 1 – تثبيت Aspose OCR والتحقق من توفر GPU

GpuSettings هي فئة تتحكم في استخدام GPU لمحرك Aspose OCR.

أضف تبعية Maven (أو ضع ملف JAR في `libs/`):

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Check for the latest version -->
</dependency>
```

شغّل مقطع الفحص البسيط لعرض الأجهزة المتاحة:

```java
import com.aspose.ocr.GpuSettings;

public class GpuCheck {
    public static void main(String[] args) {
        GpuSettings settings = new GpuSettings();
        System.out.println("GPU enabled? " + settings.getEnable());
        System.out.println("Detected GPU count: " + settings.getDeviceCount());
    }
}
```

إذا أظهر الناتج عدد أجهزة غير صفرية، فإن JVM يرى الـ GPU. إذا أظهر صفرًا، فتحقق مرة أخرى من تثبيت التعريف وأن متغيّر البيئة `CUDA_PATH` مضبوط.

## الخطوة 2 – كيفية تمكين GPU في Aspose OCR

الإجابة المباشرة (40‑70 كلمة): قم بتمكين GPU بإنشاء كائن `GpuSettings`، وتعيين `setEnable(true)`، واختيارياً تحديد معرف الجهاز، وتمرير كائن الإعدادات هذا إلى مُنشئ `AsposeOCR`. بعد ذلك، ستُنفّذ جميع استدعاءات OCR على الـ GPU المحدد، مما يوفّر تحسينات السرعة الموضحة في قسم الأداء.

تتيح لك فئة `GpuSettings` تشغيل أو إيقاف استخدام GPU واختيار جهاز محدد عندما تكون هناك عدة وحدات معالجة رسومات.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.GpuSettings;
import com.aspose.ocr.ImageProcessingOptions;
import com.aspose.ocr.RecognitionLanguage;
import com.aspose.ocr.OcrResult;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // 2️⃣ Enable GPU processing (auto‑detects available device)
        GpuSettings gpuSettings = new GpuSettings();
        gpuSettings.setEnable(true);          // turn GPU on
        gpuSettings.setDeviceId(0);           // first GPU (change if you have multiple)
        ocrEngine.setGpuSettings(gpuSettings);

        // 3️⃣ Optimize image preprocessing for GPU performance
        ImageProcessingOptions imgOpts = new ImageProcessingOptions();
        imgOpts.setAutoDeskew(true);
        imgOpts.setBinarization(true);
        ocrEngine.setImageProcessingOptions(imgOpts);

        // 4️⃣ Recognize text from an image file (PNG in this case)
        OcrResult result = ocrEngine.recognizeImage(
                "YOUR_DIRECTORY/large_invoice.png",
                RecognitionLanguage.ENGLISH);

        // 5️⃣ Output the detected text
        System.out.println("Detected text:\n" + result.getText());
    }
}
```

### لماذا تمكين GPU؟

تسرّع وحدة معالجة الرسومات (GPU) الأعمال الثقيلة لتعدد المصفوفات التي تقوم بها نماذج OCR إلى آلاف الأنوية المتوازية. عمليًا، ستلاحظ **تحسينات سرعة 2‑5×** على بطاقة RTX 2060 متوسطة، وأكثر على البطاقات الأحدث. العيب هو استهلاك ذاكرة أعلى قليلًا، لكنه عادةً ليس مشكلة بالنسبة لملفات PNG بحجم الفواتير المعتادة.

## الخطوة 3 – التعرف على النص من صورة جافا – أفضل الممارسات

طريقة `recognizeImage` تعالج ملف الصورة المُعطى وتعيد النص المستخرج.

الإجابة المباشرة (40‑70 كلمة): استدعِ `ocrEngine.recognizeImage(filePath)` بعد تمكين GPU؛ الطريقة تكتشف تنسيق الملف تلقائيًا، وتشغّل نموذج OCR على الـ GPU، وتعيد النص المستخرج. للحصول على أفضل دقة، تأكد من أن الصورة مُثنّية (binary) ومُصححة الانحراف قبل الاستدعاء.

الكود أعلاه يقوم بذلك بالفعل، لكن إليك نسخة مبسطة تعزل استدعاء OCR:

```java
// Assuming ocrEngine is already configured with GPU
String imagePath = "sample.png";
OcrResult ocrResult = ocrEngine.recognizeImage(imagePath, RecognitionLanguage.ENGLISH);
String extractedText = ocrResult.getText();

System.out.println("Extracted text from PNG:");
System.out.println(extractedText);
```

**ما ستلاحظه:** طريقة `recognizeImage` تكتشف نوع الملف تلقائيًا، لذا يمكنك تقديم JPEG أو TIFF أو PNG دون علامات إضافية. لهذا السبب **استخراج النص من PNG** يعمل مباشرةً.

### معالجة الملفات الكبيرة

إذا كان ملف PNG أكبر من 5 ميغابايت، فكر في تصغير حجمه قبل OCR:

```java
imgOpts.setResizeFactor(0.5); // shrink to 50 % of original dimensions
ocrEngine.setImageProcessingOptions(imgOpts);
```

تقليل الدقة يقلل من استهلاك ذاكرة GPU وغالبًا ما يحسن الدقة لأن النموذج يرى حوافًا أنظف.

## الخطوة 4 – كيفية ضبط خيارات الصورة لتحسين الدقة

ImageOptions هو كائن تكوين يتيح لك ضبط خطوات ما قبل المعالجة مثل تصحيح الانحراف والتحويل إلى أبيض وأسود قبل OCR.

الإجابة المباشرة (40‑70 كلمة): استخدم كائن `ImageOptions` لتفعيل التصحيح التلقائي للانحراف (auto‑deskew)، والتحويل إلى أبيض وأسود، وإعادة التحجيم الاختيارية قبل تمرير الصورة إلى محرك OCR. القيم النموذجية هي `setAutoDeskew(true)`، `setBinarization(true)`، وعامل إعادة التحجيم بين 0.5 و 0.8 للمسحات الكبيرة. هذه الإعدادات تحسّن التباين والمحاذاة، مما يساعد الشبكة العصبية على التعرف على الأحرف بدقة أكبر، خاصةً في المستندات الضوضائية أو المائلة.

عبارة **كيفية ضبط الصورة** تظهر طبيعيًا عندما نتحدث عن ما قبل المعالجة. تقدم Aspose OCR مجموعة من الخيارات:

| الخيار                     | ما يفعله                                 | القيمة النموذجية |
|----------------------------|------------------------------------------|------------------|
| `setAutoDeskew(true)`      | يقوم بتصحيح خطوط النص المائلة            | true             |
| `setBinarization(true)`    | يحوّل إلى أبيض وأسود لزيادة التباين      | true             |
| `setResizeFactor(x)`       | يقوم بتكبير/تصغير الصورة (0 < x ≤ 1)     | 0.5‑0.8          |
| `setContrastAdjustment(y)` | يعزز التباين (0‑100)                     | 30               |

يمكنك دمجها بأي ترتيب؛ المكتبة تطبقها تسلسليًا قبل تمرير الصورة إلى الشبكة العصبية. التجربة هي المفتاح—فواتير مختلفة قد تحتاج إلى عتبات مختلفة.

## الخطوة 5 – كيفية التعرف على النص في الحالات الخاصة

فئة `GpuExample` توضح سير عمل OCR كامل من البداية إلى النهاية باستخدام Aspose OCR مع تسريع GPU.

الإجابة المباشرة (40‑70 كلمة): للمسحات منخفضة الدقة، قم أولاً بتكبير الصورة أو اطلب مصدرًا بدقة DPI أعلى؛ للملاحظات المكتوبة يدويًا، انتقل إلى نموذج مُدرب مخصص؛ وللمستندات متعددة اللغات، مرّر قائمة مفصولة بفواصل إلى `RecognitionLanguage`. تضمن هذه التعديلات أن محرك GPU لا يزال يقدم نتائج موثوقة.

1. **مسحات منخفضة الدقة (< 150 dpi).** قم بتكبيرها أولاً أو اطلب من المستخدم مسحًا بدقة أعلى.  
2. **ملاحظات مكتوبة يدويًا.** النموذج الافتراضي يركز على النص المطبوع؛ ستحتاج إلى نموذج مُدرب مخصص للخط اليدوي.  
3. **عدة لغات.** مرّر قائمة مفصولة بفواصل إلى `RecognitionLanguage`، مثال: `RecognitionLanguage.ENGLISH_FRENCH`.

```java
ocrEngine.recognizeImage("multilang.png",
        RecognitionLanguage.ENGLISH_FRENCH);
```

## النتيجة المتوقعة

تشغيل الفئة الكاملة `GpuExample` على `large_invoice.png` يجب أن يطبع شيئًا مشابهًا لـ:

```
Detected text:
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
...
```

إذا رأيت نصًا غير مفهوم، تحقق مرة أخرى من أن `gpuSettings.setEnable(true)` قد تم تفعيله فعلاً (ستظهر وحدة التحكم جهاز GPU إذا فعلت تسجيل الأخطاء).

## الأخطاء الشائعة والنصائح الاحترافية

- **نسيت تعيين معرف جهاز GPU.** في الأنظمة ذات عدة GPU، قد يكون `setDeviceId(1)` مطلوبًا.  
- **تشغيل داخل Docker بدون بيئة تشغيل NVIDIA.** أضف `--gpus all` إلى أمر `docker run`.  
- **خلط مسارات الكود للمعالج فقط وGPU.** حافظ على وجود نسخة واحدة من `AsposeOCR` لكل خيط لتجنب تعارض الحالة.  
- **تسرب الذاكرة.** استدعِ `ocrEngine.dispose()` عند الانتهاء، خاصةً في الخدمات التي تعمل لفترات طويلة.

## الأسئلة المتكررة

**س: هل يدعم الإصدار التجريبي المجاني تسريع GPU؟**  
ج: نعم، يتضمن الإصدار التجريبي من Aspose OCR دعمًا كاملاً لـ GPU؛ فقط تحتاج إلى تفعيله في الكود.

**س: هل يمكنني معالجة ملفات PDF مباشرةً دون تحويلها إلى صور؟**  
ج: يمكن لـ Aspose OCR تحويل صفحات PDF إلى صور داخليًا، لكن للحصول على أفضل أداء يُفضَّل تحويلها إلى PNG عالي الدقة أولاً.

**س: ما نسخة CUDA المطلوبة؟**  
ج: يُوصى بـ CUDA 11.2 أو أحدث؛ قد تعمل الإصدارات الأقدم لكنها غير مختبرة رسميًا.

**س: هل من الآمن تشغيل OCR على ملفات تم تحميلها من مستخدمين غير موثوقين؟**  
ج: تحقق من حجم ونوع الملف قبل المعالجة، وشغّل OCR في خيط معزول لتقليل المخاطر.

**س: كيف يمكنني تمكين التسجيل للتحقق من استخدام GPU؟**  
ج: اضبط `ocrEngine.setDebugMode(true)`؛ ستظهر وحدة التحكم جهاز GPU المختار وإحصائيات الذاكرة.

## الخلاصة

لقد استعرضنا **كيفية تمكين GPU** لـ Aspose OCR في جافا، وأظهرنا لك **كيفية التعرف على النص من الصورة**، وبيّنّا أبسط طريقة **لاستخراج النص من PNG**، وشرحنا **كيفية ضبط خيارات الصورة**، وتناولنا تفاصيل **كيفية التعرف على النص** في ملفات العالم الحقيقي. مع تشغيل GPU، يجب أن يصبح خط أنابيب OCR أسرع بشكل ملحوظ، مما يجعله مناسبًا للسيناريوهات ذات الإنتاجية العالية مثل معالجة الفواتير على دفعات أو مسح المستندات مباشرةً.

هل أنت مستعد للخطوة التالية؟ جرّب استبدال النموذج الإنجليزي الافتراضي بنموذج متعدد اللغات، أو جرب خطوط معالجة مسبقة مخصصة للإيصالات الضوضائية. السماء هي الحدّ—خاصةً عندما يكون لديك GPU يقوم بالعمل الشاق.

**آخر تحديث:** 2026-08-22  
**تم الاختبار مع:** Aspose OCR لجافا 24.10  
**المؤلف:** Aspose

## دروس ذات صلة

- [التعرف على نص الصورة باستخدام Aspose OCR كامل دليل Java OCR](/ocr/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [كيفية ضبط ترخيص Aspose OCR والتحقق منه في جافا](/ocr/java/ocr-basics/set-license/)
- [استخراج النص من صورة جافا باستخدام Aspose.OCR وضع كشف المناطق](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}