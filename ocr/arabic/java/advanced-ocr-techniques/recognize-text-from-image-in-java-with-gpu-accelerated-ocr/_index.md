---
category: general
date: 2026-06-19
description: التعرف على النص من الصورة باستخدام دليل OCR بلغة Java – اكتشف OCR المدعوم
  بتقنية GPU واستخراج النص بسرعة من ملفات PNG.
draft: false
keywords:
- recognize text from image
- extract text from png
- how to recognize text
- gpu accelerated ocr
- java ocr tutorial
language: ar
og_description: التعرف على النص من الصورة في جافا مع تسريع GPU. يوضح هذا الدرس كيفية
  استخراج النص من ملف PNG باستخدام Aspose OCR.
og_title: التعرف على النص من الصورة في جافا – دليل OCR المدعوم بتقنية GPU
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: recognize text from image using a Java OCR tutorial – discover GPU
    accelerated OCR and quickly extract text from png files.
  headline: recognize text from image in Java with GPU‑accelerated OCR
  type: TechArticle
- description: recognize text from image using a Java OCR tutorial – discover GPU
    accelerated OCR and quickly extract text from png files.
  name: recognize text from image in Java with GPU‑accelerated OCR
  steps:
  - name: 1. *What if my image is a JPEG or TIFF?*
    text: The same `recognizeImage` call works for JPEG, BMP, TIFF, and even PDF.
      No code change needed—just pass the correct file path.
  - name: 2. *Can I process multiple images in a loop?*
    text: Absolutely. Create the `OcrEngine` once, then call `recognizeImage` repeatedly.
      Re‑using the engine saves memory and keeps the GPU context alive.
  - name: 3. *My GPU isn’t detected—what gives?*
    text: Make sure you have a recent graphics driver installed. Aspose OCR supports
      CUDA 11+ and OpenCL 2.0+. If the driver is missing, the engine automatically
      falls back to CPU, which is slower but still functional.
  - name: 4. *How do I improve accuracy on noisy scans?*
    text: 'Pre‑process the image: increase contrast, apply binarization, or use the
      `PreprocessOptions` class that Aspose provides. Example:'
  - name: 5. *Is there a way to get bounding boxes for each word?*
    text: Yes—`OcrResult` contains a collection of `OcrRegion` objects. Iterate over
      them to retrieve coordinates, useful for highlighting text in UI.
  type: HowTo
tags:
- OCR
- Java
- GPU
title: التعرف على النص من الصورة في جافا باستخدام OCR المعجل بالمعالج الرسومي
url: /ar/java/advanced-ocr-techniques/recognize-text-from-image-in-java-with-gpu-accelerated-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من صورة في Java مع OCR معزز بالـ GPU

هل تساءلت يومًا كيف **تتعرف على النص من صورة** دون كتابة آلاف السطور من الشيفرة؟ لست وحدك—المطورون يسألون باستمرار، *“كيف يمكن التعرف على النص* في صورة بكفاءة؟* الخبر السار هو أن Aspose OCR يوفر لك محركًا جاهزًا يمكنه حتى الاستفادة من وحدة معالجة الرسومات الخاصة بك، محولًا مهمة المعالج البطيئة إلى عملية سريعة كالبرق.  

في هذا **java ocr tutorial** سنستعرض كل خطوة، من الترخيص إلى طباعة السلسلة النهائية، وسنظهر لك أيضًا كيفية **extract text from png** ملفات ببضع أسطر فقط. في النهاية ستحصل على برنامج قابل للتنفيذ يوضح **gpu accelerated ocr** عمليًا، بالإضافة إلى مجموعة من النصائح التي يمكنك تطبيقها على صيغ صور أخرى.

## ما ستحتاجه

- Java 17 (أو أي JDK حديث) مثبت ومُعّين `JAVA_HOME`.
- ملف ترخيص Aspose OCR for Java (`Aspose.OCR.lic`). النسخة التجريبية المجانية تعمل، لكن الترخيص المناسب يزيل علامة التقييم.
- صورة PNG عالية الدقة تريد اختبارها، مثال `sample-highres.png`.
- Maven أو Gradle لجلب تبعية Aspose OCR (سنظهر مقتطف Maven).

