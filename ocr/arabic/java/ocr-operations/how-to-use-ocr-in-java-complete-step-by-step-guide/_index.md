---
category: general
date: 2026-02-22
description: كيفية استخدام OCR في جافا لاستخراج النص من الصورة، تحسين دقة OCR، وتحميل
  الصورة لـ OCR مع أمثلة عملية على الشيفرة.
draft: false
keywords:
- how to use OCR
- extract text from image
- improve OCR accuracy
- load image for OCR
- OCR preprocessing
language: ar
og_description: كيفية استخدام OCR في جافا لاستخراج النص من الصورة وتحسين دقة OCR.
  اتبع هذا الدليل للحصول على مثال جاهز للتنفيذ.
og_title: كيفية استخدام OCR في جافا – دليل خطوة بخطوة كامل
tags:
- OCR
- Java
- Image Processing
title: كيفية استخدام OCR في جافا – دليل خطوة بخطوة كامل
url: /ar/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في جافا – دليل كامل خطوة بخطوة

هل احتجت يومًا إلى **how to use OCR** على لقطة شاشة مائلة وتساءلت لماذا يبدو الناتج غير مفهوم؟ لست وحدك. في العديد من التطبيقات الواقعية—مسح الإيصالات، رقمنة النماذج، أو استخراج النص من الميمات—يعتمد الحصول على نتائج موثوقة على بعض الإعدادات البسيطة.

في هذا الدرس سنستعرض **how to use OCR** لاستخراج النص من ملفات *extract text from image*، ونوضح لك كيفية **improve OCR accuracy**، ونظهر الطريقة الصحيحة لـ **load image for OCR** باستخدام مكتبة OCR شائعة لجافا. في النهاية ستحصل على برنامج مستقل يمكنك إدراجه في أي مشروع.

## ما ستتعلمه

- الكود الدقيق الذي تحتاجه لـ **load image for OCR** (بدون تبعيات مخفية).
- أي علامات المعالجة المسبقة تعزز **improve OCR accuracy** ولماذا هي مهمة.
- كيفية قراءة نتيجة OCR وطباعةها على وحدة التحكم.
- المشكلات الشائعة—مثل نسيان تعيين منطقة الاهتمام أو تجاهل تقليل الضوضاء—وكيفية تجنبها.

### المتطلبات المسبقة

- Java 17 أو أحدث (الكود يُترجم مع أي JDK حديث).
- مكتبة OCR توفر الفئات `OcrEngine`، `ImagePreprocessingOptions`، `OcrInput`، و `OcrResult` (على سبيل المثال، الحزمة الوهمية `com.example.ocr` المستخدمة في المقتطف). استبدلها بالمكتبة الفعلية التي تستخدمها.
- صورة عينة (`skewed_noisy.png`) موجودة في مجلد يمكنك الإشارة إليه.

> **نصيحة احترافية:** إذا كنت تستخدم SDK تجاريًا، تأكد من وجود ملف الترخيص في مسار الفئات الخاص بك؛ وإلا سيتسبب المحرك في حدوث خطأ تهيئة.

---

## الخطوة 1: إنشاء مثيل محرك OCR – **how to use OCR** بفعالية

أول شيء تحتاجه هو كائن `OcrEngine`. فكر فيه كالعقل الذي سيفسر البكسلات.

```java
// Step 1: Initialize the OCR engine
import com.example.ocr.OcrEngine;

OcrEngine ocrEngine = new OcrEngine();
```

*لماذا هذا مهم:* بدون محرك لا يوجد لديك سياق لنماذج اللغة أو مجموعات الأحرف أو خوارزميات الصورة. إنشاءه مبكرًا يتيح لك أيضًا إرفاق خيارات المعالجة المسبقة لاحقًا.

---

## الخطوة 2: ضبط معالجة الصورة – **improve OCR accuracy**

المعالجة المسبقة هي الصلصة السرية التي تحول المسح الضوضائي إلى نص نظيف قابل للقراءة آليًا. أدناه نقوم بتمكين تصحيح الميل (deskew)، تقليل الضوضاء عالي المستوى، التباين التلقائي، ومنطقة الاهتمام (ROI) للتركيز على الجزء المناسب من الصورة.

```java
import com.example.ocr.ImagePreprocessingOptions;
import java.awt.Rectangle;

// Step 2: Set up preprocessing to improve OCR accuracy
ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
preprocessing.setDeskewEnabled(true); // Correct image rotation
preprocessing.setNoiseReductionLevel(
        ImagePreprocessingOptions.NoiseReduction.HIGH); // Reduce speckles
preprocessing.setAutoContrastEnabled(true); // Boost contrast
preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600)); // Process a sub‑region only

ocrEngine.setPreprocessingOptions(preprocessing);
```

*لماذا هذا مهم:*  
- **Deskew** يضبط النص المدور، وهو أمر أساسي عند مسح الإيصالات التي ليست مسطحة تمامًا.  
- **Noise reduction** يزيل البكسلات العشوائية التي قد تُفسَّر كحروف.  
- **Auto‑contrast** يوسّع نطاق النغمات، مما يجعل الحروف الخفيفة بارزة.  
- **ROI** يخبر المحرك بتجاهل الحدود غير ذات الصلة، مما يوفر الوقت والذاكرة.

إذا تخطيت أيًا من هذه، فمن المحتمل أن تلاحظ انخفاضًا في نتائج **improve OCR accuracy**.

---

## الخطوة 3: تحميل الصورة لـ OCR – **load image for OCR** بشكل صحيح

