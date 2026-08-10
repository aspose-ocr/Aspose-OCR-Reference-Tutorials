---
category: general
date: 2026-06-19
description: قم بأداء OCR على منطقة الاهتمام (ROI) في Java باستخدام Aspose OCR. تعلم
  كيفية التعرف على النص في المنطقة باستخدام كود خطوة بخطوة وأفضل الممارسات.
draft: false
keywords:
- perform OCR on ROI
- recognize text in region
- Aspose OCR Java
- OCR region detection
- Java image processing
language: ar
og_description: قم بتنفيذ OCR على منطقة الاهتمام (ROI) في جافا باستخدام Aspose OCR.
  يوضح لك هذا الدليل كيفية التعرف على النص في المنطقة، ومعالجة لغات متعددة، وتجنب
  الأخطاء الشائعة.
og_title: إجراء OCR على منطقة الاهتمام (ROI) في جافا – دليل Aspose OCR الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on ROI in Java using Aspose OCR. Learn how to recognize
    text in region with step‑by‑step code and best practices.
  headline: Perform OCR on ROI in Java – Full Aspose OCR Guide
  type: TechArticle
- description: Perform OCR on ROI in Java using Aspose OCR. Learn how to recognize
    text in region with step‑by‑step code and best practices.
  name: Perform OCR on ROI in Java – Full Aspose OCR Guide
  steps:
  - name: 1. License Path Errors
    text: If `setLicense` throws a `FileNotFoundException`, double‑check the absolute
      path or place the `.lic` file in the project’s resources folder and load it
      with `getResourceAsStream`.
  - name: 2. Overlapping or Out‑of‑Bounds ROIs
    text: Aspose does not automatically clip ROIs that extend beyond the image dimensions.
      Overlapping rectangles can cause duplicated text. Use `engine.getImageSize()`
      to verify bounds before creating rectangles.
  - name: 3. Unsupported Languages
    text: Attempting to set a language not bundled with the library will raise `UnsupportedOperationException`.
      Stick to the languages listed in Aspose’s documentation, or download the additional
      language packs.
  - name: 4. Low‑Resolution Images
    text: OCR accuracy drops dramatically below 100 dpi. If you have a low‑resolution
      scan, consider up‑scaling with a library like **Imgscalr** before feeding it
      to Aspose.
  type: HowTo
tags:
- OCR
- Java
- Aspose
- Image Recognition
title: إجراء التعرف الضوئي على الأحرف (OCR) على منطقة الاهتمام (ROI) في جافا – الدليل
  الكامل لـ Aspose OCR
url: /ar/java/advanced-ocr-techniques/perform-ocr-on-roi-in-java-full-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء OCR على ROI في Java – دليل Aspose OCR الكامل

هل تساءلت يومًا كيف تقوم **perform OCR on ROI** في Java؟ أنت لست الوحيد—المطورون يسألون باستمرار، *“كيف يمكنني استخراج جزء الجدول فقط من الفاتورة دون مسح الصورة بالكامل؟”* في هذا الدليل سنستعرض بالتفصيل كيفية **perform OCR on ROI** باستخدام Aspose OCR، وسنظهر لك أيضًا كيفية **recognize text in region** عندما تظهر لغات مختلفة جنبًا إلى جنب.

الأمر هو أن استهداف مستطيل محدد (أو ROI) يوفر وقت المعالجة، يقلل الضوضاء، وغالبًا ما ينتج نتائج أنظف. سواء كنت تتعامل مع إيصالات متعددة اللغات، نماذج، أو عقود ممسوحة ضوئيًا، فإن إتقان OCR القائم على ROI يُغيّر قواعد اللعبة. هيا نبدأ.

## ما ستحتاجه

- **Java 8+** (الكود يعمل على أي JDK حديث)
- **Aspose.OCR for Java** library (حمّل من موقع Aspose أو أضفه عبر Maven)
- ملف ترخيص **Aspose OCR** صالح (`Aspose.OCR.lic`) – العرض التجريبي يعمل بدون ترخيص لكنه سيضيف علامة مائية.
- صورة تحتوي على مناطق متميزة تريد معالجتها (مثال: فاتورة بها رأس وجدول بالفرنسية).

هذا كل شيء—لا أطر إضافية، لا تبعيات ثقيلة. إذا كنت مرتاحًا مع بيئة تطوير أساسية مثل IntelliJ IDEA أو Eclipse، فأنت جاهز للبدء.

