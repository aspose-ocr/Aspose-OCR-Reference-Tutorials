---
category: general
date: 2026-02-22
description: تعلم كيفية تمكين وحدة معالجة الرسومات (GPU) في OCR للغة Java للتعرف على
  النص من الصورة واستخراج النص من الفاتورة بسرعة باستخدام Aspose OCR.
draft: false
keywords:
- how to enable gpu
- recognize text from image
- extract text from invoice
- java ocr example
- load image for ocr
language: ar
og_description: كيفية تمكين وحدة معالجة الرسومات في OCR باستخدام جافا، التعرف على
  النص من الصورة واستخراج النص من الفاتورة مع مثال كامل لـ OCR بجافا.
og_title: كيفية تمكين وحدة معالجة الرسومات لتقنية OCR في جافا – دليل سريع
tags:
- Java
- OCR
- GPU
- Aspose
title: كيفية تمكين الـ GPU لتقنية OCR في جافا – التعرف على النص من الصورة
url: /ar/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين GPU لـ Java OCR – التعرف على النص من الصورة

هل تساءلت يومًا **كيف يتم تمكين GPU** عند إجراء OCR في Java؟ لست وحدك—العديد من المطورين يواجهون جدارًا في الأداء عند معالجة مستندات كبيرة وعالية الدقة مثل الفواتير. الخبر السار؟ مع Aspose OCR يمكنك تبديل زر واحد والسماح لبطاقة الرسومات بالقيام بالعمل الشاق. في هذا البرنامج التعليمي سنستعرض **مثال java ocr** يقوم بتحميل صورة، تمكين معالجة GPU، واستخراج النص من فاتورة بسرعة البرق.

سنغطي كل شيء من تثبيت المكتبة إلى معالجة الحالات الحدية مثل عدم وجود تعريفات GPU. بحلول النهاية ستكون قادرًا على **التعرف على النص من ملفات الصورة** في الوقت الفعلي، وستحصل على قالب قوي لأي مشاريع OCR مستقبلية. لا حاجة لمراجع خارجية—فقط كود نقي قابل للتنفيذ.

## المتطلبات المسبقة

- **Java Development Kit (JDK) 11** أو أحدث مثبت على جهازك.  
- **Maven** (أو Gradle) لإدارة التبعيات.  
- نظام **يدعم GPU** مع تعريفات محدثة (NVIDIA، AMD، أو Intel).  
- ملف صورة لفاتورة (مثال: `large_invoice_300dpi.png`).  

إذا كنت تفتقد أيًا من هذه المتطلبات، قم بتوفيرها أولًا؛ باقي الدليل يفترض أنها موجودة.

## الخطوة 1: إضافة Aspose OCR إلى مشروعك

أول شيء نحتاجه هو مكتبة Aspose OCR. باستخدام Maven، فقط أضف المقتطف التالي إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

> **نصيحة احترافية:** رقم الإصدار يتغير بانتظام؛ تحقق من Maven Central للحصول على أحدث إصدار لتظل محدثًا.

إذا كنت تفضل Gradle، فإن المكافئ هو:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

بمجرد حل التبعيات، ستكون جاهزًا لكتابة كود يتواصل مع محرك OCR.

## الخطوة 2: كيفية تمكين GPU في محرك Aspose OCR

الآن يأتي نجمة العرض—تشغيل معالجة GPU. تقدم Aspose OCR ثلاث أوضاع معالجة:

| الوضع | الوصف |
|------|-------------|
| `CPU_ONLY` | معالج CPU فقط، آمن لأي جهاز. |
| `GPU_ONLY` | يفرض استخدام GPU، يفشل إذا لم يكن هناك جهاز متوافق. |
| `AUTO_GPU` | يكتشف GPU ويستخدمه إذا كان متاحًا، وإلا يعود إلى CPU. |

في معظم السيناريوهات نوصي بـ **`AUTO_GPU`** لأنه يمنحك أفضل ما في الاثنين. إليك كيفية تمكينه:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Enable GPU processing (AUTO_GPU uses GPU when available)
        ocrEngine.setProcessingMode(OcrEngine.ProcessingMode.AUTO_GPU);

        // The rest of the steps follow...
    }
}
```

> **لماذا هذا مهم:** تمكين GPU يمكن أن يقلل زمن المعالجة لفاتورة بدقة 300 dpi من عدة ثوانٍ إلى أقل من ثانية، حسب عتادك.

## الخطوة 3: تحميل الصورة لـ OCR – التعرف على النص من الصورة

قبل أن يتمكن المحرك من القراءة، عليك تزويده بصورة. تقبل فئة `OcrInput` في Aspose OCR مسارات الملفات، أو التدفقات، أو حتى كائنات `BufferedImage`. للتبسيط سنستخدم مسار ملف:

```java
// Step 3.1: Prepare the input image
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/large_invoice_300dpi.png"); // <-- replace with your actual path
```

> **حالة حدية:** إذا كانت الصورة أكبر من 5 MB، فكر في تقليل دقتها أولاً لتجنب أخطاء نفاد الذاكرة على GPU.

## الخطوة 4: تنفيذ OCR واستخراج النص من الفاتورة

الآن نطلب من المحرك أن يقوم بسحره. تُعيد طريقة `recognize` كائن `OcrResult` يحتوي على النص المستخرج، درجات الثقة، ومعلومات التخطيط.

```java
// Step 4.1: Run the recognition
OcrResult ocrResult = ocrEngine.recognize(ocrInput);

