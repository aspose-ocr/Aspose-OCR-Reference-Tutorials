---
category: general
date: 2026-04-26
description: تعلم كيفية تنفيذ تقنية التعرف الضوئي على الأحرف (OCR) واستخراج النص من
  الصورة باستخدام Aspose OCR. يوضح هذا الدليل كيفية تحميل الصورة للتعرف الضوئي على
  الأحرف، وتمكين الكشف التلقائي عن اللغة، واكتشاف اللغة تلقائيًا في OCR.
draft: false
keywords:
- how to perform OCR
- extract text from image
- load image for OCR
- enable automatic language detection
- auto detect language OCR
language: ar
og_description: كيفية تنفيذ OCR في جافا باستخدام Aspose OCR. تعلم كيفية تحميل الصورة
  للـ OCR، وتمكين الكشف التلقائي عن اللغة، واستخراج النص من الصورة.
og_title: كيفية تنفيذ OCR في جافا – الكشف التلقائي عن اللغة
tags:
- OCR
- Java
- Aspose
title: كيفية تنفيذ OCR في جافا – الكشف التلقائي عن اللغة واستخراج النص
url: /ar/java/advanced-ocr-techniques/how-to-perform-ocr-in-java-auto-detect-language-and-extract/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR في Java – الكشف التلقائي عن اللغة واستخراج النص

هل احتجت يومًا إلى معرفة **كيفية تنفيذ OCR** على صورة تمزج بين الإنجليزية والإسبانية وربما بعض الأحرف اليابانية؟ لست وحدك—المطورون يواجهون هذه العقبة باستمرار عندما يتعين على تطبيقاتهم قراءة النص من المستندات الممسوحة، الإيصالات، أو العلامات متعددة اللغات.  

الخبر السار؟ ببضع أسطر من Java و Aspose OCR يمكنك **تحميل الصورة لـ OCR**، تفعيل **الكشف التلقائي عن اللغة**، واستخراج **النص من الصورة** على الفور دون الحاجة لتخمين اللغة أولاً. في هذا الدرس سنستعرض المثال الكامل القابل للتنفيذ، نشرح لماذا كل خطوة مهمة، ونظهر لك كيفية التحقق من نتيجة **auto detect language OCR**.

> **ما ستحصل عليه**  
> * برنامج Java يعمل يقرأ صورة PNG متعددة اللغات.  
> * معرفة إعدادات OCR الرئيسية التي تجعل كشف اللغة سهلًا.  
> * نصائح للتعامل مع الملفات المفقودة، اللغات غير المدعومة، وتحسينات الأداء.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من أن لديك:

| المتطلب | لماذا يهم |
|-------------|----------------|
| Java 17 (أو أحدث) | Aspose OCR يستهدف JVM الحديثة؛ قد تفتقد الإصدارات القديمة ميزات API. |
| مكتبة Aspose OCR للـ Java (أحدث نسخة) | توفر `OcrEngine` وإمكانيات الكشف التلقائي عن اللغة. |
| ملف صورة (`mixed_lang.png`) يحتوي على نص على الأقل بلغتين | يوضح ميزة **auto detect language OCR**. |
| بيئة تطوير Java IDE أو إعداد سطر أوامر بسيط | لتجميع وتشغيل كود العينة. |

إذا لم تقم بعد بالحصول على ملف JAR الخاص بـ Aspose OCR، احصل عليه من مستودع Maven الرسمي:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- replace with the latest -->
</dependency>
```

## الخطوة 1: إنشاء مثيل محرك OCR – كيفية تنفيذ OCR

أول شيء تقوم به عندما تريد **تنفيذ OCR** هو إنشاء مثيل للمحرك. فكر في `OcrEngine` كالعقل الذي سيحلل الصورة النقطية ويحول البكسلات إلى أحرف.

```java
// Step 1: Initialize the OCR engine
import com.aspose.ocr.*;

