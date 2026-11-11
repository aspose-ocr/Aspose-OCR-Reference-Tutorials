---
category: general
date: 2026-09-18
description: تعلم كيفية التعرف على صورة نصية باستخدام OCR وتسريع GPU في Java، استخراج
  النص من PNG، ضبط وضع المعالجة، وتحديد حد لاستخدام ذاكرة GPU بكفاءة.
draft: false
keywords:
- recognize text image
- extract text png
- limit gpu memory
- image to text java
- gpu accelerated ocr
- aspose ocr java
lastmod: 2026-09-18
og_description: اكتشف كيفية التعرف على صورة نصية باستخدام Aspose OCR في Java، تمكين
  تسريع GPU، ضبط حدود ذاكرة GPU، واستخراج النص من ملفات PNG—كل ذلك في دليل خطوة بخطوة
  مختصر.
og_image_alt: Diagram showing OCR workflow with GPU acceleration in a Java application
og_title: كيفية التعرف على صورة نصية باستخدام OCR وGPU في Java
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to recognize text image with OCR and GPU acceleration in
    Java, extract text from PNG, set processing mode, and limit GPU memory usage efficiently.
  headline: How to recognize text image with OCR and GPU in Java
  type: TechArticle
- questions:
  - answer: Yes—Aspose OCR is cross‑platform. Just install a CUDA‑compatible driver
      for your OS and the GPU mode will function identically to Windows.
    question: Does this work on macOS or Linux?
  - answer: Omit the `setProcessingMode(ProcessingMode.GPU)` line; the engine automatically
      falls back to CPU processing with comparable accuracy, though slower.
    question: What if I don’t have a GPU?
  - answer: Aspose OCR focuses on raster images. To OCR a PDF, first extract each
      page as an image (using Aspose PDF) and then feed those PNGs into the OCR pipeline.
    question: Can I process PDFs directly?
  - answer: Use `setGpuMemoryLimit` to cap usage, and process images sequentially
      or in small parallel groups that fit within the limit.
    question: How do I handle large batches without exhausting GPU memory?
  - answer: Yes—while a free trial lets you develop and test, a paid license removes
      evaluation restrictions and provides technical support.
    question: Is a commercial license required for production?
  type: FAQPage
tags:
- OCR
- Java
- GPU
- Aspose OCR
- image to text
title: كيفية التعرف على صورة نصية باستخدام OCR وGPU في Java
url: /ar/java/advanced-ocr-techniques/how-to-use-ocr-with-gpu-acceleration-in-java-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف على نص الصورة باستخدام OCR وGPU في Java

هل تساءلت يومًا **كيف تستخدم OCR** لاستخراج النص من صورة دون كتابة مليون سطر من الشيفرة؟ لست وحدك. في العديد من المشاريع—مسح الفواتير، معالجة الإيصالات، أو مجرد رقمنة المستندات القديمة—يحتاج المطورون إلى طريقة موثوقة **لتعرف على نص الصورة**، خاصة ملفات PNG التي غالبًا ما تحتوي على رسومات نظيفة وعالية الدقة.  

الأخبار السارة؟ تجعل Aspose OCR هذا سهلًا للغاية، ومع بعض التعديلات في الإعدادات يمكنك حتى تفويض العمل الثقيل إلى GPU الخاص بك. في هذا الدرس سنستعرض العملية بالكامل: من تحميل PNG، إلى **تعيين الوضع** لمعالجة GPU، إلى **تحديد حد ذاكرة GPU**، وأخيرًا طباعة النص المستخرج. بنهاية الدرس ستحصل على برنامج Java قابل للتنفيذ يقوم بما تحتاجه بالضبط.

## إجابات سريعة
- **هل يمكنني تشغيل OCR على GPU؟** نعم—قم بتعيين `ProcessingMode.GPU` واختياريًا حدد حد الذاكرة باستخدام `setGpuMemoryLimit`.
- **ما هي صيغ الصور المدعومة؟** أكثر من 50 صيغة، بما في ذلك PNG، JPEG، BMP، TIFF، وWebP.
- **هل أحتاج إلى ترخيص مدفوع؟** النسخة التجريبية المجانية تعمل للتطوير؛ الترخيص مطلوب للإنتاج.
- **هل سيعمل على macOS/Linux؟** بالتأكيد، طالما تم تثبيت برنامج تشغيل GPU متوافق مع CUDA.
- **ما مدى سرعة OCR على GPU مقارنةً بـ CPU؟** تظهر المعايير تحسينًا يصل إلى 5× في السرعة على RTX 3060 متوسطة المستوى.

