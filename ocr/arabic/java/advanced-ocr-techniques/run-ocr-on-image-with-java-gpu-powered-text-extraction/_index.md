---
category: general
date: 2026-03-07
description: تشغيل OCR على الصورة باستخدام Java. تعلم كيفية التعرف على النص من PNG،
  استخراج النص من الفاتورة، وتحميل الصورة للـ OCR مع مثال كامل للـ OCR باستخدام Java.
draft: false
keywords:
- run OCR on image
- recognize text from png
- extract text from receipt
- java OCR example
- load image for OCR
language: ar
og_description: تشغيل OCR على الصورة باستخدام جافا. يوضح هذا الدليل كيفية التعرف على
  النص من ملف PNG، استخراج النص من الفاتورة، وتحميل الصورة للـ OCR باستخدام مثال كامل
  لـ OCR بجافا.
og_title: تشغيل OCR على الصورة باستخدام Java – استخراج النص باستخدام GPU
tags:
- OCR
- Java
- GPU
- Image Processing
title: تشغيل OCR على الصورة باستخدام Java – استخراج النص باستخدام GPU
url: /ar/java/advanced-ocr-techniques/run-ocr-on-image-with-java-gpu-powered-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تشغيل OCR على صورة باستخدام Java – استخراج نص مدعوم بالـ GPU

هل احتجت يومًا إلى **run OCR on image** ملفات ولكن لم تكن متأكدًا من أين تبدأ في Java؟ لست وحدك—العديد من المطورين يواجهون نفس المشكلة عندما يحاولون استخراج النص من إيصال ممسوح ضوئيًا أو لقطة شاشة PNG.  

في هذا الدرس سنرشدك خلال **complete Java OCR example** لا يقتصر فقط على **recognizes text from PNG** بل يوضح أيضًا كيفية **extract text from receipt** من الصور، مع الاستفادة من تسريع الـ GPU للسرعة. في النهاية ستحصل على برنامج جاهز للتنفيذ يحمل صورة للـ OCR، يعالجها، ويطبع النتيجة كنص عادي.

## ما ستتعلمه

- كيفية **load image for OCR** باستخدام `ImageInputStream` بسيط.
- تمكين دعم الـ GPU بحيث يعمل المحرك أسرع على الأجهزة الحديثة.
- الخطوات الدقيقة لـ **recognize text from PNG** واستخراج السلاسل المفيدة من الإيصال.
- الأخطاء الشائعة (مثل معرف جهاز الـ GPU الخاطئ) ونصائح أفضل الممارسات.
- شفرة كاملة قابلة للتنفيذ يمكنك نسخها ولصقها في بيئة التطوير المتكاملة الخاصة بك.

**المتطلبات المسبقة**

- Java 17 أو أحدث (تستخدم الشفرة كلمة المفتاح `var` للتبسيط، لكن يمكنك استبدالها بأنواع صريحة إذا كنت تستخدم Java 8).
- مكتبة OCR توفر الفئات `OcrEngine` و `ImageInputStream` و `OcrResult` (مثلاً SDK *FastOCR* الخيالي؛ استبدله بالمكتبة الفعلية التي تستخدمها).
- جهاز يدعم الـ GPU إذا أردت الاستفادة من تحسين الأداء (اختياري لكن يُنصح به).

---

## الخطوة 1: تشغيل OCR على صورة – تمكين تسريع الـ GPU

الخطوة الأولى هي إنشاء محرك OCR وإبلاغه باستخدام الـ GPU. هذه الخطوة حاسمة لأن عدم تمكين الـ GPU يجعل المحرك يعود إلى المعالج المركزي، مما قد يكون أبطأ بشكل ملحوظ للوصلات ذات الدقة العالية.

```java
// Step 1: Create the OCR engine and enable GPU acceleration
OcrEngine ocrEngine = new OcrEngine();

// Turn on GPU usage – this makes the recognition much faster
ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage

// Optional: select which GPU device to use (0 = first GPU)
ocrEngine.getConfig().setGpuDeviceId(0);
```

**لماذا هذا مهم:**  
تسريع الـ GPU يخفّف الحسابات المصفوفية الثقيلة التي تقوم بها محركات OCR. إذا كان لديك عدة بطاقات GPU، يمكنك اختيار البطاقة ذات الذاكرة الأكبر بتغيير قيمة `setGpuDeviceId`. نسيان تمكين الـ GPU هو سبب شائع لشكاوى “لماذا OCR الخاص بي بطيء؟”.

> **نصيحة احترافية:** إذا لم يكن جهازك يحتوي على GPU متوافق، فإن استدعاء `setUseGpu(true)` سيتجاهل ببساطة—لن يحدث تعطل، فقط معالجة أبطأ.

---

## الخطوة 2: تحميل صورة للـ OCR

الآن بعد أن أصبح المحرك جاهزًا، نحتاج إلى تزويده بصورة. يوضح المثال أدناه كيفية تحميل إيصال PNG مخزن على القرص. يمكنك استبدال المسار بأي صيغة صورة يدعمها مكتبة OCR الخاصة بك.

```java
// Step 2: Load the image you want to recognize
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
```

**حالة حافة:**  
إذا كان الملف غير موجود أو كان المسار خاطئًا، فإن `ImageInputStream` سيطرح استثناء `IOException`. احwrap الاستدعاء داخل كتلة try‑catch وسجل رسالة مفيدة:

