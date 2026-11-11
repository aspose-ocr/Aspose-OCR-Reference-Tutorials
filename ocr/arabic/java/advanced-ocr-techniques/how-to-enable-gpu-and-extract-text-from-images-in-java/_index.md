---
category: general
date: 2026-09-16
description: تعرّف على كيفية تمكين وحدة معالجة الرسومات (GPU) للحصول على OCR أسرع
  في Java، واستخراج النص من ملفات الصور وتحويل الصورة إلى نص باستخدام Aspose OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize text from image
- extract text from image
- how to perform ocr
- convert image to text
language: ar
lastmod: 2026-09-16
og_description: كيفية تمكين وحدة معالجة الرسومات (GPU) للتعرف الضوئي على الحروف (OCR)
  في جافا، التعرف على النص من ملفات الصور وتحويل الصورة إلى نص باستخدام Aspose OCR
  – دليل كامل خطوة بخطوة.
og_image_alt: Screenshot showing Java code that enables GPU for OCR and extracts text
  from an image
og_title: كيفية تمكين وحدة معالجة الرسومات واستخراج النص من الصور في جافا
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: Learn how to enable GPU for faster OCR in Java, recognize text from
    image files and convert image to text using Aspose OCR.
  headline: How to enable GPU and extract text from images in Java
  type: TechArticle
- description: Learn how to enable GPU for faster OCR in Java, recognize text from
    image files and convert image to text using Aspose OCR.
  name: How to enable GPU and extract text from images in Java
  steps:
  - name: '**Pre‑processing** – de‑skew, binarize, and enhance contrast (GPU‑accelerated).'
    text: '**Pre‑processing** – de‑skew, binarize, and enhance contrast (GPU‑accelerated).'
  - name: '**Segmentation** – locate text lines, words, and characters.'
    text: '**Segmentation** – locate text lines, words, and characters.'
  - name: '**Classification** – match each character against the built‑in language
      model.'
    text: '**Classification** – match each character against the built‑in language
      model.'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: كيفية تمكين وحدة معالجة الرسومات واستخراج النص من الصور في جافا
url: /ar/java/advanced-ocr-techniques/how-to-enable-gpu-and-extract-text-from-images-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين GPU واستخراج النص من الصور في Java

إذا كنت بحاجة إلى **كيفية تمكين GPU** للتعرف الضوئي على الحروف، يوضح لك هذا الدليل الخطوات الدقيقة. من خلال تشغيل تسريع GPU يمكنك **التعرف على النص من الصورة** بسرعة أعلى بضع مرات مقارنةً بالمعالجة باستخدام المعالج المركزي فقط. يستخدم المثال Aspose OCR for Java، لكن المفاهيم تنطبق على أي مكتبة OCR متوافقة مع GPU.

في هذا البرنامج التعليمي ستتعلم كيفية:

* تمكين تسريع GPU في محرك OCR.  
* تحميل صورة و **استخراج النص من الصورة**.  
* **تحويل الصورة إلى نص** ببضع أسطر من الشيفرة فقط.  

لا توجد خدمات خارجية مطلوبة — كل شيء يعمل محليًا على جهازك. بيئة تطوير Java الأساسية ومكتبة Aspose OCR for Java هما المتطلبان الوحيدان.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

| المتطلبات | الإصدار / التفاصيل |
|-------------|------------------|
| Java Development Kit (JDK) | 8 أو أحدث |
| Maven أو Gradle (لإدارة الاعتمادات) | أي نسخة حديثة |
| GPU مع دعم CUDA (اختياري لكن يُنصح به) | NVIDIA GPU مع برنامج تشغيل ≥ 450 |
| Aspose OCR for Java library | 23.9 أو أحدث (تحميل من موقع Aspose) |

إذا لم يكن لديك GPU، لا يزال الكود يعمل؛ سيعمل فقط على المعالج المركزي.

## الخطوة 1: إضافة Aspose OCR إلى مشروعك

لـ Maven، أضف الاعتماد التالي إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

لـ Gradle، ضع هذا في `build.gradle`:

```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

هذه الإدخالات تجلب محرك OCR والملفات الثنائية الأصلية لتسريع GPU تلقائيًا.

## الخطوة 2: كيفية تمكين GPU لمحرك OCR

المهمة الأساسية هي إخبار `OcrEngine` باستخدام GPU. Aspose OCR يوفّر علمًا بسيطًا:

```java
// Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Enable GPU acceleration – this is the “how to enable gpu” step
ocrEngine.setGpuEnabled(true);
```

**لماذا هذا مهم:** عند استدعاء `setGpuEnabled(true)`، تقوم المكتبة بتحميل نوى مبنية على CUDA تُوازي مرحلة ما قبل معالجة الصورة وتقسيم الأحرف. على بطاقة NVIDIA حديثة، يمكنك ملاحظة تحسينات في السرعة تتراوح بين 2‑4× مقارنةً بالمسار الافتراضي للمعالج المركزي.

> **نصيحة محترف:** تحقق من اكتشاف GPU الخاص بك عن طريق تشغيل `SystemInfo.isCudaSupported()` قبل تفعيل العلم. إذا أعاد الأسلوب `false`، سيتراجع المحرك تلقائيًا إلى المعالج المركزي.

## الخطوة 3: تحميل الصورة التي تريد معالجتها

يمكنك إمداد محرك OCR بأي تنسيق صورة يدعمه Aspose (JPEG, PNG, BMP, TIFF, إلخ). إليك كيفية تحميل ملف JPEG:

```java
// Load the image that contains the text to be recognized
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

**حالة خاصة:** إذا كانت الصورة كبيرة (أكثر من 5 ميغابايت) فكر في تصغير حجمها أولاً لتقليل استهلاك الذاكرة. يعمل محرك OCR بأفضل شكل مع الصور بحوالي 300 dpi.

