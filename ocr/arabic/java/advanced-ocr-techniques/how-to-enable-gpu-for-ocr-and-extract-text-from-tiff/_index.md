---
category: general
date: 2026-02-14
description: كيفية تمكين وحدة معالجة الرسومات (GPU) في Aspose OCR Java لاستخراج النص
  من الصورة بسرعة. تعلم تحويل ملفات TIFF إلى نص، وتعيين معرف جهاز GPU، وقراءة النص
  من ملفات TIFF.
draft: false
keywords:
- how to enable gpu
- extract text from image
- convert tiff to text
- set gpu device id
- read text from tiff
language: ar
og_description: كيفية تمكين وحدة معالجة الرسومات (GPU) في Aspose OCR Java لاستخراج
  النص من الصورة بسرعة. اتبع هذا الدليل لتحويل ملفات TIFF إلى نص، وتعيين معرف جهاز
  GPU، وقراءة النص من ملف TIFF.
og_title: كيفية تمكين وحدة معالجة الرسومات (GPU) للتعرف الضوئي على الأحرف – استخراج
  النص من ملف TIFF
tags:
- OCR
- Java
- GPU acceleration
title: كيفية تمكين الـ GPU للتعرف الضوئي على الأحرف واستخراج النص من ملفات TIFF
url: /ar/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-and-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين وحدة معالجة الرسومات (GPU) للتعرف الضوئي على الأحرف (OCR) واستخراج النص من ملفات TIFF

هل تساءلت يومًا **كيف يمكنك تمكين الـ GPU** عند إجراء OCR على ملفات TIFF الكبيرة؟ لست وحدك—المطورون يسعون دائمًا للحصول على تلك الزيادة في السرعة، خاصةً عندما تكون الصورة المصدر ملف TIFF متعدد الميجابايت. الخبر السار؟ مع Aspose OCR for Java يمكنك تبديل زر، وتحديد الـ GPU المناسب، ومشاهدة المحرك يندفع عبر الصورة.

في هذا الدرس سنستعرض سير العمل بالكامل: تحميل ملف TIFF، تشغيل تسريع الـ GPU، اختيار جهاز GPU محدد اختياريًا، تشغيل OCR، وأخيرًا **استخراج النص من الصورة**. في النهاية ستتمكن من **تحويل TIFF إلى نص** ببضع أسطر من الشيفرة، وسترى أيضًا كيف **تقرأ النص من ملفات TIFF** على أي منصة مدعومة.

## ما ستحتاجه

- Java 17 أو أحدث (الشيفرة تعمل أيضًا مع Java 8+)
- Aspose OCR for Java 23.10 (أو أحدث نسخة متوفرة وقت الكتابة)
- GPU متوافق مع CUDA مع أحدث برنامج تشغيل مثبت
- ملف TIFF متعدد الصفحات تجريبي (سنسميه `sample_large.tif`)

لا تستخدم Maven؟ لا مشكلة—فقط ضع ملف الـ JAR في مسار الـ classpath وستكون جاهزًا.

![How to enable GPU tutorial](gpu-ocr.png)

*نص بديل للصورة: كيفية تمكين الـ GPU للتعرف الضوئي على الأحرف في Java*

## الخطوة 1: تحميل صورة TIFF للتعرف الضوئي على الأحرف

أولاً وقبل كل شيء: تحتاج إلى كائن `OcrEngine` وصورة مصدر. Aspose OCR يمكنه قراءة أي تنسيق نقطي تقريبًا، لكن TIFF شائع للوثائق الممسوحة ضوئيًا.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the TIFF file – this is where we "read text from TIFF"
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample_large.tif"));
```

> **لماذا هذا مهم:** استدعاء `setImage` يلف الملف في `ImageStream`، مما يسمح للمحرك بمعالجة ملفات TIFF متعددة الصفحات دون الحاجة لتقسيمها يدويًا. إذا تعذر العثور على الملف، ستحصل على استثناء واضح `FileNotFoundException`—لذا تأكد من صحة المسار.

## الخطوة 2: تمكين تسريع الـ GPU

الآن يحدث السحر. تشغيل الـ GPU هو مجرد علم منطقي، لكنه يمكن أن يقلل الثواني—أو حتى الدقائق—من وقت المعالجة.

```java
        // Enable GPU acceleration (requires a supported driver)
        ocrEngine.getEngineOptions().setUseGpu(true);
```

> **نصيحة احترافية:** إذا كان جهازك يحتوي على عدة وحدات GPU، فإن الافتراضي عادةً ما يكون الأولى (الجهاز 0). يمكنك ترك Aspose يختار أفضل جهاز تلقائيًا، لكن تحديده يدويًا قد يجنبك المفاجآت في محطات العمل متعددة الـ GPU.

## الخطوة 3: تعيين معرف جهاز الـ GPU (اختياري)

أحيانًا تعرف بالضبط أي GPU تريد استخدامه—ربما البطاقة الثانية مخصصة لأعباء عمل الذكاء الاصطناعي. هنا يأتي دور `setGpuDeviceId`.

```java
        // Optional: select the GPU device (0 = first device, 1 = second, etc.)
        ocrEngine.getEngineOptions().setGpuDeviceId(0);
