---
category: general
date: 2026-02-14
description: استخراج النص من الصورة باستخدام Aspose OCR في جافا. تعلّم كيفية استخراج
  النص من حقول النموذج مع مناطق الاهتمام للحصول على نتائج دقيقة.
draft: false
keywords:
- extract text from image
- extract text from form
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR في Java. يوضح هذا الدليل
  كيفية استخراج النص من حقول النموذج عبر مناطق الاهتمام.
og_title: استخراج النص من الصورة باستخدام Aspose OCR – دليل Java
tags:
- OCR
- Java
- Aspose
- Image Processing
title: استخراج النص من الصورة باستخدام Aspose OCR – دليل جافا
url: /ar/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة باستخدام Aspose OCR – دليل Java

هل احتجت يومًا إلى **استخراج النص من الصورة** لكن انتهى بك الأمر إلى تحليل الصورة بالكامل، مضيعًا دورات المعالج والحصول على نتائج مشوشة؟ لست وحدك. في العديد من التطبيقات الواقعية—مثل ماسحات الفواتير، قارئات جوازات السفر، أو نماذج إدخال البيانات—أنت تهتم فقط بعدد قليل من الحقول، وليس باللوحة الكاملة.  

الخبر السار هو أن Aspose OCR يتيح لك **استخراج النص من الصورة** *و* من مناطق نموذج محددة عن طريق تعريف مضلعات. في هذا الدرس ستتعرف بالضبط على كيفية **استخراج النص من حقول النموذج** باستخدام Java، ولماذا هذه الطريقة مهمة، وما الذي يجب تعديله عندما تسوء الأمور.

أدناه سنغطي كل شيء من إعداد المكتبة إلى التعامل مع الحالات الحافة الصعبة، بحيث يكون لديك في النهاية مقتطف جاهز للتنفيذ يجلب فقط البيانات التي تحتاجها.

## ما ستحتاجه

- Java 17 (أو أي JDK حديث) – الإصدارات الأحدث تدعم Unicode بشكل أفضل.  
- Aspose.OCR for Java 23.10 (أو أحدث نسخة في وقت القراءة).  
- صورة نموذجية باسم `form.png` تحتوي على حقول معرفة بوضوح.  
- بيئة تطوير متكاملة أو محرر نصوص بسيط—IntelliJ IDEA، VS Code، أو حتى Notepad يكفي.

لا حاجة إلى سحر Maven/Gradle للعرض الأساسي؛ فقط أضف ملف Aspose OCR JAR إلى مسار الفصول الخاص بك.

---

## الخطوة 1 – تهيئة محرك OCR وتحميل الصورة الخاصة بك

أول شيء يحتاجه المحرك هو صورة bitmap للعمل عليها. سنشير إليه إلى `form.png`، التي توجد في نفس المجلد مع ملف المصدر.

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

> **نصيحة احترافية:** إذا كانت صورتك ضخمة (أكثر من 5 ميغابايت)، فكر في تغيير حجمها أولاً. Aspose OCR يعمل أسرع على الصور التي يقل عرضها أو ارتفاعها عن 2000 بكسل.

## الخطوة 2 – تعريف المضلعات للحقول التي تريد قراءتها

*منطقة الاهتمام* (ROI) هي مجرد مضلع يخبر المحرك أين ينظر. أدناه ننشئ مستطيلين—واحد لـ “First Name” وآخر لـ “Date of Birth”. عدّل الإحداثيات لتتناسب مع نموذجك الخاص.

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
المضلعات تمنحك المرونة للتعامل مع الصناديق المائلة أو غير المستطيلة—وهو شائع عند مسح النماذج المطبوعة التي لا تكون محاذاة تمامًا.

## الخطوة 3 – إخبار Aspose OCR بالتركيز فقط على تلك المناطق

الآن نربط المضلعات بالمحرك. طريقة `setRegionsOfInterest` تقبل قائمة، لذا يمكنك إضافة عدد الحقول التي تريدها.

```java
        // Limit OCR to the defined regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));
```

*ماذا يحدث خلف الكواليس؟*  
Aspose OCR يقتطع كل مضلع إلى صورة bitmap منفصلة، يشغل خوارزمية التعرف، ثم يجمع النتائج معًا. هذا يقلل بشكل كبير من الإيجابيات الزائفة من الرسومات المحيطة.

## الخطوة 4 – تشغيل عملية OCR