هذا كل شيء—لا مكتبات أصلية إضافية، ولا إعداد أدوات CUDA. الـ SDK يكتشف الـ GPU تلقائيًا ويتولى الأعمال الثقيلة نيابةً عنك.

## الخطوة 1: إضافة Aspose OCR إلى مشروعك

إذا كنت تستخدم Maven، أضف هذا إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

محبو Gradle يمكنهم إضافة:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

> **نصيحة احترافية:** حافظ على تحديث رقم الإصدار؛ الإصدارات الأحدث تحسن اكتشاف الـ GPU وتضيف حزم اللغات.

## الخطوة 2: تطبيق ترخيص Aspose OCR

الترخيص هو أول شيء يتحقق منه الـ SDK، لذا قم به في بداية `main`. إذا تخطيت هذه الخطوة سيعمل المحرك في وضع التقييم ويضيف علامة مائية إلى الناتج.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // Apply your Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

لاحظ كيف أن الشيفرة صغيرة—سطران فقط، لكنها تفتح مجموعة الميزات الكاملة، بما في ذلك **gpu accelerated ocr**.

## الخطوة 3: تمكين تسريع الـ GPU

كائن `Device` داخل `OcrEngine` يعرف ما إذا كان هناك GPU متوافق. ضبط `useGpu` على `true` يخبر المحرك باكتشاف أفضل جهاز تلقائيًا (CUDA، OpenCL، أو الرجوع إلى CPU).

```java
        // Create the OCR engine and turn on GPU support
        OcrEngine engine = new OcrEngine();
        engine.getDevice().setUseGpu(true);
```

إذا لم يكن لجهازك GPU، فإن الاستدعاء غير ضار—المحرك يبقى ببساطة على CPU. هذا يجعل المقتطف قابلًا للنقل بين الحواسيب المحمولة والخوادم.

## الخطوة 4: اختيار لغة التعرف

يمكنك اختيار أي لغة يدعمها Aspose OCR. بالنسبة لمعظم العروض التجريبية الإنجليزية كافية، لكن الـ API يجعل من السهل التحويل إلى الفرنسية أو الألمانية أو حتى الصينية.

```java
        // Set the language (English in this example)
        engine.setLanguage(Language.English);
```

> **لماذا اللغة مهمة؟** نماذج OCR يتم تدريبها لكل لغة؛ اختيار اللغة الصحيحة يعزز الدقة، خاصةً على الأحرف ذات العلامات.

## الخطوة 5: التعرف على النص من صورة

الآن نصل إلى جوهر الموضوع—**recognize text from image**. الطريقة `recognizeImage` تقبل مسار ملف (أو `InputStream`) وتعيد `OcrResult` يحتوي على السلسلة الخام.

```java
        // Recognize text from a PNG file
        OcrResult result = engine.recognizeImage("YOUR_DIRECTORY/sample-highres.png");
```

نظرًا لأننا نتعامل مع PNG، يوضح هذا السطر أيضًا كيفية **extract text from png** دون أي خطوات تحويل إضافية. الـ SDK يتعامل داخليًا مع فك تشفير PNG، لذا لا تحتاج للقلق بشأن `ImageIO`.

## الخطوة 6: إخراج النص المعترف به

أخيرًا، اطبع النتيجة إلى وحدة التحكم أو مررها إلى خدمة أخرى. الطريقة `getText()` تُعيد `String` نصًا عاديًا.

```java
        // Print the extracted text
        System.out.println(result.getText());
    }
}
```

تشغيل البرنامج يجب أن يعرض الأحرف الموجودة في `sample-highres.png`. إذا كانت الصورة واضحة وكانت اللغة مطابقة، سترى نسخة تقريبًا مثالية.

## مثال كامل يعمل

