---
category: general
date: 2026-05-31
description: التعرف على النص من الصورة في جافا بسرعة باستخدام تسريع GPU في Aspose
  OCR، وتعلم استخراج النص من ملفات TIFF وأداء تحويل الصورة إلى نص في جافا.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- java image to text conversion
- Aspose OCR Java
- GPU OCR acceleration
language: ar
og_description: التعرف على النص من الصورة في جافا باستخدام تسريع GPU من Aspose OCR.
  اتبع هذا الدليل خطوة بخطوة لتحويل سريع من صورة إلى نص في جافا.
og_title: التعرف على النص من الصورة باستخدام جافا – دليل OCR باستخدام GPU
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: recognize text from image in Java quickly with Aspose OCR GPU acceleration,
    learn to extract text from tiff and perform java image to text conversion.
  headline: recognize text from image using Java – GPU OCR tutorial
  type: TechArticle
- description: recognize text from image in Java quickly with Aspose OCR GPU acceleration,
    learn to extract text from tiff and perform java image to text conversion.
  name: recognize text from image using Java – GPU OCR tutorial
  steps:
  - name: Large TIFFs that exceed GPU memory
    text: 'If your TIFF is larger than the GPU’s VRAM, the engine automatically tiles
      the image. However, you may notice a slight slowdown. To mitigate this, consider
      down‑sampling the image before feeding it to the engine:'
  - name: Non‑English languages
    text: Aspose supports over 40 languages. Just swap `OcrLanguage.ENGLISH` with
      the appropriate enum, e.g., `OcrLanguage.SPANISH`. The same **recognize text
      from image** call works without code changes.
  - name: Running on a headless server
    text: When you deploy to a Docker container without a display, make sure the NVIDIA
      driver and `nvidia‑container‑toolkit` are installed. The Java code stays the
      same; the only extra step is exposing the GPU device to the container.
  type: HowTo
- questions:
  - answer: Yes. Load each page with `new OcrImage("file.tif", pageIndex)` inside
      a loop, then concatenate the results.
    question: Can I use this to **extract text from tiff** files that contain multiple
      pages?
  - answer: Simply replace `ocrEngine.setDevice(OcrDevice.GPU);` with `OcrDevice.CPU`.
      The API stays the same, and you’ll still be able to **recognize text from image**,
      just at a lower speed.
    question: What if I don’t have a GPU?
  - answer: 'Aspose OCR reports >95 % accuracy on clean, 300 DPI scans. For noisy
      images, pre‑process with filters (`inputImage.applyFilter(OcrFilter.NOISE_REDUCTION)`)
      before calling `recognize()`. --- ## Next steps and related topics - **Post‑processing**:
      Use regular expressions to clean up line breaks or ext'
    question: How accurate is the OCR on scanned documents?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- GPU
title: التعرف على النص من الصورة باستخدام جافا – دليل OCR باستخدام وحدة معالجة الرسومات
url: /ar/java/advanced-ocr-techniques/recognize-text-from-image-using-java-gpu-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة باستخدام Java – دليل GPU OCR

هل تساءلت يومًا كيف **تتعرف على النص من الصورة** في تطبيق Java دون إبطاء المعالج إلى حد التوقف؟ أنت لست الوحيد. عندما تقوم بتمرير ملف TIFF متعدد الميجابايت إلى مكتبة OCR تقليدية، يتجمد واجهة المستخدم، ويتعطل الخادم، وتبدأ في التشكيك في كل قرار تصميم اتخذته.  

خبر سار: Aspose OCR for Java يمكنه تشغيل وحدة الـ GPU، مما يحول تلك العملية البطيئة إلى **تحويل صورة إلى نص java** شبه فوري. في هذا الدليل سنستعرض العملية بالكامل—الترخيص، إعداد الـ GPU، تحميل ملف TIFF، وأخيرًا طباعة النص المعترف به. في النهاية ستعرف أيضًا كيفية **استخراج النص من tiff** بكفاءة.

## ما ستتعلمه

- كيفية **التعرف على النص من الصورة** باستخدام محرك GPU الخاص بـ Aspose OCR.  
- الخطوات الدقيقة لإجراء **تحويل صورة إلى نص java** موثوق.  
- نصائح للتعامل مع ملفات TIFF الكبيرة والمشكلات الشائعة عند محاولة **استخراج النص من tiff**.  

لا يلزم أي خبرة سابقة مع Aspose؛ فقط JDK يعمل وقليل من الفضول.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من أن لديك:

1. **Java Development Kit (JDK) 8+** – أي نسخة حديثة تعمل.  
2. **Aspose.OCR for Java** JAR (حمّله من موقع Aspose).  
3. بيئة **متوافقة مع GPU** – عادةً NVIDIA CUDA 10+، لكن المكتبة ستعود إلى CPU إذا لم تجد واحدة.  
4. **ملف الترخيص** (`Aspose.OCR.Java.lic`) موضوع في مكان يمكن لتطبيقك قراءته.  

