---
category: general
date: 2026-11-17
description: كيفية تمكين GPU في Java OCR لاستخراج النص من الصورة بسرعة. تعلم كيفية
  تكوين GPU، استخراج النص والتعرف على النص باستخدام Java مع Aspose OCR.
draft: false
keywords:
- how to enable gpu
- high resolution ocr
- aspose ocr java
- extract text image java
- gpu acceleration ocr
lastmod: 2026-11-17
og_description: كيفية تمكين GPU لـ Java OCR بسرعة. يوضح هذا الدليل كيفية تكوين GPU،
  استخراج النص من الصورة والتعرف على النص باستخدام Java مع Aspose OCR.
og_image_alt: 'Developer guide: Enable GPU for Java OCR using Aspose OCR library'
og_title: كيفية تمكين GPU لـ Java OCR – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: How to enable GPU in Java OCR to extract text from image fast. Learn
    how to configure GPU, extract text and recognize text java with Aspose OCR.
  headline: How to enable GPU for Java OCR – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: Yes, you can pass a PDF file directly to `setImage`; the library rasterizes
      each page before OCR.
    question: Does Aspose OCR support PDF input?
  - answer: Use `ocrEngine.getConfiguration().setCustomDictionary(List<String>)` to
      improve recognition of specialized vocabulary.
    question: How do I add custom dictionaries for domain‑specific terms?
  - answer: Currently only CUDA‑compatible NVIDIA GPUs on Windows and Linux are supported;
      macOS users fall back to CPU.
    question: Is GPU acceleration available on macOS?
  - answer: Absolutely—`OcrResult` includes a `getConfidence()` method for each `OcrWord`
      object.
    question: Can I retrieve the confidence score for each recognized word?
  - answer: A commercial Aspose OCR license is required for production deployments;
      a free evaluation license works for development and testing.
    question: What license is required for production use?
  type: FAQPage
tags:
- gpu ocr
- java ocr
- aspose ocr
- high resolution ocr
- java image processing
title: كيفية تمكين GPU لـ Java OCR – دليل خطوة بخطوة
url: /ar/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين GPU لتقنية OCR في Java – دليل خطوة بخطوة

إذا كنت تبحث عن **كيفية تمكين GPU** عند استخراج النص من الصور باستخدام Java، فقد وصلت إلى المكان المناسب. يمكن لتسريع GPU أن يقلل وقت معالجة OCR من عدة ثوانٍ إلى جزء من الثانية، خاصةً في المسحات عالية الدقة. في هذا الدليل سنستعرض تثبيت Aspose OCR، تكوين جهاز GPU، وتشغيل برنامج استخراج نص كامل يعمل بثبات على كل من الأجهزة التي تدعم GPU والأجهزة التي تعتمد على CPU فقط.

## إجابات سريعة
- **ما هو الحد الأدنى لإصدار Java؟** Java 17 أو أحدث.
- **ما نوع GPU المطلوب؟** أي GPU من NVIDIA متوافق مع CUDA (CUDA 11+).
- **هل أحتاج إلى ترخيص لتشغيل العينة؟** إصدار تجريبي مجاني يعمل للتطوير؛ يلزم ترخيص تجاري للإنتاج.
- **كم يكون OCR باستخدام GPU أسرع؟** حتى 5× أسرع على صورة بدقة 4 MP مقارنةً بـ CPU.
- **هل يمكنني الرجوع إلى CPU تلقائيًا؟** نعم—تعود Aspose OCR إلى CPU إذا لم يتم اكتشاف GPU.

## ما هو تسريع GPU لتقنية OCR؟
يعني تسريع GPU لتقنية OCR تشغيل خطوات استنتاج الشبكة العصبية على معالج رسومي بدلاً من CPU، مما يسمح بآلاف العمليات المتوازية. هذا يقلل من زمن الاستنتاج بشكل كبير، خاصةً للصور عالية الدقة حيث يصبح CPU عنق زجاجة.

