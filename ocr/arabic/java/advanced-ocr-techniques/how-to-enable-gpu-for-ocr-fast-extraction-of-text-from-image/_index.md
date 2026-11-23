---
category: general
date: 2026-10-19
description: كيفية استخراج النص من صورة بسرعة باستخدام تسريع GPU عبر Aspose OCR في
  Java. تعلم كيفية تمكين GPU، التعرف على النص من PNG، قراءة النص من صورة، وتحويل الصورة
  إلى نص.
draft: false
keywords:
- extract text from image
- recognize text from png
- read text from photo
- convert image to text
lastmod: 2026-10-19
og_description: تعلم كيفية استخراج النص من صورة باستخدام Aspose OCR المدعوم بتقنية
  GPU في Java. تمكين GPU، التعرف على النص من PNG، قراءة النص من صورة، وتحويل الصورة
  إلى نص بكفاءة.
og_image_alt: Diagram showing GPU‑accelerated OCR flow from image loading to text
  extraction
og_title: استخراج النص من صورة باستخدام Aspose OCR المدعوم بتقنية GPU (Java)
schemas:
- author: Aspose
  dateModified: '2026-10-19'
  description: How to extract text from image quickly with GPU acceleration using
    Aspose OCR in Java. Learn to enable GPU, recognize text from PNG, read text from
    photo, and convert image to text.
  headline: How to extract text from image with GPU‑accelerated Aspose OCR
  type: TechArticle
- description: How to extract text from image quickly with GPU acceleration using
    Aspose OCR in Java. Learn to enable GPU, recognize text from PNG, read text from
    photo, and convert image to text.
  name: How to extract text from image with GPU‑accelerated Aspose OCR
  steps:
  - name: initialize the OCR engine – **how to enable GPU**
    text: '`OcrEngine` is the central class that holds all OCR settings, including
      the GPU flag. > **Why this matters:** Without an `OcrEngine` you have no context
      for the image or the hardware options. Instantiating it early also allows you
      to tweak options before loading the file.'
  - name: load the image you want to process – **extract text from image**
    text: '`ImageStream.fromFile` reads any supported format; PNG is preferred because
      it retains lossless detail. > **Edge case:** If your image lives in a different
      folder, adjust the path accordingly. For large batches, loop over a directory
      and call `setImage` for each file.'
  - name: turn on GPU acceleration – **how to enable GPU**
    text: Calling `setUseGpu(true)` instructs the native library to off‑load the heavy
      lifting to the graphics card. If no compatible GPU is found, Aspose silently
      falls back to CPU, so your application never crashes. > **What if I don’t have
      a GPU?** The call is ignored and OCR runs on the CPU. You can verif
  - name: perform the OCR – **recognize text from PNG**
    text: Invoke `recognize()` to start the analysis. The method returns an `OcrResult`
      object containing raw text, confidence scores, and optional bounding‑box data.
      > **Why wait until now?** The OCR process is computationally intensive; doing
      it after all settings are applied ensures maximum efficiency, esp
  - name: output the detected string – **read text from photo**
    text: 'Print the result to the console. In production you might store it in a
      database or send it over a network, but `System.out.println` keeps the example
      minimal. > **Expected output:** If `sample-photo.png` contains the words “Hello
      World”, the console will display: That’s the whole program—no external'
  type: HowTo
- questions:
  - answer: Yes, Aspose OCR will automatically fall back to CPU if no CUDA‑compatible
      GPU is detected.
    question: Can I use GPU acceleration on any machine?
  - answer: Java 17 or newer is recommended for best performance and long‑term support.
    question: What Java version is required?
  - answer: A free trial works for evaluation; a commercial license is required for
      production use.
    question: Do I need a license for development?
  - answer: Tests show up to 5× speed‑up on an NVIDIA RTX 3080 versus CPU‑only processing.
    question: How much faster is GPU OCR?
  - answer: The Java API runs on Windows, Linux, and macOS; GPU acceleration works
      on any system with an NVIDIA CUDA driver.
    question: Is the code cross‑platform?
  type: FAQPage
tags:
- OCR
- Java
- GPU-Acceleration
title: كيفية استخراج النص من صورة باستخدام Aspose OCR المدعوم بتقنية GPU
url: /ar/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-fast-extraction-of-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخراج النص باستخدام Aspose OCR المدعوم بتسريع GPU