مع تكوين كل شيء، نطلق عملية OCR. استدعاء `process()` يُعيد كائن `OcrResult` الذي يحتوي على النص المستخرج ودرجات الثقة.

```java
        // Execute OCR on the selected ROIs
        OcrResult ocrResult = ocrEngine.process();
```

إذا كنت بحاجة إلى ثقة لكل حقل، يمكنك فحص `ocrResult.getRegions()`—كل منطقة تحمل درجتها الخاصة. بالنسبة لمعظم النماذج البسيطة، النص العام يكفي.

## الخطوة 5 – عرض (أو تخزين) النص المستخرج

أخيرًا، نطبع النتيجة إلى وحدة التحكم. في تطبيق حقيقي قد تكتب إلى قاعدة بيانات، ملف JSON، أو ترسل عبر API.

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

السطران يتطابقان مع المضلعين الذين حددناهما. إذا رأيت مسافات إضافية، قم بإزالتها باستخدام `String.trim()`.

## كيفية استخراج النص من النموذج عندما يكون لديك العديد من الحقول

عندما يحتوي النموذج على العشرات من المدخلات، يصبح كتابة الإحداثيات يدويًا أمرًا شاقًا. إليك نمطًا سريعًا يمكنك اعتماده:

1. **إنشاء ملف CSV** حيث يحتوي كل صف على `fieldName, x1, y1, x2, y2, x3, y3, x4, y4`.  
2. **تحميل CSV** أثناء التشغيل، التكرار عبر كل سطر، بناء `Polygon`، وإضافته إلى قائمة ROI.  

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
أتمتة إنشاء ROI تتيح لك إعادة استخدام نفس كود Java عبر تخطيطات نماذج متعددة، مما يحافظ على مشروعك DRY (Don’t Repeat Yourself).

## الحالات الخاصة والنصائح التي قد لا تكون قد فكرت فيها

- **المسحات المدورة:** إذا كانت الصورة بأكملها مدورة، استدعِ `ocrEngine.getEngineOptions().setRotateAngle(degrees)`.  
- **قليل التباين:** اضبط `ocrEngine.getEngineOptions().setContrast(1.5f)` لتعزيز قابلية القراءة.  
- **الخطوط غير اللاتينية:** غيّر اللغة باستخدام `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.Spanish)` (أو أي لغة مدعومة).  
- **فشل جزئي في OCR:** تحقق دائمًا من `ocrResult.getConfidence()`؛ إذا انخفضت عن 80 %، فكر في طلب التحقق اليدوي من المستخدم.  

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

الترجمة باستخدام:

```bash
javac -cp "aspose-ocr-23.10.jar" MultiRoiDemo.java
java -cp ".:aspose-ocr-23.10.jar" MultiRoiDemo
```

يجب أن ترى السطرين من النص الذين ينتميان إلى مناطق ROI المحددة.

## الأسئلة المتكررة

**س: هل يعمل هذا مع ملفات PDF؟**  
ج: ليس مباشرة. حوّل كل صفحة PDF إلى صورة أولاً (مثلاً باستخدام Aspose PDF) ثم قدم الصورة إلى محرك OCR.

**س: ماذا لو كان للنموذج الخاص بي مربعات اختيار؟**  
ج: لا يستطيع OCR قراءة الحالات المنطقية، لكن يمكنك اعتبار منطقة مربع الاختيار كـ ROI وفحص كثافة البكسل لاستنتاج وجود علامة.

**س: هل يمكنني استخراج النص من نموذج متعدد الصفحات دفعة واحدة؟**  
ج: قم بالتكرار على كل صورة صفحة، أعد استخدام نفس قائمة ROI، ودمج النتائج.

## الخلاصة

لقد استعرضنا حلًا كاملاً من البداية إلى النهاية لـ **استخراج النص من الصورة** باستخدام Aspose OCR، وأظهرنا كيف تسمح لك نفس التقنية **باستخراج النص من حقول النموذج** بدقة عالية. من خلال تعريف المضلعات، وتحديد تركيز المحرك، ومعالجة المشكلات الشائعة، تحصل على بيانات سريعة ونظيفة دون عبء معالجة الصورة بالكامل.

هل أنت مستعد للخطوة التالية؟ جرّب ربط ناتج OCR هذا إلى حمولة JSON، أو إرساله إلى نموذج تعلم آلي للتحقق. السماء هي الحد، والآن أنت

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}