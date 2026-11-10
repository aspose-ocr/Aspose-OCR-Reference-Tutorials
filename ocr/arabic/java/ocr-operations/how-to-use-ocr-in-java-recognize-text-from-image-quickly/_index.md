---
category: general
date: 2026-02-17
description: تعلم كيفية استخدام OCR في جافا للتعرف على النص من ملفات الصور، واستخراج
  النص من إيصالات PNG وتحويل الإيصال إلى JSON باستخدام Aspose OCR.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from png
- convert receipt to json
language: ar
og_description: دليل خطوة بخطوة حول كيفية استخدام OCR في جافا للتعرف على النص من الصورة،
  واستخراج النص من إيصالات PNG، وتحويل الإيصال إلى JSON.
og_title: كيفية استخدام OCR في جافا – التعرف على النص من الصورة
tags:
- OCR
- Java
- Aspose
- Image Processing
title: كيفية استخدام OCR في جافا – التعرف على النص من الصورة بسرعة
url: /ar/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في جافا – التعرف على النص من الصورة بسرعة

هل تساءلت يومًا **كيف تستخدم OCR** لاستخراج النص من صورة إيصال؟ ربما جربت بعض الأدوات عبر الإنترنت، لكنك انتهيت بحروف مشوشة أو تنسيق لا يمكنك تحليله. الخبر السار هو أنه ببضع أسطر من كود جافا يمكنك **التعرف على النص من الصورة**، **استخراج النص من إيصالات PNG**، وحتى **تحويل الإيصال إلى JSON** للمعالجة اللاحقة.  

في هذا الدرس سنستعرض سير العمل الكامل — من ترخيص مكتبة Aspose OCR إلى الحصول على حمولة JSON نظيفة يمكنك إدخالها في قاعدة بيانات أو نموذج تعلم آلي. لا إطالة، مجرد مثال عملي قابل للتنفيذ يمكنك نسخه ولصقه في بيئة التطوير المتكاملة الخاصة بك. في النهاية ستحصل على برنامج مستقل يأخذ `receipt.png` ويُخرج سلسلة JSON جاهزة للاستخدام.

## ما ستحتاجه

- **Java Development Kit (JDK) 8+** – أي نسخة حديثة تعمل.  
- مكتبة **Aspose OCR for Java** (حزمة Maven هي `com.aspose:aspose-ocr`).  
- **ملف ترخيص Aspose OCR صالح** (`Aspose.OCR.lic`). النسخة التجريبية المجانية تعمل للاختبار، لكن الترخيص المناسب يزيل حدود التقييم.  
- ملف صورة (PNG، JPEG، إلخ) يحتوي على النص الذي تريد قراءته — لنسمه `receipt.png` وضعه في مجلد معروف.  
- بيئة التطوير المتكاملة المفضلة لديك (IntelliJ IDEA، Eclipse، VS Code…) – حرية الاختيار لك.  

> **نصيحة احترافية:** احتفظ بملف الترخيص خارج مجلد المصدر وأشر إليه عبر مسار مطلق أو نسبي لتجنب إضافته إلى نظام التحكم في الإصدارات.

الآن بعد أن أصبحت المتطلبات واضحة، دعنا نغوص في الكود الفعلي.

## كيفية استخدام OCR – الخطوات الأساسية

فيما يلي نظرة عامة على المستوى العالي للإجراءات التي سنقوم بها:

1. **تحميل مكتبة Aspose OCR** وتطبيق الترخيص الخاص بك.  
2. **إنشاء مثيل `OcrEngine`** – هذا هو المحرك الذي يقوم بالعمل الشاق.  
3. **تحضير كائن `OcrInput`** الذي يشير إلى الصورة التي تريد معالجتها.  
4. **استدعاء `recognize` مع `ResultFormat.JSON`** للحصول على تمثيل JSON للنص المستخرج.  
5. **معالجة مخرجات JSON** – طباعتها، كتابتها إلى ملف، أو تحليلها بشكل أعمق.  

سيتم شرح كل خطوة بالتفصيل في الأقسام التالية.

## الخطوة 1 – تثبيت Aspose OCR وتطبيق الترخيص

أولاً، أضف تبعية Aspose OCR إلى ملف `pom.xml` إذا كنت تستخدم Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

