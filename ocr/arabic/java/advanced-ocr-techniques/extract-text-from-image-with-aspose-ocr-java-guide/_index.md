---
category: general
date: 2026-09-28
description: تعلم كيفية استخراج النص من صورة java باستخدام Aspose OCR، بما في ذلك
  استخراج form data java عبر regions of interest للحصول على نتائج دقيقة.
draft: false
keywords:
- extract text from image java
- extract form data java
- aspose ocr tutorial java
lastmod: 2026-09-28
og_description: تعلم كيفية استخراج النص من صورة java باستخدام Aspose OCR، بما في ذلك
  استخراج form data java عبر regions of interest. دليل سريع للمطورين.
og_image_alt: Guide showing how to extract text from image java using Aspose OCR
og_title: استخراج النص من صورة java باستخدام Aspose OCR – guide
schemas:
- author: Aspose
  dateModified: '2026-09-28'
  description: Learn how to extract text from image java with Aspose OCR, including
    extracting form data java via regions of interest for precise results.
  headline: Extract text from image java using Aspose OCR – guide
  type: TechArticle
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., using Aspose
      PDF) and then feed the image to the OCR engine.
    question: Does this work with PDFs?
  - answer: OCR can’t read boolean states, but you can treat the checkbox area as
      an ROI and inspect the pixel density to infer a tick.
    question: What if my form has checkboxes?
  - answer: Loop over each page image, reuse the same ROI list, and concatenate the
      results.
    question: Can I extract text from a multi‑page form in one go?
  - answer: Increase the contrast, enable binarization via `ocrEngine.getEngineOptions().setBinarization(true)`,
      and consider pre‑processing the image to remove noise.
    question: How do I improve accuracy on low‑quality scans?
  - answer: Yes. Aspose OCR offers a free trial, but a commercial license is needed
      for deployment.
    question: Is a license required for production use?
  type: FAQPage
tags:
- extract text from image java
- aspose ocr tutorial java
- extract form data java
title: استخراج النص من صورة java باستخدام Aspose OCR – guide
url: /ar/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من صورة جافا باستخدام Aspose OCR – دليل

هل احتجت يومًا إلى **استخراج النص من الصورة** لكن انتهى بك الأمر إلى تحليل الصورة بالكامل، مضيعًا دورات المعالج والحصول على نتائج مشوشة؟ لست وحدك. في العديد من التطبيقات الواقعية—مثل ماسحات الفواتير، قارئات جوازات السفر، أو نماذج إدخال البيانات—أنت تهتم فقط بعدد قليل من الحقول، وليس باللوحة الكاملة.

الخبر السار هو أن Aspose OCR يتيح لك **استخراج النص من الصورة** *و* من مناطق نموذج محددة عن طريق تعريف المضلعات. في هذا الدرس ستتعرف بالضبط على كيفية **استخراج النص من حقول النموذج** باستخدام Java، ولماذا هذه الطريقة مهمة، وما الذي يجب تعديله عندما تسوء الأمور.

سنعرض أدناه كل شيء من إعداد المكتبة إلى التعامل مع الحالات الصعبة، بحيث يكون لديك في النهاية مقتطف جاهز للتنفيذ يجلب فقط البيانات التي تحتاجها.

## إجابات سريعة
- **ما هي الفائدة الرئيسية؟** يقلل OCR المستهدف من وقت المعالجة بنسبة تصل إلى 70 % ويقضي على الضوضاء غير المتعلقة.  
- **أي مكتبة تُستخدم؟** Aspose OCR for Java، أحدث إصدار 23.10.  
- **هل أحتاج إلى Maven/Gradle؟** لا، فقط أضف ملف JAR إلى مسار الفئات الخاص بك.  
- **هل يمكنني معالجة حقول متعددة؟** نعم—عرّف مضلعًا لكل حقل وأضفه إلى قائمة ROI.  
- **ما الصيغ المدعومة؟** أكثر من 30 صيغة صورة، حتى 100 ميغابايت لكل ملف دون تحميل كامل في الذاكرة.

## ما هو استخراج النص من صورة جافا؟
**استخراج النص من صورة جافا** يشير إلى استخدام محرك OCR قائم على Java لقراءة الأحرف من الرسومات النقطية. يوفر Aspose OCR محركًا عالي الدقة يدعم Unicode، ولغات متعددة، ومناطق اهتمام مخصصة. يعمل عن طريق تحليل أنماط البكسل، وتقسيم الأحرف، وتطبيق نماذج اللغة لإنتاج سلاسل قابلة للقراءة آليًا.

## لماذا تستخدم Aspose OCR لاستخراج بيانات النموذج باستخدام جافا؟
يدعم Aspose OCR **50+ input image formats** (بما في ذلك PNG، JPEG، TIFF، BMP) ويمكنه معالجة مستندات متعددة الصفحات دون تحميل الملف بالكامل في الذاكرة، محققًا أداءً أسرع حتى **3× faster** عندما يتم تطبيق تصفية ROI. بالإضافة إلى ذلك، تقلل قدرة ROI من استهلاك الذاكرة، مما يجعلها مناسبة لمعالجة دفعات واسعة النطاق في بيئات السحابة.