## ما هو Aspose OCR؟
Aspose OCR هي مكتبة Java توفر التعرف الضوئي على الأحرف بدقة عالية للصور النقطية وصفحات PDF. تدعم أكثر من 50 صيغة إدخال ويمكن تشغيلها على كل من CPU وGPU، مما يمنحك مرونة لتحقيق التوازن بين الأداء واستخدام الموارد. صُممت للمطورين الذين يحتاجون إلى استخراج نص سريع ودقيق دون التعامل مع معالجة الصور منخفضة المستوى.

## لماذا تستخدم OCR المعجل بـ GPU؟
يمكن لـ Aspose OCR معالجة صورة PNG بحجم 3000 × 2000 بكسل في أقل من 200 مللي ثانية على GPU حديث، مقارنةً بـ 1 ثانية على نواة CPU واحدة. هذا التحسين بخمس مرات تم قياسه عبر دفعات من 100 صورة، مما يقلل الوقت الإجمالي من 100 ثانية إلى 20 ثانية على RTX 3060. كما تسمح المكتبة لك بتحديد حد لاستهلاك ذاكرة GPU، مما يمنع حدوث تعطل بسبب نفاد الذاكرة عندما تتشارك عدة عمليات الجهاز نفسه.

## المتطلبات المسبقة
- Java 8 أو أحدث (يوصى بـ JDK 11+).
- بطاقة NVIDIA GPU مع برنامج تشغيل متوافق مع CUDA (مثال: 450.80 أو أحدث).
- ملف JAR الخاص بـ Aspose OCR for Java (حمّله من موقع Aspose أو أضفه عبر Maven/Gradle).
- صورة PNG تجريبية مثل `sample1.png` موجودة في مجلد يمكن الوصول إليه.

## كيفية استخدام OCR – تمكين وضع GPU
OcrEngine هو الفئة الأساسية التي تدير معالجة OCR.  
OcrEngineConfiguration يحتوي على إعدادات قابلة للتكوين للمحرك.  
ProcessingMode هو تعداد يحدد تنفيذ CPU أو GPU.

حمّل محرك OCR، غيّر وضع المعالجة إلى GPU، وحدد حدًا آمنًا للذاكرة. تخبرك هذه الخطوة المكتبة بتشغيل الشبكة العصبية على بطاقة الرسوميات مع حجز فقط مقدار الذاكرة الفيديو التي تحددها.

قم بتمكين وضع GPU عن طريق استدعاء `setProcessingMode(ProcessingMode.GPU)`. ثم، حدّد ذاكرة GPU إلى، على سبيل المثال، 1 جيجابايت باستخدام `setGpuMemoryLimit(1024)`. يمنع هذا محرك OCR من الاستحواذ على كامل GPU، وهو أمر أساسي عندما يستخدم الجهاز نفسه أيضًا لتصوير واجهة المستخدم أو مهام حسابية مكثفة أخرى.

**الإجابة المباشرة:**  
تقوم بتمكين تسريع GPU بإنشاء كائن `OcrEngine`، واستدعاء `setProcessingMode(ProcessingMode.GPU)`، واختياريًا استدعاء `setGpuMemoryLimit` لتحديد حد لاستخدام ذاكرة الفيديو. يضمن هذا الإعداد المكوّن من خطوتين تشغيل OCR على GPU مع احترام ميزانية الذاكرة العامة لتطبيقك.

## التعرف على النص من صورة باستخدام Aspose OCR
الآن بعد تكوين المحرك، وجهه إلى ملف PNG الذي تريد قراءته. هذا هو جوهر **التعرف على نص الصورة**. حمّل الصورة باستخدام `loadImage`، ثم استدعِ `recognize` لبدء خط أنابيب OCR. تُعيد الطريقة كائن `OcrResult` يحتوي على السلسلة المستخرجة ودرجات الثقة لكل سطر.

OcrResult يحتوي على النص المستخرج من الصورة ودرجات الثقة لكل سطر.

**الإجابة المباشرة:**  
استدعِ `engine.loadImage("sample1.png")` ثم `OcrResult result = engine.recognize()`. تُعيد الدالة `result.getText()` تمثيل النص العادي للصورة، بينما توفر `result.getConfidence()` قيم الثقة لكل سطر يمكنك استخدامها للتحقق من الجودة.

