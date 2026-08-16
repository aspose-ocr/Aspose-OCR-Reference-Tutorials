---
category: general
date: 2026-04-26
description: تعلم كيفية التعرف على النص من الصورة باستخدام Aspose OCR مع تسريع GPU
  في Java. يتضمن تعيين حد ذاكرة GPU وتحميل الصورة لخطوات OCR.
draft: false
keywords:
- recognize text from image
- set gpu memory limit
- load image for ocr
- Aspose OCR Java
- GPU acceleration OCR
language: ar
og_description: اكتشف كيفية التعرف على النص من الصورة بسرعة باستخدام تقنية Aspose
  OCR المدعومة بوحدة معالجة الرسوميات في جافا. دليل خطوة بخطوة لتحديد حد ذاكرة وحدة
  معالجة الرسوميات وتحميل الصورة للتعرف الضوئي على الأحرف.
og_title: التعرف على النص من الصورة باستخدام GPU Aspose OCR (Java)
tags:
- OCR
- Java
- GPU
- Aspose
title: التعرف على النص من الصورة باستخدام GPU Aspose OCR (Java)
url: /ar/java/advanced-ocr-techniques/recognize-text-from-image-with-gpu-aspose-ocr-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة باستخدام GPU Aspose OCR (Java)

هل احتجت يومًا إلى **التعرف على النص من الصورة** بسرعة في خلفية Java؟ مع تسريع GPU في Aspose OCR يمكنك تقليل الثواني المستغرقة في كل عملية مسح — لا مزيد من الانتظار حتى يطحن المعالج المركزي ميغابايتات من البكسلات. في هذا الدرس سنستعرض كيفية تشغيل GPU، واختيارياً **تحديد حد ذاكرة GPU**، وأخيرًا **تحميل الصورة للـ OCR** للحصول على سلسلة نصية نظيفة في بضع أسطر من الشيفرة فقط.

سنغطي كل ما تحتاجه لتشغيل العرض التجريبي على بطاقة تدعم CUDA، نشرح لماذا كل إعداد مهم، ونظهر لك مثالًا كاملًا جاهزًا للتنفيذ. بنهاية الدرس ستتمكن من دمج OCR المدعوم بـ GPU في أي خدمة Java، سواء كانت خط أنابيب استيعاب مستندات أو خلفية هاتفية في الوقت الحقيقي.

## ما الذي ستحتاجه

- **Java 17** أو أحدث (حزمة Aspose OCR JAR تستهدف JVM الحديثة)  
- **GPU متوافق مع CUDA** بسعة VRAM لا تقل عن 2 GB (العرض التجريبي يحد الاستخدام إلى 1024 MB)  
- مكتبة **Aspose.OCR for Java** (حمّلها من موقع Aspose أو احصل عليها عبر Maven)  
- ملف صورة تريد معالجته — يفضَّل أن يكون مسحًا عالي الدقة أو صورة فوتوغرافية  

لا خدمات خارجية، لا مفاتيح سحابية، مجرد تثبيت محلي. إذا لم يكن لديك GPU بعد، يمكنك تشغيل الشيفرة؛ استدعاء `setUseGpu(true)` سيتحول تلقائيًا إلى CPU.

## الخطوة 1: إضافة Aspose OCR إلى مشروعك والتعرف على النص من الصورة

أولًا، تأكد من أن ملف Aspose OCR JAR موجود في مسار الفئات (classpath). إذا كنت تستخدم Maven، أضف:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
```

بعد توفر المكتبة، أنشئ كائن `OcrEngine`. هذا الكائن هو نقطة الدخول لعمليات **التعرف على النص من الصورة**.

```java
// Step 1: Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

لماذا ننشئ `OcrEngine` أولًا؟ لأنه يحتفظ بجميع إعدادات التعرف (علامات GPU، حزم اللغات، إلخ) ويعزل كل مسح، بحيث يمكنك إعادة استخدام نفس المحرك لعدة صور دون تسرب الذاكرة.

## الخطوة 2: تمكين تسريع GPU واختيارياً **تحديد حد ذاكرة GPU**

تسريع GPU هو المكوّن السري الذي يجعل OCR على نطاق واسع ممكنًا. يتيح لك Aspose تفعيله باستدعاء واحد:

```java
// Step 2: Turn on GPU acceleration (requires a CUDA‑enabled GPU)
ocrEngine.getRecognitionSettings().setUseGpu(true);
```

إذا كان GPU مشتركًا مع أحمال عمل أخرى، قد ترغب في تقييد مقدار VRAM الذي يمكن للمحرك استهلاكه. هنا يأتي دور **تحديد حد ذاكرة GPU**:

```java
// Optional: Limit the amount of GPU memory the engine may use (in MB)
ocrEngine.getRecognitionSettings().setGpuMemoryLimit(1024);
```