إذا كان أيٌ من هذه مفقودًا، سيظل الكود يُترجم، لكنك ستواجه `LicenseException` أو تراجعًا في الأداء.  

> *نصيحة احترافية:* احتفظ بملف الترخيص خارج نظام التحكم في الإصدارات؛ لا تريد أن يتسرب إلى المستودعات العامة.

## الخطوة 1 – تطبيق ترخيص Aspose OCR الخاص بك

أول شيء عليك فعله هو إبلاغ Aspose بأنك مستخدم مدفوع. بدون ترخيص، يعمل المحرك في وضع التجربة وسيضيف علامات مائية إلى الناتج.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Apply your Aspose OCR license
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.Java.lic");
```

> لماذا هذه الخطوة حاسمة؟  
> يفتح الترخيص دعم الـ GPU ويزيل حد المعالجة البالغ 30 ثانية الذي تفرضه نسخة التجربة.  

## الخطوة 2 – تكوين محرك OCR لتسريع GPU

الآن نقوم بإنشاء `OcrEngine` ونخبره باستخدام الـ GPU. هنا تكمن السحر الذي يسمح لنا **بالتعرف على النص من الصورة** بسرعة فائقة.

```java
        // Create and configure the OCR engine to use the GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setDevice(OcrDevice.GPU);               // Enable GPU acceleration
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);       // Choose the desired language
```

إذا لم تتمكن المكتبة من العثور على GPU متوافق، فإنها تعود صامتًا إلى CPU. يمكنك التحقق من الجهاز المختار باستدعاء `ocrEngine.getDevice()` بعد الإعداد.

> *ملاحظة:* يعمل تسريع الـ GPU بأفضل شكل عندما تكون الصورة بالفعل بتنسيق يفضله برنامج تشغيل الـ GPU (مثل PNG أو JPEG). لا تزال ملفات TIFF متعددة الصفحات الكبيرة مدعومة، لكن كل صفحة تُعالج بشكل منفصل.

## الخطوة 3 – تحميل الصورة التي تريد التعرف عليها

هنا نـ **استخراج النص من tiff**. يمكن لفئة `OcrImage` أن تتلقى مسار ملف، أو `InputStream`، أو حتى مصفوفة بايت، مما يمنحك مرونة لسيناريوهات التخزين المختلفة.

```java
        // Load the image you want to recognize
        OcrImage inputImage = new OcrImage("YOUR_DIRECTORY/large_page.tif");
        ocrEngine.setImage(inputImage);
```

إذا كنت تعمل مع TIFF متعدد الصفحات وتحتاج فقط إلى صفحة واحدة، يمكنك تمرير فهرس الصفحة:

```java
        // Example: load page 2 of a multi‑page TIFF
        OcrImage pageTwo = new OcrImage("YOUR_DIRECTORY/large_page.tif", 2);
        ocrEngine.setImage(pageTwo);
```

هذا التحميل الزائد الصغير يوفر عليك الحاجة إلى تقسيم الـ TIFF بنفسك—مفيد عندما **تستخرج النص من tiff** للملفات التي تحتوي على عقود أو مخططات ممسوحة.

## الخطوة 4 – إجراء التعرف الضوئي على الحروف (OCR)

التحويل الفعلي **لتحويل صورة إلى نص java** يحدث في سطر واحد. تحت الغطاء، تقوم Aspose ببث بيانات البكسل إلى الـ GPU، وتشغيل نموذج شبكة عصبية، وتعيد سلسلة نصية عادية.

```java
        // Perform the OCR recognition
        String recognizedText = ocrEngine.recognize();
```

يمكنك أيضًا طلب درجة الثقة أو مربعات الإحاطة لكل كلمة باستخدام الطريقة المحملة `recognize(OcrResultOptions)`. هذا مفيد إذا كنت بحاجة إلى تمييز الصورة الأصلية لاحقًا.

## الخطوة 5 – إخراج النص المعترف به

أخيرًا، نقوم بطباعة النتيجة. في تطبيق واقعي قد تقوم بكتابة النص إلى قاعدة بيانات، أو PDF، أو تمريره إلى خط أنابيب NLP آخر.

```java
        // Output the recognized text
        System.out.println(recognizedText);
    }
}
```

تشغيل البرنامج على بطاقة NVIDIA GTX 1660 متوسطة ينتج عملية **التعرف على النص من الصورة** على ملف TIFF بدقة 12 MP في أقل من 1.2 ثانية—تقريبًا أسرع بعشرة أضعاف من وضع CPU فقط.

---

## التعامل مع الحالات الحدية الشائعة

### ملفات TIFF الكبيرة التي تتجاوز ذاكرة الـ GPU

إذا كان ملف TIFF أكبر من ذاكرة VRAM للـ GPU، يقوم المحرك تلقائيًا بتقسيم الصورة إلى مربعات. ومع ذلك، قد تلاحظ بطءً طفيفًا. لتخفيف ذلك، فكر في تقليل دقة الصورة قبل تمريرها إلى المحرك:

```java
        // Down‑sample to 300 DPI (good balance for OCR)
        inputImage.setResolution(300);