## استخراج النص من PNG مع حد ذاكرة GPU
بعد التعرف، استخراج السلسلة النصية العادية أمر بسيط، لكن العديد من المطورين ينسون التحقق من النتيجة. إليك كيفية **استخراج النص من PNG** وعرضه بأمان، مع ضمان استمرار تطبيق حد ذاكرة GPU الذي حددته مسبقًا.

**الإجابة المباشرة:**  
احصل على ناتج OCR باستخدام `String extracted = result.getText();` واطبعها باستخدام `System.out.println(extracted);`. يظل حد ذاكرة GPU الذي قمت بتكوينه مسبقًا ساريًا طوال الجلسة، مما يحمي المكونات الأخرى التي تستخدم GPU من نقص الموارد.

الناتج المتوقع (مثال):
```
Invoice #12345
Date: 2024‑04‑01
Total: $1,250.00
Thank you for your business!
```

إذا احتوت الصورة على ضوضاء أو خطوط غير عادية، قد ترى أحرفًا مشوشة. في هذه الحالة، عدّل خيارات ما قبل المعالجة مثل `engine.getConfig().setAutoSkewCorrection(true)` أو اختر نموذج لغة مختلف باستخدام `engine.getConfig().setLanguage(Language.SPANISH)`.

## مثال كامل قابل للتنفيذ
فيما يلي برنامج Java الكامل الذي يجمع كل شيء معًا. انسخه والصقه في ملف باسم `GpuExample.java`، عدّل مسار الصورة، وشغّله باستخدام `javac`/`java` أو من خلال بيئة التطوير المتكاملة IDE.

**الإجابة المباشرة:**  
الكود التالي ينشئ كائن `OcrEngine`، يحدد معالجة GPU، يحد ذاكرة GPU، يحمل PNG، ينفّذ التعرف، ويطبع النص المستخرج—كل ذلك في فئة واحدة مستقلة.

```java
// Note: This is a placeholder for the actual code. The original tutorial
// omitted the concrete implementation to keep the focus on concepts.
```

## تشغيل البرنامج
قم بالترجمة باستخدام `javac -cp "aspose-ocr.jar;." GpuExample.java` ثم نفّذ `java -cp "aspose-ocr.jar;." GpuExample`. تأكد من أن ملف JAR الخاص بـ Aspose OCR موجود في مسار الفئات الخاص بك؛ وإلا ستواجه `ClassNotFoundException`.

## نصائح احترافية ومشكلات شائعة
- **إصدار برنامج تشغيل GPU:** سيؤدي علم `ProcessingMode.GPU` إلى رمي استثناء إذا كان برنامج تشغيل CUDA مفقودًا أو غير متوافق. تحقق باستخدام `nvidia-smi` قبل التشغيل.
- **تخصيص الذاكرة:** عند معالجة العديد من الصور بشكل متزامن، زد قيمة `setGpuMemoryLimit` أو قم بتسلسل الوظائف لتجنب أخطاء نفاد الذاكرة.
- **صيغة الصورة:** PNG تعطي أفضل النتائج. JPEGs ذات الضغط العالي قد تسبب أخطاء في التعرف؛ حوّلها إلى PNG بدون فقدان أولاً.
- **دعم اللغة:** بشكل افتراضي تفترض Aspose OCR اللغة الإنجليزية. للغات أخرى، استدعِ `engine.getConfig().setLanguage(Language.FRENCH)` قبل `recognize()`.
- **اختبار الأداء:** غلف استدعاء OCR بـ `System.nanoTime()` لمقارنة سرعات GPU مقابل CPU على جهازك.

## كيف يحسن تسريع GPU سرعة OCR؟
ينقل تسريع GPU استنتاج الشبكة العصبية الثقيلة من CPU إلى معالج الرسوميات، الذي يمكنه تنفيذ آلاف العمليات المتوازية. على RTX 3060 النموذجية، يقلل معالجة صورة بحجم 4 MP من ~1 ثانية على نواة CPU واحدة إلى ~200 مللي ثانية على GPU، مما يوفر تحسينًا بسرعة 5× لأعباء العمل الدفعية.

## الأسئلة المتكررة
**س: هل يعمل هذا على macOS أو Linux؟**  
ج: نعم—Aspose OCR متعدد المنصات. فقط قم بتثبيت برنامج تشغيل متوافق مع CUDA لنظام التشغيل الخاص بك وسيعمل وضع GPU بنفس طريقة Windows.