الآن، في كود جافا الخاص بك، حمّل الترخيص. هذه الخطوة أساسية؛ بدونها تعمل المكتبة في وضع التقييم وقد تضع علامات مائية في المخرجات.

```java
import com.aspose.ocr.*;

public class OcrSetup {
    public static void applyLicense() throws Exception {
        // Replace the path with the actual location of your Aspose.OCR.lic file
        License ocrLicense = new License();
        ocrLicense.setLicense("C:/licenses/Aspose.OCR.lic");
    }
}
```

> **لماذا هذا مهم:** كائن `License` يخبر محرك OCR أنك مخول لاستخدام مجموعة الميزات الكاملة، والتي تشمل التعرف عالي الدقة وتصدير JSON. تخطي هذه الخطوة سيظل يسمح لك **بالتعرف على النص من الصورة**، لكن النتائج قد تكون محدودة.

## الخطوة 2 – إنشاء مثيل محرك OCR

فئة `OcrEngine` هي نقطة الدخول لجميع عمليات OCR. فكر فيها كـ “العقل” الذي يقرأ البكسلات ويقرر ما هي الأحرف التي تمثلها.

```java
import com.aspose.ocr.*;

public class OcrEngineFactory {
    public static OcrEngine createEngine() {
        // No special configuration needed for basic usage
        return new OcrEngine();
    }
}
```

يمكنك تخصيص المحرك (مثلاً، ضبط اللغة، تمكين تصحيح الميل) لاحقًا إذا كانت إيصالاتك تحتوي على نصوص غير لاتينية أو تم مسحها بزاوية. بالنسبة لمعظم الإيصالات الأمريكية، الإعدادات الافتراضية تعمل بشكل جيد.

## الخطوة 3 – تحميل الصورة التي تريد معالجتها

الآن سنشير محرك OCR إلى الملف الذي يحتوي على الإيصال. يمكن لفئة `OcrInput` قبول عدة صور، لكن في هذا الدرس سنبقي الأمر بسيطًا بصورة PNG واحدة.

```java
import com.aspose.ocr.*;

public class ImageLoader {
    public static OcrInput loadImage(String imagePath) {
        OcrInput input = new OcrInput();
        // Add the PNG receipt – this is where we **extract text from PNG**
        input.add(imagePath);
        return input;
    }
}
```

إذا احتجت يومًا إلى **استخراج النص من ملفات PNG** بشكل جماعي، فقط استدعِ `input.add()` بشكل متكرر أو مرّر قائمة بمسارات الملفات.

## الخطوة 4 – التعرف على النص وتحويل الإيصال إلى JSON