## المتطلبات المسبقة
- Java 17 (أو أي JDK حديث) – الإصدارات الأحدث تدعم Unicode بشكل أفضل.  
- Aspose.OCR for Java 23.10 (أو أحدث نسخة في وقت القراءة).  
- صورة نموذجية باسم `form.png` تحتوي على حقول معرفة بوضوح.  
- بيئة تطوير متكاملة أو محرر نص بسيط—IntelliJ IDEA، VS Code، أو حتى Notepad يكفي.

لا حاجة إلى سحر Maven/Gradle للعرض الأساسي؛ فقط أضف ملف JAR الخاص بـ Aspose OCR إلى مسار الفئات الخاص بك.

---

## الخطوة 1 – تهيئة محرك OCR وتحميل صورتك

OcrEngine هو الفئة الأساسية التي تنسق عمليات OCR، وتكشف عن إعدادات مثل اللغة ومعالجة الصورة مسبقًا.  
ImageStream يمثل بيانات الصورة المصدر ويوفر مساعدات ثابتة مثل `fromFile` لتحميل صورة من القرص.  
Polygon هو شكل Java AWT يُستخدم لتحديد رؤوس منطقة الاهتمام.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the source image – replace the path if your file lives elsewhere
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));
```

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the source image – replace the path if your file lives elsewhere
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));
```

*لماذا هذا مهم:*  
إنشاء `OcrEngine` جديد يمنحك صفحة نظيفة، مما يضمن عدم تأثير الإعدادات المتبقية على تشغيلك. تحميل الصورة مبكرًا يتحقق أيضًا من وجود الملف، لذا ستحصل على استثناء مفيد قبل إضاعة الوقت في الخطوات اللاحقة.

> **نصيحة احترافية:** إذا كانت صورتك ضخمة (أكثر من 5 ميغابايت)، فكر في تغيير حجمها أولاً. يعمل Aspose OCR بشكل أسرع على الصور التي يقل عرضها أو ارتفاعها عن 2000 بكسل.

## الخطوة 2 – تعريف المضلعات للحقول التي تريد قراءتها

منطقة *Region of interest* (ROI) هي مجرد مضلع يخبر المحرك أين يبحث. أدناه ننشئ مستطيلين—واحد لـ “First Name” وآخر لـ “Date of Birth”. عدل الإحداثيات لتتناسب مع نموذجك.

```java
        // Polygon for the first field (e.g., First Name)
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},   // X‑coordinates
                new int[]{100, 100, 150, 150}, // Y‑coordinates
                4);

        // Polygon for the second field (e.g., Date of Birth)
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);
```

*لماذا المضلعات بدلاً من المستطيلات؟*  
تمنحك المضلعات مرونة التعامل مع الصناديق المائلة أو غير المستطيلة—وهو شائع عند مسح النماذج المطبوعة التي ليست محاذاة تمامًا.

## الخطوة 3 – إخبار Aspose OCR بالتركيز فقط على تلك المناطق

الآن نقوم بربط المضلعات بالمحرك. طريقة `setRegionsOfInterest` تسجل قائمة المضلعات التي يجب على المحرك التركيز عليها، وتقبل قائمة، لذا يمكنك إضافة أي عدد من الحقول كما تشاء.

```java
        // Limit OCR to the defined regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));
```

*ما يحدث خلف الكواليس؟*  
يقوم Aspose OCR بقص كل مضلع إلى صورة bitmap منفصلة، ثم تشغيل خوارزمية التعرف، ثم دمج النتائج معًا. هذا يقلل بشكل كبير من الإيجابيات الزائفة من الرسومات المحيطة.

## الخطوة 4 – تشغيل عملية OCR

OcrResult يجمع النص المعترف به مع مقاييس الثقة لكل منطقة تمت معالجتها.

```java
        // Execute OCR on the selected ROIs
        OcrResult ocrResult = ocrEngine.process();
```

إذا كنت بحاجة إلى ثقة لكل حقل، يمكنك فحص `ocrResult.getRegions()`—كل منطقة تحمل درجتها الخاصة. بالنسبة لمعظم النماذج البسيطة، يكون النص العام كافيًا.

## الخطوة 5 – عرض (أو تخزين) النص المستخرج

أخيرًا، نقوم بطباعة النتيجة إلى وحدة التحكم. في تطبيق حقيقي قد تكتب إلى قاعدة بيانات، ملف JSON، أو ترسل عبر API.