بجمع كل ذلك معًا، إليك الفئة الكاملة الجاهزة للتنفيذ:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply the Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // 2️⃣ Create OCR engine & enable GPU acceleration
        OcrEngine engine = new OcrEngine();
        engine.getDevice().setUseGpu(true);

        // 3️⃣ Set the language for recognition
        engine.setLanguage(Language.English);

        // 4️⃣ Recognize text from image (PNG in this case)
        OcrResult result = engine.recognizeImage("YOUR_DIRECTORY/sample-highres.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

**المخرجات المتوقعة** (بافتراض أن PNG يحتوي على “Hello, World!”):

```
=== Extracted Text ===
Hello, World!
```

إذا ظهرت النتيجة مشوشة، تحقق مرة أخرى من جودة الصورة وإعداد اللغة.

## أسئلة شائعة وحالات خاصة

### 1. *ماذا لو كانت صورتي JPEG أو TIFF؟*  
نفس استدعاء `recognizeImage` يعمل مع JPEG، BMP، TIFF، وحتى PDF. لا حاجة لتغيير الشيفرة—فقط مرّر مسار الملف الصحيح.

### 2. *هل يمكنني معالجة صور متعددة في حلقة؟*  
بالطبع. أنشئ `OcrEngine` مرة واحدة، ثم استدعِ `recognizeImage` بشكل متكرر. إعادة استخدام المحرك يوفر الذاكرة ويحافظ على سياق الـ GPU نشطًا.

```java
String[] files = {"img1.png", "img2.png"};
for (String f : files) {
    OcrResult r = engine.recognizeImage(f);
    System.out.println(r.getText());
}
```

### 3. *لم يتم اكتشاف الـ GPU الخاص بي—ماذا يحدث؟*  
تأكد من تثبيت برنامج تشغيل رسومات حديث. Aspose OCR يدعم CUDA 11+ و OpenCL 2.0+. إذا كان برنامج التشغيل مفقودًا، فإن المحرك يعود تلقائيًا إلى CPU، وهو أبطأ لكنه لا يزال يعمل.

### 4. *كيف أحسن الدقة في المسحات الضوضائية؟*  
قم بتمهيد الصورة مسبقًا: زيادة التباين، تطبيق التثن binary، أو استخدام فئة `PreprocessOptions` التي توفرها Aspose. مثال:

```java
engine.getPreprocessOptions().setAutoContrast(true);
engine.getPreprocessOptions().setDenoise(true);
```

### 5. *هل هناك طريقة للحصول على مربعات الإحاطة لكل كلمة؟*  
نعم—`OcrResult` يحتوي على مجموعة من كائنات `OcrRegion`. قم بالتكرار عليها لاسترجاع الإحداثيات، مفيد لتسليط الضوء على النص في واجهة المستخدم.

```java
for (OcrRegion region : result.getRegions()) {
    System.out.println(region.getText() + " → " + region.getBoundingBox());
}
```

## نصائح الأداء لـ OCR معزز بالـ GPU

- **معالجة دفعات:** قدم دفعة من الصور إلى المحرك قبل استدعاء `flush()`؛ هذا يقلل من عبء إطلاق نواة الـ GPU.
- **حجم الصورة:** الـ GPUs تفضل أبعادًا بقوة اثنين. تغيير حجم الصور الكبيرة إلى أقرب 1024×1024 (مع الحفاظ على نسبة الأبعاد) يمكن أن يوفر بضعة مليثانية لكل استدعاء.
- **إدارة الذاكرة:** استدعِ `engine.dispose()` عند الانتهاء، خاصةً في الخدمات الطويلة التشغيل، لتحرير ذاكرة الـ GPU.

## الخطوات التالية

الآن بعد أن يمكنك **recognize text from image** و **extract text from png** باستخدام **gpu accelerated ocr**، فكر في استكشاف:

- **OCR متعدد اللغات** (`engine.setLanguage(Language.Multilingual)`) للتطبيقات العالمية.
- **استخراج نص PDF** باستخدام `engine.recognizePdf`.
- **دمج مع Spring Boot** لإنشاء نقطة نهاية HTTP تقبل تحميل الصور وتعيد JSON بالنص المعترف به.

هذه الإضافات تبنى مباشرةً على المفاهيم التي تم تغطيتها في هذا **java ocr tutorial**، مما يتيح لك تحويل عرض بسيط على وحدة التحكم إلى خدمة كاملة المميزات.

---

*برمجة سعيدة! إذا واجهت مشكلة، اترك تعليقًا أدناه—سأكون سعيدًا بمساعدتك للحصول على أقصى استفادة من Aspose OCR وتسريع الـ GPU.*

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [التعرف على نص الصورة باستخدام Aspose OCR – دليل OCR كامل لـ Java](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [استخراج النص من صورة Java باستخدام وضع اكتشاف المناطق في Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [كيفية التعرف على نص الصورة باستخدام اللغة مع Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}