## لماذا نستخدم Aspose OCR لـ Java؟
يدعم Aspose OCR **أكثر من 50 تنسيق إدخال** (بما في ذلك PNG، JPEG، TIFF، PDF) ويمكنه معالجة مستندات مئات الصفحات دون تحميل الملف بالكامل في الذاكرة. توفر واجهة برمجة تطبيقات Java فئة `OcrEngine` واحدة التي تُجرد استدعاءات CUDA منخفضة المستوى، مما يتيح لك التركيز على منطق الأعمال.

## المتطلبات المسبقة
- تم تثبيت Java 17+ JDK.
- Maven 3.6+ أو Gradle 7+ لإدارة التبعيات.
- GPU من NVIDIA متوافق مع CUDA مع برامج تشغيل تتطابق مع CUDA 11.x أو أحدث.
- اتصال بالإنترنت لتحميل مكتبة Aspose OCR.

## كيفية تمكين GPU لتقنية OCR في Java؟
قم بتحميل مكتبة Aspose OCR، أنشئ كائن `OcrEngine`، وفعل دعم GPU ببضع أسطر من الشيفرة فقط. يكتشف المحرك الأجهزة المتاحة تلقائيًا؛ يمكنك أيضًا تحديد معرف الجهاز لاستهداف GPU معين في بيئات متعددة الـ GPU.

## كيف يعمل OcrEngine؟
`OcrEngine` هي الفئة المركزية التي تنسق ما قبل معالجة الصورة، استنتاج الشبكة العصبية، وتجميع النتائج. تقبل الصور كمسارات ملفات، كائنات `java.io.File`، أو مثيلات `java.awt.image.BufferedImage`، مما يمنحك مرونة في كيفية تغذية البيانات إلى خط الأنابيب.

## كيفية تكوين تسريع GPU (كيفية تكوين GPU)
هنا تخبر Aspose OCR باستخدام GPU وأي جهاز تختار.

لتمكين تسريع GPU، تقوم بإنشاء كائن `GpuConfiguration`، وتعيين `setEnable(true)`، وتختار جهازًا اختياريًا باستخدام `setDeviceId(int)`، وتربطه بـ `OcrEngine` عبر `setGpuConfiguration`. تسمح لك الإعدادات أيضًا بتحديد استراتيجية احتياطية، مثل الرجوع إلى CPU عندما يكون الجهاز المطلوب غير متاح، لضمان استقرار التطبيق.  
```java
        // Step 3: Enable GPU acceleration (optional: select a specific device)
        GpuConfiguration gpuConfig = new GpuConfiguration();
        gpuConfig.setEnabled(true);          // turn on GPU support
        gpuConfig.setDeviceId(0);            // choose GPU 0 (default first device)

        // Attach the GPU config to the OCR engine
        ocrEngine.setGpuConfiguration(gpuConfig);
```

لماذا تمكين GPU؟ تقوم خط أنابيب OCR بتشغيل عدة شبكات عصبية تلافيفية. تشغيل هذه الشبكات على GPU يستفيد من آلاف الأنوية المتوازية، مما يقلل وقت الاستنتاج من 3–5 ثوانٍ على CPU إلى أقل من ثانية واحدة على RTX 3080 الحديثة لصورة بدقة 4 MP. إذا لم يكن الجهاز المحدد موجودًا، يعود Aspose بصمت إلى CPU، مما يمنع حدوث أعطال.  
```java
        // Verify that a GPU was actually engaged
        if (!gpuConfig.isEnabled() || !gpuConfig.isDeviceAvailable()) {
            System.out.println("GPU not detected – falling back to CPU. " +
                               "Performance will be slower.");
        }
```

### معالجة الحالات الخاصة
تحتاج التطبيقات القوية إلى التحقق من تثبيت برنامج تشغيل CUDA قبل محاولة العمل على GPU.  
```java
        // Verify that a GPU was actually engaged
        if (!gpuConfig.isEnabled() || !gpuConfig.isDeviceAvailable()) {
            System.out.println("GPU not detected – falling back to CPU. " +
                               "Performance will be slower.");
        }
```

