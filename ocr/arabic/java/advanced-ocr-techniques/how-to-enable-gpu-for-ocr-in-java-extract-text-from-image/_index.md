---
category: general
date: 2026-10-19
description: تعلم كيفية تمكين GPU في كود Aspose OCR Java لاستخراج النص من الصورة.
  حوّل الصورة إلى نص وتعرّف على النص من الصورة بكفاءة.
draft: false
keywords:
- how to enable gpu
- extract text from image
- convert photo to text
- how to extract text
- recognize text from photo
lastmod: 2026-10-19
og_description: تمكين GPU لتقنية OCR في Java يتيح لك استخراج النص من الصورة بسرعة،
  مما يقلل وقت المعالجة حتى 90٪ على وحدات GPU الحديثة. تعلّم إعداد الخطوة بخطوة، مقتطفات
  الكود، ونصائح استكشاف الأخطاء وإصلاحها.
og_image_alt: Diagram illustrating how to enable GPU in Aspose OCR Java code – how
  to enable gpu
og_title: كيفية تمكين GPU لتقنية OCR في Java – استخراج نص سريع
schemas:
- author: Aspose
  dateModified: '2026-10-19'
  description: Learn how to enable GPU in Aspose OCR Java code to extract text from
    image. Convert photo to text and recognize text from photo efficiently.
  headline: How to Enable GPU for OCR in Java – Extract Text from Image
  type: TechArticle
- questions:
  - answer: Yes, as long as you have a Metal‑compatible GPU and the appropriate Aspose
      OCR binary for macOS. The same `setUseGpu(true)` call applies.
    question: Does this work on macOS?
  - answer: The Community Edition includes CPU‑only inference. To unlock GPU you need
      a licensed version (or a trial that includes GPU support).
    question: Can I use the free Community Edition?
  - answer: Call `ocrEngine.getConfig().setLanguage("spa")` for Spanish, `"fra"` for
      French, etc. Language packs are bundled with the library.
    question: What if I need to **recognize text from photo** in a language other
      than English?
  - answer: Yes—`ocrResult.getWords()` returns a collection where each `Word` object
      has a `getConfidence()` method.
    question: Is there a way to get confidence scores for each word?
  - answer: After creating the engine, invoke `ocrEngine.getConfig().setRequireGpu(true)`.
      The library will throw an exception if no compatible GPU is found, preventing
      silent CPU fallback.
    question: How can I enforce a strict GPU‑only mode?
  type: FAQPage
tags:
- OCR
- Java
- GPU
- Aspose
title: كيفية تمكين GPU لتقنية OCR في Java – استخراج النص من الصورة
url: /ar/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين GPU للتعرف الضوئي على الأحرف (OCR) في Java – استخراج النص من الصورة

هل تساءلت يومًا **كيفية تمكين GPU** عند تشغيل OCR على صورة عالية الدقة؟ لست وحدك. يواجه العديد من مطوري Java عائقًا عندما يصبح خط أنابيب OCR بطيئًا على إعداد يعتمد على CPU فقط، خاصةً عندما يتضخم حجم الصورة إلى أكثر من بضعة ميغابكسل. الخبر السار؟ تمكين تسريع GPU مع Aspose OCR سهل للغاية، ويسمح لك **باستخراج النص من الصورة** في جزء من الوقت.

في هذا البرنامج التعليمي سنستعرض العملية بالكامل: من إعداد مكتبة Aspose OCR، وتفعيل علم GPU، وإمداده بصورة كبيرة، وأخيرًا **تحويل الصورة إلى نص**. في النهاية ستعرف **كيفية تمكين GPU** بشكل موثوق، وسترى أيضًا كيف **تتعرف على النص من الصورة** على الأجهزة التي تحتوي على عدة وحدات معالجة رسومات. لا حاجة لمراجع خارجية—كل ما تحتاجه موجود هنا.

## إجابات سريعة
- **ماذا يفعل “enable GPU”?** يقوم بتحميل استدلال شبكة OCR العصبية إلى بطاقة الرسومات، مما يقلل وقت المعالجة حتى 90 % على الأجهزة الحديثة.  
- **هل أحتاج إلى ترخيص خاص؟** نعم، دعم GPU متاح فقط في نسخة Aspose OCR for Java المرخصة (أو نسخة تجريبية تشمل نوى GPU).  
- **ما هي وحدات GPU المدعومة؟** وحدات NVIDIA GPU مع CUDA 12.x (قابلية حساب 3.5+) ووحدات AMD GPU مع ROCm 5.x (قابلية حساب 6.0+).  
- **هل يمكنني الرجوع إلى CPU تلقائيًا؟** المكتبة تكتشف وحدات GPU المفقودة أو غير المتوافقة وتتحول إلى CPU بشكل شفاف، لكن يمكنك فرض وضع GPU‑only صارم.  
- **هل الكود متوافق مع Java 17؟** بالتأكيد—Aspose OCR 23.x يستهدف Java 11+ ويعمل بلا مشاكل مع Java 17.