public class AutoDetectDemo {
    public static void main(String[] args) throws Exception {

        // Create a fresh OcrEngine object – this is where the magic starts
        OcrEngine ocrEngine = new OcrEngine();
```

> **نصيحة احترافية:** إعادة استخدام نفس `OcrEngine` للعديد من الصور يمكن أن يعزز الأداء لأن المحرك يخزن نماذج اللغة داخليًا.

## الخطوة 2: تمكين الكشف التلقائي عن اللغة – Enable Automatic Language Detection

بشكل افتراضي، يفترض Aspose OCR أن اللغة هي الإنجليزية. للصور متعددة اللغات يجب أن تخبره بـ “تخمين” اللغة لكل كتلة نصية. هذا ما يفعله علم **enable automatic language detection**.

```java
        // Step 2: Turn on auto‑language detection for each region
        ocrEngine.getRecognitionSettings()
                 .setLanguage(OcrLanguage.AUTO_DETECT);
```

لماذا هذا مهم: الآن يقوم المحرك بفحص كل جزء من الصورة، يختار اللغة الأكثر احتمالًا، ويطبق مجموعة الأحرف الصحيحة. بدون ذلك، ستحصل على مخرجات مشوشة للأقسام غير الإنجليزية.

## الخطوة 3: تحميل الصورة لـ OCR – Load Image for OCR

الآن نقوم فعليًا **بتحميل الصورة لـ OCR**. يمكن أن يكون المسار مطلقًا أو نسبيًا؛ فقط تأكد من وجود الملف، وإلا ستواجه `FileNotFoundException`.

```java
        // Step 3: Point the engine at the image that contains mixed‑language text
        ocrEngine.setImage("YOUR_DIRECTORY/mixed_lang.png");
```

> **حالة خاصة:** إذا كانت صورتك موجودة في مجلد الموارد لمشروع Maven، استخدم `getClass().getResource("/mixed_lang.png")` لتجنب المسارات الصلبة.

## الخطوة 4: تشغيل التعرف واستخراج النص من الصورة – Extract Text from Image

مع تكوين المحرك وتحميل الصورة، حان الوقت فعليًا **لتنفيذ OCR**. استدعاء `recognize()` يقوم بالعمل الشاق، بينما `getText()` يُعيد سلسلة `String` بسيطة.

```java
        // Step 4: Execute OCR and fetch the recognized text
        String recognizedText = ocrEngine.recognize().getText();
```

في هذه المرحلة، المكتبة قد نفذت بالفعل **auto detect language OCR** لكل كتلة، لذا فإن المتغير `recognizedText` يحتوي على نص نظيف ومدرك للغة.

## الخطوة 5: عرض النتيجة – Verify Auto‑Detect Language OCR Output

أخيرًا، نطبع النتيجة إلى وحدة التحكم. في تطبيق حقيقي قد تكتبها إلى ملف، قاعدة بيانات، أو تمررها إلى خدمة ترجمة.

```java
        // Step 5: Show the output – you’ll see language tags if you enable them
        System.out.println("Auto‑detected language output:\n" + recognizedText);
    }
}
```

### النتيجة المتوقعة

بافتراض أن `mixed_lang.png` يحتوي على “Hello” (إنجليزي) و “¡Hola!” (إسباني)، سترى شيئًا مثل:

```
Auto‑detected language output:
Hello
¡Hola!
```

إذا فعلت `setShowLanguage(true)` في الإعدادات، سيضيف المحرك قبل كل سطر رمز اللغة، مثل `[en] Hello` و `[es] ¡Hola!`.

## أسئلة شائعة ومشكلات محتملة

### ماذا لو كان مسار الصورة خاطئًا؟

المحرك يرمي `FileNotFoundException`. غلف الاستدعاء بكتلة try‑catch وقدم للمستخدم رسالة ودية:

```java
try {
    ocrEngine.setImage("path/to/image.png");
} catch (FileNotFoundException e) {
    System.err.println("Image not found – check the file path!");
    return;
}
```

### هل يمكنني تحديد اللغات لتسريع الكشف؟

نعم. بدلاً من `AUTO_DETECT`، يمكنك توفير قائمة:

```java
ocrEngine.getRecognitionSettings()
         .setLanguage(new OcrLanguage[]{OcrLanguage.ENGLISH, OcrLanguage.SPANISH});