```java
        // Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**الناتج المتوقع (مثال):**

```
=== Extracted Text ===
John Doe
12/04/1990
```

السطران يتطابقان مع المضلعين الذين عرّفناهما. إذا لاحظت مسافات إضافية، قم بإزالتها باستخدام `String.trim()`.

## كيفية استخراج النص من النموذج عندما يكون لديك العديد من الحقول

إدخال الإحداثيات يدويًا لكل حقل يصبح سريعًا عرضة للأخطاء ومستهلكًا للوقت، خاصةً عندما تتطور النماذج. من خلال استخراج تعريفات ROI إلى ملف CSV، يمكنك صيانتها بشكل منفصل، والتحكم في إصدارات التغييرات، والسماح لكود Java بإنشاء المضلعات المطلوبة ديناميكيًا أثناء التشغيل.

1. **إنشاء ملف CSV** حيث يحتوي كل صف على `fieldName, x1, y1, x2, y2, x3, y3, x4, y4`.  
2. **تحميل ملف CSV** أثناء التشغيل، التكرار عبر كل سطر، بناء `Polygon`، وإضافته إلى قائمة ROI.  

```java
List<Polygon> rois = new ArrayList<>();
try (BufferedReader br = new BufferedReader(new FileReader("fields.csv"))) {
    String line;
    while ((line = br.readLine()) != null) {
        String[] parts = line.split(",");
        int[] xs = { Integer.parseInt(parts[1]), Integer.parseInt(parts[3]),
                    Integer.parseInt(parts[5]), Integer.parseInt(parts[7]) };
        int[] ys = { Integer.parseInt(parts[2]), Integer.parseInt(parts[4]),
                    Integer.parseInt(parts[6]), Integer.parseInt(parts[8]) };
        rois.add(new Polygon(xs, ys, 4));
    }
}
ocrEngine.getEngineOptions().setRegionsOfInterest(rois);
```

*لماذا العناء؟*  
يتيح لك أتمتة إنشاء ROI إعادة استخدام نفس كود Java عبر تخطيطات نماذج متعددة، مما يحافظ على مبدأ DRY (Don’t Repeat Yourself) في مشروعك.

## حالات حافة ونصائح قد لا تكون فكرت فيها
- **Rotated scans:** إذا كانت الصورة بأكملها مائلة، استدعِ `ocrEngine.getEngineOptions().setRotateAngle(degrees)`.  
- **Low contrast:** اضبط `ocrEngine.getEngineOptions().setContrast(1.5f)` لتعزيز قابلية القراءة.  
- **Non‑Latin scripts:** غيّر اللغة باستخدام `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.Spanish)` (أو أي لغة مدعومة).  
- **Partial OCR failures:** تحقق دائمًا من `ocrResult.getConfidence()`؛ إذا انخفضت عن 80 %، فكر في طلب التحقق اليدوي من المستخدم.

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل، جاهز للترجمة والتنفيذ. استبدل `YOUR_DIRECTORY` بالمجلد الذي يحتوي على `form.png`.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Step 1 – Initialize engine and load image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));

        // Step 2 – Define polygons for each form field
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},
                new int[]{100, 100, 150, 150},
                4);
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);

        // Step 3 – Limit OCR to those regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));

        // Step 4 – Run OCR
        OcrResult ocrResult = ocrEngine.process();

        // Step 5 – Show the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

قم بالترجمة باستخدام:

```bash
javac -cp "aspose-ocr-23.10.jar" MultiRoiDemo.java
java -cp ".:aspose-ocr-23.10.jar" MultiRoiDemo
```

يجب أن ترى السطرين من النص الذين ينتميان إلى مناطق ROI المحددة.

## الأسئلة المتكررة
**س: هل يعمل هذا مع ملفات PDF؟**  
ج: ليس مباشرة. حوّل كل صفحة PDF إلى صورة أولاً (مثلاً باستخدام Aspose PDF) ثم قدم الصورة إلى محرك OCR.

**س: ماذا لو كان للنموذج الخاص بي مربعات اختيار؟**  
ج: لا يمكن لـ OCR قراءة الحالات المنطقية، لكن يمكنك اعتبار منطقة مربع الاختيار كـ ROI وفحص كثافة البكسل لاستنتاج وجود علامة.

**س: هل يمكنني استخراج النص من نموذج متعدد الصفحات مرة واحدة؟**  
ج: قم بالتكرار على كل صورة صفحة، أعد استخدام نفس قائمة ROI، ودمج النتائج.

**س: كيف أحسن الدقة في المسحات منخفضة الجودة؟**  
ج: زد التباين، فعّل التثنيم عبر `ocrEngine.getEngineOptions().setBinarization(true)`، وفكّر في معالجة مسبقة للصورة لإزالة الضوضاء.

**س: هل يلزم ترخيص للاستخدام في الإنتاج؟**  
ج: نعم. يقدم Aspose OCR نسخة تجريبية مجانية، لكن يلزم الحصول على ترخيص تجاري للنشر.

**آخر تحديث:** 2026-09-28  
**تم الاختبار مع:** Aspose.OCR for Java 23.10  
**المؤلف:** Aspose

## دروس ذات صلة
- [استخراج النص من صورة Java باستخدام وضع اكتشاف المناطق في Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [معالجة مسبقة لصورة OCR في Java لتعزيز الدقة واستخراج النص](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)
- [اكتشاف لغة الصورة باستخدام Aspose OCR Java Tutorial](/ocr/java/advanced-ocr-techniques/detect-language-image-with-aspose-ocr-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}