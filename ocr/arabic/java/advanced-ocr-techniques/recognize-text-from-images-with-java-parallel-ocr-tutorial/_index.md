---
category: general
date: 2026-01-12
description: تعرّف على كيفية التعرف على النص من الصور واستخراج النص من ملفات PNG باستخدام
  Aspose OCR في Java. تجعل المعالجة المتوازية العملية سريعة.
draft: false
keywords:
- recognize text from images
- extract text from png
language: ar
og_description: اكتشف أسهل طريقة للتعرف على النص من الصور في جافا واستخراج النص من
  ملفات PNG باستخدام Aspose OCR مع المعالجة المتوازية.
og_title: التعرف على النص من الصور باستخدام جافا – دليل OCR المتوازي
tags:
- OCR
- Java
- Aspose
title: التعرف على النص من الصور باستخدام جافا – دليل OCR المتوازي
url: /ar/java/advanced-ocr-techniques/recognize-text-from-images-with-java-parallel-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصور باستخدام Java – دليل OCR المتوازي

هل احتجت يومًا إلى **التعرف على النص من الصور** لكن شعرت بالحيرة أمام سؤال “كيف أفعل ذلك؟”. لست وحدك. سواءً كنت تقوم برقمنة الفواتير، أو استخراج البيانات من لقطات الشاشة، أو بناء أرشيف قابل للبحث، فإن القدرة على *التعرف على النص من الصور* تُغيّر قواعد اللعبة.  

في هذا الدليل سنستعرض مثالًا كاملًا وجاهزًا للتنفيذ بلغة Java لا يقتصر فقط على **التعرف على النص من الصور** بل يوضح لك أيضًا كيفية **استخراج النص من ملفات png** باستخدام محرك Aspose OCR المتوازي المدمج. لا سكريبتات خارجية، ولا أجزاء مفقودة—فقط كود واضح وتفسيرات مبسطة.

## ما ستتعلمه

- إعداد Aspose OCR في مشروع Java  
- تمكين المعالجة المتوازية لتسريع وظائف الدُفعات  
- تحميل مجموعة من ملفات PNG و **استخراج النص من png** بكفاءة  
- التعامل مع المشكلات الشائعة (ملفات كبيرة، نتائج فارغة، حدود الخيوط)  
- مشاهدة الكود المصدري الكامل القابل للتنفيذ في نهاية المقال  

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من أن لديك:

| المتطلب | لماذا يهم |
|-------------|----------------|
| Java 8 أو أحدث | واجهة برمجة تطبيقات Aspose OCR للـ Java تستهدف Java 8+ |
| Maven أو Gradle (لإدارة الاعتمادات) | يبسط إضافة مكتبة Aspose OCR |
| بضع صور PNG تريد معالجتها | يستخدم الدليل `doc1.png`‑`doc4.png` كأمثلة |
| معرفة أساسية بتركيب Java | الكود بسيط، لكن سيتعين عليك تجميعه وتشغيله |

إذا كان أيٌ من هذه غير متوفر لديك, قم بتنزيل أحدث JDK من Oracle أو AdoptOpenJDK وأعد إعداد مشروع Maven بسيط—ليس هناك حاجة للتعقيد.

![recognize text from images diagram](image.png){alt="مخطط التعرف على النص من الصور"}

## الخطوة 1 – إضافة Aspose OCR إلى مشروعك

أولاً، أخبر Maven (أو Gradle) بسحب مكتبة Aspose OCR. في ملف `pom.xml`، أضف:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