هل تساءلت يومًا **how to enable GPU** لـ OCR والحصول على نتائج فورية من صورة؟ لست وحدك. في العديد من مشاريع الرؤية الحاسوبية تكون خطوة OCR هي العنق الزجاجي، خاصةً عندما تتعامل مع ملفات PNG عالية الدقة. الخبر السار هو أن Aspose OCR يتيح لك تشغيل تسريع GPU بسطر واحد من الشيفرة، مما يمكنه تقليل وقت المعالجة بشكل كبير. في هذا الدليل ستتعلم **extract text from image**، **recognize text from PNG**، **read text from photo**، وفي النهاية **convert image to text** باستخدام مكتبة Aspose OCR.

## إجابات سريعة
- **Can I use GPU acceleration on any machine?** نعم، سيعود Aspose OCR تلقائيًا إلى المعالج إذا لم يتم اكتشاف GPU متوافق مع CUDA.  
- **What Java version is required?** يُنصح باستخدام Java 17 أو أحدث للحصول على أفضل أداء ودعم طويل الأمد.  
- **Do I need a license for development?** النسخة التجريبية المجانية تكفي للتقييم؛ يلزم الحصول على رخصة تجارية للاستخدام في الإنتاج.  
- **How much faster is GPU OCR?** تُظهر الاختبارات تسريعًا يصل إلى 5× على NVIDIA RTX 3080 مقارنةً بالمعالجة على المعالج فقط.  
- **Is the code cross‑platform?** يعمل Java API على Windows وLinux وmacOS؛ يعمل تسريع GPU على أي نظام يحتوي على برنامج تشغيل NVIDIA CUDA.

## ما هو extract text from image؟
يشير استخراج النص من صورة إلى عملية تحويل الأحرف البصرية التي تظهر في صورة نقطية — مثل PNG أو JPEG أو TIFF — إلى سلاسل قابلة للبحث والتحرير باستخدام تقنية التعرف الضوئي على الأحرف (OCR). يقوم محرك OCR بتحليل أنماط البكسل، وتحديد الحروف والأرقام، وإخراج نص عادي يمكن فهرسته أو تحريره.

## لماذا استخدام OCR المدعوم بتسريع GPU؟
يدعم Aspose OCR **أكثر من 50 تنسيقًا للإدخال والإخراج** ويمكنه معالجة مستندات مئات الصفحات دون تحميل الملف بالكامل في الذاكرة. عندما يتم تمكين تسريع GPU، يمكن لنفس عبء عمل OCR الذي يستغرق حوالي 2 ثانية على المعالج أن يكتمل في أقل من 0.4 ثانية على RTX 3080 الحديثة، مما يوفر زيادة ملحوظة في الإنتاجية لخطوط معالجة الدُفعات.

## المتطلبات المسبقة

| المتطلب | لماذا يهم |
|-------------|----------------|
| Java 17 أو أحدث | يوفر دعمًا طويل الأمد وتحسينات في الأداء مقارنةً ببيئات التشغيل القديمة. |
| أداة بناء Maven أو Gradle | تجلب تبعية `aspose-ocr` تلقائيًا وتحافظ على تحديثها. |
| GPU متوافق مع CUDA (اختياري) | يتيح استدعاء `setUseGpu(true)` لتفريغ تحليل الصورة الثقيل إلى بطاقة الرسوميات. |
| ملف صورة (`sample-photo.png`) في مجلد معروف | يعمل كمصدر لمحرك OCR للقراءة والتحويل. |

إذا كان أي من هذه العناصر مفقودًا، لا يزال بإمكانك تشغيل المثال؛ ستعود المكتبة ببساطة إلى المعالجة باستخدام المعالج.

## إعداد المشروع

### 1️⃣ إضافة Aspose OCR إلى بناء المشروع

لـ Maven، أضف هذا المقتطف إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest stable version -->
</dependency>
```

لـ Gradle، ضع ما يلي في `build.gradle`:

```gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

> **نصيحة احترافية:** راقب مستودع Aspose Maven؛ يطلقون تصحيحات أداء بانتظام.