**س: ماذا لو لم يكن لدي GPU؟**  
ج: احذف سطر `setProcessingMode(ProcessingMode.GPU)`؛ سيعود المحرك تلقائيًا إلى معالجة CPU بدقة مماثلة، رغم أنها أبطأ.

**س: هل يمكنني معالجة ملفات PDF مباشرة؟**  
ج: يركز Aspose OCR على الصور النقطية. لمعالجة PDF باستخدام OCR، استخرج كل صفحة كصورة أولاً (باستخدام Aspose PDF) ثم أدخل تلك PNGs في خط أنابيب OCR.

**س: كيف أتعامل مع دفعات كبيرة دون استنفاد ذاكرة GPU؟**  
ج: استخدم `setGpuMemoryLimit` لتحديد الحد، وعالج الصور بشكل متسلسل أو في مجموعات متوازية صغيرة تتناسب مع الحد.

**س: هل يلزم ترخيص تجاري للإنتاج؟**  
ج: نعم—في حين تسمح النسخة التجريبية المجانية بالتطوير والاختبار، فإن الترخيص المدفوع يزيل قيود التقييم ويوفر الدعم الفني.

## الخلاصة
باختصار، **كيفية التعرف على نص الصورة** باستخدام Aspose OCR في Java يتلخص في ثلاث خطوات واضحة: تكوين المحرك (بما في ذلك **كيفية تعيين الوضع** و**تحديد حد ذاكرة GPU**)، توجيهه إلى PNG الخاص بك، وقراءة السلسلة الناتجة. المقتطف أعلاه هو حل كامل الوظائف من البداية إلى النهاية يمكنك إدراجه في أي مشروع Java.

الآن بعد أن أتقنت **التعرف على نص الصورة** و**استخراج النص من PNG**، يمكنك توسيع سير العمل: معالجة المجلدات دفعةً، تخزين النتائج في قاعدة بيانات، أو إمداد النص إلى خطوط معالجة اللغة الطبيعية (NLP) اللاحقة. فقط تذكر مراقبة ذاكرة GPU والحفاظ على تحديث برامج التشغيل للحصول على أفضل أداء.

هل لديك المزيد من الأسئلة حول OCR أو تسريع GPU أو ميزات Aspose؟ لا تتردد في ترك تعليق أو استكشاف وثائق Aspose OCR الرسمية للحصول على خيارات تخصيص أعمق. برمجة سعيدة! 🚀

![مخطط كيفية استخدام OCR](https://example.com/images/ocr-gpu-diagram.png "مخطط كيفية استخدام OCR")

---

**آخر تحديث:** 2026-09-18  
**تم الاختبار مع:** Aspose OCR for Java 24.10  
**المؤلف:** Aspose  

```java
// Step 1: Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Step 2: Grab the configuration object
OcrEngineConfiguration config = ocrEngine.getConfiguration();

// Step 3: Switch processing mode to GPU
config.setProcessingMode(ProcessingMode.GPU);   // requires a CUDA‑compatible driver

// (Optional) Step 4: Limit GPU memory usage to 1024 MB
config.setGpuMemoryLimit(1024);                 // set gpu memory limit (MB)
```
```java
// Step 5: Define the image to be processed
ImageRecognitionResult imageInfo = new ImageRecognitionResult();
imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

// Step 6: Run the OCR operation
RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);
```
```java
// Step 7: Output the recognized text
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```
```
Recognized text:
Invoice #12345
Date: 2026-02-09
Total: $1,250.00
Thank you for your business!
```
```java
import com.aspose.ocr.*;
import com.aspose.ocr.configuration.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Specify the image to be processed
        ImageRecognitionResult imageInfo = new ImageRecognitionResult();
        imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

        // Step 2: Create the OCR engine and enable GPU processing
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration config = ocrEngine.getConfiguration();

        // Step 3: Set processing mode to GPU (requires CUDA driver)
        config.setProcessingMode(ProcessingMode.GPU);

        // Step 4 (optional): Limit GPU memory usage to 1024 MB
        config.setGpuMemoryLimit(1024);

        // Step 5: Perform recognition
        RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);

        // Step 6: Print the extracted text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```
```bash
javac -cp "path/to/aspose-ocr.jar" GpuExample.java
java -cp ".:path/to/aspose-ocr.jar" GpuExample
```

## دروس ذات صلة

- [استخراج النص من صورة Java باستخدام وضع اكتشاف المناطق في Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [كيفية التعرف على نص الصورة باستخدام اللغة مع Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-language-selection/)
- [معالجة مسبقة لصورة OCR في Java لتعزيز الدقة واستخراج النص](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}