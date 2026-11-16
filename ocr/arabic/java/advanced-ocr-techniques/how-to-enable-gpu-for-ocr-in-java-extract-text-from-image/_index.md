---
category: general
date: 2026-02-27
description: تعلم كيفية تمكين وحدة معالجة الرسومات (GPU) في كود Aspose OCR Java لاستخراج
  النص من الصورة. حوّل الصورة إلى نص وتعرّف على النص من الصورة بكفاءة.
draft: false
keywords:
- how to enable gpu
- extract text from image
- convert photo to text
- how to extract text
- recognize text from photo
language: ar
og_description: كيفية تمكين وحدة معالجة الرسومات (GPU) في Aspose OCR Java واستخراج
  النص من الصورة بسرعة. تحويل الصورة إلى نص والتعرف على النص من الصورة بسهولة.
og_title: كيفية تمكين وحدة معالجة الرسومات (GPU) للتعرف الضوئي على الأحرف (OCR) في
  جافا – استخراج نص سريع
tags:
- OCR
- Java
- GPU
- Aspose
title: كيفية تمكين وحدة معالجة الرسومات (GPU) للتعرف الضوئي على الحروف (OCR) في جافا
  – استخراج النص من الصورة
url: /ar/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين GPU لتقنية OCR في Java – استخراج النص من الصورة

هل تساءلت يومًا **كيف يتم تمكين GPU** عند تشغيل OCR على صورة عالية الدقة؟ لست وحدك. يواجه العديد من مطوري Java عقبة عندما يصبح خط أنابيب OCR بطيئًا على إعداد يعتمد على CPU فقط، خاصةً عندما يتجاوز حجم الصورة عدة ميغابكسل. الخبر السار؟ تمكين تسريع GPU مع Aspose OCR سهل للغاية، ويسمح لك **باستخراج النص من الصورة** في جزء من الوقت.

في هذا الدليل سنستعرض العملية بالكامل: من إعداد مكتبة Aspose OCR، تشغيل علامة GPU، إمدادها بصورة كبيرة، وأخيرًا **تحويل الصورة إلى نص**. في النهاية ستعرف **كيفية استخراج النص** بشكل موثوق، وسترى أيضًا كيف **تتعرف على النص من الصورة** على أجهزة تحتوي على عدة وحدات GPU. لا حاجة لمراجع خارجية—كل ما تحتاجه هنا.

## المتطلبات المسبقة

* Java 17 أو أحدث مثبت (أفضل نسخة هي أحدث نسخة LTS).
* GPU مدعوم من NVIDIA أو AMD مع أحدث برامج التشغيل (CUDA 12.x لـ NVIDIA، ROCm لـ AMD).
* Aspose OCR for Java JARs—احصل على أحدث إصدار 23.x من موقع Aspose.
* Maven أو Gradle لإدارة التبعيات (سنظهر مثالًا لـ Maven).
* صورة عالية الدقة (مثال: `high-res-photo.jpg`) تريد معالجتها.

إذا كان أي من هذه العناصر مفقودًا، سيظل الكود يُترجم، لكن علامة GPU ستُتجاهل وستعود المعالجة إلى CPU.

## الخطوة 1 – إضافة Aspose OCR إلى بناء المشروع (كيفية تمكين GPU)

أولًا: أخبر مشروعك بمكان العثور على مكتبة OCR. في Maven، أضف الاعتماد التالي إلى ملف `pom.xml` الخاص بك:

