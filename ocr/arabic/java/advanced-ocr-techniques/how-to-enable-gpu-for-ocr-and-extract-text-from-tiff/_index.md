---
category: general
date: 2026-09-23
description: تعلم كيفية استخراج النص من ملف tiff بسرعة عن طريق تمكين تسريع GPU في
  Aspose OCR for Java. دليل خطوة بخطوة يغطي تحميل TIFF، تعيين معرف جهاز GPU، وقراءة
  النص.
draft: false
keywords:
- extract text from tiff file
- gpu acceleration java
- ocr tiff java
- aspose ocr gpu
lastmod: 2026-09-23
og_description: تعلم كيفية استخراج النص من ملف tiff بسرعة عن طريق تمكين تسريع GPU
  في Aspose OCR for Java. يوضح الدليل تحميل TIFF، اختيار جهاز GPU، وقراءة النص المستخرج.
og_image_alt: 'Tutorial image: enabling GPU for OCR in Java'
og_title: استخراج النص من ملف tiff مع تسريع GPU في OCR Java
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Learn how to extract text from tiff file quickly by enabling GPU acceleration
    in Aspose OCR for Java. Step‑by‑step guide covers loading TIFF, setting GPU device
    ID, and reading text.
  headline: How to extract text from tiff file using GPU in OCR Java
  type: TechArticle
- questions:
  - answer: Absolutely—Aspose OCR runs on Windows, Linux, and macOS as long as the
      CUDA toolkit and drivers are installed.
    question: Does this work on Linux?
  - answer: Omit the `setUseGpu(true)` call or explicitly call `setUseGpu(false)`;
      the engine will run on CPU.
    question: What if I don’t have a GPU?
  - answer: Yes. `setImage` accepts JPEG, PNG, BMP, PDF, and more.
    question: Can I extract text from other formats?
  - answer: Accuracy drops sharply below 300 dpi. Pre‑process the image (binarization,
      deskew) for better results.
    question: How accurate is OCR on low‑resolution TIFFs?
  - answer: The library handles 30+ raster and document formats, including TIFF, JPEG,
      PNG, BMP, PDF, and GIF.
    question: How many formats does Aspose OCR support?
  type: FAQPage
tags:
- OCR
- Java
- GPU acceleration
title: كيفية استخراج النص من ملف tiff باستخدام GPU في OCR Java
url: /ar/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-and-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخراج النص من ملف TIFF باستخدام GPU في OCR Java

إذا كنت بحاجة إلى **استخراج النص من ملف TIFF** بسرعة، فإن تشغيل تسريع GPU في Aspose OCR for Java هو أسرع طريقة. في أول 100 كلمة سنشرح لماذا GPU مهم، ثم نرشدك عبر تحميل TIFF، تمكين GPU، اختيار جهاز محدد اختياريًا، تشغيل OCR، وأخيرًا قراءة النص المستخرج. في النهاية ستتمكن من تحويل TIFF إلى نص ببضع أسطر من الشيفرة فقط.

## إجابات سريعة
- **ما هي الفائدة الرئيسية من OCR باستخدام GPU؟** حتى 5× أسرع في المعالجة للملفات الكبيرة متعددة الصفحات من نوع TIFF.  
- **ما نسخة Java المطلوبة؟** Java 17 أو أحدث (Java 8+ يعمل أيضاً).  
- **هل أحتاج إلى ترخيص خاص؟** يلزم وجود ترخيص صالح لـ Aspose OCR for Java للاستخدام في الإنتاج.  
- **هل يمكن تشغيله على Linux؟** نعم—Aspose OCR متعدد المنصات؛ فقط قم بتثبيت مجموعة أدوات CUDA.  
- **هل GPU اختياري؟** يمكنك الرجوع إلى CPU باستدعاء `setUseGpu(false)`.

## ما هو OcrEngine؟
فئة `OcrEngine` هي المكوّن المركزي في Aspose OCR for Java. إنها تغلف جميع وظائف OCR، مما يتيح لك تحميل الصور، تكوين خيارات المعالجة مثل اللغة واستخدام GPU، واسترجاع النص المعترف به وبيانات الثقة في كائن مريح.

`OcrEngine` هي الفئة الأساسية في Aspose OCR التي تمثّل محرك معالجة OCR وتوفر طرقًا لتحميل الصور، تكوين الخيارات، واسترجاع النتائج.