### 2️⃣ تخطيط الدليل

أنشئ مجلدًا باسم `resources` في جذر مشروعك وضع فيه `sample-photo.png`. سيشير الكود إليه باستخدام مسار نسبي، لذلك لن تحتاج إلى كتابة مسارات مطلقة.

## كيفية تمكين GPU لـ OCR؟

حمّل محرك OCR، فعل GPU، وشغّل التعرف في ثلاث خطوات مختصرة. يوضح هذا الجواب المباشر ما عليك القيام به بالضبط: إنشاء كائن `OcrEngine`, تمكين GPU باستخدام `setUseGpu(true)`, ثم استدعاء `recognize()` على الصورة المحملة. يكتمل العملية بأكملها في سلسلة طريقة واحدة، مما يمنحك أقصى سرعة بأقل شيفرة.

### الخطوة 1: تهيئة محرك OCR – **how to enable GPU**

`OcrEngine` هو الفئة المركزية التي تحتفظ بجميع إعدادات OCR، بما في ذلك علامة GPU.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **لماذا هذا مهم:** بدون `OcrEngine` لا يوجد لديك سياق للصورة أو خيارات الأجهزة. إن إنشاءه مبكرًا يتيح لك تعديل الخيارات قبل تحميل الملف.

### الخطوة 2: تحميل الصورة التي تريد معالجتها – **extract text from image**

`ImageStream.fromFile` يقرأ أي تنسيق مدعوم؛ يُفضَّل PNG لأنه يحتفظ بالتفاصيل بدون فقدان.

```java
        // Step 2: Load the image to be recognized
        ocrEngine.setImage(ImageStream.fromFile("resources/sample-photo.png"));
```

> **حالة حافة:** إذا كانت صورتك موجودة في مجلد مختلف، عدل المسار وفقًا لذلك. للدفعات الكبيرة، قم بالتكرار عبر دليل واستدعِ `setImage` لكل ملف.

### الخطوة 3: تشغيل تسريع GPU – **how to enable GPU**

استدعاء `setUseGpu(true)` يوجه المكتبة الأصلية لتفريغ الأعمال الثقيلة إلى بطاقة الرسوميات. إذا لم يتم العثور على GPU متوافق، سيعود Aspose صامتًا إلى المعالج، لذا لن يتعطل تطبيقك.

```java
        // Step 3: Enable GPU acceleration (optional – ignored if no GPU is available)
        ocrEngine.getEngineOptions().setUseGpu(true);
```

> **ماذا لو لم يكن لدي GPU؟** يتم تجاهل الاستدعاء ويعمل OCR على المعالج. يمكنك التحقق من الوضع لاحقًا باستخدام `ocrEngine.getEngineOptions().isUseGpu()`.

### الخطوة 4: تنفيذ OCR – **recognize text from PNG**

استدعِ `recognize()` لبدء التحليل. تُعيد الطريقة كائن `OcrResult` يحتوي على النص الأصلي، درجات الثقة، وبيانات إطارات اختيارية.

```java
        // Step 4: Perform the OCR recognition
        OcrResult ocrResult = ocrEngine.recognize();
```

> **لماذا الانتظار حتى الآن؟** عملية OCR مكثفة حسابيًا؛ تنفيذها بعد تطبيق جميع الإعدادات يضمن أقصى كفاءة، خاصةً عندما يكون GPU نشطًا.

### الخطوة 5: إخراج السلسلة المكتشفة – **read text from photo**

اطبع النتيجة إلى وحدة التحكم. في الإنتاج قد تخزنها في قاعدة بيانات أو ترسلها عبر الشبكة، لكن `System.out.println` يبقي المثال بسيطًا.

```java
        // Step 5: Output the recognized text
        System.out.println("Detected text:");
        System.out.println(ocrResult.getText());

        // Optional: Verify GPU usage
        System.out.println("GPU used: " + ocrEngine.getEngineOptions().isUseGpu());
    }
}
```

> **الناتج المتوقع:** إذا كان `sample-photo.png` يحتوي على الكلمات “Hello World”، سيعرض وحدة التحكم:

```
Detected text:
Hello World
GPU used: true
```

هذا هو البرنامج بالكامل — لا خدمات خارجية، ولا ملفات إعداد مخفية.