```

> **حالة حافة:** إذا مررت معرفًا غير صالح، سيطرح المحرك استثناء `IllegalArgumentException`. يمكن لكود سريع مثل `System.out.println(ocrEngine.getEngineOptions().getAvailableGpuDevices())` أن يعرض لك قائمة المعرفات المتاحة.

## الخطوة 4: معالجة الصورة و **استخراج النص من الصورة**

بعد تكوين المحرك، حان وقت تشغيل OCR. كائن النتيجة يمنحك السلسلة النصية الخام، بالإضافة إلى درجات الثقة إذا احتجت إليها.

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

إذا كان ملف TIFF يحتوي على العبارة “Hello, World!” يجب أن ترى شيئًا مثل:

```
Recognized text:
Hello, World!
```

المحرك يتعامل مع فواصل الأسطر، وعلامات الترقيم، وحتى اكتشاف التخطيط الأساسي. للحصول على تحكم أكثر تفصيلاً (مثل استخراج النص لكل صفحة)، استكشف `ocrResult.getPages()`.

## الخطوة 5: التحقق من النتيجة ومعالجة المشكلات الشائعة

### لماذا قد لا يُستخدم الـ GPU؟

- **عدم توافق برنامج التشغيل:** يجب أن يكون برنامج تشغيل الـ GPU على الأقل بالإصدار الموصى به من Aspose (تحقق من ملاحظات الإصدار).
- **الذاكرة غير كافية:** الصور الكبيرة جدًا قد تتجاوز سعة VRAM للـ GPU. في هذه الحالة، يعود المحرك تلقائيًا إلى الـ CPU—ابحث عن تحذير في وحدة التحكم.
- **عِتاد غير مدعوم:** غالبًا ما تفتقر الرسومات المتكاملة إلى القدرة الحوسبية المطلوبة.

### كيفية الرجوع إلى الـ CPU برمجيًا

```java
if (!ocrEngine.getEngineOptions().isGpuAvailable()) {
    System.out.println("GPU not available – switching to CPU.");
    ocrEngine.getEngineOptions().setUseGpu(false);
}
```

### قراءة النص من TIFF في حلقة

إذا كان لديك مجلد مليء بملفات TIFF، يمكنك التكرار كالتالي:

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".tif"))) {
    ocrEngine.setImage(ImageStream.fromFile(file.getAbsolutePath()));
    OcrResult result = ocrEngine.process();
    System.out.println("File: " + file.getName());
    System.out.println(result.getText());
}
```

هذا المقتطف يوضح كيف **تقرأ النص من ملفات TIFF** بالجملة، مع الاستمرار في الاستفادة من تسريع الـ GPU.

## الأسئلة المتكررة (FAQ)

**س: هل يعمل هذا على لينكس؟**  
ج: بالتأكيد—Aspose OCR متعدد المنصات. فقط تأكد من تثبيت مجموعة أدوات CUDA وبرامج التشغيل.

**س: ماذا لو لم يكن لدي GPU؟**  
ج: عيّن `setUseGpu(false)` أو ببساطة احذف الاستدعاء. المحرك يستخدم الـ CPU افتراضيًا.

**س: هل يمكنني استخراج النص من صيغ أخرى؟**  
ج: نعم، طريقة `setImage` نفسها تقبل JPEG، PNG، BMP، وحتى تدفقات PDF.

**س: ما مدى دقة الـ OCR على ملفات TIFF منخفضة الدقة؟**  
ج: الدقة تنخفض تحت 300 dpi. يُنصح بمعالجة مسبقة للصورة (تحويل إلى ثنائي، تصحيح الميل) قبل تمريرها إلى المحرك.

## الخلاصة

أنت الآن تعرف **كيفية تمكين الـ GPU** لـ Aspose OCR Java، وكيف **تعيين معرف جهاز الـ GPU**، والأهم من ذلك **كيفية استخراج النص من ملفات الصورة**، وخاصة **تحويل TIFF إلى نص** و**قراءة النص من TIFF** بكفاءة. من خلال تبديل علم واحد واختيار جهاز إذا لزم الأمر، ستحصل على تحسينات هائلة في الأداء دون الحاجة لإعادة كتابة أي منطق OCR.

هل أنت مستعد للخطوة التالية؟ جرّب تجربة:

- **معالجة دفعات** مئات ملفات TIFF باستخدام خيوط متوازية.
- **حزم لغات مخصصة** لتحسين التعرف على المستندات المتخصصة.
- **معالجة ما بعد الاستخراج** للسلسلة باستخدام تعبيرات regex لتنظيف التنسيق.

لا تتردد في ترك تعليق إذا واجهت أي صعوبات، وتمنياتنا لك ببرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}