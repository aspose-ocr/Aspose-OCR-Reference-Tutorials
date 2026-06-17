---
category: general
date: 2026-02-17
description: تعرف على النص في الصورة بسرعة باستخدام دعم Aspose OCR للمعالجة باستخدام
  وحدة معالجة الرسوميات (GPU) في Java. تعلم كيفية استخراج النص من الصورة وتعيين معرف
  جهاز GPU لتحقيق الأداء الأمثل.
draft: false
keywords:
- recognize text image
- extract text from image
- set gpu device id
- Aspose OCR Java
- GPU acceleration OCR
language: ar
og_description: تعرّف على النص في الصورة بسرعة باستخدام دعم Aspose OCR لمعالجة GPU
  في Java. يوضح هذا الدليل كيفية استخراج النص من الصورة وتعيين معرف جهاز GPU.
og_title: التعرف على نص الصورة باستخدام Aspose OCR GPU – Java
tags:
- Java
- OCR
- Aspose
- GPU
title: التعرف على نص الصورة باستخدام Aspose OCR GPU – Java
url: /ar/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

bottom unchanged.

Let's craft final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص في الصورة باستخدام Aspose OCR GPU – Java

هل احتجت يومًا إلى **التعرف على نص الصورة** في تطبيق Java لكن المعالج كان يواجه صعوبة مع الملفات الكبيرة؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عند معالجة المسحات عالية الدقة. الخبر السار؟ Aspose OCR يتيح لك **استخراج النص من الصورة** على وحدة معالجة الرسومات، مما يقلل وقت المعالجة بشكل كبير.  

في هذا الدرس سنستعرض مثالًا كاملاً جاهزًا للتنفيذ يوضح بالضبط كيفية إعداد الترخيص، تمكين تسريع الـ GPU، و**تحديد معرف جهاز الـ GPU** عندما يكون لديك أكثر من بطاقة رسومية. في النهاية ستحصل على برنامج مستقل يطبع النص المعترف به إلى وحدة التحكم—بدون خطوات إضافية.

## ما ستحتاجه

- **Java 17** أو أحدث (الواجهة البرمجية متوافقة مع Java 8+، لكن أحدث نسخة LTS تمنحك أداءً أفضل).  
- مكتبة **Aspose OCR for Java** (حمّل ملف JAR من موقع Aspose).  
- ملف ترخيص **Aspose OCR** صالح (`Aspose.OCR.lic`). النسخة التجريبية المجانية تعمل، لكن ميزات الـ GPU محجوبة خلف ترخيص مدفوع.  
- ملف صورة (`sample-image.png`) يحتوي على نص واضح يمكن قراءته آليًا.  
- بيئة تدعم الـ GPU (بطاقة NVIDIA متوافقة مع CUDA هي الأفضل).  

إذا كان أي من هذه غير مألوف لك، لا تقلق—سنشرح كل نقطة أثناء المتابعة.

## الخطوة 1: إضافة Aspose OCR إلى مشروعك

أولاً، أضف ملف JAR الخاص بـ Aspose OCR إلى مسار الفئات (classpath). إذا كنت تستخدم Maven، أضف الاعتماد التالي إلى `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

لـ Gradle، يكون كالتالي:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

إذا كنت تفضّل الطريقة اليدوية، ضع ملف JAR في مجلد `libs/` وأضفه إلى مسار الوحدة في IDE.

> **نصيحة احترافية:** حافظ على توافق رقم الإصدار مع ملاحظات إصدار المكتبة؛ الإصدارات الأحدث غالبًا ما تجلب تحسينات أداء لمعالجة الـ GPU.

## الخطوة 2: تحميل ترخيص Aspose OCR (مطلوب لاستخدام الـ GPU)

بدون ترخيص، ستعود الدالة `setEnableGpu(true)` صامتًا إلى وضع المعالج المركزي. حمّل الترخيص في بداية الدالة `main`:

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

استبدل `YOUR_DIRECTORY` بالمسار المطلق أو النسبي حيث حفظت ملف `.lic`. إذا كان المسار غير صحيح، سيطلق Aspose استثناء `FileNotFoundException`، لذا تحقق من صحة الكتابة.

## الخطوة 3: إنشاء محرك OCR وتمكين تسريع الـ GPU

الآن نقوم بإنشاء كائن `OcrEngine` ونخبره باستخدام الـ GPU. تسمح لك الدالة `setGpuDeviceId` باختيار بطاقة محددة عندما يكون هناك أكثر من واحدة.

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

لماذا نحتاج معرف الجهاز؟ في خادم متعدد الـ GPU قد تخصص بطاقة واحدة لمعالجة الصور وأخرى للـ OCR. تحديد المعرف يضمن أن العتاد الصحيح هو الذي يقوم بالعمل الشاق.

## الخطوة 4: إعداد صورة الإدخال

Aspose OCR يدعم مجموعة متنوعة من الصيغ (PNG، JPG، BMP، TIFF). غلف ملفك في كائن `OcrInput`:

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

إذا كنت تحتاج إلى معالجة تدفق (مثلاً ملف تم رفعه)، استخدم `ocrInput.add(InputStream)` بدلاً من ذلك.

## الخطوة 5: تشغيل عملية التعرف واسترجاع النتيجة

الدالة `recognize` تُعيد كائن `OcrResult` يحتوي على النص العادي، درجات الثقة، وحتى معلومات التخطيط إذا احتجت إليها.

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

ستظهر وحدة التحكم شيئًا مثل:

```
Recognized text:
Hello, world!
This is a sample image.
```

إذا كانت الصورة غير واضحة أو اللغة غير مدعومة، قد تكون النتيجة فارغة. في هذه الحالة، تحقق من قيمة `ocrResult.getConfidence()` (0‑100) لتقرر ما إذا كنت ستعيد المحاولة مع معالجة مسبقة.

## مثال كامل قابل للتنفيذ

جمع كل الأجزاء معًا يمنحك فئة Java واحدة يمكنك نسخها ولصقها في IDE:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license – required for GPU usage
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // 2️⃣ Create OCR engine and turn on GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getDevice().setEnableGpu(true);      // enable GPU acceleration
        ocrEngine.getDevice().setGpuDeviceId(0);       // optional: select GPU index

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/sample-image.png");

        // 4️⃣ Perform recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + ocrResult.getText());
    }
}
```