## نظرة بصرية

![كيفية تمكين gpu لـ OCR](gpu-ocr-diagram.png "مخطط يوضح التدفق من تحميل الصورة إلى OCR المدعوم بتسريع GPU")

[كيفية تمكين gpu لـ OCR](gpu-ocr-diagram.png "مخطط يوضح التدفق من تحميل الصورة إلى OCR المدعوم بتسريع GPU")

*المخطط يوضح كل خطوة من خط الأنابيب، مع إبراز مكان علم **how to enable GPU**.*

## أسئلة شائعة وحالات حافة

| السؤال | الإجابة |
|----------|--------|
| **Can I process multiple images in one run?** | نعم. غلف الخطوات 2‑5 في حلقة `for (File img : folder.listFiles())` واستدعِ `ocrEngine.setImage` لكل ملف. |
| **What image formats are supported?** | JPEG, PNG, BMP, TIFF، وGIF كلها مدعومة أصلاً من قبل Aspose OCR. |
| **How do I handle low‑quality scans?** | اضبط `ocrEngine.getEngineOptions().setPreprocessMode(PreprocessMode.Auto)` قبل التعرف لتسمح للمحرك بتنظيف الضوضاء تلقائيًا. |
| **Is there a way to get confidence scores?** | `ocrResult.getMeanConfidence()` يُعيد متوسط الثقة (0‑100). تتوفر ثقة كل حرف عبر `ocrResult.getTextLines()`. |
| **Will this work on macOS with Metal GPU?** | حاليًا يستخدم Aspose OCR CUDA على بطاقات NVIDIA فقط. على macOS ستعود إلى المعالج ما لم تستخدم eGPU من NVIDIA. |

## نصائح الأداء

1. **Batch processing:** حمّل جميع الصور في الذاكرة أولاً، فعل GPU مرة واحدة، ثم نفّذ الحلقة. هذا يقلل من عبء برنامج التشغيل.  
2. **Image resizing:** قلل حجم PNGs الكبيرة جدًا إلى حد أقصى 2000 px على الجانب الأطول؛ تظل دقة OCR عالية بينما ينخفض استهلاك ذاكرة GPU.  
3. **Warm‑up call:** شغّل `recognize()` تجريبيًا على صورة صغيرة قبل عبء العمل الحقيقي لتسمح لبرنامج تشغيل GPU بالتهيئة — يمكن أن يوفر ذلك بضع مللي ثانية من الصورة الأولى الحقيقية.

## ملخص وخطوات قادمة

لقد غطينا **how to enable GPU** لـ Aspose OCR، وأظهرنا لك كيفية **extract text from image** للملفات، وشرحنا **recognize text from PNG**، وتناولنا سير عمل **read text from photo** و**convert image to text**. المقتطف الكامل للـ Java أعلاه جاهز للنسخ واللصق، ويجب أن تساعد ملاحظات الأداء في استخراج كل مللي ثانية من عتادك.

ما الخطوة التالية؟ فكر في توسيع الحل إلى:

* **Export OCR results to JSON** للتحليلات اللاحقة.  
* **Integrate with a Spring Boot REST endpoint** حتى تتمكن الخدمات الأخرى من إرسال صور وتلقي ردود نصية صافية.  
* **Apply language‑specific dictionaries** عبر `ocrEngine.getEngineOptions().setLanguage(Language.English)` لتحسين الدقة في المستندات متعددة اللغات.

لا تتردد في التجربة — استبدل PNG بملف PDF ممسوح، فعّل `setPreserveFormatting(true)`, أو ربط عدة تمريرات OCR للصور المشوشة. السماء هي الحد عندما تتقن **how to enable GPU** لـ OCR.

---

**آخر تحديث:** 2026-10-19  
**تم الاختبار مع:** Aspose OCR 24.11 for Java  
**المؤلف:** Aspose

## دروس ذات صلة

- [كيفية تمكين GPU لـ OCR في Java استخراج النص من صورة](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)
- [التعرف على نص الصورة باستخدام Aspose OCR GPU Java](/ocr/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/)
- [معالجة دفعة من صور OCR في Java استخراج النص من ملفات PNG بسرعة](/ocr/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}