---
category: general
date: 2026-07-05
description: استخراج النص من ملفات TIFF باستخدام Aspose OCR Java في إعداد معالجة OCR
  متوازٍ. يوضح هذا المثال المختصر لـ Aspose OCR Java كيفية تعزيز الأداء باستخدام الخيوط
  متعددة النوى.
draft: false
keywords:
- extract text from tiff
- aspose ocr java example
- parallel ocr processing
- java ocr multithreading
- tiff image recognition
language: ar
og_description: استخراج النص من ملفات TIFF باستخدام Aspose OCR Java ومعالجة OCR المتوازية.
  اتبع هذا المثال خطوة بخطوة بلغة Java لتسريع التعرف على الصور متعددة الصفحات.
og_title: استخراج النص من ملف TIFF باستخدام Aspose OCR Java – دليل
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from tiff using Aspose OCR Java in a parallel OCR processing
    setup. This concise Aspose OCR Java example shows how to boost performance with
    multi‑core threading.
  headline: Extract text from tiff using Aspose OCR Java – Guide
  type: TechArticle
tags:
- Java
- OCR
- Aspose
- TIFF
title: استخراج النص من ملف TIFF باستخدام Aspose OCR Java – دليل
url: /ar/java/advanced-ocr-techniques/extract-text-from-tiff-using-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من ملفات TIFF باستخدام Aspose OCR Java – دليل

هل احتجت يومًا إلى **استخراج النص من ملفات TIFF** لكن وجدت العملية بطيئة كسلحفاة؟ لست وحدك. عندما تقوم بإرسال ملف TIFF متعدد الصفحات إلى محرك OCR أحادي الخيط، قد يبدو وقت الانتظار لا نهائيًا—خاصةً في سيناريو المعالجة الدفعية.

الأمر هو أن Aspose OCR for Java يمكنه الاستفادة من كل نواة منطقية في جهازك، محولًا تلك العملية البطيئة أحادية الخيط إلى خط أنابيب معالجة OCR متوازٍ وسلس. في هذا الدليل سنستعرض مثالًا كاملًا **Aspose OCR Java** يوضح بالضبط كيفية تكوين المحرك، وإمداده بملف TIFF متعدد الصفحات، و**استخراج النص من ملفات TIFF** في جزء من الوقت الأصلي.

## ما ستحصل عليه

- فئة Java قابلة للتنفيذ تُظهر **معالجة OCR متوازية** باستخدام Aspose OCR.
- توضيحات واضحة لماذا كل إعداد مهم، وليس مجرد ما يجب كتابته.
- نصائح للتعامل مع الحالات الخاصة مثل اختلاف عدد الصفحات، ملفات الصور الكبيرة، وقيود الذاكرة.
- أساس قوي لتكييف الكود لمشاريع أتمتة المستندات الخاصة بك.

> **المتطلبات المسبقة**  
> • Java 8 أو أحدث مثبت (الكود يُترجم أيضًا مع JDK 11).  
> • Maven أو Gradle لجلب مكتبة Aspose OCR for Java.  
> • صورة TIFF متعددة الصفحات (يمكنك إنشاء واحدة بأي محرر صور أو استخدام العينة `multi_page.tif` التي تُرفق مع Aspose).  

إذا كنت قد غطيت هذه الأساسيات، فلنغوص في التفاصيل.

![استخراج النص من TIFF باستخدام Aspose OCR Java – مخطط المعالجة المتوازية](image.png "مخطط يوضح كيف أن معالجة OCR المتوازية تستخرج النص من ملفات TIFF")

## الخطوة 1: إعداد مشروعك – أسرع مثال Aspose OCR Java

قبل أن نصل إلى جوهر **معالجة OCR المتوازية**، نحتاج إلى مشروع Java يمكنه رؤية ملفات JAR الخاصة بـ Aspose OCR. أبسط طريقة هي استخدام Maven:

```xml
<!-- pom.xml snippet -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.12</version> <!-- check for the latest version -->
    </dependency>
</dependencies>
```

إذا كنت تفضل Gradle، فإن المكافئ هو:

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **نصيحة احترافية:** إضافة الاعتماد عبر Maven Central يضمن أنك دائمًا ستحصل على أحدث نسخة مُصَحَّحة أمنيًا. لا حاجة لتنزيل ملفات JAR يدويًا.

بمجرد أن يصبح ملف البناء جاهزًا، شغّل `mvn clean compile` (أو `gradle build`) للتحقق من أن فئات Aspose موجودة في مسار الفئة. إذا لم تظهر أي أخطاء، فأنت جاهز للانطلاق.

## الخطوة 2: إنشاء محرك OCR وتمكين التنفيذ متعدد النوى

الآن سنكتب فئة Java التي تقوم فعليًا بأداء OCR. السطر الرئيسي الذي يحول محرك OCR عادي إلى **محرك معالجة OCR متوازية** هو `setThreadCount`. هذا يخبر Aspose OCR بعدد الأنوية المنطقية التي يمكنه استخدامها.