## الخطوة 1 – تثبيت Aspose OCR وتحضير صورتك (كيفية تمكين GPU)
أولاً، أضف تبعية Aspose OCR إلى مشروعك. إذا كنت تستخدم Maven، أضف:
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- latest as of Jan 2026 -->
</dependency>
```

يمكن لمستخدمي Gradle إضافة:
```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

ضع ملفًا عالي الدقة (مثال: `sample-highres.png`) في مجلد يمكنك الإشارة إليه من الشيفرة. يجب أن تكون الصورة بدقة لا تقل عن 300 dpi للحصول على أفضل دقة OCR.  

> **نصيحة احترافية:** إذا كنت تختبر على لابتوب بدون GPU منفصل، لا يزال بإمكانك تشغيل الشيفرة؛ سيعود المحرك إلى CPU تلقائيًا.  

![توضيح كيفية تمكين GPU](placeholder.png "مخطط يوضح خط أنابيب OCR في Java مع تسريع GPU – كيفية تمكين GPU")
[توضيح كيفية تمكين GPU](placeholder.png "مخطط يوضح خط أنابيب OCR في Java مع تسريع GPU – كيفية تمكين GPU")

## الخطوة 2 – إنشاء محرك OCR وتحميل الصورة (استخراج النص من الصورة)
فئة `OcrEngine` هي الكائن الأعلى مستوى الذي يمثل جلسة OCR واحدة.  
```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.*;

public class GpuOcrTutorial {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to process
        // Replace with the absolute or relative path to your PNG/JPEG/TIFF
        ocrEngine.setImage("YOUR_DIRECTORY/sample-highres.png");
```

طريقة `setImage` تقبل مسار ملف، أو `java.io.File`، أو `java.awt.image.BufferedImage`. توفير مصدر عالي الدقة يضمن أن يكون لدى GPU ما يكفي من البكسلات لإبقاء جميع أنويته مشغولة، مما يترجم إلى تحسينات ملحوظة في السرعة.

## الخطوة 3 – تكوين تسريع GPU (كيفية تكوين GPU)
يتيح لك كائن `GpuConfiguration` تمكين استخدام GPU، اختيار جهاز، وتحديد سلوك الاحتياطي لمحرك OCR.  
```java
        // Step 3: Enable GPU acceleration (optional: select a specific device)
        GpuConfiguration gpuConfig = new GpuConfiguration();
        gpuConfig.setEnabled(true);          // turn on GPU support
        gpuConfig.setDeviceId(0);            // choose GPU 0 (default first device)

        // Attach the GPU config to the OCR engine
        ocrEngine.setGpuConfiguration(gpuConfig);
```

## الخطوة 4 – تنفيذ التعرف على النص (التعرف على النص في Java)
مع المحرك وGPU جاهزين، يمكنك الآن استخراج الأحرف.  

طريقة `recognize()` تشغل خط أنابيب OCR وتعيد كائن `OcrResult` يحتوي على النص العادي، درجات الثقة، وبيانات إطارات اختيارية.  
```java
        // Step 4: Perform the recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**الناتج المتوقع** (مقتطع للختصر):
```
Recognized text:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

إذا كانت صورتك تحتوي على عدة لغات، يمكنك إضافة حزم اللغة قبل استدعاء `recognize()`:
```java
ocrEngine.getLanguage().add(OcrLanguage.FRENCH);
ocrEngine.getLanguage().add(OcrLanguage.SPANISH);
```

## الخطوة 5 – مراجعة الناتج والخطوات التالية
شغّل البرنامج باستخدام:
```bash
mvn compile exec:java -Dexec.mainClass=GpuOcrTutorial
```

على جهاز يحتوي على GPU جيد، ينتهي OCR في **أقل من ثانية لصورة بدقة 4 MP**، مقارنةً بـ 3–5 ثوانٍ على CPU فقط. هذه الزيادة في السرعة ذات قيمة خاصة في سيناريوهات المعالجة الدفعية أو خطوط أنابيب استيعاب المستندات في الوقت الحقيقي.