## كيفية تمكين GPU لـ OCR في Java؟
حمّل صورتك، شغّل GPU، واستدعِ `recognize`—هذا كل ما تحتاجه. تمكين GPU باستخدام `setUseGpu(true)` يسمح للمحرك بتحميل الأعمال المكثفة من البكسلات إلى بطاقة الرسوميات، مما يقلل وقت المعالجة بشكل كبير، خاصةً للصور عالية الدقة أو ملفات TIFF متعددة الصفحات.

## ما ستحتاجه

- Java 17 أو أحدث (الكود يعمل أيضاً على Java 8+).  
- Aspose OCR for Java 23.10 (أو أحدث إصدار).  
- GPU متوافق مع CUDA مع أحدث برنامج تشغيل مثبت.  
- ملف TIFF متعدد الصفحات تجريبي (مثال: `sample_large.tif`).  

لا Maven؟ فقط ضع ملف JAR في مسار الفئات الخاص بك.

![كيفية تمكين GPU لـ OCR في Java](gpu-ocr.png)

[كيفية تمكين GPU لـ OCR في Java](gpu-ocr.png)

*نص بديل للصورة: كيفية تمكين GPU لـ OCR في Java*

## الخطوة 1: تحميل صورة TIFF لـ OCR

طريقة `setImage` تغلف الملف في `ImageStream`، مما يسمح للمحرك بمعالجة ملفات TIFF متعددة الصفحات دون الحاجة إلى تقسيم يدوي. إذا تعذر العثور على الملف، سيتم إلقاء استثناء واضح `FileNotFoundException`.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the TIFF file – this is where we "read text from TIFF"
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample_large.tif"));
```

> **لماذا هذا مهم:** استدعاء `setImage` يختصر التعامل مع الصفحات، بحيث يمكنك معالجة مستند كامل باستخدام نسخة محرك واحدة.

## الخطوة 2: تمكين تسريع GPU

تشغيل GPU هو مجرد علم منطقي واحد. في معظم الأنظمة يكون GPU الافتراضي هو الجهاز 0، لكن يمكنك السماح لـ Aspose باختيار الجهاز الأمثل تلقائيًا.

```java
        // Enable GPU acceleration (requires a supported driver)
        ocrEngine.getEngineOptions().setUseGpu(true);
```

> **نصيحة احترافية:** في محطات العمل التي تحتوي على عدة بطاقات GPU، تحديد معرف الجهاز يجنب الانتقال غير المتوقع إلى GPU مدمج أبطأ.

## الخطوة 3: تعيين معرف جهاز GPU (اختياري)

إذا كنت تعرف أي GPU يجب أن يتولى OCR—ربما بطاقة AI مخصصة—يمكنك تعيينه صراحةً باستخدام `setGpuDeviceId`.  

```java
        // Optional: select the GPU device (0 = first device, 1 = second, etc.)
        ocrEngine.getEngineOptions().setGpuDeviceId(0);
```

> **حالة حافة:** تمرير معرف غير صالح يثير استثناء `IllegalArgumentException`. استخدم `ocrEngine.getEngineOptions().getAvailableGpuDevices()` لسرد المعرفات الصالحة.

## الخطوة 4: معالجة الصورة واستخراج النص من الصورة

تشغيل OCR يُعيد كائن `OcrResult` يحتوي على السلسلة النصية العادية ودرجات الثقة الاختيارية.  

```java
        // Perform OCR – this is where we "convert TIFF to text"
        OcrResult ocrResult = ocrEngine.process();

        // Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

### النتيجة المتوقعة

إذا كان TIFF يحتوي على “Hello, World!” فإن النتيجة ستظهر كالتالي:

```
Recognized text:
Hello, World!
```

المحرك يتعامل تلقائيًا مع فواصل الأسطر، علامات الترقيم، واكتشاف التخطيط الأساسي. لاستخراج النص لكل صفحة، استكشف `ocrResult.getPages()`.

## الخطوة 5: التحقق من النتيجة ومعالجة المشكلات الشائعة

قد يتم تجاوز GPU لعدة أسباب. إذا كان إصدار برنامج التشغيل المثبت أقدم من الحد الأدنى المطلوب، لا يمكن للمكتبة تهيئة CUDA. نقص الذاكرة الفيديوية قد يسبب عودة المحرك إلى CPU، وبعض الرسومات المدمجة تفتقر إلى القدرة الحوسبية المطلوبة لتسريع OCR.