```java
try {
    ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
} catch (IOException e) {
    System.err.println("Failed to load image: " + e.getMessage());
    return;
}
```

---

## الخطوة 3: التعرف على النص من PNG

مع تحميل الصورة، يمكن لمحرك OCR الآن القيام بسحره. هذه الخطوة في الواقع **recognizes text from PNG** (أو أي صيغة مدعومة أخرى) وتعيد كائن `OcrResult`.

```java
// Step 3: Run the OCR process on the image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

**ما الذي يحدث خلف الكواليس؟**  
يقوم المحرك بعملية ما قبل المعالجة (إزالة الميل، التحويل إلى ثنائي)، ثم يشغل شبكة عصبية لاكتشاف الأحرف، ثم يجمعها في أسطر نصية. لأننا فعلنا الـ GPU مسبقًا، تُجرى حسابات الشبكة العصبية على بطاقة الرسوميات، مما يقلل الثواني من زمن التنفيذ الكلي.

---

## الخطوة 4: استخراج النص من الإيصال

بعد التعرف، عادةً ما تحتاج فقط إلى النص الخام. عادةً ما توفر فئة `OcrResult` طريقة `getText()` التي تُعيد `String` واحدة. يمكنك بعد ذلك إجراء معالجة لاحقة (مثل استخدام regex لاستخراج الإجماليات، التواريخ، إلخ).

```java
// Step 4: Print the recognized plain‑text result
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**ناتج إيصال نموذجي:**  

```
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

يمكنك الآن تمرير هذه السلسلة إلى محلل خاص بك لاستخراج المبلغ الإجمالي، بنود الفاتورة، أو معلومات الضرائب.

---

## الخطوة 5: مثال Java OCR كامل – جاهز للتنفيذ

بجمع كل ما سبق، إليك **complete Java OCR example** يمكنك وضعه في ملف `Main.java`. تأكد من وجود مكتبة OCR على مسار الـ classpath الخاص بك.

```java
import com.fastocr.OcrEngine;
import com.fastocr.ImageInputStream;
import com.fastocr.OcrResult;

public class Main {
    public static void main(String[] args) {
        // 1️⃣ Create OCR engine and enable GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage
        ocrEngine.getConfig().setGpuDeviceId(0);        // optional: select GPU #0

        // 2️⃣ Load the image you want to recognize
        ImageInputStream imageStream;
        try {
            imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
        } catch (Exception e) {
            System.err.println("Error loading image: " + e.getMessage());
            return;
        }

        // 3️⃣ Run OCR on the image
        OcrResult ocrResult = ocrEngine.recognize(imageStream);

        // 4️⃣ Output the plain‑text result
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**الناتج المتوقع في وحدة التحكم** (مع افتراض الإيصال النموذجي أعلاه):

```
Recognized text:
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

إذا كان الناتج مشوشًا، تحقق مرة أخرى من وضوح الصورة (دقة DPI عالية) وأن حزمة لغة OCR تتطابق مع لغة الإيصال الخاص بك.

---

## أسئلة شائعة ومشكلات محتملة

| السؤال | الجواب |
|----------|--------|
| *ماذا لو لم يتم اكتشاف الـ GPU الخاص بي؟* | سيعود المحرك تلقائيًا إلى المعالج المركزي. تحقق من التعريفات وتأكد من أن `setGpuDeviceId` يطابق جهازًا موجودًا (`nvidia-smi` على لينكس يمكن أن يساعد). |
| *هل يمكنني معالجة ملفات JPEG أو TIFF؟* | نعم—فقط غيّر امتداد الملف في `ImageInputStream`. عادةً ما تقوم مكتبة OCR بالكشف التلقائي عن الصيغة. |
| *هل هناك طريقة لمعالجة دفعات متعددة من الإيصالات؟* | ضع شفرة التعرف داخل حلقة وأعد استخدام نفس كائن `OcrEngine`؛ إعادة التهيئة لكل صورة تهدر ذاكرة الـ GPU. |
| *كيف أحسن الدقة على الإيصالات منخفضة التباين؟* | قم بعملية ما قبل المعالجة (زيادة التباين، التحويل إلى تدرج الرمادي) قبل تمرير الصورة إلى محرك OCR. بعض المكتبات توفر واجهة `preprocess`. |

---

## الخلاصة

أنت الآن تعرف **how to run OCR on image** في Java، من تحميل الصورة إلى استخراج نص نظيف من الإيصال. شمل الشرح **recognize text from PNG**، **extract text from receipt**، وعرض **java OCR example** يمكنك تكييفه مع أي مشروع.  

ما الخطوات التالية؟ جرّب إيقاف علم الـ GPU لترى فرق الأداء، جرب صيغ دقة صورة مختلفة، أو دمج محلل يعتمد على regex لاستخراج الإجماليات تلقائيًا. إذا كنت مهتمًا بمواضيع أكثر تقدمًا، استكشف **OCR post‑processing**، **language model correction**، أو **batch processing pipelines**.

برمجة سعيدة، ولتكن إيصالاتك دائمًا قابلة للقراءة!  

![مثال تشغيل OCR على صورة](/images/run-ocr-on-image.png "تشغيل OCR على صورة – مثال Java")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}