## ما هو تسريع GPU للتعرف الضوئي على الأحرف (OCR)؟
تسريع GPU للتعرف الضوئي على الأحرف (OCR) هو عملية استخدام معالج الرسومات لتشغيل نماذج التعلم العميق التي تتعرف على الأحرف، بدلاً من CPU. هذا يسرّع استخراج النص بشكل كبير، خاصةً للصور الكبيرة أو المعالجة على دفعات. بنقل الطبقات الالتفافية الثقيلة إلى GPU، ينخفض زمن الاستجابة وتزداد القدرة الإنتاجية، مما يجعل المعالجة في الوقت الفعلي ممكنة للصور عالية الدقة.

## لماذا نستخدم وضع GPU في Aspose OCR؟
يدعم Aspose OCR **أكثر من 50 تنسيق إدخال** (JPEG، PNG، BMP، TIFF، PDF، إلخ) ويمكنه معالجة صورة بدقة 20 MP في أقل من ثانية واحدة على RTX 3080، مقارنةً بـ 8 ثوانٍ على CPU عالي الأداء. توفر المكتبة أيضًا fallback مدمج، وحزم لغات لأكثر من 30 لغة، وواجهة برمجة تطبيقات Java بسيطة تتطلب علمًا واحدًا فقط لتمكين GPU.

## المتطلبات المسبقة
- Java 17 أو أحدث مثبت.  
- وحدة GPU مدعومة من NVIDIA أو AMD مع برامج تشغيل محدثة (CUDA 12.x لـ NVIDIA، ROCm 5.x لـ AMD).  
- ملفات JAR الخاصة بـ Aspose OCR for Java – حمّل أحدث إصدار 23.x من موقع Aspose.  
- Maven أو Gradle لإدارة التبعيات (سنظهر مثال Maven).  
- صورة عالية الدقة (مثال: `high-res-photo.jpg`) تريد معالجتها.

إذا كان أي من هذه مفقودًا، سيظل الكود يُترجم، لكن علم GPU سيتجاهل وسيتم الرجوع إلى معالجة CPU.

## كيفية تمكين GPU للتعرف الضوئي على الأحرف (OCR) في Java؟
حمّل محرك OCR، استدعِ `setUseGpu(true)`، وشغّل صورتك عبر طريقة `recognize`. هذا السطر الواحد يُفعّل نوى GPU التي تشغّل الشبكة العصبية الالتفافية. **`setUseGpu(true)` يتيح معالجة GPU لمحرك OCR.** محرك OCR هو مثال من `com.aspose.ocr.OcrEngine` الذي يقوم بالتعرف على النص.

## الخطوة 1 – إضافة Aspose OCR إلى بناء المشروع (كيفية تمكين GPU)
أولًا: أخبر مشروعك بمكان العثور على مكتبة OCR. في Maven، أضف التبعية التالية إلى ملف `pom.xml`:

```xml
<!-- Step 1: Include Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

> **نصيحة احترافية:** إذا كنت تستخدم Gradle، المكافئ هو `implementation 'com.aspose:aspose-ocr:23.10'`. الحفاظ على تحديث المكتبة يضمن حصولك على أحدث نوى GPU وإصلاحات الأخطاء.

الآن بعد أن أصبحت المكتبة في مسار الفئات، يمكننا فعليًا **تمكين GPU** في محرك OCR.

## الخطوة 2 – إنشاء محرك OCR وتفعيل GPU (كيفية تمكين GPU)

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Instantiate the OCR engine – this is the core object.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Enable GPU acceleration.
        // This is the line that answers the question "how to enable gpu".
        ocrEngine.getConfig().setUseGpu(true);

        // Optional: If your system has more than one GPU, pick the one you want.
        // The device ID is zero‑based, so 0 refers to the first GPU.
        // ocrEngine.getConfig().setGpuDeviceId(0);

        // Step 2.3: Process the image and get the result.
        OcrResult ocrResult = ocrEngine.processImage("YOUR_DIRECTORY/high-res-photo.jpg");

        // Step 2.4: Print the recognized text – now you have converted photo to text.
        System.out.println(ocrResult.getText());
    }
}
```