تحديد حد للذاكرة يمنع حدوث أعطال نفاد الذاكرة عند معالجة العديد من الصور عالية الدقة بشكل متوازي. القيمة بالمغابايت، لذا `1024` تعني “استخدام ما لا يزيد عن 1 GB من VRAM”.

> **نصيحة احترافية:** على بطاقة سعة 4 GB، الحد 2 GB عادةً ما يكون نقطة آمنة؛ يمكنك تجربة قيم أعلى إذا لاحظت أن GPU يبقى غير مستخدم.

## الخطوة 3: **تحميل الصورة للـ OCR** – إشارة المحرك إلى ملفك

الآن بعد أن أصبح المحرك جاهزًا، علينا إخبارها أي صورة يجب مسحها. تقبل Aspose مسار ملف، أو `java.io.File`، أو حتى `java.awt.image.BufferedImage`. للتبسيط سنستخدم مسارًا:

```java
// Step 3: Load the high‑resolution image to be processed
ocrEngine.setImage("YOUR_DIRECTORY/high_res_photo.jpg");
```

استبدل `YOUR_DIRECTORY/high_res_photo.jpg` بالموقع الفعلي لصورتك التجريبية. إذا كانت الصورة في مجلد الموارد (resources)، يمكنك استخدام `getClass().getResource("/images/sample.png").getPath()` بدلاً من ذلك.

لماذا يهم التحميل؟ يقوم المحرك بخطوة ما قبل المعالجة (إزالة الميل، التثنيم) التي تعتمد بشكل كبير على GPU. توفير ملف نظيف وعالي الدقة يسمح للـ GPU بالعمل بكفاءة ويحسّن دقة **التعرف على النص من الصورة**.

## الخطوة 4: تشغيل التعرف واستخراج السلسلة النصية

مع تشغيل GPU وتحميل الصورة، يكون الاستدعاء النهائي بسيطًا:

```java
// Step 4: Run the recognition and retrieve the extracted text
String extractedText = ocrEngine.recognize().getText();
```

طريقة `recognize()` تحجب التنفيذ حتى ينتهي الـ GPU، ثم تُعيد `getText()` سلسلة `String` عادية. تحت الغطاء، يستخدم Aspose نموذج تعلم عميق يعمل على نوى CUDA، لذا عادةً ما تكون الكمون جزءًا صغيرًا من ما يتطلبه OCR على CPU فقط.

## الخطوة 5: إظهار النتيجة

لنطبع مخرجات OCR إلى وحدة التحكم لتتحقق من أنها تعمل:

```java
// Step 5: Output the GPU‑accelerated OCR result
System.out.println("GPU‑accelerated result:\n" + extractedText);
```

إذا تم توصيل كل شيء بشكل صحيح، ستظهر النصوص المستخرجة فورًا. على بطاقة RTX 2060 متوسطة، تُعالج صورة بحجم 3000 × 2000 px في أقل من ثانية.

![recognize text from image using GPU Aspose OCR](/images/gpu-ocr-demo.png "GPU‑accelerated OCR demo")

*نص بديل للصورة:* **التعرف على النص من الصورة** – لقطة شاشة لمخرجات وحدة التحكم بعد OCR باستخدام GPU.

## النتيجة المتوقعة

تشغيل البرنامج الكامل على إيصال تجريبي يعطي شيء مشابه لـ:

```
GPU‑accelerated result:
Item      Qty   Price
Apple      2    $1.20
Banana     5    $0.75
Total          $3.75
```

النص الفعلي سيختلف بناءً على الصورة المصدر، لكن الشكل أعلاه يوضح أن المحرك يستخرج فواصل الأسطر والأرقام بشكل صحيح.

## المشكلات الشائعة والنصائح العملية

| المشكلة | السبب | طريقة الإصلاح |
|---------|-------|----------------|
| **GPU غير مكتشف** | نقص برنامج تشغيل CUDA أو نسخة JAR غير متوافقة | ثبّت أحدث برنامج تشغيل NVIDIA، تحقق من عمل `nvidia-smi`، واستخدم Aspose OCR 23.12 أو أحدث |
| **خطأ نفاد الذاكرة** | الصورة كبيرة جدًا بالنسبة للـ VRAM المحدود | زد قيمة `setGpuMemoryLimit` أو قلل أبعاد الصورة قبل التحميل |
| **حروف غير مفهومة** | الصورة غير واضحة أو ذات تباين منخفض | عالج مسبقًا باستخدام `ocrEngine.getPreprocessingSettings().setBinarization(true)` |
| **أداء بطيء في أول تشغيل** | تكلفة تهيئة سياق GPU | سخّن المحرك بمعالجة صورة تجريبية صغيرة قبل بدء العمل الفعلي |

تذكّر أن **تحديد حد ذاكرة GPU** اختياري لكن

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}