## إجراء OCR على ROI – إعداد المحرك

الخطوة الأولى هي تجهيز محرك OCR وإبلاغه باللغة الافتراضية التي سيستخدمها. هنا يبدأ سير عمل **perform OCR on ROI** فعليًا.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.geometry.*;

public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply the Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

> **نصيحة احترافية:** إذا نسيت ضبط الترخيص، سيستمر Aspose في العمل لكنه سيضيف علامة مائية “Evaluation” في الناتج. هذا غير مؤذٍ للاختبار لكنه غير مناسب للإنتاج.

## تعريف المناطق التي تريد التعرف عليها

الآن نقوم بإنشاء المستطيلات التي تمثل أجزاء الصورة التي نهتم بها. فكر في كل `Rectangle` كـ “صندوق قص” يخبر المحرك *أين* يبحث.

```java
        // Step 2: Create an OCR engine and set the default language
        OcrEngine engine = new OcrEngine();
        engine.setLanguage(Language.English);

        // Step 3: Define the regions (ROIs) you want to recognize
        // Header region (top part of the image)
        Rectangle header = new Rectangle(0, 0, 1200, 200);
        // Table body region (below the header)
        Rectangle table = new Rectangle(0, 210, 1200, 800);
```

لاحظ كيف استخدمنا مصطلح **perform OCR on ROI** ضمنيًا—كل `Rectangle` هو ROI. يمكنك تعديل الإحداثيات لتتناسب مع تخطيط مستندك. مستطيل `header` يلتقط الشريط العلوي، بينما مستطيل `table` يلتقط الجزء الأساسي حيث سنقوم لاحقًا بـ **recognize text in region**.

## إضافة المناطق وتعيين لغات لكل منطقة

يتيح لك Aspose OCR تعيين لغة لكل منطقة، وهو مثالي للمستندات متعددة اللغات. هنا نحتفظ بالإنجليزية للرأس ونحول إلى الفرنسية للجدول.

```java
        // Step 4: Add the regions to the engine
        engine.addRegion(header);                     // uses default language (English)
        engine.addRegion(table, Language.French);    // optional per‑region language
```

إذا كنت تحتاج لغة واحدة فقط، يمكنك حذف الوسيط الثاني. سيعود المحرك تلقائيًا إلى اللغة الافتراضية التي ضبطتها مسبقًا.

## إجراء OCR على ROI واسترجاع النص المدمج

أخيرًا، نقوم بتشغيل عملية OCR على الصورة بالكامل، لكن فقط الـ ROI المحددة سيتم معالجتها. النتيجة تجمع النص بالترتيب الذي أضفت به المناطق، مما يجعل ما بعد المعالجة بسيطًا.

```java
        // Step 5: Perform OCR on the image and retrieve the combined text
        OcrResult result = engine.recognizeImage("YOUR_DIRECTORY/invoice.png");
        System.out.println(result.getText()); // text from all defined regions in order
    }
}
```

**الناتج المتوقع** (مقتطع للاختصار):

```
Invoice #12345
Date: 2026‑06‑01
...
Produit   Quantité   Prix
Café      2          5,00 €
...
```

الكتلة الأولى تأتي من الرأس الإنجليزي، والثانية من الجدول الفرنسي—مثال كلاسيكي على **recognize text in region** مع لغات مختلطة.

## التعامل مع المشكلات الشائعة

حتى سير عمل **perform OCR on ROI** البسيط قد يواجه بعض العقبات الخفية. أدناه أكثر المشكلات شيوعًا وكيفية تجنبها.

### 1. أخطاء مسار الترخيص

إذا ألقى `setLicense` استثناء `FileNotFoundException`، تحقق مرة أخرى من المسار المطلق أو ضع ملف `.lic` في مجلد الموارد الخاص بالمشروع وحمّله باستخدام `getResourceAsStream`.

```java
License license = new License();
license.setLicense(RoiDemo.class.getResourceAsStream("/Aspose.OCR.lic"));
```

### 2. تداخل أو تجاوز حدود الـ ROI

Aspose لا يقتطع الـ ROI تلقائيًا إذا تجاوز أبعاد الصورة. المستطيلات المتداخلة قد تتسبب في تكرار النص. استخدم `engine.getImageSize()` للتحقق من الحدود قبل إنشاء المستطيلات.