> **لماذا هذا مهم:** ضبط `setUseGpu(true)` يخبر المكتبة الأصلية بتحميل عمل الشبكة العصبية الالتفافية الثقيلة إلى GPU. على RTX 3080 الحديثة، يمكن معالجة نفس الصورة التي تستغرق 8 ثوانٍ على CPU في أقل من ثانية واحدة. إذا تخطيت هذه الخطوة، ستظل **تتعرف على النص من الصورة**، لكنك لن تحصل على تحسينات الأداء.

## الخطوة 3 – التحقق من أن GPU يُستخدم فعليًا
قد تتساءل، “هل GPU فعلاً يقوم بالعمل؟” أسهل طريقة للتحقق هي النظر إلى مخرجات وحدة التحكم لمكتبة Aspose OCR عند تمكين تسجيل التصحيح:

```java
// Enable verbose logging – helpful for confirming GPU usage.
ocrEngine.getConfig().setLogLevel(com.aspose.ocr.Config.LogLevel.DEBUG);
```

عند تشغيل البرنامج، ستظهر لك أسطر مثل:

```
[DEBUG] Using GPU device 0 (NVIDIA GeForce RTX 3080) for OCR processing.
```

إذا لم تشاهد تلك الرسالة، تحقق مرة أخرى من تثبيت برنامج التشغيل وتأكد من أن GPU يفي بالحد الأدنى لقدرة الحوسبة (3.5 لـ NVIDIA، 6.0 لـ AMD).

## الخطوة 4 – التعامل مع عدة وحدات GPU وحالات الحافة
### اختيار GPU مختلف
إذا كان جهازك يحتوي على أكثر من GPU (مثلاً، GPU مدمج من Intel وبطاقة NVIDIA مخصصة)، يمكنك استهداف الأسرع:

```java
ocrEngine.getConfig().setGpuDeviceId(1); // 1 = second GPU in the system
```

### ماذا لو لم يتم اكتشاف أي GPU؟
يتحول Aspose OCR بسلاسة إلى CPU عندما لا يستطيع العثور على GPU مناسب. لتجنب الانتقال الصامت إلى CPU، يمكنك إضافة قيد. **`setRequireGpu(true)` يجبر المكتبة على استخدام GPU ويرمي استثناءً إذا لم يُعثر على أي واحد.** هذا يضمن أنك على علم عندما يكون GPU غير متاح.

```java
if (!ocrEngine.getConfig().isGpuAvailable()) {
    throw new IllegalStateException("No compatible GPU found – cannot enable GPU acceleration.");
}
```

### الصور الكبيرة وحدود الذاكرة
معالجة صورة بدقة 100 MP قد تستنزف ذاكرة GPU. حيلة عملية هي تقليل حجم الصورة **بقدر كافٍ** للبقاء ضمن حدود الذاكرة مع الحفاظ على وضوح النص:

```java
ocrEngine.getConfig().setMaxImageDimension(4096); // caps width/height to 4096px
```

### تنسيقات الصور المدعومة
يفهم Aspose OCR تنسيقات JPEG، PNG، BMP، TIFF، وحتى PDF. إذا كنت بحاجة إلى **استخراج النص من الصورة** للملفات المخزنة بتنسيق مختلف، حوّلها أولاً باستخدام مكتبة مثل ImageIO.

## الخطوة 5 – النتيجة المتوقعة والتحقق
عند انتهاء البرنامج، ستطبع وحدة التحكم النص الخام الناتج عن OCR. بالنسبة لصورة إيصال نموذجية، قد ترى:

```
Store: Coffee Corner
Date: 2026-02-25
Items:
  - Latte $4.50
  - Croissant $2.75
Total: $7.25
```

إذا كان الإخراج مشوشًا، فكر في:
* التأكد من أن الصورة مضاءة جيدًا وغير مضغوطة بشكل مفرط.
* تعديل خيار `setLanguage` إذا لم يكن النص بالإنجليزية.
* التحقق من أن نسخة نواة GPU تتطابق مع برنامج التشغيل الخاص بك (الإصدارات غير المتطابقة قد تسبب عيوبًا دقيقة).

**`ocrResult.getWords()` تُعيد مجموعة من كائنات `Word`، كل منها يوفر درجة ثقة عبر `getConfidence()`.** هذا يتيح لك تصفية النتائج ذات الثقة المنخفضة.