## الخطوة 4: تنفيذ OCR و **التعرف على النص من الصورة**

الآن بعد أن تم تكوين المحرك وتحميل الصورة، يمكنك تشغيل عملية التعرف:

```java
// Execute OCR – this is the core “how to perform ocr” step
String recognizedText = ocrEngine.recognize();
```

طريقة `recognize()` تُعيد `String` نصًا عاديًا. داخليًا، يمر المحرك بعدة مراحل:

1. **ما قبل المعالجة** – تصحيح الميل، تحويل إلى ثنائي، وتعزيز التباين (مُسرّع بـ GPU).  
2. **التقسيم** – تحديد خطوط النص، الكلمات، والأحرف.  
3. **التصنيف** – مطابقة كل حرف مع نموذج اللغة المدمج.

نظرًا لتفعيل GPU، تستفيد الخطوتان 1 و2 أكثر من التنفيذ المتوازي.

## الخطوة 5: عرض أو تخزين النص المستخرج

أخيرًا، قم بإخراج النتيجة إلى وحدة التحكم، ملف، أو أي معالج لاحق:

```java
// Show the extracted text – this completes the “convert image to text” flow
System.out.println("Recognized text:\n" + recognizedText);

// Optional: write the text to a file
Files.write(Paths.get("output.txt"), recognizedText.getBytes(StandardCharsets.UTF_8));
```

**الناتج النموذجي** (لصورة تجريبية تحتوي على “Hello World”):

```
Recognized text:
Hello World
```

إذا فشل OCR في اكتشاف أي أحرف، سيكون `recognizedText` سلسلة فارغة. في هذه الحالة، تحقق مرة أخرى من جودة الصورة أو عطل GPU للمقارنة بين الأداء.

## معالجة المشكلات الشائعة

| المشكلة | السبب | الحل |
|-------|-------|-----|
| **لم يتم اكتشاف GPU** | نقص برنامج تشغيل CUDA أو GPU غير مدعوم | قم بتثبيت أحدث برنامج تشغيل NVIDIA وتحقق باستخدام `nvidia-smi`. |
| **أحرف غير صحيحة** | تباين منخفض أو خلفية مشوشة | قم بعملية ما قبل المعالجة للصورة (مثل زيادة التباين) قبل إمدادها للمحرك. |
| **خطأ نفاد الذاكرة** | صور كبيرة جدًا على ذاكرة GPU محدودة | صغّر الصورة إلى ≤ 2000 px عرض أو عالجها على شكل مربعات. |
| **عدم توافق اللغة** | نموذج اللغة الافتراضي هو الإنجليزية لكن النص بلغة أخرى | استدعِ `ocrEngine.setLanguage(OcrLanguage.SPANISH)` (أو التعداد المناسب) قبل `recognize()`. |

## مثال كامل قابل للتنفيذ

فيما يلي فئة Java مستقلة تجمع جميع الخطوات معًا. احفظها باسم `GpuEnabledOcrExample.java`، عدل مسار الصورة، وشغّلها باستخدام `javac`/`java` أو عبر بيئة التطوير المتكاملة الخاصة بك.

```java
import com.aspose.ocr.*;
import java.nio.file.*;

public class GpuEnabledOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Turn on GPU acceleration for faster processing
        // This is the core "how to enable gpu" call
        ocrEngine.setGpuEnabled(true);

        // Optional sanity check – ensures CUDA is available
        if (!SystemInfo.isCudaSupported()) {
            System.out.println("CUDA not detected. Falling back to CPU.");
        }

        // Step 3: Load the image that contains the text to be recognized
        // Replace with the absolute path to your image file
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Perform the OCR operation and obtain the recognized text
        // This answers "how to perform ocr" and "recognize text from image"
        String recognizedText = ocrEngine.recognize();

        // Step 5: Display the extracted text – completes "convert image to text"
        System.out.println("Recognized text:\n" + recognizedText);

        // (Optional) Save the result to a text file
        Path output = Paths.get("recognized_output.txt");
        Files.write(output, recognizedText.getBytes());
        System.out.println("Text saved to " + output.toAbsolutePath());
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج يطبع النص المستخرج إلى وحدة التحكم ويكتب نفس المحتوى في `recognized_output.txt`. مع تمكين GPU، يكون إجمالي زمن التنفيذ لصورة بدقة 2 MP عادةً أقل من 200 ms على NVIDIA RTX 3060، مقارنةً بـ ~500 ms على المعالج المركزي فقط.

## الخلاصة

أنت الآن تعرف **كيفية تمكين GPU** لـ Aspose OCR في Java، **التعرف على النص من الصورة**، و**تحويل الصورة إلى نص** ببضع أسطر برمجية بسيطة. من خلال الاستفادة من تسريع GPU تحصل على معالجة أسرع، وهو أمر أساسي للتطبيقات الدفعية أو ذات الوقت الحقيقي مثل مسح الفواتير، معالجة الإيصالات، ورقمنة المستندات.

**الخطوات التالية**

* جرّب نماذج لغات مختلفة (`ocrEngine.setLanguage`) لت **استخراج النص من الصورة** باللغات الفرنسية، الألمانية، أو الصينية.  
* دمج مخرجات OCR مع Apache Tika لفهرسة المحتوى المستخرج تلقائيًا.  
* استكشاف تدفق ملفات PDF الكبيرة صفحة بصفحة إذا كنت بحاجة إلى **التعرف على النص من الصورة** داخل إطار PDF.

لا تتردد في تعديل العينة، دمجها في خدماتك الخاصة، ومشاركة نتائجك. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Read Text from an Image in Java Using Aspose OCR – Complete Guide](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [image to text java: Convert Image to Text with Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}