// Step 4.2: Print the extracted text to console
System.out.println("=== Extracted Text ===");
System.out.println(ocrResult.getText());
```

عند تشغيل البرنامج، يجب أن ترى شيئًا مشابهًا لـ:

```
=== Extracted Text ===
Invoice #12345
Date: 2026-02-20
Total: $1,245.67
...
```

إذا كان الناتج مشوشًا، تحقق مرة أخرى من وضوح الصورة وأن لغة OCR مضبوطة بشكل صحيح (Aspose الافتراضية هي الإنجليزية، لكن يمكنك تغييرها عبر `ocrEngine.setLanguage(OcrEngine.Language.SPANISH)` إلخ).

## الخطوة 5: مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي الفئة الكاملة المستقلة في Java. الصقها في بيئة التطوير IDE الخاصة بك، عدل مسار الصورة، واضغط **Run**.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU (auto‑detect)
        ocrEngine.setProcessingMode(OcrEngine.ProcessingMode.AUTO_GPU);

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace with the absolute or relative path to your invoice image
        ocrInput.add("YOUR_DIRECTORY/large_invoice_300dpi.png");

        // 4️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### النتيجة المتوقعة

تشغيل الكود على فاتورة واضحة بدقة 300 dpi عادةً ما ينتج تمثيل نصي بسيط لكل سطر في المستند. النتيجة الدقيقة تعتمد على تخطيط الفاتورة، لكنك سترى حقولًا مثل *Invoice Number*، *Date*، *Total Amount*، ووصف بنود السطر.

## المشكلات الشائعة وكيفية إصلاحها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| **`java.lang.UnsatisfiedLinkError`** | نقص تعريف GPU أو عدم توافقه | تثبيت أحدث تعريف من NVIDIA/AMD/Intel. |
| **معالجة بطيئة جدًا** | التحويل إلى CPU بشكل صامت | تحقق من أن `ocrEngine.getProcessingMode()` يعيد `AUTO_GPU` وأن `SystemInfo.isGpuAvailable()` true. |
| **ناتج فارغ** | الصورة مظلمة جدًا أو منخفضة التباين | قم بمعالجة مسبقة للصورة (زيادة التباين، تحويل إلى ثنائي) قبل تمريرها إلى OCR. |
| **نفاد الذاكرة** | صورة كبيرة جدًا (>10 MP) | تغيير حجم الصورة أو تقسيمها إلى بلاطات؛ عالج كل بلاطة على حدة. |

## ملخص خطوة بخطوة (مرجع سريع)

| الخطوة | ما قمت به |
|------|--------------|
| 1 | إضافة تبعية Aspose OCR |
| 2 | إنشاء `OcrEngine` وتعيين `AUTO_GPU` |
| 3 | تحميل صورة فاتورة عبر `OcrInput` |
| 4 | استدعاء `recognize` وطباعة `ocrResult.getText()` |
| 5 | معالجة الأخطاء الشائعة والتحقق من الناتج |

## التقدم أكثر – الخطوات التالية

- **معالجة دفعات:** التكرار عبر مجلد من الفواتير وتخزين كل نتيجة في قاعدة بيانات.  
- **دعم اللغات:** تغيير `ocrEngine.setLanguage(OcrEngine.Language.FRENCH)` للفواتير متعددة اللغات.  
- **معالجة لاحقة:** استخدام تعبيرات نمطية لاستخراج حقول مثل *Invoice Number* أو *Total Amount* من النص الخام.  
- **ضبط GPU:** إذا كان لديك عدة وحدات GPU، استكشف `ocrEngine.setGpuDeviceId(int id)` لاختيار الأسرع.

## الخلاصة

لقد أظهرنا **كيفية تمكين GPU** لـ Java OCR، قدمنا مثالًا نظيفًا **java ocr example**، وتابعنا كامل التدفق من **تحميل الصورة لـ OCR** إلى **استخراج النص من الفاتورة**. باستخدام وضع `AUTO_GPU` من Aspose تحصل على تعزيز في الأداء دون التضحية بالتوافق—مثالي لكل من أجهزة التطوير وخوادم الإنتاج.

جرّبه، عدّل معالجة الصورة، وجرب وظائف الدفعات. السماء هي الحد عندما تجمع بين تسريع GPU ومكتبة OCR قوية.

![مخطط يوضح خط أنابيب OCR المعجل بـ GPU – كيفية تمكين GPU لـ Java OCR](https://example.com/images/gpu-ocr-pipeline.png "كيفية تمكين GPU لـ Java OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}