```java
Size imgSize = engine.getImageSize("YOUR_DIRECTORY/invoice.png");
if (header.getRight() > imgSize.getWidth()) {
    // Adjust width to stay inside the image
    header.setWidth(imgSize.getWidth() - header.getX());
}
```

### 3. لغات غير مدعومة

محاولة تعيين لغة غير مدمجة مع المكتبة ستؤدي إلى رفع `UnsupportedOperationException`. التزم باللغات المذكورة في وثائق Aspose، أو حمّل حزم اللغات الإضافية.

### 4. صور منخفضة الدقة

دقة OCR تنخفض بشكل كبير تحت 100 dpi. إذا كان لديك مسح ضوئي منخفض الدقة، فكر في تكبيره باستخدام مكتبة مثل **Imgscalr** قبل تمريره إلى Aspose.

```java
BufferedImage src = ImageIO.read(new File("invoice.png"));
BufferedImage highRes = Scalr.resize(src, Scalr.Method.QUALITY, 300);
ImageIO.write(highRes, "png", new File("invoice_high.png"));
```

ثم وجه `recognizeImage` إلى `invoice_high.png`.

## توسيع المثال: عدة ROI واكتشاف ديناميكي

العرض التجريبي يستخدم مستطيلات ثابتة، لكن في سيناريوهات العالم الحقيقي قد ترغب في اكتشاف الجداول تلقائيًا. اجمع بين Aspose OCR ومكتبة **معالجة الصور** بسيطة (مثل OpenCV) لتحديد الحدود، ثم أدخل تلك الحدود إلى `engine.addRegion`. هذا يحول سكريبت **perform OCR on ROI** الثابت إلى خط أنابيب ديناميكي يعمل على أي تخطيط فاتورة.

```java
// Pseudo‑code: Detect contours → create Rectangle objects → addRegion()
List<Rect> detected = OpenCVHelper.findTables("invoice.png");
for (Rect r : detected) {
    engine.addRegion(new Rectangle(r.x, r.y, r.width, r.height), Language.French);
}
```

الآن يمكنك **recognize text in region** دون ترميز قيم البكسل يدويًا—مفيد للمعالجة الدفعية.

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل الجاهز للتنفيذ. استبدل `YOUR_DIRECTORY` بالمسار الفعلي على جهازك.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.geometry.*;

public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Apply license (optional for evaluation)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // Initialize engine with default language
        OcrEngine engine = new OcrEngine();
        engine.setLanguage(Language.English);

        // Define ROIs
        Rectangle header = new Rectangle(0, 0, 1200, 200);   // top banner
        Rectangle table  = new Rectangle(0, 210, 1200, 800); // body table

        // Add regions – per‑region language optional
        engine.addRegion(header);                     // English (default)
        engine.addRegion(table, Language.French);    // French for table

        // Run OCR on the image – only the defined ROIs are processed
        OcrResult result = engine.recognizeImage("YOUR_DIRECTORY/invoice.png");

        // Output combined text
        System.out.println("--- OCR Result ---");
        System.out.println(result.getText());
    }
}
```

شغّل `javac RoiDemo.java && java RoiDemo`. إذا تم إعداد كل شيء بشكل صحيح، ستظهر النصوص المدمجة من كلا المنطقتين مطبوعة في وحدة التحكم.

## الخلاصة

لقد غطينا للتو كيفية **perform OCR on ROI** في Java باستخدام Aspose OCR، والآن تعرف كيف تقوم بـ **recognize text in region** لكل من السيناريوهات أحادية اللغة ومتعددة اللغات. من خلال تقسيم الصورة إلى مستطيلات منطقية يمكنك:

1. تقليل وقت المعالجة،
2. خفض الإيجابيات الكاذبة،
3. الحصول على تحكم دقيق في اختيار اللغة.

من هنا قد تستكشف اكتشاف ROI الديناميكي، دمج النتائج في قاعدة بيانات، أو إنشاء ملفات PDF قابلة للبحث. السماء هي الحد—فقط تذكر التحقق من إحداثيات ROI، الحفاظ على مسار الترخيص منظمًا، واختيار حزم اللغات المناسبة.

هل لديك تخطيط معقد تواجه صعوبة معه؟ اترك تعليقًا أو أرسل طلب سحب (pull request) مع تحسيناتك. برمجة سعيدة، ولتكن OCR دائمًا دقيقة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}