> **الناتج المتوقع:** تقوم وحدة التحكم بطباعة النص الدقيق الموجود في `sample-image.png`. إذا كان الـ GPU نشطًا، ستلاحظ انخفاض وقت المعالجة من عدة ثوانٍ (CPU) إلى أقل من ثانية للمسحات بدقة 300 dpi تقريبًا.

## أسئلة شائعة وحالات خاصة

### هل يعمل هذا على خادم بدون واجهة رسومية؟

نعم. يجب تثبيت برنامج تشغيل الـ GPU، لكن لا تحتاج إلى شاشة. فقط تأكد من أن مجموعة أدوات `CUDA` (أو ما يعادلها لبطاقتك) موجودة في متغير النظام `PATH`.

### ماذا لو كان لدي أكثر من بطاقة GPU وأريد استخدام GPU 1؟

غيّر معرف الجهاز:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

### كيف أستخرج النص من صورة بلغة مختلفة؟

حدد اللغة قبل استدعاء `recognize`:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose يدعم أكثر من 30 لغة؛ راجع وثائق الـ API للحصول على القائمة الكاملة.

### ماذا لو كانت الصورة تحتوي على عدة صفحات (مثلاً PDF تم تحويله إلى صور)?

أنشئ إدخالًا منفصلًا في `OcrInput` لكل صفحة، أو كرّر العملية على الملفات:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

سيقوم المحرك بدمج النتائج بالترتيب.

### كيف أتعامل مع النتائج ذات الثقة المنخفضة؟

تحقق من درجة الثقة:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

خطوات المعالجة المسبقة الشائعة تشمل التحويل إلى ثنائي، تقليل الضوضاء، أو تغيير الحجم إلى 300 dpi.

## نصائح للأداء

- **المعالجة الدفعية:** إضافة العديد من الصور إلى كائن `OcrInput` واحد يقلل من تكلفة تهيئة سياق الـ GPU المتكررة.  
- **التسخين (Warm‑up):** نفّذ عملية تعرف تجريبية واحدة بعد بدء تشغيل JVM؛ الاستدعاء الأول يتضمن زمن تهيئة برنامج التشغيل.  
- **إدارة الذاكرة:** حرّر كائنات `OcrInput` الكبيرة (`ocrInput.clear()`) بعد الانتهاء لتحرير ذاكرة الـ GPU.  

## الخلاصة

أنت الآن تعرف كيف **تتعرف على نص الصورة** بفعالية باستخدام محرك Aspose OCR الـ GPU في Java، وكيف **استخراج النص من الصورة** بأي لغة مدعومة، وكيف **تحديد معرف جهاز الـ GPU** عند العمل مع بطاقات رسومية متعددة. يجب أن يعمل الكود القابل للتنفيذ أعلاه مباشرةً—فقط استبدل مسارات الترخيص والصورة الخاصة بك.

هل أنت مستعد للخطوة التالية؟ جرّب معالجة مجلد من ملفات PDF الممسوحة، واختبر خيارات `setLanguage` المختلفة، أو اجمع بين OCR ونموذج تعلم آلي للمعالجة اللاحقة. الإمكانيات لا حصر لها، ومكاسب الأداء من تسريع الـ GPU تجعل المشاريع الكبيرة قابلة للتنفيذ.

برمجة سعيدة، ولا تتردد في ترك تعليق إذا واجهت أي صعوبات!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}