### لماذا قد لا يتم استخدام GPU؟

- **عدم توافق السائق:** يجب أن يفي سائق GPU بالحد الأدنى من الإصدار المذكور في ملاحظات إصدار Aspose.  
- **الذاكرة غير كافية:** قد تتجاوز الصور الكبيرة سعة VRAM؛ ثم يعود المحرك إلى CPU ويسجل تحذيراً.  
- **الأجهزة غير المدعومة:** غالباً ما تفتقر الرسومات المتكاملة إلى القدرة الحوسبية المطلوبة لتسريع OCR.

### كيفية الرجوع إلى CPU برمجياً

إذا كنت بحاجة إلى ضمان معالجة عبر CPU، استدعِ مُعدّل خيارات المحرك مع علم false. هذا يعطل أي محاولات GPU ويجبر خط أنابيب OCR على العمل بالكامل على المعالج المضيف، وهو مفيد على الأجهزة التي لا تحتوي على بطاقات رسومية متوافقة.

```java
if (!ocrEngine.getEngineOptions().isGpuAvailable()) {
    System.out.println("GPU not available – switching to CPU.");
    ocrEngine.getEngineOptions().setUseGpu(false);
}
```

### قراءة النص من TIFF في حلقة

عند معالجة العديد من الملفات، كرّر عبر دليل مع الحفاظ على تمكين تسريع GPU.

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".tif"))) {
    ocrEngine.setImage(ImageStream.fromFile(file.getAbsolutePath()));
    OcrResult result = ocrEngine.process();
    System.out.println("File: " + file.getName());
    System.out.println(result.getText());
}
```

يظهر هذا المقتطف كيفية **قراءة النص من ملفات TIFF** بالجملة دون فقدان تعزيز الأداء.

## الأسئلة المتكررة (FAQ)

**س: هل يعمل هذا على Linux؟**  
ج: بالتأكيد—Aspose OCR يعمل على Windows وLinux وmacOS طالما تم تثبيت مجموعة أدوات CUDA والسائقين.

**س: ماذا لو لم يكن لدي GPU؟**  
ج: احذف استدعاء `setUseGpu(true)` أو استدعِ صراحةً `setUseGpu(false)`؛ سيعمل المحرك على CPU.

**س: هل يمكن استخراج النص من صيغ أخرى؟**  
ج: نعم. `setImage` يقبل JPEG, PNG, BMP, PDF، وأكثر.

**س: ما مدى دقة OCR على ملفات TIFF منخفضة الدقة؟**  
ج: الدقة تنخفض بشكل حاد تحت 300 dpi. قم بتهيئة الصورة مسبقاً (تحويل إلى ثنائي، تصحيح الميل) للحصول على نتائج أفضل.

**س: كم عدد الصيغ التي يدعمها Aspose OCR؟**  
ج: المكتبة تدعم أكثر من 30 صيغة من الصيغ النقطية والوثائق، بما في ذلك TIFF, JPEG, PNG, BMP, PDF, وGIF.

## الخلاصة

أنت الآن تعرف **كيفية استخراج النص من ملف TIFF** باستخدام تسريع GPU في Aspose OCR for Java، وكيفية تعيين معرف جهاز GPU محدد، وكيفية معالجة ملفات TIFF واحدة أو متعددة بفعالية. عبر تبديل علم واحد تحصل على تحسينات هائلة في السرعة دون تغيير أي من منطق OCR.

الخطوات التالية التي قد تجربها:

- معالجة دفعات مئات ملفات TIFF في خيوط متوازية.  
- تحميل حزم لغات مخصصة لتحسين التعرف على المفردات المتخصصة.  
- معالجة النص المستخرج باستخدام regex لتنظيف التنسيق.

إذا واجهت أي مشكلات، اترك تعليقاً أدناه. برمجة سعيدة!

---

**آخر تحديث:** 2026-09-23  
**تم الاختبار مع:** Aspose OCR for Java 23.10  
**المؤلف:** Aspose

## دروس ذات صلة

- [كيفية تمكين GPU لـ OCR Java خطوة بخطوة](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-step-by-step-guide/)
- [التعرف على النص من صورة باستخدام Aspose OCR دليل Java كامل](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/)
- [معالجة مسبقة لصورة OCR في Java لزيادة الدقة واستخراج النص](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}