إذا كنت تفضل Gradle، فإن المكافئ هو:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **نصيحة احترافية:** تحقق من [مستودع Aspose OCR Maven](https://repo.aspose.com/repo) للحصول على أحدث نسخة. الحفاظ على تحديث المكتبة يضمن حصولك على أحدث تحسينات OCR وإصلاحات الأخطاء.

## الخطوة 2 – تمكين المعالجة المتوازية (السر السحري)

يمكن لـ Aspose OCR توزيع عبء العمل عبر عدة نوى CPU. هذا هو السبب في أن عملية **التعرف على النص من الصور** تظل سريعة، حتى عندما يكون لديك العشرات من ملفات PNG.

```java
// Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Configure parallel options – up to 4 cores in this demo
ParallelOptions parallelOptions = new ParallelOptions();
parallelOptions.setMaxDegreeOfParallelism(4); // Adjust based on your machine
ocrEngine.setParallelOptions(parallelOptions);
```

لماذا نحدد حدًا؟ إن حجز عدد كبير من الخيوط قد يحرم العمليات الأخرى من الموارد، خاصةً على الخوادم المشتركة. أربعة نوى هو الإعداد الافتراضي الآمن لمعظم أجهزة الحاسوب المكتبية؛ يمكنك رفعه إذا كنت تعلم أن عتادك يتحمل المزيد.

## الخطوة 3 – إعداد قائمة ملفات PNG

يركّز الدليل على **استخراج النص من png**، لكن نفس الكود يعمل مع JPEG، BMP، إلخ. ضع صورك في مجلد وأشر إليها هكذا:

```java
String[] imageFiles = {
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
};
```

> **ملاحظة:** استبدل `YOUR_DIRECTORY` بالمسار المطلق أو النسبي حيث توجد ملفات PNG. إذا كنت بحاجة لمعالجة مجلد ديناميكي، يمكنك استخدام `Files.list(Paths.get("YOUR_DIRECTORY"))` لإنشاء المصفوفة تلقائيًا.

## الخطوة 4 – تشغيل OCR على كل صورة (المحرك يقوم بالعمل الشاق)

على الرغم من تمكيننا للمعالجة المتوازية، ما زلنا نكرر عبر مصفوفة الملفات. يقوم Aspose OCR داخليًا بتوزيع عمل التعرف عبر الخيوط التي قمنا بتكوينها.

```java
for (String imagePath : imageFiles) {
    // Load the image into the engine
    ocrEngine.setImage(imagePath);
    
    // Perform recognition
    OcrResult result = ocrEngine.recognize();
    
    // Guard against empty results
    String text = result.getText();
    if (text == null || text.isEmpty()) {
        System.out.println("[" + imagePath + "] => No text found.");
        continue;
    }
    
    // Print a short preview (first 50 characters)
    System.out.println("[" + imagePath + "] => " +
        text.substring(0, Math.min(50, text.length())) + "...");
}
```

### لماذا حلقة وليس تدفقًا متوازيًا؟

يقوم Aspose OCR بالفعل بتقسيم معالجة الصور داخليًا بناءً على `ParallelOptions`. تغليف الاستدعاء في تدفق متوازي خارجي سيؤدي إلى تغليف مزدوج للعمل وقد يضعف الأداء فعليًا. ثق بالمكتبة لإدارة الخيوط.

## الخطوة 5 – الحالات الخاصة والنصائح العملية

| الموقف | ما الذي يجب فعله |
|-----------|------------|
| **PNG كبير ( > 10 MB )** | زيادة حجم ذاكرة JVM (`-Xmx2g`) أو تغيير حجم الصورة قبل تمريرها إلى المحرك. |
| **تنسيقات صور مختلطة** | استخدم `ocrEngine.setImage(new File(imagePath))` – المحرك يكتشف التنسيق تلقائيًا. |
| **الحاجة إلى النص الكامل، وليس مجرد معاينة** | احفظ `result.getText()` في `StringBuilder` أو اكتبها إلى ملف للتحليل لاحقًا. |
| **التشغيل على خادم CI بدون واجهة رسومية** | لا خطوات إضافية—Aspose OCR يعمل بالكامل بدون واجهة. |
| **انتهاء صلاحية الترخيص** | سجِّل ترخيصًا مؤقتًا باستخدام `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` لتجنب علامات مائية للتقييم. |

## مثال كامل يعمل

فيما يلي الفئة الكاملة بلغة Java التي يمكنك نسخها، لصقها، وتشغيلها. تتضمن جميع الأجزاء التي ناقشناها، بالإضافة إلى بعض التعليقات للتوضيح.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.parallel.*;

public class ParallelOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create and initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing (up to 4 CPU cores)
        ParallelOptions parallelOptions = new ParallelOptions();
        parallelOptions.setMaxDegreeOfParallelism(4); // Adjust as needed
        ocrEngine.setParallelOptions(parallelOptions);

        // Step 3: Define the PNG files to be processed
        String[] imageFiles = {
            "YOUR_DIRECTORY/doc1.png",
            "YOUR_DIRECTORY/doc2.png",
            "YOUR_DIRECTORY/doc3.png",
            "YOUR_DIRECTORY/doc4.png"
        };

        // Step 4: Recognize text from each image (engine handles parallelism internally)
        for (String imagePath : imageFiles) {
            // Load the image
            ocrEngine.setImage(imagePath);

            // Perform OCR
            OcrResult result = ocrEngine.recognize();

            // Extract the recognized text
            String text = result.getText();

            // Guard against empty results
            if (text == null || text.isEmpty()) {
                System.out.println("[" + imagePath + "] => No text found.");
                continue;
            }

            // Step 5: Output a short preview (first 50 characters)
            System.out.println("[" + imagePath + "] => " +
                text.substring(0, Math.min(50, text.length())) + "...");
        }
    }
}
```

### النتيجة المتوقعة

إذا كان `doc1.png` يحتوي على العبارة “Invoice #12345 – Total $250.00”، فسترى شيئًا مثل:

```
[YOUR_DIRECTORY/doc1.png] => Invoice #12345 – Total $250.00...
[YOUR_DIRECTORY/doc2.png] => No text found.
[YOUR_DIRECTORY/doc3.png] => Customer Name: John Doe...
[YOUR_DIRECTORY/doc4.png] => ...
```

المعاينة تقص النص عند 50 حرفًا، لكن السلسلة الكاملة موجودة داخل `result.getText()` لأي معالجة لاحقة تحتاجها.

## الخاتمة

أصبح لديك الآن نمط قوي وجاهز للإنتاج **للتعرف على النص من الصور** باستخدام Aspose OCR في Java، وقد رأيت بالضبط كيفية **استخراج النص من png** مع تسريع متوازي. تم تغطية الخطوات الأساسية—إعداد المحرك، تكوين المعالجة المتوازية، إعداد قائمة الصور، ومعالجة النتائج—بالإضافة إلى مجموعة من النصائح العملية لتجنب المشكلات الشائعة.

ما التالي؟ جرّب استبدال قائمة PNG بمسح دليل ديناميكي، أو صلّ مخرجات OCR إلى فهرس بحث مثل Elasticsearch، أو جرّب إعدادات OCR الخاصة باللغات (`ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH)`). السماء هي الحد عندما تتقن سير العمل الأساسي.

إذا واجهت أي مشاكل أو لديك أفكار لتوسيع هذا الدليل، اترك تعليقًا أدناه. برمجة سعيدة، واستمتع بتحويل تلك الصور العنيدة إلى نص قابل للبحث!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}