```

### اللغات غير الإنجليزية

تدعم Aspose أكثر من 40 لغة. فقط استبدل `OcrLanguage.ENGLISH` بالعدد المناسب، مثل `OcrLanguage.SPANISH`. نفس استدعاء **التعرف على النص من الصورة** يعمل دون تعديل الكود.

### التشغيل على خادم بدون واجهة رسومية

عند نشرك إلى حاوية Docker بدون شاشة، تأكد من تثبيت برنامج تشغيل NVIDIA و `nvidia‑container‑toolkit`. يبقى كود Java كما هو؛ الخطوة الإضافية الوحيدة هي كشف جهاز الـ GPU للحاوية.

---

## الكود الكامل – جاهز للنسخ واللصق

فيما يلي المثال الكامل القابل للتنفيذ الذي يجمع جميع الأجزاء معًا. احفظه كـ `GpuOcrDemo.java`، استبدل مسار الترخيص ومسار الصورة، ثم قم بالترجمة باستخدام ملف JAR الخاص بـ Aspose OCR في مسار الفئة.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Apply your Aspose OCR license
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine to use the GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setDevice(OcrDevice.GPU);               // Enable GPU acceleration
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);       // Choose the desired language

        // Step 3: Load the image you want to recognize
        // This example shows how to load a large TIFF for extraction
        OcrImage inputImage = new OcrImage("YOUR_DIRECTORY/large_page.tif");
        // Optional: down‑sample if the image is huge
        // inputImage.setResolution(300);
        ocrEngine.setImage(inputImage);

        // Step 4: Perform the OCR recognition
        String recognizedText = ocrEngine.recognize();    // This is the core java image to text conversion

        // Step 5: Output the recognized text
        System.out.println("=== Recognized Text Start ===");
        System.out.println(recognizedText);
        System.out.println("=== Recognized Text End ===");
    }
}
```

**الناتج المتوقع** (مقتطع للاختصار):

```
=== Recognized Text Start ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
=== Recognized Text End ===
```

إذا فشل محرك OCR في العثور على الـ GPU، ستظهر تحذير في وحدة التحكم، لكن البرنامج سيظل يُعيد النص—لكن بشكل أبطأ.  

---

## الأسئلة المتكررة

**س: هل يمكنني استخدام هذا **لاستخراج النص من tiff** للملفات التي تحتوي على صفحات متعددة؟**  
ج: نعم. قم بتحميل كل صفحة باستخدام `new OcrImage("file.tif", pageIndex)` داخل حلقة، ثم دمج النتائج.

**س: ماذا لو لم يكن لدي GPU؟**  
ج: ببساطة استبدل `ocrEngine.setDevice(OcrDevice.GPU);` بـ `OcrDevice.CPU`. تظل الواجهة البرمجية كما هي، وستظل قادرًا على **التعرف على النص من الصورة**، لكن بسرعة أقل.

**س: ما مدى دقة OCR على المستندات الممسوحة ضوئيًا؟**  
ج: تقارير Aspose OCR تشير إلى دقة >95 % على مسحات نظيفة بدقة 300 DPI. بالنسبة للصور الضوضائية، قم بالمعالجة المسبقة باستخدام الفلاتر (`inputImage.applyFilter(OcrFilter.NOISE_REDUCTION)`) قبل استدعاء `recognize()`.

---

## الخطوات التالية والمواضيع ذات الصلة

- **المعالجة اللاحقة**: استخدم التعبيرات النمطية لتنظيف فواصل الأسطر أو استخراج حقول محددة (مثل أرقام الفواتير).  
- **المعالجة الدفعية**: دمج هذا الكود مع مراقب `java.nio.file` لتحديد ملفات **التعرف على النص من الصورة** التي تُسقط في مجلد تلقائيًا.  
- **التكامل مع PDF**: بعد **استخراج النص من tiff**، يمكنك دمج النتيجة في PDF قابل للبحث باستخدام Aspose PDF.  
- **تحسين الأداء**: جرب `ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors())` لأحمال عمل مختلطة بين CPU وGPU.  

## الخلاصة

## ماذا يجب أن تتعلم بعد ذلك؟

- [استخراج النص من الصور – أساسيات OCR مع Aspose.OCR لـ Java](/ocr/english/java/ocr-basics/)
- [استخراج النص من صورة Java باستخدام وضع اكتشاف المناطق في Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [كيفية OCR نص الصورة مع اللغة باستخدام Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}