```

هذا يقلل مساحة البحث ويمكن أن يحسن الأداء على دفعات كبيرة.

### كيف يتعامل **auto detect language OCR** مع النص المكتوب يدويًا؟

Aspose OCR يركز على النص المطبوع. النصوص المكتوبة يدويًا عادةً تحتاج إلى محرك مختلف (مثل Aspose OCR for Handwriting). محاولة إجبار الكشف ستؤدي إلى نتائج سيئة.

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل، جاهز للتجميع والتنفيذ. استبدل `YOUR_DIRECTORY` بالمجلد الفعلي الذي يحتوي على `mixed_lang.png`.

```java
import com.aspose.ocr.*;

public class AutoDetectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine – this is where the magic starts
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable automatic language detection for each text block
        ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.AUTO_DETECT);

        // Step 3: Load the image that contains mixed‑language text
        // Make sure the file exists; otherwise an exception is thrown
        ocrEngine.setImage("YOUR_DIRECTORY/mixed_lang.png");

        // Step 4: Run the recognition process and obtain the extracted text
        String recognizedText = ocrEngine.recognize().getText();

        // Step 5: Display the auto‑detected language output
        System.out.println("Auto‑detected language output:\n" + recognizedText);
    }
}
```

شغّله باستخدام:

```bash
javac -cp "aspose-ocr-23.10.jar" AutoDetectDemo.java
java -cp ".:aspose-ocr-23.10.jar" AutoDetectDemo
```

يجب أن ترى مخرجات وحدة التحكم الموضحة سابقًا.

## توسيع الحل

الآن بعد أن عرفت **كيفية تنفيذ OCR**، فكر في الخطوات التالية:

* **Batch processing** – تكرار عبر مجلد من الصور، وإعادة استخدام نفس مثيل `OcrEngine` للسرعة.
* **Saving results** – كتابة النص المستخرج إلى ملفات `.txt` أو تخزينه في قاعدة بيانات.
* **Post‑processing** – استخدام تعبيرات نمطية لتنظيف فواصل الأسطر أو إزالة الأحرف غير المرغوب فيها.
* **Integration** – تمرير الناتج إلى واجهة برمجة تطبيقات ترجمة (Google Translate، Azure Translator) لتطبيقات متعددة اللغات.

كل من هذه الإضافات لا يزال يعتمد على المفاهيم الأساسية التي غطيناها: تحميل الصورة، تمكين كشف اللغة، واستخراج النص.

## الخلاصة

لقد استعرضنا مثالًا كاملاً من البداية إلى النهاية يوضح **كيفية تنفيذ OCR** في Java مع الكشف التلقائي عن اللغات. باتباع الخطوات الخمس—إنشاء المحرك، تمكين الكشف التلقائي عن اللغة، تحميل الصورة، تشغيل التعرف، وعرض النتائج—يمكنك بثقة **استخراج النص من الصورة** التي تحتوي على عدة أنظمة كتابة.

تذكر، المفتاح للحصول على **auto detect language OCR** سلس هو السماح للمحرك بالقرار لكل كتلة؛ فرض لغة واحدة غالبًا ما يؤدي إلى مخرجات مشوشة. جرب جودة صور مختلفة، قوائم لغات، وتعديلات الأداء لضبط التجربة وفقًا لحالتك الخاصة.

هل لديك سيناريو غير مغطى هنا؟ اترك تعليقًا، ولنحل المشكلة معًا. برمجة سعيدة!  

![how to perform OCR example](/images/ocr-demo.png "Screenshot showing how to perform OCR with Aspose OCR in Java")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}