الآن نوجه المحرك فعليًا إلى الملف الذي نريد قراءته. يمكن لفئة `OcrInput` قبول صور متعددة، لكن في هذا المثال نبقي الأمور بسيطة.

```java
import com.example.ocr.OcrInput;

// Step 3: Load the image you want to extract text from
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png"); // replace with your real path
```

*لماذا هذا مهم:* يجب أن يكون المسار مطلقًا أو نسبيًا إلى دليل العمل؛ وإلا سيتسبب المحرك في إلقاء استثناء `FileNotFoundException`. أيضًا، لاحظ أن اسم الطريقة `add` يشير إلى إمكانية إضافة عدة صور—مفيد للمعالجة الدفعية.

---

## الخطوة 4: تنفيذ OCR وإخراج النص المعترف به – **how to use OCR** من البداية إلى النهاية

أخيرًا، نطلب من المحرك التعرف على النص وطباعة النتيجة. يحتوي كائن `OcrResult` على السلسلة الخام، درجات الثقة، وبيانات التعريف سطرًا بسطر (إذا احتجتها لاحقًا).

```java
import com.example.ocr.OcrResult;

// Step 4: Run OCR and print the extracted text
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**الناتج المتوقع** (بافتراض أن صورة العينة تحتوي على “Hello, OCR World!”):

```
=== OCR Output ===
Hello, OCR World!
```

إذا كان الناتج مشوشًا، عد إلى الخطوة 2 وعدل خيارات المعالجة المسبقة—ربما خفّض مستوى تقليل الضوضاء أو عدّل مستطيل ROI.

---

## مثال كامل قابل للتنفيذ

فيما يلي برنامج جافا كامل يمكنك نسخه ولصقه في ملف باسم `OcrDemo.java`. يجمع جميع الخطوات التي ناقشناها.

```java
// OcrDemo.java – A complete, runnable example showing how to use OCR in Java
import com.example.ocr.OcrEngine;
import com.example.ocr.ImagePreprocessingOptions;
import com.example.ocr.OcrInput;
import com.example.ocr.OcrResult;
import java.awt.Rectangle;

public class OcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing (this is the key to improve OCR accuracy)
        ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
        preprocessing.setDeskewEnabled(true);
        preprocessing.setNoiseReductionLevel(
                ImagePreprocessingOptions.NoiseReduction.HIGH);
        preprocessing.setAutoContrastEnabled(true);
        preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600));
        ocrEngine.setPreprocessingOptions(preprocessing);

        // 3️⃣ Load the image you want to extract text from
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace the path with your own image location
        ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png");

        // 4️⃣ Run the OCR engine and print the result
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

احفظ الملف، قم بتجميعه باستخدام `javac OcrDemo.java`، وشغّله بـ `java OcrDemo`. إذا تم إعداد كل شيء بشكل صحيح، سترى النص المستخرج مطبوعًا على وحدة التحكم.

---

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| **ماذا لو كانت صورتي بصيغة JPEG؟** | طريقة `OcrInput.add()` تقبل أي صيغة نقطية مدعومة—PNG، JPEG، BMP، TIFF. فقط غيّر امتداد الملف في المسار. |
| **هل يمكنني معالجة صفحات متعددة في آن واحد؟** | بالطبع. استدعِ `ocrInput.add()` لكل ملف، ثم مرّر نفس `ocrInput` إلى `recognize()`. سيعيد المحرك `OcrResult` متسلسل. |
| **ماذا لو كانت نتيجة OCR فارغة؟** | تحقق مرة أخرى أن ROI يحتوي فعليًا على نص. أيضًا تأكد من أن `setDeskewEnabled(true)` مفعّل؛ دوران 90° سيجعل المحرك يظن أن الصورة فارغة. |
| **كيف أغيّر نموذج اللغة؟** | معظم المكتبات توفر طريقة `setLanguage(String)` في `OcrEngine`. استدعها قبل `recognize()`، مثال: `ocrEngine.setLanguage("eng")`. |
| **هل هناك طريقة للحصول على درجات الثقة؟** | نعم، غالبًا ما يوفر `OcrResult` طريقة `getConfidence()` لكل سطر أو لكل حرف. استخدمها لتصفية النتائج ذات الثقة المنخفضة. |

## الخلاصة

لقد غطينا **how to use OCR** في جافا من البداية إلى النهاية: إنشاء المحرك، ضبط المعالجة المسبقة لـ **improve OCR accuracy**، تحميل الصورة بشكل صحيح لـ **load image for OCR**، وأخيرًا طباعة النص المستخرج. مقتطف الكود الكامل جاهز للتنفيذ، وتوضح الشروحات السبب وراء كل سطر.

هل أنت مستعد للخطوة التالية؟ جرّب تغيير مستطيل ROI للتركيز على أجزاء مختلفة من الصورة، جرب `NoiseReduction.MEDIUM`، أو دمج الناتج في ملف PDF قابل للبحث. يمكنك أيضًا استكشاف مواضيع ذات صلة مثل **extract text from image** باستخدام خدمات السحابة، أو معالجة آلاف الملفات دفعةً باستخدام طابور متعدد الخيوط.

هل لديك المزيد من الأسئلة حول OCR أو معالجة الصور أو دمج جافا؟ اترك تعليقًا، وبرمجة سعيدة! 

![مثال على كيفية استخدام OCR](/images/ocr-demo.png "كيفية استخدام OCR – مثال جافا يوضح المعالجة المسبقة والنتيجة")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}