```xml
<!-- Step 1: Include Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

> **نصيحة احترافية:** إذا كنت تستخدم Gradle، فإن المكافئ هو `implementation 'com.aspose:aspose-ocr:23.10'`. الحفاظ على تحديث المكتبة يضمن حصولك على أحدث نوى GPU وإصلاحات الأخطاء.

الآن بعد أن أصبحت المكتبة في مسار الفئة (classpath)، يمكننا فعليًا **تمكين GPU** في محرك OCR.

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

> **لماذا هذا مهم:** ضبط `setUseGpu(true)` يخبر المكتبة الأصلية بتحميل عمل الشبكة العصبية الالتفافية الثقيلة إلى GPU. على RTX 3080 حديث، نفس الصورة التي تستغرق 8 ثوانٍ على CPU يمكن معالجتها في أقل من ثانية واحدة. إذا تخطيت هذه الخطوة، ستظل **تتعرف على النص من الصورة**، لكنك لن تحصل على تحسين الأداء.

## الخطوة 3 – التحقق من أن GPU يُستخدم فعليًا

قد تتساءل، “هل يقوم GPU فعليًا بالعمل؟” أسهل طريقة للتحقق هي النظر إلى مخرجات وحدة التحكم لمكتبة Aspose OCR عندما تمكّن تسجيل الأخطاء:

```java
// Enable verbose logging – helpful for confirming GPU usage.
ocrEngine.getConfig().setLogLevel(com.aspose.ocr.Config.LogLevel.DEBUG);
```

عند تشغيل البرنامج، سترى أسطرًا مثل:

```
[DEBUG] Using GPU device 0 (NVIDIA GeForce RTX 3080) for OCR processing.
```

إذا لم تشاهد تلك الرسالة، تحقق مرة أخرى من تثبيت برنامج التشغيل وتأكد أن GPU يفي بالحد الأدنى لقدرة الحوسبة (3.5 لـ NVIDIA، 6.0 لـ AMD).

## الخطوة 4 – التعامل مع عدة وحدات GPU وحالات الحافة

### اختيار GPU مختلف

إذا كان جهازك يحتوي على أكثر من GPU (مثلاً GPU مدمج من Intel وبطاقة NVIDIA مخصصة)، يمكنك استهداف الأسرع:

```java
ocrEngine.getConfig().setGpuDeviceId(1); // 1 = second GPU in the system
```

### ماذا لو لم يتم اكتشاف أي GPU؟

Aspose OCR يتراجع بأناقة إلى CPU عندما لا يستطيع العثور على GPU مناسب. لتجنب التراجع الصامت، يمكنك إضافة حارس:

```java
if (!ocrEngine.getConfig().isGpuAvailable()) {
    throw new IllegalStateException("No compatible GPU found – cannot enable GPU acceleration.");
}
```

### الصور الكبيرة وحدود الذاكرة

معالجة صورة بحجم 100 MP قد تستنزف ذاكرة GPU. حيلة عملية هي تقليل حجم الصورة **بقدر ما يكفي** للبقاء ضمن حدود الذاكرة مع الحفاظ على وضوح النص:

```java
ocrEngine.getConfig().setMaxImageDimension(4096); // caps width/height to 4096px
```

### صيغ الصور المدعومة

Aspose OCR يدعم JPEG، PNG، BMP، TIFF، وحتى PDF. إذا كنت بحاجة إلى **استخراج النص من الصورة** للملفات المخزنة بصيغة مختلفة، قم بتحويلها أولاً باستخدام مكتبة مثل ImageIO.

## الخطوة 5 – المخرجات المتوقعة والتحقق

عند انتهاء البرنامج، ستطبع وحدة التحكم النص الخام الناتج عن OCR. في صورة إيصال نموذجية، قد ترى:

```
Store: Coffee Corner
Date: 2026-02-25
Items:
  - Latte $4.50
  - Croissant $2.75
Total: $7.25
```

إذا كان الإخراج مشوشًا، فكر في:

* التأكد من أن الإضاءة على الصورة جيدة وليست مضغوطة بشكل مفرط.
* ضبط خيار `setLanguage` إذا لم يكن النص باللغة الإنجليزية.
* التحقق من أن نسخة نواة GPU تتطابق مع برنامج التشغيل (الإصدارات غير المتطابقة قد تسبب عيوبًا دقيقة).

## الخطوة 6 – ما بعد ذلك: المعالجة الدفعية والنداءات غير المتزامنة

المشاريع الواقعية غالبًا ما تحتاج إلى **استخراج النص من الصورة** لمجموعات. يمكنك تغليف المنطق أعلاه في حلقة أو استخدام `CompletableFuture` في Java لتشغيل عدة مهام OCR بالتوازي، كل منها على تدفق GPU منفصل (إذا كان جهازك يدعم ذلك). إليك مخطط سريع:

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
ج: نعم، طالما لديك GPU متوافق مع Metal والملف الثنائي المناسب لـ Aspose OCR لنظام macOS. نفس استدعاء `setUseGpu(true)` يُطبق.

**س: هل يمكنني استخدام النسخة المجانية Community Edition؟**  
ج: النسخة المجانية تشمل الاستدلال على CPU فقط. لتمكين GPU تحتاج إلى نسخة مرخصة (أو تجربة مع دعم GPU).

**س: ماذا لو احتجت إلى **التعرف على النص من الصورة** بلغة غير الإنجليزية؟**  
ج: استدعِ `ocrEngine.getConfig().setLanguage("spa")` للإسبانية، `"fra"` للفرنسية، إلخ. حزم اللغات مدمجة مع المكتبة.

**س: هل هناك طريقة للحصول على درجات الثقة لكل كلمة؟**  
ج: نعم—`ocrResult.getWords()` تُعيد مجموعة حيث يحتوي كل كائن `Word` على طريقة `getConfidence()`.

## الخلاصة

لقد غطينا **كيفية تمكين GPU** لـ Aspose OCR في Java، استعرضنا مثالًا كاملاً قابلًا للتنفيذ، واستكشفنا المشكلات الشائعة عندما تريد **استخراج النص من الصورة**، **تحويل الصورة إلى نص**، أو **التعرف على النص من الصورة**. من خلال تبديل علامة واحدة وضمان تحديث برامج التشغيل، يمكنك تقليل الثواني من كل استدعاء OCR وتوسيع نطاق دفعات الصور الضخمة دون عناء.

هل أنت مستعد للخطوة التالية؟ جرّب تغذية مخرجات OCR إلى خط أنابيب معالجة اللغة الطبيعية، أو جرب فلاتر معالجة مسبقة مختلفة للصور لتحسين الدقة. لا حدود لك عندما تجمع بين OCR المدعوم بـ GPU وأدوات Java الحديثة.

---

![مخطط يوضح كيفية تمكين GPU في كود Aspose OCR Java – كيفية تمكين GPU](gpu-ocr-diagram.png)

*نص بديل للصورة:* "مخطط يوضح كيفية تمكين GPU في كود Aspose OCR Java – كيفية تمكين GPU"

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}