## الخطوة 6 – ما بعد ذلك: المعالجة الدفعية والنداءات غير المتزامنة
غالبًا ما تحتاج المشاريع الواقعية إلى **استخراج النص من الصورة** لمجموعات. يمكنك تغليف المنطق أعلاه داخل حلقة أو استخدام `CompletableFuture` في Java لتشغيل عدة مهام OCR بالتوازي، كل واحدة على تدفق GPU منفصل (إذا كان جهازك يدعم ذلك). إليك مخطط سريع:

```java
import java.util.concurrent.*;
import java.nio.file.*;

public class BatchGpuOcr {
    public static void main(String[] args) throws Exception {
        ExecutorService pool = Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors());

        Files.list(Paths.get("photos/"))
             .filter(p -> p.toString().endsWith(".jpg"))
             .forEach(path -> pool.submit(() -> {
                 OcrEngine engine = new OcrEngine();
                 engine.getConfig().setUseGpu(true);
                 OcrResult result = engine.processImage(path.toString());
                 System.out.println("Result for " + path.getFileName() + ":\n" + result.getText());
             }));

        pool.shutdown();
        pool.awaitTermination(1, TimeUnit.HOURS);
    }
}
```

هذا النهج يتيح لك **تحويل الصورة إلى نص** على نطاق واسع مع الاستفادة من تسريع GPU.

## الأسئلة المتكررة (FAQ)
**س: هل يعمل هذا على macOS؟**  
A: نعم، طالما لديك GPU متوافق مع Metal والملف الثنائي المناسب لـ Aspose OCR لنظام macOS. نفس استدعاء `setUseGpu(true)` يُطبق.

**س: هل يمكنني استخدام نسخة Community المجانية؟**  
A: نسخة Community تتضمن استدلال CPU‑only فقط. لتمكين GPU تحتاج إلى نسخة مرخصة (أو نسخة تجريبية تشمل دعم GPU).

**س: ماذا لو احتجت إلى **التعرف على النص من الصورة** بلغة غير الإنجليزية؟**  
A: استدعِ `ocrEngine.getConfig().setLanguage("spa")` للإسبانية، `"fra"` للفرنسية، إلخ. حزم اللغات مدمجة مع المكتبة.

**س: هل هناك طريقة للحصول على درجات الثقة لكل كلمة؟**  
A: نعم—`ocrResult.getWords()` تُعيد مجموعة حيث كل كائن `Word` يحتوي على طريقة `getConfidence()`.

**س: كيف يمكنني فرض وضع GPU‑only صارم؟**  
A: بعد إنشاء المحرك، استدعِ `ocrEngine.getConfig().setRequireGpu(true)`. سترمي المكتبة استثناءً إذا لم يُعثر على GPU متوافق، مما يمنع الانتقال الصامت إلى CPU.

## الخلاصة
لقد غطينا **كيفية تمكين GPU** لـ Aspose OCR في Java، واستعرضنا مثالًا كاملاً قابلًا للتنفيذ، واستكشفنا المشكلات الشائعة عندما تريد **استخراج النص من الصورة**، **تحويل الصورة إلى نص**، أو **التعرف على النص من الصورة**. من خلال تبديل علم واحد وضمان تحديث برامج التشغيل، يمكنك تقليل ثوانٍ من كل استدعاء OCR وتوسيع نطاق دفعات الصور الضخمة دون عناء.

هل أنت مستعد للخطوة التالية؟ جرّب تغذية مخرجات OCR إلى خط أنابيب معالجة اللغة الطبيعية، أو جرب فلاتر ما قبل معالجة الصور المختلفة لتعزيز الدقة. لا حدود عندما تجمع بين OCR المدعوم بـ GPU وأدوات Java الحديثة.

---

![مخطط يوضح كيفية تمكين GPU في كود Aspose OCR Java – كيفية تمكين gpu](gpu-ocr-diagram.png)

[مخطط يوضح كيفية تمكين GPU في كود Aspose OCR Java – كيفية تمكين gpu](gpu-ocr-diagram.png)

*نص بديل للصورة:* "مخطط يوضح كيفية تمكين GPU في كود Aspose OCR Java – كيفية تمكين gpu"

---

**آخر تحديث:** 2026-10-19  
**تم الاختبار مع:** Aspose OCR for Java 23.10  
**المؤلف:** Aspose  

```xml
<!-- Step 1: Include Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

## دروس ذات صلة
- [كيفية تكوين GPU للتعرف الضوئي على الأحرف (OCR) واستخراج النص من الصورة](/ocr/java/advanced-ocr-techniques/how-to-configure-gpu-for-ocr-recognize-text-from-image/)
- [التعرف على نص الصورة باستخدام Aspose OCR GPU Java](/ocr/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/)
- [استخراج النص من الصورة باستخدام دليل Aspose OCR Java](/ocr/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}