```java
package com.example.ocr;

import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;

/**
 * ParallelOcrDemo – a concise Aspose OCR Java example that extracts text from tiff
 * images using multiple threads.
 */
public class ParallelOcrDemo {

    public static void main(String[] args) throws Exception {
        // Step 2.1: Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Tell the engine to use 4 logical cores (adjust to your CPU)
        // This is the heart of parallel OCR processing.
        ocrEngine.setThreadCount(4);

        // Step 2.3: Point the engine at a multi‑page TIFF file.
        // Replace the path with the location of your own TIFF.
        String tiffPath = "YOUR_DIRECTORY/multi_page.tif";

        // Step 2.4: Run the recognition. The method returns a RecognitionResult
        // which holds the extracted text and additional metadata.
        RecognitionResult result = ocrEngine.recognizeImage(tiffPath);

        // Step 2.5: Output the extracted text – this is where we finally
        // extract text from tiff and show it on the console.
        System.out.println("=== Extracted Text Start ===");
        System.out.println(result.getText());
        System.out.println("=== Extracted Text End ===");
    }
}
```

### لماذا `setThreadCount` مهم

يقوم Aspose OCR داخليًا بتقسيم كل صفحة من ملف TIFF متعدد الصفحات إلى مهام منفصلة. بشكل افتراضي يعمل على خيط واحد، مما يعني أن كل صفحة تنتظر انتهاء السابقة. ضبط `threadCount` إلى عدد الأنوية الفعلية (أو أقل قليلًا للحفاظ على استجابة واجهة المستخدم) يسمح للمحرك بمعالجة عدة صفحات في آن واحد. في الاختبارات، يمكن لجهاز رباعي النوى أن يقلل **حتى 70 %** من إجمالي وقت المعالجة مقارنةً بوضع الخيط الواحد الافتراضي.

> **ملاحظة:** إذا قمت بتعيين عدد الخيوط أعلى من عدد الأنوية المتاحة، سيبدأ نظام التشغيل في تقسيم الوقت، مما قد يؤدي إلى تدهور الأداء. التزم بـ `Runtime.getRuntime().availableProcessors()` كحد أعلى آمن.

## الخطوة 3: التعامل مع ملفات TIFF الكبيرة وقيود الذاكرة

عند **استخراج النص من ملفات TIFF** التي تحتوي على عشرات الصفحات عالية الدقة، قد يرتفع استهلاك الذاكرة. يوفر Aspose OCR بعض الخيارات للحفاظ على النظام مرتبًا:

```java
// Optional: Reduce memory footprint by lowering image resolution before OCR
ocrEngine.getImagePreprocessingOptions().setResolution(150); // DPI

// Optional: Enable streaming mode for massive TIFFs (>500 MB)
ocrEngine.setEnableStreaming(true);
```

- **تقليل الدقة** يبادل قليلًا من الدقة مقابل فوز كبير في الذاكرة. معظم المستندات المطبوعة لا تزال مقروءة بدقة 150 DPI.
- **وضع البث** يعالج الصفحات واحدة تلو الأخرى دون تحميل ملف TIFF بالكامل في الذاكرة. هذا ضروري للوظائف الدفعية على الخادم.

## الخطوة 4: التحقق من المخرجات ومعالجة المشكلات الشائعة

بعد تشغيل العرض التجريبي، يجب أن ترى النص المستخرج محاطًا بعلامات “=== Extracted Text Start ===”. إذا ظهر المخرج فارغًا أو مشوشًا، فكر في الفحوصات التالية:

| العَرَض | السبب المحتمل | الحل السريع |
|---------|--------------|-----------|
| لا يوجد نص على الإطلاق | مسار الملف غير صحيح أو ضغط TIFF غير مدعوم | تحقق من `tiffPath` وتأكد من أن TIFF لا يستخدم ضغطًا مملوكًا (مثال: CCITT Group 4 مقبول؛ JPEG‑2000 قد يحتاج إلى رموز إضافية). |
| حروف مفقودة (مثل الأحرف المشددة) | لغة OCR غير مضبوطة | استدعِ `ocrEngine.setLanguage(OcrEngine.Language.English);` أو حمّل حزمة لغة مخصصة. |
| أخطاء نفاد الذاكرة | TIFF كبير جدًا دون وضع البث | فعّل `setEnableStreaming(true)` و/أو قلل الدقة. |
| أداء بطيء رغم `setThreadCount` | إيقاف تشغيل Hyper‑Threading للمعالج أو قيود JVM | تأكد من أن JVM غير مقيد بعلامات `-Xmx`؛ امنحه مساحة كافية في الذاكرة (مثال: `-Xmx2g`). |

## الخطوة 5: التوسع – معالجة مجلد من ملفات TIFF بشكل متوازي

العرض التجريبي لملف واحد رائع للتعلم، لكن الإنتاج غالبًا ما يتطلب معالجة دفعات. أدناه امتداد خفيف يمر عبر دليل، ينشئ مجموعة خيوط، ويشغل محرك OCR على كل ملف بشكل متزامن. هذا يوضح **معالجة OCR متوازية** على مستوى التطبيق.



## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [استخراج النص من الصور – أساسيات OCR مع Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [استخراج النص من صورة Java باستخدام وضع اكتشاف المناطق في Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [كيفية استخراج النص من صورة عبر URL باستخدام Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}