هذه هي جوهر الدرس. نطلب من المحرك التعرف على النص ونطلب النتيجة بصيغة JSON. علم `ResultFormat.JSON` يقوم بكل العمل الشاق نيابةً عنا.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonRecognizer {
    public static String recognizeToJson(OcrEngine engine, OcrInput input) throws Exception {
        // Perform OCR and request JSON output
        OcrResult result = engine.recognize(input, ResultFormat.JSON);
        // Retrieve the JSON string
        return result.getJson();
    }
}
```

حمولة JSON تشمل كل سطر تم التعرف عليه، ومربع الحد، ومستوى الثقة، والنص الأصلي. هذا الهيكل يجعل من السهل **تحويل الإيصال إلى JSON** ثم إرساله إلى أي واجهة برمجة تطبيقات لاحقة.

## الخطوة 5 – جمع كل شيء معًا وتشغيل البرنامج

فيما يلي الفئة الكاملة القابلة للتنفيذ في جافا التي تربط كل شيء معًا. احفظها باسم `JsonExportDemo.java` (أو أي اسم تفضله) وشغّلها من بيئة التطوير المتكاملة أو سطر الأوامر.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonExportDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply your Aspose OCR license (replace with your actual license file)
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.lic"); // <-- adjust path if needed

        // 2️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Prepare the input image that contains the text to be recognized
        OcrInput ocrInput = new OcrInput();
        // Replace with the absolute or relative path to your receipt PNG
        ocrInput.add("YOUR_DIRECTORY/receipt.png"); // <-- **extract text from PNG** here

        // 4️⃣ Perform recognition and request the result in JSON format
        OcrResult ocrResult = ocrEngine.recognize(ocrInput, ResultFormat.JSON);

        // 5️⃣ Retrieve the JSON string from the result
        String jsonResult = ocrResult.getJson();

        // 6️⃣ Output the JSON (or save it to a file for further processing)
        System.out.println(jsonResult);
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج يطبع سلسلة JSON مشابهة لما يلي (المحتوى الدقيق يعتمد على إيصالك):

```json
{
  "pages": [
    {
      "lines": [
        {
          "text": "Store Name",
          "confidence": 0.99,
          "boundingBox": [12, 34, 200, 45]
        },
        {
          "text": "Date: 2024-02-15",
          "confidence": 0.98,
          "boundingBox": [12, 60, 180, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.97,
          "boundingBox": [12, 120, 150, 45]
        }
      ]
    }
  ]
}
```

يمكنك الآن إدخال هذا الـ JSON إلى قاعدة بيانات، أو نقطة نهاية REST، أو خط أنابيب تحليل بيانات. خطوة **تحويل الإيصال إلى JSON** قد أُنجزت بالفعل لك.

## أسئلة شائعة وحالات خاصة

### ماذا لو كانت الصورة مائلة؟

Aspose OCR يكتشف تلقائيًا ويصحح الدورانات الخفيفة. بالنسبة للصور المائلة بشدة، استدعِ `engine.getImagePreprocessingOptions().setDeskew(true)` قبل عملية التعرف.

### كيف أتعامل مع لغات متعددة؟

استخدم `engine.getLanguage()` لتعيين اللغة المطلوبة، مثل `engine.setLanguage(Language.FRENCH)`. هذا مفيد عندما تحتاج إلى **التعرف على النص من الصورة** التي تحتوي على إيصالات متعددة اللغات.

### هل يمكنني إخراج نص عادي بدلاً من JSON؟

بالتأكيد. استبدل `ResultFormat.JSON` بـ `ResultFormat.TEXT` واستدعِ `result.getText()`.

### هل هناك طريقة لتقييد OCR على منطقة معينة؟

نعم — استخدم `ocrInput.add(imagePath, new Rectangle(x, y, width, height))` للتركيز على منطقة الإيصال، مما قد يحسن السرعة والدقة.

## نصائح احترافية لـ OCR جاهز للإنتاج

- **قم بتخزين كائن الترخيص في الذاكرة** إذا كنت تعالج العديد من الملفات داخل حلقة؛ إن إنشائه بشكل متكرر يضيف عبئًا.  
- **معالجة دفعات**: حمّل جميع مسارات الإيصالات في كائن `OcrInput` واحد واستدعِ `recognize` مرة واحدة. سيحتوي الـ JSON على مصفوفة من الصفحات، كل صفحة تحتوي على سطورها.  
- **تحقق من صحة JSON**: بعد الحصول على السلسلة، قم بتحليلها باستخدام مكتبة مثل Jackson لضمان أنها صالحة قبل تخزينها.  
- **راقب مستوى الثقة**: يتضمن الـ JSON حقل `confidence` لكل سطر. استبعد السطور التي يكون مستوى الثقة فيها أقل من عتبة (مثلاً 0.85) لتجنب البيانات غير الصالحة.  
- **أمن ترخيصك**: احفظ `Aspose.OCR.lic` في خزانة آمنة أو متغيّر بيئي، خاصةً في عمليات النشر السحابية.  

## الخلاصة

لقد غطينا **كيفية استخدام OCR** في جافا لـ **التعرف على النص من الصورة**، **استخراج النص من إيصالات PNG**، و**تحويل الإيصال إلى JSON** — كل ذلك من خلال مثال مختصر وشامل. الخطوات بسيطة، الكود قابل للتنفيذ بالكامل، ومخرجات JSON توفر لك تمثيلًا منظمًا جاهزًا لأي نظام لاحق.

بعد ذلك، قد تستكشف سيناريوهات أكثر تقدمًا: إدخال الـ JSON إلى Apache Kafka للمعالجة في الوقت الحقيقي، تطبيق أنماط regex لاستخراج إجماليات العناصر، أو دمجه مع خدمة OCR سحابية للتوسع. مهما كان اختيارك، ستظل الأساسيات التي تعلمتها الآن هي نفسها.

هل لديك أسئلة، أو واجهت مشكلة أثناء التجربة؟ اترك تعليقًا أدناه، وسنحل المشكلة معًا. برمجة سعيدة، واستمتع بتحويل صور الإيصالات الفوضوية إلى بيانات نظيفة قابلة للبحث!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}