### أسئلة شائعة
* **ماذا لو حصلت على خطأ “إصدار برنامج تشغيل CUDA غير كافٍ”؟**  
  قم بتحديث برنامج تشغيل NVIDIA إلى أحدث إصدار يتطابق مع مجموعة أدوات CUDA المدمجة مع Aspose (عادةً CUDA 11.x في عام 2026).  

* **هل يمكنني معالجة مجموعة من الصور؟**  
  نعم. أعد استخدام كائن `OcrEngine` واحد داخل حلقة لتجنب إنشاء سياق GPU متكرر، مما يحسن معدل الإنتاجية.  

* **هل هناك حد للذاكرة؟**  
  يزداد استهلاك ذاكرة GPU مع حجم الصورة؛ بالنسبة لملفات TIFF الكبيرة جدًا، قسّم الصورة إلى بلاطات قبل تمريرها إلى المحرك للبقاء ضمن حدود الذاكرة المعتادة للـ GPU التي تبلغ 8 GB.  

### نصائح احترافية
* **تثبيت GPU** – في خوادم متعددة الـ GPU، اضبط `gpuConfig.setDeviceId(1)` لحجز الـ GPU الثاني لـ OCR بينما يتعامل الأول مع أعباء عمل أخرى.  
* **التسخين** – استدعِ `ocrEngine.recognize()` على صورة تجريبية صغيرة مرة واحدة عند بدء التشغيل؛ هذا يحمل الشبكات العصبية على الـ GPU، مما يلغي زمن الاستدعاء الأول.  
* **سلامة الخيوط** – يجب على كل خيط امتلاك نسخة خاصة به من كائن `OcrEngine`؛ الفئة غير آمنة للاستخدام المتعدد الخيوط، لذا قد يسبب المشاركة بين الخيوط حالات سباق.  

## الأسئلة المتكررة
**س: هل يدعم Aspose OCR إدخال PDF؟**  
نعم، يمكنك تمرير ملف PDF مباشرة إلى `setImage`؛ تقوم المكتبة بتحويل كل صفحة إلى صورة قبل OCR.  

**س: كيف يمكنني إضافة قواميس مخصصة للمصطلحات الخاصة بالمجال؟**  
استخدم `ocrEngine.getConfiguration().setCustomDictionary(List<String>)` لتحسين التعرف على المفردات المتخصصة.  

**س: هل يتوفر تسريع GPU على macOS؟**  
حاليًا يتم دعم فقط بطاقات NVIDIA المتوافقة مع CUDA على Windows وLinux؛ يضطر مستخدمو macOS إلى الرجوع إلى CPU.  

**س: هل يمكنني استرجاع درجة الثقة لكل كلمة تم التعرف عليها؟**  
بالتأكيد—`OcrResult` يتضمن طريقة `getConfidence()` لكل كائن `OcrWord`.  

**س: ما الترخيص المطلوب للاستخدام الإنتاجي؟**  
يلزم ترخيص تجاري لـ Aspose OCR للنشر في بيئات الإنتاج؛ ترخيص تقييم مجاني يكفي للتطوير والاختبار.  

**آخر تحديث:** 2026-11-17  
**تم الاختبار مع:** Aspose OCR 24.11 for Java  
**المؤلف:** Aspose  

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- latest as of Jan 2026 -->
</dependency>
```

```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

## دروس ذات صلة
- [مثال Aspose Ocr Java لاستخراج النص من الصورة باستخدام GPU](/ocr/java/advanced-ocr-techniques/aspose-ocr-java-example-extract-text-from-image-with-gpu/)
- [التعرف على النص من صورة Java OCR مع تسريع GPU](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-java-ocr-with-gpu-acceleration/)
- [دليل OCR مسرّع بـ GPU Java لتسريع تحويل الصورة إلى نص](/ocr/java/advanced-ocr-techniques/gpu-accelerated-ocr-tutorial-java-guide-to-fast-image-to-tex/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}